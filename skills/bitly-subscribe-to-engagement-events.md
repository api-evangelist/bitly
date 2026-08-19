---
name: bitly-subscribe-to-engagement-events
description: >-
  Register, verify and operate a Bitly webhook that receives engagement events (link clicks, QR
  scans, link-in-bio presses). Use when an agent needs Bitly activity pushed to a system rather
  than polled.
api: Bitly API v4
base_url: https://api-ssl.bitly.com/v4
generated: '2026-08-13'
method: generated
source: openapi/bitly-webhooks-api-openapi.yml, asyncapi/bitly-engagement-webhooks.yml
operations:
  - getOrganizations
  - getGroups
  - createWebhook
  - verifyWebhook
  - getWebhook
  - getWebhooks
  - updateWebhook
  - deleteWebhook
---

# Subscribe to engagement events

## Check eligibility first

Webhooks are an **Enterprise-plan feature**. On any other tier these operations return
**402 UPGRADE_REQUIRED**. Confirm the plan before building on this — 402 here is a commercial
answer, not a bug, and no amount of reformulating the request will change it.

## 1. Resolve the scope

A Bitly webhook is scoped to **both** an organization and a group.

- `GET /v4/organizations` → `getOrganizations`
- `GET /v4/groups` → `getGroups`

You need `organization_guid` and `group_guid` before you can create anything.

## 2. Create the webhook

`POST /v4/webhooks` → `createWebhook`

```json
{
  "name": "engagement-stream",
  "organization_guid": "<org guid>",
  "group_guid": "<group guid>",
  "event": "engagement",
  "url": "https://your-endpoint.example.com/bitly",
  "fetch_tags": true
}
```

- `event` has exactly one valid value: **`engagement`**. It covers link clicks, QR Code scans and
  link-in-bio button presses. It was previously called `click`; there is no separate click event.
- Set `fetch_tags: true` if you want the Bitlink's `tags` in the payload. It is off by default and
  cannot be backfilled onto events already delivered.
- Bitly authenticates **outbound** to your endpoint. Supply the credentials on the webhook record
  — API key in a query parameter, HTTP Basic, or OAuth 2.0 client credentials via `oauth_url`,
  `client_id` and `client_secret`.

## 3. Verify

`POST /v4/webhooks/{webhook_guid}/verify` → `verifyWebhook`

Run this before relying on delivery. Then read the record back with
`GET /v4/webhooks/{webhook_guid}` → `getWebhook` and check `is_active`, `status`, `is_alert` and
`deactivated`.

## 4. Receive

Deliveries are HTTPS `POST`, `application/json`, with a **10-second timeout**.

Payload fields: `event_id`, `event_type` (always the literal `"engagement"`), `timestamp`,
`timezone`, `long_url`, `bitlink`, `country`, `referrer`, `device_type`, `account_guid`,
`group_guid`, `webhook_guid`, `tags` (when `fetch_tags`), `references`.

Respond **2xx quickly**. Do the work asynchronously — anything past 10 seconds counts as a failure.

## 5. Survive failures

Bitly retries **five times with exponential backoff**. A failure is a client timeout or a 5xx.

- First failure → requeued.
- Second failure → the webhook enters **alert status** and the account administrator is notified.
- After **24 hours** in alert status it either clears on a 2xx or is **deactivated**.

Poll `GET /v4/organizations/{organization_guid}/webhooks` → `getWebhooks` and watch `is_alert`
and `deactivated`. A silently deactivated webhook is the failure mode to guard against: events
stop and nothing calls you to say so.

Re-enable with `PATCH /v4/webhooks/{webhook_guid}` → `updateWebhook`. Remove with
`DELETE /v4/webhooks/{webhook_guid}` → `deleteWebhook`.

## Rules that bite

- **No payload signature.** Bitly publishes no HMAC header and no signing secret, so you cannot
  cryptographically prove a delivery came from Bitly. Treat the endpoint as untrusted input:
  authenticate with the outbound scheme you configured, restrict by network where you can, and
  validate every field before acting on it.
- **No AsyncAPI document exists.** There is no machine-readable event contract to validate
  against — the payload shape above is from prose documentation, so parse defensively.
- **No ordering guarantee** is published. Deduplicate on `event_id` and treat `timestamp` as the
  ordering key, not arrival order.
- **This surface is REST-only.** Bitly's MCP server exposes none of these operations, so an agent
  working purely through MCP cannot subscribe to Bitly events at all.
