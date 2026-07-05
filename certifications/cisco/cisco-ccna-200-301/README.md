# Cisco CCNA 200-301 - Study Cheatsheet

The Cisco CCNA 200-301 is a single, associate-level exam that validates your ability to install, configure, operate, and troubleshoot small-to-medium enterprise networks. It covers six domains - network fundamentals, network access, IP connectivity, IP services, security fundamentals, and automation - and is aimed at entry-level network engineers and technicians. The exam runs 120 minutes, requires a scaled score of roughly 825/1000 to pass, and mixes multiple-choice, drag-and-drop, and simulation-style items.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | Cisco CCNA 200-301 |
| Credential | Cisco CCNA 200-301 |
| Level | Intermediate |
| Practice mock length | ~100 questions |
| Duration | ~120 minutes |
| Passing score | 825 out of 1000 |
| Notes reviewed | 2026-06-23 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Network Fundamentals | ~23% |
| 2 | Network Access | ~21% |
| 3 | IP Connectivity | ~14% |
| 4 | IP Services | ~16% |
| 5 | Security Fundamentals | ~13% |
| 6 | Automation and Programmability | ~13% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Network Fundamentals

- The OSI model has seven layers; Layer 1 (Physical) moves bits, Layer 2 (Data Link) uses MAC addresses and switches, Layer 3 (Network) uses IP addresses and routers, and Layer 4 (Transport) uses TCP/UDP port numbers.
- TCP is connection-oriented and reliable: it uses a three-way handshake (SYN, SYN-ACK, ACK), sequence/acknowledgment numbers, and a sliding window for flow control. UDP is connectionless, best-effort, low-overhead, and used for DNS, VoIP, and streaming.
- Switches operate at Layer 2, forward frames by MAC address, and create separate collision domains per port but a single broadcast domain (per VLAN). Routers operate at Layer 3 and separate broadcast domains.
- ARP resolves a known IPv4 address to an unknown MAC address on the local segment; the request is a broadcast and the reply is a unicast.
- A /24 yields 254 usable hosts, a /23 (255.255.254.0) yields 510 usable hosts, and a /26 yields 62 usable hosts. Usable hosts = 2^(host bits) - 2.
- RFC 1918 private ranges are 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16. The 169.254.0.0/16 range is APIPA, auto-assigned when a DHCP server cannot be reached.

### Domain 2 - Network Access

- An access port belongs to a single VLAN; 'switchport mode access' then 'switchport access vlan 20' assigns it. The VLAN is auto-created in the database if it does not already exist.
- A trunk port carries multiple VLANs using IEEE 802.1Q tagging, which inserts a 4-byte tag into each frame. 'switchport trunk allowed vlan 10,20,30' restricts which VLANs cross the trunk.
- The native VLAN (default VLAN 1) is sent untagged across an 802.1Q trunk; the native VLAN must match on both ends or a mismatch is flagged.
- STP (IEEE 802.1D) prevents Layer 2 loops by blocking redundant paths; without it, broadcast storms, MAC table instability, and duplicate frames occur.
- The root bridge is the switch with the lowest bridge ID (bridge priority + MAC address). Default priority is 32768; the lowest bridge ID wins, and ties break on the lowest MAC.
- 802.1D STP port states are blocking, listening, learning, and forwarding (plus disabled). Rapid PVST+ (802.1w) port roles include root, designated, alternate (backup path to root), and backup.

### Domain 3 - IP Connectivity

- Administrative distance ranks route trustworthiness when multiple sources offer the same prefix: connected = 0, static = 1, eBGP = 20, EIGRP = 90, OSPF = 110, RIP = 120, external EIGRP = 170, iBGP = 200. Lowest AD wins.
- When routes tie on AD, the router compares the metric within that protocol; the longest prefix match always wins over AD when prefixes differ in length.
- OSPF is a link-state protocol that floods LSAs to build an LSDB and runs the Dijkstra SPF algorithm to compute a loop-free shortest-path tree. Default OSPF cost = 100 Mbps / interface bandwidth.
- OSPF neighbors must agree on area ID, subnet/mask on the connecting interface, Hello and Dead timers, authentication, and MTU before they form an adjacency.
- All OSPF areas must connect to the backbone Area 0. An Area Border Router (ABR) has interfaces in Area 0 and at least one other area and generates Type 3 summary LSAs between them.
- OSPF uses Hello packets to discover and maintain neighbors; the default Hello is 10 seconds and the Dead interval is 40 seconds on broadcast/point-to-point links.

