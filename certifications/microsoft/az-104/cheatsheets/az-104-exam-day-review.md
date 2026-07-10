# AZ-104 Exam-Day Review

Use this page in the final 30-45 minutes before the exam. It is intentionally short and focused on high-frequency decisions.

## The Exam Mindset

AZ-104 is an administration exam. Questions describe a requirement and ask for the option that meets it with the least cost, least effort, or least privilege. Case studies bury the requirement in a paragraph; find the constraint words: SLA numbers, "on-premises", "no public IP", "lowest cost", "instantly", "automatically".

When stuck, ask:

1. Which domain is this: identity/governance, storage, compute, networking, or monitoring/backup?
2. What is the single hard constraint (SLA, privacy, cost, time)?
3. Which two answers are near-duplicates? The differentiator between them is usually the tested fact.
4. Is the question about WHO (RBAC), WHAT (Policy), or KEEP (lock)?

## Must-Know Pairs

| Pair                                    | Difference                                                      |
| --------------------------------------- | --------------------------------------------------------------- |
| Entra roles vs Azure RBAC               | Directory admin vs resource permissions                         |
| Owner vs Contributor                    | Only Owner assigns access                                       |
| Policy vs RBAC                          | What is allowed vs who can act; both must pass                  |
| CanNotDelete vs ReadOnly                | Block delete vs block delete and change                         |
| LRS vs ZRS vs GRS vs GZRS               | Datacenter vs zones vs paired region vs zones + paired region   |
| GRS vs RA-GRS                           | RA- adds an always-readable secondary                           |
| Cool/cold vs archive                    | Instant access vs rehydration (hours)                           |
| SAS vs stored access policy             | Token vs revocable policy behind it                             |
| Service endpoint vs private endpoint    | Backbone to public endpoint (free) vs private IP (on-prem OK)   |
| Availability set vs zones               | 99.95% racks vs 99.99% datacenters                              |
| Stop vs deallocate                      | Billing continues vs compute billing stops                      |
| Incremental vs complete deployment      | Keep extras vs delete extras                                    |
| ACI vs Container Apps                   | Quick single container vs autoscale/scale-to-zero microservices |
| Slots on Basic vs Standard              | None vs 5 (Premium 20)                                          |
| Peering vs VPN Gateway                  | Backbone VNet link vs encrypted tunnel                          |
| NSG vs ASG                              | Filter vs grouping label inside the filter                      |
| Load Balancer vs Application Gateway    | L4 TCP/UDP vs L7 HTTP (URL routing, WAF, TLS offload)           |
| Metrics vs logs                         | Real-time numbers vs KQL records                                |
| Alert rule vs action group              | What fires vs who is told                                       |
| Backup vs Site Recovery                 | Restore data vs fail over a region                              |
| Recovery Services vault vs Backup vault | VMs/Files/ASR vs Disks/Blobs/PostgreSQL                         |

## Numbers That Decide Answers

| Number                | Meaning                                                   |
| --------------------- | --------------------------------------------------------- |
| 99.9 / 99.95 / 99.99% | Single premium VM / availability set / availability zones |
| 3 / 20 (5)            | Max fault domains / max update domains (default 5)        |
| 30 / 90 / 180         | Min days: cool / cold / archive tiers                     |
| 5                     | IPs Azure reserves per subnet (/24 = 251 usable)          |
| 100-4096              | NSG priority range; lower wins                            |
| /26                   | Minimum AzureBastionSubnet size                           |
| 3-24                  | Storage account name length (lowercase + digits)          |
| 700                   | Passing score out of 1000                                 |
| 6                     | Management group depth levels                             |
| 5 / 20                | App Service slots: Standard / Premium                     |
| 93 / 90               | Days: metrics retention / activity log retention          |
| 14                    | Default backup soft delete days                           |
| 445                   | SMB port for Azure Files                                  |

## Final Decision Tables

### "Give access" questions

