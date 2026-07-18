# AWS Certified Cloud Practitioner (CLF-C02) - Study Guide

The AWS Certified Cloud Practitioner (CLF-C02) validates a foundational, high-level understanding of the AWS Cloud: its value proposition, core services, security and compliance model, architecture, pricing, and support options. It is aimed at people in technical, managerial, sales, purchasing, or financial roles who need cloud fluency without deep hands-on engineering experience, and it is the natural entry point before role-based associate certifications. The exam is 90 minutes, has 65 questions (multiple choice and multiple response), and requires a scaled score of 700 out of 1000 to pass. Questions reward recognition and correct service selection over deep configuration, so breadth beats depth here.

## Exam at a glance

| Item                | Detail                                                             |
| ------------------- | ------------------------------------------------------------------ |
| Exam code           | CLF-C02                                                            |
| Credential          | AWS Certified Cloud Practitioner                                   |
| Level               | Foundational (Beginner)                                            |
| Questions           | 65 (multiple choice / multiple response; ~15 are unscored)         |
| Duration            | 90 minutes                                                         |
| Passing score       | 700 out of 1000 (scaled)                                           |
| Delivery            | Pearson VUE test center or online proctored                        |
| Last verified       | 2026-07-18                                                         |
| Official exam guide | https://aws.amazon.com/certification/certified-cloud-practitioner/ |

## Domains

| #   | Domain                        | Weight |
| --- | ----------------------------- | ------ |
| 1   | Cloud Concepts                | 24%    |
| 2   | Security and Compliance       | 30%    |
| 3   | Cloud Technology and Services | 34%    |
| 4   | Billing, Pricing, and Support | 12%    |

_These weights are the official CLF-C02 content-outline weights. Weightings can be adjusted by AWS between exam guide revisions, so confirm the current objectives on the vendor site before your exam. Note that Domains 2 and 3 together make up nearly two thirds of the exam, so budget your study time accordingly._

## How to use this guide

Work top to bottom once for coverage, then use the tables as your revision layer. The exam is overwhelmingly about matching a scenario keyword to the single correct service or concept ('threat detection' points to GuardDuty, 'DDoS' points to Shield, 'no servers to manage' points to Lambda or Fargate), so the comparison and 'Service picker' tables are the highest-value material. Read the 'Common confusions' and 'Exam traps' notes in each domain closely, since most wrong answers on this exam come from mixing up two similar services rather than from not knowing a service at all. Finish with the readiness checklist and pair the guide with timed practice questions to expose gaps.

## Key concepts by domain

### Domain 1 - Cloud Concepts

This domain covers why organizations move to the cloud, the economics of that shift, the AWS Well-Architected Framework, cloud design principles, and the global infrastructure that everything else runs on.

**Benefits of the cloud**

- Trade capital expense (CapEx) for variable operational expense (OpEx): pay only for what you consume instead of buying data centers and servers upfront.
- Benefit from massive economies of scale: aggregated usage across millions of customers gives lower pay-as-you-go pricing than any single organization could achieve.
- Stop guessing capacity: scale up or down on demand instead of over-provisioning for a peak that may never come or under-provisioning and running out.
- Increase speed and agility: new IT resources are a few clicks away, cutting provisioning time from weeks to minutes.
- Stop spending money running and maintaining data centers: focus on customers and applications, not racking, cooling, and power.
- Go global in minutes: deploy in multiple AWS Regions worldwide to give users lower latency with no long-term footprint.

**Cloud economics (CapEx vs OpEx and TCO)**

| Concept                       | CapEx (traditional data center)                      | OpEx (cloud)                                          |
| ----------------------------- | ---------------------------------------------------- | ----------------------------------------------------- |
| Spending shape                | Large upfront purchase, depreciated over years       | Ongoing, pay-as-you-go per usage                      |
| Capacity                      | Fixed; must guess ahead                              | Elastic; matches real demand                          |
| Risk                          | Over- or under-provisioning                          | Right-size continuously                               |
| Total Cost of Ownership (TCO) | Includes hardware, facilities, power, cooling, staff | Includes usage fees plus reduced operational overhead |
| Time to value                 | Weeks to months                                      | Minutes                                               |

- TCO comparisons should include hidden on-premises costs (real estate, power, cooling, hardware refresh cycles, staffing) that the cloud absorbs into the service price.
- Cloud models: IaaS gives the most control (you manage the OS, runtime, and apps on virtualized hardware, for example EC2); PaaS abstracts the OS and infrastructure (for example Elastic Beanstalk, RDS); SaaS delivers a finished application you just consume.
- Deployment models: cloud (all in AWS), hybrid (AWS connected to on-premises, for example via AWS Direct Connect or AWS Outposts), and on-premises / private cloud.

