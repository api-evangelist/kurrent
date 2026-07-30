---
name: kurrent-append-and-read-stream
description: >-
  Use when writing events to a KurrentDB stream and reading them back over the HTTP API, including
  optimistic concurrency with expected version and safe retries using the event id. NOT for the
  gRPC client SDKs (use Kurrent's own kurrent-docs skill) or for projections.
api: openapi/kurrent-kurrentdb-http-api-openapi.yml
operations:
  - appendToStream
  - appendEventToStreamIdempotent
  - readStream
  - readEventsBackward
  - readEventsForward
  - readEvent
  - readStreamMetadata
  - updateStreamMetadata
---

# Append events to a KurrentDB stream and read them back

KurrentDB is an append-only event log. You never update an event and you never overwrite a stream —
you append a new event and read the stream forward or backward to reconstruct state.

## Before you start

- The base URL is the KurrentDB node or Kurrent Cloud cluster itself, on port 2113 by default. It is
  the same URL you use for the admin UI. There is no shared multi-tenant host.
- AtomPub over HTTP must be enabled on the server (`--enable-atom-pub-over-http`). If reads return
  404 on a stream you know exists, check this first.
- Authenticate with HTTP Basic. Authorization is per-stream ACLs, so a 401 can mean "wrong password"
  *or* "this user is not in the stream's `$acl`".
- Name streams `category-identifier` (for example `order-1234`). The standard by-category projection
  splits on the first dash.

## Append an event

Call `appendToStream` — `POST /streams/{stream}`.

Always set these headers:

- `Kurrent-EventType` — the event type name, for example `OrderPlaced`. Names beginning with `$` are
  reserved for system events.
- `Kurrent-EventId` — a UUID you generate on the client. **This is the idempotency key.** KurrentDB
  deduplicates on it within the target stream, so if the request times out you retry the identical
  request rather than guessing whether it landed.
- `Kurrent-ExpectedVersion` — the event number you expect the stream to already be at. This is
  optimistic concurrency control.

If you prefer to carry the id in the URL rather than a header, call
`appendEventToStreamIdempotent` — `POST /streams/{stream}/incoming/{guid}` — which does the same
thing with the UUID as a path segment.

A `201 Created` means the event is durable. A `307 Temporary Redirect` means you reached a follower
node; follow the `Location` header, or set `Kurrent-RequireLeader: true` and let the node route it.

## Handle the concurrency conflict

A `400 Bad Request` on an append usually means the expected version did not match — someone else
appended first. **Do not blind-retry with the same expected version.** The correct loop is:

1. Read the stream from the version you last saw.
2. Re-apply your business decision to the events you had not seen. The decision may no longer be
   valid — that is the point of the check.
3. Append again with the new expected version, reusing a *fresh* event id if the event content
   changed and the *same* event id only if you are retrying the byte-identical write.

## Read the stream back

- `readStream` — `GET /streams/{stream}` returns the head of the stream as an AtomPub feed.
- `readEventsBackward` — `GET /streams/{stream}/{event}/backward/{count}` walks toward older events.
- `readEventsForward` — `GET /streams/{stream}/{event}/forward/{count}` walks toward newer events.
- `readEvent` — `GET /streams/{stream}/{event}` returns one event; `head` is a valid event number.

Page by following the feed's link relations (`first`, `last`, `previous`, `next`) rather than by
computing offsets. To rebuild an aggregate, start at event `0` and read `forward` until the feed
stops returning a `previous` link. Pages other than the head are permanently cacheable, because the
log is immutable.

## Retention and access

`readStreamMetadata` and `updateStreamMetadata` — `GET`/`POST /streams/{stream}/metadata` — control
`$maxCount` and `$maxAge` (retention), `$cacheControl`, `$tb` (truncate-before) and `$acl`
(permissions). Setting retention does not free disk space on its own; a scavenge does.

## Errors you will actually hit

| Status | Meaning | Do this |
|---|---|---|
| 400 | Expected-version conflict, or malformed request | Re-read, re-decide, retry with the new version |
| 401 | Bad credentials, or user not in the stream `$acl` | Fix credentials, then check `$acl` and the `$settings` default |
| 404 | Stream, event or feed page does not exist — or the stream was hard-deleted | A soft-deleted stream can be appended to again; a tombstoned one never can |
| 307 | You reached a follower | Follow `Location`, or set `Kurrent-RequireLeader` |

The gRPC surface returns a far richer typed error model — see `errors/kurrent-error-codes.yml` for
`StreamRevisionConflictErrorDetails`, `StreamTombstonedErrorDetails` and the rest.
