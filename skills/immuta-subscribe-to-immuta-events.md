---
name: Subscribe to Immuta events with webhooks
description: Register, test and monitor Immuta webhooks so a downstream system reacts to access decisions, policy changes and health events instead of polling.
api: openapi/immuta-marketplace-api-openapi.yml
generated: '2026-08-01'
method: generated
operations:
  - user
  - getWebhooks
  - createWebhook
  - getWebhook
  - updateWebhook
  - testWebhookConfig
  - testWebhook
  - getWebhookHistory
  - deleteWebhook
---

# Subscribe to Immuta events with webhooks

Immuta has no AsyncAPI document and no streaming surface; webhooks are the event
mechanism. There are two webhook surfaces — the Request app's (in the Marketplace
OpenAPI, under the Notification tag) and the Govern app's (documented as REST
endpoints on the tenant host). The 73 subscribable Govern event types are catalogued
in `asyncapi/immuta-webhooks.yml`.

## Before you start

- **Request app base URL**: `https://{global-segment}.api.immutacloud.com/marketplace`,
  auth `Authorization: Bearer <personal access token>`.
- **Govern app base URL**: the customer's own Immuta tenant host, auth
  `Authorization: <api-key>` (raw, no scheme prefix) or a bearer token exchanged at
  `POST /bim/apikey/authenticate`. Registering system-wide Govern webhooks requires
  the `APPLICATION_ADMIN` permission; any user may register webhooks for their own
  access-request and activity notifications.

## Steps (Request app)

1. **List what exists.** `getWebhooks` — never register a second webhook for a URL
   that is already subscribed; duplicates double-deliver.
2. **Dry-run the config.** `testWebhookConfig` validates a webhook configuration
   before you persist it. Use it first; it is cheaper than creating and deleting.
3. **Create it.** `createWebhook` with the receiver `url`, `verifyTls`, and the
   signing key handling your receiver expects. Keep `verifyTls` true — turning it off
   means Immuta will post governance events to an unverified endpoint.
4. **Test the live hook.** `testWebhook` fires a test delivery at the registered
   webhook. Confirm your receiver returns 2xx.
5. **Watch deliveries.** `getWebhookHistory` returns the delivery record for a
   webhook — the first place to look when a downstream system says it missed an event.
6. **Change or remove.** `updateWebhook`, `deleteWebhook`.

## Steps (Govern app)

The Govern webhook endpoints are `POST /webhooks` (create, accepts multiple in one
request), `GET /webhooks` (search), `GET /webhooks/{id}`, `GET /webhooks/actions`
(the subscribable notification actions), `GET /webhooks/history`,
`POST /webhooks/history/retry/{id}` (retry a delivery) and `DELETE /webhooks/{id}`.

A registration carries:
- `notificationType` — an array of event types, or `ALL_NOTIFICATIONS` for everything.
- `actionType` — `triggered` (fire when the registering user caused the event) or
  `received` (fire when the registering user is the recipient of an event another
  user caused).
- `global` — when true, receive all notifications even those that do not pertain to
  the registering user. Only set this deliberately; it is a firehose.

## Rules

- **Your receiver has 10 seconds.** Immuta documents that a user-configured webhook
  integration must respond within 10 seconds or the request times out. Acknowledge
  immediately and do the work asynchronously.
- **Subscribe narrowly.** `ALL_NOTIFICATIONS` plus `global: true` will deliver every
  governance event in the tenant. Pick the specific event types you handle —
  `modelAccessRequested`, `modelAccessApproved`, `modelAccessDenied`,
  `modelAccessRevoked`, `globalPolicyUpdated`, `healthCheckFailed` and
  `nativeIntegrationValidationFailed` cover most integrations.
- **Retry is manual on the Govern side** — `POST /webhooks/history/retry/{id}`. There
  is no documented automatic backoff, so a receiver outage means lost events until
  someone retries them. Build your consumer to be replay-safe.
- **Events carry governance decisions about people.** Treat payloads as sensitive:
  they name users, data sources and policies.
