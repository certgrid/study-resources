# (ISC)² CCSP - Study Cheatsheet

The (ISC)² Certified Cloud Security Professional (CCSP) validates advanced, vendor-neutral expertise in designing, securing, and operating cloud environments across six domains. It is aimed at experienced security architects, engineers, and managers (the credential requires five years of IT experience, three of them in information security and one in a CCSP domain). Since October 1, 2025 the exam uses Computerized Adaptive Testing (CAT) with 100 to 150 questions in a maximum of 180 minutes (3 hours), scored 0-1000 with 700 to pass.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | (ISC)² CCSP |
| Credential | (ISC)² CCSP |
| Level | Intermediate |
| Practice mock length | ~100 questions |
| Duration | ~180 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Cloud Concepts, Architecture and Design | ~15% |
| 2 | Cloud Data Security | ~19% |
| 3 | Cloud Platform and Infrastructure Security | ~18% |
| 4 | Cloud Application Security | ~14% |
| 5 | Cloud Security Operations | ~25% |
| 6 | Legal, Risk and Compliance | ~10% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Cloud Concepts, Architecture and Design

- The three standard service models are IaaS (provider manages physical infrastructure, host, hypervisor, storage, and networking; customer owns guest OS upward), PaaS (provider also manages OS and runtime), and SaaS (provider manages the entire stack except data and access).
- NIST SP 800-145 defines five essential characteristics of cloud: on-demand self-service, broad network access, resource pooling, rapid elasticity, and measured service.
- Rapid elasticity lets resources be provisioned and released automatically to scale out and in with demand, often appearing unlimited to the consumer; measured service means usage is metered, monitored, and billed per consumption.
- In the shared responsibility model the customer is ALWAYS responsible for their data, its classification, and identity/access configuration (IAM), regardless of service model; the provider secures the infrastructure it controls.
- Multi-tenancy means multiple customers share the same physical infrastructure, so the key risk is a failure of logical isolation; providers enforce separation via hypervisor, container, and network controls.
- The four deployment models are public, private, community (shared by organizations with common concerns such as mission, compliance, or policy), and hybrid (combination connected by standardized or proprietary technology).

### Domain 2 - Cloud Data Security

- The cloud data lifecycle has six phases in order: Create, Store, Use, Share, Archive, Destroy; protection decisions (classification, labeling, encryption) should be designed starting at Create.
- Crypto-shredding (crypto-erasure) renders encrypted data permanently unrecoverable by securely destroying the encryption keys, and is the practical sanitization method in shared cloud storage where physical destruction is not possible.
- Tokenization replaces sensitive values with non-sensitive tokens while preserving usability; the token vault that maps tokens to real data must be isolated from the application data stores.
- Data masking (static or dynamic) obscures or substitutes sensitive identifiers so that non-production or unauthorized users see protected values while format and usability are preserved.
- Symmetric encryption uses one shared key (fast, needs secure key exchange); asymmetric uses a public/private key pair (slower, enables secure key exchange and digital signatures).
- Encryption in transit uses TLS/SSL; encryption at rest protects stored data; key control determines who can decrypt, making key management the central control in cloud data security.

### Domain 3 - Cloud Platform and Infrastructure Security

- Network microsegmentation isolates workloads with fine-grained policy to limit lateral movement, so a compromise in one segment cannot freely spread across the environment.
- A bastion host or jump server provides a single hardened, monitored entry point for administrative access to private resources, reducing direct exposure of management interfaces to the internet.
- Resilience and availability come from eliminating single points of failure: deploy across multiple availability zones/regions and maintain regularly tested backups paired with a documented disaster recovery plan.
- RTO (recovery time objective) is the maximum acceptable time to restore a service after an outage; RPO (recovery point objective) is the maximum acceptable data loss measured in time.
- VM escape is the threat where an attacker breaks out of a guest VM to the hypervisor or host, potentially enabling cross-tenant compromise; hypervisor hardening and patching are critical mitigations.
- The principle of least privilege grants only the minimum permissions needed; enforce it with RBAC, regular access reviews, and restricting administrative access to authorized, audited paths.

