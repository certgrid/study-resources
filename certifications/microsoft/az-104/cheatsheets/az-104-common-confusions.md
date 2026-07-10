# AZ-104 Common Confusions

Most lost points on AZ-104 come from mixing up paired concepts. Work through every pair; if you hesitate on one, reread the matching study note section.

## Identity and governance

| Pair                                      | Difference                                                                          |
| ----------------------------------------- | ----------------------------------------------------------------------------------- |
| Microsoft Entra roles vs Azure RBAC roles | Directory administration (users, licenses) vs resource permissions (VMs, storage)   |
| Global Administrator vs Owner             | Top directory role vs top resource role; one does not imply the other               |
| Owner vs Contributor                      | Both manage resources; only Owner also assigns access                               |
| Contributor vs User Access Administrator  | Manage everything but access vs manage only access                                  |
| Member user vs guest user                 | Created in your tenant vs invited external identity (B2B); both can hold RBAC roles |
| Security group vs Microsoft 365 group     | Access control vs collaboration (mailbox/Teams); types cannot be converted          |
| Assigned vs dynamic membership            | Manual vs attribute rules (needs Entra ID P1)                                       |
| Azure Policy vs RBAC                      | What can be deployed/configured vs who can act; both must allow an action           |
| Policy Deny vs non-compliance             | Blocks new/changed resources vs flags existing ones (never deletes)                 |
| CanNotDelete vs ReadOnly lock             | Delete blocked vs delete AND modify blocked                                         |
| Tags vs Azure Policy                      | Organization/cost metadata vs enforcement (Policy can require/inherit tags)         |
| Budget vs allowed-SKU policy              | Alerts on spend vs prevents expensive deployments                                   |
| Management group vs subscription          | Governance grouping of subscriptions vs billing/access boundary                     |

## Storage

| Pair                                 | Difference                                                                     |
| ------------------------------------ | ------------------------------------------------------------------------------ |
| LRS vs ZRS                           | Three copies in one datacenter vs three copies across zones                    |
| ZRS vs GRS                           | Zone resilience in one region vs a second copy in the paired region            |
| GRS vs RA-GRS                        | Secondary readable only after failover vs readable at all times                |
| GRS vs GZRS                          | LRS-in-primary + paired region vs ZRS-in-primary + paired region               |
| Access keys vs SAS                   | Full-control root secrets vs scoped, time-limited signed URLs                  |
| Account SAS vs service SAS           | Many services vs one service/resource (can use a stored access policy)         |
| Service SAS vs user delegation SAS   | Signed by account key vs signed by Entra credentials (blob only)               |
| SAS vs stored access policy          | The token itself vs the revocable server-side policy it references             |
| Cool vs cold tier                    | 30-day vs 90-day minimum; both online and instant                              |
| Cold vs archive tier                 | Online instant access vs offline, needs rehydration (up to ~15h)               |
| Soft delete vs versioning            | Undo deletion within retention vs automatic history of every overwrite         |
| Version vs snapshot                  | Automatic per write vs manual point-in-time copy                               |
| Blob Storage vs Azure Files          | Object storage over HTTPS vs mountable SMB/NFS shares                          |
| Azure Files vs Azure File Sync       | The cloud share vs syncing it with on-premises Windows Servers (cloud tiering) |
| Storage Explorer vs AzCopy           | GUI browsing/management vs command-line bulk copy                              |
| Service endpoint vs private endpoint | Subnet-to-service over backbone (free, no on-prem) vs private IP in your VNet  |

## Compute

