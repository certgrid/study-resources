# NCM-MCI: Nutanix Certified Master - Multicloud Infrastructure - Study Cheatsheet

The NCM-MCI (Nutanix Certified Master - Multicloud Infrastructure) validates advanced, design- and troubleshooting-level expertise across the Nutanix stack: cluster resiliency design, AHV/VM management, advanced networking, storage and performance internals, data protection and DR (Leap, Metro, NearSync), security, monitoring, and lifecycle/upgrade operations. It is aimed at senior administrators, architects, and consultants who already hold or exceed NCP-level skills and must justify design trade-offs and diagnose complex multi-component failures. The 180-minute exam is a live, performance-based lab of roughly 16-20 hands-on scenarios (not multiple-choice questions) and requires a scaled score of 3000 (on a 1000-6000 scale) to pass.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | NCM-MCI |
| Credential | NCM-MCI: Nutanix Certified Master - Multicloud Infrastructure |
| Level | Intermediate |
| Practice mock length | ~60 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Advanced Cluster Management and Design | ~13% |
| 2 | Advanced AHV and VM Management | ~13% |
| 3 | Advanced Networking | ~14% |
| 4 | Advanced Storage and Performance | ~11% |
| 5 | Advanced Data Protection and Disaster Recovery | ~12% |
| 6 | Security and Compliance | ~11% |
| 7 | Advanced Monitoring and Troubleshooting | ~13% |
| 8 | Lifecycle, Upgrades, and Migration | ~13% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Advanced Cluster Management and Design

- Resilient capacity is the fill threshold up to which a cluster can still self-heal back to its configured RF after a fault domain is lost; it equals total usable capacity minus the contribution of the single largest fault domain (node, block, or rack).
- RF2 keeps two data copies and uses three-way Cassandra metadata replication, tolerating one fault-domain failure; RF3 keeps three data copies and uses five-way metadata replication, tolerating two simultaneous fault-domain failures.
- RF3 requires a minimum of five nodes for full protection and consumes roughly a third of raw capacity as additional copies, versus RF2's ~50% overhead (two full copies).
- Block awareness needs a minimum of three blocks for RF2 so a complete second replica can be reconstructed after losing the largest block; with only two blocks both copies of some data can be lost together.
- RF3 block awareness needs enough remaining blocks to hold a full replica set after the largest block fails (more blocks than RF2 block awareness).
- Severe capacity skew between blocks (one block holding disproportionately more data) breaks block awareness because Curator can no longer place a balanced second replica in the surviving blocks.

### Domain 2 - Advanced AHV and VM Management

- Acropolis Dynamic Scheduling (ADS/Lazan) runs roughly every 15 minutes, is contention-driven, and migrates a VM only when the move will actually resolve sustained contention and improve placement.
- ADS evaluates both host CPU and the CVM's storage-controller (Stargate) CPU; high Stargate CPU on a CVM is treated as a hotspot and can trigger migrations even when host CPU is low.
- VM-VM anti-affinity is a soft (preferential) rule: HA can still restart all the VMs even if it forces co-location, and ADS later re-separates them once capacity returns.
- VM-host affinity is a hard rule: a VM pinned exclusively to one host is never restarted elsewhere by HA, which is exactly the behavior license-compliance pinning relies on.
- Pinning a critical VM to two or more hosts (VM-host affinity to a host set) still allows HA restart on an alternate listed host if one fails, balancing strict placement against availability.
- Lazan solves for the minimal-cost set of migrations to clear a hotspot, so it may move a small idle VM rather than the largest consumer to reduce migration overhead.

### Domain 3 - Advanced Networking

