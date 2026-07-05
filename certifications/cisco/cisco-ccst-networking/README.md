# Cisco CCST Networking - Study Cheatsheet

The Cisco Certified Support Technician (CCST) Networking exam is an entry-level certification validating foundational knowledge of networking standards, IP addressing and subnetting, endpoints and media, infrastructure devices, and basic security and troubleshooting. It is aimed at students, early-career IT staff, and anyone starting a networking path or preparing for CCNA. The 50-minute exam scores on a scale where 700 is passing.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | Cisco CCST Networking |
| Credential | Cisco CCST Networking |
| Level | Intermediate |
| Practice mock length | ~60 questions |
| Duration | ~50 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-06-23 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Standards and Concepts | ~16% |
| 2 | Addressing and Subnet Formats | ~17% |
| 3 | Endpoints and Media Types | ~13% |
| 4 | Infrastructure and Connectivity | ~24% |
| 5 | Security and Diagnostics | ~29% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Standards and Concepts

- The OSI model has 7 layers: Physical (1), Data Link (2), Network (3), Transport (4), Session (5), Presentation (6), Application (7). The TCP/IP model collapses these into 4: Link, Internet, Transport, and Application.
- Layer 3 (Network) handles logical addressing and routing; IP lives here and routers forward packets by examining destination IP and consulting a routing table.
- Layer 2 (Data Link) uses MAC addresses and switches; Layer 4 (Transport) uses TCP and UDP with port numbers to identify applications.
- TCP is connection-oriented and reliable: it uses a three-way handshake (SYN, SYN-ACK, ACK), sequence numbers for ordering, acknowledgments, and retransmission of lost segments.
- UDP is connectionless and low-overhead with no handshake, ordering, or retransmission; it favors timeliness over reliability and suits VoIP, video, DNS queries, and gaming.
- Well-known ports to memorize: SSH 22, Telnet 23, DNS 53, HTTP 80, HTTPS 443, FTP 20/21, SMTP 25, SNMP 161/162, NTP 123, DHCP 67/68.

### Domain 2 - Addressing and Subnet Formats

- RFC 1918 private IPv4 ranges are 10.0.0.0/8, 172.16.0.0/12 (172.16.0.0-172.31.255.255), and 192.168.0.0/16; these are not routable on the public internet.
- CIDR prefix length equals the number of network bits; usable hosts per subnet equal 2^(host bits) minus 2 for the network and broadcast addresses.
- A /24 (255.255.255.0) has 256 total addresses and 254 usable hosts; a /26 (255.255.255.192) has 64 total and 62 usable hosts per subnet.
- For a /26, subnets begin at .0, .64, .128, .192; the second subnet's usable host range is 192.168.1.65 through 192.168.1.126 with .127 as the broadcast.
- The network address has all host bits set to 0 and the broadcast address has all host bits set to 1; neither is assignable to a host.
- DHCP automatically assigns IP address, subnet mask, default gateway, and DNS server, eliminating manual configuration and reducing errors.

### Domain 3 - Endpoints and Media Types

- A MAC address is a 48-bit (6-octet) Layer 2 hardware address written in hexadecimal that uniquely identifies a network interface within a broadcast domain.
- Wi-Fi is defined by the IEEE 802.11 standard family; amendments a/b/g/n/ac/ax add speed and features such as MIMO and OFDMA.
- The 2.4 GHz band has longer range and better obstacle penetration but only 3 non-overlapping channels (1, 6, 11), so it congests easily in dense areas.
- The 5 GHz band offers more non-overlapping channels and higher throughput at the cost of shorter range and weaker wall penetration.
- To increase per-client throughput in a crowded WLAN, deploy more APs with smaller cells, lower transmit power, and non-overlapping channels.
- Twisted-pair copper (Cat5e/Cat6/Cat6a) is the standard LAN medium; the maximum run for 1000BASE-T and 10GBASE-T is 100 meters.

### Domain 4 - Infrastructure and Connectivity

- A switch is a Layer 2 device that forwards frames by destination MAC address, learns MACs into a CAM table, and creates a separate collision domain per port.
- A router is a Layer 3 device that forwards packets by destination IP, connects different IP networks, serves as the default gateway, and can perform NAT and filtering.
- A VLAN logically segments one physical switch into multiple independent Layer 2 broadcast domains; inter-VLAN traffic must be routed at Layer 3.
- An access port belongs to a single VLAN; configure it with 'switchport mode access' and 'switchport access vlan <id>'.
- A trunk port carries multiple VLANs over one link using IEEE 802.1Q tagging, which inserts a 4-byte VLAN tag into each frame.
- A wireless access point broadcasts an SSID for clients to join and bridges wireless traffic onto the wired network.

### Domain 5 - Security and Diagnostics

- ping sends ICMP Echo Requests and reports round-trip time and packet loss; it is the first tool for verifying basic Layer 3 reachability.
- traceroute (Linux/macOS) and tracert (Windows) reveal each router hop by incrementing TTL and reading the ICMP Time Exceeded replies, exposing where a path breaks.
- If a host can ping IP addresses but not hostnames, the IP path works and the fault is DNS: missing, wrong, or unreachable DNS server.
- ipconfig (Windows) and ifconfig / 'ip addr show' (Linux) display IP address, mask, gateway, and DNS; nslookup and dig test DNS resolution.
- ARP maps a known IPv4 address to a MAC address on the local segment; 'arp -a' (Windows) or 'ip neigh show' (Linux) displays the neighbor cache.
- A structured troubleshooting process starts with identifying the problem and gathering information (link LEDs, IP config, scope) before changing anything.

## Study tips

- Memorize the OSI layers in order plus which device and protocol live at each layer (switch/MAC at L2, router/IP at L3, TCP-UDP/ports at L4) - many questions hinge on this mapping.
- Drill subnetting until you can find network address, broadcast, usable range, and host count for /24 through /30 from memory; practice both /26 and /27 boundaries.
- Know standard port numbers cold (22, 23, 53, 80, 443, 123, 161/162, 67/68) and which use TCP vs UDP.
- For troubleshooting questions, follow the structured order: identify and gather information first, then test from the bottom of the stack up (cable/link, IP config, gateway, DNS).
- Read scenario questions for the deciding constraint - distance, EMI immunity, cost, or interference - which usually points directly to fiber vs copper, or 2.4 GHz vs 5 GHz.

---

Want the full breakdown? See the complete **[Cisco CCST Networking study guide](https://certgrid.app/study-guide/cisco-ccst-networking)** and **[free practice questions](https://certgrid.app/practice/cisco-ccst-networking)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

