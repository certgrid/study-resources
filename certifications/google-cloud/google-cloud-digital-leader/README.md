# Google Cloud Digital Leader - Study Guide

The Google Cloud Digital Leader exam validates that you understand general cloud concepts and the business and technical value of Google Cloud products across data, artificial intelligence, infrastructure modernization, security, and operations. It is a foundational credential built for non-engineers: business leaders, program and project managers, sales and procurement staff, analysts, and anyone who needs to talk about Google Cloud with confidence. There is no coding and no hands-on lab work, and the questions reward knowing the business value of a service and WHEN to use it rather than how to configure it. The 90-minute exam has roughly 50 to 60 multiple-choice and multiple-select questions and returns a simple pass or fail.

## Exam at a glance

| Item               | Detail                                                            |
| ------------------ | ----------------------------------------------------------------- |
| Exam name          | Google Cloud Digital Leader                                       |
| Credential         | Google Cloud Digital Leader                                       |
| Level              | Foundational (Beginner)                                           |
| Prerequisites      | None; no coding or hands-on required                              |
| Questions          | ~50 to 60 (multiple choice and multiple select)                   |
| Duration           | 90 minutes                                                        |
| Result type        | Pass or fail (Google does not publish a numeric score)            |
| CertGrid mock bar  | 700 out of 1000 style pass mark                                   |
| Official exam page | https://cloud.google.com/learn/certification/cloud-digital-leader |
| Last verified      | 2026-07-18                                                        |

## Domains

| #   | Section                                                       | Weight |
| --- | ------------------------------------------------------------- | ------ |
| 1   | Introduction to digital transformation with Google Cloud      | ~14%   |
| 2   | Exploring data transformation with Google Cloud               | ~14%   |
| 3   | Innovating with Google Cloud artificial intelligence          | ~15%   |
| 4   | Modernizing infrastructure and applications with Google Cloud | ~21%   |
| 5   | Trust and security with Google Cloud                          | ~20%   |
| 6   | Scaling with Google Cloud operations                          | ~16%   |

