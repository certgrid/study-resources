# NCA: Nutanix Certified Associate - Study Cheatsheet

The Nutanix Certified Associate (NCA) validates foundational knowledge of Nutanix hyperconverged infrastructure, covering core architecture, cluster management with Prism, VM and storage administration, AHV networking, data protection, and monitoring. It is aimed at IT professionals new to Nutanix - administrators, support staff, and sales engineers - who need to demonstrate baseline competency operating an AOS cluster. The 90-minute exam has roughly 60 questions, a passing score of 600 (on a scaled basis), and focuses on operating the platform through Prism rather than deep design or troubleshooting.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | NCA |
| Credential | NCA: Nutanix Certified Associate |
| Level | Associate |
| Practice mock length | ~50 questions |
| Duration | ~90 minutes |
| Passing score | 600 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Nutanix Concepts and Architecture | ~16% |
| 2 | Managing the Cluster with Prism | ~17% |
| 3 | Virtual Machine Management | ~17% |
| 4 | Storage Management | ~16% |
| 5 | Networking and Data Protection | ~19% |
| 6 | Monitoring, Health, and Maintenance | ~16% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Nutanix Concepts and Architecture

- Hyperconverged infrastructure (HCI) collapses compute, storage, and virtualization into a single software-defined layer running on commodity x86 servers, eliminating the separate SAN/NAS array and the dedicated storage network fabric.
- The legacy 3-tier model separates compute servers, a centralized storage array (SAN or NAS), and the storage network (e.g. Fibre Channel switches), with each tier procured, scaled, and administered independently - often by different teams.
- A Nutanix node is a single physical x86 server; a cluster is a logical group of nodes that work together as one system. A block is the chassis that houses one or more nodes.
- Every node runs a hypervisor (AHV, ESXi, or Hyper-V) for user VMs plus a Controller VM (CVM) that provides AOS storage services; together they form the HCI node.
- AOS (Acropolis Operating System) is the core software that runs in the CVMs and delivers the Distributed Storage Fabric plus data services such as snapshots, replication, deduplication, and compression. AOS is hypervisor-agnostic.
- The Distributed Storage Fabric (DSF) aggregates the local SSDs and HDDs from every node into a single, shared, cluster-wide storage pool that any VM on any node can access.

### Domain 2 - Managing the Cluster with Prism

- Prism Element (PE) is the built-in, per-cluster management interface; it can fully manage a single cluster on its own, and Prism Central is optional.
- Prism Central (PC) is a separate, deployable appliance that provides single-pane-of-glass management and cross-cluster monitoring across multiple registered clusters.
- Registering a cluster with Prism Central establishes a management connection so PC can monitor and manage it; unregistering severs that link. If the connection is impaired, the cluster keeps running but PC can no longer manage it.
- The Home (main) dashboard in PE is the default landing page and shows consolidated widgets: Hypervisor Summary, Cluster-wide Controller IOPS, CPU/Memory usage, Storage Summary, Health, and recent Alerts and Events.
- The Cluster-wide Controller IOPS widget reports the combined storage IOPS served by all CVMs, reflecting the real storage workload because every VM's I/O is serviced by the DSF.
- The Hardware view manages the physical layer: a Diagram tab shows blocks and the nodes within them, while the Table tab lists hosts (CPU, memory, model) and disks (capacity, tier, status).

### Domain 3 - Virtual Machine Management

- In the AHV Create VM dialog, the vCPU(s) field sets the number of virtual sockets and Cores per vCPU sets cores each, so total logical processors = vCPUs x cores per vCPU.
- The Memory field is expressed in GiB by default; the value entered is what the guest OS sees as installed RAM.
- Adding a disk with the Allocate on Storage Container option provisions a new empty, thin-provisioned vDisk whose capacity is carved from the selected storage container (space is consumed only as data is written).
- ISO and disk images must first be uploaded to the Image Service (Image Configuration) before they can be attached to a VM.
- To install an OS, attach a disk allocated on a storage container plus a CD-ROM with the installation ISO (via Clone from Image Service); set the boot device order accordingly, then power on.
- After OS installation, eject (unmount) the ISO from the CD-ROM so the VM boots from its disk instead of the installation media.

