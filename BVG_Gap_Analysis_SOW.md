# STATEMENT OF WORK (SOW)
## BETWEEN VETERAN VECTORS AND BVG & COMPANY

---

**Client Legal Name:** BVG & CO CONSULTING LLC

**Client Jurisdiction:** Florida

**Client Registered Address:** Eustis, FL

**Client Representative:** [CLIENT REPRESENTATIVE NAME]

---

**Contractor:** VETERAN VECTORS LLC

**EIN:** 39-3991719

**Registered Address:** 32 N Gould St, Sheridan WY 82801

**Representative:** Anthony Pinto, Founder

**Email:** anthony@veteranvectors.com

---

**Project Name:** Gap Analysis Automation Platform

**Agreement Date:** [DATE SIGNED]

**Project Start Date:** [START DATE]

**Estimated Completion:** 6 months from Project Start Date

---

## TABLE OF CONTENTS

1. PROJECT OVERVIEW
2. SCOPE OF WORK
3. DELIVERABLES
4. PROJECT TIMELINE AND MILESTONES
5. INVESTMENT AND PAYMENT TERMS
6. CLIENT RESPONSIBILITIES
7. ACCEPTANCE CRITERIA
8. CHANGE MANAGEMENT AND SCOPE CONTROL
9. INTELLECTUAL PROPERTY RIGHTS
10. CONFIDENTIALITY
11. DATA PROTECTION AND COMPLIANCE
12. WARRANTIES AND LIMITATIONS OF LIABILITY
13. INDEMNIFICATION
14. TERM AND TERMINATION
15. GENERAL PROVISIONS
16. AUTHORIZATION AND SIGNATURES

---

## 1. PROJECT OVERVIEW

### 1.1 Project Background

BVG & Company currently operates a gap analysis workflow built on Microsoft Forms, Excel, Power Automate, and Power BI. This system experiences frequent breakages due to Excel-to-Power BI connection fragility, relies on 10+ siloed Power Automate flows with no version control, and has no pathway to deployment on classified networks (Secret/TS/SCI) where BVG's government clients operate.

The current system creates a single-operator knowledge dependency, lacks automated report generation, and cannot leverage AI/narrative features on classified networks due to internet egress requirements.

### 1.2 Project Objectives

Veteran Vectors will design, develop, and deploy a containerized Gap Analysis Automation Platform that:

1. **Replaces fragile Excel-based data storage** with PostgreSQL for reliable, ACID-compliant data persistence
2. **Consolidates 10+ Power Automate flows** into 5 unified n8n workflows with version control
3. **Automates report generation** including top-10 gaps, factor analysis, and trend tracking
4. **Enables classified deployment** via Game Warden on AWS GovCloud (IL2-IL6) and AWS Secret/Top Secret Regions
5. **Eliminates single-operator dependency** through documentation, training, and self-contained deployment artifacts

### 1.3 Success Criteria

The project will be deemed successful when:

- All 5 core workflows pass end-to-end testing with live user data
- Unclassified (Black) tier is operational and validated at the March event (~15 users)
- Secret (Yellow) tier is deployed and operational on SIPRNet via Game Warden
- TS/SCI (Red) tier is deployed and operational on JWICS via Game Warden
- Client personnel can independently operate the system using delivered documentation
- All compliance documentation (SSP, POA&M, SBOM) is accepted by Client

---

## 2. SCOPE OF WORK

### 2.1 Services to be Provided

Veteran Vectors will provide the following services as part of this engagement:

**Architecture & Design:**
- Technical architecture design across three classification tiers (Unclassified, Secret, TS/SCI)
- Database schema design (PostgreSQL) for surveys, responses, demographics, gaps, and reports
- Workflow design for 5 core automation processes
- Game Warden deployment architecture and Helm chart development

**Development & Build:**
- n8n workflow development (5 workflows: Survey Distribution, Form Submission Handler, Data Processing & Analytics, Report Generator, Lifecycle Manager)
- Docker containerization (n8n, PostgreSQL 16, NGINX)
- Helm chart conversion for Kubernetes/Game Warden deployment
- Iron Bank image hardening and submission support for n8n
- Integration with classified email relay systems

