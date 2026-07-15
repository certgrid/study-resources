# SC-900 Common Confusions

SC-900 wrong answers usually come from mixing up sibling products or sibling concepts. Work through every pair below. If you cannot explain the difference in one sentence, re-read that section in the study notes.

## The Big Three: Defender for Cloud vs Defender XDR vs Sentinel

The most tested confusion on the exam.

| Product                      | Category    | Focus                                                          | Choose it when the question says...                                  |
| ---------------------------- | ----------- | -------------------------------------------------------------- | -------------------------------------------------------------------- |
| Microsoft Defender for Cloud | CNAPP       | Posture and threat protection for cloud INFRASTRUCTURE         | Secure score for Azure/AWS/GCP, recommendations, workload protection |
| Microsoft Defender XDR       | XDR         | Detect/respond across M365: email, endpoints, identities, apps | Unified incidents, automatic attack disruption, M365 signals         |
| Microsoft Sentinel           | SIEM + SOAR | Collect ALL logs including third party; hunt; automate         | Third-party sources, playbooks, log analytics at scale               |

One-liners:

- Defender for Cloud: "Is my cloud infrastructure configured securely, and are its workloads under attack?"
- Defender XDR: "Correlate this phishing email, the endpoint infection, and the compromised account into one incident."
- Sentinel: "Bring every log in the company together, detect, investigate, and auto-respond."

## Identity Concept Pairs

| Pair                                   | Difference                                                       |
| -------------------------------------- | ---------------------------------------------------------------- |
| Authentication vs authorization        | Prove who you are vs what you may do; AuthN always comes first   |
| Identity provider vs directory service | Verifies identities and issues tokens vs stores identity objects |
| Federation vs synchronization          | Trust between IdPs vs copying accounts from AD DS to Entra ID    |
| SSO vs MFA                             | One sign-in for many apps vs multiple proofs for one sign-in     |
| AD DS vs Microsoft Entra ID            | On-premises Kerberos/LDAP directory vs cloud identity service    |
| Encryption vs hashing                  | Reversible with key vs one-way fingerprint                       |
| Zero Trust vs defense in depth         | Trust model for every request vs layered controls architecture   |

## Microsoft Entra Pairs

| Pair                                              | Difference                                                                                                                             |
| ------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| Entra ID Protection vs Conditional Access         | DETECTS risk (leaked credentials, odd sign-ins) vs ENFORCES policy (require MFA, block); Protection feeds risk INTO Conditional Access |
| User risk vs sign-in risk                         | Account likely compromised vs this specific sign-in looks wrong                                                                        |
| PIM vs access reviews                             | Just-in-time temporary elevation vs periodic recertification                                                                           |
| Access reviews vs entitlement management          | Recheck existing access vs package and grant new access with expiry                                                                    |
| Security defaults vs Conditional Access           | Free fixed baseline vs licensed customizable policies (P1)                                                                             |
| SSPR vs Password Protection                       | Reset forgotten passwords vs ban weak passwords                                                                                        |
| Managed identity vs service principal             | Azure-managed credentials (no secrets) vs app identity you manage                                                                      |
| System-assigned vs user-assigned managed identity | Dies with its resource vs standalone and shareable                                                                                     |
| Entra roles vs Azure RBAC roles                   | Manage identity resources (users, groups) vs manage Azure resources (VMs)                                                              |
| Entra registered vs Entra joined devices          | Personal/BYOD device vs organization-owned device                                                                                      |

## Security Solution Pairs

| Pair                                                       | Difference                                                               |
| ---------------------------------------------------------- | ------------------------------------------------------------------------ |
| Azure Firewall vs NSG                                      | Managed central stateful firewall vs basic subnet/NIC allow-deny rules   |
| Azure Firewall vs WAF                                      | General network traffic vs HTTP attacks on web apps (SQLi, XSS)          |
| DDoS Protection vs Azure Firewall                          | Absorb traffic floods vs filter traffic by rules                         |
| Azure Bastion vs VPN Gateway                               | Browser RDP/SSH to VMs, no public IP vs network-level encrypted tunnel   |
| Defender for Identity vs Entra ID Protection               | On-premises AD attack detection vs cloud sign-in/user risk               |
| Defender for Endpoint vs Defender Vulnerability Management | Detect and respond on devices vs find and prioritize weaknesses          |
| Defender for Office 365 vs Exchange Online Protection      | Advanced phishing/attachment protection vs baseline mail filtering       |
| Defender for Cloud Apps vs Defender for Cloud              | SaaS app security (CASB) vs cloud infrastructure security                |
| SIEM vs SOAR                                               | Collect and analyze vs orchestrate and auto-respond (Sentinel does both) |
| CSPM vs CWP                                                | Configuration posture and score vs live threat protection for workloads  |
| Microsoft Secure Score vs Defender for Cloud secure score  | M365 posture (Defender portal) vs Azure/multicloud posture               |

## Microsoft Purview Pairs

| Pair                                                 | Difference                                                                |
| ---------------------------------------------------- | ------------------------------------------------------------------------- |
| Sensitivity labels vs retention labels               | Classify and PROTECT (encrypt, watermark) vs KEEP or DELETE on schedule   |
| Sensitivity labels vs DLP                            | Protection travels with the file vs blocking data from leaving            |
| Retention policy vs retention label                  | Broad location-level rule vs per-item rule; explicit label wins           |
| Records vs regulatory records                        | Restricted edits/deletes vs absolute lock even for admins                 |
| Content explorer vs Activity explorer                | What/where snapshot of classified items vs history of actions on them     |
| Sensitive info types vs trainable classifiers        | Pattern matching (regex, keywords) vs machine learning from examples      |
| Compliance Manager vs compliance score               | The solution (assessments, actions) vs the metric inside it               |
| Compliance score vs Secure Score                     | Compliance posture vs security posture                                    |
| Insider risk management vs DLP                       | Watch risky insider BEHAVIOR patterns vs block sensitive CONTENT movement |
| eDiscovery vs audit                                  | Find and preserve CONTENT for legal cases vs search ACTIVITY logs         |
| Content search vs eDiscovery (Standard) vs (Premium) | Search only vs + cases/holds vs + custodians/review sets/analytics        |
| Service Trust Portal vs Compliance Manager           | Microsoft's compliance evidence vs YOUR compliance posture                |
| Microsoft Priva vs privacy principles                | Product for your privacy obligations vs Microsoft's commitments           |

## Zero Trust: Principles vs Pillars

Do not mix the two lists.

| The 3 principles       | The 6 pillars  |
| ---------------------- | -------------- |
| Verify explicitly      | Identities     |
| Least privilege access | Devices        |
| Assume breach          | Applications   |
|                        | Data           |
|                        | Infrastructure |
|                        | Networks       |

## Quick Self-Test

Cover the right column and answer from the left:

| Question                                                     | Answer                          |
| ------------------------------------------------------------ | ------------------------------- |
| Which product detects leaked credentials?                    | Microsoft Entra ID Protection   |
| Which product enforces "require MFA from unknown locations"? | Conditional Access              |
| Which product ingests third-party firewall logs?             | Microsoft Sentinel              |
| Which product protects on-premises domain controllers?       | Microsoft Defender for Identity |
| Which label type encrypts a document?                        | Sensitivity label               |
| Which label type deletes email after 7 years?                | Retention label                 |
| Which tool blocks credit card numbers in outbound email?     | DLP                             |
| Which tool detects a departing employee exfiltrating files?  | Insider risk management         |
| Where do you download Microsoft's SOC reports?               | Service Trust Portal            |
| Which score measures your GDPR progress?                     | Compliance score                |
