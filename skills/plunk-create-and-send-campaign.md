---
name: Create and send a Plunk campaign to a segment
description: Build an audience segment, create a campaign against it, test it, then send or schedule it — with the confirmation and cost checks a broadcast deserves.
api: openapi/_original/plunk-api-openapi.json
operations: [createSegment, listSegments, createTemplate, listTemplates, createCampaign, listCampaigns, sendCampaign]
base_url: https://next-api.useplunk.com
---

# Create and send a Plunk campaign to a segment

**This is the highest-consequence flow in the Plunk API.** `sendCampaign` mails an entire audience and bills
1 credit per recipient. It is not reversible once the campaign reaches `SENDING`, and it accepts **no
idempotency key**. Confirm with a human before the final step.

All operations here require the **secret key** (`sk_*`) and return the resource **directly** — these are
dashboard routes, so there is no `{"success": true, "data": ...}` wrapper.

## Steps

1. **Confirm the sending domain.** The campaign's `from` address must be on a verified domain, or creation
   fails with `403`. List them with `GET /domains/project/{projectId}`.

2. **Pick or build the audience.**
   - `listSegments` (`GET /segments`) — returns every segment as one small unpaginated list, each with a
     cached `memberCount`.
   - `createSegment` (`POST /segments`) — `type: "DYNAMIC"` **requires** `condition`; `type: "STATIC"`
     **rejects** it. A dynamic segment is a live filter; a static segment is an explicit list you add emails to
     with `POST /segments/{id}/members`.
   - Check the real size before you commit: `GET /segments/{id}/contacts` is page-based (`page`, `pageSize`,
     max 100) and is live for dynamic segments. `POST /segments/{id}/refresh` does a cheap count refresh
     without firing membership events.

3. **Prepare the content.** Either inline `subject` + `body`, or `createTemplate` / `listTemplates` and
   reference one. Template `type` matters:
   - `MARKETING` — Plunk auto-injects a localized unsubscribe footer.
   - `HEADLESS` — no footer; **you must include `{{unsubscribeUrl}}` or `{{manageUrl}}` yourself**, or
     recipients have no way to opt out.
   - `TRANSACTIONAL` — skips subscription checks; wrong choice for a broadcast.

4. **Create the campaign.** `createCampaign` (`POST /campaigns`) creates it in `DRAFT`. Two independent fields
   control different things and are easy to confuse:
   - `type` — the content class (`TRANSACTIONAL` / `MARKETING` / `HEADLESS`), which drives the footer.
   - `audienceType` — who receives it (`ALL` / `SEGMENT` / `FILTERED`). Set `segmentId` when `SEGMENT`,
     `audienceCondition` when `FILTERED`.

5. **Test it.** `POST /campaigns/{id}/test` with `{ "email": "you@example.com" }` sends a single test copy.
   Do this before every send. It costs one credit; a wrong broadcast costs the whole audience.

6. **Confirm cost and audience with a human.** Recipients × 1 credit (× 2 if the email carries attachments).
   Check the per-category **Campaigns** cap under `GET /users/@me/projects/{id}/billing-limits` and current
   usage under `.../billing-consumption` — exceeding a cap returns `402 BILLING_LIMIT_EXCEEDED` mid-flight.

7. **Send or schedule.** `sendCampaign` (`POST /campaigns/{id}/send`). Pass `scheduledFor` (ISO 8601) to
   schedule rather than send now — scheduling is the safer default, because it leaves a cancellation window.

8. **Watch it.** `GET /campaigns/{id}/stats` returns send / open / click / bounce counts.
   `POST /campaigns/{id}/cancel` stops a campaign that is still `SCHEDULED` or `SENDING`.

## Status machine

`DRAFT` → `SCHEDULED` → `SENDING` → `SENT`, with `CANCELLED` reachable from `SCHEDULED` and `SENDING`.
`DELETE /campaigns/{id}` returns `409` while active executions exist.

## Errors

| Status | Code | Meaning |
|---|---|---|
| `400` | *(flat `{"error": "..."}`)* | `POST /campaigns` and `POST /segments` return a **bare error string**, not the standard envelope, for missing required fields. Branch on shape. |
| `403` | `FORBIDDEN` | The `from` address is not on a verified domain, or the project is disabled. |
| `422` | `VALIDATION_ERROR` | Field-level detail in `error.errors[]` — commonly a `DYNAMIC` segment with no `condition`. |
| `404` | `CAMPAIGN_NOT_FOUND` | Wrong ID, or the campaign belongs to another project. |
| `409` | `CONFLICT` | Deleting a campaign with active executions, or a segment used by an active campaign. |
| `402` | `BILLING_LIMIT_EXCEEDED` | The Campaigns category cap or the plan allowance was hit. |

## References

- Operations: `createSegment`, `listSegments`, `createTemplate`, `listTemplates`, `createCampaign`,
  `listCampaigns`, `sendCampaign` in `openapi/_original/plunk-api-openapi.json`
- https://docs.useplunk.com/api-reference/campaigns/sendCampaign
- https://docs.useplunk.com/guides/segment-filters
- https://docs.useplunk.com/guides/unsubscribe-pages
- `data-model/plunk-data-model.yml`, `errors/plunk-problem-types.yml`