**The six AWS Well-Architected Framework pillars**

| Pillar                 | Focus                                                                         |
| ---------------------- | ----------------------------------------------------------------------------- |
| Operational Excellence | Run and monitor systems, continually improve processes and procedures         |
| Security               | Protect data, systems, and assets; apply least privilege and defense in depth |
| Reliability            | Recover from failure, scale to meet demand, avoid single points of failure    |
| Performance Efficiency | Use compute resources efficiently and evolve as needs change                  |
| Cost Optimization      | Avoid unnecessary cost, pick the right pricing model, right-size              |
| Sustainability         | Minimize the environmental impact of running cloud workloads                  |

- Sustainability is the sixth and most recently added pillar; a question listing only five pillars or omitting Sustainability is a common trap.
- The AWS Cloud Adoption Framework (CAF) is different from Well-Architected: CAF organizes an organization's cloud journey into six perspectives (Business, People, Governance, Platform, Security, Operations), while Well-Architected reviews a specific workload.

**Cloud design principles**

- Design for failure and assume nothing lasts forever: build in redundancy across Availability Zones and treat servers as disposable.
- Decouple components (for example with Amazon SQS or Amazon SNS) so one failing part does not take down the whole system.
- Scale horizontally (add more instances) rather than only vertically (bigger instances) for elasticity and fault tolerance.
- Automate everything you can, and use managed services to reduce operational burden.

**Global infrastructure basics**

| Element                            | What it is                                                                                                  | Exam cue                                                   |
| ---------------------------------- | ----------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| Region                             | A physical geographic area containing multiple, isolated Availability Zones                                 | Data residency, latency to users, service availability     |
| Availability Zone (AZ)             | One or more discrete data centers with independent power, cooling, and networking, isolated within a Region | High availability and fault tolerance within a Region      |
| Edge location                      | A site that caches content and serves DNS close to end users                                                | Amazon CloudFront delivery, Amazon Route 53, lower latency |
| Local Zone / Wavelength / Outposts | Extends AWS closer to users, telecom 5G networks, or on-premises                                            | Ultra-low latency or hybrid on-premises needs              |

- Deploying across multiple Availability Zones is the primary pattern for high availability and fault tolerance; deploying across multiple Regions adds disaster recovery and data-residency options.
- Choose a Region based on compliance and data-residency laws, proximity to users (latency), available services, and pricing (which varies by Region).

**Common confusions:** Region vs Availability Zone vs Edge location; Well-Architected Framework (reviews a workload) vs Cloud Adoption Framework (guides the whole migration); IaaS vs PaaS vs SaaS responsibility split.

**Exam traps:** The Well-Architected Framework has six pillars (Sustainability is easy to forget). Edge locations are for content delivery and DNS, not for running your application servers. Economies of scale is the reason cloud pricing keeps dropping, not a customer action.

### Domain 2 - Security and Compliance

This is the single heaviest domain at 30%. It centers on who is responsible for what (the Shared Responsibility Model), identity and access management, and the catalog of AWS security, governance, and compliance services.

**AWS Shared Responsibility Model**

| Responsibility             | Owner    | Examples                                                                                                                                              |
| -------------------------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| Security OF the cloud      | AWS      | Physical data centers, hardware, the global network, the virtualization layer, managed-service software                                               |
| Security IN the cloud      | Customer | Customer data, IAM users and permissions, OS patching on EC2, security group rules, network configuration, encryption settings                        |
| Shared / varies by service | Both     | Patch management and configuration shift toward AWS for managed services (for example, AWS patches the RDS engine but you manage RDS access and data) |

- The more managed the service, the more responsibility shifts to AWS. On EC2 (IaaS) you patch the guest OS; on RDS or Lambda, AWS handles the underlying OS and you focus on data and access.
- Rule of thumb: if the question is about data, IAM, OS on EC2, or security group rules, it is the customer's job; if it is about physical hardware or the underlying platform, it is AWS's job.

**Identity and Access Management (IAM)**

| IAM object | What it is                                                 | Use it for                                                     |
| ---------- | ---------------------------------------------------------- | -------------------------------------------------------------- |
| Root user  | The account owner login created at sign-up                 | Only a few account-level tasks; secure it and do not use daily |
| IAM user   | A long-lived identity for a person or app                  | Individual human or programmatic access                        |
| IAM group  | A collection of users sharing permissions                  | Assign permissions by job function                             |
| IAM role   | An identity assumed temporarily for short-term credentials | EC2 instances, Lambda, cross-account access, federation        |
| IAM policy | A JSON document granting or denying permissions            | Attach to users, groups, or roles                              |