| Requirement                     | Answer                               |
| ------------------------------- | ------------------------------------ |
| Manage everything incl. access  | Owner                                |
| Manage everything except access | Contributor                          |
| View only                       | Reader                               |
| Manage access only              | User Access Administrator            |
| Blob data via identity          | Storage Blob Data Reader/Contributor |
| Scope principle                 | Narrowest scope that works           |

### "Protect data" questions

| Requirement               | Answer                                   |
| ------------------------- | ---------------------------------------- |
| Survive disk/rack failure | LRS                                      |
| Survive zone failure      | ZRS                                      |
| Survive region failure    | GRS/GZRS (RA- if secondary reads needed) |
| Undo blob deletion        | Soft delete                              |
| Undo blob overwrite       | Versioning                               |
| VM restore points         | Azure Backup                             |
| Region failover           | Azure Site Recovery                      |

### "Connect things" questions

| Requirement                             | Answer                              |
| --------------------------------------- | ----------------------------------- |
| VNet to VNet                            | Peering                             |
| VNet to on-premises, encrypted internet | VPN Gateway                         |
| VNet to on-premises, private circuit    | ExpressRoute                        |
| Admin access, no public IPs             | Azure Bastion                       |
| PaaS privately from my subnet, free     | Service endpoint                    |
| PaaS privately incl. from on-premises   | Private endpoint + private DNS zone |
| TCP/UDP spread over VMs                 | Load Balancer                       |
| HTTP routing/WAF                        | Application Gateway                 |

### "Watch and react" questions

| Requirement                | Answer                |
| -------------------------- | --------------------- |
| Chart CPU now              | Metrics               |
| Query security events      | Log Analytics (KQL)   |
| Notify people/automation   | Action group          |
| Silence during maintenance | Alert processing rule |
| Which NSG rule blocks?     | IP flow verify        |
| Continuous path monitoring | Connection monitor    |

## Last-Minute Traps

| Trap wording                                   | Better answer                                                  |
| ---------------------------------------------- | -------------------------------------------------------------- |
| "Contributor will assign the role"             | Contributor cannot assign roles                                |
| "The Deny policy deletes existing resources"   | It only blocks new/changed ones; existing become non-compliant |
| "Archive tier for instant access"              | Archive needs rehydration; pick cool/cold                      |
| "SAS expires eventually, that's revocation"    | Stored access policy or key rotation revokes now               |
| "A-B, B-C peering means A reaches C"           | Peering is not transitive                                      |
| "Higher NSG priority number wins"              | Lower number wins                                              |
| "Availability set gives 99.99%"                | Sets give 99.95%; zones give 99.99%                            |
| "Add the running VM to an availability set"    | Only at creation                                               |
| "Slots on the Basic plan"                      | Standard or higher                                             |
| "Back up the VM to a vault in another region"  | Vault must be in the VM's region                               |
| "Service endpoint reachable from on-premises"  | Only private endpoints are                                     |
| "Shut down from inside the OS to stop billing" | Deallocate it (portal/CLI), or compute still bills             |

## Case Study Tactics

1. Read the questions first, then scan the case for the matching constraint.
2. Requirements sections beat background sections; hunt for "must", "cannot", "at least".
3. Watch for numbers (SLA, retention days, instance counts): they select the answer.
4. Existing environment details (regions, tiers, licenses like P1) often disqualify options.

## Final Confidence Checklist

You are ready when you can explain these without looking:

- Owner vs Contributor vs User Access Administrator, and scope inheritance
- Policy vs RBAC vs locks vs tags
- The full redundancy ladder LRS to RA-GZRS and what each survives
- SAS types and the stored access policy revocation trick
- Hot/cool/cold/archive minimums and rehydration
- 99.9 / 99.95 / 99.99 SLA mapping to premium VM / set / zones
- Incremental vs complete deployment modes
- ACI vs Container Apps vs App Service, and slot/autoscale tier rules
- Peering non-transitivity and gateway transit
- NSG evaluation order and priorities
- Service endpoint vs private endpoint
- Metrics vs logs, alert rule vs action group, IP flow verify vs connection monitor
- Backup vs Site Recovery, and the two vault types
