# SC-900 Objective Coverage Matrix

This matrix maps every skill bullet from the official "Skills measured as of July 28, 2026" outline to the files in this pack that cover it. Source: the [official study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/sc-900). Last verified: July 10, 2026. If the study guide publishes a newer outline, update this file first.

Primary coverage is listed first (usually a study note), followed by supporting labs, cheatsheets, and diagrams.

## Domain 1: Describe the concepts of security, compliance, and identity (10-15%)

### Describe security and compliance concepts

| Official objective                                       | Covered in                                                                                                                                                                                   |
| -------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Describe the shared responsibility model                 | [Study note 01](study-notes/01-security-compliance-identity-concepts.md), [Exam-Day Review](cheatsheets/sc-900-exam-day-review.md), [Quick Reference](cheatsheets/sc-900-quick-reference.md) |
| Describe defense-in-depth                                | [Study note 01](study-notes/01-security-compliance-identity-concepts.md), [Quick Reference](cheatsheets/sc-900-quick-reference.md)                                                           |
| Describe the Zero Trust model                            | [Study note 01](study-notes/01-security-compliance-identity-concepts.md), [Core Diagrams](diagrams/sc-900-core-diagrams.md), [Common Confusions](cheatsheets/sc-900-common-confusions.md)    |
| Describe encryption and hashing                          | [Study note 01](study-notes/01-security-compliance-identity-concepts.md), [Quick Reference](cheatsheets/sc-900-quick-reference.md)                                                           |
| Describe Governance, Risk, and Compliance (GRC) concepts | [Study note 01](study-notes/01-security-compliance-identity-concepts.md), [Quick Reference](cheatsheets/sc-900-quick-reference.md)                                                           |

### Define identity concepts

| Official objective                                              | Covered in                                                                                                                                                                                       |
| --------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Define identity as the primary security perimeter               | [Study note 01](study-notes/01-security-compliance-identity-concepts.md), [Core Diagrams](diagrams/sc-900-core-diagrams.md)                                                                      |
| Define authentication                                           | [Study note 01](study-notes/01-security-compliance-identity-concepts.md), [Common Confusions](cheatsheets/sc-900-common-confusions.md), [Quick Reference](cheatsheets/sc-900-quick-reference.md) |
| Define authorization                                            | [Study note 01](study-notes/01-security-compliance-identity-concepts.md), [Common Confusions](cheatsheets/sc-900-common-confusions.md), [Quick Reference](cheatsheets/sc-900-quick-reference.md) |
| Describe identity providers                                     | [Study note 01](study-notes/01-security-compliance-identity-concepts.md), [Quick Reference](cheatsheets/sc-900-quick-reference.md)                                                               |
| Describe the concept of directory services and Active Directory | [Study note 01](study-notes/01-security-compliance-identity-concepts.md), [Quick Reference](cheatsheets/sc-900-quick-reference.md)                                                               |
| Describe the concept of federation                              | [Study note 01](study-notes/01-security-compliance-identity-concepts.md), [Common Confusions](cheatsheets/sc-900-common-confusions.md)                                                           |

## Domain 2: Describe the capabilities of Microsoft Entra (25-30%)

### Describe function and identity types of Microsoft Entra ID

| Official objective                               | Covered in                                                                                                                                                                        |
| ------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Describe Microsoft Entra ID                      | [Study note 02](study-notes/02-microsoft-entra-capabilities.md), [Lab 01](labs/01-tour-microsoft-entra-admin-center.md), [Quick Reference](cheatsheets/sc-900-quick-reference.md) |
| Describe types of identities, including agent ID | [Study note 02](study-notes/02-microsoft-entra-capabilities.md), [Lab 02](labs/02-create-user-and-group.md), [Quick Reference](cheatsheets/sc-900-quick-reference.md)             |
| Describe hybrid identity                         | [Study note 02](study-notes/02-microsoft-entra-capabilities.md), [Common Confusions](cheatsheets/sc-900-common-confusions.md)                                                     |

### Describe authentication capabilities of Microsoft Entra ID

| Official objective                                       | Covered in                                                                                                                                                                        |
| -------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Describe the authentication methods                      | [Study note 02](study-notes/02-microsoft-entra-capabilities.md), [Lab 03](labs/03-review-mfa-and-conditional-access.md)                                                           |
| Describe multifactor authentication (MFA)                | [Study note 02](study-notes/02-microsoft-entra-capabilities.md), [Lab 03](labs/03-review-mfa-and-conditional-access.md), [Exam-Day Review](cheatsheets/sc-900-exam-day-review.md) |
| Describe password protection and management capabilities | [Study note 02](study-notes/02-microsoft-entra-capabilities.md), [Lab 03](labs/03-review-mfa-and-conditional-access.md)                                                           |

### Describe access management capabilities of Microsoft Entra ID

| Official objective                                                  | Covered in                                                                                                                                                                 |
| ------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Describe Microsoft Entra Conditional Access                         | [Study note 02](study-notes/02-microsoft-entra-capabilities.md), [Lab 03](labs/03-review-mfa-and-conditional-access.md), [Core Diagrams](diagrams/sc-900-core-diagrams.md) |
| Describe Microsoft Entra roles and role-based access control (RBAC) | [Study note 02](study-notes/02-microsoft-entra-capabilities.md), [Common Confusions](cheatsheets/sc-900-common-confusions.md)                                              |

