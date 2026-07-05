# AWS SCS-C02: Security Specialty - Study Cheatsheet

The AWS Certified Security - Specialty (SCS-C02) validates deep expertise in securing AWS workloads across threat detection, logging, infrastructure, identity, data protection, and governance. It targets security engineers and architects with hands-on AWS experience who design and operate secure cloud environments. The exam is 170 minutes, scenario-heavy, and demands you choose the most secure, operationally efficient, and cost-effective option among several plausible answers.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | AWS SCS-C02 |
| Credential | AWS SCS-C02: Security Specialty |
| Level | Specialty |
| Practice mock length | ~65 questions |
| Duration | ~170 minutes |
| Passing score | 750 out of 1000 |
| Notes reviewed | 2026-06-23 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Threat Detection and Incident Response | ~16% |
| 2 | Security Logging and Monitoring | ~18% |
| 3 | Infrastructure Security | ~20% |
| 4 | Identity and Access Management | ~18% |
| 5 | Data Protection | ~19% |
| 6 | Management and Security Governance | ~10% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Threat Detection and Incident Response

- Amazon GuardDuty is an agentless service that uses machine learning and AWS threat intelligence to analyze CloudTrail management events, VPC Flow Logs, and Route 53 DNS query logs for malicious activity such as credential exfiltration and crypto-mining.
- GuardDuty protection plans (S3 Protection, EKS Protection, RDS Protection, Lambda Protection, and Malware Protection for EC2) are enabled independently; EC2 Malware Protection is NOT turned on automatically with the others and must be explicitly enabled.
- GuardDuty Malware Protection performs agentless scans of EBS volume snapshots (it creates a snapshot copy) to detect malware without installing an agent on the instance.
- Designate a delegated administrator in AWS Organizations and enable GuardDuty auto-enable so new member accounts are protected automatically; aws guardduty create-detector --enable turns it on and returns a detector ID.
- While a GuardDuty detector is suspended it stops monitoring data sources and generates no new findings, but existing findings and configuration settings are retained.
- Upload your own list of known-malicious IPs with aws guardduty create-threat-intel-set so GuardDuty raises findings on matching traffic; trusted IP lists suppress findings instead.

### Domain 2 - Security Logging and Monitoring

- AWS CloudTrail records account-wide API calls (caller identity, source IP, timestamp, parameters, response); management events are logged by default while S3/Lambda/DynamoDB data events must be explicitly enabled and incur extra cost.
- Create an organization trail (multi-region) delivering to an S3 bucket in a dedicated log-archive account with S3 Object Lock; this enforces separation of duties and tamper resistance because source-account admins cannot modify the logs.
- Enable CloudTrail log file integrity validation to produce hourly digest files using SHA-256 hashing and digital signatures, letting you detect any post-delivery modification or deletion of log files.
- aws cloudtrail create-trail with --is-multi-region-trail creates a trail covering all regions; global service events (IAM, STS, CloudFront) are recorded via the global-events setting and only need one trail to capture them.
- Enable S3 object-level (data event) logging with aws cloudtrail put-event-selectors using a DataResources AWS::S3::Object entry.
- VPC Flow Logs capture IP traffic metadata (source/destination IP and port, protocol, packet/byte counts, ACCEPT or REJECT) for ENIs, subnets, or VPCs; they do NOT capture packet payloads.

### Domain 3 - Infrastructure Security

- Security groups are stateful and operate at the instance/ENI level (return traffic is automatically allowed); network ACLs are stateless at the subnet level and require explicit inbound AND outbound rules, evaluated by rule number in order.
- Reference a security group as the source in another security group's rule for tiered designs - e.g. set the web tier's SG ID as the inbound source on the app tier SG so only web instances can reach the app tier.
- Add an inbound HTTPS rule with aws ec2 authorize-security-group-ingress --protocol tcp --port 443 --cidr <range>; security groups support only allow rules, while NACLs support both allow and deny.
- AWS WAF inspects HTTP/S requests and protects CloudFront, Application Load Balancers, API Gateway, and AppSync against SQL injection, XSS, and OWASP Top 10 threats; attach a web ACL with aws wafv2 associate-web-acl using the resource ARN.
- AWS Shield Standard is free and automatic for layer 3/4 DDoS protection; Shield Advanced is a paid tier adding enhanced detection, 24/7 Shield Response Team (SRT) access, and DDoS cost protection for scaling charges.
- Gateway VPC endpoints (S3 and DynamoDB only) add a route-table entry at no cost; Interface endpoints (AWS PrivateLink) provision ENIs with private IPs for most other services and incur hourly and data charges.

