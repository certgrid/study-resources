# VMware VCAP-VCF: Cloud Foundation Design - Study Cheatsheet

The VMware VCAP-VCF: Cloud Foundation Design exam validates senior, architect-level skill in designing software-defined data centers on VMware Cloud Foundation, covering logical and physical design of management and workload domains and advanced vSphere, vSAN, NSX, and Aria decisions. It is aimed at experienced solution architects and infrastructure designers who must justify every design decision against explicit requirements, constraints, assumptions, and risks. Expect scenario-driven questions that test not just product knowledge but the reasoning and trade-offs behind design qualities such as availability, manageability, performance, recoverability, and security.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | VMware VCAP-VCF |
| Credential | VMware VCAP-VCF: Cloud Foundation Design |
| Level | Intermediate |
| Practice mock length | ~60 questions |
| Duration | ~135 minutes |
| Passing score | 600 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Requirements, constraints, assumptions, and risks | ~14% |
| 2 | Logical and physical design of management and workload domains | ~22% |
| 3 | Advanced NSX overlay/underlay and multi-site design | ~18% |
| 4 | vSAN advanced design (stretched clusters, ESA/OSA, fault domains) | ~15% |
| 5 | Availability, disaster recovery, and business continuity design | ~16% |
| 6 | Operations, monitoring, and lifecycle design | ~15% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Requirements, constraints, assumptions, and risks

- Business drivers are the strategic motivations for a project, such as time to market (agility) or regulatory compliance; they explain why the initiative exists rather than prescribing a technical solution.
- A requirement is a stated, measurable need the design must satisfy; a constraint is an externally imposed limitation the design cannot change; an assumption is an unverified planning condition; and a risk is an uncertain future event with a negative impact.
- A measurable availability target (for example, a stated uptime percentage or the ability to survive a rack failure) is a requirement, not a constraint, and must be treated as something the design has to achieve.
- Functional requirements describe specific capabilities the solution must provide, such as self-service Kubernetes provisioning or Active Directory integration.
- An expectation formed from informal comments and not yet formally confirmed is an assumption, and it must be explicitly validated with the accountable stakeholder before dependent design decisions rely on it.
- Unvalidated assumptions must remain visible as tracked open items; if an assumption is later invalidated, every design decision that depended on it must be reassessed.

### Domain 2 - Logical and physical design of management and workload domains

- Consolidated architecture runs management and tenant workloads on a single shared cluster with one vCenter Server and one NSX Manager, so every lifecycle operation touches both at once; standard architecture keeps a dedicated management domain plus separate VI workload domains, giving stronger isolation and independent lifecycle at the cost of more hardware.
- The management domain must exist and be fully deployed before any VI workload domain can be created.
- Compliance mandates for hard administrative separation, projected growth beyond a single cluster, and the need for independently scheduled patch or upgrade cadences all favor starting with standard architecture rather than consolidated.
- A shared NSX Manager control plane can serve multiple workload domains, but Edge node and gateway design still remains independent per workload domain; strong isolation requirements favor a dedicated NSX Manager instance.
- Clustered application node VMs should use anti-affinity rules to keep nodes on separate hosts, and the cluster needs at least one host more than the number of nodes so vSphere HA can still honor the rule after a host failure.
- Percentage-based admission control is the recommended default for most production clusters; it must reserve at least 1/N of cluster resources per tolerated host failure (rounded up), so reserving one of six hosts is about 16.7 percent and two of six is about 33.3 percent.

### Domain 3 - Advanced NSX overlay/underlay and multi-site design

- A leaf-spine (Clos) fabric connects every leaf to every spine in a full mesh, so adding spines increases aggregate bandwidth and redundancy; Layer 3 ECMP replaces spanning tree, letting all links carry traffic simultaneously.
- Geneve is the NSX overlay encapsulation; its key advantage over the older fixed-header VXLAN is an extensible, variable-length option header, and its transport uses the address family configured for the TEP/underlay (commonly IPv4), not a mandatory IPv6 header.
- Host transport nodes have only local TEPs for intra-location overlay traffic, while Remote Tunnel Endpoints (RTEPs) exist only on Edge transport nodes; therefore cross-location overlay traffic always transits Edge nodes and never flows directly host-to-host between sites.
- The NSX native Load Balancer attaches only to a Tier-1 gateway, never directly to Tier-0; adding a Load Balancer to a Tier-0-only topology requires inserting a Tier-1, which also forces that Tier-1 into Active-Standby mode.
- Tier-0 gateways can run Active-Active with ECMP for north-south scale-out and BGP peering, while Tier-1 centralized services always run Active-Standby with exactly one active Edge node regardless of span; VCF AVN bring-up deploys a two-tier topology with an Active-Active BGP Tier-0 above Tier-1s that host the AVN segments.
- North-south ECMP requires the Tier-0 to run active-active across at least two Edge nodes that peer to distinct top-of-rack switches, with each Edge uplink on its own dedicated uplink VLAN for redundant paths.

