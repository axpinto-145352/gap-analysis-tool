# Gap Analysis Automation Platform — Executive Proposal
### Veteran Vectors | Condensed Briefing (20 Slides)

---

## Slide 1: Title

**Gap Analysis Automation Platform**
Secure, Scalable Survey-to-Insight Pipeline for Defense & Intelligence Operations

*Prepared by Veteran Vectors*

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

Replace the fragile Microsoft patchwork with a **self-hosted n8n automation platform** in Docker:

- **One platform** replaces Forms + Power Automate + VBA scripts
- **PostgreSQL** replaces fragile Excel connections permanently
- **Automated analytics & reports** — no manual calculations
- **Docker containerized** — deploys at any classification level
- **Game Warden pathway** — inherited ATO, not 6-18 month certification

---

## Slide 4: Before → After

| | Current | Proposed |
|---|---|---|
| Automation | 10+ Power Automate flows | 5 unified n8n workflows |
| Data Store | Excel (fragile) | PostgreSQL (reliable) |
| Reports | Manual | Auto-generated on demand |
| Classified Path | None | Game Warden (IL2→TS/SCI) |
| Operator Dependency | 1 person | Any trained operator |
| Licensing | Per-user Microsoft fees | Open-source, $0 licensing |

---

## Slide 5: How It Works — 5 Core Workflows

1. **Survey Distribution** — Roster-driven sends + auto-reminders
2. **Form Submission Handler** — Webhook intake, validation, DB storage
3. **Data Processing & Analytics** — Likert/NPS scoring, factor analysis, trend tracking
4. **Report Generator** — Templated consultancy report with top-10 gaps, recommendations
5. **Lifecycle Manager** — Auto open/close surveys, analyst notifications

All 5 workflows are built, tested, and handed off as a complete system.

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

## Slide 7: Three Deployment Tiers

| Tier | Classification | Environment | Timeline |
|---|---|---|---|
| **Black** (MVP) | Unclassified / IL2-IL4 | AWS GovCloud or on-prem Docker | Weeks 1-6 |
| **Yellow** | Secret / IL5-IL6 | Game Warden (AWS Secret Region) | Weeks 7-12 |
| **Red** | TS/SCI | Game Warden (AWS TS Region) | Weeks 13-20 |

Each tier has a **milestone gate** — proceed or conclude with full deliverables.

---

## Slide 8: Tier 1 — Black MVP (Weeks 1-6)

- n8n + PostgreSQL + NGINX in Docker
- All 5 workflows operational
- Google Sheets/Excel Online integration for familiar interface
- Optional Power BI connector
- **Target:** Functional prototype for March event (~15 users)

**Development:** $20K - $31K
**Monthly Infra:** ~$130 - $270/mo

---

## Slide 9: Tier 2 — Yellow / Secret (Weeks 7-12)

- Kubernetes/Helm deployment through Game Warden pipeline
- PostgreSQL-only (no external API dependencies)
- Iron Bank base images; STIG hardening
- Inherited ATO via Game Warden
- **Target:** Operational on classified (SIPRNet)

**Development:** $23K - $40K
**Monthly Infra:** ~$3,500 - $9,500/mo (Game Warden platform fee is the driver)

---

## Slide 10: Tier 3 — Red / TS/SCI (Weeks 13-20)

- Promotion to TS region via AWS Diode cross-domain solution
- Additional SCI access controls
- Fully air-gapped; all dependencies bundled
- **Target:** Full operational deployment at highest classification

**Development:** $30K - $62K
**Monthly Infra:** ~$10K - $19K/mo (TS region premium pricing)

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

## Slide 12: Security & Compliance Summary

| Framework | Coverage |
|---|---|
| CMMC Level 2 | Access control, audit logging, encryption, input sanitization |
| NIST 800-171 | CUI handling, separation of duties, automated audit trail |
| FedRAMP | Containerized arch, no 3rd-party SaaS, all processing within auth boundary |
| DISA STIGs | Applied automatically via Game Warden pipeline |

Zero external API calls on classified. All processing stays inside the boundary.

---

## Slide 13: Implementation Timeline

