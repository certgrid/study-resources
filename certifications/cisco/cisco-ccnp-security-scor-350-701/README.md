# Cisco CCNP Security SCOR (350-701) - Study Cheatsheet

The Cisco CCNP Security SCOR (350-701) exam validates the ability to implement and operate core security technologies across network, cloud, content, and endpoint security, plus secure network access, visibility, and automation. It is a 120-minute exam (about 90-110 questions, passing score 825/1000) that serves as both the core exam for the CCNP Security certification and the qualifying exam for CCIE Security. It targets network and security engineers with several years of hands-on experience deploying Cisco security solutions.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | Cisco CCNP Security SCOR (350-701) |
| Credential | Cisco CCNP Security SCOR (350-701) |
| Level | Intermediate |
| Practice mock length | ~100 questions |
| Duration | ~120 minutes |
| Passing score | 825 out of 1000 |
| Notes reviewed | 2026-06-22 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Security Concepts | ~17% |
| 2 | Network Security | ~25% |
| 3 | Securing the Cloud | ~16% |
| 4 | Content Security | ~14% |
| 5 | Endpoint Protection and Detection | ~13% |
| 6 | Secure Network Access, Visibility, Enforcement | ~15% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Security Concepts

- The CIA triad is Confidentiality (data accessible only to authorized parties), Integrity (data is unaltered), and Availability (systems/data reachable when needed); every control maps to protecting one of these pillars.
- Zero trust assumes no implicit trust based on network location and verifies every request continuously using identity, device posture, and context before granting least-privilege access.
- AAA splits into Authentication (proving who you are), Authorization (what you may do), and Accounting (logging what you did); RADIUS combines authn/authz in one exchange while TACACS+ separates all three.
- Symmetric encryption (AES) is fast and used for bulk/VPN data confidentiality; asymmetric crypto (RSA, ECDSA, Diffie-Hellman) is slower and used to exchange session keys and for digital signatures.
- Digital signatures and HMAC both provide integrity and authenticity; HMAC uses a shared secret while a digital signature uses the sender's private key and is verified with the public key.
- Defense in depth layers multiple controls (perimeter NGFW, internal IPS, endpoint protection, segmentation, encryption) so the failure of one control does not lead to full compromise.

### Domain 2 - Network Security

- A stateful firewall tracks connection state and auto-permits return traffic of an established session; a stateless ACL evaluates each packet independently with no session awareness.
- Cisco Secure Firewall (Firepower Threat Defense / FTD) is the NGFW that adds AVC, URL filtering, Advanced Malware Protection, and Snort-based IPS on top of stateful inspection; managed by FMC or FDM.
- An IPsec site-to-site VPN uses IKE (Phase 1 negotiates the ISAKMP/IKE SA and authenticates peers; Phase 2 negotiates the IPsec SAs) and ESP to encrypt and authenticate the data.
- IKEv2 is the modern key-exchange protocol with built-in NAT traversal, EAP support, fewer messages than IKEv1, and asymmetric authentication; it replaces IKEv1 main/aggressive mode.
- DMVPN builds scalable dynamic site-to-site tunnels using mGRE, NHRP, and IPsec; Phase 3 enables direct dynamic spoke-to-spoke tunnels with NHRP redirects, removing hub data-plane bottlenecks.
- A DMZ is a segmented zone for internet-facing servers (web, mail, DNS) so a compromise there gives no direct path to the internal network.

### Domain 3 - Securing the Cloud

- The shared responsibility model splits duties: the provider secures the underlying infrastructure (hardware, hypervisor, fabric) while the customer secures data, IAM, OS, application config, and network rules; the boundary shifts across IaaS, PaaS, and SaaS.
- Cloud security best practices center on least-privilege IAM, encryption of data at rest (cloud KMS or customer-managed keys) and in transit (TLS), and network/micro-segmentation.
- A Cloud Access Security Broker (CASB) sits between users and SaaS apps to give visibility into shadow IT, enforce DLP, and apply access policy; Cisco Umbrella and Cisco Cloudlock provide CASB functions.
- Cisco Umbrella enforces DNS-layer security by resolving queries through threat-intelligence-checked recursive resolvers, blocking malicious domains before a connection is made, on or off network.
- ip name-server 208.67.222.222 208.67.220.220 points a device at the Umbrella (OpenDNS) public resolvers for DNS-layer protection.
- Cisco Secure Workload (formerly Tetration) provides application-dependency mapping and micro-segmentation, pushing host-based firewall rules into each workload's OS firewall via an agent.

### Domain 4 - Content Security

