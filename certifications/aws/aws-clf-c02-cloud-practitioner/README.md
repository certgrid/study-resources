# AWS CLF-C02: Cloud Practitioner - Study Cheatsheet

The AWS Certified Cloud Practitioner (CLF-C02) validates a foundational, high-level understanding of the AWS Cloud, its core services, security and compliance model, architecture, pricing, and support options. It is aimed at people in technical, managerial, sales, purchasing, or financial roles who need cloud fluency without deep hands-on engineering experience. The exam is 90 minutes, requires a scaled score of 700 out of 1000 to pass, and covers four weighted domains.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | AWS CLF-C02 |
| Credential | AWS CLF-C02: Cloud Practitioner |
| Level | Intermediate |
| Practice mock length | ~65 questions |
| Duration | ~90 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-06-23 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Cloud Concepts | ~23% |
| 2 | Security and Compliance | ~24% |
| 3 | Cloud Technology and Services | ~33% |
| 4 | Billing, Pricing, and Support | ~20% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Cloud Concepts

- The six AWS Well-Architected Framework pillars are Operational Excellence, Security, Reliability, Performance Efficiency, Cost Optimization, and Sustainability (Sustainability was added as the sixth pillar in 2021).
- The AWS Shared Responsibility Model splits duties: AWS secures 'OF the cloud' (hardware, data centers, the global infrastructure, managed-service software), while the customer secures 'IN the cloud' (data, IAM, OS patching on EC2, security group rules, encryption configuration).
- Cloud value propositions include: trade fixed/capital expense (CapEx) for variable/operational expense (OpEx), benefit from massive economies of scale, stop guessing capacity, increase speed and agility, stop spending on running data centers, and go global in minutes.
- IaaS gives the most control over IT resources (you manage the OS, runtime, and applications on virtualized hardware); PaaS abstracts the OS and infrastructure (e.g. Elastic Beanstalk, RDS); SaaS delivers a ready-to-use application.
- An AWS Region is a physical geographic location; an Availability Zone (AZ) is one or more discrete data centers with redundant power, networking, and connectivity, physically isolated within a Region; Edge Locations cache content for CloudFront close to users.
- Deploying an application across multiple Availability Zones is the primary pattern for achieving high availability and fault tolerance.

### Domain 2 - Security and Compliance

- Always enable MFA on the AWS account root user and avoid using the root user for daily tasks; create individual IAM users/roles instead and grant least-privilege permissions.
- In IAM policy evaluation, an explicit Deny always overrides any Allow; by default access is implicitly denied unless explicitly allowed.
- IAM roles let EC2 instances and other AWS services obtain temporary credentials to access AWS services securely, eliminating the need to embed long-term access keys in code.
- AWS CloudTrail records account API activity (who, when, from where, what resource) for governance, auditing, and compliance; Amazon CloudWatch is for performance/operational monitoring and alarms.
- AWS Config continuously records and evaluates resource configurations against desired-state rules to assess compliance over time.
- Amazon GuardDuty is the intelligent threat-detection service that analyzes logs (VPC Flow Logs, CloudTrail, DNS) for malicious activity; Amazon Inspector performs automated vulnerability assessments on EC2 instances, containers, and Lambda.

### Domain 3 - Cloud Technology and Services

- Amazon EC2 provides resizable virtual servers; you control the OS, instance type, and networking. Pricing models include On-Demand, Reserved Instances, Spot Instances, and Savings Plans.
- Container and serverless compute: Amazon ECS and EKS orchestrate containers, AWS Fargate runs containers serverlessly (no instances to manage), and AWS Lambda runs event-driven code with no servers.
- Amazon S3 is object storage with 11 nines (99.999999999%) of durability, virtually unlimited capacity, and a maximum single-object size of 5 TB; S3 can also host static websites (HTML/CSS/JS).
- S3 storage classes: S3 Standard (frequent access), S3 Standard-Infrequent Access (S3 Standard-IA, immediate retrieval with a per-GB fee), S3 One Zone-IA, and S3 Glacier tiers for low-cost archival.
- Block vs file vs object storage: Amazon EBS provides block storage volumes attached to a single EC2 instance; Amazon EFS provides shared NFS file storage usable by many Linux EC2 instances at once; S3 is object storage accessed via API.
- Managed databases: Amazon RDS is a managed relational database (MySQL, PostgreSQL, MariaDB, Oracle, SQL Server) handling patching/backups/failover; Amazon Aurora is MySQL/PostgreSQL-compatible with up to 5x MySQL performance.

### Domain 4 - Billing, Pricing, and Support

- EC2 pricing models: On-Demand (pay per use, no commitment), Reserved Instances (1- or 3-year commitment for up to ~72% savings on steady workloads), Spot Instances (spare capacity up to ~90% off but can be interrupted), and Savings Plans (commit to hourly spend for discounts).
- The greatest EC2 savings come from a 3-year, all-upfront Reserved Instance term; Spot Instances best suit fault-tolerant, interruption-tolerant batch workloads.
- Compute Savings Plans apply flexibly across any EC2 instance family, size, OS, tenancy, and Region, and also cover Fargate and Lambda usage; EC2 Instance Savings Plans are tied to a specific instance family in a Region.
- The four AWS Support plans are Basic (free), Developer, Business, and Enterprise; only Enterprise (and Enterprise On-Ramp) includes a designated Technical Account Manager (TAM) and a concierge support team.
- Enterprise Support offers a 15-minute response-time target for business-critical system-down cases and 24/7 access; it also includes Infrastructure Event Management.
- AWS Trusted Advisor inspects your environment across five categories: cost optimization, performance, security, fault tolerance, and service limits; all customers get core checks but the full set requires Business or Enterprise Support.

## Study tips

- Master the Shared Responsibility Model and use it as a tiebreaker: if a question is about the OS, data, IAM, or security group config, it is the customer's job; if it is about physical hardware or the underlying service, it is AWS's job.
- Learn to match the service to the keyword. Questions are heavily service-identification based: 'threat detection' = GuardDuty, 'sensitive data in S3' = Macie, 'compliance reports' = Artifact, 'DDoS' = Shield, 'web exploits' = WAF, 'API auditing' = CloudTrail.
- Memorize the four cost-saving levers (Reserved Instances, Spot, Savings Plans, right-sizing) and which Support plan unlocks a TAM (Enterprise only) and full Trusted Advisor (Business/Enterprise).
- Eliminate obviously wrong distractors first. The exam often pairs the correct service with three services from a completely different category, so recognizing 'this is a database question, so RDS/DynamoDB/Aurora' narrows it fast.
- Watch for absolute words and outdated numbers: the Well-Architected Framework now has six pillars (not five), and there are six CAF perspectives. Flag any question you are unsure of and return to it, since all questions are weighted equally and there is no penalty for guessing.

---

Want the full breakdown? See the complete **[AWS CLF-C02 study guide](https://certgrid.app/study-guide/aws-clf-c02-cloud-practitioner)** and **[free practice questions](https://certgrid.app/practice/aws-clf-c02-cloud-practitioner)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

