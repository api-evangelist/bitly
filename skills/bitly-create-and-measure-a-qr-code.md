---
name: bitly-create-and-measure-a-qr-code
description: >-
  Create a branded, re-pointable Bitly QR Code for a link, fetch its image, and read scan
  analytics by country, city, browser and device OS. Use when an agent is asked for a QR Code for
  print, packaging or an event.
api: Bitly API v4
base_url: https://api-ssl.bitly.com/v4
generated: '2026-08-13'
method: generated
source: openapi/bitly-qr-codes-api-openapi.yml, openapi/bitly-bitlinks-api-openapi.yml
operations:
  - createFullBitlink
  - createQRCodePublic
  - createStaticQRCodePublic
  - getQRCodeByIdPublic
  - getQRCodeImagePublic
  - updateQRCodePublic
  - redirectQRCodeDestination
  - getScanMetricsSummaryForQRCode
  - getScanMetricsForQRCode
  - getScanMetricsForQRCodeByCountries
  - getScanMetricsForQRCodeByCities
  - getScanMetricsForQRCodeByBrowser
  - getScanMetricsForQRCodeByDevicesOS
  - listQRMinimal
---

# Create and measure a QR Code

## Dynamic or static — decide before you print

This is the decision that cannot be undone after the code is on physical media.

- **Dynamic** (`POST /v4/qr-codes` → `createQRCodePublic`) encodes a Bitlink. The destination can
  be changed later and every scan is tracked.
- **Static** (`POST /v4/qr-codes/static` → `createStaticQRCodePublic`) encodes the destination
  directly. It cannot be re-pointed and yields no scan analytics.

**Default to dynamic.** Only use static when the caller explicitly requires a code that works with
no Bitly dependency, and tell them what they are giving up.

## 1. Create the Bitlink

`POST /v4/bitlinks` → `createFullBitlink`

Pass `long_url`, `group_guid` and, for a branded code, a `domain` from `GET /v4/bsds`.

## 2. Create the QR Code

`POST /v4/qr-codes` → `createQRCodePublic`

```json
{
  "bitlink": "bit.ly/3AbCdEf",
  "group_guid": "<guid>",
  "title": "Spring packaging",
  "render_customizations": { }
}
```

`render_customizations` is a deep object — foreground and background colours, gradients, corner
(pip) styling, dot pattern, logo, branding, frame and frame text. The schemas are
`QRCodeCustomizationsPublic`, `QRCodeCorners`, `QRCodeGradient`, `QRCodeLogoPublic`,
`QRCodeBranding`, `QRCodeFrameRequest` and `QRCodeText` in the spec. Read them before composing;
do not guess field names.

Heavy customisation lowers scan reliability. Keep contrast strong and do not oversize the logo.

## 3. Fetch the image

`GET /v4/qr-codes/{qrcode_id}/image` → `getQRCodeImagePublic`

Returns a **URL to download the image**, not the image bytes. Fetch that URL separately.

## 4. Re-point later, without reprinting

- `PATCH /v4/qr-codes/{qrcode_id}` → `updateQRCodePublic` — title, customizations, archived state
- `PATCH /v4/qr-codes/{qrcode_id}/redirect` → `redirectQRCodeDestination` — change where the
  printed code sends people

This is the whole point of a dynamic code. Confirm with the caller before re-pointing anything
already in circulation.

## 5. Measure scans

Summary first: `GET /v4/qr-codes/{qrcode_id}/scans/summary` → `getScanMetricsSummaryForQRCode`

Then as needed, using the same `unit` / `units` / `unit_reference` window as every other Bitly
analytics call:

- `/scans` → `getScanMetricsForQRCode` (time series)
- `/scans/countries` → `getScanMetricsForQRCodeByCountries`
- `/scans/cities` → `getScanMetricsForQRCodeByCities`
- `/scans/browsers` → `getScanMetricsForQRCodeByBrowser`
- `/scans/device_os` → `getScanMetricsForQRCodeByDevicesOS`

`device_os` is the operating system, **not** the form factor. Bitly's April 2026 MCP changelog
called this out specifically because the two were being confused.

## Inventory

`GET /v4/groups/{group_guid}/qr-codes` → `listQRMinimal` — cursor-paginated with `search_after`
and `size`, filterable by `query`, `is_gs1`, `has_render_customizations` and `qrc_type`.

## Rules that bite

- QR Code creation is metered separately and tightly: **2/month on Free, 5 on Core, 10 on Growth,
  200 on Premium**. Check the plan before generating a batch.
- No idempotency key exists. A retried create makes a second QR Code and consumes another unit
  of that small monthly allowance. Check `listQRMinimal` before retrying.
- `DELETE /v4/qr-codes/{qrcode_id}` → `deleteQRCode` is destructive and a printed code will stop
  working. Never call it without explicit confirmation.
- **410 GONE** means the code existed and was deleted — distinct from 404. Do not retry.
