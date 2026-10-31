# PersistIQ

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
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

PersistIQ is a sales engagement platform for small teams to find new customers, start conversations, and personalize sales outreach at scale from one place. It combines prospect research (Chrome extension), multi-channel outreach (email, calls, tasks), campaign management with A/B testing, performance analytics, and CRM integrations. PersistIQ exposes a REST API (v1) for users, leads (prospects), lead statuses and fields, tags, campaigns (including duplication and inbox replies), activity events, Do Not Contact domains, and a webhook plugin carrying five events. It is specified by PersistIQ's own OpenAPI 3.0.1 document, served from the API host at /api-docs/v1/swagger.json. Authentication is a single company-wide API key sent in the x-api-key header, with page-number pagination and a documented 100 request/minute per-key rate limit.

**Areas:** Company · Sales Engagement · Sales · Outbound · Email Outreach · CRM · Lead Management · Marketing · Webhook · SEP

## PersistIQ on APIs.io

Everything profiled for PersistIQ is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/persistiq/](https://apis.io/providers/persistiq/)** — or go straight to one of the APIs or properties below.

### APIs (12)

- [PersistIQ Campaigns API](https://apis.io/apis/persistiq/persistiq-campaigns-api/) — Outreach campaigns
- [PersistIQ Do Not Contact Domains API](https://apis.io/apis/persistiq/persistiq-do-not-contact-domains-api/) — Suppressed domains
- [PersistIQ Events API](https://apis.io/apis/persistiq/persistiq-events-api/) — Activity events
- [PersistIQ Lead Fields API](https://apis.io/apis/persistiq/persistiq-lead-fields-api/) — Lead field definitions
- [PersistIQ Lead Statuses API](https://apis.io/apis/persistiq/persistiq-lead-statuses-api/) — Lead status definitions
- [PersistIQ Leads API](https://apis.io/apis/persistiq/persistiq-leads-api/) — Leads (prospects)
- [PersistIQ Users API](https://apis.io/apis/persistiq/persistiq-users-api/) — Company users
- [PersistIQ Campaign Leads API](https://apis.io/apis/persistiq/persistiq-campaign-leads-api/) — The Campaign Leads API from PersistIQ — 2 operation(s) for campaign leads.
- [PersistIQ DNC Domains API](https://apis.io/apis/persistiq/persistiq-dnc-domains-api/) — The DNC Domains API from PersistIQ — 1 operation(s) for dnc domains.
- [PersistIQ Replies API](https://apis.io/apis/persistiq/persistiq-replies-api/) — The Replies API from PersistIQ — 1 operation(s) for replies.
- [PersistIQ Tags API](https://apis.io/apis/persistiq/persistiq-tags-api/) — The Tags API from PersistIQ — 1 operation(s) for tags.
- [PersistIQ Webhook Plugin API](https://apis.io/apis/persistiq/persistiq-webhook-plugin-api/) — The Webhook Plugin API from PersistIQ — 1 operation(s) for webhook plugin.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Persistiq Webhooks](https://apis.io/asyncapis/persistiq/persistiq-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [persistiq](https://apis.io/servers/persistiq/persistiq/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Persistiq Agentic Access](https://apis.io/agentic-access/persistiq/persistiq-agentic-access/)

#### Collections (7)

Postman and Open Collection request collections.

- [PersistIQ Campaigns API](https://apis.io/collections/persistiq/open-persistiq-campaigns-api/)
- [PersistIQ Campaigns Do Not Contact Domains API](https://apis.io/collections/persistiq/open-persistiq-do-not-contact-domains-api/)
- [PersistIQ Campaigns Events API](https://apis.io/collections/persistiq/open-persistiq-events-api/)
- [PersistIQ Campaigns Lead Fields API](https://apis.io/collections/persistiq/open-persistiq-lead-fields-api/)
- [PersistIQ Campaigns Lead Statuses API](https://apis.io/collections/persistiq/open-persistiq-lead-statuses-api/)
- [PersistIQ Campaigns Leads API](https://apis.io/collections/persistiq/open-persistiq-leads-api/)
- [PersistIQ Campaigns Users API](https://apis.io/collections/persistiq/open-persistiq-users-api/)

#### Overlays (2)

OpenAPI overlays, including conversational phrasing for each operation.

- [Persistiq Api V1 Overlay](https://apis.io/overlays/persistiq/persistiq-api-v1-overlay/)
- [Persistiq Openapi Overlay](https://apis.io/overlays/persistiq/persistiq-openapi-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Persistiq Authentication](https://apis.io/security/persistiq/persistiq-authentication/)
- [Persistiq Domain Security](https://apis.io/security/persistiq/persistiq-domain-security/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Persistiq Plans Pricing](https://apis.io/plans/persistiq/persistiq-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Persistiq Rate Limits](https://apis.io/rate-limits/persistiq/persistiq-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://persistiq.com)
- [Documentation](https://apidocs.persistiq.com/)
- [Getting started](http://help.persistiq.com/en/articles/466972-getting-started-guide)
- [API reference](https://apidocs.persistiq.com/)
- [Pricing](https://www.persistiq.com/pricing/)
- [Sign up](https://persistiq.com/users/sign_up)
- [Support](http://help.persistiq.com/en/)
- [Blog](https://blog.persistiq.com/)
- [Terms of service](https://www.persistiq.com/terms-of-service/)
- [Privacy policy](https://www.persistiq.com/privacy/)
- [GitHub](https://github.com/PersistIQ)

## API Evangelist rating

**Kin Score 49.6** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 73.2 |
| Contract quality | 54.2 |
| Contract governance | 4.5 |
| Operational transparency | 47.4 |
| Developer ergonomics | 56.5 |
| Access clarity | 44.7 |

**Agent readiness 36.1** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | partial |
| Rate Limit Signal | verified |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | mostly (partial credit) |

**Regulatory alignment 24.5** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/persistiq/](https://apis.io/providers/persistiq/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for PersistIQ: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/persistiq/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
