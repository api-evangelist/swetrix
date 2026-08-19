---
name: Instrument a site and send events to Swetrix
description: Create a Swetrix project, then record pageviews, custom events, heartbeats and errors against it from server-side code.
api: openapi/swetrix-projects-api-openapi.yml, openapi/swetrix-events-api-openapi.yml, openapi/swetrix-errors-api-openapi.yml
operations: [createProject, getProject, recordPageview, recordCustomEvent, recordHeartbeat, recordError]
generated: '2026-08-13'
method: generated
source: >-
  openapi/*.yml (every operationId verified present), plus
  https://swetrix.com/docs/events-api and https://swetrix.com/docs/install-script
---

# Instrument a site and send events to Swetrix

Swetrix separates **admin** operations (project CRUD, versioned under `/v1`) from
**event ingestion** (unversioned, under `/log`). Both live on
`https://api.swetrix.com`.

## Before you start

- Authenticate every admin call with the `X-Api-Key` header. Generate the key in
  Account Settings → Account → API key (`https://swetrix.com/docs/settings/api-keys`).
- Ingestion calls carry the project id (`pid`) in the body; they do not need an
  API key unless noted.
- Event-ingestion endpoints return **201 Created**, not 200. Treat 200 as unexpected.

## Steps

1. **Create the project** — `createProject` (`POST /v1/project`). Keep the returned
   project id; it is the `pid` every later call needs.
2. **Confirm it exists** — `getProject` (`GET /v1/project/{id}`) before sending
   traffic, so a typo in `pid` does not silently discard events.
3. **Record a pageview** — `recordPageview` (`POST /log`). Set `unique: true` when
   you want Swetrix to de-duplicate the first pageview of a session. A `403` on a
   `unique` pageview is **not a failure** — it means the pageview was already
   recorded for that session and was intentionally dropped. Count it as success.
4. **Record product actions** — `recordCustomEvent` (`POST /log/custom`) with an
   event name and an optional string key/value `metadata` object.
5. **Keep sessions alive** — `recordHeartbeat` (`POST /log/hb`) for long-lived
   pages, so session duration is measured correctly.
6. **Report client errors** — `recordError` (`POST /log/error`) when you are
   catching exceptions yourself rather than letting the browser tracker do it.

## Rules

- **Rate limits.** 300 requests/hour on Standard, 6,000/hour on Plus, custom on
  Enterprise. Swetrix returns `429` and publishes **no** `RateLimit-*` or
  `Retry-After` headers, so track your own budget and back off exponentially with
  jitter. See `rate-limits/swetrix-rate-limits.yml`.
- **Errors are not RFC 9457.** The envelope is
  `{"statusCode": int, "message": string | string[], "error": string}`. For a
  `400` the `message` is an array, one entry per failed constraint — read it, fix
  the named field, do not blind-retry. See `errors/swetrix-problem-types.yml`.
- **`402 Payment Required` means collection is off.** The subscription lapsed or
  the monthly event quota is exceeded. Swetrix stops accepting new events until a
  human resolves it; retrying will not help.
- **Never invent a `pid`.** An unknown project id returns `400` with
  `"The provided Project ID (pid) is incorrect"`.
