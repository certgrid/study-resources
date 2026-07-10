# AZ-104: Microsoft Azure Administrator

AZ-104 is the core Azure operations exam. Unlike AZ-900, it expects you to know how services are actually configured: identity and RBAC scopes, storage redundancy and access control, VM deployment options, virtual networking, and monitoring plus backup. Questions are scenario-driven and often ask "which option meets the requirement at the lowest cost or effort."

These notes are built for fast revision and real understanding. Read the domain notes in order, do the labs so the portal blades feel familiar, then use the cheatsheets to remove confusion before taking practice tests.

Be honest about the time: typical AZ-104 preparation is 4-6 weeks alongside a job at 1-2 hours per day; only people with real Azure administration experience should plan for less.

## Start Here

Pick the path that matches where you are. The short paths are REVISION paths for people who already studied, not total prep time:

| Where you are                     | Use this path                                                                                                                        |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| Final day before the exam         | Read [Exam-Day Review](cheatsheets/az-104-exam-day-review.md), then [Common Confusions](cheatsheets/az-104-common-confusions.md)     |
| Final week (already prepared)     | Reread the five study notes, drill [Service Picker](cheatsheets/az-104-service-picker.md), take practice tests, review wrong answers |
| 4-6 weeks (recommended full prep) | Follow the recommended plan below, domain by domain with the matching labs                                                           |
| New to Azure                      | Do the [AZ-900 pack](../az-900/) first, then come back and start with [Lab 00](labs/00-set-up-az104-lab-environment.md)              |

## Exam Snapshot

| Item           | Detail                                                    |
| -------------- | --------------------------------------------------------- |
| Exam code      | AZ-104                                                    |
| Certification  | Microsoft Certified: Azure Administrator Associate        |
| Level          | Associate                                                 |
| Passing score  | 700 out of 1000                                           |
| Question style | Multiple choice, scenario questions, and case studies     |
| Best for       | Admins who deploy, manage, and monitor Azure environments |
| Study approach | Learn how services differ, do labs, drill decision tables |

## Official Skill Areas

Aligned to the official "Skills measured as of April 17, 2026" outline. Always confirm the active outline on the [official study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/az-104) before booking; Microsoft updates it periodically.

Last verified: July 10, 2026.

| Domain | Skill area                                | Weight |
| ------ | ----------------------------------------- | ------ |
| 1      | Manage Azure identities and governance    | 20-25% |
| 2      | Implement and manage storage              | 15-20% |
| 3      | Deploy and manage Azure compute resources | 20-25% |
| 4      | Implement and manage virtual networking   | 15-20% |
| 5      | Monitor and maintain Azure resources      | 10-15% |

## What to Memorize vs Understand

| Memorize                                                              | Understand                                                  |
| --------------------------------------------------------------------- | ----------------------------------------------------------- |
| Built-in roles: Owner, Contributor, Reader, User Access Administrator | How role assignments inherit down scopes                    |
| Storage redundancy options: LRS, ZRS, GRS, RA-GRS, GZRS, RA-GZRS      | Which failure each redundancy level survives                |
| Blob access tiers: hot, cool, cold, archive                           | How lifecycle management moves blobs between tiers          |
| VM availability: sets, zones, scale sets and their SLA logic          | Fault domain vs update domain vs zone                       |
| App Service plan tiers and which features unlock at which tier        | Why slots and autoscale need Standard or higher             |
| NSG rule processing: priority, default rules, inbound vs outbound     | How effective rules combine at subnet and NIC level         |
| Azure Monitor pieces: metrics, logs, alerts, action groups, insights  | Which data goes where and what KQL queries against          |
| Backup vault types: Recovery Services vault vs Backup vault           | Backup vs Site Recovery: restore data vs fail over a region |

## How to Use This Folder

1. Read the five study notes in order; they map one-to-one to the official domains.
2. After each note, do the matching labs so the concepts become portal muscle memory.
3. Work through the common-confusions file and check every pair you mix up.
4. Review the diagrams before practice tests; they anchor inheritance, storage, networking, and monitoring flows.
5. Use the quick reference and exam-day review on the final day.

