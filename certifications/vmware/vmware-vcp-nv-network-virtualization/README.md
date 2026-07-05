# VMware VCP-NV: Network Virtualization - Study Cheatsheet

The VMware VCP-NV (Network Virtualization) certification validates your ability to design, install, configure, secure, and troubleshoot VMware NSX network-virtualization environments. It is aimed at network and virtualization administrators who deploy and operate NSX overlay networking, distributed routing and switching, micro-segmentation, and NSX Edge services. The exam has 628 items across five domains, a 130-minute duration, and a scaled passing score of 600.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | VMware VCP-NV |
| Credential | VMware VCP-NV: Network Virtualization |
| Level | Intermediate |
| Practice mock length | ~70 questions |
| Duration | ~130 minutes |
| Passing score | 600 out of 1000 |
| Notes reviewed | 2026-06-24 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Architecture and Technologies | ~21% |
| 2 | NSX Installation and Configuration | ~20% |
| 3 | NSX Switching and Routing | ~21% |
| 4 | NSX Security | ~19% |
| 5 | NSX Troubleshooting and Operations | ~19% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Architecture and Technologies

- NSX uses three planes: the Management Plane (NSX Manager, configuration and policy), the Control Plane (CCP/LCP, computes and distributes logical state), and the Data Plane (transport nodes that forward packets).
- The NSX Manager cluster contains three Manager appliance nodes that collapse the management plane and Central Control Plane (CCP) functions into a single converged appliance for high availability.
- The Central Control Plane (CCP) runs inside the Manager cluster and computes the logical networking and security state, then distributes it to the Local Control Plane (LCP) agent on each transport node.
- The Local Control Plane (LCP) runs on every transport node, communicates with the CCP, and programs the data plane (forwarding tables) on that node.
- NSX overlay traffic is encapsulated with Geneve (Generic Network Virtualization Encapsulation), which uses a variable-length options header to carry metadata, replacing the older fixed VXLAN header.
- Tunnel Endpoints (TEPs) are the IP addresses on transport nodes that originate and terminate Geneve tunnels for east-west overlay traffic between nodes.

### Domain 2 - NSX Installation and Configuration

- Installation begins by deploying the NSX Manager OVA; the Medium form factor (4 vCPU, 16 GB RAM) is the typical production size, and three nodes form the cluster.
- The standard host preparation order is: create IP Pool, create Uplink Profile, create Transport Zone, then configure the Transport Node.
- Configuring a host as a transport node automatically installs the NSX VIBs (kernel modules) and configures the host switch (uplink profile + transport zone assignments).
- A Transport Node Profile applies a consistent transport-node configuration to all hosts in a vSphere cluster, including current and future hosts added to that cluster.
- TEP IP addresses are assigned from an IP Pool configured in NSX Manager (or via DHCP); the Uplink Profile defines the TEP VLAN ID and teaming policy.
- The transport VLAN carrying TEP traffic must be trunked end to end, and MTU must be at least 1600 bytes between all TEPs to accommodate Geneve overhead.

### Domain 3 - NSX Switching and Routing

- NSX uses a two-tier routing model: Tier-0 gateways provide north-south routing to the physical network, and Tier-1 gateways provide tenant-level routing connected upstream to a Tier-0.
- A common multi-tenant design is a single Tier-0 gateway with a separate Tier-1 gateway per tenant for isolation and independent service configuration.
- Every gateway has a Distributed Router (DR) component that runs on all transport nodes where connected workloads exist, providing optimized first-hop (distributed) routing.
- The Service Router (SR) component runs on Edge nodes and handles stateful or centralized services such as NAT, load balancing, VPN, and gateway firewall.
- A segment (logical switch) is a Layer 2 broadcast domain that spans the transport nodes within its transport zone; an overlay segment uses Geneve while a VLAN segment maps to a VLAN ID with no encapsulation.
- Active-active ECMP routing on a Tier-0 requires at least two Edge nodes; both establish BGP sessions and forward north-south traffic in parallel for higher throughput.

### Domain 4 - NSX Security

- The Distributed Firewall (DFW) is a stateful, kernel-level firewall enforced at the vNIC of each VM, applying granular policy to workloads regardless of network location (micro-segmentation).
- DFW rule categories are evaluated top to bottom in this order: Ethernet, Emergency, Infrastructure, Environment, then Application; higher categories are processed before lower ones.
- A common micro-segmentation pattern sets the default rule in the Application category to Drop and places explicit Allow rules above it (positive security / allow-list model).
- Security Groups can use dynamic membership based on NSX security tags applied to workloads, so policy follows the workload automatically as VMs are created or moved.
- If traffic you expect to be blocked is still allowed, check for a higher-priority Allow rule in a category that is evaluated before your Block rule - rule order and category matter.
- Use the Applied To field to scope a policy to specific groups; this reduces rule sprawl and lowers resource (memory/CPU) consumption on transport nodes.

### Domain 5 - NSX Troubleshooting and Operations

- Geneve adds encapsulation overhead, so the physical network MTU must be at least 1600 bytes; an MTU of 1500 causes fragmentation or packet drops on overlay traffic.
- Traceflow is a diagnostic tool that injects a synthetic packet and traces its path through the NSX data plane, showing where (e.g., which DFW rule) a packet is dropped.
- To verify TEP-to-TEP connectivity, run a TEP ping (vmkping with the TEP VMkernel stack and large packet size with do-not-fragment) from the hypervisor CLI between hosts.
- Verify NSX VIBs on an ESXi host with esxcli software vib list and filter for nsx; missing VIBs indicate incomplete host preparation.
- Run upgrades in order: NSX Manager (Upgrade Coordinator) first, then Edge clusters, then host transport nodes - never reverse this sequence.
- When a transport node shows configuration accepted by the management plane but not realized on the data plane, the realized state differs from the intended state and requires investigation of the LCP/CCP path.

## Study tips

- Memorize the three-plane model (Management/Control/Data) and which component lives where: NSX Manager cluster (3 nodes) holds the Management Plane plus the converged CCP, while the LCP runs on each transport node.
- Lock down the two ordered lists the exam loves: the install workflow (IP Pool > Uplink Profile > Transport Zone > Transport Node) and the upgrade order (Manager > Edge clusters > Host transport nodes).
- Know the MTU rule cold: Geneve overhead requires at least 1600 bytes end to end; an MTU of 1500 is a classic cause of overlay drops and a frequent distractor.
- Understand DFW category precedence (Ethernet, Emergency, Infrastructure, Environment, Application) and that a higher allow rule can override a lower block rule - many security questions hinge on rule order.
- For routing questions, separate Tier-0 (north-south to physical, ECMP/BGP) from Tier-1 (tenant), and distinguish the distributed DR (on all hosts) from the centralized SR (on Edge nodes).

---

Want the full breakdown? See the complete **[VMware VCP-NV study guide](https://certgrid.app/study-guide/vmware-vcp-nv-network-virtualization)** and **[free practice questions](https://certgrid.app/practice/vmware-vcp-nv-network-virtualization)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

