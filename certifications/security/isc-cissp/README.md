# (ISC)² CISSP - Study Cheatsheet

The (ISC)² CISSP validates the broad knowledge and managerial judgment needed to design, engineer, and lead an enterprise security program across eight domains defined by the Common Body of Knowledge (CBK). It is aimed at experienced practitioners (the cert requires five years of cumulative paid work in two or more domains) such as security managers, architects, analysts, and CISOs. The exam is delivered as a Computerized Adaptive Test (CAT) and rewards the 'manager's-eye' answer (risk-based, big-picture) over the most technical one.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | (ISC)² CISSP |
| Credential | (ISC)² CISSP |
| Level | Intermediate |
| Practice mock length | ~100 questions |
| Duration | ~240 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Security and Risk Management | ~13% |
| 2 | Asset Security | ~9% |
| 3 | Security Architecture and Engineering | ~12% |
| 4 | Communication and Network Security | ~11% |
| 5 | Identity and Access Management | ~11% |
| 6 | Security Assessment and Testing | ~12% |
| 7 | Security Operations | ~18% |
| 8 | Software Development Security | ~15% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Security and Risk Management

- The CIA Triad is the foundation: Confidentiality (no unauthorized disclosure), Integrity (no unauthorized alteration), and Availability (accessible when needed); the inverse triad is Disclosure, Alteration, and Destruction (DAD).
- Risk = likelihood x impact. Quantitative formulas: SLE = Asset Value x Exposure Factor; ALE = SLE x ARO (Annualized Rate of Occurrence). A control is justified only when its annual cost is less than the reduction it produces in ALE.
- The four risk treatment options are mitigate (reduce), transfer (e.g., insurance or outsourcing), avoid (eliminate the risky activity entirely when impact far exceeds benefit), and accept. Residual risk is what remains after controls are applied.
- Document hierarchy: a Policy states high-level mandatory intent (approved by senior management), Standards define mandatory specifics, Procedures give step-by-step instructions, and Guidelines are optional recommendations.
- Risk appetite is the amount and type of risk leadership is willing to accept in pursuit of objectives; it is set by the board. Senior management 'tone at the top' and governance buy-in are prerequisites for any program.
- GDPR mandates breach notification to the supervisory authority within 72 hours of becoming aware. The controller determines purpose and means of processing; the processor acts only on the controller's instructions, governed by a Data Processing Agreement (DPA).

### Domain 2 - Asset Security

- Data classification (e.g., public, internal, confidential, restricted) applies protection proportional to sensitivity, driving access controls, encryption, labeling, retention, and disposal while avoiding over-protecting low-value data.
- A record inherits the highest classification of any single element it contains (aggregation can raise sensitivity).
- Key data roles: the data owner (a senior business role) classifies data and bears ultimate responsibility; the data custodian implements and maintains controls; the data steward handles quality; the user follows AUP.
- Under privacy law the data controller determines the purpose and means of processing; the data processor acts only on the controller's documented instructions.
- Need-to-know limits access to only the information required for a specific task, and operates in addition to (not instead of) a subject's clearance/privilege level.
- Data states require different controls: at rest (full-disk encryption, e.g., LUKS via cryptsetup), in transit (TLS between services), and in use (application/field-level encryption with keys in an HSM or KMS that DBAs cannot access).

### Domain 3 - Security Architecture and Engineering

- Defense-in-depth layers multiple diverse controls (perimeter, network, host, application, data) so that the failure of any single control does not lead to compromise.
- Symmetric cryptography uses one shared secret key and is fast (e.g., AES, often with AES-NI hardware acceleration); asymmetric uses a public/private key pair, solving the n(n-1)/2 key-distribution problem and enabling scalable key establishment.
- Hashing (a one-way function, e.g., SHA-256) provides integrity by detecting changes; it is not encryption and has no key. HMAC adds a key for authenticated integrity.
- Digital signatures provide integrity, authentication, and non-repudiation: the sender signs a hash with their private key and the recipient verifies with the sender's public key.
- A PKI issues, manages, and validates X.509 certificates that bind public keys to identities; the CA signs certs, the RA verifies requests, and revocation is published via CRLs or OCSP.
- Authenticated encryption modes (e.g., AES-GCM) provide confidentiality plus integrity simultaneously. ECB (Electronic Codebook) mode is insecure because identical plaintext blocks produce identical ciphertext, leaking patterns.

### Domain 4 - Communication and Network Security

- The OSI model has 7 layers (Physical, Data Link, Network, Transport, Session, Presentation, Application); the TCP/IP model has 4. Map protocols to layers (e.g., IP at Layer 3, TCP/UDP at Layer 4, TLS spans 5-6).
- A VPN creates an encrypted tunnel protecting confidentiality and integrity over untrusted networks. IPsec ESP (Encapsulating Security Payload) provides encryption (confidentiality) plus optional integrity/authentication; AH provides integrity/authentication only, no encryption.
- Network segmentation (VLANs, subnetting with ACLs, microsegmentation) limits lateral movement and contains breaches by isolating zones.
- Firewall types in increasing sophistication: packet filter (Layer 3/4 ACLs), stateful inspection (tracks connection state), and next-generation/application-layer (deep packet inspection, app awareness).
- An IDS passively monitors a copy of traffic and alerts on suspicious activity (often via a SPAN/mirror port); an IPS sits inline and can actively block or drop malicious traffic in real time.
- A DMZ hosts internet-facing services; sensitive back-end systems (e.g., databases) belong on an internal segment behind a second firewall, reachable only from the DMZ application tier on required ports.

