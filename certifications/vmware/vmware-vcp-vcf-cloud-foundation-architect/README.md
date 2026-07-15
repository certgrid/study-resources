# VMware VCP-VCF: Cloud Foundation Architect - Study Cheatsheet

The VMware VCP-VCF: Cloud Foundation Architect exam validates the ability to translate business and technical requirements into a complete VMware Cloud Foundation design, covering topology choices, NSX and vSAN design, and design for availability, recovery, security, and lifecycle. It is aimed at solution architects and senior engineers who make design decisions rather than perform hands-on administration. Expect scenario questions that ask you to classify requirements, justify topology and component choices, and reason about trade-offs against constraints.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | VMware VCP-VCF |
| Credential | VMware VCP-VCF: Cloud Foundation Architect |
| Level | Intermediate |
| Practice mock length | ~60 questions |
| Duration | ~135 minutes |
| Passing score | 600 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | VCF design principles and requirements gathering | ~13% |
| 2 | Consolidated vs standard topology and multi-domain design | ~20% |
| 3 | NSX overlay and network design within VCF | ~18% |
| 4 | vSAN design (ESA vs OSA, availability zones) | ~15% |
| 5 | Availability, recovery, and security design | ~19% |
| 6 | Lifecycle, monitoring, and capacity design | ~15% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - VCF design principles and requirements gathering

- An assumption is a statement the architect believes true for planning but has not had formally confirmed; if later invalidated, it forces re-evaluation of every design decision that depended on it.
- A requirement is a stated need the design must satisfy, while a constraint is a pre-existing limitation (existing hardware, budget, timeline, rack space) that narrows the set of viable design choices.
- A dependency is a task or deliverable owed by another party that must be completed before the design can proceed, such as DNS, NTP, or an NFS export being available before bring-up.
- Requirements split into functional (what the system does) and non-functional quality attributes; an explicit uptime target is a non-functional requirement and a mandated logging or retention capability is a compliance-driven non-functional requirement.
- Distinguish business outcomes (cost reduction, time-to-market) from technical or project requirements (migration scope, NSX Federation), because they are captured and validated differently.
- Conceptual design deliverables are high-level, vendor-neutral diagrams showing major building blocks such as the management domain and VI workload domains and how they relate, without specific hardware or configuration values.

### Domain 2 - Consolidated vs standard topology and multi-domain design

- A VCF instance is bounded by exactly one SDDC Manager plus the management domain it creates and zero or more VI workload domains it commissions; that SDDC Manager boundary, not physical location, defines the instance and is the exclusive lifecycle authority.
- The consolidated architecture runs management and workloads together in a single cluster, while the standard architecture separates management and workloads into distinct domains.
- Approaching the supported cluster scale ceiling is a clear trigger to expand from consolidated to standard architecture by commissioning hosts and creating a dedicated VI workload domain.
- A vCenter Server and its version are shared by every cluster in a VI workload domain, so independent vCenter upgrade timing and full RBAC or administrative separation require separate workload domains.
- A dedicated VI workload domain provides full compute, storage, and management-plane isolation, which is what compliance boundaries typically demand.
- A dedicated NSX instance for a workload domain is justified when it needs an independent upgrade schedule or strict, policy-driven tenant network segregation.

### Domain 3 - NSX overlay and network design within VCF

- The recommended multi-rack underlay uses routed access with per-rack VLANs and subnets and BGP between leaf and spine, rather than stretching the same Layer 2 VLANs across racks, improving scalability and fault isolation.
- The underlay must provide a consistent 9000-byte MTU across fabric, distributed switch, and host TEP interfaces to absorb Geneve encapsulation overhead, plus redundant top-of-rack switches so each host has uplinks to two separate ToR switches.
- AVN segments attach to a Tier-1 gateway that uplinks to a Tier-0 gateway; the Tier-0 is where NSX peers with the physical fabric via dynamic routing.
- NSX overlay-backed AVN segments fully support vMotion between hosts and clusters sharing the transport zone without the segment existing as a VLAN on the physical network, so VLAN backing is not required.
- VCF creates two AVN segments, a region-specific segment and a cross-region segment, and their routed subnets must be unique and advertised via dynamic routing, requiring coordination with the network team.
- A Tier-0 gateway runs its service router component on Edge nodes; a Tier-1 with no centralized services and no dedicated uplink runs fully distributed and needs no Edge node.

