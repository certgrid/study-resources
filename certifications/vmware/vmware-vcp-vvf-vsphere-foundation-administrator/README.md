# VMware VCP-VVF: vSphere Foundation Administrator - Study Cheatsheet

The VMware VCP-VVF (VMware vSphere Foundation Administrator) certification validates your ability to deploy, configure, and operate a VMware vSphere Foundation environment, spanning ESXi and vCenter Server, VM and resource management, networking, storage including vSAN, and lifecycle, monitoring, and troubleshooting. It is the current successor to the retired VCP-DCV. It is aimed at administrators and engineers who manage production vSphere infrastructure and want to prove core competency across the modern subscription-based VVF stack.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | VMware VCP-VVF |
| Credential | VMware VCP-VVF: vSphere Foundation Administrator |
| Level | Intermediate |
| Practice mock length | ~60 questions |
| Duration | ~135 minutes |
| Passing score | 600 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | VMware vSphere Foundation architecture and licensing | ~11% |
| 2 | vCenter Server and ESXi installation and configuration | ~19% |
| 3 | Virtual machine and resource management (DRS, HA, vMotion) | ~21% |
| 4 | Networking (standard and distributed switches, VMkernel) | ~16% |
| 5 | Storage (datastores, vSAN, storage policies) | ~18% |
| 6 | Monitoring, lifecycle management, and troubleshooting | ~15% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - VMware vSphere Foundation architecture and licensing

- VVF and VCF are sold as subscriptions rather than perpetual licenses, and VVF is the foundational offering that VCF extends for hybrid extensions such as VMware Cloud on AWS.
- VVF licensing uses a per-core model that requires a minimum of 16 core licenses per physical CPU, and any CPU with more physical cores than that minimum must be licensed for its full actual core count.
- To compute total core licenses, license each CPU at whichever is greater between its actual physical core count and the 16-core minimum, then sum across sockets (for example, a 12-core CPU plus a 20-core CPU equals 16 plus 20, or 36 core licenses).
- VVF bundles the Enterprise Plus feature set, vCenter Server, vSAN capacity, and Aria Operations for Logs, but does not include NSX or Aria Automation.
- VVF includes an entitlement of 0.25 TiB of vSAN capacity per licensed core, and this bundled amount is a floor that additional vSAN capacity can be purchased on top of.
- A subscription license is valid only for its purchased term; if it is not renewed before expiration, the affected assets lose valid license status and behave like an unlicensed or expired-evaluation asset.

### Domain 2 - vCenter Server and ESXi installation and configuration

- A permission is the pairing of a user or group with a role on a specific inventory object, and enabling Propagate to children extends that permission down the hierarchy to descendant objects such as hosts, resource pools, and VMs.
- A permission assigned directly to a user on an object overrides any permission that user inherits through a group on that same object.
- The Read-only role lets a user view an object's state and configuration without changing anything or running tasks.
- Global Permissions are managed in the Administration area at a level above any individual vCenter's inventory, applying across the entire SSO domain.
- Enhanced Linked Mode is enabled by joining vCenter instances to the same SSO domain, is underpinned by vmdir multi-master replication, and supports linking up to 15 vCenter Server instances.
- Repointing a vCenter to a different SSO domain does not carry over local permissions, so they must be recreated afterward.

### Domain 3 - Virtual machine and resource management (DRS, HA, vMotion)

- DRS handles initial VM placement and ongoing load balancing across a cluster using vMotion, and starting in vSphere 7.0 it evaluates balance using each VM's individual DRS score (VM happiness) rather than a cluster-wide standard-deviation metric.
- In Partially Automated DRS mode, DRS applies initial placement automatically but requires administrator approval for migrations, including host evacuations for maintenance mode.
- Priority 1 DRS recommendations are always applied or displayed regardless of the migration threshold setting.
- The default resource share ratio for Low, Normal, and High is 1:2:4, so High receives exactly twice the shares of Normal.
- vSphere HA elects a master host, and subordinate hosts send network heartbeats to the master over the management network, while datastore heartbeats help distinguish an isolated host from a failed one.
- VM Component Protection with a Conservative APD policy only powers off affected VMs when HA is confident they can be restarted successfully on another host.

### Domain 4 - Networking (standard and distributed switches, VMkernel)

