---
name: Triage and prioritize findings
description: List, inspect, and manage the state of Binarly Transparency Platform findings using risk, reachability, and exploitability signals.
api: openapi/binarly-openapi-original.yml
operations: [GridListFindings, GetFinding, FindingAdvisory, CreateFindingState, ListVulnerabilities]
---

# Triage and prioritize findings

Work the findings queue for a product, focusing on what is actually reachable and exploitable.

## Auth
- Bearer JWT from Keycloak. Base URL `https://dashboard-{slug}.binarly.cloud/api/v4`.

## Steps
1. **GridListFindings** — `POST /api/v4/grids/findings:gridList`. Filter by CVSS range, EPSS, EMS (Exploitation Maturity Score), KEV, known-ransomware-use, has-known-fix, and code/environment reachability to rank by real risk.
2. **GetFinding** — `GET /api/v4/products/{productId}/findings/{findingId}` for full detail.
3. **FindingAdvisory** — `GET /api/v4/products/{productId}/findings/{findingId}/advisory` for the advisory writeup.
4. **CreateFindingState** — `POST /api/v4/products/{productId}/findings/{findingId}/CreateFindingState` to set triage state (e.g. accepted, false-positive).
5. **ListVulnerabilities** — `GET /api/v4/vulnerabilities` to cross-reference the CVE/advisory database.

## Prioritization signals
- Binarly Risk Score (0–1), EMS (0–10), reachability (code + environment), KEV, and ransomware-use flags are all queryable filters on the findings grid.
- See `data-model/binarly-data-model.yml` for how findings relate to products, images, scans, and components.
- Errors: `403` names the missing RBAC permission; `404` means the finding/product id is not visible to your role.
