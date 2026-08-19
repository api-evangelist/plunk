---
name: Track an event and upsert a contact in Plunk
description: Record an application event against a contact from client-side or server-side code, creating the contact if it does not exist and triggering any matching Plunk workflow.
api: openapi/_original/plunk-api-openapi.json
operations: [trackEvent, createContact, getContact, listContacts]
base_url: https://next-api.useplunk.com
---

# Track an event and upsert a contact in Plunk

`POST /v1/track` is the only Plunk endpoint designed to be called from a browser or mobile app, and the only
one that requires the **public** key. It does three things at once: it records the event, it creates or
updates the contact, and it fires any workflow whose trigger matches the event name.

## Key class — get this right first

- `/v1/track` requires the **public key** (`pk_*`). A secret key is rejected with `401 INVALID_API_KEY`.
- Every other endpoint in this skill requires the **secret key** (`sk_*`) and must run server-side.

The two are not interchangeable in either direction. The project is derived from the key itself — there is no
project ID parameter on any request.

## Steps

1. **Track the event.** `POST /v1/track` with `Authorization: Bearer pk_...`:
   - `email` — the contact. Created if it does not exist.
   - `event` — your event name, e.g. `signed_up`, `order.completed`. This is the string a workflow trigger matches on.
   - `data` (optional) — arbitrary JSON merged onto the contact's `data` object and carried into any webhook that forwards this event.

2. **Set an `Idempotency-Key`.** `/v1/track` accepts one, same contract as `/v1/send`: project-scoped,
   24h TTL, reuse returns `409 IDEMPOTENCY_KEY_REUSED` rather than replaying. Use it whenever the event is
   derived from something that must count once — a purchase, a signup, a form submission.

3. **Read the wrapped envelope.** `{"success": true, "data": {contact, event, timestamp}}`.

4. **Enrich server-side if needed.** `POST /contacts` (secret key) is a full upsert keyed on email, and
   returns `_meta.isNew` / `_meta.isUpdate` so you can tell which happened. Use it when you want to set
   `subscribed` or write a larger `data` payload than a client should be trusted with.

5. **Read a contact back** with `GET /contacts/{id}` (`getContact`), or find one with `GET /contacts` and the
   `search` parameter (email substring), `limit` and `cursor`. Note these dashboard routes return the resource
   **directly** — no `success`/`data` wrapper.

## Choosing event names

Event names become the vocabulary for the whole automation layer, so pick them once and keep them stable:

- Workflow triggers match on the exact event name.
- Segment filters can test whether an event fired, and within what window.
- `GET /events/names` lists every distinct name in the project; `GET /events/{eventName}/usage` shows every
  segment filter, workflow trigger and condition that references it — check this before renaming or deleting.
- `DELETE /events/{eventName}` removes every event with that name from the project. It is not reversible.

## Custom data and segmentation

Anything you pass in `data` lands on the contact's open `data` object and becomes available as `{{key}}` in
templates and webhooks. `GET /contacts/fields` reports every standard and custom field with its inferred type
and the percentage of contacts that carry it — use it to check a field is populated widely enough to segment
on before building a filter over it.

## Errors

| Status | Code | Meaning |
|---|---|---|
| `401` | `INVALID_API_KEY` | You used `sk_` on `/v1/track`, or `pk_` on a contacts route. |
| `422` | `VALIDATION_ERROR` | Missing `email` or `event`. `error.errors[]` names the field. |
| `409` | `IDEMPOTENCY_KEY_REUSED` | The event was not recorded twice. |
| `409` | `CONFLICT` | On `PATCH /contacts/{id}`, the target email already belongs to another contact. |
| `404` | `CONTACT_NOT_FOUND` | The contact ID does not exist in this project. |
| `429` | `RATE_LIMIT_EXCEEDED` | 1000 req/min per project. Back off exponentially; no `Retry-After` header is returned. |

## Safety note for client-side use

The public key is safe to ship in browser code, but it is not secret — treat it as semi-sensitive and rotate
it if your tracking endpoint is being abused. Rotation regenerates **both** keys at once with no grace period,
so plan a deployment window. Use separate Plunk projects for staging and production.

## References

- Operations: `trackEvent`, `createContact`, `getContact`, `listContacts` in `openapi/_original/plunk-api-openapi.json`
- https://docs.useplunk.com/api-reference/public-api/trackEvent
- https://docs.useplunk.com/guides/api-keys
- https://docs.useplunk.com/guides/custom-fields
