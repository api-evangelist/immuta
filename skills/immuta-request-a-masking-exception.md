---
name: Request an Immuta masking exception
description: Ask for unmasked values on specific restricted columns of a data product, and track the exception request separately from a general access request.
api: openapi/immuta-marketplace-api-openapi.yml
generated: '2026-08-01'
method: generated
operations:
  - user
  - getDataProductById
  - searchDataProductColumns
  - getRequestForms
  - requestMaskingException
  - searchAccessRequestMaskingExceptionColumns
  - getApprovedMaskingExceptionColumns
  - getAccessRequestById
  - cancelAccessRequest
---

# Request an Immuta masking exception

A masking exception is narrower and more sensitive than an access request: the user
already has (or is asking for) access to the data product, and now wants to see the
real values in columns Immuta masks. Immuta treats it as its own request type with its
own form, because the justification a steward needs is different.

## Before you start

- **Base URL**: `https://{global-segment}.api.immutacloud.com/marketplace`.
- **Auth**: `Authorization: Bearer <personal access token>`; confirm with `user`.
- Since July 2026 a data product can carry a request form dedicated to masking
  exceptions, separate from its data-access form. Use that one.

## Steps

1. **Check what is already unmasked.** `getApprovedMaskingExceptionColumns` returns
   the columns the user already has approved exceptions for. If the column they want
   is on that list, there is nothing to request — say so and stop.
2. **Identify the exact columns.** `getDataProductById` for the product, then
   `searchDataProductColumns` with `maskedOnly` to list the restricted columns.
   Request the specific columns the user named, never a whole table "to be safe" —
   over-broad exception requests are the ones stewards reject.
3. **Fetch the masking-exception form.** `getRequestForms` on the product returns the
   forms; take the masking-exception form, not the data-access form. Read the
   questions and any attached data use agreement.
4. **Submit.** `requestMaskingException`
   (POST `/api/data-product/{id}/request/masking-exception`) with the column list and
   the completed form. The justification must state why masked values are insufficient
   for the stated task — that is the question the steward is actually answering.
   Do not write it for the user; use what they said.
5. **Track it.** `searchAccessRequestMaskingExceptionColumns` shows the columns tied
   to a given exception request; `getAccessRequestById` shows the request status.
   `cancelAccessRequest` withdraws it while it is still pending.

## Rules

- **Least privilege is the point.** Request the minimum column set. If the user asks
  for "everything", push back and get a specific list.
- **Never present a masking exception as routine.** It removes a privacy control that
  someone deliberately applied. Surface the data use agreement text to the human and
  let them accept it.
- **Not idempotent** — after a timeout, check the product's requests before resending.
- Errors are plain JSON with a status and message; see `errors/immuta-problem-types.yml`.
