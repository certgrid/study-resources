# Google Cloud Associate Data Practitioner - Study Cheatsheet

The Google Cloud Associate Data Practitioner certification validates associate-level skills for preparing, analyzing, orchestrating, and managing data on Google Cloud. It is aimed at data analysts, engineers, and BI professionals early in their cloud journey. The exam covers ingestion (Cloud Storage, Storage Transfer Service, Pub/Sub, Datastream, BigQuery loading), analysis and presentation (BigQuery SQL, BigQuery ML, notebooks, Looker and Looker Studio), pipeline orchestration (Dataflow, Cloud Composer, Workflows, Eventarc), and governance (IAM, Dataplex, Sensitive Data Protection, lifecycle, and security).

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | Google Cloud Associate Data Practitioner |
| Credential | Google Cloud Associate Data Practitioner |
| Level | Associate |
| Practice mock length | ~50 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Data Preparation and Ingestion | ~30% |
| 2 | Data Analysis and Presentation | ~27% |
| 3 | Data Pipeline Orchestration | ~18% |
| 4 | Data Management | ~25% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Data Preparation and Ingestion

- For a BigQuery load with an extra source column, either enable ignore-unknown-values to drop the column or update the destination schema to add it; both resolve the schema mismatch.
- Storage Transfer Service recurring jobs are incremental after the first full run, copying only new or changed objects each scheduled run, which keeps nightly transfers efficient.
- Transfer Appliance is for offline migration of very large datasets when network bandwidth cannot complete an online transfer in time; the device is shipped and loaded over Google's internal network.
- Pub/Sub delivers at-least-once by default, so subscribers can receive duplicate copies of a message and must be idempotent; exactly-once is a separate optional subscription setting.
- Prefix a function with SAFE (for example SAFE.PARSE_DATE) to return NULL on unparseable input instead of failing the whole query; plain PARSE_DATE raises an error on malformed values.
- Firestore's document model lets each document store a different set of fields with no fixed predefined schema, unlike a relational table.

### Domain 2 - Data Analysis and Presentation

- A BigQuery dry run parses and validates SQL and estimates bytes processed without executing the query or incurring on-demand scan charges, making it a safe cost preview.
- COUNT(DISTINCT column) counts unique values, so a customer with five orders is counted once, unlike COUNT(*) which counts every row.
- Reduce BigQuery bytes scanned by filtering on the partition column (partition pruning), selecting only needed columns, and filtering on clustered columns (block pruning); partitioning and clustering can combine.
- The ML.PREDICT input table must contain the same feature columns with compatible types as the training data; it does not need the true label or matching row count.
- In Looker Studio, report edit access and data source edit access are separate grants; sharing as Viewer lets people view and filter without changing chart definitions.
- A scheduled query writes results to a destination BigQuery table that reports and dashboards read from; the notebook Executor can run a saved notebook on a recurring schedule.

### Domain 3 - Data Pipeline Orchestration

- Dataflow is built on Apache Beam's unified model, so the same code runs bounded batch or unbounded streaming pipelines; batch jobs reach a completed state when finished, streaming jobs run continuously.
- Choose Dataflow when a pipeline needs custom Beam code or windowed processing of an unbounded source; Dataflow templates let a job launch from the console with parameters, no source edits needed.
- The Dataflow job graph shows each transform stage with per-stage metrics such as throughput and system lag, the primary place to diagnose stage-level bottlenecks.
- Eventarc delivers at-least-once, so a function may be invoked more than once for the same event and must be idempotent; it can source events from Cloud Audit Logs, not just object notifications.
- In Airflow, a DAG (Directed Acyclic Graph) defines task ordering; the scheduler parses DAGs and decides which task instances run.
- The catchup parameter controls whether missed scheduled intervals are backfilled when a DAG starts; catchup=false skips missed intervals and begins from the most recent one.

### Domain 4 - Data Management

- IAM controls which identities can perform which actions; VPC Service Controls restricts where data can move by defining a perimeter, protecting against exfiltration even by an IAM-permitted principal.
- Grant least privilege: replace broad Editor with narrower roles like BigQuery Data Editor and Storage Object Viewer, scope Data Viewer to the single needed dataset, and use time-limited signed URLs for external object access.
- Storage Admin manages buckets including their settings and IAM policy, while Object Admin manages only the objects within them.
- The secretAccessor role reads a secret's payload in Secret Manager; policy tags organized in a taxonomy attach to BigQuery columns to control column-level access.
- Google Cloud encrypts data at rest by default with Google-managed keys; CMEK keys live in Cloud KMS, while CSEK keys are supplied by the customer at each request.
- Cloud KMS automatic key rotation sets how often a new key version is generated on a schedule.

## Study tips

- When a question describes duplicate deliveries or a function running twice, the fix is almost always idempotency plus knowing Pub/Sub and Eventarc are at-least-once by default.
- For cost-control questions, reach first for partition filtering, column selection, clustering, dry runs, BI Engine, and the long-term storage discount and what resets it.
- Match the tool to the job: Dataflow for custom or streaming Beam code, Cloud Composer for multi-step cross-service DAGs, Workflows for lightweight service orchestration, and a scheduled query for a single BigQuery job.
- On access questions, pick the narrowest role that meets the need (Data Editor over Editor, Object Admin over Storage Admin, dataset-scoped Data Viewer) and use signed URLs for temporary external access.
- Know the ingestion decision tree: Transfer Appliance for offline bulk, Storage Transfer Service for recurring bucket-to-bucket, BigQuery Data Transfer Service for supported SaaS sources, and Datastream for CDC.

---

Want the full breakdown? See the complete **[Google Cloud Associate Data Practitioner study guide](https://certgrid.app/study-guide/google-cloud-associate-data-practitioner)** and **[free practice questions](https://certgrid.app/practice/google-cloud-associate-data-practitioner)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

