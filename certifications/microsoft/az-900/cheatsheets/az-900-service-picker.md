# AZ-900 Service Picker

Use this page when a question asks: "Which Azure service should you choose?"

AZ-900 usually gives a short business requirement and expects you to map it to the right service family. Do not overthink advanced configuration. Pick the service that best matches the keyword.

## Compute

| Requirement                                               | Choose                     | Why                             |
| --------------------------------------------------------- | -------------------------- | ------------------------------- |
| Full control over operating system and installed software | Azure Virtual Machines     | IaaS gives maximum control      |
| Run many identical VMs and scale them together            | Virtual Machine Scale Sets | Designed for scalable VM groups |
| Host a web app or API without managing servers            | Azure App Service          | PaaS web hosting                |
| Run code when an event happens                            | Azure Functions            | Serverless event-driven compute |
| Run a container quickly without orchestrating a cluster   | Azure Container Instances  | Simple container hosting        |
| Manage many containers with orchestration                 | Azure Kubernetes Service   | Managed Kubernetes              |
| Provide cloud-hosted Windows desktops or remote apps      | Azure Virtual Desktop      | Desktop and app virtualization  |

## Storage

| Requirement                                            | Choose        | Why                             |
| ------------------------------------------------------ | ------------- | ------------------------------- |
| Store images, logs, backups, documents, or media files | Blob Storage  | Object storage                  |
| Provide a shared folder using SMB/NFS                  | Azure Files   | Managed file shares             |
| Store a disk for an Azure VM                           | Managed Disk  | Persistent VM disk              |
| Store simple messages between application components   | Queue Storage | Basic queue messaging           |
| Store NoSQL key-value data                             | Table Storage | Simple structured NoSQL storage |
| Protect data inside one datacenter                     | LRS           | Locally redundant storage       |
| Protect data across zones in one region                | ZRS           | Zone-redundant storage          |
| Protect data by copying to paired region               | GRS           | Geo-redundant storage           |
| Store frequently accessed blob data                    | Hot tier      | Optimized for frequent access   |
| Store infrequently accessed blob data                  | Cool tier     | Lower storage cost              |
| Store rarely accessed blob data                        | Cold tier     | Lower storage cost for rare use |
| Store long-term archive data with delayed retrieval    | Archive tier  | Lowest storage cost             |

## Networking

| Requirement                                              | Choose                 | Why                            |
| -------------------------------------------------------- | ---------------------- | ------------------------------ |
| Create a private network in Azure                        | Virtual Network        | Core Azure networking boundary |
| Split a virtual network into smaller ranges              | Subnet                 | Network segmentation           |
| Allow or deny traffic to resources                       | Network Security Group | Traffic filtering              |
| Connect on-premises to Azure over encrypted internet     | VPN Gateway            | Encrypted tunnel               |
| Connect on-premises to Azure over private dedicated link | ExpressRoute           | Private connectivity           |
| Distribute TCP/UDP traffic                               | Azure Load Balancer    | Layer 4 load balancing         |
| Distribute HTTP/HTTPS web traffic                        | Application Gateway    | Layer 7 web traffic            |
| Host DNS records                                         | Azure DNS              | Domain name resolution         |
| Connect two Azure virtual networks privately             | VNet peering           | Private VNet-to-VNet routing   |

## Identity and Access

| Requirement                                           | Choose                           | Why                             |
| ----------------------------------------------------- | -------------------------------- | ------------------------------- |
| Cloud user sign-in and single sign-on                 | Microsoft Entra ID               | Cloud identity platform         |
| Require a second sign-in factor                       | Multifactor authentication       | Stronger identity protection    |
| Allow access only when conditions are met             | Conditional Access               | Policy-based access control     |
| Give a user permission to manage Azure resources      | RBAC                             | Authorization for Azure actions |
| Traditional domain join, LDAP, Kerberos, Group Policy | Active Directory Domain Services | Classic Windows domain services |
| Prove a user's identity                               | Authentication                   | Sign-in, password, MFA          |
| Decide what the signed-in user can do                 | Authorization                    | Roles and permissions           |

## Governance and Cost

| Requirement                                                  | Choose                    | Why                                   |
| ------------------------------------------------------------ | ------------------------- | ------------------------------------- |
| Enforce allowed locations, required tags, or allowed VM SKUs | Azure Policy              | Controls resource compliance          |
| Prevent accidental deletion                                  | Resource lock             | Protects resources from delete/update |
| Organize resources for cost reporting                        | Tags                      | Metadata for grouping/reporting       |
| Estimate planned Azure service cost                          | Pricing Calculator        | Before deployment                     |
| Compare on-premises cost with Azure                          | TCO Calculator            | Migration cost comparison             |
| Track real Azure spend                                       | Microsoft Cost Management | Actual usage and cost                 |
| Get cost/security/reliability recommendations                | Azure Advisor             | Best-practice recommendations         |

## Monitoring and Health

| Requirement                           | Choose               | Why                               |
| ------------------------------------- | -------------------- | --------------------------------- |
| Collect metrics and logs              | Azure Monitor        | Telemetry platform                |
| Analyze application performance       | Application Insights | App monitoring                    |
| Query logs                            | Log Analytics        | Log workspace and queries         |
| See personalized Azure service issues | Azure Service Health | Tenant-specific service incidents |
| See public Azure service status       | Azure Status         | Public status page                |
| Check one resource's health           | Resource Health      | Resource-level health             |

## Security and Compliance

| Requirement                                   | Choose                       | Why                                |
| --------------------------------------------- | ---------------------------- | ---------------------------------- |
| Improve cloud security posture                | Microsoft Defender for Cloud | Secure score and recommendations   |
| View regulatory compliance posture            | Defender for Cloud / Purview | Compliance visibility              |
| Discover and classify data                    | Microsoft Purview            | Data governance                    |
| Store secrets, keys, and certificates         | Azure Key Vault              | Secret management                  |
| Review Microsoft compliance and audit reports | Service Trust Portal         | Trust and compliance documentation |
| Find Microsoft and partner cloud solutions    | Azure Marketplace            | Marketplace catalog                |

## Quick Decision Rules

- If the question says "who can do this", think RBAC.
- If the question says "what is allowed", think Azure Policy.
- If the question says "prevent deletion", think resource lock.
- If the question says "before moving to Azure", think TCO Calculator.
- If the question says "estimate a planned Azure service", think Pricing Calculator.
- If the question says "actual current spend", think Cost Management.
- If the question says "logs, metrics, alerts", think Azure Monitor.
- If the question says "recommendations", think Azure Advisor.
- If the question says "private dedicated connection", think ExpressRoute.
- If the question says "encrypted connection over internet", think VPN Gateway.
- If the question says "long-term rarely accessed blob data", think Archive tier.
- If the question says "prove who the user is", think authentication.
- If the question says "what the user can do", think authorization.
