# AZ-104 Service Picker

AZ-104 is a service-selection exam: most scenarios reduce to "which service or option meets the requirement." Match the strongest keyword in the question to the row below.

## Identity and access

| Scenario keyword                                      | Pick                                          |
| ----------------------------------------------------- | --------------------------------------------- |
| External consultant needs access with their own login | Guest user (B2B invitation)                   |
| Group membership from a user attribute rule           | Dynamic security group (Entra ID P1)          |
| Users reset their own passwords                       | Self-service password reset (SSPR)            |
| Bulk create users from a spreadsheet                  | CSV bulk create in Microsoft Entra ID         |
| Give access, least privilege, one resource group      | Built-in role at resource group scope         |
| Manage VMs but not the network                        | Virtual Machine Contributor                   |
| Grant access without managing resources               | User Access Administrator                     |
| Built-in roles don't fit exactly                      | Custom RBAC role (clone the closest built-in) |
| See why a user has a permission                       | Access control (IAM) > Check access           |

## Governance and cost

| Scenario keyword                                       | Pick                                          |
| ------------------------------------------------------ | --------------------------------------------- |
| Enforce allowed regions/SKUs/naming                    | Azure Policy (Deny)                           |
| Auto-fix or auto-deploy settings on existing resources | Policy DeployIfNotExists/Modify + remediation |
| Many related policies as one unit                      | Initiative (policy set)                       |
| Govern many subscriptions at once                      | Management group (assign policy/RBAC there)   |
| Prevent accidental deletion                            | CanNotDelete lock                             |
| Freeze a resource completely                           | ReadOnly lock                                 |
| Cost reporting by department/project                   | Tags (+ Policy to require/inherit them)       |
| Warn at 80% of monthly spend                           | Budget with cost alert                        |
| Right-size or shut down underused VMs                  | Azure Advisor cost recommendations            |
| Explore last month's spend by service                  | Cost analysis                                 |

## Storage

| Scenario keyword                                       | Pick                                           |
| ------------------------------------------------------ | ---------------------------------------------- |
| Cheapest redundancy, single datacenter risk OK         | LRS                                            |
| Survive a zone failure, data stays in region           | ZRS                                            |
| Survive a region outage                                | GRS / GZRS                                     |
| Read data in the secondary region continuously         | RA-GRS / RA-GZRS                               |
| Time-limited access for an external party              | SAS token with expiry                          |
| Revocable SAS                                          | Service SAS + stored access policy             |
| SAS without exposing account keys                      | User delegation SAS                            |
| Identities instead of keys for blob access             | Entra ID + Storage Blob Data roles             |
| Only my VNet/subnet may reach the account (free)       | Storage firewall + service endpoint            |
| Private IP for the account, reachable from on-premises | Private endpoint                               |
| Lift-and-shift file shares (SMB)                       | Azure Files                                    |
| Keep hot files on the local server, rest in cloud      | Azure File Sync with cloud tiering             |
| Cheapest for rarely read data, instant when needed     | Cool or cold tier                              |
| Long-term compliance data, retrieval can wait hours    | Archive tier                                   |
| Auto-move old blobs to cheaper tiers / delete          | Lifecycle management policy                    |
| Recover overwritten blobs                              | Blob versioning                                |
| Recover deleted blobs/containers                       | Soft delete                                    |
| WORM/immutable storage                                 | Immutability policy (time-based or legal hold) |
| Script a 50 TB migration                               | AzCopy                                         |
| Copy blobs continuously to another account/region      | Object replication                             |

## Compute

| Scenario keyword                                        | Pick                                  |
| ------------------------------------------------------- | ------------------------------------- |
| Repeatable infrastructure deployments                   | ARM template or Bicep file            |
| Re-run must never delete extra resources                | Incremental mode (default)            |
| Resource group must exactly match the template          | Complete mode                         |
| 99.95% SLA, region without zones                        | Availability set (2+ VMs)             |
| 99.99% SLA for VMs                                      | 2+ VMs across availability zones      |
| Auto add/remove identical VMs on demand                 | Virtual Machine Scale Set + autoscale |
| Encrypt temp disk and caches                            | Encryption at host                    |
| In-guest BitLocker with Key Vault                       | Azure Disk Encryption                 |
| Move VM to another region                               | Azure Resource Mover / Site Recovery  |
| Extreme disk IOPS for a database                        | Ultra Disk (data disk)                |
| Quick container, per-second billing, no orchestrator    | Azure Container Instances             |
| Containers that scale to zero, revisions, microservices | Azure Container Apps                  |
| Private registry for images                             | Azure Container Registry              |
| Web app, no OS management                               | Azure App Service                     |
| Zero-downtime web deploys with rollback                 | Deployment slots + swap (Standard+)   |
| Web autoscale                                           | App Service Standard+ (or Premium)    |
| Free HTTPS certificate for a custom domain              | App Service managed certificate       |
| App outbound calls into a VNet                          | VNet integration                      |
| App inbound on a private IP                             | Private endpoint for the app          |

