# Google Cloud Professional Cloud Security Engineer - Study Cheatsheet

The Google Cloud Professional Cloud Security Engineer exam validates your ability to design, implement, and manage secure infrastructure, identity, data protection, and security operations on Google Cloud. It is a 2-hour exam covering IAM and access control, network boundary protection, data encryption, security operations and monitoring, and compliance enforcement. It targets security professionals and cloud engineers responsible for protecting Google Cloud workloads and demonstrating regulatory compliance.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | Google Cloud Professional Cloud Security Engineer |
| Credential | Google Cloud Professional Cloud Security Engineer |
| Level | Advanced |
| Practice mock length | ~50 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-06-23 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Configuring Access | ~23% |
| 2 | Securing Communications and Boundary Protection | ~22% |
| 3 | Ensuring Data Protection | ~19% |
| 4 | Managing Operations | ~25% |
| 5 | Supporting Compliance Requirements | ~12% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Configuring Access

- Least privilege favors predefined roles (e.g., roles/storage.objectViewer) or custom roles over the primitive Owner/Editor/Viewer roles, which span nearly every Google Cloud service and grant far more access than any single task needs.
- Custom IAM roles let you define an exact permission set; create one with 'gcloud iam roles create' using --project (or --organization) and a --file YAML definition listing includedPermissions.
- Workload Identity (GKE) lets a Kubernetes service account impersonate a Google service account via the GKE metadata server, issuing short-lived tokens automatically and eliminating downloaded JSON key files.
- Enabling GKE Workload Identity requires two steps: annotating the Kubernetes service account with the Google SA email and adding the IAM policy binding for roles/iam.workloadIdentityUser.
- Workload Identity Federation lets external identities (AWS, Azure, on-prem OIDC/SAML providers) impersonate Google service accounts without keys, extending keyless auth beyond GKE.
- IAM Conditions add context constraints to a binding (time windows, resource names, request attributes); a time-bound grant uses a --condition with a request.time expression for a temporary window.

### Domain 2 - Securing Communications and Boundary Protection

- VPC Service Controls draws a service perimeter around projects so API calls to supported services (BigQuery, Cloud Storage, etc.) stay inside it; requests from outside are denied even with valid IAM credentials, mitigating data exfiltration.
- To extend a VPC Service Controls perimeter, create it with restricted-services and update it to add more projects; ingress/egress rules allow controlled cross-perimeter access.
- Cloud Armor is the managed WAF and DDoS mitigation service for the global external HTTP(S) Load Balancer, inspecting Layer 7 attributes and applying OWASP ModSecurity Core Rule Set rules against SQLi, XSS, and similar exploits.
- Attach a Cloud Armor policy with 'gcloud compute backend-services update BACKEND --security-policy=POLICY'; rate-limiting uses 'gcloud compute security-policies rules create' with --action=rate-based-ban and threshold flags.
- Private Google Access lets VMs with only internal IPs reach Google APIs and services over Google's network without a public route; enable it with 'gcloud compute networks subnets update SUBNET --enable-private-ip-google-access'.
- Private Service Connect gives granular, private endpoints to Google or third-party services, and pulling images from Artifact Registry over Private Google Access avoids public egress entirely.

### Domain 3 - Ensuring Data Protection

- All customer data is encrypted at rest by default with AES-256 using Google-managed keys, requiring no configuration; CMEK and CSEK/EKM are opt-in for greater key control.
- Cloud KMS lets you create, rotate, import, and destroy keys used as Customer-Managed Encryption Keys (CMEK) for Cloud Storage, BigQuery, Compute Engine, and more.
- Create KMS keys with 'gcloud kms keyrings create' then 'gcloud kms keys create --purpose=encryption'; key rings and keys are regional and cannot be deleted, only key versions destroyed.
- Set a bucket's CMEK with 'gcloud storage buckets create --default-encryption-key=FULL_KEY_RESOURCE_NAME', and first grant the Cloud Storage service agent roles/cloudkms.cryptoKeyEncrypterDecrypter on the key.
- Cloud HSM provides FIPS 140-2 Level 3 hardware-backed KMS keys; Cloud External Key Manager (EKM) keeps key material in a customer-controlled external key manager outside Google.
- Customer-Supplied Encryption Keys (CSEK) let you provide your own AES-256 key per request; Google holds it only transiently and never stores it, but you bear full key-management responsibility.

### Domain 4 - Managing Operations

- Cloud Audit Logs has four streams: Admin Activity (always on, free), Data Access (opt-in, records reads/writes), System Event, and Policy Denied; all flow to Cloud Logging.
- A principal granting itself a highly privileged role (a setIamPolicy event) is a classic privilege-escalation indicator; alert on it via Cloud Monitoring or a SIEM and investigate immediately.
- For forensic readiness, enable Data Access logs and route them through a log sink to a locked-down bucket or BigQuery dataset in a separate security project so an attacker cannot tamper with evidence.
- Use bucket retention policies and Bucket Lock on the log-sink destination to make exported audit logs immutable and tamper-resistant.
- Security Command Center aggregates findings from Security Health Analytics, Web Security Scanner, Event Threat Detection, and Container Threat Detection into one risk dashboard.
- SCC Premium/Enterprise adds Event Threat Detection (log-based detection of malware, credential access, lateral movement) and compliance posture reporting against benchmarks like CIS.

### Domain 5 - Supporting Compliance Requirements

- Organization Policy Service defines constraints inherited down the org/folder/project hierarchy to set guardrails on configuration; unlike IAM (who can act), it controls what configurations are allowed.
- The constraints/gcp.resourceLocations constraint with an allowedValues list of approved regions prevents creating resources outside those locations regardless of IAM permissions, enforcing data residency centrally.
- Set a resource-location policy via 'gcloud resource-manager org-policies set-policy' with a YAML policy listing allowed regions, applied at the org, folder, or project node.
- Enforce constraints/iam.disableServiceAccountKeyCreation to block downloadable SA keys org-wide, pushing teams toward Workload Identity and short-lived tokens.
- Custom Organization Policy constraints inspect resource fields at creation time (e.g., restrict allowed machineType on compute.googleapis.com/Instance) and deny non-conforming resources.
- Use a policy override at a project or folder node to exempt a specific constraint where a justified exception is needed, keeping the broader guardrail intact.

## Study tips

- Distinguish IAM (who can do what) from Organization Policy (what configurations are allowed) and VPC Service Controls (which API data flows are permitted) - exam scenarios often hinge on choosing the right layer.
- When a question mentions service account keys, the preferred answer is almost always keyless: Workload Identity, Workload Identity Federation, or short-lived impersonated tokens, plus iam.disableServiceAccountKeyCreation.
- Read carefully for the requirement being optimized - least privilege, data exfiltration prevention, data residency, immutability, or cost - and match it to the one mechanism designed for that goal.
- Memorize key gcloud command shapes: add-iam-policy-binding with --condition, kms keyrings/keys create, subnets update --enable-private-ip-google-access, and backend-services update --security-policy.
- For data residency or location compliance, the answer is the gcp.resourceLocations Organization Policy constraint, not firewall rules or IAM - centralized, hierarchy-inherited enforcement is the differentiator.

---

Want the full breakdown? See the complete **[Google Cloud Professional Cloud Security Engineer study guide](https://certgrid.app/study-guide/google-cloud-professional-cloud-security-engineer)** and **[free practice questions](https://certgrid.app/practice/google-cloud-professional-cloud-security-engineer)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

