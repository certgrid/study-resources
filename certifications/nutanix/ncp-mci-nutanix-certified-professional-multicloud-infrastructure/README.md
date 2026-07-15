# NCP-MCI: Nutanix Certified Professional - Multicloud Infrastructure - Study Cheatsheet

The NCP-MCI (Nutanix Certified Professional - Multicloud Infrastructure) validates your ability to deploy, administer, and troubleshoot a Nutanix multicloud environment built on AHV - covering cluster deployment, VM management, networking, distributed storage, data protection and DR, security, monitoring, and lifecycle upgrades. It is aimed at administrators and engineers who manage Nutanix clusters day to day through Prism Element and Prism Central. The exam is 120 minutes with a passing score of 700, and rewards hands-on familiarity with Prism workflows, AOS defaults, and resiliency behavior.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | NCP-MCI |
| Credential | NCP-MCI: Nutanix Certified Professional - Multicloud Infrastructure |
| Level | Advanced |
| Practice mock length | ~60 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Cluster Management and Deployment | ~13% |
| 2 | AHV Virtualization and VM Management | ~12% |
| 3 | Networking | ~12% |
| 4 | Storage Management | ~13% |
| 5 | Data Protection and Disaster Recovery | ~12% |
| 6 | Security | ~13% |
| 7 | Monitoring, Health, and Alerts | ~12% |
| 8 | Lifecycle Management and Upgrades | ~12% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Cluster Management and Deployment

- Foundation discovers unconfigured (factory or wiped) nodes by sending IPv6 link-local multicast on the local segment; because link-local traffic is never forwarded by a router, the Foundation VM and the nodes must be on the same Layer 2 broadcast domain or discovery fails.
- Foundation images bare-metal nodes with the chosen hypervisor (AHV, ESXi, or Hyper-V) plus a selected AOS version and can create the cluster in one workflow; if a single node fails during imaging, re-image only that failed node rather than restarting the whole job.
- Foundation Central runs as a service inside Prism Central for remote, centralized imaging and cluster creation across many sites; edge nodes obtain Foundation Central's address via DHCP option 234 (or are registered through the Foundation Central API).
- A cluster is created from the CLI with 'cluster -s <CVM IPs> create' run from a CVM; the CVMs of the cluster are the targets for cluster operations.
- Redundancy Factor 2 (RF2) keeps two data copies on two different nodes and tolerates one node or drive failure; RF3 keeps three data copies, tolerates two simultaneous failures, requires a minimum of five nodes, and consumes more usable capacity.
- Replication factor is applied at the storage container level (on written data), not at the node level; RF3 on a container additionally requires the cluster to meet the minimum node and fault-tolerance prerequisites.

### Domain 2 - AHV Virtualization and VM Management

- In the AHV VM dialog, vCPU(s) is the number of virtual sockets and Cores Per Socket multiplies it; total logical processors = vCPU(s) x Cores Per Socket (e.g. 4 vCPU x 2 cores = 8, and 1 vCPU x 8 cores = 8).
- A VM's vDisks live in a storage container, so the container's replication factor, compression, deduplication, and erasure-coding settings govern how that VM's data is stored.
- AHV vDisks are thin-provisioned by default, consuming physical space only as data is actually written.
- ISOs are managed through the Image Service (image repository); to install an OS you add a CD-ROM device, mount the ISO, and place the CD-ROM ahead of the (empty) boot disk in the boot order, otherwise firmware tries to boot the blank disk and never reaches the installer.
- After installation, eject the ISO so the CD-ROM is empty (or remove the CD-ROM device) so the VM boots from disk on the next power cycle.
- Secure Boot is a UEFI feature, so the VM must use UEFI firmware and be powered off before Secure Boot can be enabled; UEFI without enforced signature validation boots without checking boot-component signatures.

### Domain 3 - Networking

