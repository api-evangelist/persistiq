---
name: Handle campaign replies and wire up webhooks
description: >-
  Watch a PersistIQ campaign's inbox, read prospect replies with their sentiment,
  send a reply back through the connected mailbox, and configure the webhook
  plugin so replies and opens are pushed to you instead of polled.
api: openapi/persistiq-api-v1-openapi.json
generated: '2026-08-13'
method: generated
source: https://api.persistiq.com/api-docs/v1/swagger.json
operations:
  - 'GET /v1/campaigns'
  - 'GET /v1/campaigns/{campaign_id}/replies'
  - 'POST /v1/campaigns/{campaign_id}/replies'
  - 'GET /v1/webhook_plugin'
  - 'PUT /v1/webhook_plugin'
---

# Handle campaign replies and wire up webhooks

PersistIQ's reply and webhook surfaces exist only in its own OpenAPI document
(`https://api.persistiq.com/api-docs/v1/swagger.json`) — they are absent from the
derived per-tag specs in `openapi/`. **The official document declares no
`operationId` on any operation**, so every step below cites method + path, which
is what the specification actually guarantees.

## Before you start

- Base URL: `https://api.persistiq.com`
- Auth: `x-api-key: <key>` on every request. The key is **company-wide** — it can
  read and send mail on behalf of every user in the account. There is no scoped
  or per-user credential. Treat sending a reply as an irreversible external
  action and confirm with a human before calling `POST .../replies`.
- Read `x-ratelimit-remaining` on each response and back off before it reaches 0.
  The documented limit is 100/min; the live header has been observed at 500.
  Trust the header.
- Every response carries `x-request-id`. Log it — it is the only handle support
  has on a failed call.

## 1. Find the campaign

`GET /v1/campaigns?name=<name>`

Optional filters: `name`, `owner_id`, `lead_id`, `page`. The response envelope is
`{ has_more, next_page, status, campaigns: [...] }`. Each campaign carries `id`
(an opaque hashed id — do not parse it), `name`, `creator`, and a `stats` object
with `prospects_contacted`, `prospects_reached`, `prospects_opened`,
`prospects_replied`, `prospects_bounced`, `prospects_optedout` and
`total_prospects`.

Walk pages with `page=1,2,3…` until `has_more` is false, or follow `next_page`.

## 2. Read the replies

`GET /v1/campaigns/{campaign_id}/replies`

Filters: `lead_id`, `start_at`, `end_at` (ISO 8601), `page`. Returns `reply_type`
objects: `id`, `from_email`, `to_emails`, `cc_emails`, `subject`, `body`,
`preview`, `sent_at`, `sentiment`, `kind`, `lead_id`, `campaign_id`,
`step_message_id`.

- `sentiment` is PersistIQ's own classification of the reply. It is the only
  scored field in the API — use it to triage, but re-read `body` before acting.
- `kind` distinguishes the message type; `step_message_id` is the handle you
  need in step 3.
- `404` means the campaign does not exist or is not visible to this key.

For an incremental sync, keep the highest `sent_at` you have seen and pass it as
`start_at` on the next poll. There is no `updated_after` on this endpoint.

## 3. Send a reply

`POST /v1/campaigns/{campaign_id}/replies`

Request body (both fields required):

```json
{ "inbox_message_id": "<hashed id of the message being replied to>",
  "body": "<HTML body>" }
```

`body` is **HTML**, not plain text.

Responses:

- `201` — queued. Note the envelope is different from everything else in this
  API: `{ "status": "queued", "message": "..." }`, not the standard
  `{ "status": "success", ... }`. Do not key your success check on `"success"`.
- `400` — missing parameters, or the message does not belong to that campaign.
- `404` — campaign or inbox message not found.
- `422` — **the sending mailbox is disconnected.** This is an account problem, not
  a request problem. Do not retry; surface it to a human to reconnect the mailbox.

There is no idempotency key. A retried `POST` sends a second email. If a call
times out, poll step 2 to see whether the reply landed before retrying.

## 4. Stop polling — configure webhooks

`GET /v1/webhook_plugin` returns the current settings. `PUT /v1/webhook_plugin`
updates them. There is one plugin per company (no id, not a collection), so a
`PUT` overwrites whatever the account already had — **read first, merge, then
write**, or you will silently disable another integration's webhooks.

Each event has an independent boolean and its own URL:

| Event | Enable field | URL field |
|---|---|---|
| New prospect created | `post_new_prospect` | `post_new_prospect_url` |
| Prospect updated | `post_updated_prospect` | `post_updated_prospect_url` |
| Raw activity events | `raw_events` | `raw_events_url` |
| Email reply received | `post_email_reply` | `post_email_reply_url` |
| Email opened | `post_email_opened` | `post_email_opened_url` |

For this flow, enable `post_email_reply`:

```json
{ "post_email_reply": true,
  "post_email_reply_url": "https://your-endpoint.example.com/persistiq/replies" }
```

PersistIQ publishes **no payload schema, no signature header and no retry policy**
for these deliveries. Treat the webhook as a trigger, not as data: on receipt,
call step 2 with a tight `start_at` window and read the authoritative reply from
the API. Verify the caller some other way (a secret path segment, an allowlist) —
there is nothing to verify a signature against.

## Failure modes to expect

- `401 unauthorized` — key missing or not resolvable. The message is literal:
  `Failed to find api key`.
- `429 too_many_requests` — back off; the reset is advertised in
  `X-RateLimit-Reset` when the window is being consumed.
- 15 of the 21 operations in the official spec document only a `200` and no error
  responses at all. Assume any operation can return the standard error envelope
  `{ "status": "error", "error": { "reason", "message" } }` regardless of what
  the spec lists.

See `conventions/persistiq-conventions.yml`, `errors/persistiq-problem-types.yml`
and `asyncapi/persistiq-webhooks.yml`.
