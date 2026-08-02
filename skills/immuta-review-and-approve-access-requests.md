---
name: Review and determine Immuta access requests
description: Work a data steward's queue of pending Immuta access requests — pull the request, read the risk assessment and prior determinations, and record an approve or reject decision.
api: openapi/immuta-marketplace-api-openapi.yml
generated: '2026-08-01'
method: generated
operations:
  - user
  - searchAccessRequests
  - getAccessRequestById
  - getRiskAssessment
  - getAccessRequestRecords
  - recentDeterminations
  - searchDataProductMembers
  - updateApprovalRecord
  - revokeAccess
---

# Review and determine Immuta access requests

This is the steward side of the Request app. Every operation here changes who can see
governed data, so the default posture is: gather context, present it, and let the
human decide. An agent may prepare a determination; it should not record one unless
the reviewer explicitly said so.

## Before you start

- **Base URL**: `https://{global-segment}.api.immutacloud.com/marketplace`.
- **Auth**: `Authorization: Bearer <personal access token>` for an identity that holds
  reviewer rights on the data product. Confirm with `user`.
- Reviewing requires that the caller is on the product's review flow; a `403` here
  means the wrong identity, not a transient failure.

## Steps

1. **Pull the queue.** `searchAccessRequests` with a `status` filter for pending
   requests, plus `limit`/`offset` and `sortBy`/`sortOrder` to page it. Filter by
   `dataProductId` when working a single product.
2. **Open one request.** `getAccessRequestById` returns the hydrated record — the
   requesting user, the form version, the submitted form responses, the request type
   (access or masking exception), the target data product or asset, and any
   expiration.
3. **Read Immuta's risk assessment.** `getRiskAssessment` returns Immuta's
   AI-assisted recommendation for that request. Immuta documents its AI features as
   an augmentation with a human in the loop, and states the model is trained only on
   metadata such as group and attribute names, never on customer data. Present the
   recommendation as an input, never as the decision.
4. **Read the precedent.** `getAccessRequestRecords` returns the approval records
   already attached to this request. `recentDeterminations` returns the five most
   recent manual determinations on the same data product — the fastest way to see
   whether this request matches what stewards have already been approving.
5. **See who already has it.** `searchDataProductMembers` lists existing members of
   the product, which often answers "does this person already have equivalent access
   through a group?".
6. **Record the determination.** `updateApprovalRecord` (PUT `/api/approval-record/{id}`)
   approves or rejects the record. Do this only on an explicit human instruction, and
   echo back exactly what you are about to record before you send it.

## Revocation

`revokeAccess` (DELETE `/api/data-product/{id}/request/{requestId}`) removes a
previously granted access. Treat it as destructive: it takes data away from a working
user. Require explicit confirmation naming both the product and the person, and never
batch it across a list without per-item confirmation.

## Rules

- **Human in the loop is the product's own contract.** Immuta's published position is
  that its AI recommendations are an augmentation and not a replacement, with explicit
  human approval. An agent that auto-approves is violating the governance model the
  customer bought Immuta for.
- **No idempotency key.** If `updateApprovalRecord` times out, re-read the record
  with `getAccessRequestRecords` before resending.
- **No published rate limits and no declared `429`.** Page the queue at a human pace.
- Errors are plain JSON with a status and message; `401`/`403` are undeclared in the
  spec. See `errors/immuta-problem-types.yml`.
