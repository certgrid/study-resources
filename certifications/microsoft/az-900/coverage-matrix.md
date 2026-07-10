# AZ-900 Coverage Matrix

This matrix maps every objective in the [official AZ-900 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/az-900) (skills measured as of July 20, 2026) to the local files that cover it. Use it to confirm nothing in the official outline is left unread before you book.

Last verified: July 10, 2026

## Domain 1: Describe cloud concepts (25-30%)

### Describe cloud computing

| Official objective                                         | Covered in                                                                                                                                                                                                                               |
| ---------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Define cloud computing                                     | [01 - Cloud Concepts](study-notes/01-cloud-concepts.md) (What you must know)                                                                                                                                                             |
| Describe the shared responsibility model                   | [01 - Cloud Concepts](study-notes/01-cloud-concepts.md) (Shared responsibility model), [Exam-Day Review](cheatsheets/az-900-exam-day-review.md) (Service Model Responsibility)                                                           |
| Define cloud models, including public, private, and hybrid | [01 - Cloud Concepts](study-notes/01-cloud-concepts.md) (Cloud deployment models)                                                                                                                                                        |
| Identify appropriate use cases for each cloud model        | [01 - Cloud Concepts](study-notes/01-cloud-concepts.md) (Cloud deployment models, Common confusions)                                                                                                                                     |
| Describe the consumption-based model                       | [01 - Cloud Concepts](study-notes/01-cloud-concepts.md) (Consumption-based model), [Quick Reference](cheatsheets/az-900-quick-reference.md) (Cloud Basics)                                                                               |
| Compare cloud pricing models                               | [01 - Cloud Concepts](study-notes/01-cloud-concepts.md) (CapEx vs OpEx, Consumption-based model), [03 - Management and Governance](study-notes/03-management-governance.md) (Factors That Affect Cost: reserved capacity, savings plans) |
| Describe serverless                                        | [02 - Azure Architecture and Services](study-notes/02-azure-architecture-services.md) (Core Compute Services: Azure Functions), [Common Confusions](cheatsheets/az-900-common-confusions.md) (Service Models: Serverless)                |

### Describe the benefits of using cloud services

| Official objective                                                      | Covered in                                                                                                           |
| ----------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| Describe the benefits of high availability and scalability in the cloud | [01 - Cloud Concepts](study-notes/01-cloud-concepts.md) (Cloud benefits: High availability, Scalability, Elasticity) |
| Describe the benefits of reliability and predictability in the cloud    | [01 - Cloud Concepts](study-notes/01-cloud-concepts.md) (Cloud benefits: Reliability, Predictability)                |
| Describe the benefits of security and governance in the cloud           | [01 - Cloud Concepts](study-notes/01-cloud-concepts.md) (Cloud benefits: Security and governance)                    |
| Describe the benefits of manageability in the cloud                     | [01 - Cloud Concepts](study-notes/01-cloud-concepts.md) (Manageability)                                              |

### Describe cloud service types

| Official objective                                                                | Covered in                                                                                                                                                          |
| --------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Describe infrastructure as a service (IaaS)                                       | [01 - Cloud Concepts](study-notes/01-cloud-concepts.md) (Cloud service models), [Lab 04 - Create a Virtual Machine](labs/04-create-virtual-machine.md)              |
| Describe platform as a service (PaaS)                                             | [01 - Cloud Concepts](study-notes/01-cloud-concepts.md) (Cloud service models), [Quick Reference](cheatsheets/az-900-quick-reference.md) (Service Models)           |
| Describe software as a service (SaaS)                                             | [01 - Cloud Concepts](study-notes/01-cloud-concepts.md) (Cloud service models), [Quick Reference](cheatsheets/az-900-quick-reference.md) (Service Models)           |
| Identify appropriate use cases for each cloud service type (IaaS, PaaS, and SaaS) | [01 - Cloud Concepts](study-notes/01-cloud-concepts.md) (Mini scenarios, Fast elimination method), [Service Picker](cheatsheets/az-900-service-picker.md) (Compute) |

