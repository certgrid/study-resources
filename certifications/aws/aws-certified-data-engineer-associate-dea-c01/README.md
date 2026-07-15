# AWS Certified Data Engineer - Associate (DEA-C01) - Study Cheatsheet

The AWS Certified Data Engineer - Associate (DEA-C01) validates your ability to build and operate data pipelines on AWS: ingesting, transforming, storing, and securing data at scale. It targets data engineers who work with services like Kinesis, Glue, EMR, Redshift, Athena, S3, and Lake Formation. The exam covers data ingestion and transformation, data store management, data operations and support, and data security and governance.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | AWS Certified Data Engineer - Associate (DEA-C01) |
| Credential | AWS Certified Data Engineer - Associate (DEA-C01) |
| Level | Associate |
| Practice mock length | ~65 questions |
| Duration | ~130 minutes |
| Passing score | 720 out of 1000 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Data Ingestion and Transformation | ~34% |
| 2 | Data Store Management | ~26% |
| 3 | Data Operations and Support | ~22% |
| 4 | Data Security and Governance | ~18% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Data Ingestion and Transformation

- Kinesis Data Firehose buffers records and can deliver them directly to S3, Redshift, or an OpenSearch Service domain for near-real-time (roughly one-minute) search and dashboarding rather than true sub-second streaming.
- Firehose data transformation invokes an AWS Lambda function synchronously on batches of records before buffering, enabling per-record masking of PII, enrichment, or filtering; transformed output continues through normal delivery.
- Amazon MSK exposes standard Kafka APIs, so existing Kafka Streams applications performing stateful joins and aggregations across topics run against it largely unchanged.
- A long-running (persistent) EMR cluster suits unpredictable, all-day ad hoc Hive and Presto queries because it avoids the launch latency of starting a transient cluster per query; transient auto-terminating clusters fit scheduled batch work.
- EMR core nodes run YARN tasks and host the HDFS DataNode process that stores data blocks; EMRFS is the Hadoop-compatible file system that lets EMR read and write S3 via s3:// URIs.
- MWAA is managed Apache Airflow (scheduler, workers, and metadata database) and is favored when a team already has Airflow DAGs or needs Airflow-specific scheduling, backfill, and DAG visualization; Step Functions fits lightweight serverless event-driven orchestration.

### Domain 2 - Data Store Management

- Amazon S3 provides strong read-after-write consistency, so a GET immediately after a PUT always returns the latest version of the object.
- S3 request throughput scales with the number of distinct prefixes and parallel connections a workload uses; AWS recommends multipart upload for objects larger than about 100 MB.
- S3 storage classes: Glacier Instant Retrieval gives millisecond access for data read a few times a year, while Glacier Flexible Retrieval restores within minutes to hours; Object Lock in compliance mode enforces a retention period no user can bypass.
- Athena writes query results to an S3 location set in the workgroup settings, charges on-demand by data scanned per query, and publishes per-workgroup metrics like data scanned to CloudWatch.
- Athena CTAS can output Parquet, ORC, Avro, JSON, or text formats; INSERT INTO appends query rows to an existing table, and query result reuse can serve a cached prior result within a configured maximum result age.
- Redshift UNLOAD writes results to S3 in parallel across the cluster's slices, producing multiple output files by default; short query acceleration prioritizes short queries so they do not wait behind long ones.

### Domain 3 - Data Operations and Support

- In CloudWatch Logs Insights, the stats command with count(*) by jobName aggregates matching events and groups counts by job name; a single query can span multiple log groups.
- Redshift HealthStatus reports a binary healthy/unhealthy signal for reachability, while PercentageDiskSpaceUsed tracks how much storage capacity has been consumed.
- Redshift cost controls include pausing an idle provisioned cluster, capping Serverless RPU usage, using WLM query monitoring rules to abort costly queries, and concurrency scaling free credits that accrue daily.
- aws s3 sync copies only new or changed files based on size and timestamp comparison, making it efficient for repeatedly deploying updated Glue scripts.
- sam local invoke runs a Lambda function locally in a container emulating the Lambda runtime using a sample event, for fast iterative testing without deploying.
- Glue natively emits Job State Change and Crawler State Change events to EventBridge; the numFailedTasks metric reports how many Spark tasks failed during a Glue job run.

### Domain 4 - Data Security and Governance

- AWS Glue requires a security group with a self-referencing inbound rule allowing all traffic from itself so the multiple ENIs it provisions for a job run can communicate.
- Interface VPC endpoints are backed by elastic network interfaces and support attached security groups (for example, allow inbound HTTPS on port 443 only from approved subnets); gateway endpoints for S3 are not ENI-backed and do not use security groups.
- AWS KMS is reached privately from a VPC through an interface endpoint built on AWS PrivateLink, keeping key API calls off the public internet.
- Lake Formation requires registering the S3 location with a data lake role before it can manage and vend access; a row-level data filter on a SELECT grant restricts which rows a principal sees via a filter expression.
- Column-level permissions cannot inspect free-text content, so unpredictable PII in a text column is best removed upstream with a Glue Detect PII transform before data reaches the governed table.
- CloudTrail separates S3 activity into object-level data events (which record the calling identity, source IP, and object key) and bucket-level management events; data event logs land in S3 as JSON and can be queried with Athena.

## Study tips

- Read scenario questions for the decisive constraint: latency requirement, cost sensitivity, existing tooling, or governance need usually points to exactly one service (for example, near-real-time to Firehose or OpenSearch, all-day ad hoc queries to a persistent EMR cluster).
- Know the boundaries between overlapping services: Step Functions vs MWAA for orchestration, Glue vs EMR for transformation, Kinesis Data Streams vs Firehose vs MSK for ingestion, and Athena vs Redshift for query.
- Memorize cost-and-performance levers for the big services: Athena data scanned (partitioning, columnar formats, result reuse), Redshift WLM and concurrency scaling, S3 storage classes, and DynamoDB capacity modes.
- For security questions, distinguish the layers: IAM for identity, KMS for encryption, Lake Formation for fine-grained (row and column) data access, and VPC endpoints (interface vs gateway) for private connectivity.
- With 802 practice questions and a 130-minute exam, pace to roughly 90 seconds per question, flag long scenarios, and eliminate options that contradict a stated requirement before choosing.

---

Want the full breakdown? See the complete **[AWS Certified Data Engineer - Associate (DEA-C01) study guide](https://certgrid.app/study-guide/aws-certified-data-engineer-associate-dea-c01)** and **[free practice questions](https://certgrid.app/practice/aws-certified-data-engineer-associate-dea-c01)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