- Secure the root user first: enable MFA, do not create access keys for it, and use it only for the handful of tasks that require it (for example closing the account or changing the support plan).
- Apply least privilege: grant only the permissions a task requires, and prefer roles over embedding long-term access keys in code.
- Policy evaluation logic: access is denied by default (implicit deny); an explicit Allow grants access; an explicit Deny always overrides any Allow.
- Multi-factor authentication (MFA) adds a second factor (hardware key, virtual authenticator, or passkey) on top of the password and is strongly recommended for the root user and all privileged users.
- IAM Identity Center provides centralized workforce single sign-on across multiple AWS accounts and business applications, replacing per-account IAM users for human access at scale.

**AWS Organizations and Service Control Policies (SCPs)**

- AWS Organizations lets you centrally manage multiple AWS accounts, group them into Organizational Units (OUs), and get consolidated billing.
- Service Control Policies (SCPs) are guardrails that set the maximum available permissions for accounts or OUs; they do not grant permissions by themselves, they only limit what IAM can allow.
- AWS Control Tower sits on top of Organizations to set up and govern a secure, multi-account landing zone using best-practice guardrails.

**Security, detection, and protection services**

| Service                       | One-line purpose                                                                             |
| ----------------------------- | -------------------------------------------------------------------------------------------- |
| Amazon GuardDuty              | Intelligent threat detection from analyzing CloudTrail, VPC Flow Logs, and DNS logs          |
| Amazon Inspector              | Automated vulnerability assessment for EC2, container images, and Lambda                     |
| Amazon Macie                  | Discovers and protects sensitive data (for example PII) in Amazon S3                         |
| AWS Security Hub              | Central dashboard aggregating findings and security posture across accounts                  |
| AWS Shield                    | DDoS protection (Standard is free and automatic; Advanced is paid, with 24/7 response)       |
| AWS WAF                       | Web application firewall filtering common web exploits (SQL injection, cross-site scripting) |
| AWS KMS                       | Managed creation and control of encryption keys                                              |
| AWS CloudHSM                  | Dedicated hardware security modules for stricter key-custody requirements                    |
| AWS Secrets Manager           | Stores, rotates, and retrieves secrets such as database credentials and API keys             |
| AWS Certificate Manager (ACM) | Provisions and manages TLS/SSL certificates for encryption in transit                        |
| AWS CloudTrail                | Records account API activity (who did what, when, from where) for audit                      |

- CloudTrail is for auditing API history (governance and compliance); Amazon CloudWatch is for performance and operational monitoring. Do not swap them.
- Encryption: at rest is protected with KMS-managed keys (for example SSE-S3 or SSE-KMS on Amazon S3, encrypted EBS volumes); in transit is protected with TLS certificates from ACM.

**Compliance and governance**

| Service           | Purpose                                                                                 |
| ----------------- | --------------------------------------------------------------------------------------- |
| AWS Artifact      | Self-service portal for on-demand compliance reports (SOC, ISO, PCI DSS) and agreements |
| AWS Config        | Records and evaluates resource configurations against desired-state rules over time     |
| AWS Audit Manager | Automates evidence collection to help with audits against frameworks                    |

- AWS Artifact is where you download compliance attestations and reports; AWS Config is where you track configuration drift and evaluate compliance rules continuously.
- AWS maps its controls to well-known frameworks such as PCI DSS, HIPAA, ISO 27001, SOC 1/2/3, FedRAMP, and GDPR; compliance is a shared outcome under the Shared Responsibility Model.

**Common confusions:** GuardDuty (threat detection from logs) vs Inspector (vulnerability scanning of resources) vs Macie (sensitive data discovery in S3); CloudTrail (API audit) vs CloudWatch (metrics and monitoring) vs Config (configuration compliance); IAM user (person/app) vs IAM role (temporary, assumed); Artifact (get reports) vs Config (track configuration).

**Exam traps:** SCPs restrict permissions, they never grant them. Shield Standard is free and on by default; Shield Advanced is paid. An explicit Deny always wins over any Allow. The root user should have MFA and should not be used for daily work.

### Domain 3 - Cloud Technology and Services

The largest domain at 34%. It is mostly service identification across compute, storage, databases, networking, and management, plus the ways you interact with AWS.

**Ways to access AWS**

