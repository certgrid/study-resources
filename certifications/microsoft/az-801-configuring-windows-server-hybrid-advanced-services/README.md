# AZ-801: Configuring Windows Server Hybrid Advanced Services - Study Cheatsheet

AZ-801 (Configuring Windows Server Hybrid Advanced Services) validates your ability to secure, ensure high availability for, protect with disaster recovery, migrate, and monitor Windows Server workloads across on-premises and Azure hybrid environments. It targets Windows Server administrators who manage hybrid infrastructure and integrate it with Azure services such as Azure Arc, Azure Monitor, Azure Backup, and Azure Site Recovery. Passing requires a score of 700; the exam runs 120 minutes.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | AZ-801 |
| Credential | AZ-801: Configuring Windows Server Hybrid Advanced Services |
| Level | Intermediate |
| Practice mock length | ~50 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Secure Windows Server | ~22% |
| 2 | Implement and Manage Windows Server High Availability | ~18% |
| 3 | Implement Disaster Recovery | ~20% |
| 4 | Migrate Servers and Workloads | ~21% |
| 5 | Monitor and Troubleshoot Windows Server | ~18% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Secure Windows Server

- Credential Guard uses virtualization-based security (VBS) to isolate LSA secrets in a Hyper-V-backed trustlet, so derived credentials like NTLM hashes and Kerberos TGTs cannot be read by the running OS, defeating pass-the-hash and pass-the-ticket attacks.
- BitLocker provides full-volume AES encryption for data at rest, binding the key to a TPM, startup key, or recovery password so the disk is unreadable if stolen or decommissioned.
- Reduce attack surface by installing Server Core (no GUI), removing unused roles and features, keeping Windows Defender Firewall on with a default-deny inbound stance, and applying security baselines plus timely patching.
- Microsoft Defender for Servers (part of Defender for Cloud) adds EDR, threat intelligence, and continuous monitoring to Windows Server and onboards machines including Azure Arc-connected servers.
- Just Enough Administration (JEA) constrains PowerShell remoting via role-based session configurations that expose only the specific cmdlets and functions an operator needs, enforcing least privilege after a session connects (ideal for jump/RDP servers).
- Just-in-time (JIT) administration and Microsoft Entra Privileged Identity Management (PIM) grant elevated access only for a limited, time-bound window and require approval, reducing standing privilege.

### Domain 2 - Implement and Manage Windows Server High Availability

- Failover Clustering provides automatic failover of clustered roles between nodes by continuously monitoring node and resource health and restarting roles on a healthy node.
- A quorum witness (disk, file share, or cloud) provides a tie-breaking vote that prevents split-brain, ensuring only the partition that can reach the witness keeps the cluster online; a cloud witness uses an Azure storage account.
- Cluster-Aware Updating (CAU) patches cluster nodes in a coordinated rolling manner-draining roles from a node, patching it, returning it to service, then moving to the next-so the cluster stays available.
- Cluster Shared Volumes (CSV) let all cluster nodes simultaneously read and write the same volume, enabling Hyper-V VMs and Scale-Out File Server to share storage without per-role ownership handoffs.
- Storage Spaces Direct (S2D) pools local node disks into a software-defined storage cluster; enable it with Enable-ClusterStorageSpacesDirect and use RDMA-capable networking for east-west traffic.
- For S2D, pick a resiliency type appropriate to node count-three-way mirror for performance-sensitive volumes-and use NVMe/SSD as the built-in cache in front of capacity drives.

### Domain 3 - Implement Disaster Recovery

- Azure Site Recovery (ASR) continuously replicates on-premises and Azure VMs to a secondary Azure region and provides orchestrated failover for regional outages.
- RPO (Recovery Point Objective) defines maximum tolerable data loss and drives replication/backup frequency; RTO (Recovery Time Objective) defines maximum tolerable downtime and drives how fast systems must come back online.
- ASR recovery plans define ordered failover groups for multi-tier apps and can invoke Azure Automation runbooks and custom scripts so dependent components recover in the correct sequence.
- Run periodic ASR test failovers into an isolated network to validate that recovery works and meets RTO/RPO without impacting production replication.
- Hyper-V Replica asynchronously replicates a VM to a replica host; enable it with Enable-VMReplication -VMName VM1 -ReplicaServerName Replica1 -ReplicaServerPort 80 -AuthenticationType Kerberos.
- Hyper-V Replica failover is a two-step replica sequence: Start-VMFailover -VMName VM1 to bring up the replica, then Complete-VMFailover -VMName VM1 to finalize it.

