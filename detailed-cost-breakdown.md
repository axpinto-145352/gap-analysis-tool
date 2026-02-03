# Gap Analysis Platform — Integrated Cost Breakdown & Talking Points
### Veteran Vectors Internal Reference | 6-Month Milestone Engagement

This document gives you line-by-line detail on every cost in the integrated contract so you can speak confidently about where money goes, why, and how to structure conversations.

---

## 1a. What We're Delivering (Not SaaS)

This is **not a SaaS product**. It's a **self-hosted, client-owned automation appliance** packaged as Docker container images.

**What that means:**
- The entire system — n8n (automation engine), PostgreSQL (database), NGINX (web server), and all 5 workflows — ships as portable container images
- Those images run on any environment that supports Docker (unclass) or Kubernetes (classified via Game Warden)
- The client owns everything: code, containers, data, infrastructure
- No shared tenancy, no VV-hosted servers, no subscription model
- The same container images built in Black move directly to Yellow and Red without rebuilding

**How to explain it:** "Think of it like delivering a turnkey appliance that happens to be software. We build it, package it in containers, hand you the containers and all the source code, and you run it wherever you need — your own server, AWS GovCloud, or Game Warden's classified K8s cluster. You own it completely."

**Why this matters for classified:** Container portability is what makes the Black → Yellow → Red progression possible. The images are the same — only the hosting environment changes. No re-architecture, no rebuild, no new codebase per tier.

---

## 1b. Classified Network Access Model

VV's lead operator holds an active TS/SCI clearance but is not currently sponsored under a facility clearance (FCL) tied to VV. This means direct VV access to SIPRNet/JWICS requires client action. The engagement is structured to work without it.

### Primary Model: Client-Executed Classified Testing

- VV builds, packages, and validates everything on **unclassified** environments
- VV delivers **detailed test scripts, deployment runbooks, and validation checklists** for each classified milestone
- **Client's cleared personnel** execute those scripts on SIPRNet (Yellow) and JWICS (Red)
- VV provides **real-time support from unclassified** (phone, chat, screen share of unclass replica) during classified testing windows
- All bugs, issues, and configuration changes are resolved by VV on unclass and re-delivered as updated container images

**Why this works:** The system is fully containerized. If it passes end-to-end testing on unclass (which VV validates directly), the only variables on classified are network-specific configuration (mail relay, DNS, firewall rules) — not application logic. The test scripts are designed to validate exactly those variables.

### Backup Model: Client-Sponsored VV Access

- Client organization sponsors VV operator's existing TS/SCI clearance onto their program
- Client provides SCIF access for VV operator to test directly on SIPRNet/JWICS
- This is faster for troubleshooting but requires the client's security office to process the access request

**Recommendation:** Start with the primary model. If classified testing reveals issues that are difficult to debug remotely, escalate to the backup model. The access sponsorship request can be initiated at contract award as a parallel track so it's ready if needed.

**Conversation tip:** "Our operator holds TS/SCI. We've structured the engagement so classified testing works without requiring you to sponsor our access — your team runs our test scripts and we support from unclass. But if you want us hands-on-keyboard on classified, we just need your security office to sponsor the existing clearance."

---

## 2. Contract Structure at a Glance

**Single 6-month contract** with three milestone gates (Black → Yellow → Red).

| Component | Amount |
|---|---|
| Tool development (all 3 milestones) | $73,000 - $133,000 |
| Infrastructure (Year 1) | $116,560 - $250,240 |
| VV development fee (flat) | $60,000 |
| VV retainer (15% of VV fee, Months 3-12) | $7,500 |
| **Year 1 Total** | **$257,060 - $450,740** |
| **Midpoint** | **~$354,000** |

---

## 3. Veteran Vectors Revenue Breakdown

### Development Fee — $60,000 (Flat)

This is your full 6-month engagement fee. It covers:

- Architecture design and technical planning across all 3 tiers
- n8n workflow development, integration engineering, Docker/Helm packaging
- Game Warden pipeline setup and container hardening coordination
- Testing support (UAT at March event, SIPRNet validation, JWICS acceptance)
- Operator training and system documentation
- Project management across all 3 milestones

**When it's paid:** Spread across all 4 milestones — 30% at contract award ($18,000), 25% at Black MVP acceptance ($15,000), 20% at Yellow operational ($12,000), 25% at Red operational ($15,000). This keeps VV revenue flowing with each deliverable.

