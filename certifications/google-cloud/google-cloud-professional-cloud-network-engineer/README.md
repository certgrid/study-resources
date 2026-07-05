# Google Cloud Professional Cloud Network Engineer - Study Cheatsheet

The Google Cloud Professional Cloud Network Engineer exam validates your ability to design, implement, manage, and troubleshoot Google Cloud network architectures, including VPCs, hybrid connectivity, load balancing, DNS, and network security. It is aimed at network professionals who deploy and operate GCP networks at scale, often in hybrid and multi-VPC environments. The 2-hour exam has a 700 (out of 1000) passing score and emphasizes scenario-based design trade-offs across cost, security, performance, and resilience.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | Google Cloud Professional Cloud Network Engineer |
| Credential | Google Cloud Professional Cloud Network Engineer |
| Level | Advanced |
| Practice mock length | ~50 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-06-23 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Designing and Planning a Network | ~20% |
| 2 | Implementing VPC Networks | ~21% |
| 3 | Configuring Network Services | ~22% |
| 4 | Implementing Hybrid Connectivity | ~17% |
| 5 | Managing and Monitoring Network Operations | ~20% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Designing and Planning a Network

- A VPC network is a global resource that spans all regions automatically, while subnets are regional resources whose IP range is bound to one region; VMs in any zone of a region can use that region's subnets.
- Custom-mode VPCs require you to manually create each subnet and choose its CIDR, whereas auto-mode VPCs auto-create one /20 subnet per region; production designs favor custom mode for explicit IP control.
- VPC Network Peering connects two VPCs so VMs communicate over internal RFC 1918 IPs with no external hops, but it is non-transitive and requires completely non-overlapping subnet CIDR ranges (primary and secondary).
- When CIDR ranges overlap, peering is rejected; remediate by re-IPing one VPC or by using Private Service Connect to expose only a specific service endpoint instead of the whole network.
- Shared VPC designates one host project whose subnets, firewall rules, and routes are centrally managed, while service projects deploy workloads into those shared subnets - centralizing network administration across an organization.
- Cloud Interconnect (Dedicated or Partner) and Cloud VPN are the two hybrid connectivity options; Interconnect provides a private physical link (10/100 Gbps for Dedicated) that never traverses the public internet.

### Domain 2 - Implementing VPC Networks

- Private Google Access is a per-subnet flag that lets VMs without external IPs reach Google APIs and services (Cloud Storage, BigQuery, Pub/Sub) over internal IPs via Google's network.
- Cloud NAT is a managed, distributed (non-instance-based) service that gives VMs without external IPs outbound internet access by translating internal IPs to a pool of NAT IPs; it allows no unsolicited inbound connections.
- A new custom VPC has two implied rules that cannot be deleted: implied deny-all ingress and implied allow-all egress; you add higher-priority rules to override them.
- VPC firewall rules can target by network tag or service account in addition to IP range; service-account-based rules follow the VM's identity even when its IP changes, making them robust in dynamic fleets.
- GCP has two firewall constructs: VPC firewall rules (per-network) and hierarchical firewall policies (applied at the organization or folder level for centralized governance).
- Cloud NAT port exhaustion is fixed by increasing minimum ports per VM and/or adding more NAT IP addresses; each NAT IP provides about 64,512 usable source ports per destination.

### Domain 3 - Configuring Network Services

- The global external Application Load Balancer (HTTP/S) operates at Layer 7, uses a single anycast IP advertised from Google's global edge PoPs, and routes by URL map (host/path) for globally distributed apps.
- The internal passthrough Network Load Balancer keeps TCP/UDP traffic private within a region at Layer 4, does not proxy, and preserves the client source IP.
- The external passthrough Network Load Balancer (Layer 4) preserves original client source IP and supports non-HTTP protocols, unlike the proxying Application Load Balancer.
- Cloud CDN integrates with the external Application Load Balancer and caches HTTP(S) responses at Google edge PoPs; subsequent hits are served from the nearest edge, reducing latency and origin egress.
- Cloud CDN cache modes: USE_ORIGIN_HEADERS respects Cache-Control, CACHE_ALL_STATIC caches static content by default, and FORCE_CACHE_ALL caches all responses regardless of origin headers (use carefully).
- Reduce CDN origin egress by enabling negative caching for error responses, setting longer TTLs for static content, using request coalescing, and excluding unnecessary cookies and query parameters from the cache key.

