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

**When it's paid:** Spread across all 4 milestones — 30% at contract award ($10,500), 25% at Black MVP acceptance ($8,750), 20% at Yellow operational ($7,000), 25% at Red operational ($8,750). This keeps VV revenue flowing with each deliverable.

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
| VV fee — 30% ($10,500) | $10,500 | $10,500 |
| **Total upfront** | **$25,100** | **$37,100** |

### Month 2 (MS1: Black MVP Accepted)

| Item | Low | High |
|---|---|---|
| 30% of tool development | $21,900 | $39,900 |
| VV fee — 25% ($8,750) | $8,750 | $8,750 |
| Black infra (2 months accrued) | $260 | $540 |
| **Total at MS1** | **~$30,910** | **~$49,190** |

### Month 4 (MS2: Yellow Operational)

| Item | Low | High |
|---|---|---|
| 30% of tool development | $21,900 | $39,900 |
| VV fee — 20% ($7,000) | $7,000 | $7,000 |
| Yellow infra (2 months accrued) | $7,000 | $19,000 |
| VV retainer (Months 3-4) | $1,090 | $2,932 |
| **Total at MS2** | **~$36,990** | **~$68,832** |

### Month 6 (MS3: Red Operational)

| Item | Low | High |
|---|---|---|
| 20% of tool development | $14,600 | $26,600 |
| VV fee — 25% ($8,750) | $8,750 | $8,750 |
| Red infra (2 months accrued) | $20,000 | $38,000 |
| VV retainer (Months 5-6) | $4,090 | $8,632 |
| **Total at MS3** | **~$47,440** | **~$81,982** |

### Months 7-12 (Post-Engagement, Ongoing)

| Item | Monthly Low | Monthly High |
|---|---|---|
| All infra running | $13,630 | $28,770 |
| VV retainer (15%) | $2,045 | $4,316 |
| **Monthly total** | **~$15,675** | **~$33,086** |

---

## 6. Risk Assessment & Mitigation — Full Detail

### Risk Matrix

| # | Risk | Likelihood | Impact | Severity | Milestone Affected |
|---|---|---|---|---|---|
| R1 | Game Warden onboarding delays | Medium | High | **High** | MS2 (Yellow) |
| R2 | Classified network access delays | Medium | High | **High** | MS2, MS3 |
| R3 | Iron Bank submission rejected/delayed | Medium | Medium | **Medium** | MS2 (Yellow) |
| R4 | CVE count exceeds remediation budget | Medium | Medium | **Medium** | MS2 (Yellow) |
| R5 | Power BI unavailable on classified | Low | Medium | **Medium** | MS2, MS3 |
| R6 | User adoption resistance | Low | Medium | **Medium** | MS1 (Black) |
| R7 | Single-vendor dependency on VV | Low | Medium | **Medium** | All |
| R8 | Scope creep across milestones | Medium | Medium | **Medium** | All |
| R9 | AWS Diode cross-domain issues | Low | High | **Medium** | MS3 (Red) |
| R10 | Compliance assessment exceeds budget | Medium | Low | **Low** | MS3 (Red) |

### Detailed Risk Analysis

**R1: Game Warden Onboarding Delays — HIGH**
- *What happens:* Second Front Systems onboarding takes longer than expected. Yellow milestone slides.
- *Why it's likely:* Game Warden onboarding depends on a third party (Second Front). Scheduling, account provisioning, and pipeline setup are outside VV's direct control.
- *Mitigation:* Begin Game Warden coordination during Black (Month 1), not at Yellow kickoff. Build system to CMMC/NIST standards from day one so container images are ready when the pipeline is. Use pre-approved container patterns that pass scanning faster.
- *Budget impact:* If delayed 2-4 weeks, no additional cost — just schedule shift. If delayed >1 month, may need to extend Yellow timeline and accrue extra infra costs (~$3.5K-$9.5K/mo).
- *Conversation tip:* "We start Game Warden coordination on day one, not when we need it. By the time Black MVP is done, we're already in the pipeline."

