# Kurrent

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Kurrent — formerly Event Store Ltd — builds KurrentDB, an event-native database purpose-built to store, process and deliver application state changes as an immutable, append-only log of events. Where a traditional CRUD database overwrites rows and discards the history that produced them, KurrentDB retains every state change as a first-class event, giving applications a complete audit trail, temporal queries and the ability to replay history to rebuild state or seed new read models. The product line spans KurrentDB (open-source and commercial, self-hosted), Kurrent Cloud (managed clusters on AWS, Azure and Google Cloud), Kurrent Enterprise, and Capacitor, a shared memory layer for agentic coding. Developers integrate over a primary gRPC protocol with official client SDKs for .NET, Java, Node.js, Python, Go and Rust, or over the native AtomPub-style HTTP API. Connectors move events in and out of Kafka, MongoDB, Elasticsearch, RabbitMQ, Pulsar, SQL and HTTP endpoints. KurrentDB is widely used for event sourcing, CQRS, event-driven microservices, change data capture and, increasingly, as durable memory for AI agents.

**Areas:** Company · Database · Event Sourcing · Event Streaming · Event-Driven Architecture · CQRS · Data Infrastructure · Developer Tools · Cloud · Open Source · gRPC · AI Agents

## Kurrent on APIs.io

Everything profiled for Kurrent is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/kurrent/](https://apis.io/providers/kurrent/)** — or go straight to one of the APIs or properties below.

### APIs (9)

- [KurrentDB gRPC API](https://apis.io/apis/kurrent/kurrentdb-grpc-api/) — The primary protocol for KurrentDB. The published protocol buffer definitions cover the v2 streams service (multi-stream appends, reads), the schema…
- [Kurrent Admin API](https://apis.io/apis/kurrent/kurrent-admin-api/) — Node administration operations
- [Kurrent Gossip API](https://apis.io/apis/kurrent/kurrent-gossip-api/) — Cluster gossip
- [Kurrent Info API](https://apis.io/apis/kurrent/kurrent-info-api/) — Node information and configuration
- [Kurrent Projections API](https://apis.io/apis/kurrent/kurrent-projections-api/) — Create, manage and query projections
- [Kurrent Statistics API](https://apis.io/apis/kurrent/kurrent-statistics-api/) — Node statistics
- [Kurrent Streams API](https://apis.io/apis/kurrent/kurrent-streams-api/) — Append to, read from and manage event streams
- [Kurrent Subscriptions API](https://apis.io/apis/kurrent/kurrent-subscriptions-api/) — Persistent (competing consumer) subscription management and consumption
- [Kurrent Users API](https://apis.io/apis/kurrent/kurrent-users-api/) — User account management

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Kurrent Connectors Webhooks](https://apis.io/asyncapis/kurrent/kurrent-connectors-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [KurrentDB](https://apis.io/servers/kurrent/kurrentdb/)

#### Collections (16)

Postman and Open Collection request collections.

- [KurrentDB HTTP Admin API](https://apis.io/collections/kurrent/open-kurrent-admin-api/)
- [KurrentDB HTTP Admin Gossip API](https://apis.io/collections/kurrent/open-kurrent-gossip-api/)
- [KurrentDB HTTP Admin Info API](https://apis.io/collections/kurrent/open-kurrent-info-api/)
- [KurrentDB HTTP Admin Projections API](https://apis.io/collections/kurrent/open-kurrent-projections-api/)
- [KurrentDB HTTP Admin Statistics API](https://apis.io/collections/kurrent/open-kurrent-statistics-api/)
- [KurrentDB HTTP Admin Streams API](https://apis.io/collections/kurrent/open-kurrent-streams-api/)
- [KurrentDB HTTP Admin Subscriptions API](https://apis.io/collections/kurrent/open-kurrent-subscriptions-api/)
- [KurrentDB HTTP Admin Users API](https://apis.io/collections/kurrent/open-kurrent-users-api/)
- [KurrentDB HTTP Admin API](https://apis.io/collections/kurrent/postman-kurrent-admin-api/)
- [KurrentDB HTTP Admin Gossip API](https://apis.io/collections/kurrent/postman-kurrent-gossip-api/)
- [KurrentDB HTTP Admin Info API](https://apis.io/collections/kurrent/postman-kurrent-info-api/)
- [KurrentDB HTTP Admin Projections API](https://apis.io/collections/kurrent/postman-kurrent-projections-api/)
- [KurrentDB HTTP Admin Statistics API](https://apis.io/collections/kurrent/postman-kurrent-statistics-api/)
- [KurrentDB HTTP Admin Streams API](https://apis.io/collections/kurrent/postman-kurrent-streams-api/)
- [KurrentDB HTTP Admin Subscriptions API](https://apis.io/collections/kurrent/postman-kurrent-subscriptions-api/)
- [KurrentDB HTTP Admin Users API](https://apis.io/collections/kurrent/postman-kurrent-users-api/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Kurrent Kurrentdb Http Api Overlay](https://apis.io/overlays/kurrent/kurrent-kurrentdb-http-api-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Kurrent Authentication](https://apis.io/security/kurrent/kurrent-authentication/)
- [Kurrent Domain Security](https://apis.io/security/kurrent/kurrent-domain-security/)
- [Kurrent Trust Center](https://apis.io/security/kurrent/kurrent-trust-center/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Kurrent Scopes](https://apis.io/scopes/kurrent/kurrent-scopes/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.kurrent.io/)
- [Documentation](https://docs.kurrent.io/)
- [Getting started](https://docs.kurrent.io/getting-started/quickstart/)
- [API reference](https://docs.kurrent.io/server/v26.1/http-api/api.html)
- [Pricing](https://www.kurrent.io/pricing)
- [Sign up](https://identity.eventstore.com/login)
- [Support](https://eventstore.freshdesk.com/support/login)
- [Changelog](https://www.kurrent.io/releases)
- [Blog](https://www.kurrent.io/blog)
- [Trust centre](https://trust.kurrent.io/)
- [Terms of service](https://www.kurrent.io/terms-of-use)
- [Privacy policy](https://www.kurrent.io/privacy-policy)
- [GitHub](https://github.com/kurrent-io)
- [Status](https://status.eventstore.cloud/)

## API Evangelist rating

**Kin Score 46.8** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 71.7 |
| Contract quality | 21.4 |
| Contract governance | 4.5 |
| Operational transparency | 50.0 |
| Developer ergonomics | 86.9 |
| Access clarity | 38.2 |

**Agent readiness 46.5** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | documented (partial credit) |
| Auth Clarity | served (partial credit) |
| Idempotency | documented (partial credit) |
| Error Semantics | derived (partial credit) |
| OpenAPI Examples | — |
| Rate Limit Signal | — |
| Event Surface Described | yes |
| Agent Skills | yes |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | — |
| Dynamic Client Registration | yes |
| Agentic Commerce | — |
| Pagination Ratio | paginated |
| Operation Distinctiveness | distinct |

**Regulatory alignment 34.3** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/kurrent/](https://apis.io/providers/kurrent/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Kurrent: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/kurrent/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
