# Google Cloud Professional Cloud Architect - Study Cheatsheet

The Google Cloud Professional Cloud Architect exam validates your ability to design, develop, and manage robust, secure, scalable, and dynamic cloud solutions on Google Cloud, balancing business and technical requirements. It is aimed at experienced cloud architects who translate stakeholder needs into reliable architectures and guide the technical implementation across compute, storage, networking, security, and operations. The 2-hour, ~50-60 question exam (scaled to a 700 passing score) is scenario-heavy, often referencing case studies, and rewards trade-off thinking over rote service memorization.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | Google Cloud Professional Cloud Architect |
| Credential | Google Cloud Professional Cloud Architect |
| Level | Advanced |
| Practice mock length | ~50 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Designing and Planning a Cloud Solution Architecture | ~21% |
| 2 | Managing and Provisioning a Solution Infrastructure | ~19% |
| 3 | Designing for Security and Compliance | ~19% |
| 4 | Analyzing and Optimizing Processes | ~15% |
| 5 | Managing Implementation | ~11% |
| 6 | Ensuring Solution and Operations Reliability | ~16% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Designing and Planning a Cloud Solution Architecture

- A VPC network is a global resource; subnets are regional resources, each tied to one region with its own IP CIDR range. Resources across regions in the same VPC communicate privately without extra peering.
- Compute choice maps to how much infrastructure you want to manage: Compute Engine (full VM control), GKE (managed Kubernetes/containers), Cloud Run (stateless containers, scales to zero, billed per request), App Engine (fully managed platform).
- Cloud Storage holds unstructured objects (images, video, backups); Cloud SQL serves regional MySQL/PostgreSQL/SQL Server; Cloud Spanner provides horizontally scalable, globally consistent relational data; BigQuery is the serverless analytics data warehouse.
- Shared VPC designates a host project that owns the network and subnets, while service projects attach to it - network admins manage firewall rules, routes, and subnets centrally while teams deploy in their own projects. A common pattern is one host project with separate service projects per environment.
- VPC Network Peering requires a peering configuration on BOTH sides (vpc-a to vpc-b AND vpc-b to vpc-a) and does not allow overlapping IP ranges or transitive routing.
- Overlapping CIDR ranges cannot be routed directly between networks; you must re-IP one side or use Private Service Connect to expose specific endpoints.

### Domain 2 - Managing and Provisioning a Solution Infrastructure

- A regional Managed Instance Group (MIG) spreads VMs across zones and, with an autoscaler, scales on CPU, load-balancing utilization, or custom Cloud Monitoring metrics; autohealing recreates failed instances using a health check.
- The Global external Application Load Balancer is a Layer 7 load balancer with a single anycast IP that routes users to the nearest healthy backend, supports URL-based routing, SSL termination, Cloud CDN, and Google Cloud Armor.
- Internal passthrough Network Load Balancer (Layer 4) handles internal TCP/UDP traffic; choose passthrough NLB for non-HTTP protocols and Application LB for HTTP(S) features.
- Infrastructure as Code via Terraform or Google's native Infrastructure Manager describes desired state declaratively, enabling version control, peer review, and repeatable, consistent provisioning.
- Private Google Access is a subnet-level setting letting VMs with only internal IPs reach Google APIs (Cloud Storage, BigQuery, Pub/Sub) over Google's private network.
- Cloud NAT gives private VMs (no external IP) outbound-only internet access for patches and third-party APIs; it is managed and does not allow unsolicited inbound connections.

### Domain 3 - Designing for Security and Compliance

- Follow least privilege: grant predefined or custom IAM roles scoped to specific services/actions rather than broad primitive roles (Owner/Editor/Viewer), and grant roles to Google Groups rather than individual users.
- Workloads should authenticate using service accounts with least-privilege roles, never user credentials, and avoid downloaded service account keys where possible.
- Workload Identity (and Workload Identity Federation) lets GKE pods and external workloads call Google APIs using short-lived, auto-rotated credentials without exported service account keys; bind the Kubernetes SA to the Google SA.
- VPC Service Controls create a security perimeter around managed services (BigQuery, Cloud Storage) to prevent data exfiltration - data cannot move outside the perimeter even with valid IAM credentials.
- CMEK via Cloud KMS gives you cryptographic control over data at rest - you can rotate, disable, or destroy keys independently of Google; CSEK lets you supply your own raw key material.
- Organization Policy constraints enforce guardrails org-wide, such as restricting resource locations, disabling external IPs (compute.vmExternalIpAccess), and limiting allowed machine types.

