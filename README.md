# Swetrix

Swetrix is an open source, privacy-focused web analytics platform providing cookieless tracking, real-time dashboards, and GDPR-compliant analytics without collecting personal data. It offers a fully-featured REST API for tracking events, querying statistics, managing projects, and integrating analytics into custom applications.

- **Website:** https://swetrix.com
- **Documentation:** https://docs.swetrix.com
- **GitHub:** https://github.com/Swetrix/swetrix
- **Pricing:** https://swetrix.com/pricing

## APIs

### Swetrix Events API
Records pageview events, custom events, heartbeat sessions, JavaScript errors, and revenue transactions. Most endpoints are public (project ID only); the revenue endpoint requires an API key.

- **Documentation:** https://swetrix.com/docs/events-api
- **OpenAPI:** [openapi/swetrix-events-api-openapi.yml](openapi/swetrix-events-api-openapi.yml)

### Swetrix Statistics API
Queries aggregated analytics data including traffic logs, performance metrics, session details, funnel analysis, user navigation flows, error statistics, and feature flag evaluations. Requires API key.

- **Documentation:** https://swetrix.com/docs/statistics-api
- **OpenAPI:** [openapi/swetrix-statistics-api-openapi.yml](openapi/swetrix-statistics-api-openapi.yml)

### Swetrix Admin API
Manages projects, funnels, annotations, project views (segments), and organisations with full CRUD operations. Requires API key.

- **Documentation:** https://swetrix.com/docs/admin-api
- **OpenAPI:** [openapi/swetrix-admin-api-openapi.yml](openapi/swetrix-admin-api-openapi.yml)

## Artifacts

| Type | Path |
|---|---|
| OpenAPI Specs | [openapi/](openapi/) |
| Spectral Rules | [rules/swetrix-rules.yml](rules/swetrix-rules.yml) |
| Naftiko Capabilities | [capabilities/](capabilities/) |
| JSON Schema | [json-schema/](json-schema/) |
| JSON Structure | [json-structure/](json-structure/) |
| JSON-LD Context | [json-ld/swetrix-context.jsonld](json-ld/swetrix-context.jsonld) |
| Examples | [examples/](examples/) |
| Vocabulary | [vocabulary/swetrix-vocabulary.yml](vocabulary/swetrix-vocabulary.yml) |

## Naftiko Capabilities

### Shared Definitions
- [capabilities/shared/swetrix-events.yaml](capabilities/shared/swetrix-events.yaml) — Events API consumer
- [capabilities/shared/swetrix-statistics.yaml](capabilities/shared/swetrix-statistics.yaml) — Statistics API consumer
- [capabilities/shared/swetrix-admin.yaml](capabilities/shared/swetrix-admin.yaml) — Admin API consumer

### Workflow Capabilities
- [capabilities/web-analytics.yaml](capabilities/web-analytics.yaml) — Unified web analytics workflow (Events + Statistics + Admin, REST port 8080, MCP port 9090, 14 tools)

## Authentication

- **Events API:** Public (project ID only); Revenue endpoint requires `X-Api-Key` header
- **Statistics API:** `X-Api-Key` header required
- **Admin API:** `X-Api-Key` header required
- Rate limit: 600 requests/hour (free and paid plans)

## Maintainers

- Kin Lane (kin@apievangelist.com)
