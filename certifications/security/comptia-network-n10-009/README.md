# CompTIA Network+ (N10-009) - Study Cheatsheet

CompTIA Network+ (N10-009) validates the core skills needed to design, implement, operate, secure, and troubleshoot wired and wireless networks. It is a vendor-neutral, early-career certification aimed at network technicians, help-desk staff, and junior administrators who need to prove foundational networking competence. The 90-minute exam has up to ~90 questions (multiple-choice plus performance-based), and you must score 720 on a 100-900 scale to pass.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | CompTIA Network+ (N10-009) |
| Credential | CompTIA Network+ (N10-009) |
| Level | Intermediate |
| Practice mock length | ~90 questions |
| Duration | ~90 minutes |
| Passing score | 800 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Networking Concepts | ~16% |
| 2 | Network Implementation | ~17% |
| 3 | Network Operations | ~31% |
| 4 | Network Security | ~20% |
| 5 | Network Troubleshooting | ~16% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Networking Concepts

- The OSI model has 7 layers: Physical (1), Data Link (2), Network (3), Transport (4), Session (5), Presentation (6), and Application (7). Layer 3 (IP) handles logical addressing and routing; Layer 2 (MAC) handles local frame delivery; Layer 6 (Presentation) handles encryption, encoding, and format translation.
- TCP is connection-oriented and reliable, using a three-way handshake (SYN, SYN-ACK, ACK), sequence numbers, acknowledgements, retransmission, and a sliding window for flow control. UDP is connectionless, best-effort, has no flow control, and has lower overhead - preferred for VoIP, streaming, and DNS queries.
- Memorize well-known ports: FTP 20/21 (data/control), SSH/SFTP 22, Telnet 23, SMTP 25, DNS 53, DHCP 67/68, TFTP 69, HTTP 80, NTP 123, HTTPS 443, SNMP 161/162, RDP 3389, and SMB 445.
- DHCP leases addressing via the DORA process: Discover, Offer, Request, Acknowledge. A DHCP scope assigns IP address, subnet mask, default gateway, and DNS servers; DHCP relay (ip helper-address) forwards requests across subnets.
- DNS resolves hostnames to IP addresses. Record types: A (IPv4), AAAA (IPv6), CNAME (alias), MX (mail), PTR (reverse lookup), TXT (SPF/DKIM), NS (name server), SOA (zone authority). DoH (DNS over HTTPS) and DoT (DNS over TLS) encrypt DNS queries.
- NAT lets many internal private hosts share public IPs. PAT (NAT overload) maps many hosts to one public IP using different source ports; static NAT is a fixed one-to-one private-to-public mapping.

### Domain 2 - Network Implementation

- A Layer 2 switch forwards frames using destination MAC addresses stored in its CAM/MAC address table; an unknown destination is flooded out all ports. A router (Layer 3) forwards packets between different IP networks using the routing table and destination IP.
- VLANs logically segment one physical switch into multiple broadcast domains, improving security/policy separation and containing broadcast traffic. Inter-VLAN traffic requires a router or Layer 3 switch.
- A trunk port carries multiple VLANs with 802.1Q tags; an access port carries a single untagged VLAN. The native VLAN on a trunk is sent untagged - mismatched native VLANs cause connectivity and security issues.
- Example Cisco VLAN/access config: 'interface gi0/1', 'switchport mode access', 'switchport access vlan 20'. Trunk config: 'switchport mode trunk', 'switchport trunk allowed vlan 10,20'. Create a VLAN: 'vlan 50', 'name ENGINEERING'.
- A default static route is 'ip route 0.0.0.0 0.0.0.0 203.0.113.1' (next hop). OSPF example: 'router ospf 1', 'network 10.0.0.0 0.0.0.255 area 0'. Linux IP assignment: 'ip addr add 192.168.1.10/24 dev ens33'.
- PoE delivers electrical power to devices (APs, IP phones, cameras) over the Ethernet cable. 802.3af provides ~15.4W, 802.3at (PoE+) ~30W, and 802.3bt (PoE++) up to ~90-100W at the port.

### Domain 3 - Network Operations