## Contents

### Coverage Matrix

| File                                  | Use it for                                                                      |
| ------------------------------------- | ------------------------------------------------------------------------------- |
| [Coverage Matrix](coverage-matrix.md) | Mapping every official skill bullet to the note, lab, or cheatsheet covering it |

### Study Notes

| File                                                                            | Use it for                                                            |
| ------------------------------------------------------------------------------- | --------------------------------------------------------------------- |
| [01 - Identities and Governance](study-notes/01-identities-and-governance.md)   | Entra users/groups, SSPR, RBAC, Policy, locks, tags, subscriptions    |
| [02 - Storage](study-notes/02-storage.md)                                       | Storage accounts, redundancy, SAS, firewalls, Files, Blob tiers       |
| [03 - Compute](study-notes/03-compute.md)                                       | ARM/Bicep, VMs, availability, scale sets, containers, App Service     |
| [04 - Virtual Networking](study-notes/04-virtual-networking.md)                 | VNets, peering, routes, NSGs, Bastion, endpoints, DNS, load balancing |
| [05 - Monitoring and Maintenance](study-notes/05-monitoring-and-maintenance.md) | Azure Monitor, Log Analytics, alerts, Network Watcher, Backup, ASR    |

### Cheatsheets

| File                                                                | Use it for                                       |
| ------------------------------------------------------------------- | ------------------------------------------------ |
| [AZ-104 Quick Reference](cheatsheets/az-104-quick-reference.md)     | Last-day revision of limits, tiers, and defaults |
| [AZ-104 Common Confusions](cheatsheets/az-104-common-confusions.md) | Fixing the trap pairs that cause wrong answers   |
| [AZ-104 Service Picker](cheatsheets/az-104-service-picker.md)       | Choosing the right service from scenario wording |
| [AZ-104 Mock Review](cheatsheets/az-104-mock-review.md)             | 30 mixed scenario drills with an answer guide    |
| [AZ-104 Case Studies](cheatsheets/az-104-case-studies.md)           | Multi-step admin judgement practice              |
| [AZ-104 Exam-Day Review](cheatsheets/az-104-exam-day-review.md)     | Final 30-45 minute review before the exam        |
| [Azure CLI Cheatsheet](../azure-cli-cheatsheet.md)                  | Common Azure CLI command families for admin tasks |

### Hands-On Labs

Labs with running compute carry cost warnings; each one cleans up its own expensive resources at the end.