**Compliance & Security:**
- CMMC Level 2 / NIST 800-171 compliance implementation
- STIG hardening for all container images
- System Security Plan (SSP) development
- Plan of Action & Milestones (POA&M) documentation
- Software Bill of Materials (SBOM) generation at each milestone
- Section 508 / WCAG 2.1 AA accessibility compliance

**Testing & Validation:**
- Unit and integration testing on unclassified environments
- Test script development for classified testing (executed by Client personnel)
- Real-time support during classified testing windows
- User acceptance testing coordination at March event

**Training & Knowledge Transfer:**
- Operator training sessions (1-2 sessions per milestone)
- Administrator documentation and runbooks
- Workflow modification guides
- Recorded walkthrough videos

### 2.2 Included Activities

The scope includes the following activities:

- Stakeholder interviews and requirements documentation
- Access to existing Power Automate flows, Excel data, and Power BI dashboards for migration analysis
- Technical architecture design and review sessions
- Prototype development and demonstration
- Game Warden onboarding coordination with Second Front Systems
- Iron Bank image submission coordination (n8n)
- AWS Diode cross-domain transfer configuration (for Red tier)
- Compliance documentation development
- User acceptance testing coordination
- Training session delivery
- Post-milestone bug fixes within warranty period

### 2.3 Explicitly Excluded from Scope

The following items are explicitly excluded from this project scope:

- **Ongoing managed services** beyond the retainer scope defined in Section 5
- **Game Warden platform fees** — billed directly by Second Front Systems to Client
- **AWS infrastructure costs** — billed directly by AWS to Client
- **Third-party platform subscriptions** not specified in this SOW
- **Data migration** from systems other than the existing Microsoft Forms/Excel/Power BI stack
- **Custom SCI compartment logic** beyond standard role-based access control
- **Integration with systems** not listed in the technical architecture
- **Hardware procurement** or physical infrastructure
- **Clearance sponsorship processing** — Client's security office responsibility
- **Government contracting activities** (SAM.gov registration, FAR/DFARS compliance, CDRLs) for downstream government sale — Client's responsibility

### 2.4 Assumptions and Dependencies

This project scope is based on the following assumptions:

**Client-Provided:**
- Client will provide timely access to AWS GovCloud account (Black tier)
- Client has or will obtain a Game Warden contract with Second Front Systems (Yellow/Red tiers)
- Client will provide classified email relay configuration for SIPRNet and JWICS
- Client personnel with appropriate clearances will be available for classified testing windows
- Client will designate a primary point of contact with decision-making authority
- Existing Power BI dashboards can be preserved, or Metabase is an acceptable alternative

**Technical:**
- n8n dependency tree CVE count is within normal range (~$3K-$6K remediation budget)
- No custom SCI compartment logic required beyond standard RBAC
- March event timeline is firm and drives MS1 completion date
- PostgreSQL and NGINX are already in Iron Bank; only n8n requires new submission

**If assumptions prove incorrect, scope may require adjustment via the change management process in Section 8.**

---

## 3. DELIVERABLES

Veteran Vectors will provide the following deliverables as part of this project. Each deliverable includes defined acceptance criteria and delivery dates.

| # | Deliverable | Description | Acceptance Criteria | Due Date |
|---|---|---|---|---|
| 1 | Black MVP System | n8n + PostgreSQL + NGINX in Docker Compose with all 5 workflows | End-to-end test passes with sample data; March event UAT successful | Month 2 |
| 2 | Operator Documentation (Black) | Architecture diagram, admin runbook, workflow modification guide | Client operator can perform basic operations independently | Month 2 |
| 3 | Yellow Deployment Package | Helm charts, hardened container images, Game Warden pipeline config | Deploys successfully to Game Warden staging environment | Month 4 |
| 4 | Compliance Documentation (Yellow) | SSP, POA&M, SBOM for Secret deployment | Accepted by Client security team | Month 4 |
| 5 | Red Deployment Package | AWS Diode config, TS-hardened images, enhanced audit logging | Deploys successfully to AWS Top Secret Region | Month 6 |
| 6 | Compliance Documentation (Red) | TS-specific SSP addendum, SBOM update | Accepted by Client security team | Month 6 |
| 7 | Training Materials | Recorded walkthroughs, training slide decks, quick reference guides | Client personnel complete training successfully | Each milestone |
| 8 | Source Code & IaC | All custom code, Docker Compose, Helm charts, Terraform/CloudFormation templates | Client can reproduce deployment from artifacts | Each milestone |
| 9 | IP Rights Summary | Documentation of all component licenses and Client's rights | Legal review complete | Month 2 |
| 10 | Transition Plan | Handoff procedures, admin credentials, escalation contacts | Client can operate independently | Month 6 |