_Weightings are approximate. Always confirm the current section list and weights on the official [Cloud Digital Leader exam page](https://cloud.google.com/learn/certification/cloud-digital-leader) before you book, because Google adjusts the outline periodically._

## How to use this guide

Read this exam as a business exam with a technical vocabulary. Nearly every question describes a company scenario and asks which Google Cloud capability best fits, or why a business would move to the cloud in the first place. You are not asked to write commands, size a cluster, or debug a config. You are asked to match a business need to the right product, to know the value that product delivers, and to recognize the trade-offs. Work through the six sections below, then drill the product-picker and common-confusions tables until you can map a one-line scenario to a service without hesitating. If a question ever looks like it has two correct-sounding answers, choose the option that delivers more business value with less operational overhead and better fits the described scenario.

## Key concepts by domain

### Section 1 - Introduction to digital transformation with Google Cloud

- Digital transformation means using digital technology (cloud, data, and AI) to create new or improved business processes, customer experiences, and revenue streams, not simply moving existing systems online. It is a business change program, not just an IT project.
- Common drivers include faster time to market, the ability to scale globally, cost efficiency, resilience, richer data insights, and the pressure of competitors who already operate in the cloud.
- On-premises means you buy, house, power, cool, secure, and maintain your own hardware and pay for peak capacity you rarely use. Cloud means you consume managed infrastructure and services on demand and pay for what you use.
- Cloud shifts spending from capital expenditure (CapEx: large up-front hardware and data-center purchases) to operational expenditure (OpEx: ongoing, pay-as-you-go consumption), which improves cash flow and lets budgets follow real usage.
- Total cost of ownership (TCO) captures every direct and indirect cost of a solution over its full life: hardware, software, power, cooling, real estate, networking, staffing, and maintenance, not just the sticker price. Cloud usually improves TCO by removing idle capacity and undifferentiated operational work.
- The three cloud service models describe how much the provider manages for you: infrastructure as a service (IaaS), platform as a service (PaaS), and software as a service (SaaS). Responsibility and control decrease as you move from IaaS to SaaS, while managed convenience increases.
- Deployment models describe where workloads run: public cloud, private cloud, hybrid (a mix of on-premises and cloud), and multicloud (more than one public cloud provider).
- Google Cloud differentiators to remember: an open cloud built on open source and open standards to reduce lock-in (for example Kubernetes and TensorFlow originated at Google); leadership in data and AI (BigQuery, Vertex AI, Gemini); a global high-performance network; and a strong sustainability position (Google matches its operations with renewable energy and runs efficient, low-carbon data centers).
- The value of moving to the cloud includes elasticity (grow and shrink with demand), global reach, faster innovation, higher reliability, and freeing staff from maintaining hardware so they can focus on business outcomes.
- Change management matters: a cloud migration succeeds only when people, processes, skills, and executive sponsorship change alongside the technology. Expect questions that stress upskilling, culture, and organizational readiness, not just tooling.

| Model | You manage               | Provider manages                              | Typical use                                                            |
| ----- | ------------------------ | --------------------------------------------- | ---------------------------------------------------------------------- |
| IaaS  | OS, runtime, apps, data  | Physical hardware, virtualization, networking | Lift-and-shift VMs, full control (Compute Engine)                      |
| PaaS  | Apps and data            | OS, runtime, scaling, patching                | Build and deploy apps without managing servers (App Engine, Cloud Run) |
| SaaS  | Only your data and users | Everything else, end to end                   | Ready-to-use software (Google Workspace, Gmail)                        |

| Deployment model | What it is                                    | Choose it when                                                   |
| ---------------- | --------------------------------------------- | ---------------------------------------------------------------- |
| Public cloud     | Shared, provider-run infrastructure           | You want speed, scale, and no hardware to manage                 |
| Private cloud    | Dedicated infrastructure for one organization | Strict control or isolation requirements                         |
| Hybrid           | On-premises plus cloud working together       | You must keep some systems on-premises during or after migration |
| Multicloud       | More than one public cloud provider           | You want flexibility, resilience, or to avoid lock-in            |

Common confusions and exam traps: CapEx is up-front hardware spend; OpEx is ongoing pay-per-use, and cloud favors OpEx. Do not confuse hybrid (on-premises plus cloud) with multicloud (two or more public clouds). Digital transformation is a business outcome, not the act of buying cloud services. When a question stresses avoiding vendor lock-in or using open standards, the intended answer is usually Google Cloud's open-cloud positioning.

### Section 2 - Exploring data transformation with Google Cloud

- Data is a strategic asset: the value comes from collecting, storing, processing, and analyzing it to make faster and better decisions, personalize experiences, and power AI.
- Structured data fits neatly into rows and columns (transactions, inventory) and suits relational databases and data warehouses. Unstructured data has no fixed schema (images, video, audio, documents, free text) and suits object storage and AI processing.
- Cloud Storage is Google Cloud's object storage for unstructured data and files; buckets have globally unique names and storage classes (Standard, Nearline, Coldline, Archive) trade cost against access frequency.
- Cloud SQL is a fully managed relational database for MySQL, PostgreSQL, and SQL Server, ideal for lifting existing relational apps into a managed service at regional scale.
- Cloud Spanner is a fully managed relational database that combines strong consistency with horizontal, global scale, for mission-critical workloads that must scale beyond a single region without giving up transactions.
- Firestore is a fully managed, serverless NoSQL document database, well suited to web and mobile apps that need flexible schemas, real-time sync, and offline support.
- Cloud Bigtable is a fully managed NoSQL wide-column database for very large key-value and time-series datasets that need low-latency, high-throughput access (IoT, financial ticks, analytics at massive scale).
- Memorystore is the managed in-memory data store (Redis and Memcached) used to cache hot data and cut latency and database load.
- BigQuery is a serverless, fully managed analytical data warehouse for fast SQL analytics over very large datasets; it separates storage from compute and is built for reporting and analysis, not high-frequency single-row transactions. BigQuery ML lets analysts build and run machine learning models directly in BigQuery using SQL, without moving the data.
- A data lake stores large volumes of raw data in many formats (often in Cloud Storage) for later processing; a data warehouse (BigQuery) stores curated, structured data optimized for analytics. Many organizations use both together.
- Streaming and data pipelines move and transform data: Pub/Sub is managed messaging for real-time ingestion and decoupling systems; Dataflow is managed stream and batch processing (based on Apache Beam); Dataproc is managed Apache Spark and Hadoop for teams with existing open-source big-data jobs.
- Business intelligence turns data into decisions: Looker is the enterprise BI and governed-metrics platform with a semantic modeling layer; Looker Studio is the free, self-service tool for dashboards and reports.
- Data governance keeps data discoverable, trustworthy, and compliant: Dataplex provides unified governance and management across data lakes, warehouses, and marts, and Dataplex Data Catalog provides searchable metadata so people can find and understand data assets.

| Service        | Type                                               | Best for                                                     | Not for                                 |
| -------------- | -------------------------------------------------- | ------------------------------------------------------------ | --------------------------------------- |
| Cloud SQL      | Managed relational (MySQL, PostgreSQL, SQL Server) | Regional relational apps, moving existing databases          | Global horizontal scale                 |
| Cloud Spanner  | Global relational, strong consistency              | Mission-critical apps needing global scale plus transactions | Small, simple, cost-sensitive databases |
| Firestore      | NoSQL document, serverless                         | Web and mobile apps, flexible schema, real-time sync         | Heavy relational joins or analytics     |
| Cloud Bigtable | NoSQL wide-column                                  | Huge time-series and key-value workloads, low latency        | Relational queries or transactions      |
| Memorystore    | In-memory cache (Redis, Memcached)                 | Caching hot data, reducing latency                           | Durable primary storage                 |
| BigQuery       | Analytical data warehouse (OLAP)                   | SQL analytics over massive datasets, reporting               | High-frequency single-row writes        |
| Cloud Storage  | Object storage                                     | Unstructured files, backups, data lake landing zone          | Structured queries or transactions      |

Common confusions and exam traps: BigQuery is for analytics (OLAP), not transactional apps (OLTP); pick Cloud SQL or Spanner for transactions. Spanner is the answer only when a scenario needs global scale AND relational strong consistency; do not reach for it for ordinary regional databases. Bigtable is key-value and time-series at massive scale, not a document store (that is Firestore) and not relational. A data lake holds raw data of any format; a data warehouse holds curated structured data for analytics. Looker is governed enterprise BI; Looker Studio is the lightweight free dashboard tool.

### Section 3 - Innovating with Google Cloud artificial intelligence

- Artificial intelligence (AI) is the broad field of machines performing tasks that normally need human intelligence. Machine learning (ML) is a subset of AI where models learn patterns from data instead of being explicitly programmed. Generative AI is a subset that creates new content (text, images, code, audio) from patterns it learned, typically using large foundation models.
- Vertex AI is Google Cloud's unified platform for building, training, deploying, and managing ML and generative AI, bringing data, training, tuning, serving, and MLOps into one place.
- Pre-trained APIs let you add AI to an app with a simple API call and no model training: Vision API (analyze images), Speech-to-Text (convert audio to text), Natural Language API (extract meaning, sentiment, and entities from text), Translation API (translate between languages), and Document AI (extract structured data from documents and forms).
- Generative AI on Google Cloud centers on Gemini, Google's family of multimodal models, accessed through Vertex AI. Model Garden is a catalog of Google, partner, and open models you can discover and deploy. Vertex AI Agent Builder helps you create AI agents and search or assistant experiences grounded in your own data.
- BigQuery ML builds models with SQL directly on warehouse data. AutoML (in Vertex AI) trains high-quality custom models from your own labeled data with little ML expertise. Custom training is for data-science teams that build and tune their own models with full control.
- Choose pre-trained APIs when a common task is already solved (detect objects, transcribe speech, translate). Choose AutoML when you need a custom model for your specific data but lack deep ML expertise. Choose custom training when you have the expertise and need maximum control.
- Responsible AI matters and is testable: Google publishes AI principles emphasizing fairness, avoiding unfair bias, safety, privacy, accountability, transparency, and human oversight. Expect questions about using AI ethically and keeping humans in control.

| Approach                    | Who uses it                   | Data you provide    | Effort  | Use when                                                            |
| --------------------------- | ----------------------------- | ------------------- | ------- | ------------------------------------------------------------------- |
| Pre-trained API             | Developers, non-experts       | None (call the API) | Lowest  | The task is already solved (vision, speech, translation, documents) |
| BigQuery ML                 | Data analysts (SQL)           | Your warehouse data | Low     | You want ML on data already in BigQuery, using SQL                  |
| AutoML (Vertex AI)          | Teams without deep ML skills  | Your labeled data   | Medium  | You need a custom model but limited ML expertise                    |
| Custom training (Vertex AI) | Data scientists, ML engineers | Your data and code  | Highest | You need full control and custom architectures                      |

| Term          | Scope        | Simple definition                                      |
| ------------- | ------------ | ------------------------------------------------------ |
| AI            | Broadest     | Machines doing tasks that need human-like intelligence |
| ML            | Subset of AI | Systems that learn patterns from data                  |
| Generative AI | Subset of ML | Models that create new content from learned patterns   |

Common confusions and exam traps: if a scenario names a common task (read a receipt, transcribe a call, translate a page, detect an object), the answer is a pre-trained API, not building a custom model. AutoML is for a custom model without heavy ML skill; custom training is for expert teams. Vertex AI is the unified platform, Gemini is the generative model, and Model Garden is the model catalog; do not treat these as competing products. When a question stresses ethics, bias, or human oversight, it is testing responsible AI, not a specific service.

### Section 4 - Modernizing infrastructure and applications with Google Cloud

- Modernization moves workloads along a spectrum from full control to fully managed: Compute Engine (VMs you manage), Google Kubernetes Engine (managed containers), App Engine and Cloud Run (managed platforms), and Cloud Functions (event-driven functions). More management by Google means less operational overhead for you.
- Compute Engine provides infrastructure-as-a-service virtual machines you provision and control, ideal for lift-and-shift (rehost) migrations and workloads that need OS-level control.
- Google Kubernetes Engine (GKE) is managed Kubernetes for running containers at scale, giving fine-grained control over networking, scaling, and scheduling for complex or microservices workloads.
- Cloud Run is a serverless platform that runs containers, scales to zero when idle, and bills per use, ideal for stateless web services and APIs without managing servers.
- App Engine is a fully managed platform for building and hosting web and mobile back ends where Google handles the underlying infrastructure and scaling.
- Cloud Functions is Google Cloud's function-as-a-service: small single-purpose code triggered by events (HTTP, Pub/Sub, Cloud Storage) with no servers to manage and pay-per-execution billing.
- Containers package an application with its dependencies so it runs consistently across a laptop, on-premises, and any cloud; microservices break a large application into small, independently deployable services. Together they improve portability, scaling, and release speed.
- Serverless benefits: no infrastructure to manage, automatic scaling (including to zero), and paying only for actual use, which lowers operational overhead and idle cost.
- Migration paths: Migration Center is the unified hub for discovering your estate, assessing fit, and planning a move (including TCO estimates), and Migrate to Virtual Machines moves VM workloads into Compute Engine. Common strategies are rehost (lift and shift), replatform (minor optimization), and refactor (re-architect to cloud-native).
- Hybrid and multicloud: GKE Enterprise provides consistent management, policy, and operations for containerized apps across Google Cloud, on-premises, and other clouds, so teams manage many clusters with one control plane.
- API management: Apigee is Google Cloud's full-lifecycle API management platform for securing, publishing, monitoring, and monetizing APIs, which is central to exposing modernized services safely.
- Modernizing monoliths: break a large monolithic application into containerized microservices, deploy on Cloud Run or GKE, and expose functionality through managed APIs, so teams can release and scale parts independently.

| Option                   | Model                   | You manage                   | Scales to zero | Best for                            |
| ------------------------ | ----------------------- | ---------------------------- | -------------- | ----------------------------------- |
| Compute Engine           | IaaS VMs                | OS and above                 | No             | Lift-and-shift, full OS control     |
| Google Kubernetes Engine | Managed containers      | Cluster workloads and config | No (nodes run) | Complex, large-scale, microservices |
| Cloud Run                | Serverless containers   | Just your container          | Yes            | Stateless web services and APIs     |
| App Engine               | Managed platform (PaaS) | Just your code               | Yes (standard) | Web and mobile back ends            |
| Cloud Functions          | Functions (FaaS)        | Just your function           | Yes            | Event-driven, single-purpose code   |

Common confusions and exam traps: "lift and shift" or "rehost" points to Compute Engine, not containers. "Scale to zero and pay per use" points to Cloud Run or Cloud Functions. Cloud Run runs a container; Cloud Functions runs a single event-driven function. Reach for GKE only when a scenario needs container orchestration at scale or fine-grained control. GKE Enterprise is the answer for consistent management across on-premises and multiple clouds. Apigee is API management, not compute.

### Section 5 - Trust and security with Google Cloud

- The shared responsibility model splits duties: Google secures the underlying cloud infrastructure (hardware, network, facilities), while you secure what you put in the cloud (your data, identities, access configuration, and settings). The exact split shifts by service model, and Google increasingly describes it as shared fate, where Google actively helps customers be secure.
- Defense in depth layers many security controls so no single failure exposes everything. Zero trust assumes no user or device is trusted by default and verifies every request; BeyondCorp Enterprise is Google Cloud's zero-trust access approach that grants access based on identity and context rather than network location.
- Identity and Access Management (IAM) controls who (a principal: user, group, or service account) can do what (a role, which is a set of permissions) on which resource. Always apply least privilege by granting the narrowest role needed instead of broad roles like Owner or Editor, and prefer assigning roles to groups.
- The resource hierarchy for policy is Organization, then Folders, then Projects, then resources. IAM policies and organization policies are inherited downward, so granting access or a policy at a higher level flows to everything beneath it. Use it to apply controls once and have them cascade.
- Encryption protects data in two states: at rest (data is encrypted by default with no action required) and in transit (data moving across networks is encrypted). This is on by default on Google Cloud.
- Cloud Key Management Service (Cloud KMS) lets you create and control encryption keys, including customer-managed encryption keys, when you need to own key rotation and access.
- Network security controls include Cloud Armor (protects against DDoS attacks and common web exploits, and enforces web application firewall rules) and VPC Service Controls (creates a security perimeter around resources to reduce data exfiltration risk).
- Security Command Center is the central platform for security and risk posture: it surfaces misconfigurations, vulnerabilities, and threats across your Google Cloud environment.
- Google Security Operations (SecOps) is the platform for detecting, investigating, and responding to threats at scale, bringing security analytics and threat intelligence together for security teams.
- Compliance, data residency, and sovereignty: Google Cloud maintains many certifications and compliance offerings, and provides controls over where data is stored (data residency) and who can access it, which matters for regulated industries and national data-sovereignty requirements.

| Layer               | Service or concept         | What it does                                                        |
| ------------------- | -------------------------- | ------------------------------------------------------------------- |
| Identity and access | IAM                        | Controls who can do what on which resource; enforce least privilege |
| Policy scope        | Resource hierarchy         | Org, folders, projects; policies inherit downward                   |
| Zero trust access   | BeyondCorp Enterprise      | Grants access by identity and context, not network location         |
| Key management      | Cloud KMS                  | Create and control encryption keys (including CMEK)                 |
| Network protection  | Cloud Armor                | DDoS protection and web application firewall                        |
| Data perimeter      | VPC Service Controls       | Perimeter to reduce data exfiltration                               |
| Posture and risk    | Security Command Center    | Finds misconfigurations, vulnerabilities, threats                   |
| Threat operations   | Google Security Operations | Detect, investigate, and respond to threats at scale                |

Common confusions and exam traps: IAM answers "who can do what" (permissions); the resource hierarchy answers "where a policy applies and how it inherits" (scope). Encryption at rest is automatic and on by default, so the answer is rarely "you must turn it on." Cloud Armor is edge and web protection (DDoS and WAF); VPC Service Controls is a data-exfiltration perimeter. Security Command Center is posture and findings; Google Security Operations is threat detection and response. Under shared responsibility, protecting your data and access configuration is always the customer's job.

### Section 6 - Scaling with Google Cloud operations

- Financial governance keeps cloud spend under control. Cloud Billing tracks and reports spend, budgets and alerts warn you as you approach a threshold (they notify; they do not automatically cap spend), and the resource hierarchy lets you organize billing and cost controls across the organization, folders, and projects.
- Discounts lower compute cost: committed use discounts give a lower price in exchange for a one- or three-year commitment to a level of usage, while sustained use discounts apply automatically when eligible resources run for a large share of the billing month. Only committed use requires a commitment.
- Sustainability is a business and exam theme: Google Cloud runs highly efficient data centers, matches its annual electricity use with renewable energy, and gives customers tools such as the Carbon Footprint report to measure and reduce emissions.
- Google Cloud Observability is the built-in toolset for understanding system health: Cloud Monitoring collects metrics, dashboards, and alerts; Cloud Logging centralizes logs; Error Reporting groups and surfaces application errors; and Cloud Trace analyzes request latency across services.
- Site reliability engineering (SRE) and DevOps concepts define reliability targets: a service level indicator (SLI) is a measured signal (for example latency or error rate), a service level objective (SLO) is the target for that signal, and an error budget is the acceptable amount of unreliability that balances new-feature velocity against stability.
- Reliability and scalability patterns include redundancy across zones for high availability, deployment across regions for disaster recovery and lower latency, and autoscaling so capacity follows demand. Scalability is the ability to grow to handle more load; elasticity is scaling up and down automatically in real time.
- Customer Care support tiers scale with business need: Basic (included for all customers: documentation, community, and billing support), Standard, Enhanced, and Premium, with faster response times and more services as you move up. Premium adds the fastest response and a technical account manager for enterprises with critical workloads.
- Total cost of ownership stays central at scale: combine right-sizing, autoscaling, committed and sustained use discounts, and the resource hierarchy for cost controls to keep spend aligned with value.

| Tool             | Part of Google Cloud Observability | Answers the question                      |
| ---------------- | ---------------------------------- | ----------------------------------------- |
| Cloud Monitoring | Metrics, dashboards, alerts        | Is the system healthy and performing?     |
| Cloud Logging    | Centralized logs                   | What happened and when?                   |
| Error Reporting  | Grouped application errors         | Which errors are occurring and how often? |
| Cloud Trace      | Latency and request tracing        | Where is the request spending time?       |

| Discount               | How you get it                                            | Commitment   |
| ---------------------- | --------------------------------------------------------- | ------------ |
| Sustained use discount | Applied automatically for eligible long-running resources | None         |
| Committed use discount | Commit to a level of usage for a lower price              | 1 or 3 years |

Common confusions and exam traps: budgets and alerts notify you; they do not automatically stop spending. Committed use discounts need a 1- or 3-year commitment; sustained use discounts are automatic with no commitment. Cloud Monitoring is metrics and alerting; Cloud Logging is logs; do not swap them. An SLI is the measurement, an SLO is the target, and an error budget is the allowed unreliability. High availability comes from multiple zones in a region; disaster recovery and lower global latency come from multiple regions.

## Product picker (fast decisions)

Compute:

| If you need...                                      | Use                      |
| --------------------------------------------------- | ------------------------ |
| Full control of the OS or a lift-and-shift VM       | Compute Engine           |
| Container orchestration at scale, microservices     | Google Kubernetes Engine |
| A serverless container that scales to zero          | Cloud Run                |
| A managed platform for a web or mobile back end     | App Engine               |
| To run code on an event with no servers             | Cloud Functions          |
| Consistent management across on-premises and clouds | GKE Enterprise           |
| To secure, publish, and manage APIs                 | Apigee                   |

Data and databases:

| If you need...                                                 | Use                                |
| -------------------------------------------------------------- | ---------------------------------- |
| Object storage for files, images, backups                      | Cloud Storage                      |
| A managed relational database (MySQL, PostgreSQL, SQL Server)  | Cloud SQL                          |
| A relational database with global scale and strong consistency | Cloud Spanner                      |
| A NoSQL document database for web and mobile apps              | Firestore                          |
| A NoSQL store for huge time-series or key-value data           | Cloud Bigtable                     |
| An in-memory cache                                             | Memorystore                        |
| A serverless analytics data warehouse                          | BigQuery                           |
| Real-time messaging and ingestion                              | Pub/Sub                            |
| Managed stream and batch data processing                       | Dataflow                           |
| Managed Spark and Hadoop                                       | Dataproc                           |
| Enterprise governed BI vs quick dashboards                     | Looker vs Looker Studio            |
| Unified data governance and catalog                            | Dataplex and Dataplex Data Catalog |

AI:

| If you need...                                             | Use                                                                                  |
| ---------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| A common AI task solved with an API call                   | Pre-trained API (Vision, Speech-to-Text, Natural Language, Translation, Document AI) |
| One unified platform to build and run ML and generative AI | Vertex AI                                                                            |
| Generative AI (text, code, multimodal)                     | Gemini on Vertex AI                                                                  |
| A catalog of Google, partner, and open models              | Model Garden                                                                         |
| To build AI agents grounded in your data                   | Vertex AI Agent Builder                                                              |
| ML on warehouse data using SQL                             | BigQuery ML                                                                          |
| A custom model without deep ML expertise                   | AutoML on Vertex AI                                                                  |
| Full control over a custom model                           | Custom training on Vertex AI                                                         |

Security and operations:

| If you need...                                  | Use                                             |
| ----------------------------------------------- | ----------------------------------------------- |
| To control who can do what on a resource        | IAM (least privilege, assign to groups)         |
| To apply a policy that inherits to all projects | The resource hierarchy (org, folders, projects) |
| To manage your own encryption keys              | Cloud KMS                                       |
| DDoS and web application firewall protection    | Cloud Armor                                     |
| A perimeter to reduce data exfiltration         | VPC Service Controls                            |
| Central security posture and findings           | Security Command Center                         |
| Threat detection, investigation, and response   | Google Security Operations                      |
| Metrics, logs, errors, and traces               | Google Cloud Observability                      |
| To track and control spend                      | Cloud Billing with budgets and alerts           |

## Common confusions that decide pass/fail

| If you confuse...                                     | Remember                                                                               |
| ----------------------------------------------------- | -------------------------------------------------------------------------------------- |
| Compute Engine vs GKE vs Cloud Run vs Cloud Functions | VM control vs container orchestration vs serverless container vs event-driven function |
| Cloud SQL vs Spanner vs Bigtable vs Firestore         | Regional relational vs global relational vs huge NoSQL wide-column vs NoSQL document   |
| BigQuery vs a data lake                               | Curated structured analytics warehouse vs raw multi-format storage                     |
| Pre-trained API vs AutoML vs custom model             | Task already solved vs custom model with low effort vs full-control expert model       |
| IAM vs resource hierarchy                             | Who can do what vs where a policy applies and how it inherits                          |
| Cloud Monitoring vs Cloud Logging                     | Metrics, dashboards, alerts vs centralized logs                                        |
| Committed use vs sustained use discounts              | Commit for 1 or 3 years vs automatic for long-running resources                        |
| Cloud Armor vs VPC Service Controls                   | Edge DDoS and WAF vs data-exfiltration perimeter                                       |
| Security Command Center vs Google Security Operations | Posture and findings vs threat detection and response                                  |
| Hybrid vs multicloud                                  | On-premises plus cloud vs two or more public clouds                                    |
| CapEx vs OpEx                                         | Up-front hardware spend vs ongoing pay-per-use                                         |
| Budgets and alerts vs a spending cap                  | They notify you; they do not automatically stop spending                               |

## 5-day study plan

| Day | Focus                                                                                                   | Sections         |
| --- | ------------------------------------------------------------------------------------------------------- | ---------------- |
| 1   | Cloud concepts, digital transformation, service and deployment models, TCO and CapEx vs OpEx            | Section 1        |
| 2   | Data value, databases, BigQuery, data lakes, pipelines, BI, governance                                  | Section 2        |
| 3   | AI vs ML vs generative AI, Vertex AI, pre-trained APIs, Gemini, AutoML vs custom, responsible AI        | Section 3        |
| 4   | Compute spectrum, containers and serverless, migration, hybrid and multicloud, Apigee                   | Section 4        |
| 5   | Security and trust, then operations, financial governance, observability, and the product-picker tables | Sections 5 and 6 |

This is a revision-paced plan for someone with some cloud familiarity. If you are new to the cloud, give yourself two to three weeks and spend extra time on Sections 4 and 5, which carry the most weight. This exam rewards understanding the business value of each service and knowing WHEN to use it, so drill the product-picker and confusion tables until the mapping is automatic rather than memorizing feature lists.

## Readiness checklist

You are ready when you can, without notes:

- Explain what digital transformation is and why a business moves to the cloud, including TCO and CapEx vs OpEx.
- Match a business scenario to the right compute option (Compute Engine, GKE, Cloud Run, App Engine, or Cloud Functions).
- Match a data need to the right database or analytics service (Cloud SQL, Spanner, Firestore, Bigtable, Memorystore, BigQuery, Cloud Storage).
- Choose the right AI approach for a scenario: a pre-trained API, BigQuery ML, AutoML, or custom training on Vertex AI, and say what Gemini and Vertex AI are.
- Describe the shared responsibility model and who secures what.
- Explain IAM and least privilege, and how the resource hierarchy makes policies inherit downward.
- Pick the right security service for a scenario (Cloud KMS, Cloud Armor, VPC Service Controls, Security Command Center, Google Security Operations).
- Tell budgets and alerts apart from a spending cap, and committed use from sustained use discounts.
- Match an operations need to the right Google Cloud Observability tool and explain SLIs, SLOs, and error budgets.
- Read a business scenario and confidently name the single Google Cloud product or capability that best fits it.

---

Want the full breakdown? See the complete **[Google Cloud Digital Leader study guide](https://certgrid.app/study-guide/google-cloud-digital-leader)** and **[free practice questions](https://certgrid.app/practice/google-cloud-digital-leader)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_