- Route based on originating virtual port ID is the default teaming policy on both standard and distributed switches, mapping each vNIC to an uplink by its port ID with a mapping that stays consistent unless a failover occurs.
- In a teaming failover order, Standby adapters carry no traffic during normal operation and activate automatically only after every Active uplink has failed.
- IP hash teaming requires switch-side EtherChannel configuration, unlike originating virtual port ID or explicit failover order policies.
- A new vSphere Standard Switch defaults to 128 virtual ports for connecting VMkernel adapters and VM network adapters.
- Uplink adapters are the physical NICs (vmnics) that connect a switch to the physical network, and using three or more uplinks avoids ambiguity when a beacon-probing failover misses a beacon.
- Network I/O Control (NIOC) allocates and prioritizes bandwidth across traffic types, with real system traffic types including vMotion, vSAN, and Management; a Limit is an always-enforced absolute bandwidth ceiling.

### Domain 5 - Storage (datastores, vSAN, storage policies)

- Unmounting a VMFS datastore is a non-destructive, reversible action that removes it from a host's active view while leaving on-disk data intact, whereas deleting a datastore destroys the VMFS partition and all its data.
- Deleting a shared VMFS datastore destroys the VMFS partition on the LUN itself, so every host that shares that LUN loses the datastore and its data simultaneously.
- A single VMFS-6 extent can be up to 64 TB, and larger datastores are built by spanning multiple extents; VMFS-6 UNMAP space reclamation runs asynchronously in the background and is configurable per datastore.
- vSAN Storage Policy Based Management (SPBM) drives object placement, with valid rules including Failures to tolerate and IOPS limit for object; noncompliance can result from host failures or maintenance and from policy edits that exceed available resources.
- The vSAN Express Storage Architecture (ESA) uses a single per-host storage pool built from NVMe devices with no disk groups and no separate cache tier, relying on a log-structured file system that performs compression and checksums inline on sequential writes.
- vSAN OSA RAID-6 erasure coding requires a minimum of 6 hosts.

### Domain 6 - Monitoring, lifecycle management, and troubleshooting

- Seeing ballooning and hypervisor swapping occur together indicates the host is actively reclaiming memory under real memory contention.
- Active memory estimates a VM's working-set usage, while Consumed memory is the actual host memory granted to the VM.
- Aria Operations aggregates underlying metrics into three headline badges: Health for current state and faults, Risk for projected future capacity or configuration problems, and Efficiency for optimization and reclaimable resources.
- esxtop and resxtop, along with Aria Operations, are used to detect and analyze resource contention, with %RDY and %CSTP being the primary esxtop CPU counters for spotting CPU scheduling contention.
- VM Component Protection (VMCP), configured in a cluster's Failures and Responses settings, provides separate configurable automated responses to Permanent Device Loss (PDL) and All Paths Down (APD) conditions.
- An orphaned VM means vCenter's inventory record no longer matches what the host reports, so the fix is to remove the stale record and re-register the VM from its files if they still exist on disk.

## Study tips

- Practice the per-core license math: license each CPU at the greater of its actual cores or the 16-core minimum, then sum across sockets, and remember VVF includes 0.25 TiB of vSAN capacity per licensed core.
- Know exactly what VVF includes versus VCF: VVF bundles Enterprise Plus, vSAN, vCenter, and Aria Operations for Logs but not NSX or Aria Automation, which affects Tanzu load balancing and hybrid-cloud scenarios.
- Memorize default values, since the exam tests them often: 128 standard-switch ports, 90-day root password age, 1:2:4 share ratio, Round Robin's 1000-I/O threshold, and Opportunistic Encrypted vMotion.
- For vMotion and DRS questions, focus on blockers and modes: unreachable CD/DVD or device media blocks migration, Partially Automated still needs approval for migrations, and EVC masks CPU differences.
- Distinguish backup from diagnostics and recovery actions: file-based backup plus a fresh appliance restore recovers vCenter, support bundles are only for troubleshooting, and unmount is reversible while delete destroys data on the shared LUN.

---

Want the full breakdown? See the complete **[VMware VCP-VVF study guide](https://certgrid.app/study-guide/vmware-vcp-vvf-vsphere-foundation-administrator)** and **[free practice questions](https://certgrid.app/practice/vmware-vcp-vvf-vsphere-foundation-administrator)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