### Domain 4 - Analyzing and Optimizing Processes

- Committed Use Discounts (CUDs) give up to ~57% off (most/general-purpose resource types, 3-year) for committing to 1- or 3-year resource usage; ideal for predictable, steady-state baseline workloads.
- Spot VMs (the successor to preemptible VMs) offer up to ~90% off but can be preempted with ~30 seconds notice; use them for fault-tolerant, interruptible batch, HPC, and data pipelines.
- Sustained Use Discounts apply automatically with no commitment when a VM runs for a large fraction of the billing month - no action required.
- A common cost pattern is to cover baseline demand with CUDs and absorb spikes with autoscaled on-demand instances; for batch, use Spot VMs / Dataflow FlexRS for worker pools.
- Recommender / Active Assist surfaces rightsizing and idle-resource recommendations - rightsize VMs down to a smaller machine type matching observed utilization.
- An SLI is a measured indicator (latency, availability, error rate); an SLO is a target/threshold set on an SLI; an SLA is the external contractual commitment with consequences.

### Domain 5 - Managing Implementation

- Cloud Build is Google Cloud's serverless, fully managed CI/CD service that runs build steps from a cloudbuild.yaml to compile code, run tests, build images, push to Artifact Registry, and deploy to Cloud Run, GKE, or App Engine.
- Cloud Build triggers fire on repository events - create one bound to a repo and branch (e.g., --branch-pattern=^main$) to automate builds on push to main.
- Cloud Deploy is the managed continuous delivery service for progressive releases (with promotion, canary strategies, and required manual approvals) to GKE and Cloud Run.
- Speed up pipelines with build caching - cache dependencies/layers via Cloud Storage or use the Kaniko cache for Docker layer reuse.
- Canary deployment shifts a small percentage of traffic to a new version, validates with metrics, then progressively rolls forward or automatically rolls back on regression.
- Cloud Run achieves canary releases through revision traffic splitting - assign weighted percentages across revisions; the Application LB URL map can also weight traffic for canaries.

### Domain 6 - Ensuring Solution and Operations Reliability

- Eliminate zonal single points of failure with a regional MIG distributing instances across multiple zones behind a load balancer; add the MIG as a backend to a backend service with health checks.
- Protect against full regional outages by replicating data and deploying capacity across multiple regions with cross-region failover - a multi-zone design alone does not survive a regional outage.
- Cloud SQL high availability (regional) keeps a synchronous standby in another zone in the same region with automatic failover; it does NOT protect against a full regional outage - use cross-region replicas for that.
- Health checks with autohealing continuously probe instances and automatically recreate VMs that fail, reducing mean time to recovery without manual intervention.
- Take regular, automated disk snapshots (stored redundantly) to recover from data loss; schedule them with a resource policy (e.g., daily snapshot schedule with a retention period).
- Set SLOs from user needs and define SLIs measured on percentiles (p95/p99 latency), not just averages, because averages hide tail latency that real users experience.

## Study tips

- Read scenario questions for the dominant constraint - cost, latency, compliance/data residency, RTO/RPO, or operational overhead - then eliminate options that violate it before comparing the rest.
- Know the compute decision tree cold: Compute Engine vs GKE vs Cloud Run vs App Engine, driven by how much infrastructure the team wants to manage and the workload/scaling model.
- Default to managed and serverless services (Cloud Run, BigQuery, Pub/Sub, Cloud SQL) when the scenario emphasizes minimizing operational overhead, unless a hard requirement forces otherwise.
- Distinguish regional vs multi-region resilience: Cloud SQL HA and regional MIGs survive a zone failure but NOT a region failure - cross-region replication is required for regional DR.
- Memorize the cost-optimization ladder: Spot VMs (interruptible batch), CUDs (steady baseline), Sustained Use Discounts (automatic), rightsizing via Recommender, and storage lifecycle/class transitions.

---

Want the full breakdown? See the complete **[Google Cloud Professional Cloud Architect study guide](https://certgrid.app/study-guide/google-cloud-professional-cloud-architect)** and **[free practice questions](https://certgrid.app/practice/google-cloud-professional-cloud-architect)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

