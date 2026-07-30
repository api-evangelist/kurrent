---
name: kurrent-persistent-subscriptions
description: >-
  Use when consuming a KurrentDB stream through a server-managed competing-consumer group over the
  HTTP API — creating the subscription, reading events, acknowledging and negatively acknowledging
  messages, and replaying parked messages. NOT for catch-up subscriptions, which are an SDK concern.
api: openapi/kurrent-kurrentdb-http-api-openapi.yml
operations:
  - createSubscription
  - updateSubscription
  - deleteSubscription
  - listSubscriptions
  - listSubscriptionsForStream
  - getSubscriptionInfo
  - readSubscription
  - readSubscriptionEvents
  - ackMessage
  - ackMessages
  - nackMessage
  - nackMessages
  - replayParkedMessages
---

# Consume a KurrentDB stream with a persistent subscription

A persistent subscription is a *server-managed* competing-consumer group. KurrentDB tracks the
checkpoint, hands each message to one consumer, and retries or parks messages you do not
acknowledge. This is the opposite of a catch-up subscription, where the client owns the position.

Use a persistent subscription when several workers share the load and you want at-least-once
delivery with server-side retry. Use a catch-up subscription when one consumer needs ordered,
replayable delivery it controls.

## Create the group

Call `createSubscription` — `PUT /subscriptions/{stream}/{subscription}`. The settings body is where
the delivery semantics live. The ones that matter most:

- `startFrom` — the event number to begin at. Omit to start from the current head.
- `messageTimeoutMilliseconds` — how long a consumer has before the message is redelivered.
- `maxRetryCount` — how many redeliveries before the message is **parked**.
- `maxSubscriberCount` — caps concurrent consumers.
- `readBatchSize`, `bufferSize`, `liveBufferSize` — throughput tuning.
- `checkPointAfterMilliseconds`, `minCheckPointCount`, `maxCheckPointCount` — how often the group's
  position is persisted.
- `namedConsumerStrategy` — how messages are distributed across consumers.
- `resolveLinktos` — set true when subscribing to a projection-built stream of link events so you
  receive the linked-to originals rather than the links.

`updateSubscription` (`POST` on the same path) changes settings on a live group;
`deleteSubscription` removes it. `listSubscriptions`, `listSubscriptionsForStream` and
`getSubscriptionInfo` give you the inventory and the live stats.

## Consume

`readSubscription` — `GET /subscriptions/{stream}/{subscription}` — pulls the next available
messages. `readSubscriptionEvents` — `GET /subscriptions/{stream}/{subscription}/{count}` — pulls a
bounded batch, which is what you want in a worker loop.

## Acknowledge — this is the part people get wrong

Every message you read must be settled, positively or negatively, before
`messageTimeoutMilliseconds` elapses. If you do not settle it, KurrentDB redelivers it, and after
`maxRetryCount` redeliveries it is parked.

- `ackMessage` — `POST .../ack/{messageid}` settles one message.
- `ackMessages` — `POST .../ack?ids=...` settles a batch. Prefer this in a worker loop.
- `nackMessage` / `nackMessages` — negatively acknowledge, with an `action` query parameter:
  - `Retry` — put it back for another attempt. Use for transient failures.
  - `Park` — move it to the parked-messages stream immediately. Use for poison messages you want a
    human to look at.
  - `Skip` — drop it. Use only when the message is genuinely irrelevant.
  - `Stop` — stop the subscription.

Choose deliberately. Nacking everything with `Retry` on a permanent failure turns a poison message
into an infinite loop until `maxRetryCount` parks it anyway.

## Recover parked messages

`replayParkedMessages` — `POST /subscriptions/{stream}/{subscription}/replayParked` — pushes the
parked messages back into the group. Fix the defect first; replaying into the same bug just re-parks
them.

## Design notes

- Delivery is **at-least-once**, not exactly-once. Make your handler idempotent — key it on the
  event id, which KurrentDB carries on every event.
- Ordering is not guaranteed across competing consumers. If you need strict per-entity ordering, run
  one consumer, or partition by stream.
- A 401 here means credentials or the stream ACL, same as everywhere else in this API.
