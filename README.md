# Plunk

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

Plunk is an open-source (AGPL-3.0) email platform for developers that unifies transactional email, marketing campaigns, contact segmentation and event-driven workflow automation behind a single REST API. It publishes its own OpenAPI 3.1.0 at docs.useplunk.com/openapi.json, declaring next-api.useplunk.com as the production base URL, and authenticates with a two-class Bearer API key where the prefix decides capability — sk_ for every endpoint and pk_ for the client-safe /v1/track tracking call. The API supports Idempotency-Key on both public write endpoints, cursor pagination, a structured error envelope carrying machine codes plus remediation hints, and a documented webhook event catalogue delivered as workflow steps. Every documentation page is also served as Markdown. The entire stack self-hosts with Docker Compose for full data ownership and no per-email costs.

**Areas:** Email · Transactional Email · Marketing · Automation · Open Source · Software-as-a-Service · Email API · Webhook · Segmentation · Workflow Automation · Self-Hosted · Developer Tools

## Plunk on APIs.io

Everything profiled for Plunk is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/plunk/](https://apis.io/providers/plunk/)** — or go straight to one of the APIs or properties below.

### APIs (7)

- [Plunk Campaigns API](https://apis.io/apis/plunk/plunk-campaigns-api/) — Create and send marketing campaigns.
- [Plunk Contacts API](https://apis.io/apis/plunk/plunk-contacts-api/) — Manage contacts and their subscription state.
- [Plunk Events API](https://apis.io/apis/plunk/plunk-events-api/) — Track contact events that drive automations.
- [Plunk Transactional API](https://apis.io/apis/plunk/plunk-transactional-api/) — Send transactional email.
- [Plunk Public API](https://apis.io/apis/plunk/plunk-public-api-api/) — Public API endpoints for sending emails and tracking events
- [Plunk Segments API](https://apis.io/apis/plunk/plunk-segments-api/) — Audience segmentation
- [Plunk Templates API](https://apis.io/apis/plunk/plunk-templates-api/) — Email template management

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Plunk Webhooks](https://apis.io/asyncapis/plunk/plunk-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [plunk-mcp.yml](https://apis.io/servers/plunk/plunk-mcp-yml/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Plunk Agentic Access](https://apis.io/agentic-access/plunk/plunk-agentic-access/)

#### Collections (5)

Postman and Open Collection request collections.

- [Plunk API](https://apis.io/collections/plunk/open-plunk/)
- [Plunk Campaigns API](https://apis.io/collections/plunk/open-plunk-campaigns-api/)
- [Plunk Campaigns Contacts API](https://apis.io/collections/plunk/open-plunk-contacts-api/)
- [Plunk Campaigns Events API](https://apis.io/collections/plunk/open-plunk-events-api/)
- [Plunk Campaigns Transactional API](https://apis.io/collections/plunk/open-plunk-transactional-api/)

#### Overlays (8)

OpenAPI overlays, including conversational phrasing for each operation.

- [Plunk Api Overlay](https://apis.io/overlays/plunk/plunk-api-overlay/)
- [Plunk Campaigns Api Phrasing Overlay](https://apis.io/overlays/plunk/plunk-campaigns-api-phrasing-overlay/)
- [Plunk Contacts Api Phrasing Overlay](https://apis.io/overlays/plunk/plunk-contacts-api-phrasing-overlay/)
- [Plunk Events Api Phrasing Overlay](https://apis.io/overlays/plunk/plunk-events-api-phrasing-overlay/)
- [Plunk Public Api Api Phrasing Overlay](https://apis.io/overlays/plunk/plunk-public-api-api-phrasing-overlay/)
- [Plunk Segments Api Phrasing Overlay](https://apis.io/overlays/plunk/plunk-segments-api-phrasing-overlay/)
- [Plunk Templates Api Phrasing Overlay](https://apis.io/overlays/plunk/plunk-templates-api-phrasing-overlay/)
- [Plunk Transactional Api Phrasing Overlay](https://apis.io/overlays/plunk/plunk-transactional-api-phrasing-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Plunk Authentication](https://apis.io/security/plunk/plunk-authentication/)
- [Plunk Domain Security](https://apis.io/security/plunk/plunk-domain-security/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Plunk Plans Pricing](https://apis.io/plans/plunk/plunk-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Plunk Rate Limits](https://apis.io/rate-limits/plunk/plunk-rate-limits/)

#### FinOps (1)

What the API costs to run, by operation.

- [Plunk Finops](https://apis.io/finops/plunk/plunk-finops/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.useplunk.com)
- [Documentation](https://docs.useplunk.com)
- [Getting started](https://docs.useplunk.com)
- [API reference](https://docs.useplunk.com/api-reference/overview)
- [Pricing](https://www.useplunk.com/pricing)
- [Sign up](https://next-app.useplunk.com/auth/signup)
- [Support](https://www.useplunk.com/discord)
- [Compliance](https://www.useplunk.com/dpa)
- [Terms of service](https://www.useplunk.com/terms)
- [Privacy policy](https://www.useplunk.com/privacy)
- [GitHub](https://github.com/useplunk)
- [Status](https://status.useplunk.com)

## API Evangelist rating

**Kin Score 73.6** — exemplar · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 73.2 |
| Contract quality | 64.2 |
| Contract governance | 18.2 |
| Operational transparency | 73.7 |
| Developer ergonomics | 64.9 |
| Access clarity | 84.2 |

**Agent readiness 41.7** — agent-native

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | verified |
| Error Semantics | verified |
| OpenAPI Examples | verified |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | partial |
| Operation Distinctiveness | — |

**Regulatory alignment 29.4** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/plunk/](https://apis.io/providers/plunk/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Plunk: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/plunk/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
