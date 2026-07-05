# AZ-500: Azure Security Engineer Associate - Study Cheatsheet

The AZ-500: Azure Security Engineer Associate exam validates your ability to implement, manage, and monitor security across Azure identity, platform, operations, and data/applications. It is aimed at security engineers who manage identity and access, secure networks and compute, run security operations with Defender for Cloud and Microsoft Sentinel, and protect data, keys, and applications. Expect 40-60 scenario-based questions in 120 minutes, with a scaled passing score of 700.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | AZ-500 |
| Credential | AZ-500: Azure Security Engineer Associate |
| Level | Associate |
| Practice mock length | ~50 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-06-24 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Manage Identity and Access | ~26% |
| 2 | Implement Platform Protection | ~24% |
| 3 | Manage Security Operations | ~24% |
| 4 | Secure Data and Applications | ~26% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Manage Identity and Access

- Always exclude at least one break-glass (emergency access) cloud-only account with a long, complex password from every Conditional Access policy to avoid locking yourself out of the tenant.
- Microsoft Entra ID Protection has an MFA registration policy that prompts unregistered users to enroll and enforces a configurable grace period (commonly 14 days) before registration becomes mandatory at sign-in.
- Conditional Access supports authentication strength (a named requirement); use phishing-resistant strength (FIDO2, Windows Hello for Business, certificate-based) for high-risk or untrusted-location access and standard MFA for trusted locations.
- Privileged Identity Management (PIM) provides just-in-time, time-bound role activation with options to require approval, require justification, require MFA on activation, and it writes dedicated audit logs for every activation.
- System-assigned managed identities are tied to a single resource's lifecycle and are deleted automatically when the resource is deleted; user-assigned managed identities are standalone and can be shared across multiple resources.
- Use managed identities instead of stored credentials: grant an App Service's system-assigned identity Get permission on Key Vault secrets via an access policy or RBAC role like Key Vault Secrets User.

### Domain 2 - Implement Platform Protection

- Application Security Groups (ASGs) let you write NSG rules by application role (web/app/db tier) instead of IP addresses; ASGs are referenced as the source and/or destination in NSG rules.
- NSG rules are evaluated by priority (lowest number wins, 100-4096 for custom rules); the default AllowVNetInBound rule permits all intra-VNet traffic, so you must add higher-priority deny rules to restrict it.
- Azure DDoS Network Protection is the paid, always-on tier with adaptive tuning per protected public IP and access to the DDoS Rapid Response (DRR) team; DDoS IP Protection is per-IP and Basic is free/platform-level.
- Azure Firewall Premium adds TLS inspection, IDPS (intrusion detection and prevention), URL filtering, and web category filtering; Standard provides FQDN filtering and threat intelligence-based filtering only.
- Firewall Premium TLS inspection requires uploading an intermediate CA certificate to the firewall policy and distributing the corresponding root CA to the trusted root store of inspected clients.
- In hub-and-spoke, route spoke outbound traffic through Azure Firewall using User-Defined Routes (UDRs) with next hop = the firewall's private IP, and enable 'Allow forwarded traffic' on spoke peerings.

### Domain 3 - Manage Security Operations

- Microsoft Sentinel architecture: data connectors ingest logs, analytics rules (KQL) correlate and create incidents, and playbooks (Azure Logic Apps) automate response (SOAR).
- To reduce alert noise from a known benign account, modify the analytics rule's KQL query to exclude that account rather than disabling the rule entirely.
- Sentinel Fusion is a built-in, machine-learning analytics rule that correlates low-fidelity alerts across sources into high-confidence multistage attack incidents.
- Sentinel hunting uses saved KQL queries to proactively search Log Analytics data; Livestream monitors a query's results in real time during an active investigation.
- Import threat intelligence via the Threat Intelligence data connector (TAXII or the Threat Intelligence Platforms API), then enable the built-in TI Map analytics rules to match indicators against your logs.
- Collect Windows security events with the Azure Monitor Agent (AMA) and the Windows Security Events connector, choosing a collection tier (All, Common, Minimal, or custom) to control event volume.

### Domain 4 - Secure Data and Applications

- Always Encrypted encrypts sensitive columns on the client before data reaches Azure SQL, so DBAs and the server never see plaintext; store the column master key in Azure Key Vault, with the column encryption key in the database.
- Transparent Data Encryption (TDE) encrypts data at rest (data files, logs, backups) and is enabled by default on Azure SQL; switch to a customer-managed key (BYOK) in Key Vault for control over rotation and revocation.
- Rotating the TDE protector to a new Key Vault key version re-wraps the Database Encryption Key (DEK) and is an instantaneous, zero-downtime operation; only the DEK wrapping changes, not the data.
- Dynamic Data Masking obscures sensitive values (e.g., credit card numbers) for nonprivileged users at query time, while authorized users (added to the unmasked list) still see full data; it does not encrypt data at rest.
- Azure Key Vault Managed HSM provides single-tenant, FIPS 140-2 Level 3 validated hardware where keys never leave the HSM boundary; the Premium vault tier uses shared, multi-tenant HSMs.
- Key Vault access can be authorized either by the legacy access policy model or by Azure RBAC; RBAC (roles like Key Vault Secrets User, Crypto User) is the recommended, more granular model and you choose one model per vault.

## Study tips

- Read each scenario for the deciding constraint (no stored secrets, no public access, zero downtime, FIPS 140-2 Level 3, untrusted location) and pick the option that satisfies that exact requirement.
- On multiple-response 'select all that apply' items, evaluate each option independently against the requirements; partial-credit-style questions punish both missing a correct option and adding a wrong one.
- Default to the most identity-secure native option: managed identity over connection strings, RBAC over access policies, private endpoint over service endpoint when full isolation is required.
- Watch for distractors that are real services but solve the wrong layer (e.g., NSG vs. Azure Firewall vs. WAF, or Defender for Cloud vs. Sentinel) and match the tool to the threat and scope.
- Memorize where features live: PIM/Conditional Access/Access Reviews in Entra ID, JIT/Secure Score/Regulatory Compliance in Defender for Cloud, analytics rules/hunting/playbooks in Sentinel.

---

Want the full breakdown? See the complete **[AZ-500 study guide](https://certgrid.app/study-guide/az-500-azure-security-engineer-associate)** and **[free practice questions](https://certgrid.app/practice/az-500-azure-security-engineer-associate)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