**R2: Classified Network Access Delays — HIGH**
- *What happens:* Getting developer access to SIPRNet or JWICS takes longer than planned. Can't test or deploy on classified.
- *Why it's likely:* Access to classified networks involves security briefings, account provisioning, and physical facility scheduling — all bureaucratic processes.
- *Mitigation:* Begin access coordination at contract award. Build 2-week buffer into each classified milestone. All development and testing that can happen on unclassified happens first.
- *Budget impact:* Delay doesn't add development cost, but extends the timeline and accrues infra costs for tiers already running.
- *Conversation tip:* "We need the org to start access requests immediately at signing. The development can proceed in parallel, but testing on classified requires access."

**R3: Iron Bank Submission Rejected or Delayed — MEDIUM**
- *What happens:* n8n container image fails Iron Bank review. Requires additional remediation cycles.
- *Why it's likely:* n8n is not currently in Iron Bank. Submission requires Dockerfile hardening, CVE resolution, and documentation. First-time submissions sometimes require multiple rounds.
- *Mitigation:* Prepare hardened n8n image during Black phase. If formal Iron Bank submission is rejected, deploy with equivalent STIG hardening under an organizational waiver. PostgreSQL and NGINX are already in Iron Bank — only n8n is at risk.
- *Budget impact:* If org accepts waiver path, saves $3K-$5K (Iron Bank submission line item). If additional remediation rounds needed, could add $2K-$3K.
- *Conversation tip:* "Two of three components are already in Iron Bank. n8n is the only submission. If it gets delayed, we can deploy with equivalent hardening under waiver."

**R4: CVE Count in n8n Dependencies Exceeds Budget — MEDIUM**
- *What happens:* Anchore scanning reveals more critical/high CVEs than expected in n8n's Node.js dependency tree. Remediation takes longer and costs more.
- *Why it's likely:* Node.js ecosystems have deep dependency trees. CVE counts vary month to month.
- *Mitigation:* Budget acceptance criteria remediation at upper range ($6K). Pin stable dependency versions before submission. Monitor CVE feeds during Black phase to anticipate issues.
- *Budget impact:* Worst case adds $2K-$4K above the budgeted range if CVE remediation requires upstream patches or dependency replacements.
- *Conversation tip:* "We monitor the CVE landscape during Black so there are no surprises at submission. We budget the upper range for remediation to absorb this."

**R5: Power BI Unavailable on Classified Network — MEDIUM**
- *What happens:* Power BI licensing or connectivity isn't available on SIPRNet or JWICS. Client loses existing dashboard investment.
- *Why it's likely:* Low — most classified orgs have some Power BI access. But availability varies by network and org.
- *Mitigation:* Metabase (open-source) is included as a drop-in fallback. Both dashboard paths are tested during Black. If Power BI works, use it. If not, Metabase is ready.
- *Budget impact:* Already budgeted in MS1 dashboard setup ($3K-$5K covers both paths).
- *Conversation tip:* "We build both options during Black. Zero additional cost to switch."

**R6: User Adoption Resistance — MEDIUM**
- *What happens:* End users are comfortable with existing Forms/Excel workflow and resist the new system.
- *Why it's likely:* Low — the new system uses similar form-based UX. But change management is always a factor.
- *Mitigation:* Familiar form-based interface (not a radical UX change). Existing Power BI dashboards preserved where possible. Operator training and documentation included in MS1. March event UAT with ~15 users provides early feedback loop.
- *Budget impact:* None — training and UAT are already budgeted.
- *Conversation tip:* "The March event is our adoption test. 15 real users, real data. We iterate based on their feedback before going classified."

