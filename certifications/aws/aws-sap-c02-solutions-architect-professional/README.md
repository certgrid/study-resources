# AWS SAP-C02: Solutions Architect Professional - Study Cheatsheet

The AWS Certified Solutions Architect - Professional (SAP-C02) validates advanced skills in designing cost-optimized, resilient, secure, and scalable solutions across complex multi-account AWS environments. It is intended for experienced architects who can evaluate trade-offs, plan migrations, and continuously improve existing workloads. The exam is 180 minutes, 75 questions (scored plus unscored), uses a scaled passing score of 750 out of 1000, and is heavy on long multi-service scenarios with multiple-response questions.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | AWS SAP-C02 |
| Credential | AWS SAP-C02: Solutions Architect Professional |
| Level | Advanced |
| Practice mock length | ~75 questions |
| Duration | ~180 minutes |
| Passing score | 750 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Design Solutions for Organizational Complexity | ~28% |
| 2 | Design for New Solutions | ~25% |
| 3 | Continuous Improvement for Existing Solutions | ~31% |
| 4 | Accelerate Workload Migration and Modernization | ~16% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Design Solutions for Organizational Complexity

- Service Control Policies (SCPs) are guardrails that set the maximum available permissions for accounts in an OU or organization; they never grant permissions and do not apply to the management account or to service-linked roles.
- AWS IAM Identity Center (successor to AWS SSO) provides centralized workforce SSO and permission sets across all accounts, and integrates with external IdPs via SAML 2.0 and SCIM for automated user/group provisioning.
- Cross-account access is best done with IAM roles and sts:AssumeRole; for third-party access, require an ExternalId condition to prevent the confused-deputy problem.
- AWS Control Tower automates landing zone setup with a multi-account baseline, mandatory and elective guardrails (implemented via SCPs and AWS Config rules), and account provisioning through Account Factory.
- AWS Resource Access Manager (RAM) shares resources such as Transit Gateways, subnets, License Manager configurations, and Route 53 Resolver rules across accounts without resource policies or peering.
- Transit Gateway is the hub-and-spoke router for connecting many VPCs and on-premises networks; it supports route tables for segmentation and is the standard pattern for a centralized inspection/egress VPC.

### Domain 2 - Design for New Solutions

- Amazon SQS decouples producers from consumers so each scales independently; standard queues offer at-least-once delivery and best-effort ordering, while FIFO queues guarantee exactly-once processing and strict ordering within a message group.
- SQS FIFO uses MessageGroupId to preserve ordering per group (e.g., per customer) while allowing parallel processing across groups; ContentBasedDeduplication or a MessageDeduplicationId enforces exactly-once over a 5-minute window.
- SNS fan-out publishes one message to a topic that delivers to multiple subscribers (SQS queues, Lambda, HTTP); pairing SNS with SQS gives durable, decoupled parallel processing.
- Amazon Aurora Global Database replicates to up to five secondary Regions with typical sub-second lag, supports cross-Region disaster recovery with promotion in under a minute, and enables low-latency global reads.
- Multi-AZ RDS provides synchronous standby replication and automatic failover for high availability (not read scaling); read replicas provide asynchronous read scaling and can be promoted for DR.
- DynamoDB on-demand (PAY_PER_REQUEST) automatically scales for unpredictable traffic with no capacity planning; provisioned mode with auto scaling is cheaper for steady, predictable workloads. DAX provides microsecond read caching.

### Domain 3 - Continuous Improvement for Existing Solutions

- Compute Savings Plans offer the largest, most flexible discount across EC2, Fargate, and Lambda regardless of instance family or Region in exchange for a 1- or 3-year hourly spend commitment; EC2 Instance Savings Plans give deeper discounts but lock to a family/Region.
- Spot Instances provide up to about 90 percent savings for fault-tolerant, interruptible workloads; design for the 2-minute interruption notice with checkpointing and use Spot via EC2 Fleet or Auto Scaling mixed-instances policies.
- S3 lifecycle rules transition objects across tiers (Standard to Standard-IA, then Glacier Instant/Flexible Retrieval, then Glacier Deep Archive) and expire them; S3 Intelligent-Tiering moves objects automatically based on access with no retrieval fees.
- Add a caching layer to cut read load and latency: ElastiCache (Redis/Memcached) for general caching and DynamoDB Accelerator (DAX) for DynamoDB; for read-heavy relational workloads, add RDS read replicas.
- The four DR strategies in order of increasing cost and decreasing RTO/RPO are Backup and Restore, Pilot Light, Warm Standby, and Multi-Site Active/Active; warm standby keeps a scaled-down but always-running stack ready to scale up.
- AWS Config rules with automatic SSM Automation remediation enforce compliance, and conformance packs deploy rule collections across an organization for continuous governance.

### Domain 4 - Accelerate Workload Migration and Modernization

- The 7 Rs migration strategies are Retire, Retain, Rehost (lift-and-shift), Relocate (e.g., VMware Cloud on AWS), Repurchase (move to SaaS/buy new), Replatform (lift-tinker-shift), and Refactor/Re-architect (redesign cloud-native).
- AWS Application Migration Service (MGN) is the primary rehosting tool: a lightweight agent does continuous block-level replication to a staging area, then performs test launches and a short orchestrated cutover with minimal downtime.
- AWS Database Migration Service (DMS) migrates databases with minimal downtime; the full-load-and-cdc task type does a full copy then keeps changes synchronized via change data capture until cutover.
- AWS Schema Conversion Tool (SCT) converts schema and procedural code for heterogeneous migrations (e.g., Oracle/SQL Server to Aurora PostgreSQL); homogeneous migrations need only DMS.
- Refactoring a commercial database to Amazon Aurora PostgreSQL or MySQL with DMS plus SCT is the standard way to escape expensive commercial licensing while gaining managed scalability.
- AWS Application Discovery Service collects on-premises server inventory, performance, and network dependencies, feeding AWS Migration Hub for centralized discovery, dependency mapping, and migration tracking.

## Study tips

- Read the last sentence of each scenario first - it states the actual requirement (lowest cost, least operational overhead, highest availability, minimal downtime) that distinguishes the one best answer from several technically valid options.
- Watch for multiple-response questions that ask you to choose two or three answers; partial credit is not given, so each selected item must independently be correct.
- Eliminate answers that violate AWS best practices: using the management account for workloads, hardcoding credentials, opening security groups to 0.0.0.0/0, or solutions with unnecessary operational overhead.
- Map keywords to services: decouple to SQS, fan-out to SNS, event-driven to EventBridge, minimal-downtime server migration to MGN, heterogeneous database migration to DMS plus SCT, and offline bulk transfer to Snow Family.
- With 75 questions in 180 minutes you have roughly 2.4 minutes each; flag long multi-part scenarios, answer the quick ones first, and budget time to revisit flagged questions.

---

Want the full breakdown? See the complete **[AWS SAP-C02 study guide](https://certgrid.app/study-guide/aws-sap-c02-solutions-architect-professional)** and **[free practice questions](https://certgrid.app/practice/aws-sap-c02-solutions-architect-professional)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

