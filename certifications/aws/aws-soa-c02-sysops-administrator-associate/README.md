# AWS SOA-C02: SysOps Administrator Associate - Study Cheatsheet

The AWS Certified SysOps Administrator - Associate (SOA-C02) validates your ability to deploy, manage, and operate workloads on AWS, with emphasis on monitoring, reliability, automation, security, networking, and cost/performance optimization. It is aimed at operations-focused professionals with at least one year of hands-on experience operating AWS workloads. The 180-minute exam includes multiple-choice/multiple-response questions and a scaled passing score of 720 (out of 1000).

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | AWS SOA-C02 |
| Credential | AWS SOA-C02: SysOps Administrator Associate |
| Level | Associate |
| Practice mock length | ~65 questions |
| Duration | ~180 minutes |
| Passing score | 720 out of 1000 |
| Notes reviewed | 2026-07-12 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Monitoring, Logging, and Remediation | ~14% |
| 2 | Reliability and Business Continuity | ~13% |
| 3 | Deployment, Provisioning, and Automation | ~15% |
| 4 | Security and Compliance | ~19% |
| 5 | Networking and Content Delivery | ~17% |
| 6 | Cost and Performance Optimization | ~23% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Monitoring, Logging, and Remediation

- The CloudWatch unified agent must be installed on EC2 to collect OS-level metrics like memory utilization and disk space; these are NOT available from the default hypervisor-level metrics.
- CloudWatch standard metric resolution is 60 seconds; publish with StorageResolution=1 (via PutMetricData) to enable 1-second high-resolution custom metrics.
- New CloudWatch Logs log groups default to 'Never expire'; use aws logs put-retention-policy --retention-in-days 30 to set retention explicitly.
- A CloudWatch Logs metric filter scans log streams for a pattern (e.g. 'ERROR') and converts matches into a custom metric that can drive an alarm.
- CloudWatch Logs Insights queries large log volumes interactively; the two CLI calls are aws logs start-query (returns a queryId) and aws logs get-query-results.
- aws cloudwatch put-metric-alarm needs --namespace, --metric-name, --period (e.g. 300), and --evaluation-periods (e.g. 2); aws cloudwatch put-metric-data --namespace --metric-name --value publishes a single custom data point.

### Domain 2 - Reliability and Business Continuity

- RTO (Recovery Time Objective) is the maximum acceptable time to restore service; RPO (Recovery Point Objective) is the maximum acceptable data loss measured in time.
- An EC2 Auto Scaling Group monitors instance health via EC2 status checks or ELB health checks, terminates unhealthy instances, and maintains desired capacity across AZs.
- Spanning an ASG across at least two AZs with an ALB targeting subnets in each AZ provides high availability against an AZ failure.
- Increase the ASG health check grace period so it covers full application startup time; otherwise instances are killed before they finish booting.
- ASG rebalancing first terminates instances in the AZ with the most instances, then applies the default termination policy (e.g. oldest launch template/configuration).
- RDS Multi-AZ provisions a synchronous standby in another AZ with automatic failover and no data loss; it is for availability, not read scaling, and is enabled with aws rds create-db-instance --multi-az.

### Domain 3 - Deployment, Provisioning, and Automation

- AWS CloudFormation is the native IaC service: JSON/YAML templates managed as stacks with dependency ordering, automatic rollback on failure, and drift detection.
- aws cloudformation deploy creates or updates a stack idempotently in one command; use create-change-set + describe-change-set to preview exactly which resources will be modified, replaced, or deleted before applying.
- Recover a stack stuck in UPDATE_ROLLBACK_FAILED with ContinueUpdateRollback, optionally skipping problematic resources via --resources-to-skip.
- DeletionPolicy: Retain preserves (orphans) a resource in your account after the stack is deleted - useful for databases and S3 buckets you must not lose.
- CloudFormation StackSets deploy resources consistently across multiple accounts and Regions; with AWS Organizations auto-deployment, new accounts automatically receive the baseline stack.
- An ASG uses a launch template (the modern, versioned successor to the deprecated, immutable launch configuration) specifying AMI, instance type, security groups, IAM instance profile, and user data; create-launch-template-version registers a new version.

### Domain 4 - Security and Compliance

