# Swetrix (swetrix)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Swetrix is an open source, privacy-focused web analytics platform that provides cookieless tracking, real-time dashboards, and GDPR-compliant analytics without collecting personal data. It offers a fully-featured REST API for tracking events, querying statistics, managing projects, and integrating analytics into custom applications.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/swetrix/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/swetrix/refs/heads/main/apis.yml)

## Scope

- **Type:** Index

## Tags

- Analytics
- Cookieless Tracking
- GDPR Compliant
- Open Source
- Privacy
- Real-Time Analytics
- Web Analytics

## Timestamps

- **Created:** 2026-03-26
- **Modified:** 2026-05-19

## APIs

### Swetrix Events API

The Swetrix Events API provides endpoints for recording pageview events, custom events, heartbeat events, error events, and revenue transactions. Used for sending analytics data from client or server-side applications to Swetrix analytics projects.

- **Human URL:** [https://swetrix.com/docs/events-api](https://swetrix.com/docs/events-api)
- **Base URL:** `https://api.swetrix.com`

#### Tags

- Analytics
- Cookieless Tracking
- Custom Events
- Error Tracking
- Events
- Pageviews
- Revenue Tracking

#### Properties

- [Documentation](https://swetrix.com/docs/events-api)
- [OpenAPI](https://raw.githubusercontent.com/api-evangelist/swetrix/refs/heads/main/openapi/swetrix-events-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/swetrix-admin-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/swetrix-admin-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/swetrix-events-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/swetrix-events-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/swetrix-statistics-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/swetrix-statistics-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Swetrix Statistics API

The Swetrix Statistics API enables querying aggregated analytics data including traffic logs, performance metrics, session details, funnel analysis, user flows, error overviews, and feature flag statistics. Authenticated with an X-Api-Key header.

- **Human URL:** [https://swetrix.com/docs/statistics-api](https://swetrix.com/docs/statistics-api)
- **Base URL:** `https://api.swetrix.com`

#### Tags

- Analytics
- Funnels
- Performance
- Statistics
- Traffic

#### Properties

- [Documentation](https://swetrix.com/docs/statistics-api)
- [OpenAPI](https://raw.githubusercontent.com/api-evangelist/swetrix/refs/heads/main/openapi/swetrix-statistics-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/swetrix-admin-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/swetrix-admin-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/swetrix-events-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/swetrix-events-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/swetrix-statistics-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/swetrix-statistics-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Swetrix Admin API

The Swetrix Admin API manages projects, funnels, annotations, project views (segments), and organisations. Supports full CRUD operations for analytics project management. Authenticated with an X-Api-Key header.

- **Human URL:** [https://swetrix.com/docs/admin-api](https://swetrix.com/docs/admin-api)
- **Base URL:** `https://api.swetrix.com`

#### Tags

- Administration
- Analytics
- Organisations
- Project Management
- Projects

#### Properties

- [Documentation](https://swetrix.com/docs/admin-api)
- [OpenAPI](https://raw.githubusercontent.com/api-evangelist/swetrix/refs/heads/main/openapi/swetrix-admin-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/swetrix-admin-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/swetrix-admin-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/swetrix-events-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/swetrix-events-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/swetrix-statistics-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/swetrix-statistics-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [LinkedIn](https://www.linkedin.com/company/swetrix)
- [Website](https://swetrix.com)
- [Documentation](https://docs.swetrix.com)
- [Blog](https://swetrix.com/blog)
- [Pricing](https://swetrix.com/pricing)
- [Git Hub](https://github.com/Swetrix/swetrix)
- [GitHub Organization](https://github.com/Swetrix)
- [Login](https://swetrix.com/login)
- [Sign Up](https://swetrix.com/signup)
- [Support](https://swetrix.com/contact)
- [Open Source](https://github.com/Swetrix/swetrix-api)
- [SDK](https://github.com/Swetrix/swetrix-js)
- [SDK](https://github.com/Swetrix/swetrix-nextjs)
- [SDK](https://github.com/Swetrix/swetrix-browser)
- [SDK](https://github.com/Swetrix/django-plugin)
- [Status Page](https://swetrix.com/status)
- [Terms of Service](https://swetrix.com/privacy)
- [Privacy Policy](https://swetrix.com/privacy)
- [L L Ms Txt](https://swetrix.com/llms.txt)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
