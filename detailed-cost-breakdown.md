# Gap Analysis Platform — Integrated Cost Breakdown & Talking Points
### Veteran Vectors Internal Reference | 6-Month Milestone Engagement

This document gives you line-by-line detail on every cost in the integrated contract so you can speak confidently about where money goes, why, and how to structure conversations.

---

## 1. Contract Structure at a Glance

**Single 6-month contract** with three milestone gates (Black → Yellow → Red).

| Component | Amount |
|---|---|
| Tool development (all 3 milestones) | $73,000 - $133,000 |
| Infrastructure (Year 1) | $116,560 - $250,240 |
| VV development fee (flat) | $35,000 |
| VV retainer (15%, Months 3-12) | $20,450 - $43,160 |
| **Year 1 Total** | **$245,010 - $461,400** |
| **Midpoint** | **~$353,000** |

---

## 2. Veteran Vectors Revenue Breakdown

### Development Fee — $35,000 (Flat)

This is your full 6-month engagement fee. It covers:

- Architecture design and technical planning across all 3 tiers
- n8n workflow development, integration engineering, Docker/Helm packaging
- Game Warden pipeline setup and container hardening coordination
- Testing support (UAT at March event, SIPRNet validation, JWICS acceptance)
- Operator training and system documentation
- Project management across all 3 milestones

**When it's paid:** In full at contract award (included in the 20% upfront payment). This de-risks VV — you're paid for your expertise before tool development costs start flowing.

**How to position:** "This is our engineering and project management fee for the full 6-month build. It covers architecture through operational acceptance at every classification level."

### Retainer — 15% of Monthly Infrastructure, Starting Month 3

The retainer kicks in when infrastructure is running and VV shifts from build mode to support mode.

**What it covers:**
- Ongoing advisory and technical consultation
- Maintenance coordination (patching, upgrades, incident response)
- Escalation support and troubleshooting
- Enhancement scoping for future features
- Priority support SLA

**Month-by-month retainer estimates:**

| Month | Active Infra | Monthly Infra (Low) | Monthly Infra (High) | VV 15% (Low) | VV 15% (High) |
|---|---|---|---|---|---|
| 1-2 | Black only | $130 | $270 | — | — |
| 3-4 | Black + Yellow | $3,630 | $9,770 | $545 | $1,466 |
| 5-6 | Black + Yellow + Red | $13,630 | $28,770 | $2,045 | $4,316 |
| 7-12 | All three running | $13,630 | $28,770 | $2,045 | $4,316 |

**Year 1 retainer total (Months 3-12):**
- Low: (2 x $545) + (8 x $2,045) = $1,090 + $16,360 = **~$17,450**
- High: (2 x $1,466) + (8 x $4,316) = $2,932 + $34,528 = **~$37,460**

*Note: The slide deck uses a simplified flat estimate (~$20K-$43K). The month-by-month ramp above is more precise since not all tiers are running from Month 3.*

**How to position:** "Once we hand off each tier, the 15% retainer ensures you have a dedicated team that knows this system. You're not re-onboarding a vendor every time something needs attention."

---

## 3. Tool Development Costs — Line-by-Line Detail

### Milestone 1: Black MVP ($20,000 - $31,000)

| Line Item | Low | High | What You're Buying |
|---|---|---|---|
| n8n workflow build-out (5 workflows) | $8,000 | $12,000 | Core automation: survey distribution, form handler, analytics engine, report generator, lifecycle manager. This is the product. |
| Data schema design + Excel/Forms migration | $2,000 | $3,000 | PostgreSQL schema for demographics, responses, gap definitions, survey config. Migration scripts for existing data. Kills Excel fragility permanently. |
| Dashboard setup (Power BI or Metabase) | $3,000 | $5,000 | Connect PostgreSQL to BI tool. Build dashboards with filtering by demographic, working group, time period. Lower end if reusing existing Power BI dashboards. |
| Consultancy report template + generator | $2,000 | $3,000 | Auto-generated markdown report: exec summary, top-10 gaps, factor analysis tables, trend analysis, actionable recommendations (Immediate/Monitor/Maintain). |
| Docker containerization + hardening | $1,500 | $2,500 | Docker Compose: n8n + PostgreSQL + NGINX. Non-root containers, volume encryption, network isolation. Foundation for Game Warden later. |
| NGINX TLS + security config | $500 | $1,000 | TLS 1.2+, HSTS, CSP, rate limiting, reverse proxy routing. Standard security hardening. |
| Integration testing + UAT | $2,000 | $3,000 | End-to-end test with sample data. Live UAT at March event with ~15 users. Bug fixes from feedback. |
| Documentation + operator training | $1,000 | $1,500 | Admin guide, workflow modification guide, troubleshooting runbook, 1-2 training sessions. Eliminates single-operator bottleneck. |

