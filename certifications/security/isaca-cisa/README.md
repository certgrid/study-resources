# ISACA CISA - Study Cheatsheet

The ISACA Certified Information Systems Auditor (CISA) exam validates expertise in auditing, controlling, and securing an organization's information systems across the full audit lifecycle - planning, governance, system acquisition and development, operations and resilience, and asset protection. It is aimed at IS auditors, audit managers, IT consultants, compliance and security professionals who assess and assure technology controls. The 150-question exam runs 240 minutes, uses a scaled passing score of 450 out of 200-800, and weights five practice domains.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | ISACA CISA |
| Credential | ISACA CISA |
| Level | Intermediate |
| Practice mock length | ~100 questions |
| Duration | ~240 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Information Systems Auditing Process | ~20% |
| 2 | Governance and Management of IT | ~20% |
| 3 | Acquisition, Development and Implementation | ~18% |
| 4 | Operations and Business Resilience | ~22% |
| 5 | Protection of Information Assets | ~20% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Information Systems Auditing Process

- Risk-based audit planning directs audit effort toward areas of highest inherent and residual risk; it is the primary basis for scoping and prioritizing engagements rather than auditing everything equally.
- A control objective states the desired risk-mitigation outcome (what you want to achieve); a control is the specific mechanism, technology, or procedure implemented to achieve that objective.
- Auditor independence and objectivity are foundational; an auditor must not audit an area where they have a financial interest, prior operational role, or other conflict of interest that could bias conclusions.
- A compensating control is an alternative safeguard deployed when the preferred control is not feasible (e.g., due to cost or staffing) yet still reduces risk to an acceptable level - common where segregation of duties cannot be fully achieved.
- Preventive controls stop incidents before they occur (e.g., access restrictions); detective controls identify incidents during or after they occur (e.g., logs, reconciliations); corrective controls restore normal operation after an incident.
- Audit evidence must be sufficient, reliable, relevant, and useful; evidence obtained directly by the auditor from independent, objective sources is more reliable than evidence supplied by the auditee.

### Domain 2 - Governance and Management of IT

- The primary goal of IT governance is to ensure IT aligns with and advances business objectives while IT-related risks and resources are managed appropriately - it is a board and senior-management responsibility.
- Segregation of duties divides critical tasks (initiate, approve, execute, record) so no single individual can both commit and conceal fraud or error.
- An IT steering committee, composed of senior business and IT leaders, provides strategic oversight and aligns IT investments and priorities with business strategy.
- Policies, standards, defined roles/responsibilities, and oversight form the control framework; policies and procedures serve as the criteria against which auditors evaluate actual practice.
- Key performance indicators (KPIs) measure how well objectives are met; key risk indicators (KRIs) provide early warning of rising risk exposure.
- Maturity/capability models such as CMMI rate process maturity on a graduated scale (typically Level 1 initial/ad-hoc through Level 5 optimizing) to guide continuous improvement.

### Domain 3 - Acquisition, Development and Implementation

- Building and verifying controls early in the SDLC is far cheaper and more effective than retrofitting them; the cost to fix a defect rises dramatically the later it is found.
- User acceptance testing (UAT) is the final test phase, performed by business users to confirm the system meets documented business requirements and is fit for use before production go-live.
- A post-implementation review evaluates, after the system has run long enough to generate meaningful data, whether the project met its objectives and captures lessons learned.
- Authorized, tested changes are protected by formal change management with approvals plus separation of development, test, and production environments.
- For COTS/third-party software the auditor's key concern is due diligence: vendor financial stability, security, support and maintenance arrangements, escrow, and contractual SLAs.
- Referential integrity is enforced with foreign key constraints (e.g., FOREIGN KEY (cust_id) REFERENCES customers(id)) so child records cannot reference nonexistent parents.

### Domain 4 - Operations and Business Resilience

- RTO (recovery time objective) is the maximum acceptable time to restore a service after disruption; RPO (recovery point objective) is the maximum acceptable data loss measured as a point in time.
- Backups must be periodically restore-tested; an untested backup may fail when needed due to corruption, incomplete sets, or unreadable formats.
- A Business Impact Analysis (BIA) identifies critical business processes, quantifies impact over time, and establishes the RTO and RPO requirements that drive recovery strategy.
- A hot site is a fully equipped, continuously operational alternate facility with real-time or near-real-time data replication, enabling rapid failover; a warm site has hardware but stale data; a cold site is bare space requiring full build-out.
- DR test types in increasing rigor: checklist, tabletop/walkthrough, simulation, parallel (run recovery alongside production), and full interruption (cut over to recovery).
- Unauthorized changes are detected by reviewing change/configuration logs and comparing them against approved change records.

### Domain 5 - Protection of Information Assets

- Least privilege grants each user, process, or service only the minimum permissions needed; need-to-know further restricts access to information required for the task - together they minimize exposure.
- Logging and monitoring are detective controls providing an audit trail for accountability, anomaly detection, and investigation support.
- Confidentiality of data is protected by encryption at rest (renders stored data unreadable without the key) and in transit (TLS), combined with least-privilege access controls.
- Information classification and labeling (e.g., public, internal, confidential, restricted) ensure protection is commensurate with each asset's sensitivity and value.
- Data loss prevention (DLP) relies on classifying and labeling sensitive data plus content inspection and policy enforcement on egress channels.
- File integrity monitoring (FIM) detects unauthorized changes to critical files and system configurations.

## Study tips

- Always answer from the perspective of an independent IS auditor: the BEST first step is usually to understand the environment and assess risk (planning) before testing, and to report findings rather than fix them yourself.
- When two answers seem correct, choose the most preventive, most fundamental, or root-cause option; ISACA rewards addressing the cause over the symptom and favors governance/process answers over purely technical ones.
- Memorize the distinctions between paired terms - control objective vs control, preventive vs detective vs corrective, RTO vs RPO, hot/warm/cold sites, KPI vs KRI - they appear repeatedly.
- There is no penalty for wrong answers, so answer every question; budget roughly 90 seconds per item across 150 questions and 240 minutes, flagging tough ones to revisit.
- Read the question stem for qualifiers like BEST, FIRST, MOST, and GREATEST - these change which of several plausible answers is correct, and watch for EXCEPT/NOT framing.

---

Want the full breakdown? See the complete **[ISACA CISA study guide](https://certgrid.app/study-guide/isaca-cisa)** and **[free practice questions](https://certgrid.app/practice/isaca-cisa)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

