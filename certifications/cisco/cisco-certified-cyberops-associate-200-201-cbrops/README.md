# Cisco Certified CyberOps Associate (200-201 CBROPS) - Study Cheatsheet

The Cisco Certified CyberOps Associate (200-201 CBROPS) validates the foundational skills of an entry-level security operations center (SOC) analyst: understanding security concepts, monitoring network traffic, analyzing hosts, investigating intrusions, and following security policies and procedures. It targets aspiring Tier 1 analysts and blue-team defenders who monitor, detect, and respond to threats. The exam is defensive in focus, emphasizing detection frameworks, evidence handling, and structured incident response over offensive techniques.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | Cisco Certified CyberOps Associate (200-201 CBROPS) |
| Credential | Cisco Certified CyberOps Associate (200-201 CBROPS) |
| Level | Associate |
| Practice mock length | ~95 questions |
| Duration | ~120 minutes |
| Passing score | 750 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Security Concepts | ~20% |
| 2 | Security Monitoring | ~25% |
| 3 | Host-Based Analysis | ~20% |
| 4 | Network Intrusion Analysis | ~20% |
| 5 | Security Policies and Procedures | ~15% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Security Concepts

- The CIA triad defines security goals: confidentiality protects data from unauthorized disclosure, integrity ensures data is not altered, and availability guarantees authorized users can access resources when needed.
- The CVSS Base score is split into an Exploitability sub-score (Attack Vector, Attack Complexity, Privileges Required, User Interaction) and an Impact sub-score (Confidentiality, Integrity, and Availability Impact).
- Privileges Required is a CVSS Base metric rated None, Low, or High that describes the access an attacker must already hold on the target before exploiting the vulnerability; Scope reflects whether exploitation affects resources beyond the vulnerable component.
- The CVSS Temporal metric group adjusts the Base score for factors that change over a vulnerability's life, such as Exploit Code Maturity, Remediation Level, and Report Confidence; the Environmental group reflects an individual organization's context.
- A vulnerability is a weakness (such as an unpatched library) that exists whether or not it is targeted; a threat is a potential danger, and an exploit is the actual method that takes advantage of the weakness.
- An attack vector is the path or method used to gain access or deliver a payload (for example phishing email or removable USB media), while the attack surface is the total set of exposed entry points.

### Domain 2 - Security Monitoring

- Security telemetry falls into data types including full packet capture, session data, transaction data, extracted content, alert data, and statistical data, each with different storage cost and investigative value.
- Statistical data (such as an average, baseline, or top-talkers report) is computed by analyzing other data rather than captured directly off the wire, while session data (for example a NetFlow record) summarizes a conversation with addresses, ports, protocol, and counters but no payload.
- Full packet capture stores complete payloads and consumes far more storage than payload-free session data; pairing an alert with the full packet capture lets an analyst confirm whether a rule match reflects genuinely malicious traffic.
- Extracted content is data carved directly out of the traffic stream, such as a recovered file or spreadsheet reassembled from captured packets.
- Statistical and alert data have the smallest footprint of the data types because both are brief computed or triggered records rather than per-packet or per-flow copies.
- Signature-based detection matches known patterns and misses novel attacks, while anomaly-based detection compares activity against a baseline and can flag previously unseen behavior that has no existing signature.

### Domain 3 - Host-Based Analysis

- The order of volatility dictates collecting the most fragile evidence first: CPU cache and registers, then RAM contents and active network state, before durable data like disk contents that survive longer.
- Endpoint detection and response (EDR) records detailed host telemetry across many event types to support retrospective investigation, while antivirus can be signature-based or behavioral, the latter flagging malicious runtime behavior even without a known signature.
- A host-based firewall enforces allowed ports, protocols, and remote addresses directly on the server, giving host-level control that persists even if the machine moves between networks.
- MITRE ATT&CK organizes adversary behavior into tactics and techniques and publishes separate matrices for enterprise IT, mobile, and industrial control systems; process injection is cataloged under defense evasion and privilege escalation.
- The Diamond Model of Intrusion Analysis links four core features of an event: adversary, capability, infrastructure, and victim.
- On Windows, the registry root HKEY_CURRENT_USER maps to the logged-on account's settings, and autostart persistence commonly lives in the CurrentVersion\Run key and the Services configuration key.

