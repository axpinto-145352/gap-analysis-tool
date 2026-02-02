# Gap Analysis Automation Platform — Integrated Milestone Proposal
### Veteran Vectors | Executive Briefing (20 Slides)

---

## Slide 1: Title

**Gap Analysis Automation Platform**
Secure, Scalable Survey-to-Insight Pipeline for Defense & Intelligence Operations

*Veteran Vectors — 6-Month Milestone-Based Engagement*

---

## Slide 2: The Problem

- Current stack: Microsoft Forms → Excel → Power Automate → Power BI → Manual Reports
- Excel-to-Power BI connections **break constantly**, requiring manual re-mapping
- **10+ siloed Power Automate flows** for simple tasks
- No automated report generation
- AI/narrative features (Copilot) **blocked on classified networks**
- No certification pathway to Secret/TS — tool sits on a shelf
- **Single-operator bottleneck** — system fails without one person

---

## Slide 3: The Solution

Replace the fragile Microsoft patchwork with a **self-hosted automation appliance** packaged in Docker containers:

- **One platform** replaces Forms + Power Automate + VBA scripts
- **PostgreSQL** replaces fragile Excel connections permanently
- **Automated analytics & reports** — no manual calculations
- **Docker containerized** — the entire system (app, DB, web server, workflows) ships as portable container images that run on any Docker or Kubernetes host
- **Game Warden pathway** — inherited ATO in weeks, not 6-18 months

**Delivery model:** This is not SaaS. It's a self-hosted, client-owned appliance. VV builds and packages it; the client owns and operates it on their infrastructure. No vendor dependency, no subscription, no shared tenancy. The same container images move from unclass → Secret → TS without rebuilding.

---

## Slide 4: Before → After

| | Current | Proposed |
|---|---|---|
| Automation | 10+ Power Automate flows | 5 unified n8n workflows |
| Data Store | Excel (fragile) | PostgreSQL (reliable) |
| Reports | Manual | Auto-generated on demand |
| Classified Path | None | Game Warden (IL2 → TS/SCI) |
| Operator Dependency | 1 person | Any trained operator |
| Licensing | Per-user Microsoft fees | Open-source, $0 licensing |

---

## Slide 5: How It Works — 5 Core Workflows

1. **Survey Distribution** — Roster-driven sends + auto-reminders
2. **Form Submission Handler** — Webhook intake, validation, DB storage
3. **Data Processing & Analytics** — Likert/NPS scoring, factor analysis, trend tracking
4. **Report Generator** — Templated consultancy report with top-10 gaps, recommendations
5. **Lifecycle Manager** — Auto open/close surveys, analyst notifications

All 5 workflows built, tested, and handed off as a complete system.

---

## Slide 6: Technology Stack

| Component | Tool | Why |
|---|---|---|
| Automation | n8n (self-hosted) | Open-source, visual, no licensing |
| Database | PostgreSQL 16 | Replaces Excel; reliable, scalable |
| Reverse Proxy | NGINX | TLS, rate limiting, security headers |
| Containers | Docker → Helm/K8s | Portable; Game Warden compatible |
| Dashboard | Power BI or Metabase | Existing BI or open-source fallback |
| Email | SMTP relay | Survey distribution & notifications |

**All open-source or self-hosted. No vendor lock-in. No per-user licensing.**

---

## Slide 7: Engagement Structure — One Contract, Three Milestones

**6-Month Integrated Engagement** with milestone gates at each classification tier:

| Milestone | Tier | Timeline | Gate |
|---|---|---|---|
| **MS1: Black MVP** | Unclassified (IL2-IL4) | Months 1-2 | March event — live test with ~15 users |
| **MS2: Yellow Ops** | Secret (IL5-IL6) | Months 2-4 | Operational on SIPRNet via Game Warden |
| **MS3: Red Ops** | TS/SCI | Months 4-6 | Full deployment on JWICS |

Single contract. Milestone reviews at each gate. Full deliverables at every stage.

---

## Slide 8: Milestone 1 — Black MVP (Months 1-2)

