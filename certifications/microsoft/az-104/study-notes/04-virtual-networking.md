# 04 - Implement and Manage Virtual Networking

This domain is worth 15-20% of the exam. It covers virtual networks and subnets, peering, public IPs, user-defined routes, NSGs and ASGs, Azure Bastion, service endpoints and private endpoints, Azure DNS, and load balancing. Networking questions are precise: read CIDR ranges, rule priorities, and SKU names carefully.

## Mental model

Everything in Azure networking is layered: address space -> subnets -> NICs -> rules on top (NSG), routes underneath (system routes + UDRs), and connectivity between networks (peering, gateways). Security questions split into "filter traffic" (NSG/ASG), "reach privately" (endpoints), and "reach safely" (Bastion). Distribution questions split into layer 4 (Load Balancer) and layer 7 (Application Gateway).

| Scenario keyword                                     | Likely concept                        |
| ---------------------------------------------------- | ------------------------------------- |
| "Connect two VNets over the Microsoft backbone"      | VNet peering                          |
| "Peered VNets in different regions"                  | Global VNet peering                   |
| "Encrypted tunnel to on-premises over the internet"  | VPN Gateway (site-to-site)            |
| "Private dedicated circuit to on-premises"           | ExpressRoute                          |
| "Force all outbound traffic through a firewall"      | User-defined route (0.0.0.0/0 to NVA) |
| "Filter traffic by port/IP to a subnet"              | Network security group                |
| "Group VMs by role in security rules"                | Application security group            |
| "RDP/SSH without public IPs"                         | Azure Bastion                         |
| "Keep storage traffic on the Azure backbone"         | Service endpoint                      |
| "Private IP for a PaaS service in my VNet"           | Private endpoint                      |
| "Host DNS records for a domain"                      | Azure DNS public zone                 |
| "Name resolution between VNets, not on the internet" | Azure Private DNS zone                |
| "Distribute TCP traffic across VMs"                  | Azure Load Balancer                   |
| "URL path routing, cookie affinity, WAF"             | Application Gateway                   |

## Virtual networks and subnets

### Address planning

- A VNet has one or more private address spaces in CIDR notation (e.g. 10.0.0.0/16).
- Subnets carve up the address space; a subnet's range must sit inside the VNet range and not overlap other subnets.
- Azure reserves 5 IPs in every subnet: network, broadcast, gateway, and two DNS addresses (so a /24 gives 251 usable).
- VNets are regional: a VNet cannot span regions (peering connects them instead).
- Address spaces of networks you plan to connect must not overlap.

### Special subnets to recognize

| Subnet name         | Required by                        |
| ------------------- | ---------------------------------- |
| GatewaySubnet       | VPN Gateway / ExpressRoute gateway |
| AzureBastionSubnet  | Azure Bastion (/26 or larger)      |
| AzureFirewallSubnet | Azure Firewall                     |

### Public IP addresses

| Property   | Standard SKU                           | Basic SKU (being retired) |
| ---------- | -------------------------------------- | ------------------------- |
| Allocation | Always static                          | Static or dynamic         |
| Security   | Closed by default (needs NSG to allow) | Open by default           |
| Zones      | Zone-redundant or zonal                | No zone support           |

Key facts: Standard is the exam-current answer; a Standard public IP on a VM requires an NSG rule to allow inbound traffic.

## VNet peering

| Fact               | Detail                                                                           |
| ------------------ | -------------------------------------------------------------------------------- |
| What it does       | Connects two VNets over the Microsoft backbone; private IPs talk directly        |
| Regional vs global | Same region vs different regions (global)                                        |
| Transitivity       | NOT transitive: A-B and B-C does not give A-C                                    |
| Configuration      | Created on BOTH VNets (two peering objects)                                      |
| Address spaces     | Must not overlap                                                                 |
| Gateway transit    | A peered spoke can use the hub's VPN/ExpressRoute gateway ("use remote gateway") |
| Cost               | Ingress/egress charged; still far cheaper/faster than gateways                   |

