# Plunk (plunk)

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
