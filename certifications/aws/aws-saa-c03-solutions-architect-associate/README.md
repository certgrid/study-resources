# AWS SAA-C03: Solutions Architect Associate - Study Cheatsheet

The AWS Certified Solutions Architect - Associate (SAA-C03) validates your ability to design secure, resilient, high-performing, and cost-optimized distributed systems on AWS. It is aimed at people with hands-on experience designing AWS solutions who can translate business requirements into architectures using AWS compute, storage, database, networking, and security services. The exam is 130 minutes, scenario-heavy, scored 100-1000 with a passing score of 720, and uses multiple-choice and multiple-response questions.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | AWS SAA-C03 |
| Credential | AWS SAA-C03: Solutions Architect Associate |
| Level | Associate |
| Practice mock length | ~65 questions |
| Duration | ~130 minutes |
| Passing score | 720 out of 1000 |
| Notes reviewed | 2026-06-23 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Design Secure Architectures | ~26% |
| 2 | Design Resilient Architectures | ~28% |
| 3 | Design High-Performing Architectures | ~23% |
| 4 | Design Cost-Optimized Architectures | ~23% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Design Secure Architectures

- IAM roles deliver temporary credentials via the EC2 instance profile and should always be used for EC2/Lambda/ECS instead of embedding long-term access keys; follow least privilege by granting only specific actions on specific resource ARNs.
- Service Control Policies (SCPs) in AWS Organizations set the maximum permissions for member accounts but never grant permissions themselves; an explicit Deny in an SCP cannot be overridden by any account-level IAM policy.
- SSE-KMS with a customer managed key (CMK) gives you control over the key policy, automatic annual key rotation, and CloudTrail audit logging of every key use; SSE-S3 and AWS managed keys (aws/s3) do not let you control rotation or the key policy.
- Cross-account access is done with an IAM role: create the role in the target account with the needed permissions and a trust policy naming the source account/role, and have the source principal call sts:AssumeRole - never share access keys across accounts.
- A NAT gateway lives in a public subnet and provides outbound-only internet access for private subnets; the private subnet route table sends 0.0.0.0/0 to the NAT gateway, while the public subnet routes to an internet gateway.
- Security groups are stateful (return traffic is automatically allowed) and support allow rules only; reference one security group as the source in another (for example, allow DB SG inbound 3306 only from the app-tier SG) instead of using IP ranges.

### Domain 2 - Design Resilient Architectures

- RDS Multi-AZ provides a synchronous standby in a second AZ for high availability with automatic failover (typically 60-120 seconds); it is not a read scaling feature - use read replicas (asynchronous) for read scaling.
- Aurora replicates six copies of data across three AZs, automatically promotes a reader to writer on failure (failover usually under 30 seconds), and exposes a cluster (writer) endpoint and a reader endpoint for load-balanced reads.
- Aurora Global Database replicates to a secondary Region with typical lag under one second, supports promotion for cross-Region DR in under a minute, and is the preferred choice for low-RPO/RTO global resilience.
- Decouple producers from consumers with Amazon SQS so traffic spikes are buffered; set the visibility timeout to be at least as long as the consumer's processing time to prevent duplicate processing.
- An S3 event notification can push directly to SQS, SNS, Lambda, or EventBridge so uploads trigger downstream processing without polling the bucket.
- Multi-AZ Auto Scaling groups behind an ALB are the standard pattern for instance-level resilience; to survive one AZ failure, provision enough instances so the surviving AZs still meet required capacity (for example, 3 AZs x 3 = 9 instances to keep 6 running).

### Domain 3 - Design High-Performing Architectures

- Amazon CloudFront caches content at global edge locations to cut latency for distant users; it serves static and dynamic content over the AWS backbone and can use S3, ALB, or any HTTP origin as its origin.
- ElastiCache for Redis offloads read-heavy databases via a cache-aside pattern and supports advanced data structures (for example, Sorted Sets for real-time leaderboards); Memcached is simpler and multi-threaded but lacks persistence and replication.
- DynamoDB Accelerator (DAX) is an in-memory cache for DynamoDB that delivers microsecond read latency for read-heavy, eventually-consistent workloads with no application cache-management code.
- RDS read replicas (up to 15 for Aurora, 5 for RDS) offload read traffic from the primary; they are asynchronous and can be promoted to standalone databases.
- Amazon Kinesis Data Streams ingests high-volume real-time data by shards (each shard handles 1 MB/s or 1,000 records/s in); Kinesis Data Firehose batches and delivers to S3/Redshift/OpenSearch, and Managed Service for Apache Flink (formerly Kinesis Data Analytics) does real-time analytics.
- Amazon Athena runs serverless SQL directly against data in S3 and is far cheaper and faster when data is partitioned and stored in columnar formats like Parquet, which reduce data scanned.

### Domain 4 - Design Cost-Optimized Architectures

- EC2 Spot Instances offer up to 90 percent off On-Demand for interruptible, restartable workloads; diversify across instance types and AZs and use checkpointing to handle the two-minute interruption notice gracefully.
- Savings Plans and Reserved Instances reduce cost for steady workloads: Compute Savings Plans are most flexible, EC2 Instance Savings Plans give deeper discounts tied to a family/Region, and 3-year All Upfront RIs deliver the maximum discount (up to ~72 percent).
- S3 lifecycle policies transition objects across tiers to cut storage cost: Standard, then Standard-IA, then Glacier Instant Retrieval, Glacier Flexible Retrieval, and Glacier Deep Archive for long-term cold archival.
- S3 Intelligent-Tiering automatically moves objects between access tiers based on usage with no retrieval fees, ideal when access patterns are unknown or unpredictable.
- Right-size oversized resources: if an RDS instance shows low CPU and memory utilization, move to a smaller instance class (for example db.r5.2xlarge to db.r5.large) while keeping Multi-AZ to cut cost roughly in half.
- AWS Instance Scheduler starts and stops EC2 and RDS instances on a defined schedule to eliminate cost for dev/test resources outside business hours.

## Study tips

- Read the qualifiers in every scenario - words like 'most cost-effective', 'least operational overhead', 'highest availability', or 'lowest latency' usually eliminate two or three technically valid options and point to the one intended answer.
- Default to managed and serverless services (Fargate, Lambda, Aurora, SQS, S3) when a question stresses reducing operational overhead, since AWS favors removing undifferentiated heavy lifting.
- Map availability requirements to AZ and Region scope: single-AZ is not resilient, Multi-AZ survives an AZ failure, and Multi-Region survives a Region failure - match the chosen pattern to the stated RTO/RPO.
- Watch the budget: about 130 minutes for roughly 65 questions is under two minutes each, so flag long scenarios, answer the quick ones first, and return to flagged items rather than stalling.
- Memorize the decision triggers: SQS for decoupling/buffering, CloudFront/ElastiCache/DAX for latency, Spot for interruptible batch, IAM roles over access keys, and KMS CMK when you need control over rotation and audit.

---

Want the full breakdown? See the complete **[AWS SAA-C03 study guide](https://certgrid.app/study-guide/aws-saa-c03-solutions-architect-associate)** and **[free practice questions](https://certgrid.app/practice/aws-saa-c03-solutions-architect-associate)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