Hub-spoke: spokes peer to a hub that holds shared services (firewall, gateway, DNS). Spoke-to-spoke traffic goes through the hub only if routed (UDR via NVA/firewall), because peering is not transitive.

## Routing

### System routes and user-defined routes

- Azure builds system routes automatically: intra-VNet, peering, internet (0.0.0.0/0), and gateway routes.
- A route table with user-defined routes (UDRs) is associated to subnets to override system routes.
- Longest-prefix match wins; among equal prefixes: UDR beats BGP beats system route.

| Next hop type           | Use                                              |
| ----------------------- | ------------------------------------------------ |
| Virtual appliance       | Send traffic to an NVA/firewall (specify its IP) |
| Virtual network gateway | To on-premises via VPN/ExpressRoute              |
| Virtual network         | Within the VNet                                  |
| Internet                | Out to the internet                              |
| None                    | Drop the traffic (blackhole)                     |

Classic exam pattern: route 0.0.0.0/0 with next hop "virtual appliance" pointing at Azure Firewall or an NVA in the hub.

### Troubleshooting connectivity

- Effective routes (on a NIC) show the final route table after system + UDR + BGP merging.
- Effective security rules show the combined NSG result at NIC and subnet level.
- Network Watcher tools (detailed in domain 5): IP flow verify, next hop, connection troubleshoot, packet capture.

## NSGs and ASGs

### NSG essentials

| Fact                   | Detail                                                               |
| ---------------------- | -------------------------------------------------------------------- |
| Attach points          | Subnet and/or NIC                                                    |
| Rule fields            | Priority, source, destination, port, protocol, direction, allow/deny |
| Priority               | 100-4096; LOWER number is evaluated first; first match wins          |
| Default inbound rules  | Allow VNet, allow Azure Load Balancer, deny all else                 |
| Default outbound rules | Allow VNet, allow internet, deny all else                            |
| Stateful               | Return traffic of an allowed flow is automatically allowed           |

Evaluation order for inbound traffic: subnet NSG first, then NIC NSG; BOTH must allow. Outbound is NIC first, then subnet.

### Service tags

Use service tags instead of IP lists in rules: VirtualNetwork, Internet, AzureLoadBalancer, Storage, Sql, AzureCloud, and region-scoped variants like Storage.WestEurope.

### Application security groups

- An ASG is a label you attach to NICs (e.g. asg-web, asg-db).
- NSG rules can use ASGs as source/destination: "allow asg-web to asg-db on 1433."
- Removes the need to track VM IP addresses in rules; all NICs must be in the same VNet for one rule.

### NSG vs ASG vs Azure Firewall

| Tool           | What it is                                                                                               |
| -------------- | -------------------------------------------------------------------------------------------------------- |
| NSG            | Free stateful packet filter on subnets/NICs                                                              |
| ASG            | Grouping label used inside NSG rules                                                                     |
| Azure Firewall | Managed, centralized firewall service with FQDN rules, threat intel, SNAT (recognition level for AZ-104) |

## Azure Bastion

- Managed jump host: RDP/SSH to VMs through the portal (or native client on Standard+) over TLS 443.
- VMs need no public IP, and you can block 3389/22 from the internet entirely.
- Requires a subnet named AzureBastionSubnet (/26 or larger) and deploys per VNet (reachable to peered VNets).
- SKUs: Developer (limited), Basic, Standard, Premium; Standard adds native client, IP-based connection, scaling.

## Service endpoints vs private endpoints

| Aspect             | Service endpoint                                       | Private endpoint                                          |
| ------------------ | ------------------------------------------------------ | --------------------------------------------------------- |
| What it does       | Subnet traffic to a PaaS service stays on the backbone | The PaaS resource gets a private IP (NIC) in your VNet    |
| Service address    | Still the public endpoint (public IP)                  | Private IP from your subnet                               |
| Reach from on-prem | No                                                     | Yes (via VPN/ExpressRoute)                                |
| Granularity        | Whole service per subnet                               | One specific resource instance                            |
| Cost               | Free                                                   | Charged per hour + data                                   |
| Exam wording       | "Restrict storage to my subnet, no extra cost"         | "Private IP", "disable public access", "from on-premises" |

