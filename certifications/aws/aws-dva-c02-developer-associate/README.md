# AWS DVA-C02: Developer Associate - Study Cheatsheet

The AWS Certified Developer - Associate (DVA-C02) validates your ability to develop, deploy, secure, and troubleshoot cloud-native applications on AWS using core services, the SDKs/CLI, and CI/CD tooling. It targets developers with one or more years of hands-on experience building and maintaining AWS applications. The exam is 130 minutes, contains roughly 65 scored questions, and requires a scaled score of 720 out of 1000 to pass.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | AWS DVA-C02 |
| Credential | AWS DVA-C02: Developer Associate |
| Level | Associate |
| Practice mock length | ~65 questions |
| Duration | ~130 minutes |
| Passing score | 720 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Development with AWS Services | ~35% |
| 2 | Security | ~20% |
| 3 | Deployment | ~19% |
| 4 | Troubleshooting and Optimization | ~26% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Development with AWS Services

- AWS Lambda is event-driven serverless compute triggered by API Gateway, S3, SQS, SNS, DynamoDB Streams, EventBridge, and more; you pay per request and per GB-second of execution.
- Lambda synchronous (RequestResponse) invocation returns the result to the caller; pass --invocation-type Event for asynchronous invocation, which queues the event and returns immediately.
- Choose a high-cardinality DynamoDB partition key so requests spread evenly across partitions and avoid hot partitions that throttle on a single key's throughput.
- A DynamoDB Global Secondary Index (GSI) lets you query on a non-key attribute with its own partition/sort key and its own provisioned/on-demand throughput; a Local Secondary Index (LSI) must share the table's partition key and be created at table creation.
- DynamoDB Accelerator (DAX) is an in-memory cache that cuts read latency to microseconds for eventually consistent reads; ElastiCache (Redis or Memcached) is a general-purpose cache for session state and hot reads in front of databases.
- Use AWS Step Functions to orchestrate multi-step workflows with built-in Retry and Catch states for error handling and a visual state machine; start runs with aws stepfunctions start-execution.

### Domain 2 - Security

- Lambda functions, EC2 instances, and ECS tasks should obtain AWS access through an IAM role (execution/instance/task role) that supplies temporary, auto-expiring credentials, never hard-coded access keys.
- Apply least privilege: grant only the specific actions and resources required, and prefer scoping resources by ARN rather than using wildcards.
- In IAM policy evaluation an explicit Deny always overrides any Allow; access is denied by default unless an Allow grants it and no Deny matches.
- Identity-based policies attach to a user, group, or role; resource-based policies (such as an S3 bucket policy or Lambda resource policy) attach to the resource and can grant cross-account access.
- Store secrets in AWS Secrets Manager or SSM Parameter Store (SecureString) encrypted with KMS, and have the application fetch them at runtime; never embed credentials in code or environment variables in plaintext.
- AWS Secrets Manager supports automatic rotation via a rotation Lambda; the app should always fetch the current secret value at runtime so it picks up rotated credentials.

### Domain 3 - Deployment

- Lambda and CodeDeploy support three deployment strategies: all-at-once, linear (shift a fixed percentage on an interval), and canary (shift a small percentage, wait, then shift the rest).
- AWS SAM is a CloudFormation extension for serverless apps; build with sam build then deploy with sam deploy, and SAM transforms shorthand resources into full CloudFormation.
- In SAM, set AutoPublishAlias so a new Lambda version is published and an alias points to it, and add DeploymentPreference (for example Type: Canary10Percent5Minutes) to shift alias traffic gradually via CodeDeploy.
- Lambda alias traffic shifting via CodeDeploy can auto-rollback when an associated CloudWatch alarm trips during the deployment.
- AWS CloudFormation provisions infrastructure as code; update a stack with aws cloudformation update-stack, and create a change set first to preview exactly what will change before executing.
- By default CloudFormation rolls a failed stack back to the last known good state; set OnFailure or disable rollback to retain resources for debugging.

### Domain 4 - Troubleshooting and Optimization

- Handle throttling and transient errors by retrying with exponential backoff and jitter; the AWS SDKs implement this automatically for retryable errors.
- Lambda cold starts add latency when a new execution environment initializes; configure Provisioned Concurrency to keep environments warm for latency-sensitive workloads.
- Lambda CPU is allocated in proportion to the memory setting, so increasing memory can speed up CPU-bound functions and sometimes lower overall cost by reducing duration.
- Reserved concurrency (aws lambda put-function-concurrency --reserved-concurrent-executions) caps and guarantees a function's concurrent executions; it is distinct from provisioned concurrency, which pre-warms environments.
- Use AWS X-Ray for distributed tracing: enable it with aws lambda update-function-configuration --tracing-config Mode=Active, then inspect the service map and trace segments/subsegments to find latency.
- Use Amazon CloudWatch for metrics, custom metrics, alarms, and dashboards; query metrics with aws cloudwatch get-metric-statistics using the correct namespace, dimensions, and time range.

## Study tips

- Read each scenario for the deciding constraint (lowest cost, least operational overhead, fully managed, real-time vs batch, strong vs eventual consistency) and eliminate options that violate it before picking.
- Memorize when to reach for each messaging service: SQS for decoupling and buffering, SNS for fan-out/pub-sub, EventBridge for event routing with rules, and Step Functions for multi-step orchestration with retries.
- Default to IAM roles and temporary credentials plus Secrets Manager/Parameter Store; any answer that hard-codes keys or embeds plaintext secrets is almost always wrong.
- Know the SAM/CodeDeploy traffic-shifting vocabulary cold (AutoPublishAlias, DeploymentPreference, Canary vs Linear vs AllAtOnce, alarm-based rollback) since these appear repeatedly in deployment questions.
- When a question is about latency, errors, or cost, map the symptom to the right tool first: CloudWatch metrics/alarms, CloudWatch Logs Insights for log queries, and X-Ray for end-to-end tracing across services.

---

Want the full breakdown? See the complete **[AWS DVA-C02 study guide](https://certgrid.app/study-guide/aws-dva-c02-developer-associate)** and **[free practice questions](https://certgrid.app/practice/aws-dva-c02-developer-associate)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

