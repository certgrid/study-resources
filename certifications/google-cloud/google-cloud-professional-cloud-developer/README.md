# Google Cloud Professional Cloud Developer - Study Cheatsheet

The Google Cloud Professional Cloud Developer certification validates the ability to build, test, deploy, and integrate cloud-native applications on Google Cloud. It targets developers who write and run production applications using Google-managed services like Cloud Run, GKE, Cloud Build, Pub/Sub, and Firestore. The 120-minute exam covers designing scalable and resilient applications, building and testing them with proper CI and artifact management, deploying with modern release strategies, and integrating Google Cloud's data, messaging, and observability services.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | Google Cloud Professional Cloud Developer |
| Credential | Google Cloud Professional Cloud Developer |
| Level | Advanced |
| Practice mock length | ~50 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Designing Cloud-Native Applications | ~33% |
| 2 | Building and Testing Applications | ~26% |
| 3 | Deploying Applications | ~19% |
| 4 | Integrating Google Cloud Services | ~22% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Designing Cloud-Native Applications

- In-memory session state on one instance is not shared with other instances an autoscaler adds, so state must be externalized to a shared store like Memorystore for consistent behavior across a scaled-out service.
- Cache-aside (lazy loading) has the app read the cache first and populate it from the database only on a miss, while writes go straight to the database; cache TTL trades data freshness against database refresh load.
- A connection pool reuses a bounded set of persistent connections across requests instead of opening one per request, preventing exhaustion of a backend's client limit such as Redis max connections.
- An API key identifies the calling application or project for usage tracking, billing, and quota without carrying end-user identity; use OAuth 2.0 authorization code grant only when accessing a specific user's private data.
- Enabling Cloud SQL regional high availability provisions an automatic standby that fails over across zones, while a read replica offloads read traffic from the primary without affecting write performance.
- BigQuery is a serverless data warehouse built to scan terabytes efficiently for ad hoc analytical SQL, whereas Bigtable has no native SQL joins and is unsuited to relational reporting; Cloud Spanner uses the TrueTime API for globally ordered timestamps and external consistency across regions.

### Domain 2 - Building and Testing Applications

- A software bill of materials (SBOM) records component names, versions, and license metadata, letting legal teams review compliance across the full dependency tree; CVSS scores describe security risk, not licensing.
- Emulators give fast local development feedback and deterministic CI integration tests without a real project, but they do not reproduce production performance and do not enforce IAM, so permission behavior must be tested against a real project.
- A post-deployment smoke test suite is fast, automated, and limited to a few critical checks like health endpoints, giving quick confidence rather than exhaustive coverage.
- Trunk-based development keeps branches short-lived with a lightweight pull-request check for review, and each release should be tagged with an immutable semantic version rather than a reusable mutable tag like latest.
- Pulling a file from a remote URL during a build breaks reproducibility because the resource can change or disappear, so dependencies should be vendored or pinned to checksum-verified artifacts.
- Cloud Build private worker pools support VPC peering for private network access and let teams choose a machine type for dedicated build workers.

### Domain 3 - Deploying Applications

- A Cloud Run job defines a total task count and a parallelism value that caps how many tasks run simultaneously, distinct from a service's per-instance concurrency.
- Cloud Run scales instances by dividing total concurrent demand by the per-instance concurrency limit, and offers three ingress options (all, internal, internal and Cloud Load Balancing) that control which network sources reach a service.
- A rolling update swaps old instances for new ones incrementally within one environment, blue-green stands up a full parallel environment for a single-cutover switch, and canary phases shift a defined traffic percentage at each step.
- Setting maxUnavailable to 0 prevents dropping below desired capacity during a rollout while a positive maxSurge allows extra pods, and kubectl rollout status reports live rollout progress.
- A Cloud Deploy release is an immutable snapshot binding a specific artifact version to rendered config, and promoting an existing release carries forward its fixed artifact rather than triggering a new build.
- GKE Autopilot fully manages nodes with security hardening by default and bills on pod resource requests, removing node-pool and machine-type management required in GKE Standard.

### Domain 4 - Integrating Google Cloud Services

- Eventarc routes Cloud Storage object events (such as finalize when an object is fully written), Cloud Audit Logs events, and direct Pub/Sub messages as trigger sources.
- Cloud Scheduler's Pub/Sub target publishes to a topic on a cron schedule, while Cloud Tasks suits a single one-time delayed action, created as one task with a schedule time in the future.
- Cloud Tasks queues expose configurable dispatch rate, max concurrent dispatches (in-flight concurrency), and retry limits; cap max concurrent dispatches to protect a target that fails above a simultaneous-request threshold.
- Pub/Sub guarantees message ordering only among messages sharing the same ordering key, not across different keys.
- Workflows can define a subworkflow invoked with different parameters from multiple call sites, use http.get connector calls to fetch external data into a variable, and handle failures with a retry policy in a try block paired with an except block.
- A log sink exports matching log entries to a BigQuery dataset for retention and querying far beyond Cloud Logging's default retention, and GKE forwards container stdout and stderr via a Fluent Bit agent on each node.

## Study tips

- Learn the compute selection decision tree cold: Cloud Run for stateless request-driven containers, Cloud Run jobs for finite batch tasks, GKE Autopilot when you need Kubernetes without node management, and GKE Standard when you must control nodes.
- For auth questions, match the mechanism to the caller: API keys for app-level usage and quota, OAuth 2.0 for delegated user data access, service account impersonation for local dev, and Cloud Identity for workforce sign-in.
- Know the messaging and scheduling tools by their trigger shape: Pub/Sub for fan-out, Eventarc for event routing, Cloud Scheduler for recurring cron, and Cloud Tasks for rate-limited or single delayed dispatches.
- Memorize the release strategies and their cost and risk tradeoffs: rolling reuses infrastructure, blue-green needs a full parallel environment, and canary shifts traffic in validated percentage phases.
- Practice the SLO math and observability stack: compute error budgets from request volume, remember custom.googleapis.com for custom metrics, and know that Error Reporting reads Logging directly while log sinks export to BigQuery.

---

Want the full breakdown? See the complete **[Google Cloud Professional Cloud Developer study guide](https://certgrid.app/study-guide/google-cloud-professional-cloud-developer)** and **[free practice questions](https://certgrid.app/practice/google-cloud-professional-cloud-developer)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

