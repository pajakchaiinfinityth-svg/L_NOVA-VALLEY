# Master Index / ดัชนีหลัก (SYNCERA PJ VALLEY)

## 1) Master Index (TH/EN)
| File | Category | Priority | Status | Purpose |
| --- | --- | --- | --- | --- |
| README.md | Public Info | Primary | Active | Top-level project label ("L_NOVA-VALLEY"), placeholder brand marker "Humanic Master". |
| docs/master_index.md | Metadata / Index | Primary | Active | Repository catalog and knowledge map. |
| docs/pj_autostructure_plan.md | Business / Reports | Primary | Active | Gate 0→Day 90 bilingual autostructure covering scope, architecture, data, UX, API, tests, and deployment. |
| docs/raw_html/pajakchai_portfolio.html | Resume / Profile | Primary | Active | Humanic HPE HTML dossier/resume for Pajakchai (PJ) Thongchai; bilingual executive portfolio with indices and scoring matrices. |

> หมายเหตุ: หากมีไฟล์ใหม่ กรุณาอัปโหลดเพื่ออัปเดตดัชนีและ Knowledge Map.

## 2) Table of Contents / สารบัญ
1. Master Index (นี้)
2. Knowledge Map
3. Suggested Directory Structure
4. Category Summaries
5. Open Questions / รายการข้อมูลที่ต้องการเพิ่ม

## 3) Knowledge Map
### File → Category / Purpose / Relation / Status
| File | Category | Purpose | Relation | Status | Priority |
| --- | --- | --- | --- | --- | --- |
| README.md | Public Info | Identifies project name and a brand marker; currently minimal. | Root entry point; expected to link to future docs. | Active | Primary |
| docs/master_index.md | Metadata / Index | Maintains catalog of repository contents. | References README, autostructure plan, and portfolio HTML. | Active | Primary |
| docs/pj_autostructure_plan.md | Business / Reports | Summarizes requirements, architecture, UX, API, tests, deployment, and risks for Gate 0→Day 90. | Builds on user-provided brief; informs future BRD/SRS and engineering scaffolds. | Active | Primary |
| docs/raw_html/pajakchai_portfolio.html | Resume / Profile | Bilingual Humanic HPE dossier/resume for PJ; contains index, comparative overlays, legal/gov notes, and scoring matrices. | Connects to policy/legal/governance narratives and Win4U MVP storyline; acts as Raw HTML prototype for résumé view. | Active | Primary |

## 4) Suggested Directory Structure (Proposed) / โครงสร้างโฟลเดอร์แนะนำ
```
/
├─ README.md                      # Project overview (Public Info)
├─ docs/
│  ├─ master_index.md            # Catalog
│  ├─ pj_autostructure_plan.md   # Gate 0→Day 90 plan
│  ├─ requirements/              # BRD/SRS (Business / Reports)
│  ├─ privacy/                   # Privacy / Legal / Compliance
│  ├─ hpe-framework/             # HPE Framework assets
│  ├─ ux/                        # Persona, journey maps, wireframes (Raw HTML / Prototype)
│  ├─ architecture/              # System diagrams (HPE Framework / Engineering)
│  └─ governance/                # Ethics, audit logs (Policy / Compliance)
├─ apps/
│  ├─ web/                       # Frontend app (Public UI)
│  ├─ api/                       # Backend/API services
│  └─ data/                      # Schemas, migrations (Data Model)
├─ infra/                        # IaC, CI/CD (DevOps)
├─ reports/                      # KPI, finance, pilot reports (Business / Reports)
└─ archive/                      # Legacy / Temp / Archive
```

## 5) Category Summaries / สรุปหมวดหมู่
- **Public Info**: README.md (Active, Primary). High-level project identity; needs expansion to cover scope, milestones, and contacts.
- **Resume / Profile**: `docs/raw_html/pajakchai_portfolio.html` (Active, Primary). HTML dossier/resume with bilingual content and scoring matrices.
- **HPE Framework**: _None yet._ Will contain process/framework references once provided.
- **Privacy / Legal / Compliance**: _None yet._ Expected to store PDPA/DPIA, consent models, audit policies.
- **Metadata / Index**: `docs/master_index.md` (Active, Primary). Maintains catalog of repository contents.
- **Business / Reports**: `docs/pj_autostructure_plan.md` (Active, Primary). Captures scope, architecture, API, test, deployment plan.
- **Raw HTML / Prototype**: `docs/raw_html/pajakchai_portfolio.html` (Active, Primary). Printable/HTML résumé layout; can serve as prototype for portfolio microsite.
- **Legacy / Temp / Archive**: _None yet._ For deprecated or temporary assets.

## 6) Open Questions / รายการข้อมูลที่ต้องการเพิ่ม
1. มีเอกสาร BRD/SRS, DPIA, Ethics Charter, UX flows หรือ prototype ที่ต้องอัปโหลดหรือไม่?
2. มีข้อมูลภายนอก (API keys, data contracts, telemetry sources) ที่ต้อง map เข้ามาหรือไม่?
3. ต้องการเพิ่มหมวดหมู่หรือปรับโครงสร้างโฟลเดอร์จากข้อเสนอหรือไม่?
