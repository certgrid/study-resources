# GCP Associate Cloud Engineer - Study Cheatsheet

The Google Cloud Associate Cloud Engineer (ACE) exam validates the hands-on ability to deploy applications, monitor operations, and manage enterprise solutions on Google Cloud, with heavy emphasis on the gcloud CLI, the Console, IAM, and core compute, storage, and networking services. It is a 2-hour, multiple-choice and multiple-select exam (passing score 700 on a scaled basis) aimed at engineers and administrators with at least 6 months of hands-on Google Cloud experience. Expect scenario-based questions that ask you to pick the most cost-effective, secure, and operationally sound option rather than recall of pure definitions.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | GCP Associate Cloud Engineer |
| Credential | GCP Associate Cloud Engineer |
| Level | Associate |
| Practice mock length | ~50 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Setting Up a Cloud Solution Environment | ~19% |
| 2 | Planning and Configuring a Cloud Solution | ~20% |
| 3 | Deploying and Implementing a Cloud Solution | ~24% |
| 4 | Ensuring Successful Operation of a Cloud Solution | ~20% |
| 5 | Configuring Access and Security | ~17% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Setting Up a Cloud Solution Environment

- The resource hierarchy is Organization > Folders > Projects > Resources; IAM policies set at a higher level are inherited by everything below, and child-level policies are additive (you cannot remove an inherited grant lower down).
- An Organization node requires a Cloud Identity or Google Workspace account tied to a verified domain; it is created automatically the first time such a domain user signs in to Google Cloud.
- Use Organization Policy constraints (e.g. gcp.resourceLocations) for centralized governance above IAM; the Resource Locations constraint can restrict resource creation to specific regions such as us-east1 and us-central1.
- constraints/compute.trustedImageProjects restricts which projects images can be created from; constraints/storage.uniformBucketLevelAccess and the public-access-prevention constraint help lock down Cloud Storage.
- Each project has a globally unique, immutable Project ID, a mutable Project Name, and a system-assigned Project Number; billing must be linked to a project before most resources can be created.
- To create or link billing you need Billing Account Administrator; to associate a project with an existing billing account you need the Billing Account User role plus project-level billing permissions.

### Domain 2 - Planning and Configuring a Cloud Solution

- Committed Use Discounts (CUDs) give 1- or 3-year discounts for steady baseline capacity; combine CUDs for baseline with on-demand or autoscaling for burst. Sustained Use Discounts apply automatically to long-running Compute Engine usage.
- Spot VMs (the successor to Preemptible VMs) are deeply discounted but can be reclaimed at any time with a 30-second warning; use them for fault-tolerant, checkpoint-able batch workloads, not stateful services.
- Cloud Storage classes by access frequency: Standard (hot), Nearline (>=30-day min, monthly access), Coldline (>=90-day min, quarterly), Archive (>=365-day min); Object Lifecycle Management automates transitions and deletions.
- Pick managed databases by shape: Cloud SQL (managed MySQL/PostgreSQL/SQL Server, regional, ~64 TB) for relational OLTP; Spanner for global, horizontally scalable, strongly consistent relational; Bigtable for high-throughput wide-column NoSQL; Firestore (Native mode) for document data with real-time listeners and offline support.
- BigQuery is the serverless, fully managed data warehouse for large-scale SQL analytics; you pay for storage plus query bytes scanned (or via slot/capacity pricing).
- Streaming analytics reference pattern: ingest with Pub/Sub, process with Dataflow (Apache Beam), and land results in BigQuery for dashboards; use Dataproc (managed Spark/Hadoop) with autoscaling for existing Spark jobs.

### Domain 3 - Deploying and Implementing a Cloud Solution

