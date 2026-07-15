# Citrix CCE-V: Certified Expert - Virtualization - Study Cheatsheet

The Citrix CCE-V (Certified Expert - Virtualization, exam 1Y0-403) validates the ability to assess, design, and configure advanced Citrix Virtual Apps and Desktops deployments using the Citrix consulting methodology across the user, access, resource, control, and hardware layers. It is aimed at experienced architects and senior engineers who design enterprise CVAD/DaaS solutions rather than just operate them. The 120-minute exam emphasizes design decisions and trade-offs - mapping business requirements to the right FlexCast model, provisioning method, and infrastructure placement - rather than rote feature recall.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | Citrix CCE-V |
| Credential | Citrix CCE-V: Certified Expert - Virtualization |
| Level | Advanced |
| Practice mock length | ~61 questions |
| Duration | ~120 minutes |
| Passing score | 510 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Methodology and Assessment | ~14% |
| 2 | User Layer: Endpoints, Workspace App, and Authentication | ~14% |
| 3 | Access Layer: StoreFront and Citrix Gateway Design | ~15% |
| 4 | Resource Layer: Images and Provisioning | ~14% |
| 5 | Resource Layer: Applications, Profiles, and Printing | ~14% |
| 6 | Control Layer: Controllers, Database, Licensing, and Zones | ~14% |
| 7 | Hardware/Compute, Security, and Operations | ~15% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Methodology and Assessment

- The Citrix consulting methodology has five phases: Define, Assess, Design, Deploy, and Monitor; it is explicitly top-down, capturing business drivers first in Define before any technical decision is made.
- The five architectural layers are User, Access, Resource, Control, and Hardware/Compute (often called the operating layer); every design decision maps to one of these layers.
- The capabilities assessment is a Define-phase activity that translates business drivers and user requirements into the specific capabilities the solution must deliver, then maps each capability to the appropriate layer.
- The Define phase produces the conceptual architecture plus documented requirements, constraints, and assumptions; the Design phase converts that into a detailed technical blueprint with exact product versions, provisioning methods, sizing, and component placement.
- User segmentation groups users by work habits, mobility, and connectivity so each group is mapped to an appropriate FlexCast model, avoiding a one-size-fits-all design.
- FlexCast models include hosted shared (pooled multi-session) desktops, pooled VDI, dedicated/static (persistent) VDI, remote PC access, and streamed/local VM; the model is a Resource-layer decision about what is delivered to the user.

### Domain 2 - User Layer: Endpoints, Workspace App, and Authentication

- Thin clients store no local data, are centrally managed, present a minimal attack surface, and typically have a longer hardware refresh cycle than PCs, making them ideal for large homogeneous task-worker populations.
- Fat (thick) clients suit power users and developers who need substantial local compute, offline capability, or a specialized app that cannot be virtualized; Workspace app is added for occasional published-app access.
- Repurposing converts existing fat-client hardware into managed thin-client-like endpoints by replacing the full OS with a lightweight read-only conversion OS such as IGEL OS or ChromeOS Flex, extending hardware life and removing the local Windows attack surface.
- When choosing a conversion OS for endpoints, confirm it ships a compatible Workspace app build (including Linux HDX optimization for Microsoft Teams) for the required HDX features.
- The Workspace app LTSR (Long Term Service Release) track provides an extended support window with only cumulative updates, avoiding frequent feature-version churn for managed enterprise endpoints.
- Workspace app settings can be centrally managed through the Global App Configuration Service (delivers store URL and client settings to managed and unmanaged devices) and/or ADMX/GPO templates.

### Domain 3 - Access Layer: StoreFront and Citrix Gateway Design

- The Access layer defines how users authenticate to and connect with their resources, including authentication mechanisms, remote-access technology (Citrix Gateway in the DMZ), and single sign-on behavior.
- In a StoreFront server group, configuration is authoritative on one node at a time; changes must be replicated with Propagate Changes (or Publish-STFServerGroupConfiguration), which overwrites configuration on all other members.
- Within a single StoreFront server group, the subscription (Favorites) datastore replicates automatically to all members; two independent deployments each keep their own and require Subscription Synchronization (pull replication) to converge.
- A supported StoreFront HA design places all servers in one server group sharing a single base URL (the load-balanced VIP/FQDN), with the load balancer using a StoreFront service monitor and source-IP or cookie persistence.
- The StoreFront base URL must be set to the load-balanced FQDN, and a certificate valid for that FQDN must be bound on every server in the group.
- To add a server to a group, run Add Server on an existing authoritative server to generate an authorization code, then run Join Existing Server Group with that code on the new server.

### Domain 4 - Resource Layer: Images and Provisioning

