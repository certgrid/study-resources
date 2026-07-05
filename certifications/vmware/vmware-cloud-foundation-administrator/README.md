# VMware Cloud Foundation Administrator - Study Cheatsheet

The VMware Cloud Foundation Administrator exam validates your ability to deploy, configure, and operate a VMware Cloud Foundation (VCF) software-defined data center - covering the integrated vSphere, vSAN, and NSX stack, SDDC Manager lifecycle automation, workload domains, networking, and storage. It is aimed at administrators and engineers who manage VCF environments day to day, including bring-up, host commissioning, upgrades, and ongoing operations. The 120-minute exam has roughly 663 questions in the bank, with a scaled passing score of 600.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | VMware Cloud Foundation Administrator |
| Credential | VMware Cloud Foundation Administrator |
| Level | Intermediate |
| Practice mock length | ~70 questions |
| Duration | ~120 minutes |
| Passing score | 600 out of 1000 |
| Notes reviewed | 2026-06-23 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | VCF Architecture | ~19% |
| 2 | Workload Domains | ~18% |
| 3 | Networking with NSX | ~21% |
| 4 | Lifecycle and Operations | ~27% |
| 5 | Storage (vSAN) | ~14% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - VCF Architecture

- VMware Cloud Foundation is a full-stack SDDC platform that bundles vSphere (compute), vSAN (storage), NSX (networking/security), and SDDC Manager (lifecycle) as a single validated, integrated solution.
- The three software-defined pillars are vSphere for compute, vSAN for storage, and NSX for networking and security; SDDC Manager adds lifecycle automation on top.
- SDDC Manager is the central management and automation plane: it orchestrates bring-up, host commissioning, workload-domain provisioning, and lifecycle (LCM) operations like firmware and software upgrades.
- Bring-up is the automated first deployment performed by VMware Cloud Builder, which reads the deployment parameter workbook, validates prerequisites, and bootstraps the management domain.
- The deployment parameter workbook is an Excel (.xlsx) file (convertible to a JSON spec) that supplies all network, host, password, and naming inputs Cloud Builder needs for bring-up.
- The management domain is deployed during bring-up and hosts the core management VMs: vCenter Server, NSX Manager nodes, and SDDC Manager.

### Domain 2 - Workload Domains

- The management domain is the first workload domain, created during Cloud Builder bring-up; it runs a dedicated vSphere cluster with vSAN and hosts vCenter, SDDC Manager, and NSX Manager nodes.
- A Virtual Infrastructure (VI) workload domain is a logically isolated unit for tenant/production workloads, consisting of one or more vSphere clusters, its own dedicated vCenter Server, vSAN storage, and NSX networking.
- Each VI workload domain has its own vCenter Server instance, so a fault, patch, or change in one domain does not affect other domains.
- Before a host can join a workload-domain cluster it must be commissioned in SDDC Manager, which validates hardware compatibility, ESXi version, network/DNS/NTP reachability, and credentials.
- Workload domains deliver isolation (separate security/lifecycle boundaries) plus standardized automated provisioning of compute, storage, and network together as one operation.
- vSAN is the default principal storage for workload domains, though supplemental storage such as NFS, VMFS/FC, or vVols can also be attached.

### Domain 3 - Networking with NSX

- NSX provides VCF's software-defined networking and security: overlay segments using Geneve encapsulation, Tier-0/Tier-1 logical routing, and the Distributed Firewall for micro-segmentation.
- Overlay (Geneve) segments create logical Layer 2 networks decoupled from the physical VLAN/underlay, so VMs on the same segment communicate regardless of which host or rack they reside on.
- A Tier-0 gateway runs on NSX Edge nodes and handles north-south traffic, peering with physical upstream routers via BGP or static routing.
- A Tier-1 gateway sits below Tier-0 and aggregates tenant/segment networks; a common multi-tenant design is a shared Tier-0 upstream with a separate Tier-1 per tenant for isolation.
- The Distributed Firewall (DFW) runs as a kernel module in each ESXi host and enforces policy at every VM's virtual NIC, so even VMs on the same segment are filtered (east-west micro-segmentation).
- Distributed routing also runs in the hypervisor kernel, so east-west traffic between VMs on the same host need not hairpin to a central appliance.

### Domain 4 - Lifecycle and Operations

- SDDC Manager's Lifecycle Management (LCM) module orchestrates patching and upgrades for the entire stack - ESXi, vCenter, NSX, vSAN, and SDDC Manager itself - using validated bundles from the VMware depot.
- A bundle is a curated, digitally signed archive of one or more component updates that have been jointly tested for interoperability; SDDC Manager downloads, stages, and applies it.
- The VCF Bill of Materials (BOM) and interoperability matrix define the exact jointly validated versions of each component, so updates only arrive through bundles that keep the environment supported.
- LCM enforces the correct upgrade order - typically SDDC Manager first, then NSX, then vCenter, then ESXi hosts - so every component always runs a compatible version.
- Upgrade the management domain first, then VI workload domains, following SDDC Manager's validated sequence.
- Before any upgrade, run SDDC Manager prechecks (DNS, NTP, certificate validity, cluster/vSAN health, component connectivity) and confirm current backups of SDDC Manager, vCenter, and NSX exist.

### Domain 5 - Storage (vSAN)

- vSAN is the hyperconverged storage layer that aggregates host-local NVMe/SSD/HDD devices into a single shared, policy-driven datastore for all hosts in the cluster.
- Storage Policy-Based Management (SPBM) assigns storage requirements per VM/VMDK through named policies rather than per-LUN provisioning, and vSAN places data to satisfy each policy.
- Failures to Tolerate (FTT) sets redundancy: FTT=1 survives one host or disk failure using either RAID-1 mirroring or RAID-5 erasure coding.
- RAID-1 mirroring at FTT=1 costs roughly 2x raw capacity and needs 3 hosts; RAID-5 erasure coding keeps FTT=1 with less overhead but requires a minimum of 4 hosts.
- FTT=2 with RAID-1 needs 5 hosts and 3x raw overhead (three copies); RAID-6 erasure coding tolerates two failures with a minimum of 6 hosts.
- A vSAN disk group consists of one cache device (read cache/write buffer) plus 1-7 capacity devices; a host can have up to five disk groups.

## Study tips

- Memorize the SDDC Manager upgrade order (SDDC Manager, then NSX, then vCenter, then ESXi) and the rule that the management domain is always upgraded before VI workload domains.
- Know the vSAN host-count and overhead math cold: RAID-1 FTT=1 needs 3 hosts (2x), RAID-5 needs 4, RAID-1 FTT=2 needs 5 hosts (3x), RAID-6 needs 6 - exam questions hinge on these minimums.
- Distinguish the components: SDDC Manager (lifecycle/automation), Cloud Builder (one-time bring-up), and the parameter workbook (inputs). Questions often test which tool does which job.
- For NSX questions, separate north-south (Tier-0 on Edge, BGP to physical) from east-west (Distributed Firewall in the kernel at each vNIC), and remember overlay needs MTU 1600+ end-to-end.
- Always pair upgrade scenarios with the prerequisites: run SDDC Manager prechecks and confirm valid backups before applying any bundle - these are frequent correct answers.

---

Want the full breakdown? See the complete **[VMware Cloud Foundation Administrator study guide](https://certgrid.app/study-guide/vmware-cloud-foundation-administrator)** and **[free practice questions](https://certgrid.app/practice/vmware-cloud-foundation-administrator)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