**R7: Single-Vendor Dependency on VV — MEDIUM**
- *What happens:* Client is concerned about depending on VV long-term for a critical system.
- *Why it's likely:* Low — legitimate concern for any vendor engagement.
- *Mitigation:* All source code, infrastructure-as-code (Docker Compose, Helm charts), documentation, and operator training are delivered at each milestone. The client can operate the system independently after any milestone gate. The 15% retainer is for convenience, not dependency.
- *Budget impact:* None.
- *Conversation tip:* "Every milestone delivers everything — code, docs, training. You could walk away after Black with a fully operational system and never call us again. The retainer is there so you don't have to."

**R8: Scope Creep Across Milestones — MEDIUM**
- *What happens:* Client requests additional features, workflows, or integrations beyond the original scope during the 6-month engagement.
- *Why it's likely:* Medium — common in any development engagement, especially after seeing a working MVP.
- *Mitigation:* Each milestone has defined deliverables and acceptance criteria. Scope changes during Months 1-2 are handled within the $35K VV fee if minor. After Month 3, change requests route through the retainer relationship. Major scope changes require a separate SOW.
- *Budget impact:* Minor changes absorbed. Major changes ($5K+) require amendment.
- *Conversation tip:* "The milestone gates exist for exactly this. We define what 'done' looks like upfront. New ideas after MVP go through the retainer."

**R9: AWS Diode Cross-Domain Transfer Issues — MEDIUM**
- *What happens:* Cross-domain transfer from Secret to TS via AWS Diode fails or requires unexpected configuration.
- *Why it's likely:* Low — but AWS Diode is specialized infrastructure. Few teams have deep experience.
- *Mitigation:* Engage AWS Solutions Architect early (during Yellow phase). Validate image transfer in staging before production promotion. Budget AWS Diode line item at upper range ($10K).
- *Budget impact:* If issues arise, could add $3K-$5K in additional engineering time.
- *Conversation tip:* "We bring in an AWS SA during Yellow to prep the Diode path. By the time we're at Red, the cross-domain pipeline is already validated."

**R10: External Compliance Assessment Exceeds Budget — LOW**
- *What happens:* The organization's compliance team or external assessors require more extensive review than anticipated during Red milestone.
- *Why it's likely:* Medium likelihood but low impact — the widest cost range ($5K-$15K) already accounts for this.
- *Mitigation:* Clarify at contract award whether the org will use internal or external assessors. Scope compliance support hours accordingly. Game Warden's inherited ATO significantly reduces the assessment surface.
- *Budget impact:* Already captured in the $5K-$15K range. Clarifying early keeps it at the lower end.
- *Conversation tip:* "One question we need answered at signing: internal or external compliance review? That's the biggest variable in the Red tier budget."

### Risk Summary by Milestone

| Milestone | Key Risks | Biggest Concern |
|---|---|---|
| **MS1: Black** | R6 (adoption), R8 (scope creep) | Low overall risk. Controlled environment, small user group. |
| **MS2: Yellow** | R1 (Game Warden), R2 (access), R3 (Iron Bank), R4 (CVEs) | **Highest risk milestone.** Third-party dependencies (Game Warden, Iron Bank) and classified access coordination. |
| **MS3: Red** | R2 (access), R9 (Diode), R10 (compliance) | Moderate risk. Most unknowns are TS-program-specific. Budget upper ranges to absorb. |

---

## 7. Conversation Playbook

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
- Lead with the upfront: 30% of VV fee ($10,500) + 20% of tool dev — manageable first check
- Upfront outlay is ~$25K-$37K. That's the "first check."
- Infrastructure is the big number but it's **monthly and scales with deployment**
- **Key line:** "The upfront is ~$25K-$37K. After that, costs are milestone-gated — you only pay for tiers you deploy."

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
| "Can we just do Black?" | "Yes. Through Black MVP acceptance you're looking at ~$56K-$86K total (upfront + MS1). You get a working system, prove it out at the March event, and decide from there. The contract has milestone gates for exactly this." |
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