- The default gateway is the router interface IP on the host's local subnet; the host sends all off-subnet traffic to it. Verify with the host's routing table and a ping to the gateway.
- SNMP monitors and manages devices: the NMS polls agents with GET on UDP 161 to read MIB values (interface utilization, errors, CPU, memory); agents push trap alerts to the manager on UDP 162. SNMPv3 adds authentication, integrity, and encryption.
- QoS classifies and prioritizes traffic to control bandwidth, latency, jitter, and loss. VoIP is marked DSCP EF (Expedited Forwarding, value 46) and placed in a priority/Low-Latency Queue (LLQ) so it meets strict latency needs.
- Traffic shaping buffers and smooths bursts to a defined rate (delays excess); traffic policing drops or remarks traffic exceeding the rate. Shaping flattens peaks; policing enforces hard limits.
- High availability eliminates single points of failure: first-hop redundancy (HSRP/VRRP/GLBP) provides a shared virtual gateway IP for failover, plus redundant links/paths (with STP or link aggregation) and backup power (UPS/generator).
- Dynamic routing protocols (OSPF, EIGRP, BGP, RIP) automatically adapt to topology changes and failures. Path selection uses administrative distance (which protocol to trust) then the protocol metric (cost/hop count).

### Domain 4 - Network Security

- A firewall enforces an allow/deny rule set on traffic between zones based on source/destination IP, protocol, port, and connection state. Stateful firewalls track TCP session state and permit return traffic; an implicit deny-all sits at the end of rule lists.
- A next-generation firewall (NGFW) adds application awareness, integrated IPS, and deep packet inspection (DPI). A UTM appliance consolidates firewall, IPS, antivirus, content filtering, and VPN into one device.
- IDS detects and alerts on malicious traffic out-of-band; IPS sits inline and can actively block. Both use signature-based and anomaly/behavior-based detection.
- A VPN creates an encrypted tunnel over an untrusted network. Site-to-site VPNs (typically IPsec) connect whole networks/locations; remote-access VPNs connect individual users. SSL/TLS VPNs can offer clientless access to published applications.
- IPsec provides confidentiality, integrity, and authentication using AH and ESP, operating in transport or tunnel mode; IKE negotiates the security association and keys.
- 802.1X is port-based network access control: a supplicant authenticates to an authenticator (switch/AP) which checks credentials against a RADIUS server before opening the port. EAP carries the authentication.

### Domain 5 - Network Troubleshooting

- Follow the CompTIA 7-step methodology in order: 1) Identify the problem (gather info), 2) Establish a theory of probable cause, 3) Test the theory, 4) Establish a plan of action, 5) Implement the solution, 6) Verify full functionality and apply preventive measures, 7) Document findings, actions, and outcomes.
- ping uses ICMP Echo to test Layer 3 reachability, loss, and round-trip time. traceroute (Unix)/tracert (Windows) maps each hop by incrementing TTL and reading ICMP Time Exceeded replies; pathping/mtr combine both to show per-hop loss.
- nslookup and dig query DNS - target a specific server and request record types (e.g., 'dig @8.8.8.8 example.com MX') to verify name resolution. ipconfig /all (Windows) and ip addr (Linux) show host addressing.
- Renew DHCP on Linux with 'dhclient -r eth0 && dhclient eth0' (Windows: ipconfig /release then /renew). A host stuck on a 169.254.x.x APIPA address indicates the DHCP server is unreachable.
- A packet analyzer (Wireshark/tcpdump) captures and inspects frames to confirm exactly where traffic is dropped, see retransmissions, and validate protocol behavior. Flow logs and NetFlow show traffic volumes per conversation.
- A duplex/speed mismatch (one side full-duplex, other half-duplex) causes late collisions, CRC/FCS errors, and slow throughput - check interface counters on both ends and prefer matching fixed settings or auto on both.

## Study tips

- Master subnetting cold - practice converting between CIDR, dotted-decimal masks, host counts, and network/broadcast addresses until you can do it in your head, since the exam includes multiple subnetting and address-range questions plus performance-based items.
- Memorize the well-known ports and protocols table (FTP 20/21, SSH 22, DNS 53, DHCP 67/68, HTTP 80, HTTPS 443, SNMP 161/162, RDP 3389) and the OSI layers in order - these are high-frequency, easy points.
- Learn the 7-step troubleshooting methodology in exact order; questions ask which step comes next, and the first step is always to identify the problem (never to implement a fix or escalate first).
- For performance-based questions, practice reading device configs and topology diagrams - know basic Cisco/Linux commands for VLANs, trunks, access ports, static routes, ACLs, and port security.
- Watch for 'BEST' and 'MOST likely' wording: eliminate clearly wrong answers, then choose the option that directly matches the scenario's symptoms (e.g., duplex mismatch for CRC errors, MTU mismatch for jumbo-frame black-holing).

---

Want the full breakdown? See the complete **[CompTIA Network+ (N10-009) study guide](https://certgrid.app/study-guide/comptia-network-n10-009)** and **[free practice questions](https://certgrid.app/practice/comptia-network-n10-009)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

