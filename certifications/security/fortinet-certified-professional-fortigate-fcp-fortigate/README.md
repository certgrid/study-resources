# Fortinet Certified Professional - FortiGate (FCP - FortiGate) - Study Cheatsheet

The FCP - FortiGate certification (formerly NSE 4) validates the ability to deploy, configure, and operate FortiGate next-generation firewalls running FortiOS. It is aimed at network and security professionals who administer FortiGate day to day, covering system setup, firewall policy and NAT, authentication and FSSO, SSL and IPsec VPN, security profiles, routing and SD-WAN, high availability, and logging and diagnostics.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | Fortinet Certified Professional - FortiGate (FCP - FortiGate) |
| Credential | Fortinet Certified Professional - FortiGate (FCP - FortiGate) |
| Level | Advanced |
| Practice mock length | ~40 questions |
| Duration | ~90 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Deployment and system configuration | ~12% |
| 2 | Firewall policies and NAT | ~15% |
| 3 | Authentication and FSSO | ~10% |
| 4 | SSL and IPsec VPN | ~14% |
| 5 | Security profiles (AntiVirus, Web Filter, Application Control, IPS) | ~18% |
| 6 | Routing and SD-WAN | ~13% |
| 7 | High availability | ~8% |
| 8 | Logging, monitoring, and diagnostics | ~10% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Deployment and system configuration

- The admin GUI and the SSL VPN web portal both default to TCP port 443, so when both must be reachable on one interface an administrator commonly moves the GUI to an alternate port such as 8443 to avoid the conflict.
- The administrator idle timeout defines how long a GUI or CLI session can stay inactive before FortiOS logs the admin out, reducing the risk of an unattended session being misused.
- Trusted hosts restrict which source addresses may log in to an administrator account, and management access protocols (HTTPS, SSH, ping, etc.) must be explicitly enabled per interface.
- A downstream device requesting to join a Security Fabric appears as unauthorized on the root FortiGate until an administrator authorizes (trusts) it under Security Fabric settings, after which it becomes an active member in the topology.
- A fabric connector integrates an external product or platform (such as an SDN or cloud provider) with the Security Fabric, and an interface with the Undefined role does not receive the GUI's role-based default policy and configuration suggestions.
- Administrative distance measures how trustworthy a routing source is; directly connected routes default to 0, static routes to 10, OSPF to 110, and BGP to 20 (external) or 200 (internal).

### Domain 2 - Firewall policies and NAT

- FortiGate evaluates firewall policies top-to-bottom and applies the first policy that matches the traffic, so ordering is critical; the policy list view shows policies in their actual evaluation order.
- Address groups can nest other address groups, letting a single policy reference many addresses through one grouped object to simplify management.
- The Overload IP pool performs many-to-one source NAT by dynamically assigning source ports, letting many internal hosts share a few public addresses; it is the default and most common pool type.
- A Fixed Port Range pool conserves addresses like Overload but confines each host's translated sessions to a defined port span rather than the full available range.
- Per-policy NAT is the default; enabling Central NAT is a single VDOM-wide setting, and a Central SNAT rule can be configured to match and account for traffic while applying no translation.
- Security profiles are applied within the firewall policy, not within a Central SNAT rule.

### Domain 3 - Authentication and FSSO

- A user group that references a RADIUS server directly, rather than listing individual accounts, lets any user who successfully authenticates against that server be treated as a member, scaling far better than duplicating accounts locally.
- A RADIUS server object requires the server address, a shared secret matched on both ends, and an authentication protocol (PAP, CHAP, MS-CHAP-v2, or Auto); RADIUS authentication uses UDP port 1812 by default.
- The shared secret authenticates FortiGate to the RADIUS server and helps protect the credential exchange.
- RADIUS can return group membership using the standard Filter-Id attribute or the Fortinet-Group-Name vendor-specific attribute, which explicitly names the FortiGate user group the user should join.
- RSSO derives identity from RADIUS accounting messages (from 802.1X switches, wireless controllers, or VPN devices) rather than from Active Directory logon events.
- The LDAP Regular bind type requires FortiGate to authenticate first with a dedicated search account's distinguished name and password before locating users.

### Domain 4 - SSL and IPsec VPN

- IKE Phase 1 authenticates the peers and negotiates the encryption, hashing, and Diffie-Hellman parameters that build the secure IKE channel; Phase 2 then negotiates the IPsec security associations that actually encrypt user data, and Phase 2 cannot start until Phase 1 succeeds.
- Standard non-NAT-T IPsec uses UDP port 500 for IKE and IP protocol 50 (ESP) for the encrypted payload, and both must be permitted through any intervening firewall.
- Phase 1 fails outright if the two peers use different IKE versions, and a mismatch in encryption, authentication, or Diffie-Hellman group between the peers is a likely cause of Phase 1 failure.
- A Phase 2 failure with a working Phase 1 is commonly caused by the source and destination subnets in the Phase 2 selectors not matching on both sides.
- Route-based (interface mode) IPsec creates a virtual tunnel interface bound to a physical interface that participates in the routing table, so it uses standard accept policies and needs a static or dynamic route pointing traffic into the tunnel.
- Policy-based VPNs use the special IPsec policy action and lack a virtual tunnel interface, which is why they cannot run a dynamic routing protocol over the tunnel.

