# CompTIA Security+ SY0-701 - Study Cheatsheet

CompTIA Security+ SY0-701 validates the baseline knowledge needed to perform core security functions and pursue an IT security career. It is vendor-neutral and covers threats, cryptography, identity and access management, secure architecture, security operations, and governance. It is aimed at junior security analysts, systems administrators, and anyone establishing foundational cybersecurity competency.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | CompTIA Security+ SY0-701 |
| Credential | CompTIA Security+ SY0-701 |
| Level | Intermediate |
| Practice mock length | ~90 questions |
| Duration | ~90 minutes |
| Passing score | 750 out of 900 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | General Security Concepts | ~12% |
| 2 | Threats, Vulnerabilities, and Mitigations | ~22% |
| 3 | Security Architecture | ~18% |
| 4 | Security Operations | ~28% |
| 5 | Security Program Management and Oversight | ~20% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - General Security Concepts

- The CIA triad is Confidentiality (only authorized parties access data), Integrity (data is not altered without detection), and Availability (data and systems are accessible when needed); non-repudiation is added to prove a party cannot deny an action.
- The AAA framework separates Authentication (proving identity), Authorization (what an identity may access), and Accounting (logging what was done); RADIUS and TACACS+ implement AAA, with TACACS+ encrypting the full payload and separating the three functions.
- Security control categories are Technical, Managerial, Operational, and Physical; control types are Preventive, Detective, Corrective, Deterrent, Compensating, and Directive (e.g., a guard is deterrent/preventive, a CCTV camera is detective/deterrent).
- Least privilege grants users only the minimum access needed for their role; separation of duties splits sensitive tasks among people to prevent fraud; defense in depth layers multiple controls so failure of one does not expose the system.
- Zero Trust assumes no implicit trust based on network location and verifies every request; its planes are the Control Plane (Policy Engine, Policy Administrator, Policy Decision Point) and the Data Plane (Policy Enforcement Point and the subject/system).
- Access control models: MAC uses labels/clearances set by a central authority (highest security, least flexible), DAC lets owners set permissions, RBAC assigns access by job role, ABAC evaluates attributes/policies, and rule-based applies admin-defined rules.

### Domain 2 - Threats, Vulnerabilities, and Mitigations

- Threat actor types differ by motivation and resources: nation-states/APTs have the most resources and persistence, organized crime seeks financial gain, hacktivists pursue ideology, insiders abuse legitimate access, and unskilled attackers (script kiddies) use existing tools.
- Malware types: a virus needs a host file and user action, a worm self-replicates across networks without user interaction, a Trojan hides in legitimate software, ransomware encrypts data for payment, and a rootkit intercepts/modifies system calls to hide at the kernel level.
- Social engineering: phishing (email), spear phishing (targeted), whaling (executives), vishing (voice), smishing (SMS), pretexting (fabricated scenario), and Business Email Compromise (BEC) impersonating an executive for fraudulent wire transfers.
- An on-path (man-in-the-middle) attack intercepts and can modify traffic between two parties; a replay attack reuses captured valid data, mitigated with timestamps, nonces, and session tokens.
- Password attacks: credential stuffing reuses breached username/password pairs across sites, password spraying tries a few common passwords against many accounts, and brute force tries all combinations; MFA is the strongest mitigation.
- SQL injection is mitigated with parameterized queries (prepared statements) and input validation; cross-site scripting (XSS) is mitigated with input validation and output encoding; CSRF is mitigated with anti-CSRF tokens.

### Domain 3 - Security Architecture