### Describe identity protection and governance capabilities of Microsoft Entra

| Official objective                                                          | Covered in                                                                                                                                                                            |
| --------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Describe Microsoft Entra ID Governance                                      | [Study note 02](study-notes/02-microsoft-entra-capabilities.md), [Lab 01](labs/01-tour-microsoft-entra-admin-center.md)                                                               |
| Describe access reviews                                                     | [Study note 02](study-notes/02-microsoft-entra-capabilities.md), [Service Picker](cheatsheets/sc-900-service-picker.md)                                                               |
| Describe the capabilities of Microsoft Entra Privileged Identity Management | [Study note 02](study-notes/02-microsoft-entra-capabilities.md), [Service Picker](cheatsheets/sc-900-service-picker.md), [Quick Reference](cheatsheets/sc-900-quick-reference.md)     |
| Describe Microsoft Entra ID Protection                                      | [Study note 02](study-notes/02-microsoft-entra-capabilities.md), [Lab 01](labs/01-tour-microsoft-entra-admin-center.md), [Common Confusions](cheatsheets/sc-900-common-confusions.md) |

## Domain 3: Describe the capabilities of Microsoft security solutions (35-40%)

### Describe core infrastructure security services in Azure

| Official objective                                        | Covered in                                                                                                                    |
| --------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| Describe Azure DDoS Protection                            | [Study note 03](study-notes/03-microsoft-security-solutions.md), [Service Picker](cheatsheets/sc-900-service-picker.md)       |
| Describe Azure Firewall                                   | [Study note 03](study-notes/03-microsoft-security-solutions.md), [Service Picker](cheatsheets/sc-900-service-picker.md)       |
| Describe Azure Web Application Firewall (WAF)             | [Study note 03](study-notes/03-microsoft-security-solutions.md), [Service Picker](cheatsheets/sc-900-service-picker.md)       |
| Describe network segmentation with Azure virtual networks | [Study note 03](study-notes/03-microsoft-security-solutions.md), [Quick Reference](cheatsheets/sc-900-quick-reference.md)     |
| Describe network security groups (NSGs)                   | [Study note 03](study-notes/03-microsoft-security-solutions.md), [Common Confusions](cheatsheets/sc-900-common-confusions.md) |
| Describe Azure Bastion                                    | [Study note 03](study-notes/03-microsoft-security-solutions.md), [Service Picker](cheatsheets/sc-900-service-picker.md)       |
| Describe Azure Key Vault                                  | [Study note 03](study-notes/03-microsoft-security-solutions.md), [Service Picker](cheatsheets/sc-900-service-picker.md)       |

### Describe security management capabilities of Azure

| Official objective                                                                                | Covered in                                                                                                                                                              |
| ------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Describe Microsoft Defender for Cloud                                                             | [Study note 03](study-notes/03-microsoft-security-solutions.md), [Lab 08](labs/08-review-secure-score.md), [Common Confusions](cheatsheets/sc-900-common-confusions.md) |
| Describe Cloud Security Posture Management (CSPM)                                                 | [Study note 03](study-notes/03-microsoft-security-solutions.md), [Lab 08](labs/08-review-secure-score.md)                                                               |
| Describe how security policies, standards, and recommendations improve the cloud security posture | [Study note 03](study-notes/03-microsoft-security-solutions.md), [Lab 08](labs/08-review-secure-score.md)                                                               |
| Describe enhanced security features provided by cloud workload protection                         | [Study note 03](study-notes/03-microsoft-security-solutions.md), [Quick Reference](cheatsheets/sc-900-quick-reference.md)                                               |

### Describe capabilities of Microsoft Sentinel

| Official objective                                                                                                           | Covered in                                                                                                                                                          |
| ---------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Define the concepts of security information and event management (SIEM) and security orchestration automated response (SOAR) | [Study note 03](study-notes/03-microsoft-security-solutions.md), [Lab 05](labs/05-explore-microsoft-sentinel.md), [Core Diagrams](diagrams/sc-900-core-diagrams.md) |
| Describe threat detection and mitigation capabilities in Microsoft Sentinel                                                  | [Study note 03](study-notes/03-microsoft-security-solutions.md), [Lab 05](labs/05-explore-microsoft-sentinel.md)                                                    |

### Describe threat protection with Microsoft Defender XDR

