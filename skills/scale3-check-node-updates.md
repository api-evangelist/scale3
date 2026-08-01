---
name: Check blockchain node software updates
description: >-
  Retrieve the latest node software updates for a specific blockchain and
  client from the Scale3 Blockchain Intelligence API, including version, commit
  hash, release date, breaking-change flags and build artifacts.
api: openapi/scale3-blockchain-intelligence-openapi.yml
operations: [getNodeUpdates]
---

# Check blockchain node software updates

Use the Scale3 Blockchain Intelligence API to find the latest node software
updates for a chain/client so you can keep validators and full nodes current.

## Prerequisites
- An Enterprise-license API key generated from the Scale3 Autopilot **Intel** tab.
- Base URL: `https://web-backend.scale3production.com`

## Auth
Send both headers on every request:
- `x-api-key: <YOUR_API_KEY>`
- `x-user-agent: s3l-web-client`

## Steps
1. Call **getNodeUpdates** (`GET /node_updates`) with a required `chain`
   (e.g. `eth`, `sui`, `sol`) and optionally `client` (e.g. `geth`), `network`
   (`mainnet`/`testnet`/`devnet`), `breaking_changes`, `priority`.
2. To narrow results, use `sort` (e.g. `sort=priority,-release_date`),
   `fields` (e.g. `fields=name,version,release_date`), and `page`/`page_size`.
3. Read `result[]` for each update's `version`, `commit_hash`, `release_date`,
   `breaking_changes`, `required_for_upcoming_upgrade`, and `build_artifacts[]`.
4. Use `metadata.total_pages` to page through additional results.

## Example
```bash
curl --request GET \
  --url 'https://web-backend.scale3production.com/node_updates?chain=eth&client=geth&network=mainnet' \
  --header 'x-api-key: <YOUR_API_KEY>' \
  --header 'x-user-agent: s3l-web-client'
```

## Errors
On an invalid/missing key the API returns `401` with the envelope
`{ "error": { "message": "Invalid api key unauthorized", "status": 401 } }`.
See `errors/scale3-problem-types.yml`.