### Domain 4 - Identity and Access Management

- IAM policy evaluation: an explicit Deny in ANY policy (identity-based, resource-based, SCP, permissions boundary, or session policy) always overrides any Allow; otherwise the request is denied by default unless explicitly allowed.
- Service Control Policies (SCPs) are guardrails that set the maximum permissions for member accounts but grant nothing on their own - an action is allowed only if BOTH the SCP and the identity-based policy permit it (the intersection).
- SCPs do not affect the Organizations management account; to constrain workloads with SCPs, run those workloads in member accounts placed in OUs.
- Permissions boundaries cap the maximum permissions an IAM user or role can have; set one with aws iam put-user-permissions-boundary, and use them to let admins delegate role creation safely without privilege escalation.
- AWS IAM Identity Center (successor to AWS SSO) provides centralized workforce SSO across accounts and apps, integrates with external IdPs via SAML 2.0/SCIM, and supports permission sets plus attribute-based access control (ABAC) using session tags.
- OIDC/SAML federation issues short-lived STS credentials via AssumeRoleWithWebIdentity or AssumeRoleWithSAML, eliminating long-lived access keys; GitHub Actions and similar CI use OIDC to assume roles.

### Domain 5 - Data Protection

- AWS KMS creates and manages encryption keys and integrates natively with S3 (SSE-KMS), EBS, RDS, Secrets Manager, and more; it enforces key policies and logs every Decrypt/Encrypt call to CloudTrail for auditing.
- A KMS key policy is the primary access control for a key; it must include a statement enabling IAM policies (granting the account root principal kms:*) before IAM identity policies can delegate access to the key.
- Enable automatic annual rotation of AWS managed/customer managed symmetric keys with aws kms enable-key-rotation --key-id <id>; KMS retains old key material so all previously encrypted data stays transparently decryptable.
- Use a KMS multi-Region key with replicas in each region (same key ID) so encryption/decryption happens in-region for low latency and cross-region portability of ciphertext.
- Grant temporary, scoped key permissions to a principal with aws kms create-grant specifying the grantee principal and allowed operations (e.g. Decrypt, Encrypt), useful for AWS services acting on your behalf.
- SSE-S3 uses AES-256 keys managed entirely by S3 with no customer control or audit trail; SSE-KMS uses KMS keys giving per-key policies, auditable Decrypt calls, and optional customer-managed keys.

### Domain 6 - Management and Security Governance

- Service Control Policies (SCPs) enforce preventive guardrails across an Organization; attach one with aws organizations attach-policy --policy-id <id> --target-id <ou-or-account>.
- Protect logging integrity org-wide with an SCP that denies cloudtrail:StopLogging, cloudtrail:DeleteTrail, and organizations:LeaveOrganization for member-account principals.
- Restrict resource creation with an SCP, for example denying ec2:RunInstances unless the requested instance type matches an approved allow-list condition.
- AWS Config records resource configuration changes; start recording with aws configservice start-configuration-recorder, and reduce cost/noise by recording only specific in-scope resource types instead of all supported types.
- AWS Config managed rules (e.g. s3-bucket-public-read-prohibited) detect non-compliant resources; attach SSM Automation remediation with aws configservice put-remediation-configurations to auto-fix violations.
- If Config auto-remediation does not run, common causes are the automation assume role lacking permissions or the remediation being configured as manual rather than automatic.

## Study tips

- Read every scenario for the qualifier - 'most secure', 'most cost-effective', 'least operational overhead', or 'least privilege' - because several answers will be technically valid and only one fits the stated priority.
- Default to managed and automated solutions (GuardDuty, Security Hub, Config remediation, Session Manager, Secrets Manager rotation) over custom scripts or self-managed instances when the question stresses low operational overhead.
- Memorize IAM evaluation logic cold: explicit Deny always wins, SCPs only cap permissions and never grant, and the effective permission is the intersection of SCP, identity policy, permissions boundary, and resource policy.
- Know the multi-account governance stack and when to use each: SCPs for prevention, Config rules for detection/remediation, Control Tower for the landing zone baseline, StackSets for deployment, Security Hub for aggregation, and Firewall Manager for network protections.
- Watch for forensic sequencing in incident-response questions: always preserve evidence (memory dump, EBS snapshot) and isolate before terminating, and route GuardDuty findings through EventBridge to Lambda or SSM Automation for containment.

---

Want the full breakdown? See the complete **[AWS SCS-C02 study guide](https://certgrid.app/study-guide/aws-scs-c02-security-specialty)** and **[free practice questions](https://certgrid.app/practice/aws-scs-c02-security-specialty)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