| Official objective                                            | Covered in                                                                                                                                                              |
| ------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Describe Microsoft Defender XDR services                      | [Study note 03](study-notes/03-microsoft-security-solutions.md), [Lab 04](labs/04-tour-microsoft-defender-portal.md), [Core Diagrams](diagrams/sc-900-core-diagrams.md) |
| Describe Microsoft Defender for Office 365                    | [Study note 03](study-notes/03-microsoft-security-solutions.md), [Service Picker](cheatsheets/sc-900-service-picker.md)                                                 |
| Describe Microsoft Defender for Endpoint                      | [Study note 03](study-notes/03-microsoft-security-solutions.md), [Service Picker](cheatsheets/sc-900-service-picker.md)                                                 |
| Describe Microsoft Defender for Cloud Apps                    | [Study note 03](study-notes/03-microsoft-security-solutions.md), [Service Picker](cheatsheets/sc-900-service-picker.md)                                                 |
| Describe Microsoft Defender for Identity                      | [Study note 03](study-notes/03-microsoft-security-solutions.md), [Common Confusions](cheatsheets/sc-900-common-confusions.md)                                           |
| Describe Microsoft Defender Vulnerability Management          | [Study note 03](study-notes/03-microsoft-security-solutions.md), [Quick Reference](cheatsheets/sc-900-quick-reference.md)                                               |
| Describe Microsoft Defender Threat Intelligence (Defender TI) | [Study note 03](study-notes/03-microsoft-security-solutions.md), [Lab 04](labs/04-tour-microsoft-defender-portal.md)                                                    |
| Describe the Microsoft Defender portal                        | [Study note 03](study-notes/03-microsoft-security-solutions.md), [Lab 04](labs/04-tour-microsoft-defender-portal.md)                                                    |

## Domain 4: Describe the capabilities of Microsoft compliance solutions (20-25%)

### Describe Microsoft Service Trust Portal and privacy principles

| Official objective                           | Covered in                                                                                                                                                                     |
| -------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Describe the Service Trust Portal offerings  | [Study note 04](study-notes/04-microsoft-compliance-solutions.md), [Lab 07](labs/07-explore-service-trust-portal.md)                                                           |
| Describe the privacy principles of Microsoft | [Study note 04](study-notes/04-microsoft-compliance-solutions.md), [Lab 07](labs/07-explore-service-trust-portal.md), [Quick Reference](cheatsheets/sc-900-quick-reference.md) |

### Describe compliance management capabilities of Microsoft Purview

| Official objective                                 | Covered in                                                                                                                                                                          |
| -------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Describe the Microsoft Purview portal              | [Study note 04](study-notes/04-microsoft-compliance-solutions.md), [Lab 06](labs/06-tour-microsoft-purview-portal.md)                                                               |
| Describe Compliance Manager                        | [Study note 04](study-notes/04-microsoft-compliance-solutions.md), [Lab 06](labs/06-tour-microsoft-purview-portal.md), [Common Confusions](cheatsheets/sc-900-common-confusions.md) |
| Describe the uses and benefits of compliance score | [Study note 04](study-notes/04-microsoft-compliance-solutions.md), [Lab 08](labs/08-review-secure-score.md)                                                                         |

### Describe information protection, data lifecycle management, and data governance capabilities of Microsoft Purview

| Official objective                                                          | Covered in                                                                                                                                                                          |
| --------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Describe the data classification capabilities                               | [Study note 04](study-notes/04-microsoft-compliance-solutions.md), [Lab 06](labs/06-tour-microsoft-purview-portal.md)                                                               |
| Describe the benefits of Content explorer and Activity explorer             | [Study note 04](study-notes/04-microsoft-compliance-solutions.md), [Quick Reference](cheatsheets/sc-900-quick-reference.md)                                                         |
| Describe sensitivity labels and sensitivity label policies                  | [Study note 04](study-notes/04-microsoft-compliance-solutions.md), [Lab 06](labs/06-tour-microsoft-purview-portal.md), [Common Confusions](cheatsheets/sc-900-common-confusions.md) |
| Describe data loss prevention (DLP)                                         | [Study note 04](study-notes/04-microsoft-compliance-solutions.md), [Lab 06](labs/06-tour-microsoft-purview-portal.md), [Service Picker](cheatsheets/sc-900-service-picker.md)       |
| Describe records management                                                 | [Study note 04](study-notes/04-microsoft-compliance-solutions.md), [Lab 06](labs/06-tour-microsoft-purview-portal.md)                                                               |
| Describe retention policies, retention labels, and retention label policies | [Study note 04](study-notes/04-microsoft-compliance-solutions.md), [Common Confusions](cheatsheets/sc-900-common-confusions.md)                                                     |

### Describe insider risk, eDiscovery, and audit capabilities in Microsoft Purview

| Official objective                                 | Covered in                                                                                                                  |
| -------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| Describe insider risk management                   | [Study note 04](study-notes/04-microsoft-compliance-solutions.md), [Lab 06](labs/06-tour-microsoft-purview-portal.md)       |
| Describe eDiscovery solutions in Microsoft Purview | [Study note 04](study-notes/04-microsoft-compliance-solutions.md), [Quick Reference](cheatsheets/sc-900-quick-reference.md) |
| Describe audit solutions in Microsoft Purview      | [Study note 04](study-notes/04-microsoft-compliance-solutions.md), [Lab 09](labs/09-clean-up-learning-environment.md)       |

## Gaps

None. Every skill bullet in the "Skills measured as of July 28, 2026" outline maps to at least one study note, and most map to a lab or cheatsheet as well. If a future outline adds objectives, list any unmapped bullets here until they are covered.