### Domain 4 - vSAN design (ESA vs OSA, availability zones)

- vSAN ESA uses always-on, adaptive, per-object inline compression with minimal performance impact, whereas OSA offers compression only bundled with an optional deduplication toggle enabled as a single cluster-wide setting.
- OSA deduplication and compression require an all-flash cluster, add CPU overhead, are scoped per disk group but toggled cluster-wide, and cannot be set per VM.
- Valid reasons to select OSA over ESA include reusing OSA-certified hardware and wanting classic dedup and compression; the device HCL certification for the specific architecture ultimately drives the choice.
- In OSA a host supports up to 5 disk groups, each with one cache device and up to 7 capacity devices, for a theoretical maximum of 35 capacity devices per host.
- OSA RAID-5 erasure coding requires at least 4 hosts, all-flash disk groups, and FTT=1, while RAID-6 (4+2) carries roughly 50 percent capacity overhead.
- ESA's log-structured design narrows the historical performance gap between erasure coding and mirroring, making space-efficient RAID more viable for demanding workloads.

### Domain 5 - Availability, recovery, and security design

- RPO (data loss tolerance) is driven by whether inter-site bandwidth and latency can keep pace with the data change rate; a data-loss-tolerance statement is an RPO requirement.
- Meeting a near-zero RTO requires reserved standby compute and storage at the recovery site, automated and tested recovery plans, and pre-validated network mappings so failover does not stall.
- Ranking recovery approaches: a stretched cluster with automatic failover gives the lowest RPO and RTO, frequent asynchronous replication achieves a lower RPO than nightly backup, and backup-only recovery has the longest RTO.
- Full management domain recovery relies on coordinated backups of vCenter, NSX Manager, and SDDC Manager together, since no single one restores the whole management plane.
- vCenter Server file-based backup and restore is configured through the Appliance Management Interface (VAMI) on port 5480, independently of the SDDC Manager backup mechanism.
- Proactive HA works with DRS to evacuate VMs from a host that the server vendor's hardware health provider reports as degraded, so the host can be remediated before it actually fails.

### Domain 6 - Lifecycle, monitoring, and capacity design

- Air-gapped or dark-site designs download bundles on an internet-connected system and import them into SDDC Manager through the offline manual bundle upload workflow, preserving BOM-driven orchestration.
- Upgrade planning must validate version skew and interoperability: skip-level upgrades are not assumed supported and must be explicitly validated, and the witness appliance version is coordinated separately from host upgrades.
- Component compatibility is confirmed against the VMware Interoperability Matrix and the target BOM, and for Aria the Aria Suite Lifecycle version support must also be validated.
- Aria Operations HA requires a minimum of 3 analytics cluster nodes (master, master replica, and one data node) so the cluster tolerates the loss of one node without losing data or login access.
- A remote collector group provides redundancy for site-local data collection, keeping monitoring continuous when a collector fails.
- SLA-driven alerting is built from notification rules, group-based policies, and tuned symptoms; severity-based routing (paging or webhook for Critical, digest email for Warning and Info) reduces alert fatigue while preserving SLA response.

## Study tips

- Sort every scenario item into assumption, constraint, requirement, or dependency first; the question often hinges on which category a given statement belongs to.
- When a scenario mentions independent upgrade timing, RBAC separation, or a compliance boundary, the answer is almost always a separate VI workload domain, because vCenter and often NSX are shared within a domain.
- Memorize the stretched cluster numbers: 5 ms RTT between data sites, up to 200 ms RTT to the witness, 20 hosts per site and 40 total, and reserve about 50 percent capacity for failover.
- Know ESA versus OSA cold: ESA compression is always-on and inline, OSA bundles dedup with compression as an all-flash cluster-wide toggle, and the HCL certification for the architecture decides the choice.
- For availability and recovery questions, rank the options by RPO and RTO: stretched cluster with automatic failover is lowest, async replication is middle, and backup-only recovery is highest.

---

Want the full breakdown? See the complete **[VMware VCP-VCF study guide](https://certgrid.app/study-guide/vmware-vcp-vcf-cloud-foundation-architect)** and **[free practice questions](https://certgrid.app/practice/vmware-vcp-vcf-cloud-foundation-architect)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