| Lab                                                                                                 | What it teaches                                                    |
| --------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------ |
| [00 - Set Up Your AZ-104 Lab Environment](labs/00-set-up-az104-lab-environment.md)                  | Lab resource group, budget alert, cost safety rules                |
| [01 - Create Users and Groups with Bulk Operations](labs/01-create-users-and-groups.md)             | Users, bulk CSV, guest invites, group types, SSPR                  |
| [02 - Explore Built-in Roles and Build a Custom Role](labs/02-rbac-built-in-and-custom-roles.md)    | Role assignments, scopes, Actions/NotActions, custom roles         |
| [03 - Management Groups and Azure Policy Initiative](labs/03-management-groups-and-policy.md)       | Hierarchy, policy assignment, initiatives, compliance, remediation |
| [04 - Locks, Tags, and Moving Resources](labs/04-locks-tags-and-moving-resources.md)                | Both lock types, inheritance, tagging, resource moves              |
| [05 - Storage Account Redundancy, Tiers, and Lifecycle](labs/05-storage-account-tiers-lifecycle.md) | Redundancy changes, blob tiers, lifecycle rules, soft delete       |
| [06 - SAS Tokens and Stored Access Policies](labs/06-sas-and-stored-access-policies.md)             | Access keys, service SAS, stored access policy revocation          |
| [07 - Azure Files Share and File Sync Concept](labs/07-azure-files-and-file-sync.md)                | SMB shares, port 445, snapshots, File Sync architecture            |
| [08 - Export and Redeploy with ARM Templates and Bicep](labs/08-arm-templates-and-bicep.md)         | Template sections, export, decompile, deploy, idempotency          |
| [09 - Create a VM in an Availability Set](labs/09-create-vm-availability-set.md)                    | Fault/update domains, VM creation, stop vs deallocate              |
| [10 - Resize a VM and Manage Disks](labs/10-vm-resize-and-disks.md)                                 | Sizes, data disks, snapshots, unattached disk costs                |
| [11 - VM Scale Set with Autoscale](labs/11-vm-scale-set-autoscale.md)                               | Orchestration modes, autoscale rule pairs, instance limits         |
| [12 - App Service Plan and Deployment Slots](labs/12-app-service-plan-deployment-slots.md)          | Plan tiers, slots, swaps, scale up vs out                          |
| [13 - Azure Container Instances and AKS Concepts](labs/13-container-instances-and-aks-concepts.md)  | ACI deployment, container groups, ACR SKUs, ACA vs AKS             |
| [14 - Create a VNet with Subnets, NSGs, and ASGs](labs/14-vnet-subnets-nsg-asg.md)                  | CIDR planning, NSG priorities, ASGs, effective rules               |
| [15 - VNet Peering and Network Watcher](labs/15-vnet-peering-and-network-watcher.md)                | Peering options, non-transitivity, IP flow verify, next hop        |
| [16 - Azure DNS Zones](labs/16-azure-dns-zones.md)                                                  | Public/private zones, records, delegation, auto-registration       |
| [17 - Load Balancer and Application Gateway Review](labs/17-load-balancer-and-app-gateway.md)       | LB components, probes, NAT rules, App Gateway wizard walk          |
| [18 - Azure Monitor Metrics, Alerts, and Action Groups](labs/18-monitor-alerts-action-groups.md)    | Metrics Explorer, alert rules, action groups, processing rules     |
| [19 - Log Analytics and KQL Basics](labs/19-log-analytics-and-kql.md)                               | Workspaces, diagnostic settings, KQL query patterns                |
| [20 - Back Up a VM with Azure Backup](labs/20-back-up-vm-azure-backup.md)                           | Vaults, policies, restore options, backup teardown                 |
| [21 - Clean Up All Lab Resources](labs/21-clean-up-all-lab-resources.md)                            | Deletion order, silent billers, cost verification                  |

### Diagrams

| Diagram                                                  | What it teaches                                                       |
| -------------------------------------------------------- | --------------------------------------------------------------------- |
| [AZ-104 Core Diagrams](diagrams/az-104-core-diagrams.md) | Governance inheritance, storage decisions, hub-spoke, monitoring flow |

## What Usually Decides Pass or Fail

Most AZ-104 mistakes come from confusing similar options:

| If you confuse...                                 | Review                                                    |
| ------------------------------------------------- | --------------------------------------------------------- |
| RBAC scope inheritance and Entra directory roles  | Azure resource roles vs directory admin roles             |
| LRS, ZRS, GRS, and GZRS                           | Which failure each redundancy option survives             |
| SAS types and stored access policies              | Account vs service vs user delegation SAS, and revocation |
| Availability sets, zones, and scale sets          | Rack failure vs datacenter failure vs elastic capacity    |
| NSG vs Azure Firewall vs ASG                      | Filtering rules vs managed firewall vs rule grouping      |
| VNet peering vs VPN Gateway vs ExpressRoute       | Azure-to-Azure vs encrypted tunnel vs private circuit     |
| Load Balancer vs Application Gateway              | Layer 4 vs layer 7, and when you need URL routing or WAF  |
| Metrics vs logs, and alert rules vs action groups | What is collected vs what fires vs who gets notified      |
| Azure Backup vs Azure Site Recovery               | Restore data vs fail over to another region               |

## High-Value Exam Traps