- balance-tcp is an active-active OVS bond mode that requires LACP-negotiated link aggregation on the switch; standalone access ports cannot form the LAG and the bond fails to come up.
- active-backup keeps only one uplink active for failover, so total host throughput is capped at a single link's bandwidth regardless of east-west demand.
- balance-slb (source-MAC + VLAN load balancing) needs no LACP/LAG and rebalances flows roughly every minute; the same MAC appearing on two switch ports is expected behavior, so disable static MAC pinning/port-security on those uplinks.
- When uplinks span two switches, an LACP LAG cannot cross chassis, so the switches must run multi-chassis link aggregation (MLAG or vPC).
- An LACP member NIC that is up at the OS level but shows 'not bundled' means the switch port is not negotiating LACP into the same LAG; verify the matching switch port is in the same LAG and actively exchanging LACP frames.
- Any hash-based bond mode places all flows of a single conversation (VM to a given peer) on one uplink, so a single TCP conversation cannot exceed one link's bandwidth.

### Domain 4 - Advanced Storage and Performance

- Oplog coalesces small random writes and acknowledges them quickly from SSD; Stargate bypasses oplog for large sequential writes and sends them straight to the extent store since coalescing offers no benefit.
- Under RF2 a write is acknowledged after the local primary plus one remote replica are persisted to oplog; under RF3 it is acknowledged only after the local copy plus two remote replicas (three durable copies) are persisted.
- The unified cache is multi-tier: hottest data is served from RAM at lowest latency, next-warmest spills to the SSD-backed portion, and a miss is read from the local SSD extent store and inserted into cache for next time.
- Sustained random overwrite that outpaces oplog drain to the extent store fills the oplog, so Stargate applies admission control (throttles writes) to protect durability, especially on hybrid clusters draining to HDD.
- After a CVM is down or a VM migrates, data locality is lost; Stargate re-establishes locality over time by migrating egroups for accessed data to the local node and re-warming the local cache, so initial reads are slower.
- Curator disk balancing redistributes egroups to a newly added node for capacity balance at lower priority than foreground I/O, while Stargate keeps a local primary replica and re-establishes locality on access.

### Domain 5 - Advanced Data Protection and Disaster Recovery

- Synchronous replication acknowledges every write only after it commits at the remote site (RPO 0), so applying it to latency-tolerant tiers adds needless write latency; split tiers into separate protection policies (sync for the database, async for the web tier).
- NearSync uses lightweight snapshots (LWS) recorded in oplog and shipped frequently over an async-capable link to deliver RPOs as low as ~1 minute, bridging the gap when synchronous is impractical at high RTT (e.g., 40 ms).
- NearSync requires all-flash (or a flash tier sized for the LWS store) and compatible AOS versions on both source and remote; it first runs a seeding phase with standard snapshots until the LWS store sustains the sub-15-minute cadence.
- If replication bandwidth cannot keep LWS lag under threshold, NearSync falls back to async and re-attempts when it catches up; the fix is to reduce change rate or increase bandwidth/oplog capacity.
- LWS minute-granular recovery points are retained only for a bounded recent window, after which they roll up into heavier periodic snapshots to control metadata and capacity overhead.
- Metro Availability provides RPO-0 transparent storage failover; Leap Recovery Plans provide orchestrated, sequenced full-site VM failover, and the two are combined when both transparent storage failover and orchestration are required.

### Domain 6 - Security and Compliance

- Native software-based encryption encrypts data inline with AES-256 as Stargate writes to the extent store and works on any qualified drives including non-SED hardware; SED encryption offloads AES to the drive controller with negligible CVM CPU overhead.
- A self-encrypting drive always encrypts its media, but in its default state the authentication key is a well-known default so the drive auto-unlocks at power-on; configuring a key manager replaces that default and provides real protection.
- The Nutanix native (local) key manager runs on the cluster and satisfies data-at-rest encryption with the fewest external dependencies; an external KMS is chosen when the security team must own keys that cluster admins cannot manage or export.
- Encrypted clusters cannot serve data without their keys: if an external KMS is unreachable after a full power outage, Stargate cannot unlock the extent store until the KMS recovers.
- For KMS availability, configure multiple KMIP endpoints (clustered/replicated KMS) across separate failure domains so a single KMS node or site loss does not block key retrieval; in Metro, a single shared KMS in one site can leave the surviving cluster unable to unlock storage.
- Rotating the key encryption key (KEK) re-wraps the existing data encryption keys (DEKs) online; bulk stored data is not decrypted and re-encrypted, so KEK rotation is non-disruptive.

