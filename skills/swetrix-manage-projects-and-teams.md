---
name: Manage Swetrix projects, organisations, funnels, views and annotations
description: Administer a Swetrix account through the Admin API — projects, organisations and members, conversion funnels, saved views and chart annotations.
api: openapi/swetrix-projects-api-openapi.yml, openapi/swetrix-organisations-api-openapi.yml, openapi/swetrix-funnels-api-openapi.yml, openapi/swetrix-views-api-openapi.yml, openapi/swetrix-annotations-api-openapi.yml
operations: [listProjects, createProject, getProject, updateProject, deleteProject, pinProject, unpinProject, listOrganisations, createOrganisation, getOrganisation, updateOrganisation, deleteOrganisation, inviteOrganisationMember, updateOrganisationMember, removeOrganisationMember, listFunnels, createFunnel, updateFunnel, deleteFunnel, getFunnelAnalysis, listViews, createView, getView, updateView, deleteView, listAnnotations, createAnnotation, updateAnnotation, deleteAnnotation]
generated: '2026-08-13'
method: generated
source: >-
  openapi/*.yml (every operationId verified present), plus
  https://swetrix.com/docs/admin-api and
  https://swetrix.com/docs/teams-api-integrations
---

# Manage Swetrix projects, organisations, funnels, views and annotations

Every operation here is under `/v1` on `https://api.swetrix.com` and **requires**
the `X-Api-Key` header. These are destructive-capable operations — read before
you write.

## Projects

- `listProjects` (`GET /v1/project`) → `getProject` (`GET /v1/project/{id}`).
- `createProject` (`POST /v1/project`), `updateProject` (`PUT /v1/project/{id}`),
  `deleteProject` (`DELETE /v1/project/{id}`).
- `pinProject` / `unpinProject` are dashboard ordering only, not access control.

**`deleteProject` is irreversible** — Swetrix states that deleted data is
permanently and irreversibly removed. Confirm with the caller before invoking it,
and never call it to "clean up" after a failed write.

## Organisations and members

- `listOrganisations`, `createOrganisation`, `getOrganisation`,
  `updateOrganisation`, `deleteOrganisation`.
- `inviteOrganisationMember` (`POST /v1/organisation/{orgId}/invite`),
  `updateOrganisationMember`, `removeOrganisationMember`.
- Roles are **Admin** (manage settings, members and projects) and **Viewer**
  (read projects and analytics only). Grant Viewer unless Admin is explicitly asked for.
- Assigning a project to an organisation is `PATCH /v1/project/{id}/organisation`,
  documented in the Admin API reference but **not modelled in `openapi/`** — do
  not call it as a spec operationId.

## Funnels, views, annotations

- Funnels: `listFunnels` (`GET /v1/project/funnels/{pid}`), `createFunnel`,
  `updateFunnel`, `deleteFunnel`. Read the results with `getFunnelAnalysis`
  (`GET /v1/log/funnel`) — a statistics endpoint, not an admin one.
- Saved views / segments: `listViews`, `createView`, `getView`, `updateView`,
  `deleteView` under `/v1/project/{pid}/views`.
- Chart annotations: `listAnnotations`, `createAnnotation`, `updateAnnotation`,
  `deleteAnnotation`.

## Rules

- **Watch the mixed path shapes.** Deletes for funnels and annotations take two
  path segments (`/v1/project/funnel/{id}/{pid}`,
  `/v1/project/annotation/{id}/{pid}`) while views nest under the project
  (`/v1/project/{pid}/views/{viewId}`). Build the URL from the spec, not by analogy.
- **No idempotency key on writes.** Only `POST /log/revenue` has one
  (`transactionId`). A retried `createProject` or `createFunnel` creates a
  **second** object — check with the matching `list*` operation before retrying a
  create whose response you did not see.
- **Alerts and notification channels are dashboard-only.** There are no public
  endpoints for alert or channel CRUD; see `asyncapi/swetrix-alerts-webhooks.yml`.
- Errors use `{"statusCode","message","error"}`. `401` = missing/invalid key,
  `403` = the key cannot manage this project, `404` = wrong identifier.
