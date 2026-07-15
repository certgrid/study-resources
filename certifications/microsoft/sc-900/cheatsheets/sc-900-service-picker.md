# SC-900 Service Picker

SC-900 is service-heavy. Most scenario questions reduce to "which Microsoft service solves this?" Match the requirement keyword to the service.

## Identity and Access (Microsoft Entra)

| Requirement keyword                               | Pick                                                |
| ------------------------------------------------- | --------------------------------------------------- |
| Cloud identity and access management              | Microsoft Entra ID                                  |
| Single sign-on to SaaS apps                       | Microsoft Entra ID (SSO)                            |
| Sync on-premises AD users to the cloud            | Microsoft Entra Connect (hybrid identity)           |
| Verify sign-ins with a second factor              | Multifactor authentication (MFA)                    |
| Sign in with no password at all                   | Windows Hello, FIDO2 keys, Authenticator            |
| Let users reset their own passwords               | Self-service password reset (SSPR)                  |
| Ban weak or company-specific passwords            | Microsoft Entra Password Protection                 |
| Require MFA only under certain conditions         | Conditional Access                                  |
| Block sign-ins from specific countries            | Conditional Access (location signal)                |
| Detect leaked credentials and risky sign-ins      | Microsoft Entra ID Protection                       |
| Just-in-time, time-limited admin roles            | Privileged Identity Management (PIM)                |
| Periodically recertify who has access             | Access reviews                                      |
| Request-and-approve bundles of access that expire | Entitlement management                              |
| Automate joiner-mover-leaver identity tasks       | Microsoft Entra ID Governance (lifecycle workflows) |
| App identity in Azure without storing secrets     | Managed identity                                    |
| Partner signs in with their own work credentials  | B2B collaboration (external identities)             |
| Governed identity for an AI agent                 | Agent ID                                            |
| Least-privilege delegation to manage users        | Microsoft Entra roles (e.g. User Administrator)     |

## Azure Network and Infrastructure Security

| Requirement keyword                              | Pick                           |
| ------------------------------------------------ | ------------------------------ |
| Survive a volumetric traffic flood               | Azure DDoS Protection          |
| Central managed firewall across virtual networks | Azure Firewall                 |
| Stop SQL injection and cross-site scripting      | Web Application Firewall (WAF) |
| Isolate app tiers into separate subnets          | VNet segmentation              |
| Allow only port 443 into a subnet                | Network security group (NSG)   |
| RDP/SSH without exposing VMs to the internet     | Azure Bastion                  |
| Store connection strings, keys, certificates     | Azure Key Vault                |

## Posture, SIEM, and Threat Protection

| Requirement keyword                                            | Pick                                                  |
| -------------------------------------------------------------- | ----------------------------------------------------- |
| Security recommendations and secure score for Azure/AWS/GCP    | Microsoft Defender for Cloud (CSPM)                   |
| Threat alerts for servers, storage, SQL, containers            | Defender for Cloud workload protection plans          |
| Collect and correlate logs from Microsoft AND third parties    | Microsoft Sentinel (SIEM)                             |
| Automate incident response with playbooks                      | Microsoft Sentinel (SOAR)                             |
| Hunt across data with KQL queries                              | Microsoft Sentinel / Defender portal advanced hunting |
| One incident correlating email, endpoint, and identity signals | Microsoft Defender XDR                                |
| Phishing, Safe Links, Safe Attachments, attack simulation      | Microsoft Defender for Office 365                     |
| EDR, isolate a compromised laptop                              | Microsoft Defender for Endpoint                       |
| Discover shadow IT and control SaaS sessions                   | Microsoft Defender for Cloud Apps                     |
| Detect pass-the-hash against domain controllers                | Microsoft Defender for Identity                       |
| Inventory and prioritize device CVEs                           | Microsoft Defender Vulnerability Management           |
| Research a threat actor and its infrastructure                 | Microsoft Defender Threat Intelligence                |
| Single console for incidents and Secure Score                  | Microsoft Defender portal                             |

## Compliance and Data (Microsoft Purview and Trust)

| Requirement keyword                                 | Pick                                                  |
| --------------------------------------------------- | ----------------------------------------------------- |
| Microsoft's audit reports and certifications        | Service Trust Portal                                  |
| How Microsoft handles customer data                 | Microsoft privacy principles                          |
| Manage assessments against GDPR/ISO/NIST            | Compliance Manager                                    |
| Risk-weighted compliance progress metric            | Compliance score                                      |
| Find credit card numbers across the estate          | Sensitive information types                           |
| Classify contracts/resumes by ML                    | Trainable classifiers                                 |
| Snapshot of labeled items and their locations       | Content explorer                                      |
| History of label changes and file activities        | Activity explorer                                     |
| Encrypt and watermark documents; protection travels | Sensitivity labels                                    |
| Publish labels, require default/mandatory labeling  | Sensitivity label policies                            |
| Block sensitive data leaving via email/Teams/USB    | Data loss prevention (DLP, Endpoint DLP)              |
| Keep for N years then delete                        | Retention policy (broad) / retention label (per item) |
| Immutable, admin-proof record                       | Regulatory record (records management)                |
| Departing employee downloading masses of files      | Insider risk management                               |
| Search content for an investigation, no case needed | Content search                                        |
| Legal hold plus case management                     | eDiscovery (Standard)                                 |
| Custodians, review sets, ML relevance               | eDiscovery (Premium)                                  |
| Who did what, when (activity logs)                  | Audit (Standard/Premium)                              |
| Keep audit logs up to 10 years                      | Audit (Premium)                                       |

## Two-Step Elimination Method

When two services both look right:

1. Identify the ASSET: identity, network, device, email, SaaS app, cloud workload, data/content, or logs.
2. Identify the ACTION: prevent, detect, respond, prove, keep, or find.

| Asset + action                 | Winner                     |
| ------------------------------ | -------------------------- |
| Identity + detect risk         | Entra ID Protection        |
| Identity + enforce policy      | Conditional Access         |
| Identity + temporary elevation | PIM                        |
| Network + filter               | NSG or Azure Firewall      |
| Web app + attack prevention    | WAF                        |
| Device + detect/respond        | Defender for Endpoint      |
| Email + prevent phishing       | Defender for Office 365    |
| SaaS app + discover/control    | Defender for Cloud Apps    |
| Cloud workload + posture       | Defender for Cloud         |
| All logs + detect/automate     | Microsoft Sentinel         |
| Data + protect                 | Sensitivity labels         |
| Data + prevent leaving         | DLP                        |
| Data + keep/delete             | Retention                  |
| Content + legal find/preserve  | eDiscovery                 |
| Activities + investigate       | Audit                      |
| Microsoft trust + prove        | Service Trust Portal       |
| Your compliance + measure      | Compliance Manager / score |
