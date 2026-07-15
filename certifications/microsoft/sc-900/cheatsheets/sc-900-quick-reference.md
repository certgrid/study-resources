# SC-900 Quick Reference

Use this page for last-day revision. It compresses the whole exam into recognition tables.

## Core Concepts in One Line Each

| Concept                  | One-line definition                                                                  |
| ------------------------ | ------------------------------------------------------------------------------------ |
| Shared responsibility    | Provider secures the cloud platform; customer always keeps data, devices, identities |
| Defense in depth         | Multiple security layers so one failure is not fatal                                 |
| CIA triad                | Confidentiality, integrity, availability                                             |
| Zero Trust               | Verify explicitly, least privilege, assume breach                                    |
| Encryption               | Reversible protection with a key (at rest, in transit)                               |
| Hashing                  | One-way fingerprint, no key, used for passwords and integrity                        |
| GRC                      | Governance (your rules), risk (uncertainty), compliance (external rules)             |
| Authentication (AuthN)   | Proving who you are                                                                  |
| Authorization (AuthZ)    | What you are allowed to do                                                           |
| Identity provider        | Creates, manages, and verifies identities; issues tokens; enables SSO                |
| Federation               | Trust between identity providers; no duplicate credentials                           |
| Active Directory (AD DS) | On-premises directory using Kerberos/LDAP                                            |

## Microsoft Entra Family

| Capability          | Job                                                                |
| ------------------- | ------------------------------------------------------------------ |
| Microsoft Entra ID  | Cloud identity and access management                               |
| Identity types      | Users, workload identities, devices, external identities, agent ID |
| Managed identity    | Azure resource identity with no secrets to manage                  |
| Agent ID            | Governed, auditable identity for AI agents                         |
| Hybrid identity     | On-premises accounts synced to the cloud via Entra Connect         |
| MFA                 | Two or more of: know, have, are                                    |
| Passwordless        | Windows Hello, FIDO2 keys/passkeys, Authenticator sign-in          |
| SSPR                | Users reset their own passwords                                    |
| Password Protection | Global and custom banned password lists                            |
| Conditional Access  | If/then policies: signals in, decision out (P1)                    |
| Entra roles / RBAC  | Least-privilege management of identity resources                   |
| Entra ID Governance | Lifecycle workflows, entitlement management                        |
| Access reviews      | Periodic recertification of access                                 |
| PIM                 | Just-in-time, time-bound privileged access (P2)                    |
| Entra ID Protection | Detects user risk and sign-in risk (P2)                            |

## Identity Capability Matrix

One page, one question: which Entra capabilities apply to which identity type?

| Identity type       | AuthN                                       | AuthZ                                 | Conditional Access                       | PIM                           | Access reviews                       | ID Protection                                       |
| ------------------- | ------------------------------------------- | ------------------------------------- | ---------------------------------------- | ----------------------------- | ------------------------------------ | --------------------------------------------------- |
| Users               | Password, MFA, passwordless                 | Entra roles, Azure RBAC, app access   | Yes: the primary policy target           | Yes: eligible role activation | Yes: groups, apps, roles             | Yes: user risk and sign-in risk                     |
| Workload identities | Certificates, secrets; managed IDs use none | App permissions, Azure RBAC           | Yes: separate workload identity policies | No: roles assigned directly   | Limited: reviews of role assignments | Yes: risky workload identity detections             |
| Devices             | Device credential when registered/joined    | Device state informs access, no roles | Yes: require compliant or joined device  | No                            | No: cleaned up via device management | Feeds sign-in risk as a signal                      |
| External identities | Home tenant authenticates (B2B trust)       | Guest permissions, scoped access      | Yes: policies apply to guests            | Yes: guests can be eligible   | Yes: classic guest recertification   | Sign-in risk evaluated; home tenant owns user fixes |
| Agent ID            | Its own governed identity for AI agents     | Scoped, least-privilege permissions   | Governed like other non-human identities | No: scope permissions instead | Yes: governed and auditable access   | Auditable activity; watch for risk signals          |

What each capability answers:

| Capability             | Question it answers                                                |
| ---------------------- | ------------------------------------------------------------------ |
| Authentication (AuthN) | Who are you?                                                       |
| Authorization (AuthZ)  | What are you allowed to do?                                        |
| Conditional Access     | Should this sign-in be allowed right now? (policy gate at sign-in) |
| PIM                    | Do you need this privilege right now? (just-in-time elevation)     |
| Access reviews         | Do you still need this access?                                     |
| ID Protection          | How risky is this sign-in or this user?                            |