### Domain 7 - Advanced Monitoring and Troubleshooting

- Repeated oplog episode messages with an oplog-full condition mean the write ingest rate is outrunning oplog drain to the extent store; reduce write burst size or scale SSD/throughput.
- Run logbay collect with an explicit --from anchor and --duration that brackets the incident window so only relevant logs and default tags are gathered, keeping the bundle small and the upload fast.
- A Cassandra node in kToBeDetached with failed gossip heartbeats means the dynamic ring changer (autoring) is preparing to detach the unresponsive node to protect metadata quorum, after which data rebuilds to maintain RF.
- Repeated 'Failed to acquire shutdown token' during an upgrade means another node holds the single cluster-wide shutdown token, so the operation correctly serialized and waited rather than risking two simultaneous reboots.
- To confirm reads are coming from slow media, examine read-source statistics for a high proportion served from the HDD/cold tier rather than the unified cache or SSD; a working set that outgrew SSD forces ILM down-migration.
- For a flapping Stargate, read stargate.FATAL and stargate.out for the exact crash reason, then correlate restart timestamps with hardware/disk events in hades and dmesg to find a failing or unresponsive drive.

### Domain 8 - Lifecycle, Upgrades, and Migration

- On a connected cluster LCM auto-updates its framework by downloading the manifest from release-api.nutanix.com; a proxy whitelist that omits that URL blocks the framework auto-update even when general internet access works.
- In a dark-site setup the LCM framework must be supplied locally; a 'framework cannot auto-update' pre-check failure usually means the dark-site bundle was not fully extracted, so the matching lcm_dark_site_<version> files are missing from the web server root.
- Select AOS and firmware entities (e.g., SATADOM/BMC) together in a single LCM update plan so LCM resolves dependencies, orders the work, and batches reboots so each node is taken down only once.
- LCM dependency resolution blocks a plan when a chosen firmware entity declares a minimum AOS the cluster does not meet, even if no AOS upgrade was selected, until AOS is upgraded first or added to the plan.
- LCM only detects and offers updates for components whose hardware-specific modules/payloads exist in the configured source; missing disk/HBA modules mean those entities never appear even though the hardware is present.
- For LCM to auto-recover a stuck node without data unavailability, cluster data resiliency must be OK so survivors can serve the offline node's data, and the other CVMs must reach the affected node's IPMI/BMC to drive it out of phoenix.

## Study tips

- Treat every design question as a capacity-and-fault-domain math problem first: identify the largest fault domain, subtract it to get resilient capacity, then check minimum node counts (5 for RF3, 3 blocks for RF2 block awareness) before evaluating the answer.
- Memorize which affinity rules are hard versus soft: VM-host affinity is hard (blocks HA restart and maintenance-mode evacuation), VM-VM anti-affinity is soft (HA can override it). Most AHV scenario answers hinge on that distinction.
- For networking, map each bond mode to its switch requirement: balance-tcp needs LACP/LAG (MLAG/vPC across two switches), active-backup caps at one link, balance-slb needs no LAG. Then check end-to-end MTU and VLAN trunking on every hop, including inter-switch links.
- Match the DR technology to the RPO/RTO and distance: Metro for RPO-0 transparent failover, Synchronous for RPO-0 within latency limits, NearSync (all-flash, LWS) for ~1-minute RPO over async links, and Leap Recovery Plans for orchestration. RTO is about orchestration, not replication frequency.
- When a question is a troubleshooting scenario, pick the answer that names the correct log or chart for that component (stargate.FATAL/hades/dmesg for storage, Cassandra/genesis for ring changes, read-source stats for tiering, CPU Ready for scheduling) and use Logbay/NCC/LCM pre-checks scoped to the relevant window.

---

Want the full breakdown? See the complete **[NCM-MCI study guide](https://certgrid.app/study-guide/ncm-mci-nutanix-certified-master-multicloud-infrastructure)** and **[free practice questions](https://certgrid.app/practice/ncm-mci-nutanix-certified-master-multicloud-infrastructure)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