| Pair                                        | Difference                                                                      |
| ------------------------------------------- | ------------------------------------------------------------------------------- |
| Availability set vs availability zone       | Racks in one datacenter (99.95%) vs separate datacenters (99.99%)               |
| Fault domain vs update domain               | Unplanned hardware failure boundary vs planned maintenance reboot group         |
| Availability zone vs region pair            | In-region resilience vs cross-region disaster recovery                          |
| Scale up vs scale out                       | Bigger size/tier (vertical) vs more instances (horizontal)                      |
| Stop vs deallocate                          | In-OS shutdown still bills compute vs deallocation stops compute billing        |
| ARM template vs Bicep                       | JSON format Azure runs vs cleaner language compiled to it                       |
| Incremental vs complete mode                | Leaves unlisted resources vs deletes them                                       |
| Encryption at host vs Azure Disk Encryption | Host-level incl. temp/cache vs in-guest BitLocker/DM-Crypt                      |
| ACI vs Container Apps                       | Simple fast single containers vs microservices with autoscale and scale to zero |
| Container Apps vs AKS                       | Serverless abstraction vs full Kubernetes control                               |
| App Service plan vs web app                 | The billed compute vs the app on it (many apps share one plan)                  |
| Basic vs Standard App Service               | No slots/autoscale vs 5 slots + autoscale                                       |
| Slot swap vs redeploy                       | Warmed instant exchange with rollback vs fresh deployment                       |

## Networking

| Pair                                     | Difference                                                                    |
| ---------------------------------------- | ----------------------------------------------------------------------------- |
| VNet peering vs VPN Gateway VNet-to-VNet | Backbone, fast, no gateway vs encrypted tunnel through gateways               |
| VPN Gateway vs ExpressRoute              | Encrypted over internet vs private dedicated circuit                          |
| Regional vs global peering               | Same region vs cross-region peering                                           |
| NSG vs ASG                               | The filter with rules vs the VM-grouping label used in rules                  |
| NSG vs Azure Firewall                    | Free subnet/NIC filter vs managed central firewall (FQDN rules, threat intel) |
| Subnet NSG vs NIC NSG                    | Evaluated in sequence; a deny at either level blocks inbound                  |
| Azure Bastion vs jump box VM             | Managed browser/native RDP-SSH, no public IPs vs a VM you patch and secure    |
| Load Balancer vs Application Gateway     | L4 TCP/UDP vs L7 HTTP with URL routing, TLS offload, WAF                      |
| Application Gateway vs Front Door        | Regional L7 vs global edge L7 (recognition level)                             |
| Load Balancer rule vs inbound NAT rule   | Distributes across the pool vs forwards a port to one instance                |
| Public vs internal load balancer         | Internet-facing frontend vs private frontend for internal tiers               |
| Public DNS zone vs private DNS zone      | Internet records (delegated domain) vs VNet-only resolution                   |
| UDR vs system route                      | Your override in a route table vs Azure's automatic routing                   |

## Monitoring and maintenance

| Pair                                           | Difference                                                                       |
| ---------------------------------------------- | -------------------------------------------------------------------------------- |
| Metrics vs logs                                | Near real-time numbers vs KQL-queryable records                                  |
| Activity log vs resource logs                  | Control-plane audit vs inside-the-resource telemetry (needs diagnostic settings) |
| Alert rule vs action group                     | The condition that fires vs who/what gets notified                               |
| Action group vs alert processing rule          | Notification target vs at-scale suppression/attachment after firing              |
| VM insights vs Application Insights            | VM performance and dependencies vs application requests and traces               |
| IP flow verify vs connection troubleshoot      | Simulated NSG rule verdict vs live end-to-end path test                          |
| Connection troubleshoot vs connection monitor  | One-shot test vs continuous monitoring with alerts                               |
| Next hop vs effective routes                   | One destination lookup vs the whole merged route table                           |
| Recovery Services vault vs Backup vault        | VMs/Files/on-prem/ASR vs Disks/Blobs/PostgreSQL                                  |
| Azure Backup vs Azure Site Recovery            | Restore data from restore points vs replicate and fail over to another region    |
| RPO vs RTO                                     | How much data you can lose vs how long you can be down                           |
| Backup center vs Recovery Services vault blade | Cross-vault single pane vs one vault's view                                      |

## The five most expensive confusions

These pairs cost the most points because they appear across multiple questions:

1. Service endpoint vs private endpoint: "on-premises must reach it privately" or "disable public access" always means private endpoint.
2. Availability set vs zones: SLA numbers decide it: 99.95% set, 99.99% zones.
3. Backup vs Site Recovery: restore wording vs failover wording.
4. Policy vs RBAC: what can exist vs who can act; a Deny policy stops even an Owner.
5. Cool/cold vs archive: instant access vs rehydration delay.