Private endpoints usually need a matching Azure Private DNS zone (e.g. privatelink.blob.core.windows.net) so the name resolves to the private IP.

## Name resolution

| Option                 | Use                                                              |
| ---------------------- | ---------------------------------------------------------------- |
| Azure-provided DNS     | Default; resolves VMs in the same VNet, no config                |
| Azure DNS public zone  | Host records for your public domain (you delegate NS records)    |
| Azure Private DNS zone | Custom names inside VNets; link zones to VNets                   |
| Auto-registration      | A linked VNet can auto-register VM A records into a private zone |
| Custom DNS servers     | Point the VNet at your own DNS (e.g. domain controllers)         |

Record types to recognize: A (name to IPv4), CNAME (alias), MX, TXT, NS. Azure DNS also supports alias records that track Azure resources (e.g. a public IP).

Key fact: Azure DNS is not a domain registrar; you buy the domain elsewhere and delegate to Azure DNS name servers.

## Load balancing

### Azure Load Balancer (layer 4)

| Component           | Role                                                          |
| ------------------- | ------------------------------------------------------------- |
| Frontend IP         | Public (public LB) or private (internal LB) entry point       |
| Backend pool        | VMs / scale set instances receiving traffic                   |
| Health probe        | TCP/HTTP(S) check; unhealthy instances stop receiving traffic |
| Load balancing rule | Maps frontend port to backend port for a protocol             |
| Inbound NAT rule    | Port-forwards to a specific instance (e.g. RDP per VM)        |
| Outbound rule       | Controls SNAT for outbound internet (Standard)                |

| SKU      | Notes                                                                   |
| -------- | ----------------------------------------------------------------------- |
| Standard | Zone-redundant, secure by default (needs NSG), SLA, up to 1000 backends |
| Basic    | Legacy/retiring; no SLA, no zones                                       |

Key facts:

- Distribution is 5-tuple hash by default; session persistence options: client IP, client IP + protocol.
- Internal (private) load balancer: same service with a private frontend IP for internal tiers.
- Load Balancer works with TCP/UDP; it does not inspect HTTP or terminate TLS.

### Application Gateway (layer 7)

- HTTP/HTTPS only: URL path-based routing, host-based routing, TLS termination, cookie session affinity, rewrite, autoscaling (v2).
- Optional Web Application Firewall (WAF) SKU protects against OWASP attacks.
- Needs its own subnet.

### Choosing the balancer (include the two AZ-104-adjacent global options)

| Requirement                                | Service                        |
| ------------------------------------------ | ------------------------------ |
| TCP/UDP distribution, regional             | Azure Load Balancer            |
| HTTP routing by URL/host, TLS offload, WAF | Application Gateway            |
| Global HTTP acceleration + WAF at the edge | Azure Front Door (recognition) |
| DNS-based global routing to any endpoint   | Traffic Manager (recognition)  |

### Troubleshoot load balancing

- Most common cause: health probe failing (wrong port/path, NSG blocking the probe source AzureLoadBalancer, app down).
- Backend VMs must be in the pool and healthy; Standard LB backends need NSG rules allowing traffic.
- Use Network Watcher connection troubleshoot and LB Insights/metrics (health probe status).

## Limits and numbers to memorize

