# AZ-700: Azure Network Engineer Associate - Study Cheatsheet

The AZ-700 Azure Network Engineer Associate exam validates your ability to design, implement, and manage Azure networking solutions, spanning hybrid connectivity, core VNet infrastructure, routing, network security, and private access to PaaS services. It is aimed at network engineers who plan and operate Azure networks and work alongside architects, security pros, and cloud admins. Expect scenario-based questions on VPN/ExpressRoute, VNet design, UDRs and BGP, NSGs and Azure Firewall, and Private Link/private endpoints.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | AZ-700 |
| Credential | AZ-700: Azure Network Engineer Associate |
| Level | Associate |
| Practice mock length | ~50 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-06-24 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Design, Implement, and Manage Hybrid Networking | ~21% |
| 2 | Design and Implement Core Networking Infrastructure | ~20% |
| 3 | Design and Implement Routing | ~20% |
| 4 | Secure and Monitor Networks | ~18% |
| 5 | Design and Implement Private Access to Azure Services | ~21% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Design, Implement, and Manage Hybrid Networking

- Azure VPN Gateway SKUs scale by aggregate throughput: VpnGw1 up to 650 Mbps, VpnGw2 up to 1 Gbps, VpnGw3 up to 1.25 Gbps (Generation 1); choose the smallest SKU that meets the requirement.
- A VPN Gateway requires a dedicated subnet named exactly GatewaySubnet (recommended /27 or larger) plus a public IP address.
- Active-active VPN Gateway provisions two gateway instances, each with its own public IP and IPsec tunnel, giving redundancy and higher aggregate throughput with no failover delay; this requires two public IP addresses.
- ExpressRoute provides a dedicated private connection that bypasses the public internet, offering consistent latency and bandwidth; peering (private and Microsoft) is established at the provider edge.
- ExpressRoute FastPath bypasses the ExpressRoute gateway in the data path, reducing latency and improving performance for traffic to VMs in the VNet.
- ExpressRoute Global Reach connects two on-premises sites to each other through the Microsoft backbone (site-to-site via ExpressRoute circuits).

### Domain 2 - Design and Implement Core Networking Infrastructure

- Azure reserves 5 addresses in every subnet (network address, default gateway, two for Azure DNS mapping, broadcast), so a /24 yields 251 usable and a /23 yields 507 usable addresses.
- A /21 CIDR provides 2,048 total addresses (2,043 usable after Azure reserves 5), the smallest block that meets a 2,000-host requirement.
- VNet peering automatically updates route tables in both VNets for layer-3 connectivity; no additional routing configuration is needed, but NSGs still apply.
- VNet peering is non-transitive: VNet-A peered to B and B peered to C does not allow A-to-C; you need a direct peering or a transit gateway/NVA (hub-and-spoke).
- Global VNet peering connects VNets across Azure regions with private-IP, full-bandwidth connectivity over the Microsoft backbone.
- For spoke VMs to reach on-premises via the hub gateway, enable 'Allow gateway transit' on the hub-side peering and 'Use remote gateways' on the spoke-side peering.

### Domain 3 - Design and Implement Routing

- A user-defined route (UDR) with next hop set to an NVA's private IP forces subnet traffic through the appliance; UDRs are the primary mechanism to steer traffic.
- An NVA must have IP forwarding enabled on its Azure NIC to forward (route) packets between subnets or networks.
- Azure route selection is longest-prefix-match first; when prefix lengths tie, priority is UDR > BGP > system routes.
- A 0.0.0.0/0 UDR pointing to an NVA sends all traffic leaving the subnet (including internet-bound) to the NVA unless a more specific route exists.
- If a UDR next hop points to a virtual appliance that is unavailable or to a target that cannot deliver, the traffic is dropped silently.
- To force internet egress through Azure Firewall, associate a route table with a 0.0.0.0/0 route whose next hop is the firewall's private IP.

### Domain 4 - Secure and Monitor Networks

- NSGs are applied at the subnet or NIC level; to allow inbound HTTP, create an allow rule for TCP port 80 with source set to the Internet service tag.
- Azure Firewall must be deployed in a dedicated subnet named exactly AzureFirewallSubnet, with a recommended minimum size of /26 to allow autoscale.
- Azure Firewall rule processing order is DNAT rules first, then network rules, then application rules.
- Azure Firewall application rules filter outbound traffic by target FQDN; network rules handle layer-4 IP/port; NAT rules provide inbound DNAT.
- Azure Firewall Premium supports TLS inspection for outbound traffic, allowing the firewall to decrypt and inspect HTTPS payloads.
- Azure Web Application Firewall (WAF) operates at layer 7 to protect web apps from OWASP Top 10 threats like SQL injection and XSS, integrated with Application Gateway or Front Door.

### Domain 5 - Design and Implement Private Access to Azure Services

- A private endpoint projects a PaaS service into your VNet as a NIC with a private IP, so traffic to services like Azure SQL or storage stays off the public internet.
- Service endpoints keep traffic on the Azure backbone and present the subnet/VNet identity to the service's firewall, but the service is still reached over its public endpoint, unlike private endpoints which assign a private IP.
- Creating a private endpoint does not automatically disable the service's public endpoint; you must explicitly disable public network access (e.g., on the storage account) to block public access.
- For a service's public FQDN to resolve to the private endpoint IP, create the corresponding privatelink Private DNS zone (e.g., privatelink.database.windows.net or privatelink.blob.core.windows.net), link it to the VNet, and integrate the private endpoint with it.
- Private endpoints are reachable from peered VNets, globally peered VNets, and on-premises networks connected via VPN or ExpressRoute.
- Azure Private Link service lets you publish your own service privately: place VMs behind a Standard Load Balancer, then create a Private Link service linked to that load balancer's frontend.

## Study tips

- Memorize the dedicated subnet names and minimum sizes that the exam loves to test: GatewaySubnet, RouteServerSubnet (/27, ASN 65515), AzureFirewallSubnet (/26), and AzureBastionSubnet (/26).
- For routing questions, apply the rule order every time: longest prefix match first, then source priority UDR > BGP > system route; many questions hinge on this tie-breaker.
- Practice subnet math knowing Azure reserves 5 IPs per subnet (so /24 = 251 usable, /23 = 507 usable); the exam often asks for the smallest CIDR meeting a host count.
- Clearly distinguish service endpoints (subnet identity, public endpoint, backbone route) from private endpoints (private IP NIC, private DNS zone needed) - the difference drives many Private Link answers.
- Match the diagnostic tool to the symptom: IP flow verify for NSG allow/deny, Connection troubleshoot for one-time reachability, Connection monitor for continuous monitoring, and Packet capture for deep traffic analysis.

---

Want the full breakdown? See the complete **[AZ-700 study guide](https://certgrid.app/study-guide/az-700-azure-network-engineer-associate)** and **[free practice questions](https://certgrid.app/practice/az-700-azure-network-engineer-associate)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