- Attach an IAM role via an instance profile to grant EC2 AWS permissions through temporary, auto-rotated IMDS credentials - never embed long-term access keys in code or config.
- Security Groups are stateful and operate at the instance/ENI level (return traffic auto-allowed); Network ACLs are stateless at the subnet level and require explicit rules for BOTH directions.
- In IAM policy evaluation an explicit Deny always overrides any Allow, regardless of which policy granted the Allow.
- AWS Config continuously records resource configurations and evaluates them against managed/custom rules for compliance and drift, and can trigger SSM Automation remediation.
- Amazon GuardDuty uses ML, anomaly detection, and threat intelligence over CloudTrail events, VPC Flow Logs, and DNS query logs to detect compromised credentials and malicious activity.
- AWS CloudTrail records every API call (caller identity, timestamp, source IP, parameters); aws cloudtrail create-trail --is-organization-trail plus aws cloudtrail start-logging enable and activate an org-wide trail.

### Domain 5 - Networking and Content Delivery

- A subnet is public if its route table has a 0.0.0.0/0 (or ::/0) route to an Internet Gateway; a private subnet has no such IGW route.
- Private-subnet instances reach the internet via a NAT gateway placed in a public subnet PLUS a 0.0.0.0/0 route in the private subnet's route table pointing to that NAT gateway.
- Provisioning a NAT gateway requires two steps: aws ec2 allocate-address for an Elastic IP, then aws ec2 create-nat-gateway referencing that EIP and a public subnet.
- Create core VPC plumbing with aws ec2 create-vpc --cidr-block 10.0.0.0/16 and aws ec2 create-route --route-table-id --destination-cidr-block 0.0.0.0/0 --gateway-id.
- Gateway VPC endpoints (S3 and DynamoDB only) route traffic privately at no extra cost; Interface endpoints (PrivateLink) use ENIs and are created with aws ec2 create-vpc-endpoint --vpc-endpoint-type Interface.
- If a PrivateLink interface endpoint's hostname resolves to public IPs, Private DNS is not enabled on the endpoint - enable it so the service's default hostname resolves to private addresses.

### Domain 6 - Cost and Performance Optimization

- Right-size over-provisioned instances (consistently low CPU/memory) to a smaller, cheaper instance type to cut hourly cost while keeping adequate performance.
- AWS Compute Optimizer analyzes CloudWatch CPU, memory, network, and disk metrics with ML to recommend right-sizing; fetch results with aws compute-optimizer get-ec2-instance-recommendations.
- Savings Plans and Reserved Instances give up to 72% off On-Demand for steady 1-3 year usage; Compute Savings Plans are the most flexible, applying across instance family, size, and Region.
- A zonal Reserved Instance reserves capacity in one specific AZ and only discounts usage in that AZ, unlike a regional RI which is more flexible but provides no capacity reservation.
- Spot Instances offer the deepest discount for fault-tolerant, interruptible batch workloads; request one with aws ec2 run-instances --instance-market-options MarketType=spot.
- AWS Cost Explorer visualizes and forecasts spend across services, accounts, and tags; AWS Budgets sets cost/usage thresholds and alerts via SNS - create one with aws budgets create-budget --account-id with a JSON definition.

## Study tips

- Expect three exam-lab style scenarios in the older format, but SOA-C02 is now multiple-choice/multiple-response only - still practice the CLI commands (put-metric-alarm, send-command, create-change-set, assume-role) because exact flags appear in answer options.
- When a question asks for OS-level metrics (memory, disk) on EC2, the answer almost always involves installing the CloudWatch unified agent - default EC2 metrics never include these.
- Distinguish RTO vs RPO and map DR strategies (backup/restore, pilot light, warm standby, multi-site) to cost-versus-recovery-time tradeoffs; the cheapest option that meets the stated RTO/RPO is usually correct.
- For security questions, default to IAM roles over access keys, explicit Deny wins, S3 Block Public Access for exposure, and SSE-KMS with a customer managed key when key control or audit is required.
- Read carefully for 'most cost-effective' versus 'highest performance' - the same scenario has different correct answers (e.g. Spot/lifecycle for cost, Provisioned IOPS/Savings Plans for predictable performance).

---

Want the full breakdown? See the complete **[AWS SOA-C02 study guide](https://certgrid.app/study-guide/aws-soa-c02-sysops-administrator-associate)** and **[free practice questions](https://certgrid.app/practice/aws-soa-c02-sysops-administrator-associate)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

