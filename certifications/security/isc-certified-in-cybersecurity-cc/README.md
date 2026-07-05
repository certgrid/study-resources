# (ISC)² Certified in Cybersecurity (CC) - Study Cheatsheet

The (ISC)² Certified in Cybersecurity (CC) is an entry-level credential that validates foundational knowledge across security principles, business continuity and incident response, access control, network security, and security operations. It is aimed at newcomers, career changers, and IT professionals seeking to enter the cybersecurity field with no prior work experience required. The exam is 100 multiple-choice questions over 120 minutes, scored on a 1000-point scale with 700 to pass.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | (ISC)² Certified in Cybersecurity (CC) |
| Credential | (ISC)² Certified in Cybersecurity (CC) |
| Level | Intermediate |
| Practice mock length | ~100 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-06-23 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Security Principles | ~22% |
| 2 | Business Continuity, DR, and Incident Response | ~14% |
| 3 | Access Control Concepts | ~21% |
| 4 | Network Security | ~21% |
| 5 | Security Operations | ~22% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Security Principles

- The CIA triad is the core model: Confidentiality (no unauthorized disclosure), Integrity (no unauthorized or undetected alteration), and Availability (authorized users can access systems and data when needed).
- Multi-factor authentication (MFA) requires factors from at least two DIFFERENT categories: something you know (password/PIN), something you have (token/phone), and something you are (biometric). Two passwords are NOT MFA.
- A threat is a potential danger or actor; a vulnerability is a weakness; risk is the likelihood and impact of a threat exploiting a vulnerability. A threat actor is the entity that carries out the threat.
- Least privilege grants users and processes only the minimum access needed for their job, reducing the blast radius if an account is compromised.
- Defense in depth layers multiple, varied controls so no single failure leads to compromise.
- AAA stands for Authentication (proving identity), Authorization (granting permissions), and Accounting (logging actions for accountability).

### Domain 2 - Business Continuity, DR, and Incident Response

- Recovery Time Objective (RTO) is the maximum acceptable time to restore a service after a disruption; it drives how fast recovery solutions must be.
- Recovery Point Objective (RPO) is the maximum acceptable amount of data loss measured as a point in time; it drives backup and replication frequency (e.g., a 4-hour RPO requires backups at least every 4 hours).
- The NIST incident response lifecycle has four phases: Preparation; Detection and Analysis; Containment, Eradication, and Recovery; and Post-Incident Activity.
- Containment limits the scope and spread of an incident to prevent further damage; eradication removes the threat; recovery restores affected systems from known-good sources.
- A Business Continuity Plan (BCP) keeps the whole business operating during a disruption; a Disaster Recovery Plan (DRP) focuses on restoring IT systems and data after an incident.
- A Business Impact Analysis (BIA) identifies critical business functions and the impact/timeframes of disruption, and it is what informs RTO and RPO values.

### Domain 3 - Access Control Concepts

- Role-Based Access Control (RBAC) assigns permissions to roles tied to job functions; users inherit permissions by role membership, so permissions are managed once per role.
- Mandatory Access Control (MAC) enforces access via system-wide sensitivity labels and a central policy that users cannot override; it is used in government/military and highly classified environments.
- Discretionary Access Control (DAC) lets the resource owner grant access at their own discretion (e.g., file permissions set by the file's owner).
- Attribute-Based Access Control (ABAC) makes decisions based on attributes of the user, resource, action, and environment (e.g., department, time of day, location).
- Separation of duties (SoD) splits critical tasks among multiple people so no single person can commit and conceal fraud; it requires collusion to bypass.
- Need to know limits access to specific information to those who genuinely require it for their job, even if they hold sufficient clearance; it complements least privilege.

### Domain 4 - Network Security

- A firewall filters traffic by allowing or denying packets based on rules (source/destination IP, port, protocol); stateful firewalls track connection state, while stateless firewalls evaluate each packet independently.
- An IDS passively detects and alerts on suspicious activity; an IPS is deployed inline and can actively block malicious traffic.
- A VPN creates an encrypted tunnel over untrusted networks (e.g., public Wi-Fi), protecting confidentiality and integrity of data in transit using protocols like IPsec or TLS.
- A DMZ (screened subnet) hosts internet-facing servers isolated from the internal network by firewalls, so a compromise there does not directly expose internal systems.
- Network segmentation limits broadcast domains, contains traffic, and restricts lateral (east-west) movement by an attacker.
- A Denial-of-Service (DoS) attack targets availability by overwhelming a service; a DDoS uses many distributed sources, and a CDN can absorb/cache traffic to mitigate it.

### Domain 5 - Security Operations

- Symmetric encryption (e.g., AES, 3DES) uses one shared secret key for both encryption and decryption; it is fast but has a key-distribution challenge.
- Asymmetric encryption (e.g., RSA, ECC) uses a public/private key pair: encrypt with the recipient's public key, decrypt with their private key; sign with the private key, verify with the public key.
- Hashing (e.g., SHA-256) produces a fixed-length one-way digest used to verify integrity; any change to the input changes the hash, and it cannot be reversed.
- Data classification assigns labels (public, internal, confidential, restricted) based on sensitivity, driving proportional controls so confidential data gets stronger protection.
- Data states require different protection: at rest (encryption on storage), in transit (TLS/VPN), and in use (memory and access protections).
- Patch and vulnerability management remediates known vulnerabilities before attackers exploit them; patches should be tested in staging and deployed in maintenance windows with a rollback plan.

## Study tips

- Memorize the exact frameworks and their order: the CIA triad, AAA, the four (ISC)² Code of Ethics canons (in priority order), the four-phase NIST incident response lifecycle, and the risk-response options (Avoid, Mitigate, Transfer, Accept).
- Distinguish lookalike pairs cleanly: threat vs. vulnerability vs. risk, RTO vs. RPO, IDS vs. IPS, BCP vs. DRP, MAC vs. DAC vs. RBAC, and symmetric vs. asymmetric vs. hashing.
- Watch the wording on MFA questions: factors must come from DIFFERENT categories (know/have/are). Two passwords or two security questions are single-factor.
- When a question asks for the BEST or FIRST action, think in terms of priority: protect life and safety first, then contain before eradicate, and apply least privilege and need-to-know as the default answer.
- The exam is concept-focused, not vendor-specific. Pace yourself at roughly one minute per question, flag uncertain ones, and answer every question since there is no penalty for guessing.

---

Want the full breakdown? See the complete **[(ISC)² Certified in Cybersecurity (CC) study guide](https://certgrid.app/study-guide/isc-certified-in-cybersecurity-cc)** and **[free practice questions](https://certgrid.app/practice/isc-certified-in-cybersecurity-cc)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