- An IDS passively monitors and alerts on suspicious traffic, while an IPS sits inline and can actively block it; detection is either signature-based (known patterns) or anomaly/behavior-based (deviations from a baseline).
- A screened subnet (DMZ) hosts internet-facing servers in an isolated zone separate from the internal network; a bastion host/jump server is a hardened, controlled entry point for managing systems in a secured zone.
- Network segmentation and microsegmentation divide the network into isolated zones to limit lateral movement and reduce the blast radius of a breach; VLANs and firewall rules enforce the boundaries.
- Cloud service models: IaaS gives the customer the most control (manages OS up), PaaS provides a managed platform for apps, and SaaS gives the least control; the shared responsibility model defines who secures what.
- Encryption in transit uses TLS (and IPsec for VPNs) to protect data moving across networks; encryption at rest uses full-disk encryption, database/file encryption, or TDE; data in use can be protected with secure enclaves.
- High availability is achieved with redundancy: failover clusters, load balancers across multiple instances, RAID for disks, redundant power (UPS, generators), and geographic site redundancy.

### Domain 4 - Security Operations

- A SIEM aggregates and normalizes logs from many sources and applies correlation rules to detect patterns indicating an incident; SOAR adds automated playbooks to orchestrate and speed up response, reducing mean time to respond (MTTR).
- The NIST incident response lifecycle is Preparation; Detection and Analysis; Containment, Eradication, and Recovery; and Post-incident Activity (lessons learned).
- The first containment action for a compromised host is to isolate it from the network while preserving evidence; do not power off immediately if volatile data (memory) must be captured.
- The order of volatility for evidence collection is most-volatile-first: CPU registers/cache, then RAM, then network state/connections, then disk, then logs/archives, then backups.
- Chain of custody is a documented record of who handled evidence, when, and what actions were taken, establishing the evidence was not altered and making it admissible.
- MFA combines factors from different categories: something you know (password/PIN), something you have (token/smart card/phone), and something you are (biometric); two of the same category is not true MFA.

### Domain 5 - Security Program Management and Oversight

- Risk management responses are accept, avoid, transfer (e.g., cyber insurance or contractual shift to a vendor), and mitigate (apply controls); residual risk is what remains after controls are applied.
- Quantitative risk uses SLE = Asset Value x Exposure Factor, ARO = annual frequency, and ALE = SLE x ARO; qualitative risk uses ratings like low/medium/high on a risk matrix.
- A Business Impact Analysis (BIA) identifies critical business functions and the impact of their disruption, producing the RTO, RPO, MTD (maximum tolerable downtime), and MTBF/MTTR metrics that drive continuity planning.
- Governance documents form a hierarchy: policies state high-level objectives, standards define mandatory requirements, procedures give step-by-step instructions, and guidelines offer recommendations; an Acceptable Use Policy (AUP) governs use of company IT resources.
- Common frameworks/regulations: NIST CSF (Identify, Protect, Detect, Respond, Recover), ISO 27001, PCI DSS for cardholder data, HIPAA for health data, GDPR for EU personal data, and SOX for financial reporting.
- Third-party/vendor risk management uses due diligence, contracts, and assurance reports; a SOC 2 Type II report evaluates the operating effectiveness of controls over a period of time, unlike Type I (a point in time).

## Study tips

- Watch for qualifier words like BEST, MOST, FIRST, and PRIMARY; multiple answers may be technically valid, so pick the one that most directly addresses the scenario's specific goal.
- Performance-based questions (PBQs) appear first and carry the most weight; if one stalls you, flag it, finish the multiple-choice questions, and return so you do not run out of the 90 minutes.
- Memorize the incident response order (Preparation; Detection/Analysis; Containment, Eradication, Recovery; Lessons Learned) and the order of volatility, because process-sequence questions are common.
- Know the math cold: SLE = AV x EF and ALE = SLE x ARO, plus the differences between RTO, RPO, MTD, MTBF, and MTTR; these are quick points if you have the formulas memorized.
- Distinguish closely paired terms (IDS vs IPS, symmetric vs asymmetric, MAC vs DAC vs RBAC vs ABAC, vulnerability scan vs pen test, SOC 2 Type I vs Type II) since the exam tests these contrasts directly.

---

Want the full breakdown? See the complete **[CompTIA Security+ SY0-701 study guide](https://certgrid.app/study-guide/comptia-security-sy0-701)** and **[free practice questions](https://certgrid.app/practice/comptia-security-sy0-701)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

