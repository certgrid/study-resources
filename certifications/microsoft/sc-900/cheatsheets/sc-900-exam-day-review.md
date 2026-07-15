# SC-900 Exam-Day Review

Use this page in the final 30-45 minutes before the exam. It is intentionally short and focused on high-frequency decisions.

## The Exam Mindset

SC-900 is a fundamentals exam. Most questions are not asking you to configure anything. They are asking whether you can recognize the right concept or the right product from the wording.

When stuck, ask:

1. Is this a concept question (Zero Trust, AuthN/AuthZ, encryption) or a product question?
2. If product: which family? Entra (identity), Defender (threats), Sentinel (SIEM), Purview (compliance/data).
3. What is the asset: identity, network, device, email, SaaS app, cloud workload, data, or logs?
4. What is the action: prevent, detect, respond, prove, keep, or find?

## Must-Know Pairs

| Pair                                         | Difference                                            |
| -------------------------------------------- | ----------------------------------------------------- |
| Authentication vs authorization              | Prove who you are vs what you may do                  |
| Encryption vs hashing                        | Reversible with key vs one-way, no key                |
| Zero Trust vs defense in depth               | Verify every request vs layered controls              |
| Federation vs synchronization                | Trust between IdPs vs copying accounts to the cloud   |
| Entra ID Protection vs Conditional Access    | Detect risk vs enforce policy                         |
| User risk vs sign-in risk                    | Account compromised vs this sign-in suspicious        |
| PIM vs access reviews                        | Just-in-time elevation vs periodic recertification    |
| NSG vs Azure Firewall                        | Basic subnet rules vs managed central firewall        |
| Azure Firewall vs WAF                        | Network traffic vs web app attacks (SQLi, XSS)        |
| Defender for Cloud vs Defender XDR           | Cloud infrastructure posture vs M365 attack detection |
| Defender XDR vs Sentinel                     | Microsoft signals XDR vs all-source SIEM/SOAR         |
| Defender for Identity vs Entra ID Protection | On-premises AD attacks vs cloud sign-in risk          |
| Sensitivity label vs retention label         | Protect (encrypt, mark) vs keep/delete on schedule    |
| DLP vs insider risk management               | Block content movement vs watch risky user behavior   |
| eDiscovery vs audit                          | Find content for legal cases vs search activity logs  |
| Service Trust Portal vs Compliance Manager   | Microsoft's evidence vs your posture                  |
| Compliance score vs Secure Score             | Compliance posture vs security posture                |

## Zero Trust in Ten Seconds

| List         | Items                                                             |
| ------------ | ----------------------------------------------------------------- |
| 3 principles | Verify explicitly, least privilege access, assume breach          |
| 6 pillars    | Identities, devices, applications, data, infrastructure, networks |

## Shared Responsibility in Ten Seconds

Customer ALWAYS keeps: data, devices, accounts and identities. Microsoft always has: physical datacenter, hosts, network. The middle shifts with IaaS/PaaS/SaaS.

## MFA Factor Check

| Combination                   | MFA?                           |
| ----------------------------- | ------------------------------ |
| Password + Authenticator push | Yes (know + have)              |
| Password + SMS code           | Yes (know + have)              |
| Password + security questions | No (know + know)               |
| FIDO2 key + fingerprint       | Yes (have + are), passwordless |

## Final Service Picker

| Keyword                                   | Answer                            |
| ----------------------------------------- | --------------------------------- |
| Conditional "if/then" access policy       | Conditional Access                |
| Leaked credentials detected               | Entra ID Protection               |
| Temporary admin role with approval        | PIM                               |
| Recertify access quarterly                | Access reviews                    |
| No secrets in code for an Azure app       | Managed identity                  |
| AI agent needs an identity                | Agent ID                          |
| Traffic flood defense                     | Azure DDoS Protection             |
| SQL injection defense                     | WAF                               |
| Port-level subnet rules                   | NSG                               |
| RDP without public IP                     | Azure Bastion                     |
| Secrets, keys, certificates               | Azure Key Vault                   |
| Cloud posture recommendations, multicloud | Microsoft Defender for Cloud      |
| SIEM/SOAR, third-party logs, playbooks    | Microsoft Sentinel                |
| Unified M365 incidents                    | Microsoft Defender XDR            |
| Phishing and malicious attachments        | Defender for Office 365           |
| Endpoint detection and response           | Defender for Endpoint             |
| Shadow IT discovery (CASB)                | Defender for Cloud Apps           |
| On-premises AD attack detection           | Defender for Identity             |
| Device CVE prioritization                 | Defender Vulnerability Management |
| Threat actor research                     | Defender Threat Intelligence      |
| Microsoft's audit reports                 | Service Trust Portal              |
| GDPR assessment template                  | Compliance Manager                |
| Find sensitive data patterns              | Sensitive information types       |
| What classified data exists where         | Content explorer                  |
| What happened to classified data          | Activity explorer                 |
| Encrypt + watermark documents             | Sensitivity labels                |
| Block data exfiltration via email         | DLP                               |
| Keep 7 years then delete                  | Retention                         |
| Admin-proof immutable item                | Regulatory record                 |
| Departing employee data theft             | Insider risk management           |
| Legal hold + custodians + analytics       | eDiscovery (Premium)              |
| Search activity logs, 10-year retention   | Audit (Premium)                   |

## Last-Minute Traps

| Trap wording                                         | Better answer                                                    |
| ---------------------------------------------------- | ---------------------------------------------------------------- |
| "ID Protection blocks the sign-in"                   | It detects and scores risk; Conditional Access enforces          |
| "Defender XDR ingests firewall logs from any vendor" | That is Sentinel (SIEM)                                          |
| "NSG stops cross-site scripting"                     | WAF handles web attacks                                          |
| "Retention label encrypts the file"                  | Sensitivity label encrypts; retention keeps/deletes              |
| "Compliance Manager proves Microsoft is compliant"   | Service Trust Portal holds Microsoft's evidence                  |
| "Password + security questions is MFA"               | Two of the same factor category is not MFA                       |
| "Password hash sync sends passwords to the cloud"    | It syncs a hash of the hash, never plaintext                     |
| "Defender for Identity secures Entra ID"             | It monitors on-premises AD; Entra ID Protection covers the cloud |
| "Hashing is a kind of encryption"                    | Hashing is one-way and keyless                                   |
| "Customer has no security duties in SaaS"            | Data, devices, and identities always remain the customer's       |

## Final Confidence Checklist

You are ready when you can explain these without looking:

- The three Zero Trust principles and six pillars
- What the customer always keeps in shared responsibility
- AuthN vs AuthZ and identity as the primary security perimeter
- The identity types in Entra ID, including agent ID and managed identities
- Conditional Access signals, decisions, and enforcement
- PIM vs access reviews vs entitlement management
- The big three: Defender for Cloud vs Defender XDR vs Sentinel
- Which Defender protects email, endpoints, SaaS apps, and on-premises AD
- Sensitivity labels vs retention labels vs DLP vs records
- Content explorer vs Activity explorer
- Content search vs eDiscovery Standard vs Premium; Audit Standard vs Premium
- Service Trust Portal vs Compliance Manager vs compliance score