| Method                 | What it is                                              | Best for                                    |
| ---------------------- | ------------------------------------------------------- | ------------------------------------------- |
| AWS Management Console | Web-based GUI                                           | Learning, one-off tasks, visual management  |
| AWS CLI                | Command-line interface                                  | Scripting and repeatable commands           |
| AWS SDKs               | Language libraries (Python, Java, JavaScript, and more) | Building AWS calls into applications        |
| Infrastructure as Code | AWS CloudFormation templates and AWS CDK                | Repeatable, version-controlled provisioning |

- AWS CloudFormation provisions and manages resources declaratively from templates so an entire environment can be recreated consistently; the AWS Cloud Development Kit (CDK) lets you define that infrastructure in familiar programming languages.

**Compute**

| Option                  | Model                                                                  | Use when                                                                 |
| ----------------------- | ---------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| Amazon EC2              | Virtual servers you manage                                             | You need full control of the OS and instance                             |
| AWS Lambda              | Serverless functions, event-driven                                     | Short-lived code with no servers to manage; pay per request and duration |
| Amazon ECS / Amazon EKS | Container orchestration (ECS is AWS-native, EKS is managed Kubernetes) | Running containerized apps at scale                                      |
| AWS Fargate             | Serverless compute engine for containers                               | Containers without managing the underlying EC2 hosts                     |
| AWS Elastic Beanstalk   | Platform as a Service that deploys and manages your app                | Upload code and let AWS handle capacity, load balancing, and scaling     |
| Amazon Lightsail        | Simple bundles of compute, storage, and networking                     | Small, predictable workloads and simple websites                         |

- EC2 instance families map to workloads: General Purpose (balanced), Compute Optimized (CPU-heavy), Memory Optimized (large in-memory data), Storage Optimized (high disk I/O), and Accelerated Computing (GPUs for ML and graphics).
- EC2 Auto Scaling adds or removes instances automatically to match demand, improving both availability and cost efficiency; Elastic Load Balancing (ELB) distributes incoming traffic across healthy instances (Application, Network, and Gateway Load Balancers).
- Amazon ECR stores container images; Fargate removes the need to provision or patch EC2 hosts for your containers.

**Storage**

| Type               | Service             | Nature                                                       | Use for                                                  |
| ------------------ | ------------------- | ------------------------------------------------------------ | -------------------------------------------------------- |
| Object             | Amazon S3           | Objects via API, virtually unlimited                         | Backups, static websites, data lakes, media              |
| Block              | Amazon EBS          | Volumes attached to one EC2 instance                         | Boot volumes, databases on EC2                           |
| File               | Amazon EFS          | Shared NFS file system for many Linux instances              | Shared file storage across instances                     |
| File (Windows/HPC) | Amazon FSx          | Managed file systems (Windows File Server, Lustre, and more) | Windows workloads, high-performance computing            |
| Archive            | Amazon S3 Glacier   | Low-cost cold storage tiers within S3                        | Long-term archive and compliance retention               |
| Hybrid             | AWS Storage Gateway | Bridges on-premises to AWS storage                           | Extending or backing up on-premises storage to the cloud |

- Amazon S3 delivers 99.999999999% (11 nines) durability, virtually unlimited capacity, a maximum single-object size of 5 TB, and can host static websites.
- Amazon EBS is block storage attached to a single instance; Amazon EFS is shared file storage many Linux instances can mount at once; Amazon S3 is object storage accessed by API. Know these three apart.

**Amazon S3 storage classes**

| Class                                       | Best for                                    | Notes                                         |
| ------------------------------------------- | ------------------------------------------- | --------------------------------------------- |
| S3 Standard                                 | Frequently accessed data                    | Default; highest cost, immediate access       |
| S3 Intelligent-Tiering                      | Unknown or changing access patterns         | Auto-moves objects between tiers to save cost |
| S3 Standard-Infrequent Access (Standard-IA) | Infrequent but immediate-access data        | Lower storage cost, per-GB retrieval fee      |
| S3 One Zone-IA                              | Infrequent, non-critical, re-creatable data | Cheaper, stored in one AZ only                |
| S3 Glacier Instant Retrieval                | Archive needing millisecond access          | Cheaper than IA for rarely accessed data      |
| S3 Glacier Flexible Retrieval               | Archive with minutes-to-hours retrieval     | Very low cost                                 |
| S3 Glacier Deep Archive                     | Long-term archive, 12+ hour retrieval       | Lowest cost                                   |

- S3 Lifecycle policies automatically transition objects to cheaper classes over time (for example Standard to Standard-IA to Glacier Deep Archive).

**Databases**