- n8n + PostgreSQL + NGINX deployed in Docker
- All 5 workflows operational end-to-end
- Google Sheets/Excel Online integration for familiar interface
- Optional Power BI connector for existing dashboards
- Integration testing + UAT at March event (~15 users)

**Deliverables:** Working prototype, operator documentation, training

**Tool Development Cost:** $20K - $31K
**Monthly Infra:** ~$130 - $270/mo

---

## Slide 9: Milestone 2 — Yellow / Secret (Months 2-4)

- Kubernetes/Helm conversion for Game Warden pipeline
- All external API dependencies removed (PostgreSQL-only)
- Iron Bank image submission for n8n; STIG hardening
- Classified email relay integration
- SIPRNet end-to-end testing + compliance documentation (SSP, POA&M)

**Classified Testing Model:** Client's cleared personnel execute VV-provided test scripts on SIPRNet. VV provides real-time support from unclassified. If client sponsors VV operator access, VV tests directly on classified as a backup option.

**Deliverables:** Operational classified deployment, inherited ATO, compliance docs

**Tool Development Cost:** $23K - $40K
**Monthly Infra:** ~$3,500 - $9,500/mo (Game Warden platform fee)

---

## Slide 10: Milestone 3 — Red / TS/SCI (Months 4-6)

- Promotion to AWS Top Secret Region via AWS Diode
- Additional SCI compartment access controls
- Enhanced audit logging and monitoring
- Same classified testing model as Yellow — client personnel test on JWICS with VV support from unclass
- Fully air-gapped — all dependencies bundled
- JWICS operational acceptance testing

**Deliverables:** Full TS/SCI deployment, compliance documentation, operational acceptance

**Tool Development Cost:** $30K - $62K
**Monthly Infra:** ~$10K - $19K/mo (TS region premium)

---

## Slide 11: Game Warden — Why It Matters

**Problem:** Traditional ATO takes 6-18 months and costs $200K-$500K+.

**Solution:** Game Warden by Second Front Systems — DoD-accredited PaaS on AWS GovCloud.

- Applications **inherit the ATO** — weeks, not months
- Automated scanning: ClamAV (malware), Anchore (CVE), STIG hardening
- Supports IL2 through TS/SCI via AWS Secret and Top Secret regions
- Cross-domain transfer via AWS Diode

We provide hardened container images + Helm charts. Game Warden handles the rest.

---

## Slide 12: Security & Compliance

| Framework | Coverage |
|---|---|
| CMMC Level 2 | Access control, audit logging, encryption, input sanitization |
| NIST 800-171 | CUI handling, separation of duties, automated audit trail |
| FedRAMP | Containerized arch, no 3rd-party SaaS, processing within auth boundary |
| DISA STIGs | Applied automatically via Game Warden pipeline |

Zero external API calls on classified. All processing stays inside the boundary.

---

## Slide 13: Integrated Contract — Total Pricing

### Tool Development (One-Time, Across All 3 Milestones)

| Milestone | Development Cost |
|---|---|
| MS1: Black MVP | $20,000 - $31,000 |
| MS2: Yellow (Secret) | $23,000 - $40,000 |
| MS3: Red (TS/SCI) | $30,000 - $62,000 |
| **Total Tool Development** | **$73,000 - $133,000** |

### Veteran Vectors Services

| Item | Cost |
|---|---|
| **VV Development & Engineering Fee** | **$35,000** (flat — full 6-month engagement) |
| **VV Retainer (15%)** | **15% of monthly contract costs, beginning Month 3** |

---

## Slide 14: Infrastructure Costs by Milestone

| Milestone | Monthly Infra | Months Active (Yr 1) | Annual Infra |
|---|---|---|---|
| Black (runs all year) | $130 - $270/mo | 12 | $1,560 - $3,240 |
| Yellow (starts ~Mo 3) | $3,500 - $9,500/mo | 10 | $35,000 - $95,000 |
| Red (starts ~Mo 5) | $10,000 - $19,000/mo | 8 | $80,000 - $152,000 |
| **Total Year 1 Infra** | | | **$116,560 - $250,240** |

*Infrastructure timing assumes each tier goes live and stays running once deployed.*

---

## Slide 15: Veteran Vectors Retainer & Maintenance Model