### Domain 5 - Identity and Access Management

- The access control sequence is Identification (claiming an identity), Authentication (proving it), Authorization (granting access), and Accountability (logging/auditing actions, also called AAA with Auditing).
- MFA combines two or more factors from different categories: something you know (password/PIN), something you have (token/smartcard), and something you are (biometric); two passwords are not MFA.
- Access control models: DAC (owner sets permissions, e.g., file ACLs); MAC (system enforces labels/clearances non-discretionarily, used in classified environments); RBAC (permissions tied to roles/job functions, not individuals); ABAC (policy evaluates subject, resource, action, and environment attributes).
- MAC grants access only when a subject's clearance dominates an object's classification under a central policy that neither owners nor users can override.
- Least privilege grants the minimum access needed to perform a function; separation of duties splits sensitive tasks so no single person can complete a critical action alone (fraud prevention).
- SAML is the XML-based federation standard that exchanges authentication and authorization assertions between an Identity Provider (IdP) and a Service Provider (SP) for web SSO; the relying party must validate assertion signatures and audience/recipient restrictions.

### Domain 6 - Security Assessment and Testing

- A vulnerability assessment identifies and prioritizes weaknesses broadly; a penetration test goes further by attempting to exploit them to demonstrate real-world impact, always under written authorization and agreed rules of engagement.
- Penetration test knowledge levels: black-box (no internal knowledge), white-box (full knowledge/source), and gray-box (partial). Phases follow planning, reconnaissance, scanning, exploitation, and reporting.
- Audits performed by an independent third party provide objective oversight and reduce the chance of fraud or self-review bias; auditors should not assess their own work.
- SOC reports under SSAE 18: SOC 1 covers financial-reporting controls, SOC 2 covers security/availability/confidentiality (Type I is a point in time, Type II covers a period), and SOC 3 is a public summary.
- A false positive is an alert on a benign condition; a false negative is a missed detection of a real issue (the more dangerous failure because the threat goes unnoticed).
- Authenticated (credentialed) scans against an accurate asset inventory yield higher-fidelity results and reduce redundant low-value checks compared with unauthenticated scans.

### Domain 7 - Security Operations

- The incident response lifecycle (NIST SP 800-61) is Preparation, Detection & Analysis, Containment/Eradication & Recovery, and Post-Incident Activity (lessons learned).
- Disaster recovery metrics: RTO (Recovery Time Objective) is how fast you must restore; RPO (Recovery Point Objective) is the maximum tolerable data loss, which dictates backup/replication frequency; MTD is the maximum tolerable downtime.
- Recovery site types trade cost against speed: a hot site has fully replicated systems/data ready for near-immediate takeover (lowest RTO, highest cost), a warm site has hardware but needs data/config, and a cold site is just space and power.
- Backup strategy combines periodic full backups with frequent incrementals (only changed data since the last backup) or differentials (changed since the last full); test restores regularly, since untested backups are unproven.
- RAID provides availability and fault tolerance but is NOT a substitute for backups: it does not protect against deletion, corruption, ransomware, or site loss.
- The order of volatility for evidence collection is CPU registers/cache, then RAM, then network/process state, then disk, then archival media; collect the most volatile data first.

### Domain 8 - Software Development Security

- Input validation should use a positive/allow-list (reject anything not explicitly permitted) and be performed server-side; it prevents injection and many other attacks by rejecting malformed or malicious input.
- SQL injection is prevented by parameterized queries / prepared statements (which separate code from data), never by string concatenation; output encoding prevents cross-site scripting (XSS).
- Cross-Site Request Forgery (CSRF) is mitigated by per-request anti-CSRF tokens combined with the SameSite cookie attribute.
- Insecure Direct Object Reference (IDOR) / broken object-level authorization is fixed by enforcing server-side authorization checks that verify the caller actually owns or may access each requested object.
- A TOCTOU (time-of-check to time-of-use) race condition occurs when a resource's state changes between validation and use, allowing an attacker to substitute it; mitigate with atomic operations and locking.
- Shift-left / DevSecOps integrates security into design and requirements and runs SAST, DAST, and dependency/SCA scans as pipeline gates, because defects caught in design or coding cost far less to remediate than those found in production.

## Study tips

- Think like a risk manager, not a technician: when several answers are technically correct, pick the one that best addresses business risk, follows policy, and reflects management's perspective (the 'best' answer, not just a 'right' one).
- Always do the first thing first. Many questions ask what to do FIRST or NEXT - the answer is usually a process step like analyze/assess risk, get management approval, perform a BIA, or notify the right party, not jump straight to a technical fix.
- Memorize the quantitative risk formulas (SLE = AV x EF, ALE = SLE x ARO) and the access-control models (DAC/MAC/RBAC/ABAC) and security models (Bell-LaPadula vs Biba) cold - they appear repeatedly and are easy points.
- The exam is a Computerized Adaptive Test (CAT): you cannot go back to change answers, so commit to each question; the difficulty adjusts to your performance, and you can pass in as few as 100 questions.
- Watch for distractors that are plausible but address the wrong CIA element or the wrong control function (preventive vs detective vs corrective); read the full scenario, eliminate two wrong answers first, then choose between the remaining two.

---

Want the full breakdown? See the complete **[(ISC)² CISSP study guide](https://certgrid.app/study-guide/isc-cissp)** and **[free practice questions](https://certgrid.app/practice/isc-cissp)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