### Domain 5 - Security profiles (AntiVirus, Web Filter, Application Control, IPS)

- On models with local storage, quarantined files are held in a dedicated quarantine area on the FortiGate's internal disk, where an administrator can browse, download, or delete them; models without a disk have limited or no local quarantine.
- The regular (normal) AV database focuses on current, actively spreading threats with a smaller footprint and lower resource use and is the default, while the extended database covers a broader historical set.
- An external malware block list references an administrator-maintained set of file hashes (often via a threat feed connector) so matching files are blocked regardless of whether they trigger a standard AV signature.
- FortiSandbox runs dynamic behavioral analysis on files the AV engine cannot classify, returning refined verdict feedback and letting administrators view sandbox analysis logs.
- Certificate (SSL) inspection reads only the certificate and cannot examine the decrypted contents of an encrypted session, so full (deep) SSL inspection is required to let AntiVirus and IPS scan the payload, at the cost of full file buffering and added latency.
- In deep inspection FortiGate copies the original certificate's subject details into a replacement certificate but signs it with its own CA, so the site name looks correct but the issuer changes; using an internal enterprise CA that domain-joined clients already trust avoids distributing a new certificate.

### Domain 6 - Routing and SD-WAN

- Administrative distance selects between routing sources and the lower value wins; when distances tie, FortiGate uses priority as a tiebreaker and installs only the route with the lower priority value, keeping the higher-priority route in the RIB as a standby.
- A static route with distance 10 is installed over an OSPF route to the same destination because 110 is higher, and giving a backup route a higher administrative distance than the primary keeps it out of the FIB until the primary disappears.
- The default route 0.0.0.0/0.0.0.0 matches any destination for which no more specific route exists, and dragging a more specific rule higher establishes precedence in ordered lists.
- get router info routing-table database shows all candidate RIB routes including backups, while get router info routing-table all shows only the winning routes installed in the FIB; diagnose firewall route list also displays active FIB entries.
- The default ECMP load-balancing method is source-IP-based hashing.
- OSPF neighbor states progress Down, Init, 2-Way, ExStart, Exchange, Loading, Full; 2-Way means neighbors have seen each other in hellos and Full means databases are synchronized.

### Domain 7 - High availability

- FGCP is a Fortinet-proprietary protocol that synchronizes configuration and, optionally, session state across a cluster, doing far more than just failing over an IP address.
- FGCP primary election compares monitored interface status first (fewest failed monitored interfaces wins), then HA uptime, then device priority, and finally the higher serial number as the last tiebreaker.
- With override disabled, meaningful HA uptime differences (a 300-second / 5-minute threshold) generally outweigh priority; with override enabled, higher device priority is favored for primary election.
- A healthy subordinate becomes the new primary after a monitored interface failure on the current primary.
- Session pickup is disabled by default, so without it active sessions are dropped and must be re-established after a failover; it must be explicitly enabled to preserve sessions.
- The heartbeat interface with the higher priority value is preferred for carrying heartbeat traffic while others stay as backups.

### Domain 8 - Logging, monitoring, and diagnostics

- Local disk logging requires the FortiGate to have installed nonvolatile storage such as an HDD, SSD, or SD card; models without such storage cannot use disk as a log destination.
- FortiAnalyzer is the dedicated Fortinet appliance or VM for centralized multi-device log analytics and reporting, and both FortiAnalyzer and a syslog server are valid remote destinations that can run alongside local disk logging.
- FortiGate sends syslog over UDP by default, which provides no acknowledgment that messages arrived.
- In a firewall policy, the Log Allowed Traffic All Sessions option logs every matching session whether or not a detection occurred, while Security Events logs only sessions that trigger a profile detection.
- Log types map to specific events: the Local traffic log records sessions to and from the FortiGate's own interfaces, the Application Control log records matched application signatures, and the IPS log records traffic that matched an attack signature.
- Event log categories such as System, VPN, and User and Device are individually enabled or disabled on the Log Settings page.

## Study tips

- Memorize the default administrative distances (connected 0, static 10, OSPF 110, BGP 20 external / 200 internal) and remember that priority is a FortiGate tiebreaker only when distances are equal.
- Know the split between per-VDOM settings (firewall policies, static routes) and global settings (admin accounts, profiles), and that enabling multi-VDOM mode requires a reboot.
- For VPN questions, keep the Phase 1 vs Phase 2 roles straight and match failure symptoms to causes: IKE version or DH/algorithm mismatch breaks Phase 1, while mismatched selector subnets break Phase 2.
- Understand the difference between certificate inspection and full (deep) SSL inspection, and that only deep inspection lets AntiVirus and IPS scan encrypted payloads.
- Learn the FGCP primary-election order (monitored interfaces, then uptime, then priority, then serial number) and how the override setting flips priority above uptime.

---

Want the full breakdown? See the complete **[Fortinet Certified Professional - FortiGate (FCP - FortiGate) study guide](https://certgrid.app/study-guide/fortinet-certified-professional-fortigate-fcp-fortigate)** and **[free practice questions](https://certgrid.app/practice/fortinet-certified-professional-fortigate-fcp-fortigate)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