**Key conversation points for MS1:**
- This is the "prove it works" phase. Low cost, high visibility.
- March event is the tangible deliverable — real users, real data.
- Everything built here carries forward to Yellow and Red.

### Milestone 2: Yellow / Secret ($23,000 - $40,000)

| Line Item | Low | High | What You're Buying |
|---|---|---|---|
| Kubernetes/Helm chart conversion | $4,000 | $6,000 | Translate Docker Compose to Helm charts for K8s. Services, deployments, PVCs, config maps, secrets. Required for Game Warden. |
| Iron Bank image submission (n8n) | $3,000 | $5,000 | DoD's hardened container registry. PostgreSQL + NGINX already in Iron Bank. n8n requires new submission: Dockerfile hardening, CVE remediation, docs. Range depends on CVE count. |
| Game Warden onboarding + pipeline | $5,000 | $8,000 | Account setup with Second Front Systems, CI/CD pipeline config (push → scan → stage → promote). One-time cost — once set up, deployments are automated. |
| Acceptance Baseline Criteria remediation | $3,000 | $6,000 | Resolve all critical/high CVEs, apply STIG hardening (non-root, file perms, minimal packages), pass Anchore scanning (NIST 800-53). Range depends on image cleanliness. |
| Remove external API dependencies | $2,000 | $4,000 | Rip out any Google Sheets/Excel Online integrations from Black. Everything goes through PostgreSQL only. Hard requirement for classified — zero internet calls. |
| Classified email relay integration | $1,000 | $2,000 | Swap commercial SMTP (SES) for approved classified mail relay. Test on SIPRNet. Straightforward — depends on which relay the org uses. |
| SIPRNet testing + validation | $3,000 | $5,000 | Deploy to classified staging, test all 5 workflows end-to-end on SIPRNet. Validate no external calls, no broken deps. Cost is labor + access coordination time. |
| Compliance documentation (SSP, POA&M) | $2,000 | $4,000 | System Security Plan, Plan of Action & Milestones. Game Warden simplifies this vs. standalone ATO, but docs are still required. |

**Key conversation points for MS2:**
- Game Warden onboarding ($5K-$8K) is a one-time gate. Once through, classified deployments are repeatable.
- Iron Bank submission for n8n is the wildcard — if the org accepts equivalent hardening without formal Iron Bank submission, this drops.
- "Remove external APIs" is non-negotiable for classified. Budget it.

### Milestone 3: Red / TS/SCI ($30,000 - $62,000)

| Line Item | Low | High | What You're Buying |
|---|---|---|---|
| TS environment provisioning + access | $3,000 | $5,000 | Coordinate AWS Top Secret Region access. Provisioning requests, security briefings, access approvals. Primarily labor and coordination. |
| SCI access controls | $4,000 | $7,000 | Compartmented access controls beyond standard Secret. Role-based restrictions by SCI program. Enhanced access logging. Program-specific, often custom. |
| AWS Diode cross-domain deployment | $5,000 | $10,000 | Configure cross-domain transfer pipeline (unclass → Secret → TS). Validate image integrity post-transfer. Specialized skill — few people have Diode experience. Premium reflects scarcity. |
| Enhanced audit logging + monitoring | $2,000 | $4,000 | TS requires more granular audit trails. Monitoring dashboards for security events. Anomaly alerting. |
| TS-specific compliance documentation | $3,000 | $6,000 | Additional SSP sections for TS, ICD 503 alignment (if applicable), program-specific security docs. |
| Security assessment + pen test support | $5,000 | $10,000 | Support the org's security assessment team. Remediate findings. Cost is VV labor to support their review — the assessment itself may be done by the org or a third party. |
| JWICS operational acceptance testing | $3,000 | $5,000 | End-to-end testing on JWICS (Top Secret network). Fully air-gapped validation. Requires TS clearance + physical facility access. |
| External compliance team involvement | $5,000 | $15,000 | If org brings in external assessors. VV labor to support review, answer questions, remediate. Widest range — depends on assessment depth. |

