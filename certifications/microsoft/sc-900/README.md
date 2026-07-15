# SC-900: Microsoft Security, Compliance, and Identity Fundamentals

SC-900 is the best first step for learning how Microsoft approaches security, compliance, and identity across Azure and Microsoft 365. It does not expect deep hands-on administration, but it does expect you to recognize a large family of products: Microsoft Entra, Microsoft Defender, Microsoft Sentinel, and Microsoft Purview, plus the core concepts that tie them together.

These notes are built for fast revision and real understanding. Read the domain notes once, do the labs, then use the cheatsheets to remove confusion before taking practice tests.

## Start Here

Pick the path that matches your timeline:

| If you have...          | Use this path                                                                                                                    |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| 1 day                   | Read [Exam-Day Review](cheatsheets/sc-900-exam-day-review.md), then [Common Confusions](cheatsheets/sc-900-common-confusions.md) |
| 3 days                  | Read the four study notes, review [Service Picker](cheatsheets/sc-900-service-picker.md), then do practice questions             |
| 5 days                  | Follow the recommended plan below and complete the labs                                                                          |
| No Microsoft experience | Start with [00 - Set Up a Free Learning Tenant](labs/00-set-up-free-learning-tenant.md), then the Entra admin center tour        |

## What to Memorize vs Understand

| Memorize                                                                 | Understand                                                        |
| ------------------------------------------------------------------------ | ----------------------------------------------------------------- |
| Zero Trust principles: verify explicitly, least privilege, assume breach | Why identity is the primary security perimeter in the cloud       |
| Authentication vs authorization                                          | Where each happens in a sign-in flow                              |
| The four product families: Entra, Defender, Sentinel, Purview            | Which family answers identity, threat, SIEM, and compliance needs |
| Defender XDR services: Office 365, Endpoint, Cloud Apps, Identity        | Which asset each Defender service protects                        |
| Conditional Access signals and controls                                  | How signals lead to allow, block, or require MFA decisions        |
| Purview tools: labels, DLP, retention, insider risk, eDiscovery          | Protecting data vs keeping data vs investigating data             |
| SIEM vs SOAR vs XDR                                                      | Collect and analyze vs automate response vs detect across domains |

## Exam Snapshot

| Item           | Detail                                                               |
| -------------- | -------------------------------------------------------------------- |
| Exam code      | SC-900                                                               |
| Certification  | Microsoft Certified: Security, Compliance, and Identity Fundamentals |
| Level          | Beginner                                                             |
| Passing score  | 700 out of 1000                                                      |
| Question style | Conceptual and scenario-based fundamentals                           |
| Best for       | Students, business stakeholders, and new IT professionals            |
| Study approach | Learn concepts, map services to problems, do small portal tours      |

## Official Skill Areas

Aligned to the official "Skills measured as of July 28, 2026" outline. Always confirm the active outline on the [official study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/sc-900) before booking.

Last verified: July 10, 2026.

Note: the July 28, 2026 outline is dated in the future. If you take the exam before July 28, 2026, re-check the study guide to confirm which outline version applies to your exam date.

Every skill bullet in the outline is mapped to a local file in the [Objective Coverage Matrix](coverage-matrix.md).

| Domain | Skill area                                                  | Weight |
| ------ | ----------------------------------------------------------- | ------ |
| 1      | Describe the concepts of security, compliance, and identity | 10-15% |
| 2      | Describe the capabilities of Microsoft Entra                | 25-30% |
| 3      | Describe the capabilities of Microsoft security solutions   | 35-40% |
| 4      | Describe the capabilities of Microsoft compliance solutions | 20-25% |

## How to Use This Folder

1. Read the four study notes in order.
2. Open the common-confusions file and check every pair you mix up.
3. Complete the beginner labs so the portals and terms become real.
4. Review the diagrams before practice tests.
5. Use the quick reference on the final day.

## Contents