**Months 1-2:** Development phase. VV $35K fee covers all engineering, PM, and training.

**Month 3 onward:** 15% retainer kicks in on ongoing monthly infrastructure costs.

| Monthly Infra (at full deployment) | Low | High |
|---|---|---|
| Combined infra (Black + Yellow + Red) | $13,630/mo | $28,770/mo |
| **VV 15% retainer** | **$2,045/mo** | **$4,316/mo** |

**Year 1 retainer estimate (Months 3-12 = 10 months):** ~$20,450 - $43,160

### What the Retainer Covers

**Container Lifecycle Management:**
- Monitor upstream releases (n8n, PostgreSQL, NGINX) for security patches and version updates
- Rebuild container images with patches, test on unclassified, deliver updated images
- Critical CVE patches: same-week image rebuild. Minor updates: batched monthly/quarterly.
- On classified tiers, updated images go through Game Warden pipeline (scan → stage → promote)

**Operational Support:**
- Troubleshooting and incident response (priority SLA)
- Workflow modifications as operational needs evolve
- Infrastructure monitoring and alerting review
- Database maintenance (backups verification, index tuning, storage management)

**Advisory & Planning:**
- Enhancement scoping for future features (AI narrative, predictive trending, etc.)
- Quarterly architecture reviews
- Compliance posture updates as CMMC/NIST requirements evolve
- Scaling support for larger user populations (e.g., May event ~150 users)

---

## Slide 16: Total Year 1 Investment Summary

| Category | Low Estimate | High Estimate |
|---|---|---|
| Tool development (all 3 milestones) | $73,000 | $133,000 |
| Infrastructure (Year 1) | $116,560 | $250,240 |
| VV development fee | $35,000 | $35,000 |
| VV retainer (15%, Months 3-12) | $20,450 | $43,160 |
| **Total Year 1** | **$245,010** | **$461,400** |
| **Midpoint Estimate** | | **~$353,000** |

### Payment Milestones

| Milestone | Trigger | Tool Dev Payment | VV Fee Payment |
|---|---|---|---|
| Contract Award | Signed | 20% of tool dev | 30% of $35K = **$10,500** |
| MS1: Black MVP Accepted | March event UAT | 30% of tool dev | 25% of $35K = **$8,750** |
| MS2: Yellow Operational | SIPRNet deployment | 30% of tool dev | 20% of $35K = **$7,000** |
| MS3: Red Operational | JWICS acceptance | 20% of tool dev | 25% of $35K = **$8,750** |
| VV Retainer | Monthly, starting Month 3 | — | 15% of that month's infra costs |

---

## Slide 17: Where the Money Goes

| Category | Low | High | % of Total |
|---|---|---|---|
| Tool development | $73K | $133K | ~30% |
| Infrastructure (Game Warden + AWS) | $116.5K | $250.2K | ~50% |
| VV development fee | $35K | $35K | ~10% |
| VV retainer | $20.5K | $43.2K | ~10% |

- **Black tier:** Almost all development labor. Infrastructure is negligible (~$200/mo).
- **Yellow tier:** Game Warden platform fee ($3K-$8K/mo) is the dominant cost.
- **Red tier:** TS region premium ($8K-$15K/mo) drives 80% of Red spend.
- **Game Warden fees replace a $200K-$500K+ standalone ATO** that takes 6-18 months.

---

## Slide 18: Government-Ready Product & Downstream Sale

This is a **commercial B2B engagement** between VV and the defense contractor. The product is built to be **resold to a downstream government entity**.

### What VV Delivers (Product-Ready for Gov Sale)

| Requirement | How We Address It |
|---|---|
| **Data rights / IP** | Contractor receives unlimited rights to all custom code, workflows, configs, and Helm charts. Open-source components retain existing licenses (MIT for n8n, PostgreSQL License, BSD for NGINX). Clean IP chain for gov resale. |
| **Section 508 accessibility** | Web forms and dashboards built to WCAG 2.1 AA. Required for any IT product sold to the government. |
| **Software supply chain (SCRM)** | Full Software Bill of Materials (SBOM) delivered per NIST SP 800-218. Documents every component and its origin. n8n is open-source (German company, Sustainable Use License). PostgreSQL and NGINX are widely used, US-maintained open-source. |
| **CMMC / NIST 800-171 compliance** | Built-in from day one — access control, audit logging, encryption, input sanitization. Compliance documentation (SSP, POA&M) delivered at Yellow/Red milestones. |
| **Game Warden / ATO readiness** | Containerized, hardened, Iron Bank-compatible. Inherits ATO through Game Warden — the contractor doesn't need to pursue standalone certification. |
| **Transition / exit plan** | All code, IaC, docs, and training delivered at each milestone. Contractor can operate independently or hand off to government operators. |

