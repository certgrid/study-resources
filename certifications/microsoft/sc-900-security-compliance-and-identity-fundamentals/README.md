# SC-900: Security, Compliance, and Identity Fundamentals - Study Cheatsheet

SC-900: Security, Compliance, and Identity Fundamentals validates foundational knowledge of security, compliance, and identity (SCI) concepts and how related Microsoft services - Microsoft Entra, Microsoft Defender, Microsoft Sentinel, and Microsoft Purview - address them. It is aimed at people new to the field, including business stakeholders, students, and IT professionals who want a baseline understanding before pursuing role-based certifications. No deep technical experience is required, but familiarity with Azure and Microsoft 365 is helpful.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | SC-900 |
| Credential | SC-900: Security, Compliance, and Identity Fundamentals |
| Level | Beginner |
| Practice mock length | ~40 questions |
| Duration | ~45 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Describe Concepts of Security, Compliance, and Identity | ~26% |
| 2 | Describe Capabilities of Microsoft Entra | ~25% |
| 3 | Describe Capabilities of Microsoft Security Solutions | ~24% |
| 4 | Describe Capabilities of Microsoft Compliance Solutions | ~25% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Describe Concepts of Security, Compliance, and Identity

- The CIA triad stands for Confidentiality (data is accessible only to authorized parties), Integrity (data is not altered without authorization), and Availability (data and systems are accessible to authorized users when needed).
- The shared responsibility model divides duties between cloud provider and customer: in IaaS the customer manages OS, apps, and data; in PaaS the provider manages the OS while the customer manages apps and data; in SaaS the provider manages almost everything except data classification and identities.
- Data, devices, accounts, and identities are ALWAYS the customer's responsibility across IaaS, PaaS, and SaaS - the cloud provider is never responsible for classifying or protecting your data.
- Zero Trust operates on three principles: verify explicitly, use least-privilege access, and assume breach. Network location grants no implicit trust - being inside the corporate firewall provides no automatic privileges.
- Defense in depth uses multiple independent layers of protection (physical, identity/access, perimeter, network, compute, application, data) so that if one layer is breached, others still protect the asset.
- Encryption at rest protects stored data; encryption in transit protects data moving across networks. Encryption makes data unreadable without the correct decryption key.

### Domain 2 - Describe Capabilities of Microsoft Entra

- Microsoft Entra ID (formerly Azure Active Directory) is a cloud-based identity and access management service providing authentication, single sign-on (SSO), MFA, and identity governance.
- Identity types in Entra ID include users, service principals (an identity for an application or service), managed identities (automatically managed credentials for Azure resources), and devices.
- Single sign-on (SSO) lets users authenticate once and access multiple applications without re-entering credentials, improving experience while reducing password fatigue.
- Multi-factor authentication (MFA) requires two or more verification methods from different categories: something you know (password/PIN), something you have (authenticator app, FIDO2 key), or something you are (biometric).
- Self-Service Password Reset (SSPR) lets users reset their own passwords using registered verification methods, reducing helpdesk load. Admins can require a number of registered methods before reset is allowed.
- Passwordless authentication methods include Windows Hello for Business, FIDO2 security keys, and the Microsoft Authenticator app - all more phishing-resistant than passwords.

### Domain 3 - Describe Capabilities of Microsoft Security Solutions

- A Network Security Group (NSG) filters inbound and outbound traffic to Azure virtual network resources using allow/deny rules based on source/destination IP, port, and protocol; rules are processed by priority and can apply at subnet or NIC level.
- Azure Firewall is a managed, cloud-based, stateful network security service offering centralized filtering with network and application rules, built-in high availability, and threat intelligence-based filtering.
- Azure DDoS Protection detects and mitigates distributed denial-of-service attacks against Azure Virtual Network resources, with an enhanced (Network/IP) tier offering tuned, application-specific mitigation.
- Microsoft Defender for Cloud provides cloud security posture management (CSPM) and cloud workload protection (CWP) across Azure, on-premises, AWS, and GCP environments.
- Microsoft Secure Score (in Defender for Cloud and the Defender portal) expresses an organization's security posture as a percentage; a higher score reflects more recommended controls implemented and lower risk.
- Microsoft Sentinel is a cloud-native SIEM (Security Information and Event Management) and SOAR (Security Orchestration, Automation, and Response) solution that collects data enterprise-wide, detects threats with built-in analytics, and automates response with playbooks.

### Domain 4 - Describe Capabilities of Microsoft Compliance Solutions

- The Microsoft Purview compliance portal is the central hub for data protection, compliance assessment, and governance solutions across Microsoft 365 and connected data.
- Microsoft Purview Compliance Manager calculates a compliance score reflecting progress on recommended improvement actions, mapped to regulatory standards and assessments, to help reduce compliance risk.
- Improvement actions in Compliance Manager are split into those the customer controls and those Microsoft manages; the score increases as recommended controls are implemented.
- Sensitivity labels in Microsoft Purview Information Protection classify content and enforce protection that travels with the item, including encryption, content markings (headers, footers, watermarks), and access restrictions.
- Auto-labeling can automatically apply sensitivity labels to content based on detected sensitive information, either client-side (in Office apps) or service-side (for data at rest).
- Microsoft Purview Data Loss Prevention (DLP) detects sensitive information such as credit card numbers and government IDs and can block, restrict, or warn on its sharing across email, Teams, endpoints, and SharePoint.

## Study tips

- SC-900 is conceptual, not hands-on - focus on what each service does and which problem it solves, not on configuration steps or portal navigation.
- Master the shared responsibility model and be able to instantly state who owns OS patching, applications, and data in IaaS vs PaaS vs SaaS; remember data and identities are always the customer's responsibility.
- Memorize which product belongs to which family: Entra = identity, Defender = threat protection, Sentinel = SIEM/SOAR, Purview = compliance/governance. Mapping a scenario to the right family answers many questions.
- Watch for renamed products - Azure AD is now Microsoft Entra ID and Microsoft 365 Defender is now Microsoft Defender XDR; the exam may use either name.
- The exam includes true/false and 'which capability' style questions; read whether a statement is asking about a feature (e.g., sensitivity labels) versus a separate solution (e.g., DLP), since several Purview tools overlap.

---

Want the full breakdown? See the complete **[SC-900 study guide](https://certgrid.app/study-guide/sc-900-security-compliance-and-identity-fundamentals)** and **[free practice questions](https://certgrid.app/practice/sc-900-security-compliance-and-identity-fundamentals)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

