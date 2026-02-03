# Gap Analysis Automation Platform — Technical Proposal
### Veteran Vectors | Defense Contractor Executive Briefing

---

## Slide 1: Title

**Gap Analysis Automation Platform**
Containerized Survey-to-Insight Pipeline with Classified Deployment Path

*Veteran Vectors — 6-Month Milestone-Based Engagement*
*Unclassified → Secret → TS/SCI via Game Warden*

---

## Slide 2: Current State — Technical Debt

**Existing Architecture:**
```
Microsoft Forms → Excel → Power Automate (10+ flows) → Power BI → Manual Reports
```

**Technical Problems:**
- Excel-to-Power BI ODBC connections break on schema changes — requires manual re-mapping
- 10+ siloed Power Automate flows with no version control or shared state
- No programmatic report generation — analysts manually compile outputs
- Copilot/AI features require internet egress — blocked on classified networks
- Zero containerization — no path to Game Warden or Iron Bank
- Single-operator knowledge silo — undocumented tribal knowledge

---

## Slide 3: Proposed Architecture

**Target Stack:**
```
n8n (workflow engine) → PostgreSQL 16 → NGINX (reverse proxy) → Power BI/Metabase
         ↓                    ↓                ↓
    Docker/Helm         Persistent Volume    TLS termination
         ↓                    ↓                ↓
    Game Warden K8s    AWS RDS or self-hosted   STIG-hardened
```

**Key Technical Decisions:**
- **n8n** replaces Power Automate — open-source, self-hosted, visual workflow builder
- **PostgreSQL** replaces Excel — ACID-compliant, no connection fragility
- **Docker → Helm/K8s** — portable containers, Game Warden compatible
- **NGINX** — TLS 1.2+, HSTS, CSP, rate limiting, reverse proxy

---

## Slide 4: Delivery Model — Container Images, Not SaaS

**What you receive:**
- Docker Compose files (Black tier)
- Helm charts + values.yaml (Yellow/Red tiers)
- Pre-built container images (n8n, PostgreSQL 16, NGINX)
- All 5 n8n workflow JSON exports
- Infrastructure-as-Code (Terraform/CloudFormation templates)
- Source code for custom integrations

**Deployment model:**
- **Black:** `docker-compose up` on any Docker host (AWS GovCloud, on-prem)
- **Yellow/Red:** `helm install` on Game Warden K8s cluster

**Ownership:** Client owns all artifacts. No VV-hosted infrastructure. No subscription.

---

## Slide 5: Technology Stack — Component Detail

| Component | Tool | Version | License | Iron Bank Status |
|---|---|---|---|---|
| Workflow Engine | n8n | 1.x (latest stable) | Sustainable Use | Requires submission |
| Database | PostgreSQL | 16.x | PostgreSQL License | ✓ In Iron Bank |
| Reverse Proxy | NGINX | 1.25.x | BSD 2-Clause | ✓ In Iron Bank |
| Container Runtime | Docker / containerd | — | Apache 2.0 | N/A (host-level) |
| K8s Package Manager | Helm | 3.x | Apache 2.0 | N/A (tooling) |
| BI Dashboard | Metabase or Power BI | — | AGPL / Commercial | Metabase requires submission |

**Dependency note:** n8n runs on Node.js 18 LTS. Dependency tree includes ~800 npm packages. CVE remediation scoped in MS2 budget.

---

## Slide 6: Five Core Workflows — Functional Specification

| # | Workflow | Trigger | Input | Output | Complexity |
|---|---|---|---|---|---|
| 1 | Survey Distribution | Cron / manual | Roster CSV, survey template | Emails sent, tracking records | Medium |
| 2 | Form Submission Handler | Webhook POST | JSON payload | Validated record in PostgreSQL | Low |
| 3 | Data Processing & Analytics | On-demand / scheduled | Raw responses | Likert scores, NPS, factor analysis, trends | High |
| 4 | Report Generator | On-demand | Processed data | Markdown/PDF report with top-10 gaps | High |
| 5 | Lifecycle Manager | Cron | Survey config | Auto open/close, analyst notifications | Medium |

**Data flow:** Webhook → Validation → PostgreSQL → Analytics → Report → Dashboard

---

## Slide 7: Game Warden — Platform Architecture