### Domain 4 - Storage Management

- A storage pool is a logical grouping of all physical storage devices (SSDs and HDDs) across all nodes; a default storage pool containing all cluster disks is created automatically at cluster creation.
- Best practice is to use a single storage pool, because pooling all disks maximizes flexibility and is the recommended default.
- The storage hierarchy is: physical drives -> storage pool -> storage container(s) -> VM vDisks. Containers are logical subdivisions of the pool.
- A storage container is the object where data-reduction and data-protection settings - compression, deduplication, erasure coding, and replication factor - are configured. Creating one requires a name and the pool it is carved from.
- On AHV, a new container is automatically presented and mounted to the hosts as an NFS datastore (on Hyper-V it is presented as an SMB share); no manual mount is needed.
- To apply different data-reduction policies to different workloads, create separate containers (e.g. one with compression for an archive, one without for latency-sensitive SQL).

### Domain 5 - Networking and Data Protection

- On AHV, the default virtual switch vs0 is created automatically and maps to the default Open vSwitch bridge br0 on every host, providing Layer 2 connectivity for VM NICs and the CVM.
- AHV networking is implemented with Open vSwitch (OVS); virtual switches are managed centrally in Prism so configuration applies consistently across all AHV hosts.
- A subnet/network in AHV is created by assigning a VLAN ID (e.g. VLAN ID 30); attaching a VM NIC to it places that VM's traffic on the corresponding VLAN.
- A managed network has AHV-provided IP addressing (IPAM) - configure an IP address pool/range, a default gateway, and the network/prefix - so AHV assigns guest IPs without an external DHCP server.
- An unmanaged network defines only the VLAN ID; VMs must get IPs from an external DHCP server on that VLAN or be assigned static IPs in the guest.
- The physical NICs connecting a host to upstream switches are grouped into an uplink bond for redundancy; supported load-balancing modes include active-backup, balance-slb, and balance-tcp (LACP).

### Domain 6 - Monitoring, Health, and Maintenance

- Alerts are notifications of conditions that may need attention; events are a chronological record of actions or state changes that have occurred in the cluster.
- Alert severities are Info, Warning, and Critical. Critical (red) indicates a problem that can impact availability, data resiliency, or performance (e.g. failed disk, unreachable node, pool nearly full).
- Acknowledging an alert marks it as seen for other admins but does not resolve the underlying condition; resolving/closing it reflects the issue being addressed.
- An alert message includes the title, severity, affected entity, time created, and suggested resolution steps; the Alerts dashboard groups alerts by severity.
- The Health dashboard provides a consolidated, color-coded view (Good/Warning/Critical) of hosts, disks, storage pools, containers, and VMs, driven by background NCC checks.
- NCC (Nutanix Cluster Check) is the built-in health-diagnostic framework included with every cluster; it verifies configuration and stability of cluster components.

## Study tips

- Know the architecture cold: node vs cluster vs block, what the CVM does, what AOS is, and where the Distributed Storage Fabric fits. Many questions test these definitions and the HCI-vs-3-tier contrast directly.
- Distinguish Prism Element (single cluster, always present) from Prism Central (optional, multi-cluster single pane of glass), and know which dashboard/widget shows what (Hardware = physical, Storage = logical, Analysis = charts, Health = NCC results).
- Memorize the storage hierarchy - physical disks -> storage pool -> container -> vDisk - and remember that data-reduction and replication-factor settings live at the container level, with a single pool being the recommended default.
- For AHV networking, be precise about managed (IPAM provides IPs) vs unmanaged (external/static IPs) networks, that vs0 maps to br0, and that uplink trunk ports must allow the VM's VLAN or connectivity breaks.
- Learn the NCC command syntax and result types (PASS/WARN/FAIL/ERR), the difference between alerts and events, and snapshot consistency types (crash-consistent vs application-consistent via NGT). These are common, easily-scored points.

---

Want the full breakdown? See the complete **[NCA study guide](https://certgrid.app/study-guide/nca-nutanix-certified-associate)** and **[free practice questions](https://certgrid.app/practice/nca-nutanix-certified-associate)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