- Create Compute Engine VMs with gcloud compute instances create; build reusable instance templates and back MIGs with them, enabling autohealing via a health check plus an autoscaler.
- Deploy serverless containers with gcloud run deploy; set the ingress flag to 'internal' to restrict access, and use environment variables (Console, gcloud, or YAML) for configuration.
- Cloud Run and Cloud Functions reach private VPC resources (such as a Cloud SQL private IP or internal services) through a Serverless VPC Access connector.
- Store and serve container images from Artifact Registry (the successor to Container Registry); create a Docker-format repository and push images there. App images for App Engine deploy via gcloud app deploy.
- Cloud Build automates CI/CD: define steps in cloudbuild.yaml and create a trigger (e.g. on push to the main branch) to build, test, and deploy automatically.
- Event triggers: Cloud Storage object finalize fires on google.cloud.storage.object.v1.finalized; Pub/Sub triggers invoke a function when a message lands on a named topic.

### Domain 4 - Ensuring Successful Operation of a Cloud Solution

- Cloud Monitoring shows resource dashboards (CPU, memory, disk I/O) and hosts alerting policies; install the Ops Agent on VMs to collect memory and detailed disk metrics that are not available by default.
- Cloud Logging centralizes logs; filter by resource type and labels (e.g. resource type dataflow_step plus a Dataflow job ID) and route logs with sinks to Cloud Storage, BigQuery, or Pub/Sub.
- Create log-based metrics from log patterns (e.g. error counts) and attach alerting policies to them; deliver alerts through notification channels such as email, SMS, Slack, or PagerDuty.
- Cloud Monitoring uptime checks probe public HTTP/HTTPS/TCP endpoints from multiple global locations and can trigger alerts when the endpoint is unreachable or returns errors.
- The _Default and _Required log sinks/buckets exist by default; reduce cost and noise by adding exclusion filters (e.g. drop debug logs from non-prod) on the _Default sink. _Required logs cannot be excluded.
- Debug boot/connectivity problems by viewing serial port output: gcloud compute instances get-serial-port-output, or enable interactive serial console access.

### Domain 5 - Configuring Access and Security

- An IAM policy binds members (users, groups, service accounts, domains) to roles on a resource; prefer granting roles to Google Groups, then manage membership in the group, and apply at folder/project level for inheritance.
- Role types: basic (Owner/Editor/Viewer - too broad, avoid in production), predefined (service-scoped, recommended), and custom (least-privilege tailored sets). Follow least privilege and use predefined/custom over basic.
- Service accounts are both an identity and a resource: attach a custom service account with only the needed roles to a VM and use the metadata server for credentials instead of downloading and storing key files.
- IAM Conditions add context to a grant - e.g. an expiry condition gives a contractor access that automatically lapses after 30 days; conditions can also restrict by resource name or request attributes.
- Use IAM Recommender to find and remove excess/unused permissions, and disable or delete service accounts unused for 90+ days after confirming they are not needed.
- Workload Identity is the recommended way for GKE pods to call Google APIs: bind a Kubernetes service account to a Google service account so pods get credentials without node-stored keys.

## Study tips

- Read for the qualifier words - 'most cost-effective', 'least privilege', 'minimal operational overhead', 'fastest', 'highest availability' - these usually decide between two technically valid answers.
- Know the gcloud command structure cold (gcloud <group> <resource> <verb> --flags) and recognize the most common ones for compute instances, IAM, projects/config, run, container, and storage (gsutil/gcloud storage).
- Default to managed and serverless options (Cloud Run, Cloud Functions, GKE Autopilot, Cloud SQL, BigQuery) when the scenario stresses low ops burden, and reserve self-managed Compute Engine/GKE Standard for custom-control requirements.
- Memorize the resource hierarchy and IAM inheritance, the difference between organization policy constraints and IAM, and the storage-class minimum durations (Nearline 30d, Coldline 90d, Archive 365d).
- Manage your 120 minutes: flag and skip scenario-heavy questions on the first pass, answer the quick recall items, then return - and never leave a question blank since there is no penalty for guessing.

---

Want the full breakdown? See the complete **[GCP Associate Cloud Engineer study guide](https://certgrid.app/study-guide/gcp-associate-cloud-engineer)** and **[free practice questions](https://certgrid.app/practice/gcp-associate-cloud-engineer)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

