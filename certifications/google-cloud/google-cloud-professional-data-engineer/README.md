# Google Cloud Professional Data Engineer - Study Cheatsheet

The Google Cloud Professional Data Engineer exam validates your ability to design data processing systems, build and operationalize batch and streaming pipelines, store and prepare data for analysis, and enable machine learning on Google Cloud. It targets practitioners who design, build, secure, and maintain data systems, and the 120-minute exam scores on a 700-point scale (passing is roughly 70%). Expect heavily scenario-based questions that ask you to pick the most cost-effective, scalable, and operationally sound service for a given access pattern, latency, and consistency requirement.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | Google Cloud Professional Data Engineer |
| Credential | Google Cloud Professional Data Engineer |
| Level | Advanced |
| Practice mock length | ~50 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Designing Data Processing Systems | ~19% |
| 2 | Ingesting and Processing the Data | ~23% |
| 3 | Storing the Data | ~19% |
| 4 | Preparing and Using Data for Analysis | ~18% |
| 5 | Maintaining and Automating Data Workloads | ~21% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Designing Data Processing Systems

- Choose a data store primarily by access pattern (analytical OLAP vs operational/transactional) and by latency/throughput needs; structured relational data favors Cloud SQL or Spanner, columnar analytics favor BigQuery, and high-throughput key-based access favors Bigtable.
- Cloud Bigtable delivers single-digit-millisecond latency at high QPS and scales horizontally to petabytes, making it the choice for time-series, IoT, and other key-based operational workloads.
- Cloud Spanner is the only Google database that gives global horizontal write scaling with strong (external) consistency via TrueTime; a multi-region config provides zero RPO and up to 99.999% availability.
- BigQuery is a serverless, columnar, petabyte-scale warehouse for analytics; it separates storage from compute and charges on-demand by bytes scanned or by reserved slots.
- Use streaming (real-time) processing when sub-second to second-level latency is required; Pub/Sub plus Dataflow is the canonical pattern for continuous event processing.
- Bigtable row key design that promotes a high-cardinality field and reverses the timestamp (e.g., sensorId#reverseTimestamp) spreads writes across tablets and avoids hotspots from sequential keys.

### Domain 2 - Ingesting and Processing the Data

- Pub/Sub is the managed, scalable messaging service for high-volume event ingestion with at-least-once delivery; it decouples producers from consumers in event-driven pipelines.
- Dataflow (managed Apache Beam) provides unified batch and streaming processing with autoscaling workers and exactly-once processing semantics.
- Configure a Pub/Sub dead-letter topic with --dead-letter-topic and --max-delivery-attempts so messages that exceed max delivery attempts are routed aside for inspection instead of blocking the subscription.
- Enable Pub/Sub message ordering and publish with an ordering key when consumers require in-order delivery of related messages.
- Windowing groups unbounded streaming data into finite windows for aggregation; fixed (tumbling), sliding (hopping), and session windows are the valid Beam strategies.
- Datastream is the managed change data capture (CDC) service that replicates changes from MySQL, PostgreSQL, and Oracle into Google Cloud for real-time sync.

### Domain 3 - Storing the Data

- Cloud Storage is the object store for data lakes holding raw or unstructured data of any format, with unlimited scale and tight integration with BigQuery and Dataflow.
- Cloud SQL is managed MySQL, PostgreSQL, and SQL Server for regional transactional applications; add read replicas to scale reads and offload reporting from the primary.
- Cloud Spanner provides global scale with strong consistency and horizontal write scaling; choose it when a single relational system must span regions with zero downtime schema changes.
- Bigtable is a wide-column NoSQL store for low-latency, high-throughput operational and time-series workloads; BigQuery is the OLAP SQL warehouse - know this pairing cold.
- Avoid sequential or monotonically increasing Bigtable row keys (timestamps, auto-increment IDs) because they cause hotspots on a single tablet; use field promotion and salting/reversal instead.
- Cloud Storage storage classes by access frequency: Standard, Nearline (< monthly), Coldline (< quarterly), and Archive (< yearly); use the Archive class to minimize at-rest cost for annually accessed data.

### Domain 4 - Preparing and Using Data for Analysis

- On-demand BigQuery pricing is driven by bytes scanned; partitioning and clustering tables prune data before scanning and are the primary levers to cut query cost.
- Partition tables by a date/timestamp or integer-range column so filters skip irrelevant partitions; cluster on frequently filtered/joined columns (e.g., partition by event_date and cluster by customer_id) to physically co-locate rows.
- Selecting only the columns you need (never SELECT *) reduces bytes read because BigQuery uses columnar storage.
- Materialized views precompute and store query results/aggregations, returning faster and cheaper answers for repeated queries and refreshing incrementally.
- BigQuery query results caching returns cached results at no charge when the query text and underlying data are unchanged.
- BI Engine accelerates interactive dashboards with in-memory analysis and caching, dramatically lowering dashboard query latency.

### Domain 5 - Maintaining and Automating Data Workloads

- Cloud Composer is the managed Apache Airflow service that orchestrates DAG-based pipelines in Python, with retries and task dependencies and deep integrations to BigQuery, Dataflow, and Cloud Storage.
- Dataflow templates (classic and Flex) package pipeline code as reusable, parameterized artifacts in Cloud Storage so operators can launch jobs without source access, schedulable from Cloud Scheduler or Composer.
- Dataform manages SQL-based ELT transformation pipelines inside BigQuery with version control, dependencies, and testing.
- BigQuery scheduled queries automate recurring SQL; create one with bq mk --transfer_config --data_source=scheduled_query --params.
- Cloud Monitoring collects pipeline metrics (latency, throughput, error rates) and drives alerting policies, while Cloud Logging captures structured worker logs for troubleshooting.
- Apply least privilege with dataset-scoped roles such as roles/bigquery.dataViewer and roles/bigquery.dataEditor rather than broad project-level grants; bind roles with gcloud projects add-iam-policy-binding --member --role.

## Study tips

- Read each scenario for the qualifying constraints first - words like global, strongly consistent, sub-millisecond, serverless, cheapest, and least operational overhead usually map to exactly one service and eliminate the distractors.
- Memorize the storage decision tree: BigQuery for analytics/OLAP, Bigtable for high-throughput key/time-series, Spanner for global relational with strong consistency, Cloud SQL for regional relational, Cloud Storage for unstructured/data-lake, Memorystore for caching.
- When a question asks how to lower BigQuery cost, default to partitioning, clustering, selecting fewer columns, materialized views, result caching, and slot reservations versus on-demand - and watch for maximum-bytes-billed limits.
- For streaming questions, know the Pub/Sub-to-Dataflow-to-BigQuery pattern, windowing types (fixed, sliding, session), watermarks and allowed lateness, dead-letter topics, and the Storage Write API exactly-once mode.
- Eliminate answers that violate best practices: sequential Bigtable row keys, always-on Dataproc clusters, broad project-level IAM grants, and SELECT * are almost always wrong choices.

---

Want the full breakdown? See the complete **[Google Cloud Professional Data Engineer study guide](https://certgrid.app/study-guide/google-cloud-professional-data-engineer)** and **[free practice questions](https://certgrid.app/practice/google-cloud-professional-data-engineer)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