- Machine Creation Services (MCS) uses the hypervisor's snapshot capability and storage array to create thin differencing (linked-clone) disks from a single master image, so each VM consumes only its delta blocks.
- Citrix Provisioning (PVS) centralizes the OS in a single vDisk file streamed over the network to many targets; the compact vDisk is easy to replicate to each site's PVS servers.
- PVS can stream the same vDisk to both physical (bare-metal) and virtual targets, whereas MCS requires a supported hypervisor or cloud hosting connection.
- MCS integrates natively with cloud hosting connections (such as Azure) using provider APIs and needs no PXE/TFTP, streaming network, PVS server tier, or vDisk store, making it the simpler cloud choice.
- PVS write-cache options include Cache in device RAM with overflow to hard disk, which absorbs the hottest writes at memory speed and spills cold blocks to a local disk file once RAM is consumed.
- Sizing the PVS server Windows system (standby) cache so the entire vDisk fits in RAM means boot-storm reads are served from memory, dramatically cutting backend storage read IOPS and latency.

### Domain 5 - Resource Layer: Applications, Profiles, and Printing

- An application already installed in the base image is best published as a hosted (seamless) application from a multi-session VDA Delivery Group, so users see only the app window through Workspace app.
- Application Groups logically group related applications and can link to one or more Delivery Groups, centralizing entitlement and supporting AD-group scoping and tag restrictions to control where apps run and who sees them.
- Tag restrictions constrain a published app to a tagged subset of machines (for example, tag the 10 hosts licensed for a finance app and filter the Application Group to those tagged hosts).
- App-V virtualizes an application into an isolated bubble with its own runtime files and registry, letting conflicting legacy runtimes (such as a specific Visual C++ version) coexist on the same multi-session VDA.
- App-V is on a deprecation path, so new packaging efforts should favor MSIX and MSIX app attach, Microsoft's strategic successor.
- MSIX app attach dynamically mounts MSIX-packaged apps stored in VHD, VHDX, or CIM images to a session at runtime, keeping apps separate from the golden image; unassigning the image instantly removes the app.

### Domain 6 - Control Layer: Controllers, Database, Licensing, and Zones

- The Control layer comprises the Delivery Controllers that broker sessions, the SQL Server site database that stores configuration and runtime state, Studio/Director, and the License Server.
- Delivery Controller scalability is roughly 5,000 VDAs per Controller; size for N+1 so surviving Controllers carry the full session load after one fails (for example, four Controllers for ~12,000 sessions).
- VDAs should be configured with multiple Controllers (via the ListOfDDCs registry value or Controller auto-update) so registration distributes and a VDA immediately re-registers with a healthy alternative if one becomes unavailable.
- A VDA selects a Controller at random from its configured list, which statistically distributes registrations evenly across all available Controllers.
- The VDA maintains a persistent TCP connection and heartbeat with its registered Controller over port 80/443 (brokering); loss of that heartbeat triggers re-registration.
- Controller auto-update keeps the VDA's Controller list current automatically, providing resilience to Controller name and address changes without manual reconfiguration.

### Domain 7 - Hardware/Compute, Security, and Operations

- Size each VDA to fit within a single NUMA node and distribute VDAs evenly across both sockets so each VM's memory is satisfied locally, avoiding remote cross-node memory latency.
- NUMA spanning (a VM larger than one node) forces remote memory access and reduces scheduling efficiency, with potential co-stop when many vCPUs must be scheduled simultaneously.
- Asymmetric DIMM population creates unequal NUMA nodes; rebalance physical DIMMs so nodes are symmetric (for example 192 GB per socket) to let the scheduler place VMs without forcing remote access.
- Latency-sensitive, lightly threaded interactive apps such as CAD benefit from higher per-core clock frequency with a moderate core count, favoring single-thread performance over aggregate throughput.
- Simultaneous multithreading (SMT/Hyper-Threading) typically adds only ~20-30% throughput, so size primarily against physical cores and treat SMT as headroom, not a 2x multiplier.
- Smaller hosts make a single failed-host capacity loss a smaller fraction of the total, reducing the spare capacity that must be reserved for N+1.

## Study tips

- Read every scenario as a layered design problem: identify the business driver first, then map each requirement to the User, Access, Resource, Control, or Hardware layer before evaluating the answer options.
- Master the FlexCast decision tree - know exactly which user profile maps to pooled multi-session, pooled VDI, dedicated VDI, or remote PC, because many questions hinge on matching workload to model.
- Know the MCS vs PVS trade-offs cold: cloud and simplicity favor MCS; bare-metal streaming, RAM-cache IOPS offload, and built-in vDisk versioning favor PVS.
- Be ready to do sizing math: subtract host/hypervisor overhead first, size for the logon-storm peak not the average, respect NUMA boundaries, and treat SMT as headroom rather than doubling core capacity.
- Watch for distractors that confuse requirements, constraints, and assumptions, or that pick a technically valid but non-N+1 / non-HA design; the exam rewards the resilient, business-justified choice.

---

Want the full breakdown? See the complete **[Citrix CCE-V study guide](https://certgrid.app/study-guide/citrix-cce-v-certified-expert-virtualization)** and **[free practice questions](https://certgrid.app/practice/citrix-cce-v-certified-expert-virtualization)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

