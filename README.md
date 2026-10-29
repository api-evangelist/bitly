# Bitly

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

Bitly is a link management platform for creating, branding, routing and measuring short links, QR Codes and link-in-bio pages at scale. The Bitly v4 REST API is a 94-operation, bearer-authenticated JSON API at https://api-ssl.bitly.com/v4 covering Bitlink creation and expansion, custom back-halves, branded short domains, groups (workspaces) and organizations, campaigns and channels, dynamic and static QR Codes, bulk shortening, engagement webhooks, and a deep click/scan analytics surface sliced by country, city, device, OS, browser and referrer. Bitly publishes its own OpenAPI 3.0 definition and operates an official remote Model Context Protocol server, making it directly callable by AI agents.

**Areas:** Links · URL Shorteners · QR Codes · Analytics · Marketing · Link Management · Webhook · Attribution · Agents · MCP

## Bitly on APIs.io

Everything profiled for Bitly is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/bitly/](https://apis.io/providers/bitly/)** — or go straight to one of the APIs or properties below.

### APIs (11)

- [Bitly BSDs API](https://apis.io/apis/bitly/bitly-bsds-api/) — List the branded short domains (BSDs) available to the authenticated account. 1 operation(s), extracted verbatim from the OpenAPI Bitly publishes at…
- [Bitly Bitlinks API](https://apis.io/apis/bitly/bitly-bitlinks-api/) — Create, expand, update, archive and delete Bitlinks, list them by group, and read per-link click, engagement, country, city, device and referrer metrics. 21…
- [Bitly Campaigns API](https://apis.io/apis/bitly/bitly-campaigns-api/) — Manage marketing campaigns and the channels inside them, grouping Bitlinks for attribution. 8 operation(s), extracted verbatim from the OpenAPI Bitly…
- [Bitly Custom Bitlinks API](https://apis.io/apis/bitly/bitly-custom-bitlinks-api/) — Create and update custom back-halves on existing Bitlinks and read clicks by destination for A/B rotations. 5 operation(s), extracted verbatim from the…
- [Bitly Groups API](https://apis.io/apis/bitly/bitly-groups-api/) — Manage groups (workspaces) — preferences, tags, shorten counts, exports, feature usage and historical usage — plus the full group-level click, scan and…
- [Bitly Organizations API](https://apis.io/apis/bitly/bitly-organizations-api/) — Read organizations, their plan limits, and shorten counts overall and by group. 5 operation(s), extracted verbatim from the OpenAPI Bitly publishes at…
- [Bitly QR Codes API](https://apis.io/apis/bitly/bitly-qr-codes-api/) — Create dynamic and static QR Codes, customize their render, fetch the image, upgrade a code to a Bitlink, and read scan metrics by browser, city, country…
- [Bitly User API](https://apis.io/apis/bitly/bitly-user-api/) — Read and update the authenticated user profile and read the platform limits applied to the account. 3 operation(s), extracted verbatim from the OpenAPI…
- [Bitly Webhooks API](https://apis.io/apis/bitly/bitly-webhooks-api/) — Create, read, update, delete and verify webhook endpoints that receive Bitly engagement events. 6 operation(s), extracted verbatim from the OpenAPI Bitly…
- [Bitly MCP Server](https://apis.io/apis/bitly/bitly-mcp-server/) — Bitly's official remote Model Context Protocol server, exposing 25 tools for link creation, QR Codes, analytics, groups, custom domains and bulk upload.…
- [Bitly Apps API](https://apis.io/apis/bitly/bitly-apps-api/) — The Apps API from Bitly — 1 operation(s) for apps.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Bitly Engagement Webhooks](https://apis.io/asyncapis/bitly/bitly-engagement-webhooks/)

#### MCP servers (2)

Model Context Protocol servers that expose the API to agents.

- [Bitly MCP Server](https://apis.io/servers/bitly/bitly-mcp-server/)
- [https://dev.bitly.com/bitly-mcp/](https://apis.io/servers/bitly/https-dev-bitly-com-bitly-mcp/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Bitly Agentic Access](https://apis.io/agentic-access/bitly/bitly-agentic-access/)

#### Collections (11)

Postman and Open Collection request collections.

- [Bitly API v4](https://apis.io/collections/bitly/open-bitly/)
- [Bitly Bitlinks API](https://apis.io/collections/bitly/open-bitly-bitlinks-api/)
- [Bitly BSDs API](https://apis.io/collections/bitly/open-bitly-bsds-api/)
- [Bitly Campaigns API](https://apis.io/collections/bitly/open-bitly-campaigns-api/)
- [Bitly Custom Bitlinks API](https://apis.io/collections/bitly/open-bitly-custom-bitlinks-api/)
- [Bitly Groups API](https://apis.io/collections/bitly/open-bitly-groups-api/)
- [Bitly OAuth Apps API](https://apis.io/collections/bitly/open-bitly-oauth-apps-api/)
- [Bitly Organizations API](https://apis.io/collections/bitly/open-bitly-organizations-api/)
- [Bitly QR Codes API](https://apis.io/collections/bitly/open-bitly-qr-codes-api/)
- [Bitly User API](https://apis.io/collections/bitly/open-bitly-user-api/)
- [Bitly Webhooks API](https://apis.io/collections/bitly/open-bitly-webhooks-api/)

#### Overlays (20)

OpenAPI overlays, including conversational phrasing for each operation.

- [Bitly Apps Api Phrasing Overlay](https://apis.io/overlays/bitly/bitly-apps-api-phrasing-overlay/)
- [Bitly Bitlinks Api Phrasing Overlay](https://apis.io/overlays/bitly/bitly-bitlinks-api-phrasing-overlay/)
- [Bitly Bitlinks Overlay](https://apis.io/overlays/bitly/bitly-bitlinks-overlay/)
- [Bitly Bsds Api Phrasing Overlay](https://apis.io/overlays/bitly/bitly-bsds-api-phrasing-overlay/)
- [Bitly Bsds Overlay](https://apis.io/overlays/bitly/bitly-bsds-overlay/)
- [Bitly Campaigns Api Phrasing Overlay](https://apis.io/overlays/bitly/bitly-campaigns-api-phrasing-overlay/)
- [Bitly Campaigns Overlay](https://apis.io/overlays/bitly/bitly-campaigns-overlay/)
- [Bitly Custom Bitlinks Api Phrasing Overlay](https://apis.io/overlays/bitly/bitly-custom-bitlinks-api-phrasing-overlay/)
- [Bitly Custom Bitlinks Overlay](https://apis.io/overlays/bitly/bitly-custom-bitlinks-overlay/)
- [Bitly Groups Api Phrasing Overlay](https://apis.io/overlays/bitly/bitly-groups-api-phrasing-overlay/)
- [Bitly Groups Overlay](https://apis.io/overlays/bitly/bitly-groups-overlay/)
- [Bitly Oauth Apps Overlay](https://apis.io/overlays/bitly/bitly-oauth-apps-overlay/)
- [Bitly Organizations Api Phrasing Overlay](https://apis.io/overlays/bitly/bitly-organizations-api-phrasing-overlay/)
- [Bitly Organizations Overlay](https://apis.io/overlays/bitly/bitly-organizations-overlay/)
- [Bitly Qr Codes Api Phrasing Overlay](https://apis.io/overlays/bitly/bitly-qr-codes-api-phrasing-overlay/)
- [Bitly Qr Codes Overlay](https://apis.io/overlays/bitly/bitly-qr-codes-overlay/)
- [Bitly User Api Phrasing Overlay](https://apis.io/overlays/bitly/bitly-user-api-phrasing-overlay/)
- [Bitly User Overlay](https://apis.io/overlays/bitly/bitly-user-overlay/)
- [Bitly Webhooks Api Phrasing Overlay](https://apis.io/overlays/bitly/bitly-webhooks-api-phrasing-overlay/)
- [Bitly Webhooks Overlay](https://apis.io/overlays/bitly/bitly-webhooks-overlay/)

#### Security (4)

Authentication, trust centre, and vulnerability disclosure.

- [Bitly Authentication](https://apis.io/security/bitly/bitly-authentication/)
- [Bitly Domain Security](https://apis.io/security/bitly/bitly-domain-security/)
- [Bitly Trust Center](https://apis.io/security/bitly/bitly-trust-center/)
- [Bitly Vulnerability Disclosure](https://apis.io/security/bitly/bitly-vulnerability-disclosure/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Bitly Scopes](https://apis.io/scopes/bitly/bitly-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Bitly Plans Pricing](https://apis.io/plans/bitly/bitly-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Bitly Rate Limits](https://apis.io/rate-limits/bitly/bitly-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://bitly.com)
- [Documentation](https://dev.bitly.com)
- [API reference](https://dev.bitly.com/api-reference)
- [Pricing](https://bitly.com/pages/pricing)
- [Support](https://support.bitly.com)
- [Blog](https://bitly.com/blog/)
- [Trust centre](https://security.bitly.com)
- [Terms of service](https://bitly.com/pages/terms-of-service)
- [Privacy policy](https://bitly.com/pages/privacy)
- [GitHub](https://github.com/bitly)
- [Status](https://bitly.statuspage.io)

## API Evangelist rating

**Kin Score 70.5** — exemplar · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 62.8 |
| Contract governance | 4.5 |
| Operational transparency | 84.2 |
| Developer ergonomics | 74.4 |
| Access clarity | 85.5 |

**Agent readiness 59.4** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | verified |
| Auth Clarity | served (partial credit) |
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
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | yes |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | distinct |

**Regulatory alignment 45.1** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/bitly/](https://apis.io/providers/bitly/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Bitly: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/bitly/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