### 3.1 Standard Deliverables

Unless otherwise specified, all milestones include these standard deliverables:

- Project scope document and detailed project plan
- Technical specifications and architecture documentation
- Developed automation solution (production-ready container images)
- Standard Operating Procedure (SOP) documentation
- Testing reports and quality assurance documentation
- Knowledge transfer and training materials
- Recorded walkthrough video demonstrating the solution
- Software Bill of Materials (SBOM) in CycloneDX or SPDX format

---

## 4. PROJECT TIMELINE AND MILESTONES

### 4.1 Project Duration

**Project Start Date:** [START DATE]

**Estimated Completion Date:** 6 months from start

**Total Duration:** 6 months

### 4.2 Project Phases and Milestones

The project is structured across three classification tiers with milestone gates:

| Phase | Milestone | Key Activities | Duration | VV Fee Payment | Tool Dev Payment | Target Date |
|---|---|---|---|---|---|---|
| **MS1: Black MVP** | Unclassified system operational | Docker deployment, 5 workflows, March event UAT, operator training | Months 1-2 | 30% ($18,000) at contract + 25% ($15,000) at acceptance | 20% at contract + 30% at acceptance | Month 2 |
| **MS2: Yellow Ops** | Secret system operational on SIPRNet | Helm conversion, Iron Bank submission, Game Warden deployment, compliance docs | Months 2-4 | 20% ($12,000) | 30% | Month 4 |
| **MS3: Red Ops** | TS/SCI system operational on JWICS | AWS Diode transfer, TS hardening, JWICS acceptance testing | Months 4-6 | 25% ($15,000) | 20% | Month 6 |

**Parallel Activities:**
- Game Warden onboarding begins Month 1 (parallel to MS1)
- Iron Bank submission for n8n begins Month 2 (parallel to MS1/MS2)
- Clearance sponsorship request (if using backup testing model) initiated at contract award

### 4.3 Timeline Flexibility

Target dates are based on current project assumptions and client availability. Timeline adjustments may be required due to:

(a) Changes in project scope
(b) Delays in client-provided inputs, approvals, or access
(c) Game Warden onboarding or Iron Bank submission delays (third-party dependencies)
(d) Technical issues discovered during development
(e) Force majeure events

Any timeline modifications will be documented through the change management process outlined in Section 8.

---

## 5. INVESTMENT AND PAYMENT TERMS

### 5.1 Project Investment

**Tool Development (One-Time, All 3 Milestones):**

| Milestone | Development Cost Range |
|---|---|
| MS1: Black MVP | $20,000 - $31,000 |
| MS2: Yellow (Secret) | $23,000 - $40,000 |
| MS3: Red (TS/SCI) | $30,000 - $62,000 |
| **Total Tool Development** | **$73,000 - $133,000** |

**Veteran Vectors Services:**

| Item | Amount |
|---|---|
| **VV Development Fee** | **$60,000** (flat, 6-month engagement) |
| **VV Monthly Retainer** | Client selects Option A or Option B (see Section 5.6) |

### 5.2 Payment Schedule

**VV Development Fee ($60,000) — Milestone-Based:**

| Milestone | Trigger | VV Fee Payment |
|---|---|---|
| Contract Award | Signed | 30% = **$18,000** |
| MS1: Black MVP Accepted | March event UAT | 25% = **$15,000** |
| MS2: Yellow Operational | SIPRNet deployment | 20% = **$12,000** |
| MS3: Red Operational | JWICS acceptance | 25% = **$15,000** |

**Tool Development — Milestone-Based:**

| Milestone | Trigger | Tool Dev Payment |
|---|---|---|
| Contract Award | Signed | 20% of tool development estimate |
| MS1: Black MVP Accepted | March event UAT | 30% of tool development estimate |
| MS2: Yellow Operational | SIPRNet deployment | 30% of tool development estimate |
| MS3: Red Operational | JWICS acceptance | 20% of tool development estimate |

