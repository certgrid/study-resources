# CompTIA CySA+ (CS0-003) - Study Cheatsheet

CompTIA CySA+ (CS0-003) validates the hands-on skills of a security analyst working in a SOC: detecting threats with logs and behavioral analytics, managing vulnerabilities, leading incident response, and communicating findings to stakeholders. It is an intermediate-level, performance-based exam aimed at SOC analysts, threat hunters, vulnerability analysts, and incident responders with a few years of IT security experience. The single CS0-003 exam covers four domains weighted toward Security Operations and Vulnerability Management.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | CompTIA CySA+ (CS0-003) |
| Credential | CompTIA CySA+ (CS0-003) |
| Level | Intermediate |
| Practice mock length | ~85 questions |
| Duration | ~165 minutes |
| Passing score | 830 out of 1000 |
| Notes reviewed | 2026-06-23 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Security Operations | ~35% |
| 2 | Vulnerability Management | ~26% |
| 3 | Incident Response and Management | ~21% |
| 4 | Reporting and Communication | ~18% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Security Operations

- MITRE ATT&CK is a knowledge base of real-world adversary tactics (the goal, e.g. Initial Access, Exfiltration) and techniques (the method); analysts map observed behavior to TTPs to find detection gaps and build threat-informed defense.
- An Indicator of Compromise (IOC) is a forensic artifact (malicious hash, IP, domain, file name) showing a host may already be breached; an Indicator of Attack (IOA) describes attacker behavior/intent in progress.
- On the Pyramid of Pain, hash values and IP addresses are trivial for attackers to change (low pain), while TTPs are the hardest to alter (high pain) and most valuable to detect on.
- A SIEM aggregates and correlates logs/events from many sources for centralized detection, alerting, and analysis; correlation across systems plus tamper-resistant log storage defeats local log deletion by attackers.
- SOAR platforms use playbooks to orchestrate and automate repetitive response actions (enrich alert, block IP, disable account), reducing analyst toil and standardizing handling.
- EDR provides endpoint telemetry (process creation, file, registry, and network events) for detection and response; XDR extends correlation across endpoint, network, email, and cloud.

### Domain 2 - Vulnerability Management

- Credentialed (authenticated) scans log into the host for deeper visibility into installed patches and configurations and produce far fewer false positives than uncredentialed scans.
- CVSS is a standardized 0-10 severity score (Base, Temporal, Environmental metrics); use it as a starting point, not the sole driver of remediation order.
- A CVE is a single disclosed vulnerability instance with a unique ID; a CWE is the category or class of weakness (e.g., CWE-79 cross-site scripting) that the CVE is an instance of.
- Risk-based prioritization combines CVSS with threat context: EPSS estimates exploitation probability and the CISA KEV catalog flags vulnerabilities known to be actively exploited in the wild.
- A zero-day is a flaw unknown to the vendor or lacking a patch, leaving no fix available while attackers may already be exploiting it.
- When a patch is not yet available, apply compensating controls (network segmentation, WAF rules, disabling the vulnerable feature) to reduce risk until remediation.

### Domain 3 - Incident Response and Management

- The NIST SP 800-61 incident response lifecycle is: Preparation, then Detection and Analysis, then Containment/Eradication/Recovery, then Post-Incident Activity (lessons learned).
- Containment limits the spread and impact of an incident before eradication and recovery; it can be short-term (isolate now) or long-term (apply temporary fixes while keeping operations running).
- Common containment actions include disabling compromised accounts (usermod -L user), blocking malicious IPs/domains (iptables -A OUTPUT -d 203.0.113.7 -j DROP), and isolating cloud instances by swapping to a quarantine security group.
- Eradication removes the threat (malware, attacker accounts, persistence mechanisms) from the environment, while recovery restores systems to normal operation and monitors for recurrence.
- Chain of custody documents who handled evidence, when, and how, preserving integrity and admissibility; gaps can render evidence unusable in court.
- Hash acquired forensic images (sha256sum sdb.img > sdb.img.sha256) to prove integrity, and use write-blockers when imaging to prevent altering the source.

### Domain 4 - Reporting and Communication

- Root cause analysis identifies the underlying cause so corrective actions prevent recurrence, rather than just fixing the immediate symptom.
- Tailor reporting to the audience: executives need business impact, risk, and cost-to-remediate, while the SOC needs IOCs, TTPs, and concrete remediation steps.
- Mean Time to Detect (MTTD) measures how long threats dwell before discovery; a fast MTTR with a long MTTD still means attackers operated undetected for hours.
- MTTD and MTTR drive different fixes: detection gaps need better telemetry and rules, while response gaps need improved process and playbook automation.
- Express vulnerability risk in business terms and trends (risk reduction over time, exposure of internet-facing critical assets) tied to decisions, not raw technical vulnerability counts.
- Present prioritized remediation options with estimated impact, likelihood, and cost-to-remediate so leadership can make risk-based decisions.

## Study tips

- Expect performance-based questions (PBQs) early in the exam; if one is consuming too much time, flag it and return after answering the multiple-choice items so you do not run out of time across the 165-minute window.
- When a question asks what to do 'first' or 'next,' anchor to the NIST IR lifecycle and the order of volatility: containment precedes eradication, and volatile memory is collected before disk imaging.
- Differentiate the look-alike terms cold: CVE vs CWE, IOC vs IOA/TTP, SAST vs DAST, EDR vs SIEM vs SOAR, MTTD vs MTTR, and eradication vs recovery.
- For prioritization questions, pick the answer that layers threat context (CISA KEV active exploitation, then EPSS probability) and asset criticality on top of the raw CVSS score, not CVSS alone.
- Read scenario stems for the role/audience cue: 'report to executives' means business-impact and cost framing, while 'report to the SOC' means technical IOCs, TTPs, and remediation steps.

---

Want the full breakdown? See the complete **[CompTIA CySA+ (CS0-003) study guide](https://certgrid.app/study-guide/comptia-cysa-cs0-003)** and **[free practice questions](https://certgrid.app/practice/comptia-cysa-cs0-003)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

