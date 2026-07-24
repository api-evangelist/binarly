---
name: Scan firmware in a CI/CD pipeline
description: Upload a firmware or binary image to the Binarly Transparency Platform, run a scan, and gate the build on findings.
api: openapi/binarly-openapi-original.yml
operations: [CreateProduct, GenerateTempFileUploadURL, UploadImage, CreateScan, GetScan, GridListFindings]
---

# Scan firmware in a CI/CD pipeline

Use the Binarly Transparency Platform API v4 to scan a build artifact and fail the pipeline on new critical findings.

## Auth
- Obtain a Keycloak M2M token via the `client_credentials` grant at
  `https://auth-{slug}.binarly.cloud/realms/BinarlyRealm/protocol/openid-connect/token`.
- Send `Authorization: Bearer <access_token>` on every request. Tokens expire after 30 minutes — refresh per job.
- Base URL: `https://dashboard-{slug}.binarly.cloud/api/v4` (substitute your org slug).
- SaaS customers request `client_id`/`client_secret` from support@binarly.io.

## Steps
1. **CreateProduct** — `POST /api/v4/products` with `{ "name": "<product>" }`. Reuse an existing `productId` if you have one (skip this step).
2. **GenerateTempFileUploadURL** — `GET /api/v4/products/{productId}/tempFiles:generateUploadUrl` to get a temporary upload URL.
3. **UploadImage** — `POST /api/v4/products/{productId}/images:upload` to register the firmware image; capture `imageId`.
4. **CreateScan** — `POST /api/v4/products/{productId}/images/{imageId}/scans`; capture `scanId`.
5. **GetScan** — poll `GET /api/v4/products/{productId}/images/{imageId}/scans/{scanId}` until the scan completes.
6. **GridListFindings** — `POST /api/v4/grids/findings:gridList` with filters (severity, reachability, risk score). Fail the build when new criticals appear.

## Conventions & errors
- Pagination is offset-based (`skip` / `size`).
- Errors are `{ "message": ..., "details": [...] }`; `403` names the missing RBAC `permission` and `resourceName`.
- Retry `500`/`502` with backoff; refresh the token on `401`.
- See `conventions/binarly-conventions.yml` and `errors/binarly-problem-types.yml`.
