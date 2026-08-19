---
name: Pull traffic, performance and session analytics from Swetrix
description: Read aggregated traffic, performance, session and error analytics for a Swetrix project and slice them by dimension.
api: openapi/swetrix-traffic-api-openapi.yml, openapi/swetrix-performance-api-openapi.yml, openapi/swetrix-sessions-api-openapi.yml, openapi/swetrix-errors-api-openapi.yml
operations: [getTrafficLog, getBirdseyeSummary, getLiveVisitors, getUserFlow, getKeywords, getFilters, getPerformanceLog, getPerformanceBirdseye, listSessions, getSession, listErrors, getError, getErrorOverview, getCustomEvents]
generated: '2026-08-13'
method: generated
source: >-
  openapi/*.yml (every operationId verified present), plus
  https://swetrix.com/docs/statistics-api and https://swetrix.com/docs/api/stats-v2
---

# Pull traffic, performance and session analytics from Swetrix

All reads are `GET` on `https://api.swetrix.com`, authenticated with the
`X-Api-Key` header. **Public projects can be read without a key.**

## Steps

1. **Discover what you can filter on** — `getFilters`
   (`GET /v1/log/filters`) returns the values present for a dimension in this
   project, so you filter on real values instead of guessing.
2. **Get the headline numbers** — `getBirdseyeSummary` (`GET /v1/log/birdseye`)
   for the period totals.
3. **Get the chart** — `getTrafficLog` (`GET /v1/log`) with `pid`, `timeBucket`
   and `period`. Returns `{params, chart, customs, properties, appliedFilters}`.
   `chart.concurrency` is only populated when the request sets
   `includeConcurrency=true`, and it is zero-filled whenever filters are applied
   or the range exceeds a year — do not report it as "zero live visitors".
4. **Who is on the site right now** — `getLiveVisitors` (`GET /v1/log/live-visitors`).
5. **Navigation** — `getUserFlow` (`GET /v1/log/user-flow`); search terms —
   `getKeywords` (`GET /v1/log/keywords`).
6. **Speed** — `getPerformanceBirdseye` then `getPerformanceLog`. Pick a `measure`:
   `median` (default), `average`, `p95`, or `quantiles` (returns load time across
   p50/p75/p95 instead of the individual metrics).
7. **Sessions** — `listSessions` (`GET /v1/log/sessions`) then `getSession`
   (`GET /v1/log/session`) for one visitor's activity.
8. **Errors** — `getErrorOverview`, then `listErrors`, then `getError`.
9. **Product events** — `getCustomEvents` (`GET /v1/log/custom-events`).

## Parameter vocabulary — the API rejects anything else

- `timeBucket`: `minute`, `hour`, `day`, `week`, `month`, `year`.
- `period`: `1h`, `today`, `yesterday`, `1d`, `7d`, `4w`, `3M`, `12M`, `24M`, `all`.
- For a custom range use `from` + `to` together **instead of** `period`.
- `timezone`: any IANA zone; default `Etc/GMT`.
- `filters`: an array of
  `{"column": "cc", "filter": "GB", "isExclusive": false, "isContains": false}`.
  Legal columns: `cc rg ct host pg lc br brv os osv dv ref so me ca te co isp og ut ctp`.

## Rules

- **Prefer v2 when you need one thing.** `https://swetrix.com/docs/api/stats-v2`
  documents a per-dimension read API at `/v2/projects/{pid}/...` with a
  `{data, meta}` envelope, `limit`/`offset` + `meta.total` pagination and
  `sort=field:direction`. It is additive — v1 keeps working. v2 is **not** modelled
  in `openapi/`, so call it from the documentation, not from a spec operationId.
- **Rate limits.** 300/hour Standard, 6,000/hour Plus. `429` on exhaustion, no
  rate-limit headers. Batch your reads; do not poll `getLiveVisitors` in a loop.
- **v1 has no pagination.** It returns whole aggregated documents. Narrow with
  `period`/`from`+`to` and `filters` rather than paging.
- Errors use `{"statusCode","message","error"}`, not problem+json.
