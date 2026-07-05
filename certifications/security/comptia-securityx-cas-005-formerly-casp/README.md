# CompTIA SecurityX (CAS-005, formerly CASP+) - Study Cheatsheet

CompTIA SecurityX (CAS-005, formerly CASP+) validates advanced practitioner-level skills for senior security engineers and architects who design, implement, and govern enterprise security across hybrid and cloud environments. The exam runs up to 165 minutes with a maximum of about 90 multiple-choice and performance-based questions, scored on a scale where 750 is passing. It covers four domains: Governance/Risk/Compliance, Security Architecture, Security Engineering, and Security Operations.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | CompTIA SecurityX (CAS-005, formerly CASP+) |
| Credential | CompTIA SecurityX (CAS-005, formerly CASP+) |
| Level | Intermediate |
| Practice mock length | ~90 questions |
| Duration | ~165 minutes |
| Passing score | 750 out of 1000 |
| Notes reviewed | 2026-06-23 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Governance, Risk, and Compliance | ~25% |
| 2 | Security Architecture | ~24% |
| 3 | Security Engineering | ~25% |
| 4 | Security Operations | ~26% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Governance, Risk, and Compliance

- Enterprise Risk Management (ERM) is an organization-wide process to identify, assess (likelihood x impact), prioritize, and treat risk using one of four responses: accept, avoid, transfer, or mitigate, aligned to the organization's stated risk appetite.
- Residual risk is the risk remaining after controls are applied; it can never reach zero, must be compared against risk appetite/tolerance, and any excess requires a formal risk-acceptance exception with executive sign-off.
- Quantitative risk analysis assigns dollar values using SLE = Asset Value x Exposure Factor, ALE = SLE x ARO; qualitative analysis uses subjective high/medium/low ratings when numeric data is unavailable.
- Control selection is justified by cost-benefit analysis: a safeguard is worthwhile only if its cost is less than the reduction in Annual Loss Expectancy (the ALE before minus the ALE after the control).
- A Business Impact Analysis (BIA) identifies critical processes, dependencies, and tolerable downtime/data-loss, producing the RTO (max acceptable downtime) and RPO (max acceptable data loss) that drive BC/DR priorities.
- GDPR applies to any organization processing EU residents' personal data regardless of location; it mandates lawful basis/consent, privacy by design, data-subject rights (access, erasure, portability), and 72-hour breach notification to the supervisory authority.

### Domain 2 - Security Architecture

- Zero Trust assumes no implicit trust: every access request is continuously verified against identity, device posture, and context, enforcing 'never trust, always verify' regardless of network location.
- Microsegmentation isolates workloads/zones to limit lateral movement and contain a breach, in contrast to flat networks where a single compromise spreads freely.
- Secure Access Service Edge (SASE) converges networking and security (SWG, CASB, ZTNA, FWaaS) delivered as a cloud-edge service, replacing backhauling traffic to a central data center.
- Zero Trust Network Access (ZTNA) replaces traditional VPNs by granting per-application access based on identity and posture, never exposing the broader network, and pairs with MFA and short-lived credentials.
- A Cloud Access Security Broker (CASB) sits between users and SaaS to enforce visibility, DLP, threat protection, and shadow-IT discovery for cloud application usage.
- Defense in depth layers independent controls (network, host, application, data) with least privilege and segmentation so no single failure exposes the whole system.

### Domain 3 - Security Engineering

- Symmetric encryption (AES) uses one shared key and is fast for bulk data; asymmetric encryption (RSA, ECC) uses a public/private key pair, is slower, and is used for key exchange and digital signatures.
- Perfect Forward Secrecy uses ephemeral key exchange (ECDHE/DHE) so compromise of a long-term private key cannot decrypt previously captured session traffic, because each session derives a unique ephemeral key.
- A Hardware Security Module (HSM) provides tamper-resistant generation, storage, and use of cryptographic keys (often FIPS 140-2/140-3 validated) so private keys never leave the device in plaintext.
- Hardening disables deprecated protocols and weak ciphers (SSL 3.0, TLS 1.0/1.1, RC4, export-grade suites) that enable attacks like POODLE and BEAST, applying secure baselines (CIS Benchmarks/DISA STIGs).
- Certificate pinning prevents man-in-the-middle attacks by ensuring only the expected/trusted certificate or public key is accepted, rejecting otherwise-valid certs from rogue CAs.
- A measured/secure boot uses a TPM as a root of trust to verify firmware and OS integrity at startup and store boot measurements; secure boot blocks unsigned bootloaders.

### Domain 4 - Security Operations

- A SIEM (Security Information and Event Management) aggregates and correlates logs/events from endpoints, network, and cloud to provide centralized detection, alerting, and investigation for the SOC.
- SOAR (Security Orchestration, Automation, and Response) runs playbooks to enrich, deduplicate, and automatically respond to alerts, standardizing handling and reducing analyst time on low-value duplicate alerts.
- The NIST SP 800-61 incident response lifecycle is Preparation, Detection & Analysis, Containment/Eradication/Recovery, and Post-Incident Activity (lessons learned); preparation precedes detection.
- MITRE ATT&CK is a knowledge base mapping adversary tactics (goals) and techniques (methods); SOCs use it to build detections, measure coverage, and structure threat-hunting hypotheses.
- Threat hunting is proactive, hypothesis-driven searching for undetected threats already in the environment, rather than waiting for an alert to fire.
- User and Entity Behavior Analytics (UEBA) baselines normal behavior and flags anomalies (impossible travel, unusual data access) to detect insider threats and compromised accounts that signature rules miss.

## Study tips

- Watch for the BEST or MOST/FIRST qualifier - several plausible answers may all be valid, but SecurityX rewards the choice that is most cost-effective, most defense-in-depth, or correctly sequenced (e.g., BIA before BC/DR, preparation before detection).
- Memorize the quantitative risk formulas cold (SLE = AV x EF, ALE = SLE x ARO) and be ready to compare ALE before vs. after a control to justify it; numeric scenarios are common.
- Expect performance-based questions with real CLI/config snippets (az network nsg, iptables, firewall-cmd, KQL, Terraform, Sysmon) - read the exact flags, ports, and direction (Inbound/Outbound, Allow/Deny) carefully.
- Think like an architect: prefer answers that reduce attack surface, enforce least privilege, segment/isolate, and scale horizontally over point fixes; distrust answers that disable monitoring or expose management interfaces.
- Manage the clock - at ~165 minutes for up to ~90 items, flag long performance-based simulations, answer the quick multiple-choice first, and never leave blanks since there is no penalty for guessing.

---

Want the full breakdown? See the complete **[CompTIA SecurityX (CAS-005, formerly CASP+) study guide](https://certgrid.app/study-guide/comptia-securityx-cas-005-formerly-casp)** and **[free practice questions](https://certgrid.app/practice/comptia-securityx-cas-005-formerly-casp)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