Not sure something is covered? The [Objective Coverage Matrix](coverage-matrix.md) maps every official skill bullet to the file that covers it.

### Study Notes

| File                                                                                                        | Use it for                                                                                          |
| ----------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| [01 - Security, Compliance, and Identity Concepts](study-notes/01-security-compliance-identity-concepts.md) | Shared responsibility, defense in depth, Zero Trust, encryption, GRC, identity concepts             |
| [02 - Microsoft Entra Capabilities](study-notes/02-microsoft-entra-capabilities.md)                         | Entra ID, identity types, hybrid identity, MFA, Conditional Access, governance, ID Protection       |
| [03 - Microsoft Security Solutions](study-notes/03-microsoft-security-solutions.md)                         | Azure network security, Defender for Cloud, Sentinel, Defender XDR                                  |
| [04 - Microsoft Compliance Solutions](study-notes/04-microsoft-compliance-solutions.md)                     | Service Trust Portal, privacy, Purview compliance, data protection, insider risk, eDiscovery, audit |

### Cheatsheets

| File                                                                | Use it for                                                            |
| ------------------------------------------------------------------- | --------------------------------------------------------------------- |
| [SC-900 Quick Reference](cheatsheets/sc-900-quick-reference.md)     | Last-day revision, including the Identity Capability Matrix           |
| [SC-900 Common Confusions](cheatsheets/sc-900-common-confusions.md) | Fixing the traps that cause wrong answers                             |
| [SC-900 Service Picker](cheatsheets/sc-900-service-picker.md)       | Choosing the right Microsoft service quickly                          |
| [SC-900 Exam-Day Review](cheatsheets/sc-900-exam-day-review.md)     | Final 30-45 minute review before the exam                             |
| [SC-900 Mock Review](cheatsheets/sc-900-mock-review.md)             | Mixed scenario drills across all four domains, weighted like the exam |

### Hands-On Labs

| Lab                                                                                            | What it teaches                                                   |
| ---------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| [00 - Set Up a Free Learning Tenant](labs/00-set-up-free-learning-tenant.md)                   | Free tenant options, billing awareness, safe learning setup       |
| [01 - Tour the Microsoft Entra Admin Center](labs/01-tour-microsoft-entra-admin-center.md)     | Entra admin center layout, tenant basics, where key features live |
| [02 - Create a User and a Group](labs/02-create-user-and-group.md)                             | Cloud identities, users, groups, group membership types           |
| [03 - Review MFA and Conditional Access Options](labs/03-review-mfa-and-conditional-access.md) | Authentication methods, MFA, Conditional Access policy anatomy    |
| [04 - Tour the Microsoft Defender Portal](labs/04-tour-microsoft-defender-portal.md)           | Defender XDR portal, incidents, threat intelligence, exposure     |
| [05 - Explore Microsoft Sentinel](labs/05-explore-microsoft-sentinel.md)                       | SIEM/SOAR concepts, workspaces, cost awareness                    |
| [06 - Tour the Microsoft Purview Portal](labs/06-tour-microsoft-purview-portal.md)             | Purview solutions map, Compliance Manager, classification tools   |
| [07 - Explore the Service Trust Portal](labs/07-explore-service-trust-portal.md)               | Audit reports, compliance documentation, privacy resources        |
| [08 - Review Secure Score](labs/08-review-secure-score.md)                                     | Microsoft Secure Score vs Defender for Cloud secure score         |
| [09 - Clean Up Your Learning Environment](labs/09-clean-up-learning-environment.md)            | Removing lab users, policies, and any cost-bearing resources      |

### Diagrams

| Diagram                                                  | What it teaches                                                   |
| -------------------------------------------------------- | ----------------------------------------------------------------- |
| [SC-900 Core Diagrams](diagrams/sc-900-core-diagrams.md) | Zero Trust model, Microsoft security portfolio map, identity flow |

## What Usually Decides Pass or Fail

Most SC-900 mistakes come from confusing similar products and terms:

| If you confuse...                              | Review                                                   |
| ---------------------------------------------- | -------------------------------------------------------- |
| Authentication and authorization               | Proving who you are vs what you are allowed to do        |
| Defender for Cloud, Defender XDR, and Sentinel | Cloud posture vs M365 threat detection vs SIEM/SOAR      |
| Conditional Access and Entra ID Protection     | Policy enforcement vs risk detection                     |
| Defender for Identity and Entra ID Protection  | On-premises AD attacks vs cloud sign-in risk             |
| Sensitivity labels and retention labels        | Protecting data vs keeping or deleting data              |
| Compliance Manager and Microsoft Secure Score  | Compliance posture vs security posture                   |
| Federation and hybrid identity synchronization | Trust between providers vs syncing accounts to the cloud |

## High-Value Exam Traps

| Trap                                                        | Correct thinking                                                         |
| ----------------------------------------------------------- | ------------------------------------------------------------------------ |
| "Need to verify a user's identity"                          | That is authentication (AuthN), not authorization (AuthZ).               |
| "Need to block risky sign-ins automatically"                | Entra ID Protection detects risk; Conditional Access enforces the block. |
| "Need SIEM across Microsoft and third-party sources"        | Use Microsoft Sentinel, not Defender XDR.                                |
| "Need to protect on-premises Active Directory from attacks" | Use Microsoft Defender for Identity.                                     |
| "Need to find and label sensitive data"                     | Use Microsoft Purview Information Protection, not Defender.              |
| "Need to prevent credit card numbers leaving via email"     | Use Purview data loss prevention (DLP).                                  |
| "Need just-in-time admin access"                            | Use Microsoft Entra Privileged Identity Management (PIM).                |
| "Need RDP/SSH to a VM without a public IP"                  | Use Azure Bastion.                                                       |
| "Need to store secrets, keys, and certificates"             | Use Azure Key Vault.                                                     |
| "Need Microsoft's audit reports for a regulator"            | Use the Service Trust Portal.                                            |

## Recommended 5-Day Plan

| Day | Focus                                                                                  |
| --- | -------------------------------------------------------------------------------------- |
| 1   | Security, compliance, and identity concepts: Zero Trust, defense in depth, AuthN/AuthZ |
| 2   | Microsoft Entra: identity types, MFA, Conditional Access, governance, ID Protection    |
| 3   | Security solutions: Azure network security, Defender for Cloud, Sentinel, Defender XDR |
| 4   | Compliance solutions: Purview, Service Trust Portal, plus labs and common confusions   |
| 5   | Quick reference, service picker, practice questions, wrong-answer review               |

## Readiness Checklist

Before booking, you should be able to explain these without notes:

- The three Zero Trust principles and the six foundational pillars
- Authentication vs authorization, and identity as the primary security perimeter
- The four identity types in Microsoft Entra ID, including agent ID
- What Conditional Access signals, conditions, and controls are
- PIM vs access reviews vs entitlement management
- Defender for Cloud vs Defender XDR vs Microsoft Sentinel
- Which Defender service protects email, endpoints, SaaS apps, and on-premises AD
- Sensitivity labels vs retention labels vs DLP
- Compliance Manager and compliance score vs Secure Score
- What the Service Trust Portal offers

## Score Booster Routine

Use this after each practice test:

1. Write down every wrong answer in one line.
2. Label the reason: concept gap, product confusion, portal confusion, or scope confusion (Azure vs M365).
3. Re-read only the matching section in this folder.
4. Add the confused pair to your own notes.
5. Retake a small focused quiz before doing another full mock.

The goal is not to memorize answers. The goal is to stop repeating the same type of mistake.

## Note on Exam Content

These are original study notes. They do not contain real exam questions or leaked content. Use them to understand the concepts, then practice with scenario-based questions and portal exploration.

---

Maintained by the team behind [CertGrid](https://certgrid.app). Free practice is available on CertGrid, but these notes are useful on their own.