### What the Contractor Handles (for Gov Sale)

- SAM.gov registration, CAGE code, UEI, NAICS codes (contractor's responsibility)
- FAR/DFARS clause compliance in their government contract
- Contract vehicle selection (GSA Schedule, OTA, SBIR, direct award)
- CDRLs mapped to VV milestone deliverables
- Government contracting officer relationship
- Insurance requirements (cyber liability, E&O, general liability)

### Cost Reduction Levers

- **Multi-tenant Game Warden** — Share K8s cluster to cut platform fees
- **Existing Game Warden contract** — Reduces onboarding cost if contractor already has one
- **Bundle discount** — Single contract across all tiers saves 10-15% on development
- **Phased infra spin-up** — Don't start Yellow/Red infra until milestone is reached

---

## Slide 19: Risk Assessment & Mitigation

| # | Risk | Likelihood | Impact | Severity | Mitigation |
|---|---|---|---|---|---|
| R1 | Game Warden onboarding delays | Medium | High | **High** | Built to CMMC/NIST from day one; pre-approved container patterns. Parallel prep during Black so Yellow isn't blocked. |
| R2 | Classified testing coordination | Medium | Medium | **Medium** | Primary: client personnel test on classified using VV test scripts + unclass support. Backup: client sponsors VV operator clearance access for direct testing. Reduces dependency on VV clearance sponsorship. |
| R3 | n8n Iron Bank submission rejected or delayed | Medium | Medium | **Medium** | Prepare hardened image during Black. If rejected, deploy with equivalent STIG hardening outside Iron Bank under org waiver. |
| R4 | CVE count in n8n dependency tree exceeds budget | Medium | Medium | **Medium** | Scope remediation budget at upper range ($6K). Pin stable dependency versions. Monitor CVE feeds pre-submission. |
| R5 | Power BI unavailable on classified network | Low | Medium | **Medium** | Metabase (open-source) included as drop-in fallback. Both options built during Black MVP. |
| R6 | User adoption resistance | Low | Medium | **Medium** | Familiar form-based UX. Existing Power BI dashboards preserved where possible. Training included in MS1 deliverables. |
| R7 | Single-vendor dependency on VV | Low | Medium | **Medium** | All code, docs, and infra-as-code delivered at each milestone. Client can operate independently after handoff. |
| R8 | Scope creep across milestones | Medium | Medium | **Medium** | Milestone gates with defined deliverables and acceptance criteria. Change requests handled via retainer after Month 3. |
| R9 | AWS Diode cross-domain transfer issues (Red) | Low | High | **Medium** | Engage AWS SA early. Validate image transfer in staging before production promotion. Budget upper range ($10K). |
| R10 | External compliance assessment exceeds budget | Medium | Low | **Low** | Clarify internal vs. external assessment at contract award. Scope compliance support hours accordingly ($5K-$15K range). |

---

## Slide 20: Next Steps

1. **Review & Approve** this integrated milestone proposal
2. **Contract Execution** — Sign single 6-month engagement with milestone payments
3. **Onboarding (Week 1)** — Access existing Power Automate flows, Power BI, Excel data
4. **MS1 Build (Months 1-2)** — Black MVP development → March event UAT
5. **MS2 Build (Months 2-4)** — Game Warden onboarding → SIPRNet deployment
6. **MS3 Build (Months 4-6)** — TS promotion → JWICS operational acceptance
7. **Retainer Begins (Month 3)** — Ongoing VV support at 15% of monthly infra

**Single contract. Three milestones. Full classified deployment in 6 months.**

**Contact: Veteran Vectors**

---
