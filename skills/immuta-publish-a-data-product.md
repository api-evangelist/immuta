---
name: Publish an Immuta data product
description: Stand up a governed data product in the Immuta Request app — create it, attach data sources, wire a request form and data use agreement, and verify what consumers will see.
api: openapi/immuta-marketplace-api-openapi.yml
generated: '2026-08-01'
method: generated
operations:
  - user
  - getAvailableDomains
  - getImmutaTags
  - createDataProduct
  - updateDataProduct
  - updateDataSources
  - searchDataSources
  - getAllDataSources
  - searchDataProductColumns
  - createDataUseAgreement
  - createRequestForm
  - searchRequestForms
  - getRequestForms
  - getDataProductById
---

# Publish an Immuta data product

A data product is the unit consumers browse and request in the Immuta Request app. It
bundles data sources, a request form, and the policies that decide who gets in. This
skill covers standing one up end to end.

## Before you start

- **Base URL**: `https://{global-segment}.api.immutacloud.com/marketplace`.
- **Auth**: `Authorization: Bearer <personal access token>` for a data-product-manager
  identity. Confirm with `user`.
- The data sources you attach must already be registered in Immuta Govern. This API
  attaches existing sources; it does not register new ones — that is the Govern
  connections API.

## Steps

1. **Pick the domain.** `getAvailableDomains` lists the Immuta domains you may publish
   into. A data product carries a `domains` array; the domain is the governance
   boundary, so getting it wrong routes reviews to the wrong stewards.
2. **Prepare the agreement and the form first.** If consumers must accept terms, call
   `createDataUseAgreement` with the agreement body, then `createRequestForm` with the
   questions you want answered and the agreement ids attached. `searchRequestForms`
   shows what already exists — reuse before creating, because form names are unique
   and a duplicate returns `409`.
3. **Create the product.** `createDataProduct` with name, description, domains and
   metadata. The name must be unique in the tenant; a `409` means it is taken. Do not
   retry a `409` by mutating the name unless the human asked you to.
4. **Attach data sources.** `updateDataSources` (PUT `/api/data-product/{id}/datasources`)
   sets the data sources exposed by the product. This is a set operation — send the
   complete intended list, not a delta, or you will drop sources that are already
   attached. Read the current state with `searchDataSources` or `getAllDataSources`
   first.
5. **Check the column surface.** `searchDataProductColumns` shows the columns
   consumers will see and which are masked. `getImmutaTags` and the applied-tag search
   help confirm the sensitive columns carry the tags your policies target — publishing
   a product whose sensitive columns are untagged is how data leaks past a policy.
6. **Wire the forms.** `getRequestForms` on the product shows the attached forms.
   Since July 2026 a product can carry two distinct forms — one for data access
   requests and one for masking exception requests. Set both if the product has
   restricted columns.
7. **Verify.** `getDataProductById` and re-read the product as a consumer would see
   it. Confirm `suspended` is false, the expiration is what you intended, and the
   access and masking-exception policies are present.

## Rules

- **Creates are not idempotent.** `createDataProduct`, `createDataUseAgreement` and
  `createRequestForm` all return `409` on a duplicate name. After a timeout, search
  before you retry.
- **`updateDataSources` is a replace, not an append.** Always read then write.
- **Never fabricate policy.** The data access policy and masking exception policy on a
  data product decide who sees what. If the human has not specified them, ask; do not
  copy a policy from another product because it looked similar.
- Errors are plain JSON with a status and message; see `errors/immuta-problem-types.yml`.