**How to position:** "This is our engineering and project management fee for the full 6-month build. It covers architecture, development, testing, training, and operational acceptance across all three classification levels."

### Retainer — 15% of VV Fee ($9,000/year), Starting Month 3

The retainer kicks in when infrastructure is running and VV shifts from build mode to support mode. This is not a vague "advisory" fee — it covers concrete, recurring work.

**Retainer calculation:** 15% × $60,000 = **$9,000/year** = **$750/month**

**Year 1 retainer (Months 3-12 = 10 months):** $7,500

#### Container Lifecycle Management (the core of the retainer)

Containers are not patched in place like traditional servers. They follow a **rebuild-and-redeploy** cycle:

1. **VV monitors upstream releases** — n8n, PostgreSQL 16, NGINX, and all base image dependencies. Tracks CVE disclosures, version releases, and security advisories.
2. **VV rebuilds container images** — Updates the Dockerfile (e.g., bump `postgresql:16.2` → `16.3`), resolves any new CVEs, rebuilds the image.
3. **VV tests on unclassified** — Runs full end-to-end test suite against the updated images. Validates no regressions.
4. **VV delivers updated images** — Hands off tested images to the client for deployment.
5. **On classified tiers** — Updated images go through Game Warden pipeline again: push → ClamAV scan → Anchore scan → STIG check → stage → promote. Same process as initial deployment, just with a patched image.

**Update frequency:**
| Type | Frequency | Example |
|---|---|---|
| Critical CVE patches | Same-week rebuild | OpenSSL vulnerability, PostgreSQL auth bypass |
| Minor security patches | Monthly, batched | Dependency bumps, base image updates |
| Minor version upgrades | Quarterly | n8n 1.42 → 1.43, NGINX patch release |
| Major version upgrades | Annually, planned | PostgreSQL 16 → 17, n8n major release |

**Why this matters:** Without this, the client is responsible for tracking every upstream CVE, understanding which dependencies are affected, rebuilding images, and re-testing. The retainer means VV handles all of that — the client just deploys the updated images.

#### Operational Support

- **Incident response** — Priority SLA for production issues. VV triages, diagnoses, and delivers a fix or workaround.
- **Workflow modifications** — As operational needs evolve (new survey types, changed scoring logic, new report sections), VV adjusts n8n workflows. Note: n8n workflows live in the database, not the container image, so workflow changes don't require a container rebuild.
- **Infrastructure monitoring review** — Periodic review of system health, resource utilization, and alerting thresholds.
- **Database maintenance** — Backup verification, index tuning, storage management, query performance review.
- **Classified deployment support** — When updated images need to go through Game Warden pipeline, VV provides documentation and support for the promotion process.

#### Advisory & Planning

- **Enhancement scoping** — When the client wants new features (AI narrative, predictive trending, automated briefing slides), VV scopes the work, estimates cost, and plans implementation.
- **Quarterly architecture reviews** — Assess system health, identify optimization opportunities, plan for scaling.
- **Compliance posture updates** — As CMMC/NIST requirements evolve, VV assesses impact and recommends adjustments.
- **Scaling support** — For events like the May event (~150 users), VV load-tests and adjusts infrastructure/config as needed.

**How to position:** "The $750/month retainer isn't an advisory fee — it's hands-on-keyboard work. We monitor every upstream release, rebuild your container images with patches, test them, and hand them off ready to deploy. You also get priority support for production issues, workflow changes, and planning for future capabilities. Without it, your team is responsible for tracking CVEs across three open-source projects and three classification levels."

**Month-by-month retainer:**

| Month | VV Retainer |
|---|---|
| 1-2 | — (covered by $60K dev fee) |
| 3-12 | $750/month |

**Year 1 retainer total (Months 3-12 = 10 months):** **$7,500**

**How to position:** "Once we hand off each tier, the $750/month retainer ensures you have a dedicated team that knows this system. You're not re-onboarding a vendor every time something needs attention."

---

## 4. Tool Development Costs — Line-by-Line Detail

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

## 5. Infrastructure Costs — Where the Real Money Goes

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

## 6. Payment Schedule — How Cash Flows

### Upfront (Contract Award)

| Item | Low | High |
|---|---|---|
| 20% of tool development | $14,600 | $26,600 |
| VV fee — 30% ($18,000) | $18,000 | $18,000 |
| **Total upfront** | **$32,600** | **$44,600** |