### Domain 4 - Migrate Servers and Workloads

- Azure Migrate is the central tool for discovery, dependency mapping, readiness assessment, sizing, cost estimation, and migration of on-premises servers and VMs to Azure.
- Storage Migration Service (SMS) migrates file shares, data, NTFS permissions, and SMB share configuration from a source server to a new server while preserving share names and access paths; complete it with Start-SmsCutover -Name 'Job1'.
- Common migration strategies include rehost (lift-and-shift VMs as-is with Azure Migrate) and replatform (modernize to Azure managed services where appropriate); choose per workload risk and modernization goals.
- Dependency analysis-agentless via the Azure Migrate appliance or agent-based-maps server-to-server communication so interdependent workloads migrate together in the correct order and nothing breaks.
- Always test the migrated workload (connectivity, application function, performance) in an isolated environment before decommissioning the source server.
- Use Azure Migrate performance-based sizing with a comfort factor tuned to typical utilization, then right-size after migration rather than over-provisioning up front.

### Domain 5 - Monitor and Troubleshoot Windows Server

- Azure Monitor with a Log Analytics workspace centralizes logs and metrics from Azure, Arc, and on-premises servers, and queries them with Kusto Query Language (KQL).
- The modern collection path uses the Azure Monitor Agent (AMA) driven by Data Collection Rules (DCRs); the legacy Log Analytics/MMA agent is deprecated.
- To monitor an Azure Arc-enabled server, create a DCR, associate it with the machine, and install the AzureMonitorWindowsAgent extension (e.g., New-AzConnectedMachineExtension -Name AMAAgent -ExtensionType AzureMonitorWindowsAgent -Publisher Microsoft.Azure.Monitor).
- VM insights builds on the Azure Monitor Agent and Log Analytics to give performance charts plus a dependency map of processes and connections for a VM.
- Azure Monitor alert rules fire when a metric crosses a threshold; route notifications through action groups, and use alert processing rules and smart groups to manage noise and routing.
- Performance Monitor (PerfMon) collects real-time and historical counters; create a Data Collector Set logging to a .blg file for sustained capture, and import a template with logman import -n MyCollector -xml C:\template.xml.

## Study tips

- Watch for the hybrid angle in every domain: the same task often has an on-premises tool and an Azure equivalent (WSUS vs Azure Update Manager, Log Analytics agent vs Azure Monitor Agent, file share witness vs cloud witness)-pick the one that matches the stated environment and constraints.
- Know the exact PowerShell cmdlets and their key parameters cold; AZ-801 frequently shows command-completion or correct-command questions (New-Cluster, Set-ClusterQuorum, Enable-VMReplication, Start-SmsCutover, Move-ADDirectoryServerOperationMasterRole).
- For yes/no and case-study items, evaluate only whether the proposed solution fully meets the stated goal and constraints-do not assume unstated requirements, and remember a partially correct solution still answers 'No, this does not meet the goal.'
- Map every DR scenario back to RPO and RTO: synchronous vs asynchronous, replication frequency, and target VM sizing are almost always cost-versus-recovery trade-offs the question expects you to reason about.
- Prefer the least-privilege, smallest-attack-surface, Microsoft-recommended answer (Server Core, JEA, JIT/PIM, WDAC enforced, default-deny firewall) when multiple options technically work.

---

Want the full breakdown? See the complete **[AZ-801 study guide](https://certgrid.app/study-guide/az-801-configuring-windows-server-hybrid-advanced-services)** and **[free practice questions](https://certgrid.app/practice/az-801-configuring-windows-server-hybrid-advanced-services)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

