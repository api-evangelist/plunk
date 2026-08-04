# Plunk (plunk)

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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Plunk is an open-source (AGPL-3.0) email platform for SaaS that unifies transactional email, marketing campaigns, and event-driven automations behind a single REST API. The hosted service runs at api.useplunk.com with Bearer secret / public API keys, and the entire stack can be self-hosted with Docker Compose for full data ownership and no per-email costs.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/plunk/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/plunk/refs/heads/main/apis.yml)

## Tags

- Email
- Transactional Email
- Marketing
- Automation
- Open Source
- SaaS

## Timestamps

- **Created:** 2026-06-20
- **Modified:** 2026-06-20

## APIs

### Plunk Send (Transactional) API

Send a single transactional email (HTML or plain-text body) authenticated with a secret API key, with optional sender, reply-to, custom headers, and attachments.

- **Human URL:** [https://docs.useplunk.com/api-reference/transactional/send](https://docs.useplunk.com/api-reference/transactional/send)
- **Base URL:** `https://api.useplunk.com/v1`

#### Tags

- Email
- Transactional
- Send

#### Properties

- [Documentation](https://docs.useplunk.com/api-reference/transactional/send)
- [API Reference](https://docs.useplunk.com/api-reference/overview)
- [OpenAPI](openapi/plunk-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/plunk.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/plunk.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [GitHub](https://github.com/useplunk/plunk)

### Plunk Track (Events) API

Publish a named contact event that creates or updates the contact and triggers any matching automation. Callable with a public (pk_) key for safe client-side tracking, optionally carrying subscription status and metadata.

- **Human URL:** [https://docs.useplunk.com/api-reference/transactional/track](https://docs.useplunk.com/api-reference/transactional/track)
- **Base URL:** `https://api.useplunk.com/v1`

#### Tags

- Events
- Tracking
- Automation

#### Properties

- [Documentation](https://docs.useplunk.com/api-reference/transactional/track)
- [API Reference](https://docs.useplunk.com/api-reference/overview)
- [OpenAPI](openapi/plunk-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/plunk.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/plunk.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [GitHub](https://github.com/useplunk/plunk)

### Plunk Contacts API

Create, retrieve, update, count, and delete contacts, and manage subscription state with explicit subscribe / unsubscribe operations. Contacts carry arbitrary metadata used for segmentation and personalization.

- **Human URL:** [https://docs.useplunk.com/api-reference/contacts/create](https://docs.useplunk.com/api-reference/contacts/create)
- **Base URL:** `https://api.useplunk.com/v1`

#### Tags

- Contacts
- Subscribers
- Audience

#### Properties

- [Documentation](https://docs.useplunk.com/api-reference/contacts/create)
- [API Reference](https://docs.useplunk.com/api-reference/overview)
- [OpenAPI](openapi/plunk-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/plunk.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/plunk.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [GitHub](https://github.com/useplunk/plunk)

### Plunk Campaigns API

Create, update, delete, and send one-off marketing campaigns to a list of recipients or audience segments, with HTML body and styling controls.

- **Human URL:** [https://docs.useplunk.com/api-reference/campaigns/create](https://docs.useplunk.com/api-reference/campaigns/create)
- **Base URL:** `https://api.useplunk.com/v1`

#### Tags

- Campaigns
- Marketing
- Broadcast

#### Properties

- [Documentation](https://docs.useplunk.com/api-reference/campaigns/create)
- [API Reference](https://docs.useplunk.com/api-reference/overview)
- [OpenAPI](openapi/plunk-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/plunk.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/plunk.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [GitHub](https://github.com/useplunk/plunk)

## Common Properties

- [GitHub Organization](https://github.com/useplunk)
- [LinkedIn](https://www.linkedin.com/company/useplunk)
- [Website](https://www.useplunk.com)
- [Documentation](https://docs.useplunk.com)
- [Plans](plans/plunk-plans-pricing.yml)
- [Rate Limits](rate-limits/plunk-rate-limits.yml)
- [Fin Ops](finops/plunk-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