Invoices will be issued upon completion and acceptance of each milestone. Payment terms are **Net 30 days** from invoice date.

### 5.3 Additional Costs and Third-Party Services

The project investment includes Veteran Vectors' professional services only. The following costs are the responsibility of the Client and are not included:

- **Game Warden platform fees** ($3,000 - $15,000/month depending on tier)
- **AWS GovCloud / Secret / Top Secret Region compute costs**
- **Third-party software subscriptions** (if any)
- **Compliance assessment fees** (if using external assessors)

**Estimated Monthly Infrastructure Costs:**

| Tier | Monthly Cost |
|---|---|
| Black (Unclassified) | $130 - $270/mo |
| Yellow (Secret) | $3,500 - $9,500/mo |
| Red (TS/SCI) | $10,000 - $19,000/mo |

### 5.4 Out-of-Scope Work and Additional Services

Any work that falls outside the defined scope in Section 2 will be considered out-of-scope and will be billed separately according to the following terms:

- **Standard hourly rate:** $150 per hour
- **Premium rate (urgent or after-hours):** $225 per hour
- **Minimum billing increment:** 0.5 hours

Out-of-scope work requires written authorization before commencement. See Section 8 for detailed change management procedures.

### 5.5 Late Payment Terms

**Late Payment Interest:** If any payment due under this Agreement is not received within 30 days of its due date, Veteran Vectors shall be entitled to charge interest on the outstanding amount at the rate of 1.5% per month (18% annually).

**Suspension of Services:** If any payment remains unpaid for more than 45 days after its due date, Veteran Vectors reserves the right to suspend all services until payment is made in full.

**Retention of Intellectual Property:** Veteran Vectors shall retain all intellectual property rights in deliverables until full payment has been received.

### 5.6 Monthly Retainer Options — Starting Month 3

Client selects one of the following retainer structures. Retainer begins Month 3 when classified infrastructure is operational.

---

#### OPTION A: Percentage of Monthly Infrastructure (15%)

**Calculation:** 15% × monthly infrastructure costs

| Deployment State | Monthly Infra (Typical) | VV Retainer (15%) |
|---|---|---|
| Black only | $200/mo | $30/mo |
| Black + Yellow | $5,000 - $9,000/mo | $750 - $1,350/mo |
| All three tiers | $14,000 - $28,000/mo | $2,100 - $4,200/mo |

**Year 1 estimate (Months 3-12):** ~$17,000 - $37,000

**Best for:** Clients who want all-inclusive support that scales naturally with deployment footprint.

---

#### OPTION B: Hourly with Monthly Minimum

**Calculation:** $150/hour with 8-hour monthly minimum

| Item | Amount |
|---|---|
| Hourly rate | $150/hr |
| Monthly minimum | 8 hours = **$1,200/mo** |
| Hours above minimum | Billed at $150/hr |

**Year 1 estimate (Months 3-12):** $12,000 minimum (more if additional hours used)

**Best for:** Clients who want a predictable baseline and prefer to pay for actual hours used.

---

#### What Both Options Cover

**Container Lifecycle Management:**
- Monitor upstream CVEs (n8n, PostgreSQL, NGINX, Node.js, base images)
- Rebuild container images with patches, test on unclassified, deliver for deployment
- Critical CVE patches: same-week rebuild
- Minor patches: monthly batch
- Support Game Warden pipeline promotion for classified tiers

**Operational Support:**
- Incident triage and resolution (priority SLA)
- Workflow modifications (n8n JSON changes)
- Database maintenance (backup verification, index tuning)
- Infrastructure monitoring review

**Advisory & Planning:**
- Enhancement scoping for future features
- Quarterly architecture reviews
- Compliance posture updates as CMMC/NIST requirements evolve
- Scaling support for larger user populations

---

**Client Selection (check one):**

☐ **Option A:** 15% of monthly infrastructure costs

☐ **Option B:** $150/hour with 8-hour monthly minimum ($1,200/mo)

---

## 6. CLIENT RESPONSIBILITIES

Successful project completion requires active Client participation and timely fulfillment of the following responsibilities:

### 6.1 Access and Credentials

- Provide timely access to AWS GovCloud account (Black tier)
- Obtain and provide access to Game Warden contract (Yellow/Red tiers)
- Provide classified email relay configuration for SIPRNet and JWICS
- Ensure proper permission levels for required integrations
- Maintain valid subscriptions for all third-party services

