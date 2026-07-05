# Google Cloud Professional Cloud DevOps Engineer - Study Cheatsheet

The Google Cloud Professional Cloud DevOps Engineer exam validates your ability to apply Site Reliability Engineering (SRE) principles and build, deploy, and operate reliable services on Google Cloud using CI/CD pipelines, observability, and incident management. It is aimed at DevOps and SRE practitioners who balance feature velocity against reliability through error budgets, automation, and Google Cloud's Operations suite. The exam is 2 hours, contains roughly 50-60 questions, and requires a scaled score of 700 to pass.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | Google Cloud Professional Cloud DevOps Engineer |
| Credential | Google Cloud Professional Cloud DevOps Engineer |
| Level | Advanced |
| Practice mock length | ~50 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-06-23 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Bootstrapping a Cloud Development Environment | ~16% |
| 2 | Building Applications | ~19% |
| 3 | Deploying Applications | ~20% |
| 4 | Integrating Google Cloud Services | ~21% |
| 5 | Managing Deployed Applications | ~23% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Bootstrapping a Cloud Development Environment

- An error budget equals 1 minus the SLO: a 99.9% availability SLO yields a 0.1% error budget, the allowable unreliability the team may 'spend' over a rolling window before slowing risky releases.
- Toil is work that is manual, repetitive, automatable, tactical, devoid of enduring value, and scales linearly with service growth; SRE teams aim to keep toil below 50% of their time.
- When the error budget is exhausted, the policy is to freeze risky feature releases and redirect engineering effort to reliability work until the budget recovers.
- Set the SLO to the lowest level that keeps users happy; each additional 'nine' of reliability dramatically increases cost and effort, and 100% reliability is unrealistic.
- Shared ownership of reliability between developers and SREs aligns incentives so teams build services that are operable, observable, and debuggable, avoiding 'throw it over the wall' handoffs.
- Surplus error budget can be deliberately spent on calculated risk such as faster rollouts, chaos experiments, or planned maintenance.

### Domain 2 - Building Applications

- Cloud Build is Google Cloud's fully managed CI/CD platform; it executes ordered steps defined under the steps: field in cloudbuild.yaml, runs tests, builds Docker images, and can trigger deployments via Cloud Deploy.
- Artifact Registry is the recommended managed registry for container images and language packages (Maven, npm, Python); it supports per-repository IAM and automated vulnerability scanning, superseding the deprecated Container Registry.
- gcloud builds submit --tag builds an image and pushes it to Artifact Registry; gcloud artifacts repositories create --repository-format=docker creates a Docker repo; gcloud auth configure-docker configures Docker auth to Artifact Registry.
- A canary deployment routes a small slice (typically 1-5%) of real traffic to the new version to observe error rate, latency, and business metrics before a full rollout.
- A blue/green deployment keeps two identical environments and switches all traffic at once, enabling near-instant rollback by flipping back to the previous environment.
- Binary Authorization is a deploy-time control for GKE and Cloud Run that blocks images lacking valid cryptographic attestations from trusted authorities, enforcing a trusted supply chain.

### Domain 3 - Deploying Applications

- An SLI is a measured indicator (e.g., the fraction of requests served successfully under 200ms) and an SLO is the target set on that SLI (e.g., 99.9% of requests succeed); the SLI is the measurement and the SLO is the goal.
- The best user-facing SLIs are request success rate and latency as experienced by the user, measured at the serving edge or load balancer, not internal-only signals.
- Burn-rate alerting fires when the error budget is consumed faster than sustainable; multi-window, multi-burn-rate alerts (a fast-burning short window plus a slower long window) reduce false alarms while catching fast degradation early.
- Cloud Run runs stateless containers serverlessly, scales to zero, and supports first-class traffic splitting across revisions by percentage.
- gcloud run deploy --source builds and deploys directly from source; gcloud run deploy --allow-unauthenticated --region deploys a public service; gcloud run services update-traffic --to-revisions splits traffic to a named revision.
- Set Cloud Run ingress to 'internal' (optionally with a Serverless VPC Access connector) to restrict a service to internal-only traffic from within the VPC and internal load balancers.

### Domain 4 - Integrating Google Cloud Services

- Autoscaling automatically matches capacity to load: GKE Horizontal Pod Autoscaler scales pods on CPU or custom metrics, Cloud Run scales instances on request concurrency, and Managed Instance Groups autoscale Compute Engine VMs.
- The GKE Cluster Autoscaler adds nodes when pods cannot be scheduled and removes underutilized nodes after safely evicting pods, keeping the node pool right-sized.
- Improve GKE resilience by spreading pods across zones and nodes with pod anti-affinity in multi-zone clusters, and set resource requests and limits so the scheduler places pods well and prevents noisy neighbors.
- Memorystore for Redis is a fully managed in-memory cache; caching hot reads with a TTL aligned to data update frequency cuts database load and serves data in microseconds.
- Cloud CDN caches static content at edge points of presence in front of the global HTTP(S) load balancer, reducing user latency and origin load; cache behavior is driven by Cache-Control headers.
- Cloud Pub/Sub is fully managed asynchronous messaging that decouples producers from consumers, smoothing traffic spikes; Cloud Tasks also provides reliable async task execution with per-task control.

### Domain 5 - Managing Deployed Applications

- A blameless postmortem documents the timeline and contributing factors of an incident and produces tracked action items without attributing fault, creating psychological safety so engineers report issues honestly.
- Recurrence is prevented only by completing owned, tracked postmortem action items with due dates; these fix the root cause, add earlier-detection monitoring, and automate remediation.
- Effective incident response assigns a clear Incident Commander plus defined roles (communications lead, scribe, operations responders) and follows a structured communication plan to avoid chaos.
- Pre-written, validated runbooks for known failure modes reduce mean time to recovery (MTTR) by encoding diagnosis, remediation, rollback, and escalation steps any on-call engineer can follow.
- During an active incident, restoring service availability takes priority over cost optimization; mitigate first (e.g., roll back, add capacity), then investigate root cause afterward.
- Roll back a Cloud Run regression by routing 100% of traffic to a previous known-good revision using gcloud run services update-traffic --to-revisions, since prior revisions are retained.

## Study tips

- Almost every question is a scenario that pits reliability against velocity; default to SRE doctrine, error budgets, SLOs based on user-facing SLIs, and toil reduction rather than ad hoc heroics.
- Know the deployment strategies cold: canary (gradual percentage of real traffic), blue/green (instant switch and rollback), and rolling updates, and which GCP service implements each (Cloud Run traffic splitting, GKE, Cloud Deploy).
- Memorize the Operations suite mapping: Cloud Monitoring = metrics/alerts/dashboards, Cloud Logging = logs/sinks, Cloud Trace = distributed traces, Error Reporting = grouped exceptions, Cloud Profiler = performance.
- When a question asks for the 'most secure' or 'recommended' authentication, prefer keyless options: Workload Identity Federation for CI/CD and Application Default Credentials with attached service accounts, never long-lived JSON keys.
- For incident scenarios, pick blameless postmortems, defined incident roles, runbooks, and mitigate-then-fix; for alerting scenarios, pick multi-window multi-burn-rate SLO alerts over static threshold alerts on internal causes.

---

Want the full breakdown? See the complete **[Google Cloud Professional Cloud DevOps Engineer study guide](https://certgrid.app/study-guide/google-cloud-professional-cloud-devops-engineer)** and **[free practice questions](https://certgrid.app/practice/google-cloud-professional-cloud-devops-engineer)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

