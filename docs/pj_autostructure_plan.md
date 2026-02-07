# SYNCERA PJ VALLEY – Gate 0 → Day 90 Autostructure

## 1) Executive Summary
- Establish a lean, bilingual (TH/EN) pilot for mobility + agri/SME stability with auditable ethics, privacy-by-design, and public metrics.
- Target KPIs: ETA median < 8 min, acceptance ≥ 74%, uptime ≥ 96%, CSAT ≥ 4.3/5, household savings & cost/kg reduction.
- Deliver cross-functional readiness: product/UX assets, API/infra scaffold, data/AI evaluators, privacy governance, city pilot ops, and board-ready reporting.

## 2) Requirement & Scope
- **Personas**: Citizen/Rider/Farmer end users; City Ops; Analysts; Developers; Privacy & Governance officers.
- **MVP Functions** (Phase 1):
  - Consent capture (`POST /consent/{userId}`) with purpose-binding and audit log.
  - Mobility ETA retrieval (`GET /mobility/eta`) with simulation fallbacks and SLA metrics.
  - Agri co-op routing (`POST /agri/coop/route`) for pooled logistics.
  - KPI/impact reporting (`GET /kpi/impact`) with public dashboard views (1080p + A4 printable).
  - Bilingual UI themes (Classic/Nova/Neutral) with persona/journey maps and clickable prototype.
- **Non-Functional**: Uptime ≥96%; median ETA <8m; encryption at rest (AES-256)/in transit (TLS1.3); RBAC/ABAC; OpenTelemetry traces/metrics/logs; auditability; PDPA-by-design; privacy incidents = 0.
- **Out-of-scope (initial)**: Production payments clearing, hardware telematics, large-scale ML training (only simulation/evals), multi-region failover (pilot single region).

## 3) System Architecture (textual diagram)
```
Clients (Web, Mobile) --TLS--> API Gateway
  -> FastAPI services (apps/api)
     -> Consent service (purpose-binding, audit_log append-only)
     -> Mobility/Agri service (ETA simulation, routing)
     -> KPI service (impact calculations, dashboard feed)
  -> AuthZ/RBAC-ABAC middleware (policy engine)
  -> Observability (OpenTelemetry exporter → metrics/logs/traces backend)
  -> Privacy middleware (PII tagging, log masking)
Data plane:
  -> Postgres (consent_ledger, audit_log, kpi, mobility cache)
  -> Object store (reports, exports A4/1080p)
  -> Vector store (pgvector) for policy/playbook RAG
Integrations/Stubs:
  -> Maps/Transit, Payments, Education attendance pseudo-ID
Ops:
  -> CI/CD → container registry → IaC (docker/terraform stubs)
  -> Transparency & governance pages (static site)
```

## 4) Data Model / Metadata Schema
- `consent_ledger`: `consent_id (uuid)`, `user_id`, `purpose`, `status`, `timestamp`, `expiry`, `channel`, `evidence_uri`.
- `audit_log`: `event_id`, `actor`, `action`, `resource`, `purpose`, `result`, `hashed_payload`, `created_at`, `immutable_seq` (append-only).
- `mobility_eta_cache`: `request_id`, `user_id`, `origin`, `destination`, `eta_minutes`, `confidence`, `provider`, `sim_version`, `created_at`.
- `agri_route`: `route_id`, `coop_id`, `stops[]`, `load_kg`, `cost_per_kg`, `savings_pct`, `simulation_run_id`.
- `kpi_snapshot`: `snapshot_id`, `period`, `acceptance_rate`, `median_eta`, `uptime_pct`, `csat`, `household_savings`, `cost_per_kg`, `notes`.
- Metadata tagging: `pii=true/false`, `purpose_binding`, `retention_policy`, `consent_ref`, `classification` fields on all tables.

## 5) Folder Structure (proposed)
```
/                      # repo root
├─ README.md           # public intro
├─ docs/
│  ├─ master_index.md
│  ├─ pj_autostructure_plan.md      # this file
│  ├─ requirements/BRD_SRS.md
│  ├─ privacy/privacy_intent.md
│  ├─ ux/personas_journeys.md
│  ├─ architecture/diagrams.md
│  ├─ governance/ethics_charter.md
│  └─ reports/kpi_board_pack.md
├─ apps/
│  ├─ web/   # Next.js+Tailwind+shadcn
│  └─ api/   # FastAPI
├─ packages/
│  ├─ schemas/   # JSON Schema + zod
│  └─ sdk/       # TypeScript client
├─ infra/        # docker, terraform stubs, CI/CD
└─ archive/      # legacy/temp
```