### Domain 4 - IP Services

- Static NAT maps one private address to one public address; dynamic NAT maps from a pool; PAT (NAT overload) maps many private addresses to one public IP by tracking unique source port numbers.
- 'show ip nat translations' lists active NAT/PAT entries; 'ip nat inside'/'ip nat outside' mark the interfaces and the direction of translation.
- DHCP uses the DORA sequence: Discover (client broadcast), Offer (server), Request (client broadcast), Acknowledge (server). The client starts with no IP, so initial messages are broadcasts.
- 'ip helper-address <server>' on the client-facing interface relays DHCP (and a few other UDP broadcasts) across subnets as unicast, since routers do not forward broadcasts by default. DHCP uses UDP ports 67 (server) and 68 (client).
- DNS resolves hostnames to IP addresses using UDP port 53 for normal queries; it switches to TCP port 53 for zone transfers or responses larger than 512 bytes.
- NTP synchronizes clocks; stratum 0 is the reference hardware clock, stratum 1 is directly attached to it, and higher numbers are farther away. 'ntp server <ip>' sets a sync source; 'show ntp associations' shows peers.

### Domain 5 - Security Fundamentals

- Standard ACLs (1-99, 1300-1999) match only the source IP and are placed close to the destination to avoid blocking unintended traffic. Extended ACLs (100-199, 2000-2699) match source, destination, protocol, and ports and are placed close to the source.
- ACLs are processed top-down, first match wins, and there is an implicit 'deny any' at the end; wildcard masks are inverse subnet masks (0 = must match, 255 = ignore).
- AAA stands for Authentication (who you are), Authorization (what you can do), and Accounting (what you did). RADIUS and TACACS+ are the centralized AAA servers.
- TACACS+ (Cisco, TCP port 49) encrypts the entire packet and separates the three AAA functions. RADIUS (standard, UDP 1812/1813 or 1645/1646) encrypts only the password and combines authentication with authorization.
- Port security limits MAC addresses per port. Violation modes: protect (silently drops, no log/counter), restrict (drops, logs, increments counter), and shutdown (err-disables the port - the default). 'switchport port-security maximum 3' caps the count.
- Layer 2 attack mitigation: BPDU Guard disables PortFast edge ports that receive a BPDU, DHCP Snooping stops rogue DHCP servers, and Dynamic ARP Inspection (DAI) validates ARP to stop ARP spoofing/poisoning man-in-the-middle attacks.

### Domain 6 - Automation and Programmability

- Software-Defined Networking (SDN) separates the control plane from the data (forwarding) plane and centralizes control logic, exposing it through APIs for programmability.
- Controller APIs are described by direction: northbound APIs (typically REST) face applications/automation tools, while southbound APIs (NETCONF, OpenFlow) push configuration to the network devices.
- Cisco DNA Center (Catalyst Center) is Cisco's intent-based networking controller for automation, assurance, and policy; it exposes northbound REST APIs to translate business intent into network policy.
- REST APIs are stateless and use standard HTTP methods: GET (read), POST (create), PUT (replace an entire resource), PATCH (partial update), and DELETE (remove).
- HTTP status codes: 200 OK, 201 Created (successful POST), 400 Bad Request, 401 Unauthorized (authentication required), 403 Forbidden, 404 Not Found, 500 Server Error.
- JSON uses key-value pairs in curly braces {} for objects and square brackets [] for arrays; it is lightweight, human-readable, and the most common REST payload format.

## Study tips

- Memorize the number tables cold: administrative distances, common TCP/UDP port numbers, default timers (OSPF Hello 10 / Dead 40, HSRP priority 100), and subnetting host counts - these appear in many questions and free up time.
- Practice subnetting until you can find network address, broadcast, usable range, and the most efficient mask in under 30 seconds without a calculator; it underpins multiple domains.
- On simulation (sim) and configuration questions, verify your work with show commands (show ip interface brief, show running-config, show vlan brief, show ip route) the way you would on a real device.
- Read every word of ACL, NAT, and STP questions carefully - direction (inbound/outbound, inside/outside), placement (source vs destination), and the implicit deny change the correct answer.
- You cannot move backward in the CCNA exam, so do not leave questions blank; there is no penalty for guessing - eliminate wrong options and commit before moving on.

---

Want the full breakdown? See the complete **[Cisco CCNA 200-301 study guide](https://certgrid.app/study-guide/cisco-ccna-200-301)** and **[free practice questions](https://certgrid.app/practice/cisco-ccna-200-301)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