### 6.2 Project Governance

- Designate a primary point of contact with decision-making authority
- Attend scheduled meetings and review sessions
- Provide feedback and approvals within 5 business days
- Communicate any changes in requirements or priorities promptly

### 6.3 Information and Materials

- Provide access to existing Power Automate flows, Excel data, and Power BI dashboards
- Supply accurate and complete data for testing and implementation
- Share relevant business process documentation and workflows

### 6.4 Testing and Validation

- Conduct user acceptance testing at March event (~15 users)
- Provide cleared personnel to execute VV-provided test scripts on SIPRNet and JWICS
- Provide clear, documented feedback on functionality and performance
- Coordinate classified testing windows with VV for real-time support

### 6.5 Classified Access (If Using Backup Testing Model)

- Initiate clearance sponsorship request for VV operator at contract award
- Process security office paperwork for SCIF access
- Provide access to classified terminals for VV operator testing

### 6.6 Impact of Client Delays

Delays caused by Client's inability to meet the above responsibilities may result in project timeline extensions and potential additional costs. Veteran Vectors will notify Client in writing within 48 hours of any identified delay that impacts the project schedule.

---

## 7. ACCEPTANCE CRITERIA

### 7.1 Deliverable Acceptance Process

Each deliverable specified in Section 3 will follow this formal acceptance process:

**Step 1: Submission** - Veteran Vectors submits the completed deliverable with supporting documentation.

**Step 2: Review Period** - Client has **10 business days** to review and test the deliverable.

**Step 3: Response** - Client provides either: (a) written acceptance, or (b) documented objections with specific issues identified.

**Step 4: Remediation (if needed)** - Veteran Vectors addresses documented issues within 5-10 business days.

**Step 5: Re-submission** - Process repeats until acceptance is achieved.

### 7.2 Deemed Acceptance

If Client fails to respond within the 10 business day review period, the deliverable shall be deemed accepted. This provision does not apply to critical system failures or material non-conformance that was not reasonably discoverable within the review period.

### 7.3 Milestone-Specific Acceptance Criteria

**MS1: Black MVP**
- All 5 workflows execute end-to-end with sample data
- March event UAT completed with ~15 users
- No critical or high-severity bugs open
- Operator documentation reviewed and approved

**MS2: Yellow Ops**
- System deploys successfully to Game Warden staging
- All 5 workflows execute on SIPRNet with test data
- SSP and POA&M accepted by Client security team
- No external API calls detected (air-gap validation)

**MS3: Red Ops**
- System deploys successfully to AWS Top Secret Region
- All 5 workflows execute on JWICS with test data
- TS-specific compliance documentation accepted
- Transition plan reviewed and approved

### 7.4 Post-Delivery Support Period

Veteran Vectors will provide **60 days of post-delivery support** following MS3 completion. This support includes:

- Bug fixes for issues directly related to the delivered solution
- Clarification on documentation and functionality
- Minor adjustments within the original scope

Support does not include: new feature development, integration with additional systems, changes to original requirements, or issues caused by Client modifications to the solution.

---

## 8. CHANGE MANAGEMENT AND SCOPE CONTROL

### 8.1 What Constitutes a Change

A change request is required for any work that:

- Adds new deliverables not specified in Section 3
- Modifies functionality or features of defined deliverables
- Integrates with systems or platforms not listed in assumptions
- Requires more than 2 hours of work beyond defined scope
- Changes project timeline by more than 1 week
- Involves technologies or approaches different from the agreed solution

### 8.2 Formal Change Request Process

**Initiation:** Either party may initiate a change request by submitting a written description via email.

**Impact Assessment:** Veteran Vectors will assess the request and provide within 3 business days:
- Detailed description of work required
- Estimated effort and cost
- Impact on project timeline
- Impact on other deliverables or dependencies
- Recommendation (approve, modify, or defer)

**Client Decision:** Client has 5 business days to approve, request modifications, or decline the change.

**Documentation:** Approved changes are documented in a formal Change Order including updated scope, timeline, and pricing. Both parties sign the Change Order.

**Implementation:** No work on approved changes begins until the Change Order is fully executed.

### 8.3 Change Order Pricing Structure