| Weeks | Phase | Key Milestone |
|---|---|---|
| 1-2 | Setup & Core Build | n8n deployed, survey distribution + form handler live |
| 3-4 | Analytics & Reports | Likert/NPS engine, auto-report generator |
| 5-6 | Testing & UAT | End-to-end test, March event with ~15 users |
| 7-10 | Yellow Deployment | Game Warden onboarding, K8s migration, SIPRNet testing |
| 11-12 | Yellow Operational | Compliance docs, operational acceptance |
| 13-18 | Red Deployment | TS provisioning, AWS Diode, JWICS integration |
| 19-20 | Red Operational | Final compliance review, operational acceptance |

---

## Slide 14: Total Program Pricing (Tool Development)

| Phase | Development | Year 1 Infra | Year 1 Total |
|---|---|---|---|
| Black MVP | $20K - $31K | $1.6K - $3.2K | **$21.5K - $34.2K** |
| Yellow (Secret) | $23K - $40K | $42K - $114K | **$65K - $154K** |
| Red (TS/SCI) | $30K - $62K | $120K - $228K | **$150K - $290K** |
| **All Tiers** | **$73K - $133K** | **$163.6K - $345.2K** | **$236.5K - $478.2K** |

---

## Slide 15: Veteran Vectors Services

In addition to tool/infrastructure costs above:

| Item | Cost |
|---|---|
| **Veteran Vectors Development Fee** | **$30,000** (flat) |
| **Veteran Vectors Retainer (15%)** | **15% of total contract value** |

- Development fee covers architecture, build-out, integration, training, and project management by Veteran Vectors
- 15% retainer covers ongoing advisory, maintenance coordination, escalation support, and future enhancement scoping
- These fees are **independent of** tool licensing, infrastructure, and Game Warden costs

**Example — Black MVP only:**
Tool/Infra Year 1: ~$28K (midpoint) + $30K dev fee + $4,200 retainer (15% of $28K) = **~$62,200**

**Example — Full Program (all 3 tiers):**
Tool/Infra Year 1: ~$357K (midpoint) + $30K dev fee + $53,550 retainer (15% of $357K) = **~$440,550**

---

## Slide 16: Where the Money Goes

| Tier | Development % | Infrastructure % | Key Driver |
|---|---|---|---|
| Black | ~90% | ~10% | Fast, lean — mostly engineering labor |
| Yellow | ~35% | ~65% | **Game Warden platform fee** ($3K-$8K/mo) |
| Red | ~20% | ~80% | **TS region premium** ($8K-$15K/mo) |

Game Warden fees are high but **replace a $200K-$500K+ independent ATO process** that takes 6-18 months.

---

## Slide 17: Cost Reduction Levers

- **Phase gating** — Start with Black only (~$28K). Expand based on results.
- **Multi-tenant Game Warden** — Share a K8s cluster; significantly reduces platform fees
- **Existing Game Warden contract** — If org already has one, onboarding costs drop
- **Bundle discount** — Single contract across all tiers saves 10-15% on development
- **Iron Bank images** — PostgreSQL & NGINX already in Iron Bank; only n8n needs submission

---

## Slide 18: Risk Mitigation

| Risk | Mitigation |
|---|---|
| Game Warden delays | Built to CMMC/NIST from day one; pre-approved container patterns |
| Power BI unavailable on target net | Metabase (open-source) fallback included |
| AI features unavailable on high side | Template-based reports work without AI; AI is a future add-on |
| User adoption resistance | Familiar form-based UX; existing Power BI preserved where possible |
| Network restrictions | Fully self-contained; zero external API calls |

---

## Slide 19: Optional Add-Ons

| Enhancement | Cost |
|---|---|
| Monthly maintenance & monitoring | $1,500 - $3,000/mo |
| Additional survey templates | $1,500 - $2,500 each |
| AI narrative integration (when available) | $5K - $10K |
| Scaling to ~150 users (May event) | $2K - $4K |
| Predictive gap trending (ML) | $8K - $15K |
| Auto-generated briefing slides | $5K - $8K |

---

## Slide 20: Next Steps

1. **Review & Approve** this proposal and pricing
2. **Contract Execution** — Finalize terms, milestones, and payments
3. **Onboarding** — Access existing Power Automate flows, Power BI, and Excel data
4. **Environment Provisioning** — AWS GovCloud or on-prem Docker
5. **Development Begins** — Week 1 sprint
6. **March Event** — Live MVP test with ~15 users
7. **Expand or Conclude** at each milestone gate

**Contact: Veteran Vectors**

---