### Month 2 (MS1: Black MVP Accepted)

| Item | Low | High |
|---|---|---|
| 30% of tool development | $21,900 | $39,900 |
| VV fee — 25% ($15,000) | $15,000 | $15,000 |
| Black infra (2 months accrued) | $260 | $540 |
| **Total at MS1** | **~$37,160** | **~$55,440** |

### Month 4 (MS2: Yellow Operational)

| Item | Low | High |
|---|---|---|
| 30% of tool development | $21,900 | $39,900 |
| VV fee — 20% ($12,000) | $12,000 | $12,000 |
| Yellow infra (2 months accrued) | $7,000 | $19,000 |
| VV retainer (Months 3-4) | $1,500 | $1,500 |
| **Total at MS2** | **~$42,400** | **~$72,400** |

### Month 6 (MS3: Red Operational)

| Item | Low | High |
|---|---|---|
| 20% of tool development | $14,600 | $26,600 |
| VV fee — 25% ($15,000) | $15,000 | $15,000 |
| Red infra (2 months accrued) | $20,000 | $38,000 |
| VV retainer (Months 5-6) | $1,500 | $1,500 |
| **Total at MS3** | **~$51,100** | **~$81,100** |

### Months 7-12 (Post-Engagement, Ongoing)

| Item | Monthly Low | Monthly High |
|---|---|---|
| All infra running | $13,630 | $28,770 |
| VV retainer | $750 | $750 |
| **Monthly total** | **~$14,380** | **~$29,520** |

---

## 7. Risk Assessment & Mitigation — Full Detail

### Risk Matrix

| # | Risk | Likelihood | Impact | Severity | Milestone Affected |
|---|---|---|---|---|---|
| R1 | Game Warden onboarding delays | Medium | High | **High** | MS2 (Yellow) |
| R2 | Classified testing coordination | Medium | Medium | **Medium** | MS2, MS3 |
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

**R2: Classified Testing Coordination — MEDIUM (downgraded from HIGH)**
- *What happens:* Classified testing requires coordination between VV (unclass) and client personnel (on SIPRNet/JWICS). Communication latency or unfamiliar test procedures slow progress.
- *Why it's medium, not high:* The primary access model eliminates the dependency on VV clearance sponsorship. Client personnel test on classified using VV-provided scripts; VV supports from unclass. This avoids the bureaucratic delays of clearance sponsorship entirely.
- *Primary mitigation (Option 4):* VV delivers detailed test scripts, deployment runbooks, and validation checklists. Client's cleared personnel execute on classified. VV provides real-time support from unclass (phone, chat, screen share of unclass replica). All issues resolved on unclass and re-delivered as updated containers.
- *Backup mitigation (Option 2):* Client sponsors VV operator's existing TS/SCI clearance onto their program and provides SCIF access. This enables VV to test directly on classified. Initiate sponsorship request at contract award as a parallel track so it's available if needed.
- *Budget impact:* Primary model has no additional cost — test scripts are part of the standard deliverable. Backup model depends on client's sponsorship timeline (no cost to VV, but calendar time for the client's security office).
- *Conversation tip:* "We've structured this so your team runs classified testing with our scripts and real-time support. If you'd rather have us hands-on-keyboard on classified, we just need your security office to sponsor our operator's existing TS/SCI."

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
- *Mitigation:* Each milestone has defined deliverables and acceptance criteria. Scope changes during Months 1-2 are handled within the $60K VV fee if minor. After Month 3, change requests route through the retainer relationship. Major scope changes require a separate SOW.
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
| **MS2: Yellow** | R1 (Game Warden), R2 (testing coord), R3 (Iron Bank), R4 (CVEs) | **Highest risk milestone.** Third-party dependencies (Game Warden, Iron Bank). Classified testing mitigated by client-executed model. |
| **MS3: Red** | R2 (testing coord), R9 (Diode), R10 (compliance) | Moderate risk. Most unknowns are TS-program-specific. Budget upper ranges to absorb. |

---

## 8. Government-Ready Product — Downstream Sale Considerations

### The Sales Chain

```
VV (builds) → Defense Contractor (buys, operates, resells) → Government Entity (end user)
```

**Your contract with the defense contractor is commercial B2B.** No FAR/DFARS clauses, no CDRLs, no SAM.gov registration required for this sale. Standard commercial terms.