| Change Impact | Approval Level | Pricing | Timeline |
|---|---|---|---|
| Minor (<5% budget) | Project Manager | T&M at $150/hr | 1-2 days |
| Moderate (5-15% budget) | Account Manager | T&M at $187.50/hr or fixed bid | 3-5 days |
| Major (>15% budget) | Executive Sponsor | T&M at $225/hr or fixed bid | 5-10 days |

### 8.4 Scope Protection Mechanisms

**Proactive Communication:** Veteran Vectors will notify Client immediately when any request appears to fall outside the defined scope.

**No Verbal Modifications:** All scope changes must be documented in writing.

**Monthly Scope Review:** Both parties will conduct monthly scope review meetings to ensure alignment.

---

## 9. INTELLECTUAL PROPERTY RIGHTS

### 9.1 Background Intellectual Property

Veteran Vectors retains full ownership of all pre-existing intellectual property including:

- Proprietary methodologies, frameworks, and processes
- Software tools, templates, and code libraries developed prior to this engagement
- General automation patterns and best practices

### 9.2 Newly Created Work Product

Upon receipt of full payment, Client shall own all right, title, and interest in the following work product created specifically for Client under this Agreement:

- Custom n8n workflows and configurations
- Client-specific Helm charts and deployment configurations
- Custom-written code created solely for Client's use
- PostgreSQL schema and migration scripts
- Project documentation specific to Client's implementation

**Assignment Language:** Veteran Vectors hereby assigns to Client all right, title, and interest, including all intellectual property rights, in the above work product. This assignment is effective upon Client's payment in full of all amounts due under this Agreement.

### 9.3 Third-Party Components

The deliverables incorporate third-party software including:

| Component | License | Notes |
|---|---|---|
| n8n | Sustainable Use License | Open-source, self-hosted use permitted |
| PostgreSQL | PostgreSQL License | Permissive, similar to MIT |
| NGINX | BSD 2-Clause | Permissive |
| Metabase (if used) | AGPL v3 | Open-source, self-hosted use permitted |

Client acknowledges that: (a) these components are licensed, not owned, and remain subject to their respective license terms; (b) Client must comply with license terms; (c) Veteran Vectors makes no warranties regarding third-party components beyond those provided by the vendors.

**Note on n8n License:** n8n uses the Sustainable Use License which permits self-hosting and modification. If Client intends to offer the system as a managed service to third parties, legal review of the license is recommended.

### 9.4 License to Background IP

To the extent that Background IP is incorporated into deliverables, Veteran Vectors grants Client a perpetual, irrevocable, worldwide, royalty-free, non-exclusive license to use such Background IP solely as embedded in the deliverables and solely for Client's internal business operations and downstream government sale.

### 9.5 Government Data Rights

The IP rights structure supports downstream government sale:

- **Custom code:** Client receives unlimited rights, enabling flow-down per DFARS 252.227-7014
- **Open-source components:** Licenses documented in SBOM deliverable
- **IP Rights Summary:** Delivered at MS1 for Client's contracting use

---

## 10. CONFIDENTIALITY

### 10.1 Definition of Confidential Information

"Confidential Information" means all non-public information disclosed by one party to the other, including:

- Business plans, strategies, and financial information
- Customer data, user information, and business processes
- Technical data, trade secrets, and know-how
- Product roadmaps and proprietary methodologies
- Terms and pricing of this Agreement
- Classified information and CUI (Controlled Unclassified Information)

### 10.2 Obligations

Receiving Party shall: (a) protect Confidential Information with the same degree of care it uses to protect its own confidential information (but no less than reasonable care); (b) not disclose Confidential Information to third parties without prior written consent; (c) use Confidential Information only for purposes of performing this Agreement; (d) limit access to employees, contractors, and advisors who need to know and who are bound by confidentiality obligations.

### 10.3 Classified Information Handling

All classified information handling shall comply with applicable security classification guides, ICD 503, and Client's security policies. Veteran Vectors personnel accessing classified information must hold appropriate clearances and access must be processed through Client's security office.

### 10.4 Term

These confidentiality obligations shall continue for **five (5) years** following termination of this Agreement, or indefinitely for classified information as required by applicable security regulations.

---

## 11. DATA PROTECTION AND COMPLIANCE

### 11.1 Data Processing Roles

