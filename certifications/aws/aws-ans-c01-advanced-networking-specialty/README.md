# AWS ANS-C01: Advanced Networking Specialty - Study Cheatsheet

The AWS Certified Advanced Networking - Specialty (ANS-C01) validates deep expertise in designing, implementing, operating, and securing complex AWS and hybrid network architectures. It targets networking professionals with at least five years of experience and a strong command of VPC design, Transit Gateway, Direct Connect, DNS, load balancing, and network security. The exam is 170 minutes, contains 65 scored questions plus unscored items, and requires a scaled score of 750 out of 1000 to pass.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | AWS ANS-C01 |
| Credential | AWS ANS-C01: Advanced Networking Specialty |
| Level | Specialty |
| Practice mock length | ~65 questions |
| Duration | ~170 minutes |
| Passing score | 750 out of 1000 |
| Notes reviewed | 2026-06-23 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Network Design | ~28% |
| 2 | Network Implementation | ~21% |
| 3 | Network Management and Operations | ~27% |
| 4 | Network Security, Compliance, and Governance | ~24% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Network Design

- A VPC is a Regional construct that spans all Availability Zones in one Region but never crosses Regions; each subnet is bound to exactly one AZ, which is how AZ-level fault isolation is achieved.
- Transit Gateway is a Regional hub providing transitive routing between thousands of VPCs and on-premises networks; it scales linearly versus VPC peering, which needs N*(N-1)/2 connections and has no transitive routing.
- VPC peering and Transit Gateway both require non-overlapping CIDRs because routing is IP-based; remediate overlaps by re-IPing one VPC or exposing specific services through AWS PrivateLink or NAT.
- Gateway VPC endpoints are free route-table entries that reach only Amazon S3 and DynamoDB; Interface endpoints (PrivateLink) place ENIs with private IPs in your subnets and support hundreds of services.
- The only technical difference between a public and private subnet is the route table: a public subnet has a 0.0.0.0/0 route to an internet gateway, a private subnet does not.
- Deploy one NAT gateway per AZ and route each AZ's private subnets to the NAT gateway in the same AZ; this avoids cross-AZ data charges and removes the NAT gateway as a single point of failure.

### Domain 2 - Network Implementation

- Network Load Balancer operates at Layer 4 (TCP/UDP/TLS), offers ultra-low latency, preserves the client source IP, and supports one static Elastic IP per AZ for firewall allowlisting.
- Application Load Balancer operates at Layer 7, routing HTTP/HTTPS by host header and URL path, and supports advanced features like redirects, fixed responses, OIDC/Cognito authentication, and WebSocket.
- Gateway Load Balancer uses the GENEVE protocol on port 6081 to transparently insert and scale third-party virtual firewalls and IDS/IPS appliances in the traffic path via GWLB endpoints.
- Direct Connect VIF types: a Private VIF reaches VPC resources over private IPs, a Public VIF reaches AWS public service endpoints over public IPs, and a Transit VIF connects to a Direct Connect gateway and Transit Gateway.
- BGP is required for dynamic routing on both Direct Connect and Site-to-Site VPN; AWS uses BGP ASNs to identify the customer and AWS sides, and you can influence path selection with AS-path prepending and local preference.
- A Transit Gateway VPC attachment places ENIs in one subnet per chosen AZ; the TGW can only route to resources in AZs where the attachment has a subnet.

### Domain 3 - Network Management and Operations

- VPC Flow Logs capture metadata only (source/destination IP, ports, protocol, packet and byte counts, ACCEPT or REJECT) to CloudWatch Logs, S3, or Kinesis Data Firehose; they never capture packet payloads.
- VPC Traffic Mirroring copies raw packet payloads from a source ENI, NLB, or GWLB to a target ENI or NLB, enabling deep packet inspection and IDS analysis that Flow Logs cannot provide.
- VPC Reachability Analyzer (Network Insights) statically traces the hop-by-hop path between a source and destination and identifies the exact component (SG, NACL, route table) that blocks connectivity, without sending live packets.
- A Route 53 private hosted zone is associated with one or more VPCs and only answers queries originating inside those VPCs, providing internal domain resolution not exposed to the public internet.
- Route 53 Resolver inbound endpoints accept DNS queries from on-premises resolvers (over DX or VPN) for AWS-hosted zones; outbound endpoints with forwarding rules send VPC queries for on-prem domains to on-prem resolvers.
- Latency-based routing returns the Region with the lowest measured network latency to the user, which differs from geolocation routing that selects purely by the user's geographic location.

### Domain 4 - Network Security, Compliance, and Governance

- Security Groups are stateful and applied at the ENI level: allowing inbound traffic automatically permits the return traffic; they support allow rules only, and you can reference another security group as a source.
- Network ACLs are stateless and applied at the subnet level: both inbound and outbound directions must be explicitly allowed, rules are evaluated in numbered order, and they support both allow and deny rules.
- AWS Network Firewall is a managed stateful firewall and IPS supporting Suricata-compatible rules and domain/FQDN filtering (matching TLS SNI and HTTP Host headers), commonly deployed in a centralized inspection VPC behind a Transit Gateway.
- AWS WAF inspects HTTP/HTTPS requests and integrates with CloudFront, ALB, API Gateway, and AppSync; rate-based rules throttle abusive sources and managed rule groups block common exploits like SQLi and XSS.
- AWS Firewall Manager, built on AWS Organizations, centrally enforces WAF web ACLs, Shield Advanced, Network Firewall, and security group policies and automatically applies them to new accounts and resources.
- Place backend instances in private subnets behind a public-facing load balancer and scope their security group to allow only the load balancer's security group, never the open internet.

## Study tips

- Read each scenario for the deciding constraint first - keywords like 'overlapping CIDRs', 'lowest latency', 'preserve source IP', 'no internet traversal', or 'centralized inspection' usually map directly to one correct service.
- Know the decision boundaries cold: NLB (L4, static IP, source IP) vs ALB (L7, host/path) vs GWLB (GENEVE appliances); Gateway endpoint (S3/DynamoDB only, free) vs Interface endpoint (PrivateLink, ENI, paid).
- For hybrid connectivity questions, separate the access type (Private VIF, Public VIF, Transit VIF), the routing protocol (always BGP for dynamic), and the resiliency pattern (multi-location DX plus VPN failover).
- Be precise about stateful vs stateless and where it applies: Security Groups are stateful per-ENI with allow-only rules; NACLs are stateless per-subnet with ordered allow and deny rules requiring both directions.
- Manage the 170 minutes by flagging long multi-requirement design questions and answering shorter CLI and concept questions first; eliminate options that violate a hard constraint before comparing the survivors.

---

Want the full breakdown? See the complete **[AWS ANS-C01 study guide](https://certgrid.app/study-guide/aws-ans-c01-advanced-networking-specialty)** and **[free practice questions](https://certgrid.app/practice/aws-ans-c01-advanced-networking-specialty)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