- During AHV install, AOS automatically creates the default virtual switch vs0 mapped to Open vSwitch bridge br0 on every host, with the uplinks placed in the br0-up bond; this carries CVM, host, and VM traffic.
- A virtual switch is a cluster-wide management construct that maps to an Open vSwitch (OVS) bridge on each host; bond type and uplinks are configured under Settings > Network Configuration > Virtual Switch, and AOS pushes the change to every host consistently.
- Active-Backup is the default bond mode and is fully switch-independent: only one uplink is active at a time and the others stand by for failover, so reduced aggregate bandwidth on a single active link is expected behavior.
- balance-slb (source-load-balancing) is switch-independent and hashes on source MAC to spread different VMs across both uplinks; it needs no LACP or port-channel on the upstream switch.
- balance-tcp provides true per-flow load balancing that lets a single VM exceed one NIC's bandwidth, but it requires an LACP port-channel configured on the upstream switch.
- If you set balance-tcp without a matching switch port-channel, LACP negotiation fails and the host can lose connectivity unless LACP fallback (active-backup fallback) is enabled - configure both ends together and enable fallback during the transition.

### Domain 4 - Storage Management

- A storage pool aggregates all physical disks (SSD and HDD) across the nodes assigned to it, forming the raw capacity from which containers draw; most clusters use a single storage pool.
- A storage container is a logical construct carved from a storage pool where you set replication factor, compression, deduplication, erasure coding, and capacity policies; a vDisk is a logical object inside a container representing a VM's virtual disk.
- On AHV, a newly created container is automatically presented to every host as an available NFS-backed datastore; on ESXi the same container is mounted on the hosts as an NFS datastore.
- Create a container via Storage dashboard > Table view > + Storage Container, specifying name, storage pool, and optional Advanced Settings.
- Advertised Capacity sets the maximum logical size a container can grow to and is enforced as a hard limit - once reached, writes fail with an out-of-space error rather than silently consuming the pool.
- Reserved Capacity pre-allocates physical space from the pool exclusively for that container, so the reserved amount (e.g. 1 TB or 2 TB) is subtracted from the pool's available space and cannot be claimed by other containers.

### Domain 5 - Data Protection and Disaster Recovery

- An async Protection Domain (PD) with a schedule that has no remote site selected produces local-only snapshots retained on the local cluster with no replication.
- A valid async PD requires at least one entity (VM or volume group) added to it plus a schedule defining snapshot frequency and local retention.
- A consistency group bundles one or more entities so they are all captured at a single point in time; a PD can hold multiple consistency groups, but the point-in-time guarantee applies within each consistency group.
- Add a VM's volume group to the same consistency group as the VM so application data on the volume group is captured consistently with the VM; split large sets across multiple consistency groups so each quiesces a smaller, application-aligned set.
- Application-consistent (VSS-based) snapshots require Nutanix Guest Tools (NGT) installed, enabled, and communicating on the VM; without NGT only crash-consistent snapshots are possible.
- For applications without native VSS support, supply custom pre-freeze and post-thaw scripts so the application is quiesced inside the guest before the snapshot.

### Domain 6 - Security

- Authentication to Prism requires both a configured directory (e.g. type Active Directory, with directory URL/LDAP(S), domain, and a binding service account) and a role mapping that associates AD users or groups with a Prism role - the directory alone grants no permissions.
- The directory service account lets the cluster query the directory and resolve users and groups during authentication.
- Built-in roles (Viewer, Operator, etc.) have fixed permission sets that cannot be edited; the built-in Viewer role is read-only across all entities and is the least-privilege choice for full visibility with no mutating ability.
- Custom roles let administrators assemble specific entity permissions (e.g. view/create/update/delete on VM and Image) while withholding others such as networks and storage.
- When a user is granted multiple roles, the effective permissions are the combined (union) permissions of those roles (e.g. Viewer plus Operator).
- Prism Central supports two-factor authentication (2FA), combining standard credentials with a time-based one-time passcode, and SAML 2.0 federation by adding an external IDP (Okta, ADFS, Entra ID) under authentication settings.

### Domain 7 - Monitoring, Health, and Alerts

