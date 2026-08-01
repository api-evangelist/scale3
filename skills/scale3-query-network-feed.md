---
name: Query the blockchain network intelligence feed
description: >-
  Query the Scale3 network intelligence feed for a chain and network to get the
  latest announcements (aggregated from Discord and other channels), filtered
  by label and client.
api: openapi/scale3-blockchain-intelligence-openapi.yml
operations: [getNetworkFeed]
---

# Query the blockchain network intelligence feed

Use the Scale3 Blockchain Intelligence API to pull the latest network
announcements (upgrades, time-sensitive notices, actions needed) for a chain.

## Prerequisites
- An Enterprise-license API key from the Scale3 Autopilot **Intel** tab.
- Base URL: `https://web-backend.scale3production.com`

## Auth
Send both headers on every request:
- `x-api-key: <YOUR_API_KEY>`
- `x-user-agent: s3l-web-client`

## Steps
1. Call **getNetworkFeed** (`GET /feed`) with a required `chain`
   (e.g. `sui`, `eth`).
2. Optionally filter by `labels` (`announcement`, `general information`,
   `time sensitive`, `software upgrade`, `problem`, `needs action`), `network`,
   and `clients`.
3. Page with `page` / `page_size`; read `metadata.total_pages`.
4. For each `result[]` item read `event`, `description`, `labels`, and
   `additional_info_url` for the source announcement.

## Example
```bash
curl --request GET \
  --url 'https://web-backend.scale3production.com/feed?chain=eth&labels=announcement' \
  --header 'x-api-key: <YOUR_API_KEY>' \
  --header 'x-user-agent: s3l-web-client'
```

## Errors
On an invalid/missing key the API returns `401` with the envelope
`{ "error": { "message": "Invalid api key unauthorized", "status": 401 } }`.
See `errors/scale3-problem-types.yml`.