| Item                                  | Value                                             |
| ------------------------------------- | ------------------------------------------------- |
| IPs Azure reserves per subnet         | 5 (first 4 + broadcast)                           |
| Peerings per VNet                     | 500                                               |
| NSG rule priority range               | 100-4096 (lower runs first)                       |
| AzureBastionSubnet minimum size       | /26                                               |
| Usable hosts in a /24 subnet in Azure | 251                                               |
| NSG default rules                     | Cannot be deleted; override with lower priorities |
| Load Balancer SKUs                    | Standard (current), Basic (retiring)              |
| VNet span                             | One region (peer to connect regions)              |
| Stored in mind: subnet NSG + NIC NSG  | Both must allow inbound traffic                   |

## CLI and PowerShell recognition

| Task                     | Azure CLI                                 | PowerShell                          |
| ------------------------ | ----------------------------------------- | ----------------------------------- |
| Create a VNet            | az network vnet create                    | New-AzVirtualNetwork                |
| Add a subnet             | az network vnet subnet create             | Add-AzVirtualNetworkSubnetConfig    |
| Create a peering         | az network vnet peering create            | Add-AzVirtualNetworkPeering         |
| Create a public IP       | az network public-ip create               | New-AzPublicIpAddress               |
| Create an NSG            | az network nsg create                     | New-AzNetworkSecurityGroup          |
| Add an NSG rule          | az network nsg rule create                | Add-AzNetworkSecurityRuleConfig     |
| Create a route table     | az network route-table create             | New-AzRouteTable                    |
| Add a route              | az network route-table route create       | Add-AzRouteConfig                   |
| Create a DNS zone        | az network dns zone create                | New-AzDnsZone                       |
| Add a DNS record         | az network dns record-set a add-record    | New-AzDnsRecordSet                  |
| Create a load balancer   | az network lb create                      | New-AzLoadBalancer                  |
| Show effective routes    | az network nic show-effective-route-table | Get-AzEffectiveRouteTable           |
| Show effective NSG rules | az network nic list-effective-nsg         | Get-AzEffectiveNetworkSecurityGroup |

## Common confusions

| Confusion                            | Correct idea                                                                     |
| ------------------------------------ | -------------------------------------------------------------------------------- |
| VNet peering vs VPN Gateway          | Backbone connection between VNets vs encrypted tunnel (on-prem or VNet-to-VNet)  |
| Peering transitivity                 | Not transitive; hub-spoke needs routing through an NVA or extra peerings         |
| Service endpoint vs private endpoint | Backbone path to a public endpoint vs a private IP for one resource in your VNet |
| NSG vs ASG                           | The filter vs the grouping label used inside the filter's rules                  |
| NSG vs Azure Firewall                | Free packet filtering vs managed central firewall with FQDN/threat rules         |
| Subnet NSG vs NIC NSG                | Both are evaluated; a deny in either blocks inbound traffic                      |
| Load Balancer vs Application Gateway | Layer 4 TCP/UDP vs layer 7 HTTP with URL routing/WAF                             |
| Application Gateway vs Front Door    | Regional L7 vs global edge L7                                                    |
| Public DNS zone vs private DNS zone  | Internet-facing records vs VNet-internal resolution                              |
| Azure DNS vs domain registrar        | Azure hosts the zone; it does not sell domains                                   |
| Basic vs Standard public IP/LB       | Legacy open-by-default vs current secure-by-default zone-capable SKU             |

## Exam traps

| Trap                                                         | Why people miss it                                                |
| ------------------------------------------------------------ | ----------------------------------------------------------------- |
| Counting a /24 as 254 usable IPs                             | Azure reserves 5, leaving 251                                     |
| A-B and B-C peering assumed to connect A and C               | Peering is not transitive                                         |
| Creating peering on only one VNet                            | Peering must be configured from both sides                        |
| Overlapping address spaces in peered/connected networks      | Overlaps block peering and VPN connections                        |
| Higher priority number assumed to win in NSGs                | Lower number wins; 100 beats 4096                                 |
| Allowing traffic in the NIC NSG but not the subnet NSG       | Inbound must pass both NSGs                                       |
| Blocking AzureLoadBalancer tag and wondering why probes fail | Health probes come from the AzureLoadBalancer service tag         |
| Naming the Bastion subnet "BastionSubnet"                    | It must be exactly AzureBastionSubnet, /26 or larger              |
| Using a service endpoint to reach storage from on-premises   | Service endpoints work only from the VNet; use a private endpoint |
| Choosing Application Gateway for a UDP workload              | App Gateway is HTTP/HTTPS only; use Load Balancer                 |
| Forgetting private DNS when using private endpoints          | Without the privatelink zone, names still resolve to public IPs   |

