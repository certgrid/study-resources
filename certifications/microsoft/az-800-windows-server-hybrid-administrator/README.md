# AZ-800: Windows Server Hybrid Administrator - Study Cheatsheet

AZ-800 (Windows Server Hybrid Administrator) validates your ability to administer core Windows Server identity, compute, storage, and networking workloads across on-premises and hybrid (Azure-connected) environments. It targets administrators who manage AD DS, Hyper-V, file services, and on-prem servers projected into Azure via Azure Arc, Azure File Sync, and Entra Connect. The exam is 120 minutes with a passing score of 700 on a 1000-point scale.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | AZ-800 |
| Credential | AZ-800: Windows Server Hybrid Administrator |
| Level | Intermediate |
| Practice mock length | ~50 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-06-24 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Manage Windows Servers in a Hybrid Environment | ~24% |
| 2 | Manage Identity and Access | ~22% |
| 3 | Manage Storage and File Services | ~19% |
| 4 | Manage Virtual Machines and Containers | ~20% |
| 5 | Storage and File Services | ~15% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Manage Windows Servers in a Hybrid Environment

- AD DS is the directory service storing all user, computer, and group objects in a forest/domain hierarchy and authenticates logons via Kerberos and NTLM; domain controllers issue the security tokens every domain-joined machine relies on.
- Microsoft Entra Connect (formerly Azure AD Connect) is the sync engine that replicates on-prem AD DS users, groups, and contacts to Microsoft Entra ID, enabling hybrid identity with options like Password Hash Sync, Pass-through Authentication, and federation.
- Install-ADDSForest creates a new forest and Install-ADDSDomainController promotes a server into an existing domain; Install-WindowsFeature AD-Domain-Services -IncludeManagementTools installs the role and tools first.
- A Read-Only Domain Controller (RODC) holds a read-only copy of the directory, caches only permitted credentials via the Password Replication Policy, and is designed for branch or low-physical-security locations.
- A Group Managed Service Account (gMSA) has its password automatically generated and rotated (default 30 days) by AD DS; it requires a KDS root key (Add-KdsRootKey) and supports multiple servers sharing one identity.
- Group Policy Objects (GPOs) link to sites, domains, or OUs and apply settings in LSDOU order (Local, Site, Domain, OU) with the last-applied winning unless blocked or enforced; OUs are the targetable containers for delegation and GPO scope.

### Domain 2 - Manage Identity and Access

- Active Directory Certificate Services (AD CS) provides an on-prem PKI; certificate templates plus autoenrollment driven by Group Policy let clients and servers obtain and renew certificates automatically.
- AD trust types differ by scope: a forest trust links two entire forests (transitive across all domains), while an external trust is a non-transitive link to a single domain in another forest, typically for legacy or selective access.
- New-ADOrganizationalUnit -ProtectedFromAccidentalDeletion $true creates an OU with deletion protection enabled, which sets a Deny on delete that must be cleared before the OU can be removed.
- New-ADServiceAccount with -PrincipalsAllowedToRetrieveManagedPassword specifies which computers (or a security group) can pull a gMSA password; Install-ADServiceAccount then installs it on each host.
- Universal Group Membership Caching (UGMC) is enabled per site to let a non-global-catalog DC cache universal group memberships, allowing logons at branch sites without a local global catalog.
- AD Sites and Subnets steer clients to the nearest DC; site links control replication using a configurable schedule, interval, and cost, and replication between sites can be compressed to save bandwidth.

### Domain 3 - Manage Storage and File Services

- Storage Spaces Direct (S2D) pools local disks across cluster nodes into software-defined storage for hyper-converged infrastructure; it requires Failover Clustering and a minimum of 2 nodes (3+ recommended for two-/three-way mirror resilience).
- Resiliency choices: a two-way mirror tolerates one disk/node failure, a three-way mirror tolerates two, single parity is space-efficient but slower for writes, and mirror-accelerated parity (on ReFS) combines a fast mirror tier with an efficient parity tier.
- ReFS (Resilient File System) offers integrity streams, automatic repair on mirror spaces, and block cloning; it is preferred for Hyper-V and S2D, but NTFS remains required for the boot volume and for features ReFS lacks (such as compression and quotas).
- Data Deduplication breaks files into variable-size chunks and stores each unique chunk once; choose the correct usage type (Default for general file servers, Hyper-V for VDI/virtualization, Backup for backup targets) and schedule optimization during off-peak hours.
- DFS Namespaces (DFS-N) present a single logical UNC path mapping to multiple targets, while DFS Replication (DFS-R) keeps folder contents synchronized between servers for availability and branch scenarios using multi-master replication.
- Storage Replica provides block-level volume replication: synchronous mode guarantees zero data loss between sites within latency limits, asynchronous mode tolerates higher latency for longer distances, and it requires a dedicated, SSD-backed log volume at each end.