## Domain 2: Describe Azure architecture and services (35-40%)

### Describe the core architectural components of Azure

| Official objective                                                              | Covered in                                                                                                                                                                                                                                                     |
| ------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Describe Azure regions, region pairs, and sovereign regions                     | [02 - Azure Architecture and Services](study-notes/02-azure-architecture-services.md) (Azure Global Infrastructure, Regions, Region Pairs)                                                                                                                     |
| Describe availability zones                                                     | [02 - Azure Architecture and Services](study-notes/02-azure-architecture-services.md) (Availability Zones), [Azure Core Architecture](diagrams/azure-core-architecture.md)                                                                                     |
| Describe Azure datacenters                                                      | [02 - Azure Architecture and Services](study-notes/02-azure-architecture-services.md) (Azure Global Infrastructure, Availability Zones)                                                                                                                        |
| Describe Azure resources and resource groups                                    | [02 - Azure Architecture and Services](study-notes/02-azure-architecture-services.md) (Azure Management Hierarchy), [Lab 02 - Create a Resource Group](labs/02-create-resource-group.md)                                                                       |
| Describe subscriptions                                                          | [02 - Azure Architecture and Services](study-notes/02-azure-architecture-services.md) (Azure Management Hierarchy), [Lab 00 - Create an Azure Free Account Safely](labs/00-create-azure-free-account.md)                                                       |
| Describe management groups                                                      | [02 - Azure Architecture and Services](study-notes/02-azure-architecture-services.md) (Azure Management Hierarchy)                                                                                                                                             |
| Describe the hierarchy of resource groups, subscriptions, and management groups | [02 - Azure Architecture and Services](study-notes/02-azure-architecture-services.md) (Azure Management Hierarchy), [Azure Core Architecture](diagrams/azure-core-architecture.md), [Quick Reference](cheatsheets/az-900-quick-reference.md) (Azure Hierarchy) |

### Describe Azure compute and networking services

| Official objective                                                                                                                                 | Covered in                                                                                                                                                                                                                           |
| -------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Compare compute types, including containers, virtual machines, and functions                                                                       | [02 - Azure Architecture and Services](study-notes/02-azure-architecture-services.md) (Core Compute Services, Compute Decision Table)                                                                                                |
| Describe virtual machine options, including Azure virtual machines, Azure Virtual Machine Scale Sets, availability sets, and Azure Virtual Desktop | [02 - Azure Architecture and Services](study-notes/02-azure-architecture-services.md) (Core Compute Services, VM Resiliency Options)                                                                                                 |
| Describe the resources required for virtual machines                                                                                               | [Lab 04 - Create a Virtual Machine](labs/04-create-virtual-machine.md) (Review networking, Clean up), [02 - Azure Architecture and Services](study-notes/02-azure-architecture-services.md) (Managed Disks in Core Storage Services) |
| Describe application hosting options, including web apps, containers, and virtual machines                                                         | [02 - Azure Architecture and Services](study-notes/02-azure-architecture-services.md) (Compute Decision Table), [Service Picker](cheatsheets/az-900-service-picker.md) (Compute)                                                     |
| Describe virtual networking, including the purpose of Azure virtual networks, subnets, peering, Azure DNS, Azure VPN Gateway, and ExpressRoute     | [02 - Azure Architecture and Services](study-notes/02-azure-architecture-services.md) (Core Networking Services, Networking Decision Table), [Lab 07 - Create a Basic Virtual Network](labs/07-create-basic-virtual-network.md)      |
| Define public and private endpoints                                                                                                                | [02 - Azure Architecture and Services](study-notes/02-azure-architecture-services.md) (Public vs private endpoints)                                                                                                                  |

### Describe Azure storage services