### Domain 4 - vSAN advanced design (stretched clusters, ESA/OSA, fault domains)

- A vSAN cluster must be uniformly OSA or uniformly ESA, and this applies to both sites of a stretched cluster; the two architectures cannot be mixed within one cluster.
- vSAN ESA requires an all-NVMe storage pool where every device is a qualified NVMe device in any role; SAS or SATA SSDs cannot participate, even in a capacity-only role.
- The fault-domain minimum follows the 2 times FTT plus 1 rule: FTT=1 needs 3 fault domains and FTT=2 needs 5, so 3 racks cannot provide rack-level FTT=2 protection and would fall back to host-level fault domains.
- Provisioning one fault domain beyond the strict minimum preserves full rebuild and rebalance capability during a rack failure or maintenance without dropping below the policy minimum.
- RAID-1 FTT=1 mirroring stores two full object copies and roughly doubles raw capacity consumption, while RAID-6 uses a 4+2 data-plus-parity scheme requiring a minimum of 6 hosts.
- Erasure coding such as RAID-6 splits each object into more data and parity components than a RAID-1 mirror, so at very large object counts it can approach per-host component limits sooner than mirroring.

### Domain 5 - Availability, disaster recovery, and business continuity design

- Recovery tiers should map replication interval and recovery-plan priority to measured business impact, aligning a critical system such as order processing to a tighter RPO/RTO tier and a lower-priority system such as reporting to a looser tier so investment is proportional to impact.
- Per-tier protection groups allow independent RPO tuning and precise orchestration control, while a single recovery plan can still coordinate the overall failover sequence and dependencies across all groups.
- The two supported VM data replication mechanisms are array-based replication via a Storage Replication Adapter (SRA) and host-based vSphere Replication.
- Zero RPO is physically bounded by inter-site latency; a 60 ms link rules out any synchronous technology, and a 5-minute asynchronous interval can never satisfy a true RPO=0 requirement.
- When replication transfer time is less than the configured interval no backlog accumulates, so the achievable RPO tracks the configured interval (for example, a 6-minute transfer within a 10-minute window yields a 10-minute RPO).
- A recovery test uses a temporary writable copy of replicated data on an isolated network so production is never touched and replication continues, whereas a real failover promotes the actual replica; never testing restores leaves latent failures undiscovered until a real outage.

### Domain 6 - Operations, monitoring, and lifecycle design

- A super metric is justified when a reusable custom formula must combine multiple metrics or objects into a single derived value applied consistently across many objects; it is not warranted when a built-in metric exists or a one-off calculation would suffice.
- The recommended runbook automation pattern defines a threshold as an Aria Operations alert definition linked to a recommendation or action that automatically invokes an Aria Orchestrator workflow, closing the loop without waiting for an operator.
- Immediate response plus durable evidence needs are met by combining webhook or REST outbound notifications for SLA-impacting severities with continuous log forwarding to an external SIEM for searchable, compliant retention.
- Continuous or daily scanning provides near real-time drift visibility while a separately scheduled report cadence (for example quarterly, aligned to a PCI-DSS attestation cycle) reuses that same data as attestation evidence; the two are complementary, not conflicting.
- A separate custom compliance benchmark layers organization-specific controls on top of official STIG content without corrupting the shipped STIG baseline.
- Alert thresholds and escalation priority should be tuned per workload domain by business criticality, with production tuned tighter than test or development to reduce noise in lower tiers while keeping urgent production alerts responsive.

## Study tips

- Master the precise definitions and be ready to classify a statement as a requirement, constraint, assumption, or risk; the exam repeatedly tests whether you can tell an unverified assumption from an externally imposed constraint.
- For every design decision, expect to identify its justification (which requirement it satisfies) and its implication (cost or consequence); a decision with no traceable justification or no implication is a red flag the exam wants you to catch.
- Memorize the core sizing rules cold: vSAN fault domains follow 2 times FTT plus 1 (3 for FTT=1, 5 for FTT=2), RAID-6 needs 6 hosts, stretched-cluster data sites need 5 ms or less RTT, and management domains often need 4 hosts for FTT=1 plus N+1.
- Watch for numeric contradictions between an objective and the proposed technology, such as a 4-hour interval against a 5-minute RPO or a 60 ms link against RPO=0; when the math does not work, the design must be revised regardless of tooling.
- Know the NSX topology rules exactly: the native Load Balancer attaches only to Tier-1, Tier-1 centralized services are always Active-Standby, RTEPs live only on Edge nodes, and Federation exists because Manager consensus needs roughly 10 ms RTT.

---

Want the full breakdown? See the complete **[VMware VCAP-VCF study guide](https://certgrid.app/study-guide/vmware-vcap-vcf-cloud-foundation-design)** and **[free practice questions](https://certgrid.app/practice/vmware-vcap-vcf-cloud-foundation-design)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

