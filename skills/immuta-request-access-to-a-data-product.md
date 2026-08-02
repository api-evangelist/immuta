---
name: Request access to an Immuta data product
description: Find a governed data product in the Immuta Request app, read its request form, submit an access request, and track it through to a determination.
api: openapi/immuta-marketplace-api-openapi.yml
generated: '2026-08-01'
method: generated
operations:
  - user
  - searchDataProducts
  - getDataProductById
  - searchDataSources
  - getRequestForms
  - requestAccess
  - searchDataProductAccessRequests
  - getAccessRequestById
  - getAccessRequestRecords
  - cancelAccessRequest
---

# Request access to an Immuta data product

Use this when a person or an agent acting for them needs query access to data that
Immuta governs. Immuta never grants access silently — every request lands in a human
review flow, so the job here is to submit a complete, well-justified request and then
watch it, not to force a grant.

## Before you start

- **Base URL**: `https://{global-segment}.api.immutacloud.com/marketplace`, where
  `global-segment` is `na`, `eu` or `ap` — the segment the tenant is deployed into.
- **Auth**: a personal access token generated in the Request app at
  `https://app.immutacloud.com/marketplace/personal-access-tokens`, sent as
  `Authorization: Bearer <PAT>`. The token is shown once at creation. Confirm the
  identity you are acting as with `user` before doing anything else.
- **Conventions**: list endpoints page with `limit` (default 10, max 100) and
  `offset`, sort with `sortBy` + `sortOrder`, and filter with `searchText`. Every
  list response is `{ data: [...], meta: {...} }`. See `conventions/immuta-conventions.yml`.

## Steps

1. **Confirm who you are.** Call `user` to resolve the calling identity and its
   permissions and entitlements. Do not proceed if the token belongs to a different
   person than the one you are requesting for — Immuta ties the request to the token
   holder.
2. **Find the data product.** Call `searchDataProducts` with `searchText` for the
   subject the user described. If they gave an exact name, `getDataProductByName` is
   cheaper. Pick a candidate only when its name and description actually match the
   stated need; do not guess between near-matches — ask.
3. **Read the product before requesting.** Call `getDataProductById` for the full
   record (domains, status, expiration, data access policy, masking exception
   policy), and `searchDataSources` to see which data sources it exposes. If the
   product is `suspended`, stop and report that.
4. **Fetch the request form.** Call `getRequestForms` for the product. A product may
   carry two forms — one for data access and one for masking exceptions. Take the
   data-access form here. Read every field and any attached data use agreements; the
   agreement text is a legal acceptance and must be surfaced to the human, never
   auto-accepted on their behalf.
5. **Submit.** Call `requestAccess` with the completed form response and the
   justification the user gave you in their own words. A vague justification is the
   single most common reason a steward rejects a request — if the user has not given
   you a purpose, ask for one rather than inventing it.
6. **Track it.** Poll `searchDataProductAccessRequests` for the product, or
   `getAccessRequestById` for the specific request. `getAccessRequestRecords` returns
   the approval records — who has reviewed and what they determined.
7. **Withdraw if needed.** `cancelAccessRequest` cancels a request that is still
   pending. Only do this on explicit instruction.

## Rules

- **Never revoke.** `revokeAccess` exists on this API and removes a grant from a
  user. It is not part of this flow. Do not call it while chasing an approval.
- **This API is not idempotent.** Re-POSTing a create is not safe: Immuta's
  imperative Marketplace endpoints return `409` on a duplicate name rather than
  converging. Before retrying `requestAccess` after a timeout, list the product's
  requests and check whether yours already landed. (The declarative Govern V2 API is
  the idempotent half of Immuta — see `conventions/immuta-conventions.yml`.)
- **No rate limits are published**, and no `429` is declared on any operation. Poll
  politely — seconds apart, not milliseconds.
- **Errors are plain JSON**, not `application/problem+json`, and `401`/`403` are not
  declared in the contract. Treat any non-2xx as terminal and report the status and
  message verbatim rather than retrying blind. See `errors/immuta-problem-types.yml`.