**Key conversation points for MS3:**
- The wide ranges here reflect uncertainty at TS level. Every program has different requirements.
- AWS Diode is the most specialized (and expensive) line item — this is niche expertise.
- External compliance ($5K-$15K) is the biggest variable. Ask early if they'll use internal or external assessors.

---

## 4. Infrastructure Costs — Where the Real Money Goes

### Black Infrastructure ($130 - $270/mo)

| Item | Low | High | What It Is |
|---|---|---|---|
| AWS GovCloud compute (t3.medium) | $75 | $150 | Single VM: 2 vCPU, 4GB RAM. Runs everything. Sufficient for <50 users. |
| PostgreSQL (RDS or self-hosted) | $30 | $75 | RDS is easier but costs more. Self-hosted on same VM is cheaper. |
| S3 backup storage | $5 | $10 | Daily encrypted pg_dump, 30-day retention. Negligible. |
| Domain + TLS cert | $12 | $15 | Domain registration + cert (or free via Let's Encrypt). |
| SMTP relay (SES) | $10 | $20 | $0.10 per 1,000 emails. Even heavy use is ~$10/mo. |

**Bottom line:** Black infra is almost free. ~$200/mo. The cost here is 99% development labor.

### Yellow Infrastructure ($3,500 - $9,500/mo)

| Item | Low | High | What It Is |
|---|---|---|---|
| **Game Warden platform fee** | **$3,000** | **$8,000** | **The dominant cost.** Single-tenant K8s cluster on AWS GovCloud Secret Region. Includes managed K8s, monitoring, patching, compliance tooling. |
| AWS GovCloud Secret Region compute | $500 | $1,500 | Compute within the Game Warden cluster. Premium over commercial AWS. |
| Managed services | Included | Included | Monitoring and patching bundled in Game Warden fee. |

**Bottom line:** Game Warden is $3K-$8K/mo. That's the number to know. It replaces a $200K-$500K+ standalone ATO and 6-18 months of calendar time. Multi-tenant clusters (sharing with other apps) can cut this significantly.

### Red Infrastructure ($10,000 - $19,000/mo)

| Item | Low | High | What It Is |
|---|---|---|---|
| **Game Warden platform fee (TS)** | **$8,000** | **$15,000** | **Premium pricing.** TS region has fewer customers, higher security overhead, more expensive underlying AWS TS Region. |
| AWS Top Secret Region compute | $1,500 | $3,000 | Significant premium over GovCloud commercial or Secret. |
| Enhanced monitoring + compliance tools | $500 | $1,000 | Additional tooling required at TS level. |

**Bottom line:** TS is expensive. $10K-$19K/mo. But the alternative is no TS capability at all (or $200K-$500K+ and 6-18 months for standalone ATO).

---

## 5. Payment Schedule — How Cash Flows

### Upfront (Contract Award)

| Item | Low | High |
|---|---|---|
| 20% of tool development | $14,600 | $26,600 |
| VV development fee (full) | $35,000 | $35,000 |
| **Total upfront** | **$49,600** | **$61,600** |

### Month 2 (MS1: Black MVP Accepted)

| Item | Low | High |
|---|---|---|
| 30% of tool development | $21,900 | $39,900 |
| Black infra (2 months accrued) | $260 | $540 |
| **Total at MS1** | **~$22,160** | **~$40,440** |

### Month 4 (MS2: Yellow Operational)

| Item | Low | High |
|---|---|---|
| 30% of tool development | $21,900 | $39,900 |
| Yellow infra (2 months accrued) | $7,000 | $19,000 |
| VV retainer (Months 3-4) | $1,090 | $2,932 |
| **Total at MS2** | **~$29,990** | **~$61,832** |

### Month 6 (MS3: Red Operational)

| Item | Low | High |
|---|---|---|
| 20% of tool development | $14,600 | $26,600 |
| Red infra (2 months accrued) | $20,000 | $38,000 |
| VV retainer (Months 5-6) | $4,090 | $8,632 |
| **Total at MS3** | **~$38,690** | **~$73,232** |

### Months 7-12 (Post-Engagement, Ongoing)

| Item | Monthly Low | Monthly High |
|---|---|---|
| All infra running | $13,630 | $28,770 |
| VV retainer (15%) | $2,045 | $4,316 |
| **Monthly total** | **~$15,675** | **~$33,086** |

---

## 6. Conversation Playbook

### Conversation 1: Problem & Vision (Non-Technical Decision Maker)
- Lead with pain: broken Excel, 10+ flows, single-operator risk, no classified path
- Show Before/After table
- Don't discuss tools yet — stay on business outcomes
- **Key line:** "Right now this system fails if one person is unavailable. We fix that permanently."

### Conversation 2: Technical Solution (Technical Stakeholders)
- Walk through 5 workflows and tech stack
- Emphasize: open-source, no vendor lock-in, containerized from day one
- Game Warden pathway is the differentiator vs. "just fix Power Automate"
- **Key line:** "Everything we build in Black carries directly to classified. No rebuild, no re-architecture."

### Conversation 3: Integrated Pricing (Budget Authority)
- Present the single-contract milestone structure
- Lead with the $35K VV fee — that's their cost to get started (plus 20% of tool dev)
- Upfront outlay is ~$50K-$62K. That's the "first check."
- Infrastructure is the big number but it's **monthly and scales with deployment**
- **Key line:** "The upfront is ~$50K-$62K. After that, costs are milestone-gated — you only pay for tiers you deploy."

### Conversation 4: Game Warden Deep Dive (If Classified Is the Goal)
- ATO inheritance: weeks vs. 6-18 months
- Pipeline walkthrough: push → scan → stage → promote
- IL levels: IL2/IL4 (unclass), IL5/IL6 (Secret), TS/SCI
- Multi-tenant vs. single-tenant economics
- **Key line:** "Game Warden replaces a $200K-$500K, 6-18 month ATO process with a platform fee and a weeks-long onboarding."

### Objection Handling

| Objection | Response |
|---|---|
| "That's a lot of money." | "The infrastructure costs are Game Warden + AWS — that's the price of classified deployment. The alternative is $200K-$500K for standalone ATO. Our VV fee is $35K for a 6-month build across 3 classification levels." |
| "Can we just do Black?" | "Yes. Black MVP is ~$50K-$62K upfront. You get a working system, prove it out at the March event, and decide from there. The contract has milestone gates for exactly this." |
| "Why not fix Power Automate?" | "Power Automate can't deploy to classified networks. It has no Game Warden pathway. And you'd still have 10+ siloed flows and broken Excel connections." |
| "What's the retainer for?" | "Once we build it, you need someone who knows the system for maintenance, troubleshooting, and future enhancements. The 15% retainer starting Month 3 ensures priority support without re-onboarding." |
| "Can the retainer start later?" | "It starts Month 3 — when Yellow infra is live and there's actual infrastructure to support. During Months 1-2, the $35K dev fee covers everything." |

---

## 7. Quick Reference — Tools & What They Do

| Tool | What It Is | Cost | Setup Complexity |
|---|---|---|---|
| **n8n** | Visual automation engine (self-hosted Power Automate alternative) | Free (open-source) | Medium — Docker deploy, workflow config |
| **PostgreSQL 16** | Relational database replacing Excel | Free (open-source) | Low — schema + migration scripts |
| **NGINX** | Reverse proxy with TLS | Free (open-source) | Low — standard config |
| **Docker** | Container runtime | Free (open-source) | Low — install + compose up |
| **Helm** | K8s package manager (Yellow/Red) | Free (open-source) | Medium — chart creation |
| **Game Warden** | DoD DevSecOps PaaS (Second Front Systems) | $3K-$15K/mo | High — onboarding + pipeline setup |
| **Metabase** | Open-source BI dashboard (Power BI alternative) | Free (open-source) | Medium — deploy + build dashboards |
| **AWS GovCloud** | Government-compliant cloud | $130-$19K/mo (tier-dependent) | Medium-High — account + VPC + IAM |
| **Iron Bank** | DoD hardened container registry | Free (access) | High — image submission + CVE remediation |
| **AWS Diode** | Cross-domain transfer (unclass → Secret → TS) | Included in AWS | High — specialized configuration |

**Key point:** Every tool except Game Warden and AWS is free/open-source. The licensing cost of this stack is $0. You're paying for engineering labor and cloud infrastructure.

---