| Service            | Type                                                                | Use for                                                              |
| ------------------ | ------------------------------------------------------------------- | -------------------------------------------------------------------- |
| Amazon RDS         | Managed relational (MySQL, PostgreSQL, MariaDB, Oracle, SQL Server) | Traditional relational apps with managed patching, backups, failover |
| Amazon Aurora      | Managed relational, MySQL/PostgreSQL-compatible                     | Higher performance and availability than standard RDS engines        |
| Amazon DynamoDB    | Serverless NoSQL key-value and document                             | Single-digit-millisecond, massive-scale, schemaless workloads        |
| Amazon Redshift    | Data warehouse (OLAP)                                               | Analytics and reporting over large historical datasets               |
| Amazon ElastiCache | In-memory cache (Redis, Memcached)                                  | Sub-millisecond caching to offload databases                         |

- RDS and Aurora are relational (structured, SQL, joins); DynamoDB is NoSQL (key-value/document, serverless, auto-scaling); Redshift is for analytics warehousing, not transactional apps. Other purpose-built databases include Amazon DocumentDB (document), Amazon Neptune (graph), and Amazon MemoryDB (in-memory, durable).
- Amazon RDS Multi-AZ deployments provide high availability with a standby in another AZ; read replicas scale read traffic.

**Networking and content delivery**

| Service                | Purpose                                                                                          |
| ---------------------- | ------------------------------------------------------------------------------------------------ |
| Amazon VPC             | Your isolated virtual network in AWS                                                             |
| Subnets                | Segments of a VPC; public subnets reach the internet, private subnets do not                     |
| Route tables           | Control where subnet traffic is directed                                                         |
| Internet gateway       | Allows resources in public subnets to reach the internet                                         |
| NAT gateway            | Lets private-subnet resources make outbound internet connections without being reachable inbound |
| Security groups        | Stateful virtual firewall at the instance level (allow rules only)                               |
| Network ACLs (NACLs)   | Stateless firewall at the subnet level (allow and deny rules)                                    |
| Amazon Route 53        | Scalable DNS and domain registration with health-based routing                                   |
| Amazon CloudFront      | Content delivery network caching content at edge locations                                       |
| AWS Direct Connect     | Dedicated private physical connection from on-premises to AWS                                    |
| AWS VPN                | Encrypted tunnel over the internet to your VPC                                                   |
| AWS Global Accelerator | Improves availability and performance using the AWS global network and anycast IPs               |

**Security groups vs network ACLs**

| Attribute  | Security group                         | Network ACL                            |
| ---------- | -------------------------------------- | -------------------------------------- |
| Scope      | Instance (ENI) level                   | Subnet level                           |
| State      | Stateful (return traffic auto-allowed) | Stateless (must allow both directions) |
| Rules      | Allow rules only                       | Allow and Deny rules                   |
| Evaluation | All rules evaluated together           | Rules evaluated in numbered order      |

**Management and governance**

| Service              | Purpose                                                                                                              |
| -------------------- | -------------------------------------------------------------------------------------------------------------------- |
| Amazon CloudWatch    | Metrics, logs, dashboards, and alarms for monitoring                                                                 |
| AWS CloudTrail       | Records API activity for audit and compliance                                                                        |
| AWS Config           | Tracks resource configuration and compliance over time                                                               |
| AWS Systems Manager  | Operational management, patching, and automation across resources                                                    |
| AWS Trusted Advisor  | Best-practice checks across cost, performance, security, fault tolerance, service limits, and operational excellence |
| AWS CloudFormation   | Infrastructure as code provisioning                                                                                  |
| AWS Health Dashboard | Personalized view of AWS service health affecting your account                                                       |

- Analytics services worth recognizing: Amazon Athena (query S3 with SQL), AWS Glue (serverless ETL), Amazon EMR (big-data processing), Amazon Kinesis (real-time streaming), and Amazon QuickSight (business-intelligence dashboards).
- Application integration services: Amazon SQS (message queues), Amazon SNS (pub/sub notifications), Amazon EventBridge (event bus), AWS Step Functions (workflows), and Amazon API Gateway (managed APIs).
- AI/ML services: Amazon SageMaker (build, train, deploy models), Amazon Bedrock (build with foundation models), and task-specific services such as Amazon Rekognition (images/video), Amazon Comprehend (natural-language processing), Amazon Polly (text to speech), Amazon Transcribe (speech to text), Amazon Translate, and Amazon Textract (document extraction).

**Common confusions:** EC2 (you manage the server) vs Lambda/Fargate (serverless); EBS vs EFS vs S3; security group (stateful, instance, allow-only) vs NACL (stateless, subnet, allow and deny); Route 53 (DNS) vs CloudFront (CDN); Direct Connect (private physical link) vs VPN (encrypted over internet).

