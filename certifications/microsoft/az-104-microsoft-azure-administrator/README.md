# AZ-104: Microsoft Azure Administrator - Study Cheatsheet

AZ-104: Microsoft Azure Administrator validates your ability to manage Azure identities and governance, storage, compute, virtual networking, and monitoring. It is aimed at administrators who implement, manage, and monitor an organization's Azure environment day to day, and assumes familiarity with the portal, Azure CLI, PowerShell, ARM/Bicep templates, and core Azure services.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | AZ-104 |
| Credential | AZ-104: Microsoft Azure Administrator |
| Level | Intermediate |
| Practice mock length | ~50 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-07-12 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Manage Azure Identities and Governance | ~23% |
| 2 | Implement and Manage Storage | ~20% |
| 3 | Deploy and Manage Azure Compute Resources | ~21% |
| 4 | Implement and Manage Virtual Networking | ~20% |
| 5 | Monitor and Maintain Azure Resources | ~16% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Manage Azure Identities and Governance

- Azure RBAC is additive - a user's effective permissions are the union of all their role assignments, so a Reader plus Contributor assignment yields Contributor-level access.
- Role assignments inherit downward from management group to subscription to resource group to resource; an assignment at a parent scope applies to all child scopes.
- Owner can manage resources AND assign roles; Contributor can manage resources but cannot grant access; User Access Administrator can only manage role assignments (the least-privilege choice for delegating access management).
- Microsoft Entra dynamic groups use attribute-based membership rules (e.g. user.department -eq "Sales") to add/remove members automatically and require Entra ID P1 licensing.
- Azure Policy with the Deny effect blocks non-compliant resource creation at deployment time; common built-ins include 'Allowed locations', 'Require a tag and its value on resources', and 'Allowed virtual machine size SKUs'.
- Azure Policy assignments cascade to all child scopes, so placing multiple subscriptions under one management group lets a single assignment govern them all, including future subscriptions added later.

### Domain 2 - Implement and Manage Storage

- Storage redundancy tiers: LRS (3 copies in one datacenter), ZRS (across 3 availability zones), GRS (LRS + async copy to paired region), and GZRS (ZRS + paired region); RA-GRS/RA-GZRS additionally expose a read-only secondary endpoint usable during a primary outage.
- A user delegation SAS is signed with Microsoft Entra ID credentials (most secure); service and account SAS are signed with a storage account access key, so regenerating that key is the way to immediately invalidate compromised SAS tokens.
- Blob access tiers are Hot, Cool, Cold, and Archive; default account tier can be Hot or Cool, Archive is set per-blob and is offline (requires rehydration to read), and minimum retention applies before early-deletion charges.
- Blob lifecycle management policies automatically move blobs Hot->Cool->Archive and delete them based on days since last modified or created, reducing storage cost without manual intervention.
- Azure Files supports identity-based authentication by joining the storage account to on-premises AD DS (or Entra Domain Services) so SMB clients use existing Kerberos credentials; you then set share-level RBAC plus NTFS permissions.
- Azure File Sync uses a server endpoint on an on-premises Windows file server and a cloud endpoint pointing to an Azure file share, with cloud tiering to keep hot files local and tier cold files to Azure.

### Domain 3 - Deploy and Manage Azure Compute Resources

- Availability sets protect against rack/hardware failure within a datacenter using fault domains and update domains (99.95% SLA); availability zones span physically separate datacenters in a region for a 99.99% SLA.
- ARM template/Bicep deployments are scoped to the target resource group; deploying the same template to a different resource group creates independent new resources rather than affecting the original.
- Use 'az deployment group create --resource-group RG --template-file main.bicep' to deploy; preview changes safely with the what-if operation (PowerShell -WhatIf or 'az deployment group what-if').
- Convert between formats with 'az bicep decompile --file template.json' (ARM JSON to Bicep) and 'az bicep build' (Bicep to ARM JSON).
- A VM template's required sections include hardwareProfile (VM size), storageProfile (OS disk and image reference), osProfile (credentials/hostname), and networkProfile (NIC references).
- Resizing a VM to a different size is instant if the target size is supported on the current host cluster; otherwise the VM must be stopped (deallocated) and may need redeployment to a cluster that offers the size.

### Domain 4 - Implement and Manage Virtual Networking

- VNet peering must be configured in BOTH directions to connect (one-sided peering shows 'Initiated', not 'Connected') and peered VNets must have non-overlapping address spaces.
- VNet peering is non-transitive: if A peers B and B peers C, A cannot reach C automatically - create a direct A-to-C peering or route through a hub NVA/gateway; use global VNet peering to connect VNets across regions.
- Hub-and-spoke gateway transit lets spokes use the hub's VPN/ExpressRoute gateway: enable 'Allow gateway transit' on the hub peering and 'Use remote gateways' on each spoke peering.
- NSG rules are processed in priority order from lowest number first, and the first matching rule wins; a deny rule at priority 100 beats an allow at priority 200, so give the intended rule a lower number.
- NSGs have default rules including a final deny-all inbound; to permit specific traffic you add allow rules (e.g. TCP 80/443 from Any) at a lower priority number than the defaults (which start at 65000).
- A user-defined route (UDR) with address prefix 0.0.0.0/0 and next hop type Virtual Appliance forces all subnet traffic through an NVA or Azure Firewall; UDRs override Azure's default system routes.

### Domain 5 - Monitor and Maintain Azure Resources

- A Log Analytics workspace stores log data and is required to run KQL (Kusto) queries; diagnostic logs must be sent there before you can query them in the Logs blade.
- Diagnostic settings route platform logs and metrics to up to three destinations simultaneously: Log Analytics workspace (for KQL), a storage account (long-term archive), and an event hub (streaming to external SIEM).
- Metric alerts fire on numeric platform/guest metrics (e.g. Http5xx > 10 over 5 minutes, CPU > 90%); use 'Split by dimensions' to evaluate a single rule per resource (e.g. each VM individually).
- Activity log alerts trigger on control-plane operations recorded in the Activity Log, such as Microsoft.Compute/virtualMachines/delete for VM deletion.
- Action groups define the notification/automation response to an alert: email, SMS, push, webhook, ITSM connector, Logic App, Automation runbook, or Azure Function.
- Common KQL: the ago() function gives now minus a timespan (ago(24h) = 24 hours ago); typical pattern is 'Perf | where TimeGenerated > ago(24h) | summarize avg(CounterValue) by Computer'.

## Study tips

- Watch the scope in RBAC/Policy questions - management group vs subscription vs resource group determines inheritance; the single correct answer is usually the highest scope that satisfies the requirement without over-granting.
- When a question asks for 'least privilege', prefer the narrowest built-in role (e.g. User Access Administrator over Owner) or a custom role over a broad one, even if a broader role technically works.
- Memorize exact numbers and names: /26 for AzureBastionSubnet, 99.95% (availability set) vs 99.99% (availability zones) SLA, the four redundancy tiers, and SAS types - the exam tests precise details.
- For networking troubleshooting, map the symptom to the right Network Watcher tool (IP Flow Verify for NSG, Next Hop for routing, Connection Troubleshoot for connectivity) and remember NSG rules are evaluated lowest-priority-number first.
- Expect multiple-response, drag-and-drop, and case-study questions; read whether a question wants one answer or several, and in case studies note constraints (region, cost, compliance) before choosing.

---

Want the full breakdown? See the complete **[AZ-104 study guide](https://certgrid.app/study-guide/az-104-microsoft-azure-administrator)** and **[free practice questions](https://certgrid.app/practice/az-104-microsoft-azure-administrator)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