| Trap                                                        | Correct thinking                                                                   |
| ----------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| "Give a user permission to assign roles"                    | Owner or User Access Administrator; Contributor cannot manage access               |
| "Guest user needs to manage resources"                      | Guests can hold RBAC roles; being a guest does not block assignment                |
| "Policy blocks a deployment but RBAC allows it"             | Policy still wins; RBAC and Policy are evaluated independently                     |
| "Cheapest storage for rarely accessed data, instant access" | Cool or cold tier, not archive; archive needs rehydration first                    |
| "Revoke a SAS token immediately"                            | Use a stored access policy or rotate the account key; you cannot revoke ad hoc SAS |
| "99.99% VM SLA"                                             | Two or more VMs across availability zones                                          |
| "Deployment slots required"                                 | App Service Standard tier or higher                                                |
| "VNet A peered to B, B peered to C, A cannot reach C"       | Peering is not transitive; add a peering or route through a hub                    |
| "RDP to a VM without a public IP"                           | Azure Bastion                                                                      |
| "Keep PaaS traffic private with a private IP in your VNet"  | Private endpoint, not service endpoint                                             |
| "Query log data with KQL"                                   | Log Analytics workspace via Azure Monitor Logs                                     |
| "Region failover for VMs"                                   | Azure Site Recovery, not Azure Backup                                              |

## Recommended 5-Week Plan

Built for 1-2 hours per day alongside a job. Weeks are weighted by the official domain weights; stretch to 6 weeks by giving the two 20-25% domains a few extra days each.

| Week | Domain focus                                         | Weight          | Do                                                                            |
| ---- | ---------------------------------------------------- | --------------- | ----------------------------------------------------------------------------- |
| 1    | Manage Azure identities and governance               | 20-25%          | Study note 01, labs 00-04, then the identity rows of Common Confusions        |
| 2    | Implement and manage storage                         | 15-20%          | Study note 02, labs 05-07, redo the redundancy and SAS tables from memory     |
| 3    | Deploy and manage Azure compute resources            | 20-25%          | Study note 03, labs 08-13, drill the availability SLA and tier tables         |
| 4    | Implement and manage virtual networking + monitoring | 15-20% + 10-15% | Study notes 04 and 05, labs 14-20, then clean up with lab 21                  |
| 5    | Practice tests and review                            | -               | Diagrams, all four cheatsheets, 2-3 full practice tests, wrong-answer routine |

## Readiness Checklist

Before booking, you should be able to explain these without notes:

- Owner vs Contributor vs User Access Administrator, and where assignments inherit
- Entra directory roles vs Azure RBAC roles
- Policy vs RBAC vs locks vs tags, and what each controls
- LRS vs ZRS vs GRS vs GZRS, and when read access (RA-) matters
- SAS types, stored access policies, and how to revoke access
- Hot vs cool vs cold vs archive tiers and lifecycle management
- Availability set vs availability zone vs scale set, with SLA logic
- App Service plan tiers and which features need which tier
- NSG rule evaluation, ASGs, and effective security rules
- VNet peering vs VPN Gateway, service endpoint vs private endpoint
- Load Balancer vs Application Gateway
- Metrics vs logs, alert rule vs action group, Network Watcher tools
- Azure Backup vs Azure Site Recovery, and the two vault types

## Score Booster Routine

Use this after each practice test:

1. Write down every wrong answer in one line.
2. Label the reason: identity/governance gap, storage gap, compute gap, networking gap, or monitoring gap.
3. Re-read only the matching section in this folder.
4. Add the confused pair to your own notes.
5. Retake a small focused quiz before doing another full mock.

The goal is not to memorize answers. The goal is to stop repeating the same type of mistake.

## Note on Exam Content

These are original study notes. They do not contain real exam questions or leaked content. Use them to understand the concepts, then practice with scenario-based questions and hands-on tasks.

---

Maintained by the team behind [CertGrid](https://certgrid.app). Free practice is available on CertGrid, but these notes are useful on their own.