**But the product must be government-ready** so the contractor can resell it downstream. Everything below is about making the product sellable — not about making your contract compliant.

### What VV Must Build Into the Product

**1. Data Rights / Intellectual Property — CRITICAL**

The contractor needs a clean IP chain to resell to government. Government contracts typically invoke DFARS 252.227-7014 (technical data) and 252.227-7018 (software).

- **Custom code** (n8n workflows, Helm charts, configs, migration scripts, report templates): Contractor receives **unlimited rights**. They can modify, redistribute, and deliver to government without restriction.
- **Open-source components**: Retain their existing licenses. The contractor must disclose these to the government buyer.
  - n8n: Sustainable Use License (free for self-hosted; no resale restrictions on the instance, but n8n the company retains the codebase)
  - PostgreSQL: PostgreSQL License (permissive, similar to MIT)
  - NGINX: BSD 2-clause (permissive)
  - Metabase: AGPL v3 (open-source; self-hosted use is fine)
- **Deliverable:** IP Rights Summary document delivered at MS1, listing all components, their licenses, and the contractor's rights to each.

*Conversation tip:* "You get unlimited rights to everything we build custom. The open-source components carry their existing licenses — all permissive and compatible with government use. We deliver a full IP rights summary so your contracting team has clean documentation for the gov sale."

**2. Section 508 Accessibility**

Any IT product sold to the government must comply with Section 508 of the Rehabilitation Act — meaning accessible to users with disabilities.

- Web survey forms: WCAG 2.1 AA compliance (keyboard navigation, screen reader support, color contrast, form labels)
- Dashboard views: Accessible charts and tables (alt text, data tables alongside visualizations)
- Reports: Generated in accessible markdown/HTML format
- **Deliverable:** Voluntary Product Accessibility Template (VPAT) or Section 508 conformance statement delivered at MS1.

*Budget note:* Basic 508 compliance is built into the MS1 development cost. If the contractor's gov buyer requires a formal VPAT (common for larger acquisitions), that's an additional $2K-$4K effort. Flag this early.

*Conversation tip:* "We build to WCAG 2.1 AA from the start. If the government buyer requires a formal VPAT, we can produce one — it's a small additional effort."

**3. Software Supply Chain / SCRM**

