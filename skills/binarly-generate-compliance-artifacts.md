---
name: Generate SBOM/VEX/CBOM compliance artifacts
description: Export supply-chain assurance artifacts for a scanned Binarly image — SBOM, VEX, CBOM, and findings reports.
api: openapi/binarly-openapi-original.yml
operations: [GetSbomReportCycloneDX, GetSbomReportSPDX, GetVexReportOpenVEX, GetCbomReport, ImageFindingsReportJson]
---

# Generate SBOM/VEX/CBOM compliance artifacts

For an already-scanned image (you need its `productId` and `imageId`), export the artifacts procurement and regulators ask for.

## Auth
- Bearer JWT from Keycloak (see the scan skill). Base URL `https://dashboard-{slug}.binarly.cloud/api/v4`.

## Steps
1. **GetSbomReportCycloneDX** — `GET /api/v4/products/{productId}/images/{imageId}/sbomReport:cycloneDX`.
2. **GetSbomReportSPDX** — `GET /api/v4/products/{productId}/images/{imageId}/sbomReport:SPDX`.
3. **GetVexReportOpenVEX** — `GET /api/v4/products/{productId}/images/{imageId}/vexReport:openVEX` (exploitability status per component).
4. **GetCbomReport** — `GET /api/v4/products/{productId}/images/{imageId}/cbomReport:cycloneDX` (cryptographic bill of materials; feeds PQC readiness).
5. **ImageFindingsReportJson** — `POST /api/v4/products/{productId}/images/{imageId}/findingsReport:json` for the machine-readable findings report.

## Notes
- A CycloneDX VEX variant (`GetVexReportCycloneDX`) and a PDF findings report (`ImageFindingsReportPdf`) are also available.
- Reports may return `422` if analysis is not yet complete — poll the scan first.
- See `arazzo/binarly-compliance-artifacts.yml` for the runnable workflow.
