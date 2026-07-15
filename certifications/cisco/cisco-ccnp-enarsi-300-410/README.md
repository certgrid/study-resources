# Cisco CCNP ENARSI (300-410) - Study Cheatsheet

The Cisco CCNP ENARSI (300-410) is a 90-minute, ~60-question concentration exam validating advanced enterprise routing skills: Layer 3 technologies (EIGRP, OSPF, BGP, redistribution), VPN technologies (DMVPN, MPLS Layer 3 VPN), infrastructure security, and infrastructure services. It is intended for experienced network engineers (typically 3-5 years) pursuing the CCNP Enterprise certification after passing the 350-401 ENCOR core exam.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | Cisco CCNP ENARSI (300-410) |
| Credential | Cisco CCNP ENARSI (300-410) |
| Level | Intermediate |
| Practice mock length | ~60 questions |
| Duration | ~90 minutes |
| Passing score | 825 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Layer 3 Technologies | ~31% |
| 2 | VPN Technologies | ~18% |
| 3 | Infrastructure Security | ~22% |
| 4 | Infrastructure Services | ~29% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Layer 3 Technologies

- EIGRP is Cisco's advanced distance-vector protocol that uses DUAL (Diffusing Update Algorithm) to guarantee loop-free paths and fast reconvergence via precomputed feasible successors.
- EIGRP neighbors must agree on AS number and K-values, and be on the same primary subnet; mismatched K-values or authentication prevent adjacency. The default metric uses K1 (bandwidth) and K3 (delay) only.
- The EIGRP feasibility condition requires a neighbor's reported distance (RD/advertised distance) to be less than the local feasible distance (FD); a route meeting this becomes a feasible successor (loop-free backup).
- OSPF is a link-state IGP: routers flood LSAs within an area to build an identical LSDB, then each runs Dijkstra's SPF to compute best paths. OSPFv2 uses IP protocol 89.
- OSPF requires matching area ID, subnet/mask, hello/dead timers, authentication, and stub flags to form an adjacency; the OSPF router ID must be unique.
- On broadcast/multi-access segments OSPF elects a DR/BDR (highest priority, then highest router ID); priority 0 means a router never becomes DR/BDR. The DR uses multicast 224.0.0.6.

### Domain 2 - VPN Technologies

- DMVPN provides scalable hub-and-spoke (and dynamic spoke-to-spoke) VPNs by combining multipoint GRE (mGRE), NHRP, a routing protocol, and IPsec encryption.
- NHRP (Next Hop Resolution Protocol) maps tunnel (overlay) IP addresses to physical (underlay) NBMA addresses; spokes register with the hub as the Next Hop Server (NHS) using 'ip nhrp nhs' and 'ip nhrp map'.
- The DMVPN hub uses 'tunnel mode gre multipoint' on its mGRE tunnel; spokes can use point-to-point GRE (Phase 1) or mGRE (Phase 2/3) tunnels.
- DMVPN Phase 1 forces all traffic through the hub; Phase 2 enables direct spoke-to-spoke tunnels via NHRP resolution; Phase 3 adds NHRP redirect/shortcut switching for better scalability and summarization at the hub.
- GRE alone encapsulates any protocol (including multicast and routing hellos) over IP but provides no encryption, integrity, or authentication; pairing it with IPsec adds confidentiality.
- IPsec site-to-site VPNs use IKE Phase 1 to build the bidirectional ISAKMP/IKE SA (authenticated, encrypted management channel), then IKE Phase 2 negotiates the unidirectional IPsec SAs that protect data with ESP.

### Domain 3 - Infrastructure Security

- ACLs are ordered (top-down) permit/deny lists with an implicit deny-any at the end; standard ACLs match source IP only, while extended ACLs match source/destination IP, protocol, and L4 ports.
- Order ACEs from most specific and most frequently matched first for performance; object groups let multiple ACEs reference reusable sets of addresses, ports, or services.
- Control Plane Policing (CoPP) uses the MQC (class-map, policy-map, service-policy) to classify and rate-limit traffic punted to the CPU, protecting the control plane from DoS floods and excessive management traffic.
- Apply CoPP with 'service-policy input POLICY' under 'control-plane' configuration mode; rate-limit or drop excess traffic categories such as routing-protocol, management, and undesirable packets.
- AAA with TACACS+ (TCP 49, encrypts the full packet, ideal for command authorization) or RADIUS (UDP, encrypts only the password, common for network access) centralizes authentication, authorization, and accounting.
- Use SSHv2 instead of Telnet for encrypted device management; require it on the VTY lines with 'transport input ssh' and generate an RSA key with 'crypto key generate rsa'.

### Domain 4 - Infrastructure Services

- NTP (RFC 5905) is a hierarchical clock-sync protocol over UDP 123; stratum 1 servers sync from authoritative sources (GPS/atomic) and lower devices sync downstream. Accurate time is essential for log correlation, certificates, and Kerberos.
- Configure a device as an NTP client with 'ntp server <ip>'; NTP authentication ('ntp authenticate', 'ntp authentication-key', 'ntp trusted-key') prevents spoofed time sources; using a few local stratum servers reduces WAN query cost.
- FHRPs provide default-gateway redundancy via a shared virtual IP/MAC: HSRP (Cisco-proprietary), VRRP (open standard, RFC 5798/3768), and GLBP (Cisco, load-balances across multiple active forwarders).
- HSRP elects an active router by highest priority (default 100), then highest IP; configure with 'standby 1 ip <vip>', 'standby 1 priority 110', and 'standby 1 preempt' to let a recovered higher-priority router reclaim active.
- HSRP and VRRP forward through a single active/master router (others standby), whereas GLBP uses an AVG to assign multiple AVFs so several routers forward simultaneously for true load sharing.
- The 'ip helper-address <server>' command makes a router a DHCP relay agent, converting client broadcasts into unicasts to a DHCP server on another subnet (also forwards several other UDP broadcast services by default).

## Study tips

- Expect heavy troubleshooting on this exam: practice reading 'show' and 'debug' output to diagnose broken EIGRP/OSPF adjacencies, BGP sessions stuck below Established, and redistribution loops rather than just memorizing configuration.
- Master the full BGP best-path decision list and the OSPF LSA types (1-5 and 7) cold - these are recurring high-yield topics that distinguish passing candidates.
- Build a lab (CML, EVE-NG, or GNS3) and configure DMVPN end to end, including NHRP, tunnel protection, and routing over the tunnel; verify with 'show dmvpn' and 'show crypto ipsec sa' so the moving parts stick.
- Know the exact filtering tool for each context: prefix lists with ge/le for route filtering, distribute-lists for IGP updates, route-maps for BGP attributes and PBR, and the difference between standard and extended ACLs.
- Memorize default Administrative Distances and FHRP/timer/port defaults (NTP UDP 123, BGP TCP 179, TACACS+ TCP 49, HSRP priority 100); the exam frequently hinges on a single default value.

---

Want the full breakdown? See the complete **[Cisco CCNP ENARSI (300-410) study guide](https://certgrid.app/study-guide/cisco-ccnp-enarsi-300-410)** and **[free practice questions](https://certgrid.app/practice/cisco-ccnp-enarsi-300-410)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