## Networking

| Scenario keyword                                     | Pick                                               |
| ---------------------------------------------------- | -------------------------------------------------- |
| Connect two VNets, low latency, backbone             | VNet peering (global if cross-region)              |
| Spokes use the hub's gateway                         | Peering with gateway transit + use remote gateway  |
| Encrypted site-to-site to on-premises                | VPN Gateway                                        |
| Private dedicated on-premises circuit                | ExpressRoute                                       |
| Force traffic through a firewall/NVA                 | User-defined route (next hop: virtual appliance)   |
| Filter by port/IP/protocol at subnet or NIC          | Network security group                             |
| Refer to VM roles instead of IPs in rules            | Application security groups                        |
| RDP/SSH without public IPs                           | Azure Bastion                                      |
| Central outbound filtering with FQDN rules           | Azure Firewall                                     |
| PaaS traffic stays on backbone, free, from my subnet | Service endpoint                                   |
| PaaS with a private IP, on-prem reachable            | Private endpoint (+ private DNS zone)              |
| Host public domain records                           | Azure DNS public zone                              |
| Internal-only name resolution across VNets           | Azure Private DNS zone (linked, auto-registration) |
| Distribute TCP/UDP traffic regionally                | Azure Load Balancer (Standard)                     |
| Internal tier-to-tier distribution                   | Internal load balancer                             |
| RDP to a specific VM behind an LB                    | Inbound NAT rule                                   |
| Route by URL path/host, TLS offload, sticky sessions | Application Gateway                                |
| Protect web app from OWASP attacks                   | Application Gateway WAF (or Front Door WAF)        |
| Global HTTP entry point, edge acceleration           | Azure Front Door (recognition)                     |
| DNS-based global failover                            | Traffic Manager (recognition)                      |

## Monitoring and maintenance

| Scenario keyword                                   | Pick                                       |
| -------------------------------------------------- | ------------------------------------------ |
| Near real-time performance chart                   | Azure Monitor metrics (Metrics Explorer)   |
| Query events/logs with KQL                         | Log Analytics workspace                    |
| Route resource logs to storage/workspace/event hub | Diagnostic settings                        |
| Who deleted the resource group?                    | Activity log                               |
| Notify on-call via SMS/email/webhook               | Action group                               |
| Alert when CPU > 85% for 15 minutes                | Metric alert rule                          |
| Alert on a KQL query result                        | Log search alert                           |
| Silence alerts during patching                     | Alert processing rule                      |
| Deep VM performance + dependency map               | VM insights                                |
| In-guest memory counters                           | Azure Monitor agent + data collection rule |
| Which NSG rule blocks this traffic?                | Network Watcher IP flow verify             |
| Where does traffic route next?                     | Network Watcher next hop                   |
| Test connectivity source to destination now        | Connection troubleshoot                    |
| Watch a connection continuously                    | Connection monitor                         |
| Capture packets on a VM                            | Network Watcher packet capture             |
| Daily VM restore points with retention             | Azure Backup + Recovery Services vault     |
| Restore one file from a VM backup                  | File-level recovery                        |
| Back up Azure Disks/Blobs/PostgreSQL               | Backup vault                               |
| Replicate VMs to another region, failover          | Azure Site Recovery                        |
| Prove DR works without downtime                    | ASR test failover                          |
| One dashboard for all vaults and jobs              | Backup center                              |

## When two answers both look right

| If torn between...                  | Decide by asking...                                              |
| ----------------------------------- | ---------------------------------------------------------------- |
| Service endpoint / private endpoint | Does on-premises need access, or must public access be disabled? |
| Availability set / zones            | Which SLA number is quoted: 99.95% or 99.99%?                    |
| Load Balancer / Application Gateway | Is the traffic HTTP with routing/WAF needs, or raw TCP/UDP?      |
| Backup / Site Recovery              | Restore data, or keep running in another region?                 |
| Policy / RBAC                       | Restricting the resource, or restricting the person?             |
| SAS / stored access policy          | Is instant revocation demanded?                                  |
| ACI / Container Apps                | Is scale to zero or microservices mentioned?                     |
| Cool / archive                      | Is retrieval time mentioned (instant vs hours)?                  |