**Exam traps:** Lambda has no servers to manage and is billed per request and duration. NAT gateways enable outbound-only internet for private subnets. Redshift is analytics, not a transactional database. Global Accelerator uses the AWS backbone and static anycast IPs, whereas CloudFront caches content at the edge.

### Domain 4 - Billing, Pricing, and Support

The smallest domain at 12%, but full of quick, high-yield facts on how AWS charges you, how to control cost, and which support plan to choose.

**EC2 and compute pricing models**

| Model                    | How it works                                         | Best for                                                | Savings      |
| ------------------------ | ---------------------------------------------------- | ------------------------------------------------------- | ------------ |
| On-Demand                | Pay per second/hour, no commitment                   | Short-term, spiky, or unpredictable workloads           | Baseline     |
| Reserved Instances (RIs) | 1- or 3-year commitment to an instance configuration | Steady-state, predictable workloads                     | Up to ~72%   |
| Savings Plans            | Commit to an hourly spend for 1 or 3 years           | Flexible steady usage across EC2, Fargate, Lambda       | Up to ~72%   |
| Spot Instances           | Bid on spare capacity, can be reclaimed              | Fault-tolerant, interruption-tolerant batch and CI work | Up to ~90%   |
| Dedicated Hosts          | A physical server dedicated to you                   | Licensing tied to hardware, compliance isolation        | Highest cost |

- The deepest committed discounts come from a 3-year, all-upfront term. Spot is cheapest of all but can be interrupted with a short warning, so use it only for workloads that tolerate interruption.
- Compute Savings Plans apply flexibly across any EC2 instance family, size, OS, tenancy, and Region, and also cover Fargate and Lambda; EC2 Instance Savings Plans are tied to a specific instance family in a Region for a bigger discount but less flexibility.
- Core pricing principles: pay as you go, pay less when you reserve, pay less with volume as you grow. You are generally charged for compute time, storage, and data transfer OUT of AWS (inbound data transfer is typically free).

**AWS Free Tier**

| Type           | What it gives                                 | Example                                                                  |
| -------------- | --------------------------------------------- | ------------------------------------------------------------------------ |
| Always Free    | No expiry, within monthly limits              | 1 million AWS Lambda requests per month, 25 GB DynamoDB                  |
| 12 Months Free | Free for the first year after sign-up         | 750 hours/month of a t2.micro or t3.micro EC2 instance, 5 GB S3 Standard |
| Trials         | Short-term free trial from service activation | Time-limited access to specific services                                 |

- AWS also offers a newer credit-based plan for new accounts (up to 200 USD in credits over an initial period, plus 30+ always-free services). For the exam, the classic three Free Tier categories (Always Free, 12 Months Free, Trials) remain the safe frame of reference.

**Consolidated billing and cost management tools**

| Tool                                      | Purpose                                                                                          |
| ----------------------------------------- | ------------------------------------------------------------------------------------------------ |
| AWS Organizations (consolidated billing)  | One bill for all accounts, shared volume discounts and Reserved Instance / Savings Plan benefits |
| AWS Billing (Billing and Cost Management) | View and pay bills, see charges by service                                                       |
| AWS Cost Explorer                         | Visualize and analyze cost and usage trends over time, and forecast                              |
| AWS Budgets                               | Set custom cost or usage budgets and get alerts when thresholds are crossed                      |
| AWS Cost and Usage Report (CUR)           | The most detailed, line-item billing data for deep analysis                                      |
| AWS Pricing Calculator                    | Estimate the cost of a planned architecture before you build it                                  |

- Consolidated billing through Organizations aggregates usage across accounts so you reach volume-pricing tiers faster and can share Reserved Instance and Savings Plan discounts.
- Cost Explorer analyzes and forecasts what you have already spent; AWS Budgets alerts you before or as you exceed a target; the Pricing Calculator estimates a future workload. Do not mix these three.
- AWS Trusted Advisor includes cost-optimization checks (idle load balancers, underutilized EC2 instances, unassociated Elastic IPs, unused EBS volumes) alongside its performance, security, fault tolerance, service limits, and operational excellence checks. Core checks are available to all; the full set requires Business or Enterprise Support.
- Cost allocation tags let you label resources so spend can be grouped and reported by project, team, or environment.

**AWS Support plans**