Executive Order 14028 (Improving the Nation's Cybersecurity) requires software supply chain transparency for products sold to the federal government. NIST SP 800-218 (SSDF) is the standard.

- **Software Bill of Materials (SBOM):** Machine-readable inventory of every component, dependency, and version in the container images. Generated automatically during build.
- **Provenance documentation:** Where each component comes from, who maintains it, and its security track record.
- **n8n supply chain note:** n8n GmbH is a German company. The software is open-source and source code is publicly auditable. For programs with strict supply chain requirements, flag this early — some government buyers may require a supply chain risk assessment for foreign-origin software.
- **Deliverable:** SBOM (CycloneDX or SPDX format) and supply chain summary delivered at each milestone.

*Conversation tip:* "We generate a full SBOM at every release. Every component is documented — origin, license, maintainer. n8n is open-source and publicly auditable. If the gov buyer has SCRM concerns about foreign-origin software, we can walk through the risk assessment."

**4. CMMC / NIST 800-171 Compliance (Already Covered)**

Already built into the architecture from day one (see Slides 12 and the security section of the original proposal). The compliance documentation (SSP, POA&M) delivered at Yellow/Red milestones is what the contractor will hand to the government buyer.

**5. Game Warden / ATO Readiness (Already Covered)**

The product inherits ATO through Game Warden. The contractor doesn't need to pursue a standalone ATO — Game Warden handles certification. The contractor just needs to show the government buyer that the product is deployed on a Game Warden-accredited platform.

**6. Transition / Exit Plan**

Government contracts require a plan for what happens when the contract ends. Since the contractor will be the operator:

- All source code, IaC, and documentation delivered at each milestone
- Operator training ensures the contractor's team can manage without VV
- The 15% retainer is optional after the 6-month engagement — the contractor can self-operate
- If the government eventually takes over operations, the contractor can hand off the same deliverables VV provided
- **Deliverable:** Transition Plan document delivered at MS3 (Red), covering handoff procedures, admin credentials, runbook, and escalation contacts.

**7. Key Personnel**

Defense contractor clients (and their government buyers) often want assurance that specific people will be on the project.

- Designate VV's lead operator as key personnel for the engagement
- If the lead is unavailable for >2 weeks, VV provides written notice and a qualified replacement
- This is a contract clause, not a product feature — include it in the terms.

### What the Contractor Handles (Not VV's Responsibility)

| Item | Why It's the Contractor's Problem |
|---|---|
| SAM.gov registration + CAGE code + UEI | Required to receive government payments. Contractor already has these or needs to obtain them. |
| NAICS code selection | Determines contract set-aside eligibility. Likely 541512 (Computer Systems Design) or 541519 (Other Computer Related Services). |
| Contract vehicle | GSA Schedule, OTA, SBIR, sole-source, etc. Contractor decides based on their relationship with the gov buyer. |
| FAR/DFARS compliance | Applies to the contractor's gov contract, not to VV's commercial engagement. |
| CDRLs | Contractor maps VV milestone deliverables to their gov contract's CDRL requirements. VV deliverables are designed to be CDRL-compatible. |
| Insurance (cyber liability, E&O, GL) | Contractor carries this for the gov contract. VV should carry standard business insurance for the commercial engagement. |
| Small business status / set-asides | If the contractor is SDVOSB, 8(a), HUBZone, etc., that's their competitive advantage for the gov sale. |

*Conversation tip:* "We build the product to be government-ready — 508, SBOM, CMMC, Game Warden ATO. You handle the contracting side with the government buyer. Our deliverables are designed to drop directly into your CDRLs."

### VV Deliverables Mapped to Gov Sale Requirements

| VV Deliverable | Delivered At | Gov Sale Requirement It Satisfies |
|---|---|---|
| IP Rights Summary | MS1 | DFARS data rights disclosure |
| Section 508 / VPAT | MS1 | Section 508 conformance |
| SBOM | Each milestone | EO 14028 / NIST SSDF supply chain transparency |
| SSP + POA&M | MS2, MS3 | CMMC / NIST 800-171 compliance documentation |
| Operator Training + Docs | MS1 | Transition/sustainment planning |
| Transition Plan | MS3 | Contract closeout / government takeover planning |
| Container Images + Helm Charts | Each milestone | Deployable product artifact |
| Source Code + IaC | Each milestone | Unlimited rights deliverable |

---

## 9. Conversation Playbook

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
- Lead with the upfront: 30% of VV fee ($18,000) + 20% of tool dev — manageable first check
- Upfront outlay is ~$33K-$45K. That's the "first check."
- Infrastructure is the big number but it's **monthly and scales with deployment**
- **Key line:** "The upfront is ~$33K-$45K. After that, costs are milestone-gated — you only pay for tiers you deploy."

### Conversation 4: Game Warden Deep Dive (If Classified Is the Goal)
- ATO inheritance: weeks vs. 6-18 months
- Pipeline walkthrough: push → scan → stage → promote
- IL levels: IL2/IL4 (unclass), IL5/IL6 (Secret), TS/SCI
- Multi-tenant vs. single-tenant economics
- **Key line:** "Game Warden replaces a $200K-$500K, 6-18 month ATO process with a platform fee and a weeks-long onboarding."

### Objection Handling

| Objection | Response |
|---|---|
| "That's a lot of money." | "The infrastructure costs are Game Warden + AWS — that's the price of classified deployment. The alternative is $200K-$500K for standalone ATO. Our VV fee is $60K for a 6-month build across 3 classification levels — that's the architecture, engineering, testing, and PM for the entire engagement." |
| "Can we just do Black?" | "Yes. Through Black MVP acceptance you're looking at ~$70K-$100K total (upfront + MS1). You get a working system, prove it out at the March event, and decide from there. The contract has milestone gates for exactly this." |
| "Why not fix Power Automate?" | "Power Automate can't deploy to classified networks. It has no Game Warden pathway. And you'd still have 10+ siloed flows and broken Excel connections." |
| "What's the retainer for?" | "Once we build it, you need someone who knows the system for maintenance, troubleshooting, and future enhancements. The $750/month retainer starting Month 3 ensures priority support without re-onboarding." |
| "Can the retainer start later?" | "It starts Month 3 — when classified infra is live and there's actual infrastructure to support. During Months 1-2, the $60K dev fee covers everything." |

---

## 10. Quick Reference — Tools & What They Do

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
