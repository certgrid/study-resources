# Palo Alto Networks Certified Next-Generation Firewall Engineer (NGFW-Engineer) - Study Cheatsheet

The Palo Alto Networks Certified Next-Generation Firewall Engineer (NGFW-Engineer) validates experienced engineers who deploy and operate PAN-OS next-generation firewalls in production. It targets network and security professionals responsible for interface, routing, and HA configuration, device-level settings such as authentication, certificates, User-ID, and decryption, plus Panorama, API, and automation workflows. The 90-minute exam has roughly 769 questions in its pool, uses a scaled passing score of 700, and assumes hands-on familiarity with real PAN-OS configuration rather than memorized theory.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | Palo Alto Networks Certified Next-Generation Firewall Engineer (NGFW-Engineer) |
| Credential | Palo Alto Networks Certified Next-Generation Firewall Engineer (NGFW-Engineer) |
| Level | Intermediate |
| Practice mock length | ~75 questions |
| Duration | ~90 minutes |
| Passing score | 700 out of 1000 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | PAN-OS Networking Configuration | ~40% |
| 2 | PAN-OS Device Setting Configuration | ~40% |
| 3 | Integration and Automation | ~20% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - PAN-OS Networking Configuration

- A Layer3 interface participates in policy and routing only when it is assigned both a security zone and a virtual router; missing either breaks matching or forwarding.
- In BGP best-path selection, once all higher attributes tie, the path from the router with the lowest router ID wins, and the router ID also uniquely identifies the BGP speaker.
- AS-path prepending artificially lengthens the AS-path so neighboring autonomous systems are less likely to prefer that route, steering inbound traffic to a shorter alternate path.
- PAN-OS conditional advertisement with a non-exist filter advertises a backup route only when a monitored (tracked) route is absent from the routing table, enabling failover advertising.
- OSPF adjacency on broadcast links fails when interface subnet masks disagree, because mismatched masks put the neighbors on different logical subnets; Exstart is where neighbors negotiate master/slave before exchanging DBD packets.
- Manually setting the OSPF or BGP router ID gives stability that automatic address-based selection does not guarantee, and OSPF graceful restart lets a restarting router keep its learned routes valid during the outage.

### Domain 2 - PAN-OS Device Setting Configuration

- An authentication profile defines how credentials are verified (Local, RADIUS, TACACS+, LDAP, Kerberos, or SAML), while an authentication sequence tries each listed profile in order until one succeeds.
- Generating a certificate creates a new key pair and certificate locally on the firewall, whereas importing brings in an externally produced certificate and optionally its key pair; OCSP checks revocation with a real-time query for one specific certificate.
- WebUI HTTPS access is secured by an SSL/TLS certificate assigned to the management interface, and client-certificate authentication for the WebUI is enabled by applying a certificate profile in the management authentication settings.
- Without Terminal Services (TS) agent port mapping, every session on a shared Remote Desktop Services host appears to the firewall as one source IP, so User-ID cannot distinguish individual users.
- DNS Proxy rules are evaluated top-down and the first matching domain rule handles the query; static FQDN-to-IP entries are answered directly and take precedence over cached or forwarded records.
- DNS Security categories accept actions of alert, allow, block, or sinkhole, where sinkhole substitutes a controlled IP for the resolution instead of blocking the query outright.

### Domain 3 - Integration and Automation

- Firewalls are added to Panorama by serial number on the Managed Devices page, after which each firewall or vsys is assigned to exactly one device group plus templates and a Collector Group.
- Templates and template stacks centrally manage network and device settings (interfaces, zones, virtual routers), while device groups manage policy and objects; a rule in the Shared location applies to every device group in the hierarchy.
- Moving a device group to a new parent changes which parent-level rules and objects its firewalls inherit, so hierarchy placement directly drives rule inheritance.
- A commit that is not scoped by an admin or location filter can also include other administrators' pending candidate changes, which is why partial or filtered commits matter in multi-admin environments.
- init-cfg.txt in a bootstrap package supplies day-0 settings such as hostname, IP, gateway, DNS, and the Panorama server address that a VM-Series firewall reads on first boot; full day-1 policy lives in bundle files.
- Panorama supports active/passive HA between two management servers, synchronizing device groups, templates, and managed-device information between peers, with one peer active and the other ready to take over.

## Study tips

- Treat every question as a hands-on config scenario: know the exact GUI path and object dependencies (zone plus virtual router on an interface, certificate profile in management settings) rather than just the concept name.
- Memorize the low-value-wins conventions that trip candidates up: lowest router ID wins BGP ties, lower LACP system priority means higher priority, and OSPF mask mismatches block adjacency.
- Be able to distinguish look-alike actions and objects quickly: generate vs import certificates, sinkhole vs block in DNS Security, tap (passive) vs virtual wire (inline) zones, and static vs forwarded DNS Proxy entries.
- For Panorama and automation items, keep the hierarchy straight: templates carry network/device settings, device groups carry policy/objects, Shared applies everywhere, and each firewall or vsys maps to exactly one device group.
- The exam is 90 minutes for a large pool, so pace yourself and flag configuration edge cases (multi-admin commits, HA link roles, User-ID on shared hosts) for review instead of stalling.

---

Want the full breakdown? See the complete **[Palo Alto Networks Certified Next-Generation Firewall Engineer (NGFW-Engineer) study guide](https://certgrid.app/study-guide/palo-alto-networks-certified-next-generation-firewall-engineer-ngfw-engineer)** and **[free practice questions](https://certgrid.app/practice/palo-alto-networks-certified-next-generation-firewall-engineer-ngfw-engineer)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