| Plan               | Cost model            | Key inclusions                                                                        | Response target (highest severity)          |
| ------------------ | --------------------- | ------------------------------------------------------------------------------------- | ------------------------------------------- |
| Basic              | Free for all accounts | Documentation, whitepapers, forums, core Trusted Advisor checks, Health Dashboard     | No technical case support                   |
| Developer          | Paid (lowest tier)    | Business-hours email/web access to Support, general guidance                          | System impaired: < 12 business hours        |
| Business           | Paid                  | 24/7 phone, email, and chat; full Trusted Advisor; third-party software support       | Production system down: < 1 hour            |
| Enterprise On-Ramp | Paid                  | Adds a pool of Technical Account Managers (TAMs), Concierge support access            | Business-critical system down: < 30 minutes |
| Enterprise         | Paid (highest tier)   | Designated TAM, Concierge billing team, Infrastructure Event Management, full support | Business-critical system down: < 15 minutes |

- Only Enterprise Support includes a designated Technical Account Manager (TAM); Enterprise On-Ramp provides a pool of TAMs. The Concierge support team (billing and account guidance) comes with Enterprise On-Ramp and Enterprise.
- The full set of Trusted Advisor checks and 24/7 technical support (phone/chat) start at the Business plan. Basic and Developer do not include 24/7 technical case support.
- AWS has announced changes taking effect in 2027 (Developer Support and Enterprise On-Ramp being retired, with customers moving to Business or Enterprise). For CLF-C02 today, expect all five plans above to appear as answer options.

**Additional support and self-help resources**

- AWS Marketplace is a curated digital catalog to find, buy, and deploy third-party software that runs on AWS, with billing consolidated onto your AWS bill.
- AWS re:Post is the community Q and A service; the AWS Knowledge Center answers common technical questions; the AWS Support Center is where you open and manage support cases.
- The AWS Health Dashboard shows service health, and AWS Professional Services and the AWS Partner Network (APN) provide expert and partner help for larger engagements.

**Common confusions:** Reserved Instances vs Savings Plans vs Spot; Cost Explorer (analyze past spend) vs Budgets (alert on thresholds) vs Pricing Calculator (estimate future cost); Basic vs Developer vs Business vs Enterprise support; TAM availability (Enterprise On-Ramp pool vs Enterprise designated).

**Exam traps:** Data transfer OUT is billed, data transfer IN is generally free. Spot is cheapest but interruptible. A designated TAM is Enterprise only. Consolidated billing is an AWS Organizations feature. Basic Support is free but includes no technical case support.

## Service picker (fast decisions)

**Compute**

| If you need...                            | Use                   |
| ----------------------------------------- | --------------------- |
| Full control of a virtual server          | Amazon EC2            |
| To run event-driven code with no servers  | AWS Lambda            |
| Containers without managing hosts         | AWS Fargate           |
| Managed Kubernetes                        | Amazon EKS            |
| Deploy an app and let AWS manage capacity | AWS Elastic Beanstalk |
| A simple, low-cost website or app bundle  | Amazon Lightsail      |

**Storage**

| If you need...                                    | Use                            |
| ------------------------------------------------- | ------------------------------ |
| Object storage for backups, media, or a data lake | Amazon S3                      |
| A disk volume for one EC2 instance                | Amazon EBS                     |
| Shared file storage for many Linux instances      | Amazon EFS                     |
| Windows or HPC file systems                       | Amazon FSx                     |
| Lowest-cost long-term archive                     | Amazon S3 Glacier Deep Archive |
| To connect on-premises storage to AWS             | AWS Storage Gateway            |

**Databases**

| If you need...                      | Use                |
| ----------------------------------- | ------------------ |
| A managed relational database       | Amazon RDS         |
| Higher-performance MySQL/PostgreSQL | Amazon Aurora      |
| Serverless NoSQL key-value at scale | Amazon DynamoDB    |
| A data warehouse for analytics      | Amazon Redshift    |
| Sub-millisecond in-memory caching   | Amazon ElastiCache |

**Networking**

| If you need...                        | Use                |
| ------------------------------------- | ------------------ |
| An isolated virtual network           | Amazon VPC         |
| DNS and domain routing                | Amazon Route 53    |
| To cache content near users           | Amazon CloudFront  |
| A dedicated private link to AWS       | AWS Direct Connect |
| An encrypted tunnel over the internet | AWS VPN            |
| Instance-level firewall rules         | Security groups    |

**Security**

| If you need...                      | Use              |
| ----------------------------------- | ---------------- |
| Threat detection from logs          | Amazon GuardDuty |
| Vulnerability scanning of resources | Amazon Inspector |
| To find sensitive data in S3        | Amazon Macie     |
| DDoS protection                     | AWS Shield       |
| To filter web exploits              | AWS WAF          |
| To manage encryption keys           | AWS KMS          |
| To audit API activity               | AWS CloudTrail   |
| Compliance reports on demand        | AWS Artifact     |