- The Home (main) dashboard is the default Prism Element landing page and aggregates widgets such as Hypervisor Summary, Storage Summary, VM Summary, Hardware, Data Resiliency Status, cluster-wide Controller IOPS/latency/throughput, and Critical Alerts and Events.
- The Data Resiliency Status widget reports whether the cluster can still tolerate its configured component failures while keeping data redundant; yellow means resiliency is degraded but not yet critical.
- The Analysis page is where you build and retain custom performance charts; add a metric chart, choose the metric, entity, and time range, and the chart persists across sessions.
- An entity chart plots a chosen metric for one or more named entities (e.g. select the Host entity type, Hypervisor CPU Usage metric, and add all three hosts to compare them on one graph).
- In Prism Central, use Manage Dashboards > New Dashboard to create a custom dashboard, arrange widgets from the gallery, and optionally set it as the default view.
- A Top List (top-N) widget ranks entities by a chosen metric in descending order to surface the heaviest resource consumers; you configure it by selecting the entity type and the metric/aggregation.

### Domain 8 - Lifecycle Management and Upgrades

- LCM Inventory scans every node and CVM, queries installed versions of AOS, AHV, BIOS, BMC, disk/HBA/NIC firmware, and software entities (NCC, Foundation, Calm), and compares them against bundles from the configured source; run inventory regularly to refresh the catalog.
- LCM performs firmware and AOS updates in a rolling, one-node-at-a-time fashion to preserve quorum and redundancy; running VMs are live-migrated off the AHV host and the CVM is gracefully shut down before that node is taken down.
- LCM pre-checks run automatically after entities are selected and before any node is modified; they validate data resiliency OK, sufficient free space, no other upgrades in progress, connectivity to the LCM source, CVM memory, and compatibility - and can abort an unsafe update. You can also run pre-checks independently first.
- Dark-site (offline) LCM: download the LCM dark-site framework bundle and the relevant update/release bundles on an internet-connected machine, extract them onto a local web server (HTTP/HTTPS), then point LCM at that URL in LCM Settings (select the local web server option and enter the URL).
- For dark-site issues, verify each CVM can reach the local web server URL and that the bundle is correctly extracted in the served directory, then run a new LCM inventory so the framework and catalog refresh from the dark-site server.
- LCM updates are staged on the node before being applied; if an update is interrupted, LCM auto-resumes the staged operation from where it left off once the node and its CVM recover.

## Study tips

- Memorize the resiliency math: RF2 = 2 copies, tolerates 1 failure; RF3 = 3 copies, tolerates 2 failures and needs a minimum of 5 nodes. Replication factor is set per storage container, and block/rack awareness needs enough balanced blocks/racks.
- Know the bond modes cold: Active-Backup (default, switch-independent, one active link), balance-slb (switch-independent, per-VM by source MAC), and balance-tcp (requires upstream LACP port-channel, true per-flow, enable LACP fallback). Many networking questions hinge on which mode needs switch configuration.
- Distinguish Advertised Capacity (hard maximum logical size) from Reserved Capacity (guaranteed minimum physical space subtracted from the pool), and inline (delay 0) vs post-process (delay > 0) compression - container-setting questions are common.
- For data protection, remember the prerequisites: NGT is required for application-consistent (VSS) snapshots, an async PD needs at least one entity plus a schedule, retention is a rolling count, and replication needs a remote site pointing at the destination cluster.
- Watch for 'powered off' and ordering requirements: Secure Boot/UEFI changes and firmware changes require the VM powered off; upgrade AOS before AHV; Prism Central must be equal to or newer than the AOS clusters it manages; and LCM does everything rolling, one node at a time.

---

Want the full breakdown? See the complete **[NCP-MCI study guide](https://certgrid.app/study-guide/ncp-mci-nutanix-certified-professional-multicloud-infrastructure)** and **[free practice questions](https://certgrid.app/practice/ncp-mci-nutanix-certified-professional-multicloud-infrastructure)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