## Azure Infrastructure Security

| Service               | Protects against / provides                                   |
| --------------------- | ------------------------------------------------------------- |
| Azure DDoS Protection | Traffic flood attacks at the network edge                     |
| Azure Firewall        | Managed stateful firewall, central rules, threat intelligence |
| Azure WAF             | SQL injection, XSS, and other web attacks                     |
| VNet segmentation     | Isolated subnets, contained breach zones                      |
| NSG                   | Basic allow/deny by IP, port, protocol on subnets/NICs        |
| Azure Bastion         | Portal-based RDP/SSH without public IPs on VMs                |
| Azure Key Vault       | Secrets, keys, and certificates storage and control           |

## Defend and Detect

| Product                           | Category    | Watch for keywords                                       |
| --------------------------------- | ----------- | -------------------------------------------------------- |
| Microsoft Defender for Cloud      | CNAPP       | Posture, secure score, recommendations, multicloud       |
| Foundational CSPM                 | Free tier   | Secure score, basic recommendations                      |
| Cloud workload protection (CWP)   | Paid plans  | Threat alerts for servers, storage, SQL, containers      |
| Microsoft Sentinel                | SIEM + SOAR | Collect all logs, third-party sources, playbooks         |
| Microsoft Defender XDR            | XDR         | Unified incidents across M365 signals                    |
| Defender for Office 365           | Email       | Phishing, Safe Links, Safe Attachments                   |
| Defender for Endpoint             | Devices     | EDR, isolate device, attack surface reduction            |
| Defender for Cloud Apps           | SaaS (CASB) | Shadow IT, app discovery, session controls               |
| Defender for Identity             | On-prem AD  | Domain controller sensors, lateral movement              |
| Defender Vulnerability Management | Weaknesses  | CVE inventory, risk-based prioritization                 |
| Defender Threat Intelligence      | Research    | Threat actors, indicators of compromise                  |
| Microsoft Defender portal         | Console     | security.microsoft.com, incidents, hunting, Secure Score |

## Microsoft Purview Family

| Capability                  | Job                                                                        |
| --------------------------- | -------------------------------------------------------------------------- |
| Purview portal              | Single home for compliance and governance solutions                        |
| Compliance Manager          | Assessments, controls, improvement actions                                 |
| Compliance score            | Risk-weighted percentage of compliance posture                             |
| Sensitive information types | Pattern-based classification (regex, keywords)                             |
| Trainable classifiers       | ML-based classification from examples                                      |
| Content explorer            | Snapshot: what classified data exists and where                            |
| Activity explorer           | History: what is being done with classified data                           |
| Sensitivity labels          | Classify and protect (encrypt, watermark); travels with file               |
| DLP                         | Prevent sensitive data from leaving                                        |
| Retention policies/labels   | Keep or delete content on a schedule                                       |
| Records management          | Declare immutable records; regulatory records absolute                     |
| Insider risk management     | Risky insider behavior; pseudonymized by default                           |
| eDiscovery                  | Content search < Standard (holds, cases) < Premium (custodians, analytics) |
| Audit                       | Activity logs; Standard 180 days, Premium 1-10 years                       |

## Trust and Privacy

| Item                 | Detail                                                                                                 |
| -------------------- | ------------------------------------------------------------------------------------------------------ |
| Service Trust Portal | Microsoft's audit reports, certifications, compliance documentation                                    |
| Privacy principles   | Control, transparency, security, strong legal protections, no content-based targeting, benefits to you |

## License Anchors Worth Knowing

| Feature                        | Requires              |
| ------------------------------ | --------------------- |
| Security defaults              | Free                  |
| Conditional Access             | Microsoft Entra ID P1 |
| Entra ID Protection            | Microsoft Entra ID P2 |
| Privileged Identity Management | Microsoft Entra ID P2 |

## The Four Portals

| Portal                       | URL feel               | Home of                                       |
| ---------------------------- | ---------------------- | --------------------------------------------- |
| Microsoft Entra admin center | entra.microsoft.com    | Identity: users, groups, Conditional Access   |
| Microsoft Defender portal    | security.microsoft.com | Defender XDR, incidents, Secure Score         |
| Microsoft Purview portal     | purview.microsoft.com  | Compliance and data governance solutions      |
| Azure portal                 | portal.azure.com       | Azure resources, Defender for Cloud, Sentinel |
