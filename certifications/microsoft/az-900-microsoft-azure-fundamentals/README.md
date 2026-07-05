# AZ-900: Microsoft Azure Fundamentals - Study Cheatsheet

AZ-900: Microsoft Azure Fundamentals validates foundational knowledge of cloud concepts, core Azure services, and Azure management, governance, and security features. It is aimed at candidates new to the cloud and to non-technical roles (sales, purchasing, management) as well as technical learners starting their Azure journey; no hands-on experience is required. The exam has roughly 40-60 questions, a 45-minute working time, and a passing score of 700 on a 1-1000 scale.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | AZ-900 |
| Credential | AZ-900: Microsoft Azure Fundamentals |
| Level | Beginner |
| Practice mock length | ~40 questions |
| Duration | ~45 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-06-24 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Describe Cloud Concepts | ~32% |
| 2 | Describe Azure Architecture and Services | ~34% |
| 3 | Describe Azure Management and Governance | ~34% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Describe Cloud Concepts

- CapEx is an upfront capital purchase of physical infrastructure (servers, datacenters) that depreciates over time; OpEx is an ongoing operational spend on services as you consume them. Moving to the cloud shifts spending from CapEx to OpEx.
- The consumption-based (pay-as-you-go) model means you pay only for the resources you actually use, with no upfront infrastructure cost and the ability to stop paying when a resource is no longer needed.
- Cloud benefits to know: high availability, scalability, elasticity, reliability, predictability, security, governance, and manageability.
- Scalability comes in two forms: vertical scaling (scaling up/down) adds CPU/RAM to an existing VM; horizontal scaling (scaling out/in) adds or removes more instances.
- Elasticity is the automatic adjustment of resources to match real-time demand, scaling out during peaks and back in when demand drops so you stop paying for unused capacity.
- High availability keeps a system operational despite component or datacenter failures; in Azure it is delivered through features such as Availability Zones and is backed by SLAs.

### Domain 2 - Describe Azure Architecture and Services

- An Azure region is a geographical area containing one or more datacenters deployed within a latency-defined perimeter and connected by a dedicated regional low-latency network; Azure has 60+ regions worldwide.
- Region pairs are two regions within the same geography (typically 300+ miles apart) that provide disaster recovery and data residency; Azure sequences platform updates and prioritizes recovery across paired regions.
- Availability Zones are physically separate datacenter locations within a single region, each with independent power, cooling, and networking; deploying across zones protects against a datacenter-level failure.
- The Azure management hierarchy, from top to bottom, is: management groups, subscriptions, resource groups, and resources. Governance and RBAC applied at a higher scope are inherited downward.
- A resource group is a logical container for related resources; a resource exists in exactly one resource group at a time, and deleting the resource group deletes everything inside it.
- Azure Resource Manager (ARM) is the deployment and management layer; ARM templates (JSON) and Bicep enable infrastructure as code for consistent, repeatable deployments.

### Domain 3 - Describe Azure Management and Governance

- The Azure Pricing Calculator estimates the cost of services you plan to deploy; the Total Cost of Ownership (TCO) Calculator compares the cost of running on-premises workloads versus migrating them to Azure.
- Factors that affect cost include the resource type and configuration, the Azure region where it is deployed, and the volume of data transferred OUT of Azure datacenters (egress); inbound data transfer is generally free.
- Microsoft Cost Management (Cost Management + Billing) lets you monitor, allocate, and analyze cloud spend, set budgets, and create cost alerts; analyzing spend by tag requires applying tags to resources and resource groups first.
- Cost-optimization techniques: right-size or shut down underutilized VMs, configure auto-shutdown/auto-start schedules, use Azure Reserved Instances or savings plans for predictable workloads, and use the Azure Hybrid Benefit for existing licenses.
- Tags are name/value pairs applied to resources and resource groups for organization, cost reporting, and automation; tags are not inherited from a resource group to its resources by default.
- Azure Policy enforces organizational rules and standards over resources; a policy with a deny effect blocks non-compliant deployments (for example, the built-in 'Allowed locations' policy restricts which regions resources can be created in).

## Study tips

- Master the IaaS vs PaaS vs SaaS boundaries and the shared responsibility model; many questions hinge on who (Microsoft or the customer) is responsible for a given task such as OS patching, physical security, or data.
- Memorize the management hierarchy order (management groups > subscriptions > resource groups > resources) and remember that policy and RBAC assignments are inherited downward.
- Distinguish similar concepts that are commonly confused: scaling up vs scaling out, regions vs region pairs vs availability zones, Azure Policy (what can be deployed) vs RBAC (who can act), and VPN Gateway vs ExpressRoute.
- Know which tool does what: Pricing Calculator (estimate planned cost) vs TCO Calculator (on-premises vs Azure) vs Cost Management (track actual spend) vs Azure Advisor (recommendations) vs Defender for Cloud (security posture).
- Read each scenario carefully for the keyword that points to the answer (compliance, automatic, lowest cost, no infrastructure to manage, cannot be deleted); pace yourself, flag uncertain questions, and review them since there is no penalty for guessing.

---

Want the full breakdown? See the complete **[AZ-900 study guide](https://certgrid.app/study-guide/az-900-microsoft-azure-fundamentals)** and **[free practice questions](https://certgrid.app/practice/az-900-microsoft-azure-fundamentals)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

