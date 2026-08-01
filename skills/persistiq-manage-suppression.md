---
name: Manage Do Not Contact suppression
description: Review and add domains to the PersistIQ Do Not Contact (DNC) suppression list.
api: openapi/persistiq-openapi.yml
operations: [listDncDomains, createDncDomain]
---

# Manage Do Not Contact suppression

Use this skill to keep PersistIQ from emailing suppressed domains.

## Auth
Send `x-api-key: YOUR_API_KEY` on every request. Base URL: `https://api.persistiq.com`.

## Steps
1. **Review current suppressions.** Call `listDncDomains` (`GET /v1/dnc_domains`).
   Each response holds up to 100 domains; follow `next_page` while `has_more` is
   true.
2. **Add a domain.** Call `createDncDomain` (`POST /v1/dnc_domains`) with a `name`
   (the domain to suppress). Emails to addresses at that domain will then be
   blocked without manual approval.

## Rules
- Rate limit is 100 requests/minute per key; back off on 429.
- A missing `name` returns 400 Bad Request with reason `bad_params`.
- Suppression is domain-level, not address-level.