### Domain 4 - Network Intrusion Analysis

- The Cyber Kill Chain phases progress from reconnaissance, weaponization, and delivery through exploitation, installation, command and control, to actions on objectives; periodic encrypted beaconing to an external host maps to the Command and Control phase.
- Beaconing malware checks in with its C2 server on a fixed timer, producing near-identical low-volume flows at consistent short intervals, a well-known flow-based indicator of C2.
- A heavily outbound-skewed byte ratio, where large volumes leave a host while little returns, is a strong indicator of data exfiltration, since normal browsing and downloads are inbound-heavy.
- Carrier-protocol tunneling smuggles C2 or data inside commonly permitted protocols; DNS tunneling and ICMP tunneling both abuse protocol fields to blend covert traffic with routine name resolution or diagnostics.
- TCP flags carry meaning during analysis: many unanswered SYNs to sequential ports (or many RST/ACK replies to one source) indicate a port scan, and the PSH flag tells the receiver to push buffered data to the application immediately.
- A vertical port scan targets many ports on one host, while a horizontal scan probes one port across many hosts; sequential unanswered SYNs to one target indicate vertical scanning.

### Domain 5 - Security Policies and Procedures

- The NIST SP 800-61 incident response lifecycle has four phases: Preparation; Detection and Analysis; Containment, Eradication, and Recovery; and Post-Incident Activity.
- Detection and Analysis work includes correlating alerts to confirm a real attack, determining scope and root cause, and assigning priority based on functional and informational impact, which shapes the containment strategy that follows.
- Post-Incident Activity, commonly called the lessons-learned phase, is a retrospective review meeting held after resolution to evaluate what worked, update documentation, and improve future response.
- An incident is a confirmed violation, or imminent threat of violation, of security policy that harms the confidentiality, integrity, or availability of information; active file encryption across many hosts qualifies, whereas a single blocked probe is only an event.
- A policy is a high-level statement of intent, while a playbook is a documented process for handling a specific incident type including decision points, roles, and granular details like OS-specific isolation commands and escalation contacts.
- SOC analysts work in tiers: Tier 1 performs initial triage of incoming alerts and escalates confirmed incidents, and when a Tier 1 analyst cannot determine an alert's disposition it is escalated to Tier 2 for deeper investigation.

## Study tips

- Memorize the CVSS Base metric groups cold: know which metrics belong to Exploitability (Attack Vector, Attack Complexity, Privileges Required, User Interaction) versus Impact (Confidentiality, Integrity, Availability), and how Temporal and Environmental adjust the Base score.
- Be able to classify a scenario into the correct security data type (session, full packet capture, transaction, extracted content, alert, statistical) by asking whether the data was captured off the wire or computed from other data.
- Know the mapping frameworks precisely: the Cyber Kill Chain phases, MITRE ATT&CK tactics/techniques, and the four Diamond Model features, and practice placing a described behavior into the right one.
- For host and network questions, memorize concrete identifiers: Windows event IDs (4624, 1102), protocol field values (6 = TCP, 17 = UDP), well-known ports, chmod special bits (4/2/1), and PID 1 = systemd.
- Lock in the NIST 800-61 incident response order and the order of volatility; questions frequently test which phase an activity belongs to and which evidence to collect first.

---

Want the full breakdown? See the complete **[Cisco Certified CyberOps Associate (200-201 CBROPS) study guide](https://certgrid.app/study-guide/cisco-certified-cyberops-associate-200-201-cbrops)** and **[free practice questions](https://certgrid.app/practice/cisco-certified-cyberops-associate-200-201-cbrops)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

