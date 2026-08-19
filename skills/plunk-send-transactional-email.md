---
name: Send a transactional email with Plunk
description: Send a one-off transactional email through Plunk safely — correct key class, idempotency, billing backpressure, and how to correlate the send with the delivery events that follow.
api: openapi/_original/plunk-api-openapi.json
operations: [sendEmail]
base_url: https://next-api.useplunk.com
---

# Send a transactional email with Plunk

## Before you call

- Use the **secret key** (`sk_*`). `/v1/send` rejects a public key with `401 INVALID_API_KEY`.
- The sender address must be on a **verified domain**. If you do not pass `from`, the project default is used.
- Every recipient costs **1 credit**; an email carrying attachments costs **2 credits** regardless of size.

## Steps

1. **Build the request.** `POST /v1/send` with `Authorization: Bearer sk_...` and `Content-Type: application/json`.
   Minimum body: `to`, `subject`, `body`. `to` accepts a single address or an array.

2. **Always set an `Idempotency-Key` header.** Any 1–255 character printable-ASCII string, unique per logical
   operation — a UUID, or something derived from your own data such as `receipt-order-1234`.

3. **Read the wrapped envelope.** `/v1/*` routes return `{"success": true, "data": {...}}` — not the bare
   resource that the dashboard routes return. Check `success` before touching `data`.

4. **Persist the email ID.** `data.emails[].email` is a bare UUID. Store it. It is the join key to every
   webhook event that follows (`event.emailId`), and Plunk will not hand it back to you later.

5. **Capture `X-Request-ID`** from the response headers and log it alongside your own request. It is the same
   value that appears as `error.requestId` on failures and is what support searches on.

## Handling the response

| Status | Code | What to do |
|---|---|---|
| `200` | — | Store `data.emails[].email`. Done. |
| `401` | `INVALID_API_KEY` | You sent a `pk_` key. Swap to the secret key. |
| `401` | `MISSING_AUTH` | No `Authorization` header. |
| `409` | `IDEMPOTENCY_KEY_REUSED` | **The email was NOT sent twice.** Plunk refuses rather than replaying, so you get no email ID back. Look up the ID you stored on the first attempt. `details.originalStatusCode: null` means the first request is still in flight — wait, do not retry. |
| `402` | `BILLING_LIMIT_EXCEEDED` | A per-category cap or the plan allowance is exhausted. Queue the work; caps reset at the start of the billing period. Do not hammer. |
| `422` | `VALIDATION_ERROR` | Read `error.errors[]` for `{field, message, code}`. Fix and retry **with the same key** — a 4xx releases the key. |
| `429` | `RATE_LIMIT_EXCEEDED` | 1000 req/min per project. Back off 1s, 2s, 4s, 8s. **No `Retry-After` or `RateLimit-*` header is returned**, so the delay cannot be read from the response. |
| `5xx` | `INTERNAL_SERVER_ERROR` | The key stays claimed on purpose — the send may have partially completed. Retrying with the same key returns `409`. Only retry with a **new** key if you are certain nothing went out. |

## Idempotency rules that decide your retry logic

- `2xx` → key **kept**. A retry would duplicate.
- `4xx` → key **released**. Fix the request and reuse the key.
- `5xx` → key **kept**. That is the whole point.
- Keys are scoped to the **project**, not the endpoint — a key spent on `/v1/track` cannot be used on `/v1/send`.
- Keys expire after **24 hours** and become reusable.

## Multiple recipients

`to` accepts an array, and Plunk processes recipients one at a time under a single key. If the request fails
partway with a `5xx`, some recipients have already received the email — the key stays claimed so a blind retry
does not send to them again. **If you need per-recipient control, send one request per recipient with its own key.**

## What happens next

Delivery outcomes arrive as webhooks, not in the response. Match them on `event.emailId` against the ID you
stored: `email.sent`, `email.delivery`, `email.open`, `email.click`, `email.bounce`, `email.complaint`.
Webhooks are configured as a `WEBHOOK` step inside a workflow, they are **not signed**, and they are **not
retried**. See `asyncapi/plunk-webhooks.yml`.

## References

- Operation: `sendEmail` in `openapi/_original/plunk-api-openapi.json`
- https://docs.useplunk.com/api-reference/public-api/sendEmail
- https://docs.useplunk.com/guides/idempotency
- `conventions/plunk-conventions.yml`, `errors/plunk-problem-types.yml`
