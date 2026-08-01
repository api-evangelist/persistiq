---
name: Import leads and enroll them in a campaign
description: Create new leads in PersistIQ and add them to an existing outreach campaign.
api: openapi/persistiq-openapi.yml
operations: [listUsers, createLeads, listCampaigns, addLeadsToCampaign]
---

# Import leads and enroll them in a campaign

Use this skill to bring prospects into PersistIQ and start outreach.

## Auth
Send `x-api-key: YOUR_API_KEY` on every request. The key is company-wide.
Base URL: `https://api.persistiq.com`.

## Steps
1. **Identify the creator (optional).** Call `listUsers` (`GET /v1/users`) to get a
   valid `creator_id` if you want new leads attributed to a specific user.
2. **Create the leads.** Call `createLeads` (`POST /v1/leads`) with a `leads` array
   (max 10 per call; page sequentially for more). Each lead requires `email`.
   Set `dup` to `update` or `skip` to control duplicate handling. Optionally set
   `creator_id`. Inspect the response `errors` array for per-lead failures
   (e.g. "Email can't be blank").
3. **Find the campaign.** Call `listCampaigns` (`GET /v1/campaigns`), optionally
   filtering by `name` or `owner_id`, to resolve the target `campaign_id`.
4. **Enroll the leads.** Call `addLeadsToCampaign`
   (`POST /v1/campaigns/{campaign_id}/leads`) with a `leads` array of lead ids
   (max 100 per call) and an optional `mailbox_id`. Check the `errors` array for
   leads already in the campaign ("Lead has already been taken").

## Rules
- Respect the rate limit: 100 requests/minute per key; back off on 429 using
  `X-RateLimit-Reset`.
- There is no idempotency key. Use `dup: skip` to avoid duplicate leads on retry.
- Do not exceed batch caps (10 for create leads, 100 for add-to-campaign) — the
  API returns 400 otherwise.
