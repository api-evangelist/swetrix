---
name: Record revenue transactions in Swetrix idempotently
description: Post revenue transactions to Swetrix from a payment webhook without double-counting, using a stable transactionId as the idempotency key.
api: openapi/swetrix-revenue-api-openapi.yml
operations: [recordRevenue]
generated: '2026-08-13'
method: generated
source: >-
  openapi/swetrix-revenue-api-openapi.yml (operationId verified present), plus
  https://swetrix.com/docs/events-api and
  https://swetrix.com/docs/analytics-dashboard/revenue-tracking
---

# Record revenue transactions in Swetrix idempotently

`recordRevenue` (`POST /log/revenue` on `https://api.swetrix.com`) is the only
server-side-only ingestion endpoint — it **requires an API key** and the key must
belong to an account with rights on the target project.

## The idempotency contract

Swetrix has no generic `Idempotency-Key` header. Instead, `POST /log/revenue`
takes a caller-supplied `transactionId`:

> Re-sending the same `transactionId` replaces the previous version (idempotent).
> If omitted, a UUID is generated.

**Always pass one.** Use your own order id. Payment platforms retry their
webhooks, and a generated UUID makes every retry a new transaction.

## Steps

1. Receive the payment-platform webhook and extract a **stable** order id.
2. Call `recordRevenue` with `pid`, that id as `transactionId`, the amount and
   currency, and optionally `productId`, `productName`, and `metadata` (string
   key/value pairs, max 100 keys / 2 KB).
3. For attribution, pass `profileId` (the `usr_`-prefixed profile from the
   tracking script's `identify()`) and/or `sessionId` from `getSessionId()`.
4. On a retry of the same webhook, send the **same** `transactionId` again. The
   existing record is updated, not duplicated.

## Rules

- **`409 Conflict` means stop, not retry.** It is returned when a Stripe or
  Paddle key is already connected for the project — sending revenue through the
  API as well would double-count. Disconnect the source in
  Project Settings → Revenue, or stop posting revenue via the API. Retrying the
  same request will keep failing.
- **`403 Forbidden` on this endpoint means permissions**, not de-duplication: the
  API key cannot manage the target project. (On `POST /log`, 403 means something
  entirely different — see `errors/swetrix-problem-types.yml`.)
- **`402 Payment Required`** means the project is inactive or over quota; events
  are being rejected until that is resolved.
- Success is **201 Created**.
- Rate limits are per plan (300/hour Standard, 6,000/hour Plus) with no
  rate-limit response headers — back off on `429`.
