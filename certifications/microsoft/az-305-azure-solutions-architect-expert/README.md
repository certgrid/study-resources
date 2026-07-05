# AZ-305: Azure Solutions Architect Expert - Study Cheatsheet

AZ-305 (Azure Solutions Architect Expert) validates your ability to design cloud and hybrid solutions across identity, governance, monitoring, data storage, business continuity, and infrastructure. It is a scenario-heavy, design-focused exam aimed at architects who translate business and technical requirements into Azure designs, and it assumes you already hold the AZ-104 Administrator skills as a prerequisite.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | AZ-305 |
| Credential | AZ-305: Azure Solutions Architect Expert |
| Level | Advanced |
| Practice mock length | ~50 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-06-24 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Design Identity, Governance, and Monitoring Solutions | ~27% |
| 2 | Design Data Storage Solutions | ~24% |
| 3 | Design Business Continuity Solutions | ~22% |
| 4 | Design Infrastructure Solutions | ~27% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Design Identity, Governance, and Monitoring Solutions

- Azure Policy assignments inherit downward through the management group hierarchy, so a policy assigned at a management group automatically applies to every current and future subscription beneath it.
- The Deny effect blocks non-compliant deployments at creation time (preventive); Audit only flags non-compliance in the compliance dashboard; Modify and DeployIfNotExists remediate existing or new resources (Modify needs a managed identity and a remediation task for pre-existing resources).
- Use a custom RBAC role when no built-in role fits; define Actions/NotActions (control-plane) and DataActions/NotDataActions (data-plane), and scope it to subscriptions, resource groups, or management groups via AssignableScopes.
- Microsoft Entra Privileged Identity Management (PIM) provides just-in-time, time-bound, approval-and-MFA-gated activation of privileged Entra and Azure roles, with access reviews and audit history; it requires Entra ID P2.
- Conditional Access policies are evaluated per sign-in and enforce controls like require MFA or require compliant device; always exclude break-glass (emergency access) accounts from CA and PIM enforcement to avoid lockout.
- Pass-through Authentication (PTA) validates passwords directly against on-premises AD without storing password hashes in the cloud; Password Hash Sync (PHS) syncs hashes and enables leaked-credential detection; Seamless SSO uses Kerberos for transparent sign-in on domain-joined devices.

### Domain 2 - Design Data Storage Solutions

- Blob Storage access tiers (Hot, Cool, Cold, Archive) trade storage cost for access cost; lifecycle management policies automatically transition or delete blobs based on age (for example Hot to Cool after 30 days, Cool/Archive after 180-365 days). Archive is offline and requires rehydration before reads.
- Azure Cosmos DB offers five consistency levels: Strong, Bounded Staleness, Session (default), Consistent Prefix, and Eventual; Session keeps reads consistent within a client session while allowing low cross-region latency.
- Cosmos DB multi-region writes (multi-master) enable active-active writes in every region; conflict resolution is Last-Writer-Wins by default or via a custom stored procedure.
- Choosing a good Cosmos DB partition key with high cardinality and even access avoids hot partitions; denormalizing data (for example a feed partitioned by user ID with embedded posts) optimizes read-heavy NoSQL workloads.
- Azure SQL Database Hyperscale supports databases up to 128 TB with fast backups/restores and rapid read-scale replicas; Business Critical adds a local SSD, an Always On replica, and the lowest latency.
- Azure SQL Database elastic pools share DTU/vCore capacity across many databases of varying load - ideal for SaaS multi-tenant designs with one database per tenant.

### Domain 3 - Design Business Continuity Solutions

- RTO is the maximum acceptable downtime (how fast you recover); RPO is the maximum acceptable data loss (how much data you can lose) - design choices map directly to these two targets.
- Availability Zones and Zone-Redundant Storage (ZRS) protect only against a datacenter/zone failure within a single region; they do NOT protect against a full regional outage - that requires multi-region design or GRS.
- A 99.99% (or higher) availability SLA generally cannot be met within a single region; deploy to two or more regions behind Azure Front Door or Traffic Manager for geographic redundancy.
- Azure Site Recovery (ASR) provides continuous replication of Azure VMs, on-premises VMs, and physical servers to a secondary region, with orchestrated and testable failover - good for low-RTO/low-RPO DR without a fully hot standby.
- ASR test failover runs into an isolated virtual network so you can validate the DR plan without impacting production or breaking ongoing replication.
- Azure SQL Database point-in-time restore (PITR) recovers from accidental changes within the configured retention window (1-35 days, default 7); long-term retention (LTR) keeps weekly/monthly/yearly backups for up to 10 years.

### Domain 4 - Design Infrastructure Solutions

- Azure Functions on the Consumption plan scales to zero (no idle cost) and bills per execution; Premium plan adds pre-warmed instances, VNet integration, and no cold start; for event-driven serverless compute it is the lowest-cost option.
- Azure Kubernetes Service (AKS) is the managed orchestrator for containerized microservices; the cluster autoscaler scales nodes, and KEDA adds event-driven (scale-to-zero) autoscaling based on queue length or other metrics.
- Azure Container Instances (ACI) runs short-lived containers serverlessly with per-second billing and no cluster to manage - ideal for brief batch jobs that terminate after running.
- Azure App Service deployment slots enable zero-downtime deploys and blue-green/canary releases; route a percentage of traffic to a staging slot for testing, then swap.
- App Service networking: regional VNet integration handles outbound traffic into a private network, while a private endpoint provides secure inbound access; disable public network access once private endpoints are configured.
- Private endpoints give a service a private IP inside your VNet (Azure SQL, Storage, etc.); after configuring them, disable public network access to eliminate internet exposure.

## Study tips

- Read every requirement keyword: words like 'minimize cost', 'least administrative effort', 'highest availability', or 'RPO = 0' single out the one correct design among several technically working options.
- Watch for the management-group inheritance pattern: assigning policy or RBAC at the right scope (management group vs subscription vs resource group) is a recurring deciding factor.
- Translate stated RTO/RPO numbers into mechanisms: near-zero RPO points to synchronous replication or geo-replication; tolerant RPO/RTO points to Azure Backup or periodic ASR replication.
- Distinguish regional vs global services - availability zones and Application Gateway are regional, while Front Door, Traffic Manager, and Cosmos DB multi-region span regions; a full regional outage requires a global/multi-region answer.
- Many questions are case-study or drag-and-drop matching one Azure service per requirement; eliminate options by ruling out the wrong tier or the wrong networking mode rather than memorizing every feature.

---

Want the full breakdown? See the complete **[AZ-305 study guide](https://certgrid.app/study-guide/az-305-azure-solutions-architect-expert)** and **[free practice questions](https://certgrid.app/practice/az-305-azure-solutions-architect-expert)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

