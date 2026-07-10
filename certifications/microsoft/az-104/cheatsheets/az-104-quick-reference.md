# AZ-104 Quick Reference

Use this for last-day revision. It compresses the numbers, tiers, SKUs, and defaults that AZ-104 questions hinge on.

## Identity and governance

| Fact                              | Value                                                            |
| --------------------------------- | ---------------------------------------------------------------- |
| Core roles                        | Owner, Contributor, Reader, User Access Administrator            |
| Who can assign roles              | Owner, User Access Administrator                                 |
| RBAC scopes (top to bottom)       | Management group > subscription > resource group > resource      |
| Management group depth            | 6 levels (excluding root and subscriptions)                      |
| Role assignments per subscription | 4,000                                                            |
| Dynamic groups need               | Microsoft Entra ID P1                                            |
| License prerequisite              | Usage location set on the user                                   |
| Lock types                        | CanNotDelete, ReadOnly (both inherited)                          |
| Tags per resource                 | 50; not inherited by default (Policy Modify can inherit)         |
| Policy effects                    | Deny, Audit, Append, Modify, DeployIfNotExists, AuditIfNotExists |
| SSPR targeting                    | None / Selected (a group) / All                                  |

## Storage

| Fact                        | Value                                                            |
| --------------------------- | ---------------------------------------------------------------- |
| Account name                | 3-24 chars, lowercase letters and numbers, globally unique       |
| Redundancy ladder           | LRS (3, one DC) < ZRS (3 zones) < GRS (6, paired region) < GZRS  |
| Read secondary              | RA-GRS / RA-GZRS only                                            |
| Premium redundancy          | LRS and ZRS only; no access tiers on premium                     |
| Access keys                 | 2 per account (rotate one at a time)                             |
| SAS types                   | Account, service, user delegation (Entra-signed, blob only)      |
| Revoke SAS instantly        | Stored access policy (delete/edit) or rotate the signing key     |
| Blob tiers                  | Hot, cool (30d min), cold (90d min), archive (180d min, offline) |
| Archive rehydration         | Up to ~15 hours standard priority                                |
| Soft delete retention       | 1-365 days                                                       |
| Azure Files protocol/port   | SMB over TCP 445 (NFS on premium)                                |
| Object replication requires | Blob versioning both sides + change feed on source               |
| Bulk transfer tool          | AzCopy (azcopy copy / azcopy sync)                               |

## Compute

| Fact                                 | Value                                                      |
| ------------------------------------ | ---------------------------------------------------------- |
| VM SLA: single premium / set / zones | 99.9% / 99.95% / 99.99%                                    |
| Availability set                     | Up to 3 fault domains, up to 20 update domains (default 5) |
| Set membership                       | Chosen at VM creation only                                 |
| Deallocated VM                       | No compute billing; disks and some IPs still bill          |
| Scale set max                        | 1,000 instances (100 with custom images, uniform)          |
| Orchestration modes                  | Uniform, Flexible                                          |
| Deployment modes                     | Incremental (default), Complete (deletes extras)           |
| Bicep <-> ARM                        | az bicep build (to JSON), az bicep decompile (to Bicep)    |
| Encrypt temp disk + caches           | Encryption at host                                         |
| App Service slots                    | Standard: 5, Premium: 20 (none below Standard)             |
| App Service autoscale                | Standard+ (Basic is manual to 3)                           |
| Container per-second billing         | Azure Container Instances                                  |
| Scale to zero                        | Azure Container Apps                                       |
| Private images                       | Azure Container Registry (Basic/Standard/Premium)          |

## Networking

| Fact                    | Value                                                                   |
| ----------------------- | ----------------------------------------------------------------------- |
| Reserved IPs per subnet | 5 (a /24 gives 251 usable)                                              |
| VNet span               | One region; peer VNets to connect                                       |
| Peering                 | Not transitive; configure on both sides; no overlapping ranges          |
| Peerings per VNet       | 500                                                                     |
| NSG priorities          | 100-4096, lower first, first match wins, stateful                       |
| Inbound evaluation      | Subnet NSG then NIC NSG; both must allow                                |
| Health probe source tag | AzureLoadBalancer                                                       |
| Bastion subnet          | AzureBastionSubnet, /26 minimum                                         |
| Gateway subnet          | GatewaySubnet (exact name)                                              |
| Route precedence        | Longest prefix; then UDR > BGP > system                                 |
| Service endpoint        | Free, subnet to public endpoint over backbone, not from on-prem         |
| Private endpoint        | Private IP for one resource; works from on-prem; needs private DNS zone |
| Load Balancer           | Layer 4 TCP/UDP; Standard SKU is current                                |
| Application Gateway     | Layer 7 HTTP/HTTPS; path/host routing, TLS offload, WAF                 |
| Azure DNS               | Hosts zones (public/private); not a registrar                           |

## Monitoring and maintenance

| Fact                            | Value                                                          |
| ------------------------------- | -------------------------------------------------------------- |
| Metrics retention               | 93 days; near real-time numbers                                |
| Activity log                    | Control-plane events, 90 days free                             |
| Logs                            | Log Analytics workspace, KQL, retention configurable           |
| Alert parts                     | Scope + condition + severity (0-4) + action group              |
| Suppress alerts in maintenance  | Alert processing rule                                          |
| Guest OS metrics need           | Azure Monitor agent + data collection rule                     |
| NSG rule check                  | IP flow verify                                                 |
| Routing check                   | Next hop                                                       |
| Continuous connectivity         | Connection monitor                                             |
| Recovery Services vault         | VMs, SQL in VMs, Azure Files, on-prem, Site Recovery           |
| Backup vault                    | Disks, Blobs, PostgreSQL                                       |
| Vault region rule               | Same region as protected VMs; redundancy fixed at first backup |
| Backup soft delete              | 14 days default                                                |
| Data restore vs region failover | Azure Backup vs Azure Site Recovery                            |

## CLI vs PowerShell in one glance

| Task             | CLI                                | PowerShell                                |
| ---------------- | ---------------------------------- | ----------------------------------------- |
| Pattern          | az noun verb (lowercase)           | Verb-AzNoun                               |
| Create VM        | az vm create                       | New-AzVM                                  |
| Create storage   | az storage account create          | New-AzStorageAccount                      |
| Create VNet      | az network vnet create             | New-AzVirtualNetwork                      |
| Assign role      | az role assignment create          | New-AzRoleAssignment                      |
| Deploy template  | az deployment group create         | New-AzResourceGroupDeployment             |
| Enable VM backup | az backup protection enable-for-vm | Enable-AzRecoveryServicesBackupProtection |

## Ten defaults worth points

1. NSG default inbound: allow VNet + load balancer, deny everything else.
2. Deployment mode default: incremental.
3. Storage default tier setting: hot (or cool); archive is per blob only.
4. Update domains default: 5.
5. Two storage access keys exist for rotation.
6. Peering must be created from both VNets.
7. Budgets alert; they never stop spending.
8. Locks and policies inherit down the hierarchy.
9. Stateful NSGs: allowed inbound flows get their return traffic automatically.
10. Vault redundancy cannot change after items are protected.