## Mini scenarios

| Scenario                                                                                                    | Best answer                                                                            |
| ----------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| VNet1 (10.1.0.0/16) and VNet2 (10.2.0.0/16) in different regions must communicate privately at low latency. | Global VNet peering                                                                    |
| Spoke VNets must reach on-premises through the hub's VPN gateway.                                           | Peering with gateway transit: hub "allow gateway transit", spokes "use remote gateway" |
| All internet-bound traffic from a subnet must pass through a firewall NVA.                                  | UDR: 0.0.0.0/0 next hop virtual appliance (NVA's IP)                                   |
| Web VMs and DB VMs share a subnet; only web VMs may reach DB VMs on 1433.                                   | ASGs (asg-web, asg-db) referenced in NSG rules                                         |
| Admins need RDP to VMs that must not have public IPs, without deploying jump VMs.                           | Azure Bastion                                                                          |
| A storage account must be reachable only from subnet snet-app, with no charge for the connection.           | Service endpoint + storage firewall VNet rule                                          |
| An on-premises app must reach an Azure SQL database over the private VPN connection.                        | Private endpoint for the SQL server (+ private DNS zone)                               |
| The company domain contoso.com must have its records hosted in Azure.                                       | Azure DNS public zone, delegate NS at the registrar                                    |
| VMs across three VNets must resolve each other by name internally only.                                     | Azure Private DNS zone linked to all three VNets                                       |
| An internal three-tier app needs TCP distribution from web tier to app tier with no public exposure.        | Internal (private) Azure Load Balancer                                                 |
| Requests to /images and /video must go to different backend pools, with TLS termination.                    | Application Gateway with path-based routing                                            |
| Users reach some LB backends but probes mark two VMs unhealthy; app runs fine locally on them.              | Check NSG allows the probe (AzureLoadBalancer tag) and probe port/path                 |

## Check yourself

1. How many usable IP addresses does a 10.0.1.0/24 subnet give you in Azure, and why?
2. VNet A peers with VNet B, and B peers with C. Can A reach C? What are two fixes?
3. Which NSG rule wins: priority 200 allow or priority 400 deny, for the same traffic?
4. Inbound traffic is allowed by the NIC NSG but denied by the subnet NSG. Does it arrive?
5. What subnet name and minimum size does Azure Bastion require?
6. When must you choose a private endpoint instead of a service endpoint?
7. Which load balancing service handles URL path-based routing and WAF?
8. What is the default inbound NSG rule for traffic from the internet?
9. Which route wins when a UDR, a BGP route, and a system route all match the same prefix exactly?
10. Which CLI command creates a VNet peering: az network vnet peering create or az network vnet create?

## Answer guide

1. 251; Azure reserves the first four addresses and the broadcast address (5 total).
2. No; peering is not transitive. Fix with a direct A-C peering, or route through a hub NVA/firewall with UDRs.
3. Priority 200 allow; the lower number is evaluated first and first match wins.
4. No; inbound traffic must be allowed by both the subnet NSG and the NIC NSG.
5. AzureBastionSubnet, at least /26.
6. When access must come from on-premises, when public access must be fully disabled, or when a private IP is required for one specific resource.
7. Application Gateway (WAF SKU for the firewall).
8. Deny (DenyAllInbound); only VNet and Azure Load Balancer traffic are allowed by default.
9. The user-defined route; UDR beats BGP, which beats system routes at the same prefix length.
10. az network vnet peering create; the other creates the VNet itself.