| Official objective                                                                               | Covered in                                                                                                                                                                                  |
| ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Compare Azure Storage services                                                                   | [02 - Azure Architecture and Services](study-notes/02-azure-architecture-services.md) (Core Storage Services), [Service Picker](cheatsheets/az-900-service-picker.md) (Storage)             |
| Describe storage tiers                                                                           | [02 - Azure Architecture and Services](study-notes/02-azure-architecture-services.md) (Blob Storage Access Tiers), [Quick Reference](cheatsheets/az-900-quick-reference.md) (Storage Tiers) |
| Describe redundancy options                                                                      | [02 - Azure Architecture and Services](study-notes/02-azure-architecture-services.md) (Storage Redundancy), [Lab 03 - Create a Storage Account](labs/03-create-storage-account.md)          |
| Describe storage account options and storage types                                               | [Lab 03 - Create a Storage Account](labs/03-create-storage-account.md), [02 - Azure Architecture and Services](study-notes/02-azure-architecture-services.md) (Core Storage Services)       |
| Identify options for moving files, including AzCopy, Azure Storage Explorer, and Azure File Sync | [02 - Azure Architecture and Services](study-notes/02-azure-architecture-services.md) (Moving and Migrating Data)                                                                           |
| Describe migration options, including Azure Migrate and Azure Data Box                           | [02 - Azure Architecture and Services](study-notes/02-azure-architecture-services.md) (Moving and Migrating Data)                                                                           |

### Describe Azure identity, access, and security

| Official objective                                                                                                           | Covered in                                                                                                                                                                                                                                                                |
| ---------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Describe directory services in Azure, including Microsoft Entra ID and Microsoft Entra Domain Services                       | [02 - Azure Architecture and Services](study-notes/02-azure-architecture-services.md) (Identity Services), [Lab 08 - Review Microsoft Entra ID](labs/08-review-microsoft-entra-id.md)                                                                                     |
| Describe authentication methods in Azure, including single sign-on (SSO), multifactor authentication (MFA), and passwordless | [02 - Azure Architecture and Services](study-notes/02-azure-architecture-services.md) (Identity Services table), [Lab 08 - Review Microsoft Entra ID](labs/08-review-microsoft-entra-id.md)                                                                               |
| Describe external identities in Azure                                                                                        | [02 - Azure Architecture and Services](study-notes/02-azure-architecture-services.md) (Identity Services table: External identities B2B / B2C)                                                                                                                            |
| Describe Microsoft Entra Conditional Access                                                                                  | [02 - Azure Architecture and Services](study-notes/02-azure-architecture-services.md) (Identity Services table), [Lab 08 - Review Microsoft Entra ID](labs/08-review-microsoft-entra-id.md), [Service Picker](cheatsheets/az-900-service-picker.md) (Identity and Access) |
| Describe Azure role-based access control (RBAC)                                                                              | [03 - Management and Governance](study-notes/03-management-governance.md) (RBAC), [Lab 11 - Review RBAC Access](labs/11-review-rbac-access.md)                                                                                                                            |
| Describe the concept of Zero Trust                                                                                           | [02 - Azure Architecture and Services](study-notes/02-azure-architecture-services.md) (Core Security Concepts), [Quick Reference](cheatsheets/az-900-quick-reference.md) (Security Basics)                                                                                |
| Describe the purpose of the defense-in-depth model                                                                           | [02 - Azure Architecture and Services](study-notes/02-azure-architecture-services.md) (Core Security Concepts), [Quick Reference](cheatsheets/az-900-quick-reference.md) (Security Basics)                                                                                |
| Describe the purpose of Microsoft Defender for Cloud                                                                         | [03 - Management and Governance](study-notes/03-management-governance.md) (Microsoft Defender for Cloud), [Service Picker](cheatsheets/az-900-service-picker.md) (Security and Compliance)                                                                                |

## Domain 3: Describe Azure management and governance (30-35%)

### Describe cost management in Azure

