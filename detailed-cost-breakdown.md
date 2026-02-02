# Gap Analysis Platform — Detailed Cost Breakdown & Talking Points
### Veteran Vectors Internal Reference

This document breaks down every cost line item so you can speak intelligently about where money goes, why, and how to scope conversations with the client.

---

## 1. Veteran Vectors Fees (Your Revenue)

These are **separate from** all tool, infrastructure, and platform costs below.

| Item | Amount | What It Covers |
|---|---|---|
| **Development Fee** | $30,000 (flat) | Architecture design, n8n workflow development, integration engineering, Docker/Helm packaging, testing, UAT support, operator training, documentation, project management |
| **Retainer (15%)** | 15% of total contract value | Ongoing advisory, maintenance coordination, escalation support, enhancement scoping, quarterly check-ins, priority support SLA |

**How to position:** The $30K is your build cost — the hands-on-keyboard engineering to stand this up. The 15% retainer is your ongoing relationship — the client gets a team that knows the system inside and out, available for troubleshooting, enhancements, and scaling support.

**Retainer examples by scope:**
- Black only (~$28K tool/infra): 15% = ~$4,200/yr retainer → **Total VV revenue: ~$34,200**
- All tiers (~$357K tool/infra): 15% = ~$53,550/yr retainer → **Total VV revenue: ~$83,550**

---

## 2. Tier 1 — Black (Unclassified MVP) Costs in Detail

### Development Line Items ($20K - $31K range)

**n8n Workflow Build-Out — $8,000 - $12,000**
- This is the core product: 5 production workflows in n8n
- Survey distribution with roster-driven targeting and auto-reminders
- Webhook-based form submission handler with validation/sanitization
- Analytics engine: Likert distribution, NPS scoring, factor aggregation, time-series
- Report generator: templated consultancy report with rankings and recommendations
- Survey lifecycle manager: auto open/close/warn
- *Why the range:* Lower end assumes clean data and straightforward requirements. Upper end accounts for complex business logic, edge cases, and iteration cycles.
- *Conversation tip:* This is where the automation value lives. Each workflow replaces hours of manual work per survey cycle.

**Data Schema Design & Migration — $2,000 - $3,000**
- Design PostgreSQL schema for demographics, survey responses, gap definitions, survey config
- Write migration scripts to import existing Excel/Forms data
- Set up relationships, indexes, and constraints
- *Why it matters:* This is what kills the Excel-to-Power BI fragility permanently. One-time cost to do it right.

**Dashboard Setup (Power BI or Metabase) — $3,000 - $5,000**
- If Power BI: build connector to PostgreSQL, create/update dashboards
- If Metabase: deploy open-source BI tool, build equivalent dashboards
- Filtering by demographic, working group, time period
- *Why the range:* Power BI connector is cheaper if they already have dashboards. Metabase from scratch costs more upfront but has $0 licensing.

**Consultancy Report Template & Generator — $2,000 - $3,000**
- Markdown-based templated report
- Executive summary, methodology, top-10 priority gaps, factor analysis tables, trend analysis
- Actionable recommendations categorized: Immediate (NPS < -20), Monitor (-20 to 0), Maintain (> 0)
- *Conversation tip:* This replaces the manual report-writing that takes analysts hours. Auto-generated on demand.

**Docker Containerization & Hardening — $1,500 - $2,500**
- Docker Compose setup: n8n, PostgreSQL, NGINX as services
- Non-root containers, minimal base images, health checks
- Volume encryption, network isolation between services
- This is also the foundation for Game Warden deployment later
- *Why it matters:* Containerization is what makes classified deployment possible. Do it right in Black, reuse in Yellow/Red.

**NGINX TLS & Security Configuration — $500 - $1,000**
- TLS 1.2+ termination, security headers (HSTS, CSP, X-Frame-Options)
- Rate limiting to prevent abuse
- Reverse proxy routing to n8n and dashboard
- *Straightforward cost.* Standard security configuration.