For purposes of applicable data protection laws: (a) Client is the data controller for all data provided to Veteran Vectors; (b) Veteran Vectors acts as a data processor, processing data solely under Client's documented instructions.

### 11.2 Compliance Frameworks

Both parties shall comply with applicable requirements including:

- **CMMC Level 2** — Access control, audit logging, encryption, input sanitization
- **NIST 800-171** — CUI handling, separation of duties, automated audit trail
- **NIST 800-53** — Security controls (via Game Warden inheritance)
- **DISA STIGs** — Applied automatically via Game Warden pipeline

### 11.3 Data Security Obligations

Veteran Vectors shall implement and maintain appropriate technical and organizational measures including:

- Encryption of data in transit (TLS 1.2+) and at rest
- Access controls limiting data access to authorized personnel
- Secure disposal of data upon project completion

### 11.4 Data Breach Notification

In the event of any unauthorized access to Client data, Veteran Vectors shall notify Client within **48 hours** of discovery and shall cooperate in investigating and remediating the breach.

---

## 12. WARRANTIES AND LIMITATIONS OF LIABILITY

### 12.1 Veteran Vectors' Warranties

Veteran Vectors warrants that:

- Services will be performed in a professional and workmanlike manner consistent with industry standards
- Deliverables will substantially conform to documented specifications
- It has the right and authority to enter into and perform this Agreement
- Work product will not infringe third-party intellectual property rights (subject to limitations in Section 13)

### 12.2 Warranty Period and Remedies

For a period of **90 days** following acceptance of each deliverable, if Client notifies Veteran Vectors in writing of any material non-conformance, Veteran Vectors shall use commercially reasonable efforts to correct such non-conformance at no additional charge.

### 12.3 Disclaimer of Warranties

EXCEPT AS EXPRESSLY SET FORTH IN SECTION 12.1, VETERAN VECTORS MAKES NO WARRANTIES, EXPRESS OR IMPLIED, INCLUDING ANY IMPLIED WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, OR NON-INFRINGEMENT.

### 12.4 Limitation of Liability

EXCEPT FOR BREACHES OF CONFIDENTIALITY, INDEMNIFICATION OBLIGATIONS, OR INTELLECTUAL PROPERTY INFRINGEMENT, VETERAN VECTORS' TOTAL AGGREGATE LIABILITY SHALL NOT EXCEED THE GREATER OF: (A) THE TOTAL FEES PAID OR PAYABLE BY CLIENT IN THE TWELVE (12) MONTHS PRECEDING THE CLAIM, OR (B) $500,000.

IN NO EVENT SHALL EITHER PARTY BE LIABLE FOR ANY INDIRECT, INCIDENTAL, SPECIAL, CONSEQUENTIAL, OR PUNITIVE DAMAGES.

### 12.5 Third-Party Platform Disclaimers

Veteran Vectors is not responsible for: (a) changes to third-party platforms (Game Warden, AWS, n8n) that affect deliverables; (b) third-party service outages; (c) third-party platform pricing changes; (d) deprecation of APIs or features.

---

## 13. INDEMNIFICATION

### 13.1 Veteran Vectors' Indemnification

Veteran Vectors shall defend, indemnify, and hold harmless Client from third-party claims arising from:

- Veteran Vectors' gross negligence or willful misconduct
- Veteran Vectors' breach of confidentiality obligations
- Claims that custom-developed deliverables infringe third-party IP rights

### 13.2 Client's Indemnification

Client shall defend, indemnify, and hold harmless Veteran Vectors from third-party claims arising from:

- Client's use of deliverables outside documented scope
- Client's modification of deliverables
- Claims that Client-provided materials infringe third-party rights
- Client's breach of applicable laws or regulations

### 13.3 IP Indemnification Limitations

Veteran Vectors' IP indemnification does not apply to claims arising from:

- Modifications made by Client
- Combination with non-approved systems
- Third-party platforms, APIs, or open-source components
- Compliance with Client's specific instructions

---

## 14. TERM AND TERMINATION

### 14.1 Term

This Agreement commences on the Project Start Date and continues until: (a) all deliverables are completed and accepted, and (b) the 60-day post-delivery support period has concluded, unless earlier terminated.

### 14.2 Termination for Convenience

