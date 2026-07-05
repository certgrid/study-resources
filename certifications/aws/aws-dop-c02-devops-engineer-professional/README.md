# AWS DOP-C02: DevOps Engineer Professional - Study Cheatsheet

The AWS Certified DevOps Engineer - Professional (DOP-C02) validates advanced skills in building and operating automated, resilient systems on AWS, spanning CI/CD pipelines, infrastructure as code, monitoring, incident response, and security automation. It is a 180-minute, 75-question exam (scored 100-1000, passing at 750) aimed at engineers with two or more years of provisioning, operating, and managing AWS environments. Expect scenario-heavy questions that require choosing between similar valid services based on cost, blast radius, and operational overhead.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | AWS DOP-C02 |
| Credential | AWS DOP-C02: DevOps Engineer Professional |
| Level | Advanced |
| Practice mock length | ~75 questions |
| Duration | ~180 minutes |
| Passing score | 750 out of 1000 |
| Notes reviewed | 2026-06-23 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | SDLC Automation | ~17% |
| 2 | Configuration Management and IaC | ~16% |
| 3 | Resilient Cloud Solutions | ~15% |
| 4 | Monitoring and Logging | ~16% |
| 5 | Incident and Event Response | ~14% |
| 6 | Security and Compliance | ~22% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - SDLC Automation

- CodePipeline orchestrates source, build, test, and deploy stages; each stage can hold multiple actions that run in parallel (same runOrder) or sequentially (incrementing runOrder).
- Build the artifact once in an early stage and promote the same versioned artifact through every environment; never rebuild per stage, which risks environment drift.
- CodeBuild runs commands from a buildspec.yml; the install, pre_build, build, and post_build phases run in order, and the artifacts section defines which files become the output artifact.
- CodeBuild builds have a maximum timeout of 8 hours; a build exceeding it is terminated, so split long builds or offload work.
- To reach private resources (RDS, private endpoints) from a build, configure the CodeBuild project to run inside the VPC's private subnets with a security group; CodeBuild then loses default public internet access unless a NAT gateway is present.
- Inject secrets into CodeBuild via the buildspec env/secrets-manager (or parameter-store) mapping so values are pulled at runtime and not echoed in logs or stored in the template.

### Domain 2 - Configuration Management and IaC

- A single CloudFormation stack supports up to 500 resources; refactor large templates into nested stacks or modules to stay under the limit and improve reuse.
- Share values across stacks by declaring Outputs with Export and consuming them via Fn::ImportValue; an exported value cannot be changed or deleted while another stack imports it.
- Set DeletionPolicy: Retain (and UpdateReplacePolicy: Retain) on stateful resources like databases, and enable stack termination protection, to prevent accidental data loss.
- Some property updates force a replacement: CloudFormation creates a new resource and deletes the old one, which can drop data unless a Snapshot or Retain policy is set.
- Detect configuration drift with aws cloudformation detect-stack-drift, then review per-resource drift status to find out-of-band changes.
- Preview changes safely with change sets: aws cloudformation create-change-set --stack-name <s> --change-set-name <c> --template-body file://tpl.yaml, then execute after review.

### Domain 3 - Resilient Cloud Solutions

- An Auto Scaling group behind a load balancer with health checks provides self-healing: failed instances are terminated and replaced automatically to maintain desired capacity.
- Spread the Auto Scaling group across multiple Availability Zones so the loss of one AZ does not take down the application.
- Use ELB health checks (not only EC2 status checks) on an ASG so application-layer failures, not just hardware faults, mark instances unhealthy.
- Increase the ASG health check grace period when instances need long boot/initialization time, so they are not killed before the app is ready.
- Disaster recovery strategies trade cost for RTO/RPO: backup and restore (cheapest, slowest), pilot light, warm standby (scaled-down running copy), and multi-site active/active (fastest, costliest).
- Warm standby keeps scaled-down compute pre-provisioned in a second Region with continuous data replication, ready to scale up on failover.

### Domain 4 - Monitoring and Logging