## Common confusions that decide pass/fail

| Concept A          | Concept B         | Key difference                                                                              |
| ------------------ | ----------------- | ------------------------------------------------------------------------------------------- |
| Security group     | Network ACL       | SG is stateful, instance-level, allow-only; NACL is stateless, subnet-level, allow and deny |
| Region             | Availability Zone | Region is a geographic area; an AZ is isolated data centers within a Region                 |
| Availability Zone  | Edge location     | AZ runs your workloads; edge location caches content (CloudFront) and serves DNS            |
| IAM user           | IAM role          | User is a long-lived identity; a role is assumed for temporary credentials                  |
| Reserved Instance  | Savings Plan      | RI commits to an instance config; a Savings Plan commits to hourly spend, more flexibly     |
| Savings Plan       | Spot Instance     | Savings Plan is a committed discount; Spot is cheap spare capacity that can be interrupted  |
| Shield Standard    | Shield Advanced   | Standard is free and automatic; Advanced is paid with 24/7 DDoS response                    |
| CloudTrail         | CloudWatch        | CloudTrail audits API calls; CloudWatch monitors metrics, logs, and alarms                  |
| CloudTrail         | AWS Config        | CloudTrail is who did what; Config is how resources are configured over time                |
| Cost Explorer      | AWS Budgets       | Cost Explorer analyzes past and forecasts spend; Budgets alerts on thresholds               |
| Pricing Calculator | Cost Explorer     | Pricing Calculator estimates a future build; Cost Explorer reviews actual usage             |
| Inspector          | GuardDuty         | Inspector scans resources for vulnerabilities; GuardDuty detects threats from logs          |
| GuardDuty          | Macie             | GuardDuty finds malicious activity; Macie finds and classifies sensitive data in S3         |
| Direct Connect     | VPN               | Direct Connect is a private physical link; VPN is encrypted over the public internet        |
| Enterprise On-Ramp | Enterprise        | On-Ramp gives a pool of TAMs; Enterprise gives a designated TAM                             |
| Artifact           | Config            | Artifact provides compliance reports; Config tracks configuration compliance                |

## 5-day study plan

This is a revision-paced plan for someone with a little cloud exposure. Complete beginners should stretch it over two to three weeks and add extra hands-on time in a free AWS account.

| Day | Focus                                                                                            | Domains                |
| --- | ------------------------------------------------------------------------------------------------ | ---------------------- |
| 1   | Cloud concepts, cloud economics, Well-Architected pillars, global infrastructure                 | Domain 1               |
| 2   | Shared Responsibility Model, IAM, Organizations and SCPs, security services                      | Domain 2               |
| 3   | Compute, storage, S3 classes, databases                                                          | Domain 3 (part 1)      |
| 4   | Networking, security groups vs NACLs, management and governance, analytics/integration/AI        | Domain 3 (part 2)      |
| 5   | Pricing models, Free Tier, cost tools, support plans, then a full timed practice mock and review | Domain 4 + full review |

## Readiness checklist

You are ready when you can...

- State each side of the Shared Responsibility Model and correctly place OS patching, IAM, data, security groups, and physical security.
- Name the six Well-Architected pillars, including Sustainability, and describe what each optimizes.
- Distinguish a Region, an Availability Zone, and an edge location, and explain when to use each.
- Choose the right compute option (EC2, Lambda, Fargate, Elastic Beanstalk, Lightsail) from a scenario.
- Pick the correct storage service (S3, EBS, EFS) and the right S3 storage class for an access pattern.
- Match a database need to RDS, Aurora, DynamoDB, Redshift, or ElastiCache.
- Tell a security group from a NACL, and CloudTrail from CloudWatch from Config.
- Map a security keyword to the right service (GuardDuty, Inspector, Macie, Shield, WAF, KMS, Artifact).
- Compare On-Demand, Reserved Instances, Savings Plans, and Spot, and know when each is cheapest.
- Recall what each support plan includes and which ones provide a TAM and full Trusted Advisor.
- Explain consolidated billing and tell Cost Explorer, AWS Budgets, and the Pricing Calculator apart.

---

Want the full breakdown? See the complete **[AWS Cloud Practitioner study guide](https://certgrid.app/study-guide/aws-clf-c02-cloud-practitioner)** and **[free practice questions](https://certgrid.app/practice/aws-clf-c02-cloud-practitioner)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_