Either party may terminate this Agreement for convenience by providing **30 days' written notice**. Upon such termination:

- Client shall pay for all work completed through the termination date
- Veteran Vectors shall deliver all work product completed to that point
- IP rights in completed deliverables transfer upon full payment for those deliverables

### 14.3 Termination for Cause

Either party may terminate immediately upon written notice if the other party:

- Commits a material breach and fails to cure within 30 days
- Becomes insolvent or files for bankruptcy
- Engages in fraud, gross negligence, or willful misconduct

### 14.4 Survival

The following provisions survive termination: Sections 5 (Payment), 9 (IP), 10 (Confidentiality), 12 (Warranties), 13 (Indemnification), and 15.11 (Governing Law).

---

## 15. GENERAL PROVISIONS

### 15.1 Independent Contractor

Veteran Vectors is an independent contractor, not an employee, partner, or joint venturer of Client.

### 15.2 Non-Solicitation

During the term and for 12 months thereafter, neither party shall directly solicit for employment any employee or contractor of the other party involved in the project without prior written consent.

### 15.3 Assignment

Neither party may assign this Agreement without prior written consent, except to a successor in connection with a merger or acquisition.

### 15.4 Entire Agreement

This Agreement constitutes the entire agreement between the parties and supersedes all prior discussions and agreements.

### 15.5 Severability

If any provision is found invalid, the remaining provisions remain in full force.

### 15.6 Waiver

No waiver of any provision shall be effective unless in writing.

### 15.7 Notices

All notices shall be in writing and delivered to the addresses on the cover page.

### 15.8 Electronic Signatures

Electronic signatures and PDF copies shall be as valid as original signatures.

### 15.9 Dispute Resolution

The parties agree to first attempt good faith negotiations. If negotiations fail within 30 days, either party may pursue formal legal remedies.

### 15.10 Legal Fees

The prevailing party in any action shall be entitled to recover reasonable attorneys' fees.

### 15.11 Governing Law and Jurisdiction

This Agreement shall be governed by the laws of the **State of Wyoming**. Each party submits to the exclusive jurisdiction of state and federal courts in Laramie County, Wyoming.

---

## 16. AUTHORIZATION AND SIGNATURES

By signing below, the authorized representatives acknowledge they have read, understood, and agree to be bound by all terms and conditions of this Statement of Work.

---

**CLIENT:**

**Legal Name:** BVG & CO CONSULTING LLC

**Authorized Signatory:**

Name: ________________________________

Title: ________________________________

Signature: ________________________________

Date: ________________________________

---

**VETERAN VECTORS LLC:**

**Legal Name:** VETERAN VECTORS LLC

**Authorized Signatory:**

Name: Anthony Pinto

Title: Founder

Signature: ________________________________

Date: ________________________________

---

*This Statement of Work becomes effective on the date of the last signature above.*

---

## APPENDIX A: THIRD-PARTY COMPONENT LICENSES

| Component | Version | License | Origin | Notes |
|---|---|---|---|---|
| n8n | 1.x | Sustainable Use License | n8n GmbH (Germany) | Self-hosted use permitted |
| PostgreSQL | 16.x | PostgreSQL License | PostgreSQL Global Dev Group | In Iron Bank |
| NGINX | 1.25.x | BSD 2-Clause | F5/NGINX Inc | In Iron Bank |
| Node.js | 18 LTS | MIT | OpenJS Foundation | Runtime for n8n |
| Metabase (optional) | Latest | AGPL v3 | Metabase Inc | BI fallback if Power BI unavailable |

---

## APPENDIX B: ESTIMATED YEAR 1 INVESTMENT SUMMARY

| Category | Low Estimate | High Estimate |
|---|---|---|
| Tool Development (all milestones) | $73,000 | $133,000 |
| Infrastructure (Year 1) | $116,560 | $250,240 |
| VV Development Fee | $60,000 | $60,000 |
| VV Retainer (Option A, 10 months) | $17,000 | $37,000 |
| VV Retainer (Option B, 10 months) | $12,000 | $12,000+ |
| **Total Year 1 (Option A)** | **$266,560** | **$480,240** |
| **Total Year 1 (Option B)** | **$261,560** | **$455,240+** |

**Note:** Infrastructure costs are billed directly by AWS and Second Front Systems (Game Warden) to Client.