- Publish custom metrics with aws cloudwatch put-metric-data --namespace MyApp --metric-name <m> --value <v>; metrics are namespace plus name plus dimensions.
- CloudWatch standard-resolution custom metrics aggregate to 1-minute granularity; set StorageResolution=1 for high-resolution 1-second metrics at higher cost.
- Create a metric from logs with put-metric-filter; a metric filter only emits a data point when a line matches, so configure missing-data treatment (or a default value of 0) for reliable alarming.
- Reduce alarm noise by requiring M out of N datapoints to breach over the evaluation window rather than alarming on a single spike.
- Composite alarms combine multiple alarms with AND/OR logic to alert only on meaningful correlated conditions and to suppress alarm storms.
- EC2 emits CloudWatch metrics every 5 minutes by default (basic monitoring); enable detailed monitoring for 1-minute granularity on standard EC2 metrics.

### Domain 5 - Incident and Event Response

- EventBridge is a serverless event bus: rules match event patterns from AWS services, custom apps, and SaaS, then route matching events to targets like Lambda, SNS, SQS, and SSM Automation.
- Codify remediation as SSM Automation documents (runbooks) and trigger them automatically from alarms or events to remove human delay from recovery.
- Separate notification from remediation: CloudWatch alarm to SNS notifies on-call, while EventBridge to Lambda or SSM Automation performs the automated fix.
- Match GuardDuty findings with an EventBridge rule (source aws.guardduty, detail-type GuardDuty Finding) that invokes a Lambda or SSM Automation runbook to remediate.
- Make remediation actions idempotent so re-running causes no extra harm, and add guardrails (approval steps, scope limits) for high-impact actions.
- Add an EventBridge target dead-letter queue and Lambda retry/DLQ so events that fail to deliver or process are captured for reprocessing instead of lost.

### Domain 6 - Security and Compliance

- Grant pipeline and compute permissions via IAM roles (CodeBuild service role, EC2 instance profile, OIDC for external CI), never long-lived access keys checked into config.
- Federate external CI (such as GitHub Actions) to an IAM role using OIDC for short-lived temporary credentials; create the provider with aws iam create-open-id-connect-provider --url https://token.actions.githubusercontent.com --client-id-list sts.amazonaws.com.
- Store secrets in Secrets Manager (with built-in rotation via a Lambda) or SSM Parameter Store SecureString; both encrypt at rest with KMS and are retrieved via IAM-authorized calls.
- Enable rotation with aws secretsmanager rotate-secret --rotation-lambda-arn <arn> --rotation-rules ...; use the multi-user (alternating) strategy for zero-downtime database rotation and have apps re-fetch on auth failure.
- Service Control Policies (SCPs) set the maximum permissions for an account; an action an SCP does not allow is denied even if an identity-based policy explicitly allows it.
- S3 account-level Block Public Access overrides bucket policies; a public-granting bucket policy is still blocked when account BPA is enabled.

## Study tips

- Read for the qualifier: questions ask for the MOST cost-effective, LEAST operational overhead, or FASTEST recovery. Multiple options are technically valid, so let the qualifier eliminate the rest.
- Default to managed and serverless over self-managed: EventBridge over cron on EC2, SSM Automation over custom scripts, and Secrets Manager rotation over hand-rolled rotation reduce operational overhead.
- Know the rollback and traffic-shifting story for each compute type: CodeDeploy blue/green and canary/linear for Lambda and ECS, CloudWatch-alarm-based automatic rollback, and the ECS termination wait time.
- Memorize the hard numbers: CodeBuild 8-hour build max, CloudFormation 500 resources per stack, KMS 7-30 day deletion window, EC2 basic monitoring 5 minutes vs detailed 1 minute, and high-resolution metric StorageResolution=1.
- When a question mentions cross-account or cross-Region, immediately think KMS key policies plus bucket/role trust policies, organization CloudTrail trails, and CloudWatch cross-account observability.

---

Want the full breakdown? See the complete **[AWS DOP-C02 study guide](https://certgrid.app/study-guide/aws-dop-c02-devops-engineer-professional)** and **[free practice questions](https://certgrid.app/practice/aws-dop-c02-devops-engineer-professional)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