### Domain 4 - Manage Virtual Machines and Containers

- Generation 2 Hyper-V VMs use UEFI firmware with Secure Boot, support GPT system disks larger than the 2 TB BIOS/MBR limit, and use synthetic devices; Generation cannot be changed after a VM is created.
- Hyper-V Live Migration moves a running VM between hosts with no downtime by transferring memory and state; enable compression or SMB Direct (RDMA) on a dedicated migration network to speed transfers, and use Shared Nothing Live Migration when there is no shared storage.
- Dynamic Memory assigns RAM on demand using startup, minimum, maximum, and buffer values (Set-VMMemory -DynamicMemoryEnabled $true); it lets you overcommit memory while right-sizing virtual processors to actual workload.
- Dynamically expanding VHDX grows as data is written (thin), while fixed VHDX preallocates full size for predictable performance; differencing disks chain to a parent for scenarios like VDI base images.
- Checkpoints capture VM state and disk for rollback (Checkpoint-VM); production checkpoints use VSS for application consistency and are recommended over standard (saved-state) checkpoints for server workloads.
- Hyper-V virtual switch types: external connects VMs to the physical network via a host NIC, internal connects VMs to each other and the host only, and private connects VMs to each other with no host or physical access.

### Domain 5 - Storage and File Services

- SMB runs over TCP port 445 and underpins UNC paths; modern SMB 3.x adds encryption, signing, Multichannel, and SMB Direct (RDMA), and SMB encryption can be enforced per share for data-in-transit protection.
- Azure File Sync with cloud tiering centralizes the master copy in Azure Files while caching hot data locally; the correct deployment sequence is deploy the Storage Sync Service, install the agent, register the server, create a sync group, then add server endpoints and enable tiering.
- Cloud tiering behavior is governed by the volume free-space policy (target percentage of free space to maintain) and an optional date policy (tier files not accessed within N days); recalled files stream back on access.
- Storage Migration Service (SMS), driven from Windows Admin Center, inventories source servers, transfers data and configuration, and can cut over identity (name and IP) so clients keep using the same path after migration.
- Storage Replica in synchronous mode provides zero-RPO disaster recovery between sites; Test-SRTopology validates prerequisites and New-SRPartnership establishes replication, both requiring a dedicated log volume.
- Azure Data Box is an offline, shipped appliance for transferring very large datasets to Azure when network transfer would be too slow or costly; AzCopy is the command-line tool for online copies to/from Azure storage.

## Study tips

- Expect heavy use of PowerShell cmdlet identification: memorize the verb-noun and key parameters for AD DS (Install-ADDSForest, New-ADServiceAccount), Hyper-V (New-VM, Set-VMMemory, Checkpoint-VM), storage (New-StoragePool, Enable-DedupVolume, New-SRPartnership), and DHCP/DNS cmdlets.
- When a question gives a hybrid scenario, map the requirement to the right Azure service: Azure Arc for governing on-prem servers, Entra Connect for identity sync, Azure File Sync for tiered file storage, and Azure Update Manager for patching across environments.
- Watch for drag-and-drop 'correct sequence' items (Azure File Sync setup, Storage Replica, storage pool creation) and case-study questions; read the constraints (cost, no downtime, branch security) carefully because they dictate the single best answer.
- Distinguish look-alike features under pressure: mirror vs parity vs mirror-accelerated parity, Gen 1 vs Gen 2 VMs, process- vs Hyper-V-isolated containers, external vs internal vs private switches, and forest vs external trusts.
- Remember default behaviors and precedence rules the exam loves: explicit Deny beats Allow, GPO LSDOU processing order, gMSA 30-day password rotation, the PDC Emulator as time/lockout authority, and stopped-deallocated VMs incurring no compute cost.

---

Want the full breakdown? See the complete **[AZ-800 study guide](https://certgrid.app/study-guide/az-800-windows-server-hybrid-administrator)** and **[free practice questions](https://certgrid.app/practice/az-800-windows-server-hybrid-administrator)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