## 6) UX Flows + Wireframes (ASCII)
### Consent & Dashboard (Classic theme)
```
[Landing] -> [Consent Modal]
   -> Accept -> [Dashboard: KPIs cards + ETA widget]
   -> Decline -> [Limited view + contact]
```
### Mobility ETA Request
```
Home -> Origin/Destination fields -> [Get ETA]
   -> Show ETA card (median, range, confidence)
   -> CTA: Book pilot ride / Save route
```
### Agri Co-op Routing
```
Co-op Home -> Add stops -> Load (kg) -> [Simulate]
   -> Route map ascii + savings% + cost/kg
   -> Export A4 / Share link
```
### Admin/Governance
```
Admin Login -> Audit log viewer -> Consent ledger table
   -> Download transparency report -> Privacy tests status
```

## 7) Codebase (files + run commands)
- **Scaffold targets** (to be implemented):
  - `apps/web`: Next.js 14 + Tailwind + shadcn UI; run `npm install && npm run dev`.
  - `apps/api`: FastAPI with routers for consent/mobility/agri/kpi; run `uvicorn main:app --reload`.
  - `packages/schemas`: JSON Schema + zod definitions for request/response DTOs.
  - `packages/sdk`: TS client wrapping OpenAPI 3.1 spec.
- **Mock data**: seed simulation data for ETA and agri routes; provide `.env.example` for API keys.
- **Tooling**: OpenTelemetry instrumentation; pytest for API; Playwright for web flows.

## 8) API Spec (OpenAPI-style sketch)
- `POST /consent/{userId}`: body `{purpose, channel, evidenceUri}`; returns `consentId`, `status`.
- `GET /mobility/eta`: query `origin`, `destination`, optional `mode`; returns `{etaMinutes, confidence, provider, simulated}`.
- `POST /agri/coop/route`: body `{coopId, stops[], loadKg}`; returns `{routeId, savingsPct, costPerKg, waypoints}`.
- `GET /kpi/impact`: query `period`; returns KPI snapshot list + public metrics link.
- Common: headers `x-request-id`, `x-purpose`, auth via RBAC/ABAC token; audit log on all endpoints.

## 9) Test Plan + Acceptance Criteria
- **Unit/API**: pytest for each endpoint (200/4xx/5xx), purpose-binding enforcement, audit_log append-only.
- **E2E (web)**: Playwright flows for consent, ETA request, agri simulation, admin audit download.
- **Performance**: median ETA response < 1s for cache/simulated; uptime check synthetic probes; load test 100 RPS for pilot.
- **Security/Privacy**: PII tagging verified, log masking redaction, TLS checks, RBAC/ABAC role matrix, privacy tests for consent revocation.
- **Acceptance**: KPIs hit (ETA <8m, acceptance ≥74%, uptime ≥96%, CSAT ≥4.3/5), privacy incidents = 0, transparency page live.

## 10) Deployment Guide (pilot-first)
- Dev: Docker compose for api+db+otel collector; seed data on start.
- Staging: CI/CD builds images, runs tests, deploys to single-region container host; attach managed Postgres + object store.
- Prod Pilot: enable TLS1.3, rotate keys, enforce branch protection; nightly backups; observability dashboards; canary routes for APIs.
- Artifacts: publish OpenAPI 3.1, public dashboard static build, weekly eval report (bias/fairness, KPI).

## 11) Risk & Mitigation
- **Incomplete data sources**: start with simulation; flag data contracts per provider; maintain feature toggles.
- **Privacy non-compliance**: enforce purpose-binding middleware + audit_log; run privacy tests in CI.
- **Operational adoption**: weekly city/community review; capture acceptance/cancellation signals; adjust incentives.
- **Reliability during pilot**: SLOs with alerts; caching for ETA; fallback simulators.

## 12) Optional Enhancements
- Voice assistant via Realtime API for ops support.
- Fairness/bias dashboards with weekly evals; red-team drills automation.
- Energy credit telemetry for REC/vPPA narrative and sustainability KPIs.
- Multi-theme token library (Cinzel/Inter) with exportable design kit.
