---
name: Sync lead activity and update statuses
description: Poll PersistIQ activity events and reconcile lead statuses into an external system.
api: openapi/persistiq-openapi.yml
operations: [listEvents, listLeads, getLead, updateLead, listLeadStatuses]
---

# Sync lead activity and update statuses

Use this skill to keep an external CRM or warehouse in sync with PersistIQ.

## Auth
Send `x-api-key: YOUR_API_KEY` on every request. Base URL: `https://api.persistiq.com`.

## Steps
1. **Pull recent events.** Call `listEvents` (`GET /v1/events`) with `start_at`
   (and optionally `group`, `campaign`, `lead`, or `user`) to get activity since
   your last sync. Events include kinds like `lead_created`, `message_sent`,
   `message_received` (a reply), `message_bounced`, `message_optout`,
   `message_opened`, `message_clicked`.
2. **Page through.** Each response holds up to 500 events. While `has_more` is
   true, follow the `next_page` URL until it is false.
3. **Hydrate leads.** For events of interest, call `getLead`
   (`GET /v1/leads/{lead_id}`) or `listLeads` (`GET /v1/leads`) with
   `updated_after` to fetch current lead data.
4. **Reconcile statuses.** Call `listLeadStatuses` (`GET /v1/lead_statuses`) to map
   status names to ids, then call `updateLead` (`PUT /v1/leads/{lead_id}`) with
   `status`/`status_id`, or set `bounced`/`optedout`, or a `data` hash to update
   attributes.

## Rules
- Rate limit is 100 requests/minute per key; honor `X-RateLimit-Remaining` and
  back off on 429.
- Persist the max `event_at` you processed and use it as the next `start_at` to
  avoid reprocessing.
- Errors come back as `{ "status": "error", "error": { "reason", "message" } }`.
