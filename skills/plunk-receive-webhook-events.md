---
name: Receive Plunk webhook events in your application
description: Wire Plunk's workflow-based webhooks into your own service — build the receiving endpoint correctly given no signing and no retries, and correlate every event back to the send that caused it.
api: openapi/_original/plunk-api-openapi.json
operations: [sendEmail, trackEvent]
base_url: https://next-api.useplunk.com
---

# Receive Plunk webhook events in your application

Plunk has **no webhook subscription endpoint and no webhook registry**. A webhook is a `WEBHOOK` step inside a
workflow. You create a workflow triggered by an event, add a Webhook step, and enable it. Any event that can
trigger a workflow can be forwarded — including your own custom tracked events, which makes Plunk usable as an
event router.

## What you can subscribe to

| Family | Events |
|---|---|
| Email | `email.sent`, `email.delivery`, `email.open`, `email.click`, `email.bounce`, `email.complaint`, `email.received` |
| Contact | `contact.subscribed`, `contact.unsubscribed` |
| Segment | `segment.<slug>.entry`, `segment.<slug>.exit` |
| Custom | any name you send to `POST /v1/track` |

Segment events use a slugified name — a segment called "VIP Users" emits `segment.vip-users.entry`.

## Steps

1. **Build the receiving endpoint first.** It must be reachable on the public internet — loopback and RFC 1918
   addresses are refused by Plunk's SSRF guard, and each of the up-to-5 followed redirects is re-validated.

2. **Return 2xx within 10 seconds.** The request times out at 10s. Accept, enqueue, return. Do not do the work
   inline.

3. **Make the handler idempotent.** **Plunk does not retry.** A non-2xx or a timeout fails the workflow step
   outright and the event is gone. Combined with the 10s ceiling, that means your handler must be fast *and*
   safe to receive twice, since your own infrastructure may re-deliver from your queue.

4. **Authenticate the request yourself.** **Plunk does not sign payloads** — no HMAC header, no timestamp, no
   replay protection. Configure a secret header on the Webhook step and verify it on arrival:

   ```json
   { "Authorization": "Bearer your-shared-secret" }
   ```

   The docs explicitly prefer this to IP allowlisting, because egress IPs change. Rotate it like any other
   shared secret.

5. **Create the workflow.** Trigger on the event you want, add the Webhook step (URL, method — `POST` by
   default and recommended, headers, optional body), then enable the workflow. `url`, header values and `body`
   all support `{{variable}}` interpolation; the HTTP method does not, and the URL scheme must be literal
   `http://` or `https://`.

6. **Correlate on `emailId`.** Store the bare-UUID email ID returned by `POST /v1/send` at
   `data.emails[].email`. Every email webhook carries the same value at `event.emailId`. Join on it — do not
   match on contact email plus timestamp, and do not listen for `email.sent` just to capture a provider
   `messageId`.

## Default payload

```json
{
  "contact":   { "email": "...", "subscribed": true, "data": { } },
  "workflow":  { "id": "wf_...", "name": "..." },
  "execution": { "id": "exec_...", "startedAt": "..." },
  "event":     { }
}
```

Setting a custom body on the step **replaces this payload entirely**.

## Event payloads worth branching on

- **`email.bounce`** — `bounceType` is `Permanent` or `Transient`. Only `Permanent` counts toward your bounce
  rate and auto-unsubscribes the contact; `Transient` (mailbox full, out-of-office, greylist) carries
  `transientBounce: true` and should not be treated as a hard failure. Use a workflow `CONDITION` step on
  `bounceType` if you only want hard bounces forwarded.
- **`contact.unsubscribed`** — normally an empty `event` object. When the unsubscription was automatic it
  carries `reason: "bounce" | "complaint"`. That distinction is the whole point of the event for a sync job.
- **`email.received`** — inbound mail at your verified domain, with `spamVerdict`, `virusVerdict`,
  `spfVerdict`, `dkimVerdict`, `dmarcVerdict` (`PASS` / `FAIL` / `GRAY` / `PROCESSING_FAILED`) and the
  sanitized `body`. Check the verdicts before trusting the content.

## Shaping delivery with workflow steps

Because a webhook is a workflow step, you get the rest of the step vocabulary around it: `CONDITION` to filter
before firing, `DELAY` to buffer, `WAIT_FOR_EVENT` to wait for a follow-up before deciding, `UPDATE_CONTACT`
to annotate the contact first. That `WAIT_FOR_EVENT` / fallback-branch combination is the only retry-like
semantics available — there is nothing built in.

## References

- https://docs.useplunk.com/guides/webhooks
- https://docs.useplunk.com/concepts/workflows
- `asyncapi/plunk-webhooks.yml` — the full event catalogue with per-event payload fields
- Operations: `sendEmail`, `trackEvent` in `openapi/_original/plunk-api-openapi.json`
