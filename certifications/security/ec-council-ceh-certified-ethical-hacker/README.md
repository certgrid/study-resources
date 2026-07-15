# EC-Council CEH (Certified Ethical Hacker) - Study Cheatsheet

The EC-Council Certified Ethical Hacker (CEH) validates that a candidate can think and act like an attacker while staying within legal, authorized boundaries. It spans the full offensive lifecycle - reconnaissance, scanning, enumeration, system and web attacks, wireless, mobile, IoT/OT, cloud, and cryptography - along with the defensive countermeasures for each. It suits security analysts, penetration testers, SOC staff, and IT professionals moving into offensive or defensive security roles.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | EC-Council CEH (Certified Ethical Hacker) |
| Credential | EC-Council CEH (Certified Ethical Hacker) |
| Level | Intermediate |
| Practice mock length | ~125 questions |
| Duration | ~240 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Information Security and Ethical Hacking Overview | ~5% |
| 2 | Reconnaissance Techniques | ~20% |
| 3 | System Hacking Phases and Attack Techniques | ~16% |
| 4 | Network and Perimeter Hacking | ~16% |
| 5 | Web Application Hacking | ~16% |
| 6 | Wireless Network Hacking | ~5% |
| 7 | Mobile, IoT, and OT Hacking | ~11% |
| 8 | Cloud Computing | ~5% |
| 9 | Cryptography | ~5% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Information Security and Ethical Hacking Overview

- The CIA triad defines the core goals: confidentiality (preventing unauthorized disclosure), integrity (preventing unauthorized or undetected modification), and availability (ensuring access when needed). Altering data in transit is an integrity violation.
- Risk is a function of threat, vulnerability, and impact - it expresses the likelihood and consequence of loss when a threat exploits a weakness. A vulnerability is an exploitable flaw in design, implementation, operation, or configuration.
- The Cyber Kill Chain (Lockheed Martin) runs in a fixed order: Reconnaissance, Weaponization, Delivery, Exploitation, Installation, Command and Control (C2), and Actions on Objectives.
- Weaponization is the phase where an attacker couples an exploit with a payload (such as a RAT or backdoor) into a deliverable artifact like a malicious document, before any contact with the target.
- MITRE ATT&CK is a knowledge base of real-world adversary behavior organized as tactics (the goal, the 'why') and techniques (the 'how'), with sub-techniques and procedures.
- The five phases of a hack are Reconnaissance, Scanning, Gaining Access, Maintaining Access, and Clearing Tracks. Scanning actively probes for live hosts, open ports, and services.

### Domain 2 - Reconnaissance Techniques

- Passive footprinting gathers information from public sources (search engines, social media, WHOIS, archives) without sending packets to the target's own infrastructure, so it is undetectable by the target.
- Active footprinting interacts directly with target-owned systems - for example querying the target's own authoritative name server - and can therefore be detected.
- WHOIS queries registry/registrar databases and can reveal the registrant organization, admin/technical contacts, sponsoring registrar, name servers, and creation/updated/expiration dates unless masked by privacy services.
- Regional Internet Registries allocate IP address blocks by region; ARIN covers North America, and querying the right RIR maps a target's address ranges.
- Core DNS records for footprinting: A maps a host to IPv4, AAAA (quad-A) to IPv6, MX lists inbound mail servers with preference values, and SOA holds the zone's authoritative parameters (primary name server, admin contact, serial, timers).
- A DNS zone transfer (AXFR) replicates a full zone to secondaries; a misconfigured server that honors AXFR from any host lets an attacker download every record, exposing internal hostnames and IPs. dig is the flexible DNS query tool used for this.

### Domain 3 - System Hacking Phases and Attack Techniques

- Password attacks differ by strategy: a dictionary attack tests a curated wordlist, brute force exhausts the entire keyspace (guaranteed but slow), and a hybrid attack mutates dictionary words with appended digits or character substitutions.
- Password spraying tries one common password across many accounts to stay under lockout thresholds, making it stealthier than hammering a single account.
- Rainbow tables are precomputed hash-to-plaintext lookup structures that trade storage for speed; salting (unique random data per password) defeats them by making precomputation per-user impractical.
- John the Ripper and Hashcat are the standard offline crackers; Hashcat is known for GPU-accelerated, massively parallel hash computation.
- Windows stores local account hashes in the SAM database; the legacy LM hash uppercases the password and splits it into two independently hashed 7-character halves, drastically weakening it.
- The NTLM hash is an unsalted MD4 hash of the password and can be replayed in a pass-the-hash attack, which authenticates using a captured hash without ever knowing the plaintext.