### Domain 4 - Cloud Application Security

- Shift-left security integrates automated security testing (SAST, DAST, SCA, secrets scanning) into CI/CD to catch vulnerabilities early and consistently before code reaches production.
- The SDLC phases (e.g., requirements, design, development, testing, deployment, operations/maintenance) each have security activities; threat modeling belongs in design and is commonly done with STRIDE.
- Prevent injection (SQLi) and XSS with input validation, output encoding, and parameterized queries/prepared statements rather than string concatenation.
- A web application firewall (WAF) inspects HTTP/S traffic to block common web exploits such as SQL injection and cross-site scripting at the application layer (e.g., associate a WAFv2 web ACL with an ALB).
- Store secrets in a managed secrets manager or vault with access controlled by IAM and full audit logging; never hardcode credentials in source, images, or environment defaults.
- An API gateway centralizes authentication, authorization, throttling/rate limiting, and request validation in front of services, providing consistent enforcement.

### Domain 5 - Cloud Security Operations

- Centralize logging and events into a SIEM for correlation and detection, and use SOAR with documented runbooks to automate and standardize incident containment and response.
- Logs must be tamper-resistant, time-synchronized (NTP), and retained per policy; enable integrity validation (e.g., aws cloudtrail create-trail with --enable-log-file-validation and --is-multi-region-trail).
- Forward logs to a dedicated, access-restricted account with write-once/immutable (WORM) storage so an attacker who compromises a workload cannot alter or delete the evidence.
- Cloud Security Posture Management (CSPM) continuously detects misconfigurations and compliance drift across resources and can apply automated remediation guardrails.
- The CSA Cloud Controls Matrix (CCM) is a cloud-specific control framework mapped to multiple standards and regulations, useful for assessment, gap analysis, and compliance.
- Threat detection services (e.g., GuardDuty) analyze logs and telemetry for malicious activity; enable continuous configuration recording (AWS Config) to track resource state and rule compliance.

### Domain 6 - Legal, Risk and Compliance

- Data sovereignty and jurisdictional law may require that data be stored and processed within specific geographies, directly affecting cloud region selection; enforce with policy (e.g., deny actions where aws:RequestedRegion is not in an allowed list).
- GDPR governs EU personal data and defines the data controller (determines purpose/means) and data processor (acts on the controller's instructions); cross-border transfers require an approved legal mechanism.
- Independent assurance and attestations (e.g., SOC 2 Type II, ISO/IEC 27001, ISO/IEC 27017 and 27018) let a customer evaluate a provider's controls and inherit only the controls that apply to them.
- Accountability cannot be outsourced: transferring a function to a provider does not remove the data owner's reputational, regulatory, and breach-notification obligations.
- SLAs define measurable commitments (availability, performance, support response) and remedies; review them to match service tier and price to required performance and availability.
- Contracts should include right-to-audit clauses, defined security requirements, incident-response and evidence-access provisions, and escalation/notification SLAs agreed up front.

## Study tips

- Always start from the shared responsibility model: identify the service model (IaaS/PaaS/SaaS) first, then decide who owns the control in question. Data and access management are always the customer's.
- CCSP is vendor-neutral and concept-driven. When an answer cites a specific AWS/Azure/GCP command, choose it for the principle it demonstrates (e.g., enforce encryption, deny public access) rather than memorizing syntax.
- Watch for the 'most early/most effective/best' qualifier in questions. Eliminate answers that destroy evidence (disabling logs), violate least privilege, or break separation of duties.
- Know the lifecycles and ordered lists cold: cloud data lifecycle (Create, Store, Use, Share, Archive, Destroy), risk treatment options, and the order of volatility for forensics.
- It is a long exam of up to three hours scored to 700/1000, now delivered as a Computerized Adaptive Test (CAT) presenting 100 to 150 questions. Pace yourself, and pick the answer that best reflects (ISC)² best practice rather than a real-world shortcut.

---

Want the full breakdown? See the complete **[(ISC)² CCSP study guide](https://certgrid.app/study-guide/isc-ccsp)** and **[free practice questions](https://certgrid.app/practice/isc-ccsp)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