| Official objective                              | Covered in                                                                                                                                                                       |
| ----------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Describe factors that can affect costs in Azure | [03 - Management and Governance](study-notes/03-management-governance.md) (Factors That Affect Cost, Cost Optimization)                                                          |
| Explore the pricing calculator                  | [03 - Management and Governance](study-notes/03-management-governance.md) (Cost Tools), [Common Confusions](cheatsheets/az-900-common-confusions.md) (Cost Tools)                |
| Describe cost management capabilities in Azure  | [03 - Management and Governance](study-notes/03-management-governance.md) (Cost Tools), [Lab 05 - Configure a Budget and Cost Alert](labs/05-configure-budget-and-cost-alert.md) |
| Describe the purpose of tags                    | [03 - Management and Governance](study-notes/03-management-governance.md) (Tags), [Lab 06 - Apply Tags to Resources](labs/06-apply-tags-to-resources.md)                         |

### Describe features and tools in Azure for governance and compliance

| Official objective                                 | Covered in                                                                                                                                                                      |
| -------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Describe the purpose of Microsoft Purview in Azure | [03 - Management and Governance](study-notes/03-management-governance.md) (Microsoft Purview), [Service Picker](cheatsheets/az-900-service-picker.md) (Security and Compliance) |
| Describe the purpose of Azure Policy               | [03 - Management and Governance](study-notes/03-management-governance.md) (Azure Policy), [Lab 13 - Explore Azure Policy](labs/13-explore-azure-policy.md)                      |
| Describe the purpose of resource locks             | [03 - Management and Governance](study-notes/03-management-governance.md) (Resource Locks), [Lab 12 - Apply a Resource Lock](labs/12-apply-resource-lock.md)                    |

### Describe features and tools for managing and deploying Azure resources

| Official objective                                          | Covered in                                                                                                                                                                 |
| ----------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Describe the Azure portal                                   | [03 - Management and Governance](study-notes/03-management-governance.md) (Azure Management Tools), [Lab 01 - Navigate the Azure Portal](labs/01-navigate-azure-portal.md) |
| Describe Azure Cloud Shell, Azure CLI, and Azure PowerShell | [03 - Management and Governance](study-notes/03-management-governance.md) (Azure Management Tools), [Lab 09 - Use Azure Cloud Shell](labs/09-use-azure-cloud-shell.md)     |
| Describe the purpose of Azure Arc                           | [03 - Management and Governance](study-notes/03-management-governance.md) (Azure Management Tools table row only - brief)                                                  |
| Describe infrastructure as code (IaC)                       | [03 - Management and Governance](study-notes/03-management-governance.md) (Azure Management Tools table row only - brief)                                                  |
| Describe Azure Resource Manager (ARM) and ARM templates     | [03 - Management and Governance](study-notes/03-management-governance.md) (Azure Resource Manager section)                                                                 |

### Describe monitoring tools in Azure

| Official objective                                                                                            | Covered in                                                                                                                                                                                                                                                  |
| ------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Describe the purpose of Azure Advisor                                                                         | [03 - Management and Governance](study-notes/03-management-governance.md) (Cost Tools, Common Confusions), [Lab 14 - Review Azure Advisor](labs/14-review-azure-advisor.md)                                                                                 |
| Describe Azure Service Health                                                                                 | [03 - Management and Governance](study-notes/03-management-governance.md) (Service Health vs Azure Status vs Resource Health)                                                                                                                               |
| Describe Azure Monitor, including Log Analytics, Azure Monitor alerts, and Azure Monitor Application Insights | [03 - Management and Governance](study-notes/03-management-governance.md) (Azure Monitor), [Lab 15 - Explore Azure Monitor Alerts](labs/15-explore-azure-monitor-alerts.md), [Service Picker](cheatsheets/az-900-service-picker.md) (Monitoring and Health) |

## Gaps

None. Every skill bullet in the July 20, 2026 outline maps to at least one file above. Two gaps found during the July 10, 2026 verification (cloud manageability benefits; Azure Resource Manager as the deployment layer) were fixed the same day by adding the Manageability section to study note 01 and the Azure Resource Manager section to study note 03. Re-compare against the official study guide if Microsoft revises the outline.