### Domain 4 - Network and Perimeter Hacking

- Passive sniffing only captures traffic already visible on the segment (a hub or a SPAN/mirror port) with the NIC in promiscuous mode, while active sniffing injects packets to redirect traffic on switched networks.
- A switch learns MAC-to-port mappings in its CAM table and forwards unicast frames only out the owning port, isolating conversations - which is why sniffing on a switch requires an active attack.
- ARP is stateless and unauthenticated, so hosts cache any reply, including unsolicited (gratuitous) ones. Forged ARP replies poison victim caches so gateway traffic flows to the attacker, creating a man-in-the-middle.
- Dynamic ARP Inspection (DAI) validates ARP packets on untrusted ports against the DHCP snooping binding table and drops invalid IP-to-MAC bindings, neutralizing ARP poisoning.
- MAC flooding fills the finite CAM table with bogus source MACs so the switch fails open and floods unknown-unicast frames out all ports; port security caps MACs per port and triggers a shutdown/restrict/protect action.
- DHCP starvation exhausts the address pool by requesting all leases with spoofed MACs (a DoS), while a rogue DHCP server hands out a malicious gateway/DNS to route client traffic through the attacker.

### Domain 5 - Web Application Hacking

- Directory (path) traversal uses dot-dot-slash sequences to escape the web root and read arbitrary files; the primary defense is strict input validation and canonicalization of user-supplied paths.
- Banner grabbing and web server fingerprinting read Server and X-Powered-By headers and response behavior to identify software and versions; masking banners and using generic error pages reduces this fingerprinting.
- Default credentials are a leading compromise vector because many servers ship with documented default admin accounts; hardening requires changing or removing all defaults.
- HTTP response splitting injects unsanitized CRLF characters into response headers (such as a redirect Location or cookie), letting an attacker forge headers and body, enabling cache poisoning, XSS, or defacement; strip or encode CR/LF to prevent it.
- Web cache poisoning stores an attacker-controlled, unkeyed response in a shared cache so it is served to many victims; the defense is keying the cache on all inputs that affect the response.
- Directory listing (directory browsing) discloses files, backups, scripts, and folder layout; disable it and provide default index documents.

### Domain 6 - Wireless Network Hacking

- WEP uses the RC4 stream cipher with a weak 24-bit IV; on busy networks IVs are reused, causing keystream reuse that lets attackers statistically recover the key after enough capture.
- WPA2 (802.11i) mandates CCMP, which uses AES in counter mode for confidentiality and CBC-MAC for integrity, replacing the transitional RC4-based TKIP of WPA.
- WPA3-Personal replaces the PSK handshake with SAE (Dragonfly), providing forward secrecy and resistance to offline dictionary attacks; a weak WPA2 PSK, by contrast, can be recovered by offline cracking of a captured handshake.
- WPA2-Enterprise uses 802.1X/EAP with a RADIUS authentication server; EAP-TLS uses mutual certificate-based authentication, avoiding password-based weaknesses.
- An evil twin is a rogue AP configured with a legitimate SSID to lure auto-connecting clients, enabling traffic interception or captive-portal credential harvesting.
- A rogue access point is any unauthorized AP attached to the corporate network, expanding the attack surface regardless of intent.

### Domain 7 - Mobile, IoT, and OT Hacking

- Android builds its application sandbox on the Linux kernel by assigning each app a unique UID at install, so by default one app cannot read another app's process memory or private data directory.
- SELinux adds mandatory access control that confines processes to policy-defined domains, limiting damage even from privileged or compromised processes.
- Rooting (Android) and jailbreaking (iOS) grant privileged access that defeats sandboxing, code-signing, and secure boot, widening the attack surface and allowing unverified software; client-side root/jailbreak detection helps but can be bypassed and must be one layer among server-side controls.
- Unofficial app stores often skip the malware scanning, publisher verification, and policy review official stores perform, so repackaged/trojanized apps reach users; iOS defaults to App Store installs while Android permits user-enabled sideloading.
- App repackaging (trojanizing) means modifying a legitimate app to insert malicious code and redistributing it, often through third-party stores.
- The iOS Keychain is the encrypted, access-controlled store for secrets (passwords, keys, tokens), and the Secure Enclave is an isolated hardware coprocessor that handles keys and biometrics separately from the main CPU.

