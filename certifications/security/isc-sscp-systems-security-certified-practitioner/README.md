# (ISC)² SSCP (Systems Security Certified Practitioner) - Study Cheatsheet

The (ISC)2 SSCP (Systems Security Certified Practitioner) validates the hands-on, operational security skills needed to implement, monitor, and administer IT infrastructure using established security policies and procedures. It is aimed at practitioners in roles such as security analyst, systems and network administrator, and security engineer who work day to day with access controls, monitoring, incident response, cryptography, and system hardening. The exam spans seven domains and rewards practical, defense-in-depth knowledge over pure theory.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | (ISC)² SSCP (Systems Security Certified Practitioner) |
| Credential | (ISC)² SSCP (Systems Security Certified Practitioner) |
| Level | Intermediate |
| Practice mock length | ~125 questions |
| Duration | ~180 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Security Operations and Administration | ~15% |
| 2 | Access Controls | ~15% |
| 3 | Risk Identification, Monitoring, and Analysis | ~16% |
| 4 | Incident Response and Recovery | ~11% |
| 5 | Cryptography | ~11% |
| 6 | Network and Communications Security | ~16% |
| 7 | Systems and Application Security | ~16% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Security Operations and Administration

- The CIA triad frames security goals: confidentiality restricts disclosure to authorized parties (often via encryption), integrity ensures data is not altered without detection (often via hashing), and availability ensures authorized users can reach systems and data when needed (often via redundancy and failover).
- Identification is the claim of an identity such as a username; authentication proves that claim; authorization defines what an authenticated subject may do; and accounting (auditing) logs subject activity for later review and non-repudiation.
- The (ISC)2 Code of Ethics has four mandatory canons, and protecting society, the common good, and public trust is the first and highest-priority canon that guides ordering decisions when canons appear to conflict.
- Controls are grouped by type: administrative (managerial) controls such as policies and training, technical (logical) controls implemented in hardware or software, and physical controls such as locks and badge-controlled doors.
- Controls are also grouped by function: preventive controls stop unwanted events before they occur, and detective controls identify and signal events that are happening or have occurred.
- Corrective controls remediate and restore after an event, deterrent controls discourage attackers by perception, and recovery controls restore systems and data to operational status.

### Domain 2 - Access Controls

- The AAA model comprises authentication (proving an asserted identity), authorization (granting rights and permissions), and accounting (recording what a subject did after gaining access).
- The identity lifecycle spans provisioning (creating an account and assigning initial entitlements when a user joins), ongoing management, and deprovisioning; a deprovisioning gap leaves orphaned accounts that persist as unmonitored targets.
- Authentication factors fall into distinct categories: something you know (passwords, PINs), something you have (tokens, smart cards), something you are (biometrics), somewhere you are (location), and something you do (behavior).
- True multifactor authentication requires credentials drawn from at least two different factor categories; combining two items from the same category (such as a password and a PIN) is multi-step but not multifactor.
- Biometrics include physiological traits such as iris, fingerprint, and face (something you are) and behavioral traits such as typing rhythm and mouse dynamics (something you do).
- The False Acceptance Rate (FAR) is how often the system wrongly accepts an impostor, the False Rejection Rate (FRR) is how often it wrongly rejects a valid user, and the Crossover Error Rate (CER) where FAR equals FRR is a single comparative measure of biometric accuracy.

### Domain 3 - Risk Identification, Monitoring, and Analysis

- Risk is generally the product of the likelihood of an event and its impact; a vulnerability is a weakness that a threat can exploit.
- Single Loss Expectancy (SLE) equals asset value multiplied by the exposure factor (the percentage of value lost in one event); for example a $200,000 asset with a 40 percent exposure factor gives an SLE of $80,000.
- The Annualized Rate of Occurrence (ARO) is the expected number of events per year; an event happening once every four years is a rate of 1 divided by 4, or 0.25.
- Annualized Loss Expectancy (ALE) equals SLE multiplied by ARO, giving the expected yearly cost of a risk; for example an $80,000 SLE at an ARO of 0.25 yields an ALE of $20,000.
- The net value of a safeguard equals the reduction in ALE (ALE before minus ALE after) minus the annual cost of the safeguard; a positive result means the control is cost-justified.
- Qualitative analysis ranks risk descriptively using scales such as high, medium, and low, while quantitative analysis expresses risk in numeric, usually monetary, terms to enable cost-benefit comparison.

### Domain 4 - Incident Response and Recovery