**What Game Warden provides:**
- DoD-accredited PaaS on AWS GovCloud (IL2-IL6) and AWS Secret/TS regions
- Managed Kubernetes clusters with inherited ATO
- Automated security scanning pipeline: ClamAV → Anchore → STIG validation
- Cross-domain transfer via AWS Diode (unclass → Secret → TS)

**Deployment pipeline:**
```
git push → CI/CD → ClamAV scan → Anchore CVE scan → STIG check → Stage → Promote
```

**ATO inheritance:** Applications deployed on Game Warden inherit the platform ATO. No standalone 6-18 month certification process.

**Vendor:** Second Front Systems (https://secondfront.com)

---

## Slide 8: Classification Tiers — Impact Levels

| Tier | Impact Level | Network | Hosting | ATO Path |
|---|---|---|---|---|
| **Black** | IL2-IL4 | Commercial / GovCloud | Docker on EC2 or EKS | cATO via Game Warden or self-managed |
| **Yellow** | IL5-IL6 | SIPRNet | Game Warden on AWS Secret Region | Inherited ATO |
| **Red** | TS/SCI | JWICS | Game Warden on AWS Top Secret Region | Inherited ATO |

**Cross-domain promotion:** Container images built once, transferred via AWS Diode, re-scanned at each tier.

---

## Slide 9: Engagement Structure — Milestones

**6-Month Timeline:**

| Milestone | Months | Deliverable | Gate Criteria |
|---|---|---|---|
| **MS1: Black MVP** | 1-2 | Working prototype on unclassified | March event UAT with ~15 users |
| **MS2: Yellow Ops** | 2-4 | Operational on SIPRNet | Game Warden deployment, compliance docs |
| **MS3: Red Ops** | 4-6 | Operational on JWICS | AWS Diode transfer, TS acceptance |

**Overlap:** MS2 prep begins during MS1 (Game Warden onboarding, Iron Bank submission).

---

## Slide 10: Milestone 1 — Black MVP (Months 1-2)

**Technical Deliverables:**
- n8n + PostgreSQL 16 + NGINX in Docker Compose
- All 5 workflows operational with sample data
- PostgreSQL schema: `surveys`, `responses`, `demographics`, `gaps`, `reports`
- Google Sheets/Excel Online webhook integration (optional, for familiar UX)
- Power BI DirectQuery connector or Metabase dashboards
- TLS configuration, basic auth, rate limiting

**Documentation:** Architecture diagram, operator runbook, workflow modification guide

**Validation:** End-to-end test at March event (~15 users, live data)

**Cost:** $20K-$31K development + ~$200/mo infrastructure

---

## Slide 11: Milestone 2 — Yellow / Secret (Months 2-4)

**Technical Deliverables:**
- Helm chart conversion (Deployment, Service, PVC, ConfigMap, Secret)
- Iron Bank image submission for n8n (Dockerfile hardening, CVE remediation)
- Game Warden CI/CD pipeline configuration
- External API dependencies removed (no Google Sheets, no commercial SMTP)
- Classified email relay integration (org-specific)
- STIG hardening applied to all containers

**Compliance Artifacts:** System Security Plan (SSP), Plan of Action & Milestones (POA&M)

**Validation:** SIPRNet end-to-end testing with client personnel

**Cost:** $23K-$40K development + $3.5K-$9.5K/mo infrastructure (Game Warden fee)

---

## Slide 12: Milestone 3 — Red / TS/SCI (Months 4-6)

**Technical Deliverables:**
- AWS Diode cross-domain transfer configuration
- Container image promotion to AWS Top Secret Region
- SCI compartment access controls (if applicable)
- Enhanced audit logging (all CRUD operations, auth events)
- Air-gapped dependency bundling (no external package fetches)

**Compliance Artifacts:** TS-specific SSP addendum, ICD 503 alignment (if required)

**Validation:** JWICS operational acceptance testing

**Cost:** $30K-$62K development + $10K-$19K/mo infrastructure (TS region premium)

---

## Slide 13: Classified Testing Model

**Challenge:** VV operator holds TS/SCI but is not currently sponsored under client's FCL.

**Primary Model — Client-Executed Testing:**
1. VV delivers test scripts, deployment runbooks, validation checklists
2. Client's cleared personnel execute on SIPRNet/JWICS
3. VV provides real-time support from unclassified (phone, screen share of unclass replica)
4. Issues resolved on unclass, re-delivered as updated container images

**Backup Model — Sponsored Access:**
- Client sponsors VV operator's existing clearance onto their program
- VV tests directly on classified networks
- Initiate sponsorship request at contract award as parallel track

---

## Slide 14: Security & Compliance Architecture

| Control Family | Implementation |
|---|---|
| **Access Control (AC)** | RBAC in n8n, PostgreSQL row-level security, NGINX basic auth |
| **Audit & Accountability (AU)** | PostgreSQL audit triggers, n8n execution logs, NGINX access logs |
| **Configuration Management (CM)** | IaC (Helm/Terraform), immutable containers, GitOps |
| **Identification & Authentication (IA)** | TLS client certs (optional), integration with org IdP |
| **System & Communications Protection (SC)** | TLS 1.2+, encrypted volumes, network segmentation |
| **System & Information Integrity (SI)** | ClamAV, Anchore CVE scanning, STIG baseline |

**Frameworks:** CMMC Level 2, NIST 800-171, FedRAMP-authorized infrastructure (via Game Warden), DISA STIGs

---

## Slide 15: Pricing — Tool Development

### One-Time Development Costs

| Milestone | Scope | Cost Range |
|---|---|---|
| MS1: Black MVP | Workflows, Docker, testing, training | $20,000 - $31,000 |
| MS2: Yellow | Helm, Iron Bank, Game Warden, compliance | $23,000 - $40,000 |
| MS3: Red | Diode, TS hardening, compliance, pen test support | $30,000 - $62,000 |
| **Total** | | **$73,000 - $133,000** |

### Veteran Vectors Services

| Item | Amount |
|---|---|
| **VV Development Fee** | **$60,000** (flat, 6-month engagement) |
| **VV Monthly Retainer** | **Option A or B** (see Slide 19) |

---

## Slide 16: Pricing — Infrastructure

| Tier | Monthly Cost | Components |
|---|---|---|
| **Black** | $130 - $270/mo | EC2 t3.medium, RDS micro or self-hosted, S3, SES |
| **Yellow** | $3,500 - $9,500/mo | Game Warden platform fee + GovCloud Secret compute |
| **Red** | $10,000 - $19,000/mo | Game Warden TS fee + AWS Top Secret Region compute |

**Year 1 Infrastructure (assuming staggered deployment):**

| Tier | Months Active | Annual Cost |
|---|---|---|
| Black (all year) | 12 | $1,560 - $3,240 |
| Yellow (Month 3+) | 10 | $35,000 - $95,000 |
| Red (Month 5+) | 8 | $80,000 - $152,000 |
| **Total** | | **$116,560 - $250,240** |

---

## Slide 17: Total Investment — Year 1

| Category | Low | High |
|---|---|---|
| Tool Development | $73,000 | $133,000 |
| Infrastructure | $116,560 | $250,240 |
| VV Development Fee | $60,000 | $60,000 |
| VV Retainer (10 months)* | $12,000 | $43,160 |
| **Total Year 1** | **$261,560** | **$486,400** |

*Retainer range reflects Option A (15% of infra) vs Option B (hourly). See Slide 19.

**Midpoint estimate:** ~$374,000

**Context:** Game Warden fees replace $200K-$500K standalone ATO cost and 6-18 months of calendar time.

---

## Slide 18: Payment Schedule

| Event | Trigger | Tool Dev | VV Fee |
|---|---|---|---|
| Contract Award | Signed | 20% ($14.6K-$26.6K) | 30% = **$18,000** |
| MS1 Accepted | March UAT | 30% ($21.9K-$39.9K) | 25% = **$15,000** |
| MS2 Operational | SIPRNet live | 30% ($21.9K-$39.9K) | 20% = **$12,000** |
| MS3 Operational | JWICS live | 20% ($14.6K-$26.6K) | 25% = **$15,000** |

**Retainer:** Option A or B, starting Month 3 (see Slide 19)

**Infrastructure:** Billed monthly by AWS/Game Warden, pass-through to client

---

## Slide 19: VV Retainer Options — Starting Month 3

### Option A: Percentage of Infrastructure (Scales with Deployment)

**15% of monthly infrastructure costs**

| Deployment State | Monthly Infra | VV Retainer (15%) |
|---|---|---|
| Black only | $130 - $270 | $20 - $41 |
| Black + Yellow | $3,630 - $9,770 | $545 - $1,466 |
| All three tiers | $13,630 - $28,770 | $2,045 - $4,316 |

**Year 1 estimate (Months 3-12):** ~$17,450 - $37,460

### Option B: Hourly with Monthly Minimum

**$150/hour with 8-hour monthly minimum**

| Item | Amount |
|---|---|
| Monthly minimum | $1,200/mo |
| Hours above minimum | $150/hr |
| Year 1 estimate (10 months) | $12,000 minimum |

### What Both Options Cover

- CVE monitoring and container image rebuilds
- Incident response and troubleshooting
- Workflow modifications
- Quarterly architecture reviews
- Compliance posture updates

---

## Slide 20: Government-Ready Product

**For downstream sale to government entity:**

| Requirement | VV Deliverable |
|---|---|
| **Data Rights** | Unlimited rights to custom code, configs, Helm charts. OSS licenses documented. |
| **Section 508** | WCAG 2.1 AA compliance for forms/dashboards |
| **SBOM** | CycloneDX/SPDX software bill of materials at each milestone |
| **CMMC/NIST 800-171** | SSP, POA&M delivered at MS2/MS3 |
| **ATO** | Game Warden inherited — no standalone certification |
| **Transition Plan** | Full code, IaC, docs, training delivered at each gate |

**Contractor handles:** SAM.gov, FAR/DFARS, contract vehicle, CDRLs, CO relationship

---

## Slide 21: Risk Matrix

| Risk | Severity | Mitigation |
|---|---|---|
| Game Warden onboarding delays | **High** | Begin coordination Month 1. Pre-approved container patterns. |
| n8n Iron Bank rejection | **Medium** | Prepare hardened image during Black. Waiver fallback. |
| CVE count exceeds budget | **Medium** | Budget upper range ($6K). Pin stable deps. |
| Classified testing coordination | **Medium** | Client-executed with VV scripts. Sponsor access as backup. |
| AWS Diode transfer issues | **Medium** | Engage AWS SA during Yellow. Validate in staging. |
| Power BI unavailable on classified | **Medium** | Metabase built as drop-in fallback. |
| Scope creep | **Medium** | Milestone gates with defined acceptance criteria. |

---

## Slide 22: Technical Dependencies & Assumptions

**Dependencies:**
- Client provides AWS GovCloud account access (Black)
- Client has or obtains Game Warden contract (Yellow/Red)
- Client provides classified email relay configuration
- Client personnel available for classified testing windows

**Assumptions:**
- n8n dependency tree CVE count within normal range (~$3K-$6K remediation)
- No custom SCI compartment logic beyond standard RBAC
- Existing Power BI dashboards can be preserved or Metabase is acceptable
- March event timeline is firm (drives MS1 completion)

---

## Slide 23: Timeline — Gantt View

```
Month:        1         2         3         4         5         6
              |---------|---------|---------|---------|---------|
MS1 Black:    [=========BUILD==========][UAT]
MS2 Yellow:             [--PREP--][=======BUILD=======][DEPLOY]
MS3 Red:                                    [--PREP--][===BUILD===][ACCEPT]
Game Warden:  [====ONBOARD====]
Iron Bank:              [=====SUBMIT=====]
Retainer:                         [=====Option A or B=====]
```

**Critical path:** Game Warden onboarding and Iron Bank submission run in parallel with MS1 to avoid blocking MS2.

---

## Slide 24: Next Steps

1. **Contract execution** — Single 6-month engagement, milestone-gated payments
2. **Week 1 onboarding** — Access to existing Power Automate flows, Excel data, Power BI
3. **Week 1 parallel track** — Initiate Game Warden onboarding, clearance sponsorship request
4. **Months 1-2** — MS1 Black MVP build → March event UAT
5. **Months 2-4** — MS2 Yellow build → SIPRNet deployment
6. **Months 4-6** — MS3 Red build → JWICS acceptance
7. **Month 3+** — Retainer active (Option A or B)

**Deliverable at each gate:** Working system, source code, IaC, documentation, training

---

## Slide 25: Contact

**Veteran Vectors**

*Single contract. Three milestones. Full classified deployment in 6 months.*

---