### Domain 8 - Cloud Computing

- Under the shared responsibility model, IaaS gives the customer the most control and responsibility (guest OS patching, hardening, apps, data), while the provider secures the physical facilities, hardware, network fabric, and hypervisor.
- In PaaS the provider manages the OS and runtime and the customer secures only their code, configuration, and data; in SaaS the provider manages nearly everything, but the customer always retains ownership of data, identity, permissions, and sharing settings.
- NIST deployment models: a private cloud is dedicated to one organization, a public cloud is shared, a community cloud serves a group with shared concerns, and a hybrid cloud binds two or more distinct clouds that remain separate but enable portability (such as cloud bursting).
- Public-read storage misconfiguration exposes objects to anonymous internet access, so a single wrong setting can leak large volumes of data to anyone who finds the URL.
- SSRF can coerce a server-side app into fetching the cloud instance metadata endpoint and leaking temporary credentials; enforce session-based (IMDSv2-style) metadata access and least-privilege roles.
- IAM failures - overly broad permissions, unused privileged accounts, and privilege-escalation paths - are a leading cloud attack vector, mitigated by least privilege and MFA on all accounts, especially privileged ones.

### Domain 9 - Cryptography

- AES is a symmetric block cipher that encrypts fixed 128-bit blocks with a single shared key and supports 128, 192, and 256-bit keys (using 10, 12, and 14 rounds respectively).
- DES has only a 56-bit effective key (64-bit with 8 parity bits) that modern hardware brute-forces quickly; 3DES runs DES three times in an encrypt-decrypt-encrypt sequence to extend key strength but is now legacy, retired in favor of AES.
- Block ciphers (such as AES) process fixed-size blocks and use modes of operation, while stream ciphers (such as RC4) generate a keystream XORed with plaintext one unit at a time. RC4 was deprecated in WEP and TLS due to keystream biases.
- ECB mode encrypts each block independently, so identical plaintext blocks produce identical ciphertext and leak structure; GCM is an authenticated encryption mode providing confidentiality and integrity in one operation.
- RSA security rests on the hardness of factoring a large semiprime modulus, while ECC achieves equivalent strength with much smaller keys, saving processing and bandwidth.
- Diffie-Hellman lets two parties agree on a shared secret over a public channel without transmitting the key; unauthenticated Diffie-Hellman is vulnerable to a man-in-the-middle who negotiates separate keys with each side.

## Study tips

- Watch authorization and intent keywords to classify hackers and testing types: 'authorized' points to white hat and white/black/gray-box scope, while 'without permission' plus intent separates black hats from gray hats.
- Memorize the fixed orderings the exam loves: the seven Cyber Kill Chain phases and the five hacking phases, and be able to place a described activity (for example weaponization vs delivery) in the right slot.
- For each attack, know the single best countermeasure: DAI for ARP poisoning, port security for MAC flooding, DHCP snooping for rogue DHCP, DNSSEC for cache poisoning, salting for rainbow tables, and 802.11w for deauth attacks.
- Map tools to their exact role - Shodan/Censys index devices, Maltego does link analysis, Nikto scans web servers, and in Aircrack-ng know airmon-ng vs airodump-ng vs aireplay-ng vs aircrack-ng.
- For cloud and mobile questions, reason from the shared responsibility model and the platform's built-in protections (sandbox UIDs, Keychain/Secure Enclave, IAM least privilege) rather than memorizing product names.

---

Want the full breakdown? See the complete **[EC-Council CEH (Certified Ethical Hacker) study guide](https://certgrid.app/study-guide/ec-council-ceh-certified-ethical-hacker)** and **[free practice questions](https://certgrid.app/practice/ec-council-ceh-certified-ethical-hacker)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