- The incident response lifecycle moves through preparation, detection and analysis, containment, eradication, recovery, and lessons learned (post-incident activity).
- Preparation is the proactive phase that stands up the response team, writes plans and playbooks, arranges communications, and procures tooling before any incident occurs.
- Detection and analysis identifies, correlates, and validates events and alerts to confirm whether an actual incident occurred and to understand its scope.
- Containment limits the spread and magnitude of an incident, often by isolating affected systems or network segments while responders investigate; network isolation preserves running state while stopping propagation.
- Eradication removes the threat and its artifacts and closes the entry point (deleting malware, removing malicious accounts, and remediating the exploited vulnerability) so the threat cannot simply return.
- Recovery restores affected systems to normal operation from trusted backups, validates functionality, and monitors for recurrence before the incident is declared closed.

### Domain 5 - Cryptography

- Cryptography delivers confidentiality (restricting who can read data), integrity (detecting unauthorized modification via hashes and message authentication codes), authentication, and non-repudiation (binding an action to an identity so the originator cannot deny it).
- Non-repudiation and digital signatures are achieved with the sender's private key, which only the sender possesses; verifiers check the signature using the signer's public key.
- Symmetric cryptography uses one shared secret key for both encryption and decryption, while asymmetric cryptography uses a related public/private key pair where data encrypted with one key is decrypted with the other.
- AES is a symmetric block cipher operating on fixed 128-bit blocks and supporting 128-, 192-, and 256-bit keys (using 10, 12, and 14 rounds respectively).
- DES has only a 56-bit effective key that is small enough to brute-force, so 3DES chains DES operations to raise effective key strength on existing hardware as a stopgap.
- Block ciphers process fixed-size blocks while stream ciphers process a bit or byte at a time; ECB mode encrypts each block independently so identical plaintext blocks produce identical ciphertext, leaking patterns.

### Domain 6 - Network and Communications Security

- The OSI Network layer (Layer 3) handles logical IP addressing and path determination, where routers forward packets by destination IP, and the Transport layer (Layer 4) provides end-to-end delivery, segmentation, and port addressing using TCP and UDP.
- The TCP/IP model has four layers (Application, Transport, Internet, and Network Access); its Application layer maps to OSI layers 5, 6, and 7, and its Network Access layer maps to OSI layers 1 and 2.
- Common well-known ports include DNS on UDP 53 (TCP 53 for zone transfers), DHCP on UDP 67 (server) and 68 (client), SMTP on TCP 25, POP3 on TCP 110, SSH on TCP 22, and HTTPS on TCP 443; the well-known port range is 0 to 1023.
- IP subnetting facts include that a /24 provides 254 usable host addresses, a /26 prefix equals the mask 255.255.255.192, 172.16.0.0/12 is an RFC 1918 private range, and the broadcast address of 192.168.10.0/28 is 192.168.10.15.
- In a star topology a central device failure disconnects all attached nodes, whereas a full mesh connects every node to every other node to maximize fault tolerance.
- A man-in-the-middle (on-path) attack intercepts and possibly alters traffic between two parties, and TLS with proper certificate validation defends against MITM on web sessions.

### Domain 7 - Systems and Application Security

- A worm self-propagates across networks without a host file or user action, while a Trojan horse masquerades as benign software to trick a user into running a hidden malicious payload and does not self-replicate.
- Polymorphic malware mutates its code and encryption on each infection to defeat static signatures, and a rootkit hides malicious activity by tampering with OS mechanisms such as kernel calls, making it among the hardest malware to detect and remove.
- Recovering from ransomware reliably depends on backups that are recent, restore-tested, and kept offline or otherwise isolated so the ransomware cannot encrypt them too.
- Signature-based detection cannot match zero-day or novel malware for which no signature yet exists, so behavior-based detection flags malicious activity by what code does rather than by a known pattern.
- EDR adds continuous endpoint telemetry, detection, investigation, and response beyond simple antivirus, and XDR extends detection and response across multiple security layers rather than endpoints alone.
- HIDS detects and alerts on suspicious host activity, while HIPS additionally blocks or prevents malicious activity in real time.

## Study tips

- Learn to distinguish control classifications along two axes at once: type (administrative, technical, physical) and function (preventive, detective, corrective, deterrent, compensating, recovery); questions often give a scenario and ask for both.
- Memorize the quantitative risk formulas cold: SLE = asset value x exposure factor, ALE = SLE x ARO, and safeguard value = (ALE before - ALE after) - annual safeguard cost, then practice plugging in numbers quickly.
- Know the well-known ports and subnetting shortcuts (usable hosts, masks, broadcast addresses, RFC 1918 ranges) so you can answer network questions without hesitation.
- For multifactor questions, always check whether the factors come from different categories; two things you know is never true MFA no matter how many steps are involved.
- Study the incident response and NIST RMF phase orders as sequences, because many questions ask which phase comes next or which activity belongs to a named phase.

---

Want the full breakdown? See the complete **[(ISC)² SSCP (Systems Security Certified Practitioner) study guide](https://certgrid.app/study-guide/isc-sscp-systems-security-certified-practitioner)** and **[free practice questions](https://certgrid.app/practice/isc-sscp-systems-security-certified-practitioner)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

