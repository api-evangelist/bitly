---
name: bitly-report-link-performance
description: >-
  Pull click and engagement analytics for a single Bitly link or for a whole workspace, sliced by
  time, country, city, device or referrer. Use when an agent is asked how a link, a campaign or a
  workspace performed.
api: Bitly API v4
base_url: https://api-ssl.bitly.com/v4
generated: '2026-08-13'
method: generated
source: openapi/bitly-bitlinks-api-openapi.yml, openapi/bitly-groups-api-openapi.yml
operations:
  - getClicksSummaryForBitlink
  - getClicksForBitlink
  - getEngagements
  - getEngagementsSummary
  - getMetricsForBitlinkByCountries
  - getMetricsForBitlinkByCities
  - getMetricsForBitlinkByDevices
  - getMetricsForBitlinkByReferrers
  - getMetricsForBitlinkByReferringDomains
  - getGroupClicks
  - getGroupMetricsOverTime
  - getGroupTopMetrics
  - getGroupTopLinkClicks
  - getBitlinksByGroup
---

# Report link performance

## The time-window idiom

Every analytics operation on Bitly shares the same three parameters. Learn them once:

| Parameter | Meaning |
|---|---|
| `unit` | Bucket size — `minute`, `hour`, `day`, `week`, `month` |
| `units` | How many buckets back to return. `-1` means all available |
| `unit_reference` | ISO-8601 timestamp for the most recent bucket. Defaults to now |

Retention is plan-dependent — 30 days on Core, 4 months on Growth, 1 year on Premium, 2 years on
Enterprise. Asking for `units: -1` on a Core account will not reach back further than the plan
allows, and Bitly will not tell you it truncated.

## Single link

Start with the cheap call:

`GET /v4/bitlinks/{bitlink}/clicks/summary` → `getClicksSummaryForBitlink`

One total for the window. Use this before pulling a series.

Then, as needed:

- `GET /v4/bitlinks/{bitlink}/clicks` → `getClicksForBitlink` — a time series
- `GET /v4/bitlinks/{bitlink}/engagements` → `getEngagements` — clicks, QR scans and link-in-bio
  button presses together, not just clicks
- `GET /v4/bitlinks/{bitlink}/engagements/summary` → `getEngagementsSummary`
- `.../countries` → `getMetricsForBitlinkByCountries`
- `.../cities` → `getMetricsForBitlinkByCities`
- `.../devices` → `getMetricsForBitlinkByDevices`
- `.../referrers` → `getMetricsForBitlinkByReferrers`
- `.../referring_domains` → `getMetricsForBitlinkByReferringDomains`

Prefer **engagements** over **clicks** when the link has a QR Code — clicks alone will undercount
real-world scans.

## Whole workspace

- `GET /v4/groups/{group_guid}/clicks` → `getGroupClicks`
- `GET /v4/groups/{group_guid}/engagements/over_time` → `getGroupMetricsOverTime`
- `GET /v4/groups/{group_guid}/engagements/top` → `getGroupTopMetrics`
- `GET /v4/groups/{group_guid}/links/clicks/top` → `getGroupTopLinkClicks`

To attribute results to specific links, list them first with
`GET /v4/groups/{group_guid}/bitlinks` → `getBitlinksByGroup`, filtering on `campaign_guid`,
`channel_guid`, `tags`, `created_after` or `created_before`.

## Pagination

Listing operations are **cursor-paginated**. Pass `size` (default 50) and then the opaque
`search_after` token exactly as the API returned it. There is no page number — never synthesise
a cursor.

## Interpretation warnings

- Since **2024-06-12**, analytics responses can include engagements for *all versions* of an
  edited or redirected link, not only the current destination. A jump in historical numbers may
  be this change, not real traffic. See
  https://dev.bitly.com/docs/tutorials/changes-to-engagement-metrics/
- The metrics surface is wide and each dimension is a separate call. Fan-out across nine
  dimensions for many links will exhaust a Free or Core monthly quota quickly. Summarise first,
  drill down only where the summary justifies it.
- **429 `API_USAGE_LIMIT_EXCEEDED`** during a reporting run means the month's quota is gone. Do
  not retry — it resets on the 1st. Check `GET /v4/user/platform_limits` (`getPlatformLimits`)
  before starting a large pull.
