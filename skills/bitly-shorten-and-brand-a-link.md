---
name: bitly-shorten-and-brand-a-link
description: >-
  Create a Bitly short link in the correct workspace, optionally on a branded custom domain with
  a chosen back-half, and confirm it. Use when an agent needs to turn a long URL into a
  trackable, brandable short link.
api: Bitly API v4
base_url: https://api-ssl.bitly.com/v4
generated: '2026-08-13'
method: generated
source: openapi/bitly-bitlinks-api-openapi.yml, openapi/bitly-groups-api-openapi.yml, openapi/bitly-bsds-api-openapi.yml
operations:
  - getGroups
  - getGroupPreferences
  - getBSDs
  - createFullBitlink
  - getBitlink
---

# Shorten and brand a link

Every write in Bitly lands in a **group** (workspace). Getting the group wrong is the most common
integration failure, so resolve it first rather than relying on the account default.

## 1. Resolve the target group

`GET /v4/groups` → `getGroups`

Returns every group the token can reach, each with `guid`, `name`, `organization_guid` and `bsds`.
Pick the `guid` deliberately. If the caller did not name a workspace, ask — do not silently fall
back to `default_group_guid` from `GET /v4/user`.

## 2. Decide the domain

`GET /v4/groups/{group_guid}/preferences` → `getGroupPreferences`

Returns `domain_preference`, the domain used when `domain` is omitted.

For a branded link, confirm the domain is actually available to this group:

`GET /v4/bsds` → `getBSDs`

Only pass a `domain` that appears in that list, or in the group's own `bsds` array. Passing a
domain the group cannot use returns **400 `INVALID_ARG_DOMAIN`** — Bitly documents this as its
single most common error.

## 3. Create the link

`POST /v4/bitlinks` → `createFullBitlink`

```json
{
  "long_url": "https://example.com/spring-campaign",
  "group_guid": "<guid from step 1>",
  "domain": "<branded domain, or omit for the group default>",
  "title": "Spring campaign",
  "tags": ["spring", "email"]
}
```

Use `createFullBitlink` (`POST /v4/bitlinks`), not `createBitlink` (`POST /v4/shorten`). Only the
full endpoint accepts `title`, `tags`, `deeplinks` and a custom back-half.

**Always send `group_guid` explicitly.** It is the parameter that prevents `INVALID_ARG_DOMAIN`
and it is what keeps agent-created links out of a human's personal workspace.

### Custom back-half

Add a `keyword` for a memorable back-half (`bit.ly/spring-sale`). A back-half already taken on
that domain returns **409 CONFLICT** — this is not retryable. Generate an alternative and ask
before overwriting the caller's intent.

## 4. Confirm

`GET /v4/bitlinks/{bitlink}` → `getBitlink`

`{bitlink}` is the short form itself — domain plus hash, e.g. `bit.ly/3AbCdEf` — not a surrogate
id. Confirm `long_url`, `title` and `tags` came back as sent.

## Rules that bite

- **No idempotency.** Bitly publishes no `Idempotency-Key` and no client token. If step 3 times
  out, do **not** blind-retry: call `GET /v4/groups/{group_guid}/bitlinks` (`getBitlinksByGroup`)
  filtered by `created_after` and `query` to check whether the link already exists. A blind retry
  creates a second live link and burns a second unit of metered monthly quota.
- **No sandbox.** Every link created here is public and resolvable immediately.
- **402 UPGRADE_REQUIRED** means the operation is not in the account's plan, not that the request
  was malformed. Do not retry or reformulate — surface it to the caller.
- **429** carries `RATE_LIMIT_EXCEEDED` (back off) or `API_USAGE_LIMIT_EXCEEDED` (stop; the quota
  resets on the 1st of the month). Bitly returns no `Retry-After`, so use exponential backoff
  and check `GET /v4/user/platform_limits` before a large batch.
- Errors arrive as `{message, description, resource, errors[]}`. The machine-readable code is in
  `message`, and field-level failures are in `errors[]` as `{field, error_code, message}`.