### Domain 4 - Implementing Hybrid Connectivity

- Cloud Router uses BGP as its only dynamic routing protocol to exchange routes with on-prem peers over HA VPN tunnels or Interconnect VLAN attachments, auto-advertising new VPC subnets and learning remote prefixes.
- HA VPN provides a 99.99% SLA using two gateway interfaces, each with its own external IP, establishing redundant IPsec tunnels; it requires a Cloud Router with a BGP session and does not support static routing.
- Dedicated Interconnect is a direct physical 10/100 Gbps connection at a Google peering facility with no public internet traversal; Partner Interconnect connects through a service provider for smaller (50 Mbps-50 Gbps) capacities.
- For resilience, deploy redundant connections across two separate metro edge availability domains with redundant Cloud Routers, and optionally use HA VPN as a backup path to Interconnect.
- Path preference between Interconnect and VPN is controlled with BGP attributes via Cloud Router: advertise the preferred (Interconnect) path with higher priority / lower MED so it wins over the VPN path.
- ECMP (equal-cost multipath) over BGP on Cloud Router across multiple Interconnect attachments with equal priorities load-balances traffic and increases aggregate throughput.

### Domain 5 - Managing and Monitoring Network Operations

- VPC Flow Logs record sampled metadata (5-tuple source/destination IP and port, protocol, bytes, packets, and allowed/denied disposition) per VM, GKE node, and Cloud VPN tunnel network interface.
- Flow Logs export to Cloud Logging and can be sinked to BigQuery for SQL analysis to identify which subnets and VMs generate the most egress, or detect traffic anomalies.
- Network Intelligence Center's Connectivity Tests run a configuration-based simulated trace (analyzing routes, firewall rules, peering, and LB config) without sending real packets, ideal for pinpointing why connectivity fails.
- Network Intelligence Center centralizes Topology, Connectivity Tests, Performance Dashboard, Firewall Insights, and Network Analyzer for diagnostics and optimization.
- The Performance Dashboard in Network Intelligence Center surfaces packet loss and latency between Google Cloud zones/regions and between your VMs, helping isolate performance issues.
- When Flow Logs show blocked traffic, the responsible rule is in the VPC firewall rules or a hierarchical firewall policy; review rules applied to the VM's tags or service account and confirm with a Connectivity Test.

## Study tips

- Read each scenario for the deciding constraint - cost, security, latency/performance, or resilience - because most answer choices are technically valid and only one optimizes the stated priority.
- Memorize the load balancer decision tree: global vs regional, external vs internal, Layer 7 proxy (Application LB) vs Layer 4 passthrough (Network LB), and which preserve the client source IP.
- Know the hybrid connectivity matrix cold: HA VPN (99.99% SLA, IPsec, BGP required) vs Dedicated vs Partner Interconnect, and how Cloud Router BGP priority/MED chooses the active path.
- For routing and firewall questions, remember the rule: lower priority number wins, the first match applies, and a custom VPC defaults to deny-all ingress and allow-all egress.
- When a question is about diagnosis, map the symptom to the right tool: Connectivity Tests for config/path failures, VPC Flow Logs for traffic volume and allowed/denied data, and Performance Dashboard for latency and packet loss.

---

Want the full breakdown? See the complete **[Google Cloud Professional Cloud Network Engineer study guide](https://certgrid.app/study-guide/google-cloud-professional-cloud-network-engineer)** and **[free practice questions](https://certgrid.app/practice/google-cloud-professional-cloud-network-engineer)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