- A Secure Web Gateway (SWG) / web proxy sits inline for HTTP/HTTPS to perform URL categorization and filtering, malware scanning of downloads, and DLP; Cisco Secure Web Appliance (WSA) and cloud Umbrella SIG provide it.
- Cisco Secure Web Appliance (WSA) operates in explicit mode (clients point at the proxy) or transparent mode (traffic redirected via WCCP/PBR); explicit mode requires client/PAC configuration.
- An email security gateway (Cisco Secure Email / ESA) blocks spam, phishing, and malicious attachments/links using Talos reputation, anti-spam engines, URL filtering, and file sandboxing.
- SPF authorizes which mail servers may send for a domain (DNS TXT record), DKIM cryptographically signs messages, and DMARC ties SPF/DKIM alignment to a published policy and reporting.
- DMARC policy p=none only monitors and reports; p=quarantine sends failing mail to spam; p=reject blocks it outright, so p=none does not stop spoofed mail by itself.
- Cisco Umbrella DNS-layer security blocks resolution of malicious domains before any session is established, protecting on- and off-network clients with minimal latency.

### Domain 5 - Endpoint Protection and Detection

- Traditional antivirus relies on signature matching and misses novel/fileless threats; EDR adds continuous behavioral monitoring of process, file, network, and registry activity for detection and response.
- Cisco Secure Endpoint (formerly AMP for Endpoints) is a cloud-managed EDR/AV using Talos intelligence and cloud file reputation to detect, block, and investigate malware.
- Retrospective security is Secure Endpoint's signature feature: it records file activity continuously and, when Talos later flags a file as malicious, identifies every endpoint that saw it and can quarantine after the fact.
- Device trajectory and file trajectory visualizations trace a file's path and process lineage across hosts to reconstruct lateral movement and scope an incident.
- Application allow-listing (default-deny, only approved software runs) is among the strongest endpoint controls but breaks legitimate-but-unlisted updates and scripts if not carefully maintained.
- Custom Detections - Simple uses a Blocked Application List to block files by SHA-256 hash; Advanced Custom Detections use signatures for broader matching.

### Domain 6 - Secure Network Access, Visibility, Enforcement

- Cisco Identity Services Engine (ISE) is the NAC/policy platform acting as a RADIUS/TACACS+ server that enforces 802.1X, profiling, posture assessment, and segmentation (TrustSec SGTs).
- IEEE 802.1X is port-based access control with three roles: supplicant (endpoint), authenticator (switch/AP), and authentication server (ISE/RADIUS), carrying EAP over LAN (EAPOL) before the port opens.
- MAC Authentication Bypass (MAB) authenticates non-supplicant devices (printers, cameras) by their MAC address and is combined with device profiling to apply the right authorization while keeping the port under policy.
- ISE Monitor Mode (open authentication with logging) identifies devices that would fail authentication so policy gaps are fixed before Closed/Low-Impact mode enforces and blocks production traffic.
- TACACS+ is preferred for device administration because it separates AAA and supports granular per-command authorization; RADIUS is preferred for network access (802.1X) and end-user authentication.
- Cisco Secure Network Analytics (formerly Stealthwatch) ingests NetFlow/IPFIX/NSEL telemetry and applies behavioral analytics to detect exfiltration, insider threats, and anomalies without inline inspection.

## Study tips

- Know the Cisco product portfolio by both current and legacy names: Secure Firewall (FTD/Firepower), Secure Endpoint (AMP), Secure Email (ESA), Secure Web Appliance (WSA), Secure Network Analytics (Stealthwatch), Secure Workload (Tetration), and Umbrella, since questions use either name.
- Be fluent in the CLI snippets: 802.1X (dot1x system-auth-control, access-session port-control auto, mab), AAA/RADIUS/TACACS+ groups, NetFlow exporters, crypto key generation, and IKEv2/IPsec show commands.
- For IPsec questions, separate IKE Phase 1 (peer auth, ISAKMP SA) from Phase 2 (IPsec SAs/ESP), and know DMVPN Phase 3 enables direct spoke-to-spoke tunnels.
- Distinguish RADIUS vs TACACS+ (network access vs device admin, combined vs separated AAA, UDP vs TCP, partial vs full payload encryption) - it is a recurring distractor pair.
- Expect scenario questions on cost, performance, and scaling (selective TLS decryption, flow offload, distributed PSNs/SWG PoPs, consumption licensing); pick the option that preserves security while reducing overhead, not the one that disables inspection.

---

Want the full breakdown? See the complete **[Cisco CCNP Security SCOR (350-701) study guide](https://certgrid.app/study-guide/cisco-ccnp-security-scor-350-701)** and **[free practice questions](https://certgrid.app/practice/cisco-ccnp-security-scor-350-701)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