**Integration Testing & UAT — $2,000 - $3,000**
- End-to-end testing with sample data
- Power BI connector validation
- User acceptance testing at March event with ~15 real users
- Bug fixes and iteration based on feedback
- *Conversation tip:* This is the March event milestone. Live users, real data, real feedback.

**Documentation & Operator Training — $1,000 - $1,500**
- System administration guide
- Workflow modification guide (so operators can adjust without the developer)
- Troubleshooting runbook
- 1-2 training sessions
- *Why it matters:* Eliminates the single-operator bottleneck. Anyone can run this.

### Monthly Infrastructure ($130 - $270/mo)

| Item | Low | High | Notes |
|---|---|---|---|
| AWS GovCloud compute (t3.medium) | $75 | $150 | Single VM runs everything. t3.medium = 2 vCPU, 4GB RAM. Sufficient for <50 users. |
| PostgreSQL (RDS or self-hosted) | $30 | $75 | RDS is easier but costs more. Self-hosted on same VM is cheaper. |
| S3 backup storage | $5 | $10 | Daily encrypted pg_dump backups, 30-day retention. Negligible cost. |
| Domain + TLS cert | $12 | $15 | Annual domain registration + cert (or free via Let's Encrypt). |
| SMTP relay (SES) | $10 | $20 | Amazon SES pricing: $0.10 per 1,000 emails. Even at 1,000 emails/mo this is ~$10. |

**Year 1 total infrastructure: $1,560 - $3,240**

**Key point:** Black tier is cheap to run. The cost is almost entirely development labor.

---

## 3. Tier 2 — Yellow (Secret) Costs in Detail

### Development Line Items ($23K - $40K range)

**Kubernetes/Helm Chart Conversion — $4,000 - $6,000**
- Convert Docker Compose to Helm charts for K8s deployment
- Define services, deployments, persistent volume claims, config maps, secrets
- Game Warden requires K8s — this is the translation layer
- *Conversation tip:* If you already have K8s experience in-house, this is straightforward. The cost is the conversion and testing, not learning K8s.

**Iron Bank Image Submission for n8n — $3,000 - $5,000**
- Iron Bank is DoD's hardened container registry
- PostgreSQL and NGINX already exist in Iron Bank
- n8n does NOT — requires submission: Dockerfile hardening, CVE remediation, documentation
- *Why the range:* Depends on how many CVEs exist in n8n's dependency tree at submission time.
- *Cost reduction:* If the org accepts a non-Iron Bank n8n image with equivalent hardening, this drops significantly.

**Game Warden Onboarding & Pipeline Integration — $5,000 - $8,000**
- Account setup, access provisioning, pipeline configuration
- CI/CD integration: push images → scan → stage → promote
- Working with Second Front Systems support team
- *This is a one-time cost.* Once onboarded, deployments are automated.

**Acceptance Baseline Criteria Remediation — $3,000 - $6,000**
- Resolve all critical/high CVEs in container images
- Apply STIG hardening (non-root, file permissions, removed unnecessary packages)
- Pass Anchore vulnerability scanning (NIST 800-53 aligned)
- *Why the range:* Depends entirely on CVE count at time of submission. Clean images = lower end.

**Remove External API Dependencies — $2,000 - $4,000**
- Black tier may use Google Sheets/Excel Online for familiar interface
- Yellow tier: ALL external API calls must be removed
- Migrate any Sheets integration to PostgreSQL-only
- *Conversation tip:* This is a hard requirement for classified. No internet calls, period.

**Classified Email Relay Integration — $1,000 - $2,000**
- Configure SMTP to use approved classified mail relay (not commercial SES)
- Test delivery on SIPRNet
- *Straightforward.* Depends on which mail relay the org uses.

**SIPRNet Testing & Validation — $3,000 - $5,000**
- Deploy to staging on classified network
- Test all 5 workflows end-to-end on SIPRNet
- Validate no external calls, no broken dependencies
- *Requires classified access and time on the network.* Cost is primarily labor + access coordination.

**Compliance Documentation — $2,000 - $4,000**
- System Security Plan (SSP)
- Plan of Action & Milestones (POA&M)
- Game Warden-specific documentation templates
- *Note:* Game Warden simplifies this significantly vs. standalone ATO. But docs are still required.

### Monthly Infrastructure ($3,500 - $9,500/mo)

| Item | Low | High | Notes |
|---|---|---|---|
| **Game Warden platform fee** | $3,000 | $8,000 | **This is the dominant cost.** Single-tenant K8s cluster on AWS GovCloud Secret Region. Includes managed K8s, monitoring, patching, compliance tooling. |
| AWS GovCloud Secret Region compute | $500 | $1,500 | Compute within the Game Warden cluster. Premium over commercial AWS. |
| Managed services | Included | Included | Monitoring and patching included in Game Warden fee. |

**Year 1 total infrastructure: $42,000 - $114,000**

**Key talking points:**
- Game Warden fee looks expensive but **replaces independent ATO ($200K-$500K+) and 6-18 months of calendar time**
- Multi-tenant cluster (sharing with other apps) can reduce platform fee significantly
- If the org already has a Game Warden contract, onboarding is cheaper and platform fees may already be budgeted

---

## 4. Tier 3 — Red (TS/SCI) Costs in Detail

### Development Line Items ($30K - $62K range)

**TS Environment Provisioning & Access — $3,000 - $5,000**
- Coordinate access to AWS Top Secret Region
- Provisioning requests, security briefings, access approvals
- *Primarily labor and coordination time.*

**Additional SCI Access Controls — $4,000 - $7,000**
- Compartmented access controls beyond standard Secret
- Role-based restrictions by SCI program
- Enhanced access logging
- *Why more expensive:* SCI requirements are program-specific and often require custom implementation.

**AWS Diode Cross-Domain Deployment — $5,000 - $10,000**
- AWS Diode = the mechanism to transfer data/images from unclass → Secret → TS
- Configure cross-domain transfer pipeline
- Validate image integrity post-transfer
- *This is specialized work.* Few people have experience with AWS Diode. Premium cost reflects scarcity.

**Enhanced Audit Logging & Monitoring — $2,000 - $4,000**
- TS environments require more granular audit trails
- Enhanced monitoring dashboards for security events
- Alert configuration for anomalous activity

**TS-Specific Compliance Documentation — $3,000 - $6,000**
- Additional SSP sections for TS
- ICD 503 alignment (if applicable)
- Program-specific security documentation

**Security Assessment & Pen Testing Support — $5,000 - $10,000**
- Support security assessment team during evaluation
- Remediate findings
- *Note:* This may be done by the org's own security team or a third party. Cost here is our labor to support them.

**JWICS Operational Acceptance Testing — $3,000 - $5,000**
- End-to-end testing on JWICS (Top Secret network)
- Validate all functionality in fully air-gapped environment
- *Requires TS clearance and physical access to TS facilities.*

**External Compliance Team Involvement — $5,000 - $15,000**
- If the org brings in external compliance assessors
- Our labor to support their review, answer questions, remediate findings
- *Widest range:* Depends entirely on how thorough the assessment is.

### Monthly Infrastructure ($10,000 - $19,000/mo)

| Item | Low | High | Notes |
|---|---|---|---|
| **Game Warden platform fee (TS region)** | $8,000 | $15,000 | **Premium pricing** for Top Secret region. Fewer customers, higher security overhead, more expensive AWS TS Region. |
| AWS Top Secret Region compute | $1,500 | $3,000 | Significant premium over GovCloud commercial or Secret. |
| Enhanced monitoring & compliance tools | $500 | $1,000 | Additional tooling required at TS level. |

**Year 1 total infrastructure: $120,000 - $228,000**

---

## 5. Full Program Summary with Veteran Vectors Fees

### Low Estimate (All 3 Tiers)

| Category | Cost |
|---|---|
| Black development | $20,000 |
| Yellow development | $23,000 |
| Red development | $30,000 |
| **Subtotal tool development** | **$73,000** |
| Black infra (Year 1) | $1,560 |
| Yellow infra (Year 1) | $42,000 |
| Red infra (Year 1) | $120,000 |
| **Subtotal infrastructure** | **$163,560** |
| **Tool + Infra Total** | **$236,560** |
| Veteran Vectors development fee | $30,000 |
| Veteran Vectors retainer (15% of $236,560) | $35,484 |
| **Grand Total (Year 1)** | **$302,044** |

### High Estimate (All 3 Tiers)

| Category | Cost |
|---|---|
| Black development | $31,000 |
| Yellow development | $40,000 |
| Red development | $62,000 |
| **Subtotal tool development** | **$133,000** |
| Black infra (Year 1) | $3,240 |
| Yellow infra (Year 1) | $114,000 |
| Red infra (Year 1) | $228,000 |
| **Subtotal infrastructure** | **$345,240** |
| **Tool + Infra Total** | **$478,240** |
| Veteran Vectors development fee | $30,000 |
| Veteran Vectors retainer (15% of $478,240) | $71,736 |
| **Grand Total (Year 1)** | **$579,976** |

### Black MVP Only (Most Likely Starting Point)

| Category | Low | High |
|---|---|---|
| Tool development | $20,000 | $31,000 |
| Infrastructure (Year 1) | $1,560 | $3,240 |
| **Tool + Infra** | **$21,560** | **$34,240** |
| VV development fee | $30,000 | $30,000 |
| VV retainer (15%) | $3,234 | $5,136 |
| **Grand Total** | **$54,794** | **$69,376** |

---

## 6. Conversation Setup Guide

### Conversation 1: The Problem & Vision (Non-Technical)
- Lead with the pain: broken Excel connections, 10+ flows, single-operator risk, no classified path
- Show Before/After (Slide 4)
- Don't get into tools yet — stay on business value

### Conversation 2: The Technical Solution (With Technical Stakeholders)
- Walk through the 5 workflows and tech stack
- Emphasize: open-source, no vendor lock-in, containerized
- Show Game Warden pathway — this is the differentiator vs. "just use Power Automate better"

### Conversation 3: Pricing & Phasing
- Start with Black MVP pricing — it's the easiest yes (~$55K-$69K all-in with VV fees)
- Explain milestone gates: they can stop after Black if it doesn't deliver
- Classified tiers are where infrastructure costs dominate — set expectation that Game Warden fees are real but replace $200K-$500K ATO
- Position VV's $30K dev fee as the build cost, 15% retainer as the relationship

### Conversation 4: Game Warden Deep Dive (If They Want Classified)
- Explain ATO inheritance: weeks vs. 6-18 months
- Walk through the deployment pipeline: push → scan → stage → promote
- Discuss IL levels: IL2/IL4 (unclass), IL5/IL6 (Secret), TS/SCI
- Multi-tenant vs. single-tenant cluster economics

### Key Phrases to Use
- "The tool is ready to deploy at any classification level because it's containerized from day one."
- "Game Warden replaces a 6-18 month, $200K-$500K ATO process with weeks and a platform fee."
- "We can start with Black at ~$55K and expand based on results. No commitment beyond the first milestone."
- "The 15% retainer means you have a team that knows this system — not a vendor you have to re-onboard every time something changes."
- "All open-source. No per-user licensing. No vendor lock-in."

### Tools & Setup Reference

| Tool | What It Is | Setup Needed |
|---|---|---|
| **n8n** | Visual automation platform (like Power Automate but self-hosted) | Docker install, workflow import, webhook configuration |
| **PostgreSQL** | Database replacing Excel | Schema creation, data migration from existing Excel/Forms |
| **NGINX** | Web server / reverse proxy | TLS cert, security headers, routing config |
| **Docker** | Container runtime | Install on host, docker-compose up |
| **Helm** | Kubernetes package manager (Yellow/Red only) | Chart creation, Game Warden pipeline config |
| **Game Warden** | DoD DevSecOps PaaS by Second Front Systems | Account onboarding, pipeline setup, image submission |
| **Metabase** | Open-source BI dashboard (Power BI alternative) | Docker install, PostgreSQL connection, dashboard build |
| **AWS GovCloud** | Government-compliant AWS region | Account provisioning, IAM setup, VPC config |

---
