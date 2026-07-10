# 03 - Describe Azure Management and Governance

This domain covers cost management, governance, monitoring, security posture, compliance, and management tools. AZ-900 often gives you a short scenario and asks which Azure tool solves it.

## Mental Model

Think of this domain as the "operate Azure responsibly" domain.

| If the scenario asks about...              | Think of                     |
| ------------------------------------------ | ---------------------------- |
| Estimating future Azure cost               | Pricing Calculator           |
| Comparing datacenter cost with Azure       | TCO Calculator               |
| Tracking actual spend                      | Microsoft Cost Management    |
| Enforcing allowed regions or required tags | Azure Policy                 |
| Granting a user permission                 | RBAC                         |
| Preventing accidental deletion             | Resource locks               |
| Collecting metrics, logs, and alerts       | Azure Monitor                |
| Getting best-practice recommendations      | Azure Advisor                |
| Checking personalized Azure outages        | Azure Service Health         |
| Improving security posture                 | Microsoft Defender for Cloud |

## Exam-ready summary

| Learn deeply                                                | Memorize clearly                                                |
| ----------------------------------------------------------- | --------------------------------------------------------------- |
| How cost tools fit before and after deployment              | Pricing Calculator, TCO Calculator, Cost Management             |
| How governance tools differ from each other                 | Policy, RBAC, locks, tags                                       |
| How monitoring, recommendations, and health tools differ    | Monitor, Advisor, Service Health, Resource Health, Azure Status |
| Why security posture is different from identity permissions | Defender for Cloud improves posture; RBAC grants access         |

If you only remember one idea from this domain, remember this: governance answers depend on whether the question asks who, what, protect, organize, monitor, or recommend.

## Cost Tools

| Tool                      | Purpose                                                                      |
| ------------------------- | ---------------------------------------------------------------------------- |
| Pricing Calculator        | Estimate the cost of planned Azure services                                  |
| TCO Calculator            | Compare on-premises cost with Azure migration cost                           |
| Microsoft Cost Management | Monitor and analyze actual Azure spend                                       |
| Budgets                   | Track spend and trigger alerts                                               |
| Azure Advisor             | Recommendations for cost, reliability, security, performance, and operations |

Memory hook:

- Pricing Calculator: before deployment
- Cost Management: after deployment
- TCO Calculator: compare datacenter vs Azure
- Advisor: recommendations

## Factors That Affect Cost

Cost can change based on:

- Resource type
- Resource size or SKU
- Region
- Usage time
- Storage capacity
- Data transfer out of Azure
- Reserved capacity or savings plans
- Azure Hybrid Benefit

Inbound data transfer is usually free. Outbound data transfer can cost money.

## Cost Optimization

| Method               | Why it helps                                                 |
| -------------------- | ------------------------------------------------------------ |
| Shut down unused VMs | Stops compute charges when not needed                        |
| Right-size resources | Avoids paying for oversized resources                        |
| Reserved capacity    | Reduces cost for predictable long-running workloads          |
| Azure Hybrid Benefit | Uses eligible existing Windows Server or SQL Server licenses |
| Budgets and alerts   | Helps detect unexpected spend early                          |
| Tags                 | Helps allocate cost to teams, apps, or environments          |

## Tags

Tags are name/value pairs used to organize resources.

| Tag name    | Value         |
| ----------- | ------------- |
| Environment | Production    |
| CostCenter  | Finance       |
| Owner       | PlatformTeam  |
| Application | StudentPortal |

Tags help with organization, cost reporting, and automation. Tags are not automatically inherited from a resource group to resources unless configured through policy or automation.

## Azure Policy

Azure Policy enforces rules for resources.

Use Azure Policy to:

- Restrict allowed regions
- Require specific tags
- Enforce allowed VM SKUs
- Audit non-compliant resources
- Deny non-compliant deployments

Policy controls what can be deployed or how resources must be configured.

## RBAC

Role-based access control controls who can do what.

| Role                      | Meaning                                    |
| ------------------------- | ------------------------------------------ |
| Owner                     | Full access, including assigning access    |
| Contributor               | Manage resources, but cannot assign access |
| Reader                    | View resources only                        |
| User Access Administrator | Manage user access                         |

Exam shortcut:

- Azure Policy = what is allowed
- RBAC = who can perform actions

## Resource Locks

Resource locks prevent accidental deletion or modification.

| Lock     | Effect                                                  |
| -------- | ------------------------------------------------------- |
| Delete   | Authorized users can read and modify, but cannot delete |
| ReadOnly | Authorized users can read, but cannot update or delete  |

Locks are useful for protecting critical resources.

## Azure Monitor

Azure Monitor collects and analyzes telemetry from Azure resources.

It includes:

- Metrics
- Logs
- Alerts
- Application Insights
- Log Analytics

Use Azure Monitor when the question asks about performance, logs, metrics, alerting, or visibility.

## Service Health vs Azure Status vs Resource Health

| Tool            | Scope                                                      |
| --------------- | ---------------------------------------------------------- |
| Azure Status    | Public global status page for Azure services               |
| Service Health  | Personalized view of Azure issues affecting your resources |
| Resource Health | Health of a specific Azure resource                        |

## Microsoft Defender for Cloud

Microsoft Defender for Cloud helps improve cloud security posture and protect workloads.

It provides:

- Secure score
- Recommendations
- Regulatory compliance dashboard
- Threat protection capabilities
- Security alerts

For AZ-900, think of Defender for Cloud as security posture and workload protection.

## Microsoft Purview

Microsoft Purview is used for data governance, compliance, risk, and information protection.

It can help with:

- Data discovery
- Classification
- Compliance management
- Information protection
- Audit and risk management

## Azure Management Tools

| Tool                  | Best for                                                     |
| --------------------- | ------------------------------------------------------------ |
| Azure Portal          | Web-based management                                         |
| Azure PowerShell      | Automation using PowerShell                                  |
| Azure CLI             | Cross-platform command-line automation                       |
| Azure Cloud Shell     | Browser-based shell with Azure tools preinstalled            |
| Azure Arc             | Manage resources across Azure, on-premises, and other clouds |
| ARM templates / Bicep | Infrastructure as code                                       |

## Common Confusions

| Confusion                            | Correct idea                                                           |
| ------------------------------------ | ---------------------------------------------------------------------- |
| Policy vs RBAC                       | Policy controls allowed configurations; RBAC controls user permissions |
| Lock vs Policy                       | Lock prevents deletion/modification; policy enforces standards         |
| Monitor vs Advisor                   | Monitor collects telemetry; Advisor gives recommendations              |
| Service Health vs Azure Status       | Service Health is personalized; Azure Status is public                 |
| Pricing Calculator vs TCO Calculator | Pricing estimates Azure services; TCO compares on-premises vs Azure    |

## Exam Traps

| Trap                                              | Correct thinking                                     |
| ------------------------------------------------- | ---------------------------------------------------- |
| "Use RBAC to force all resources into one region" | Use Azure Policy for allowed locations.              |
| "Use Policy to give a user read access"           | Use RBAC for permissions.                            |
| "Use Azure Status for personalized outage alerts" | Use Service Health for personalized service issues.  |
| "Use Advisor to collect logs"                     | Use Azure Monitor for logs and metrics.              |
| "Use tags to secure resources"                    | Tags organize and report; they do not secure access. |

## Fast elimination method

| Question wording                            | Usually points to    |
| ------------------------------------------- | -------------------- |
| Who can access or manage resources?         | RBAC                 |
| Which locations, SKUs, or tags are allowed? | Azure Policy         |
| Prevent accidental deletion                 | Resource lock        |
| Organize resources for reporting            | Tags                 |
| Estimate cost before deployment             | Pricing Calculator   |
| Compare datacenter cost with Azure          | TCO Calculator       |
| Track actual spend                          | Cost Management      |
| Collect logs, metrics, and alerts           | Azure Monitor        |
| Get optimization recommendations            | Azure Advisor        |
| Personalized service outage view            | Azure Service Health |

## Mini Scenarios

| Scenario                                                     | Best answer        |
| ------------------------------------------------------------ | ------------------ |
| Estimate the monthly cost of planned VMs before deployment.  | Pricing Calculator |
| Compare current datacenter costs to Azure migration costs.   | TCO Calculator     |
| Stop users from creating resources outside approved regions. | Azure Policy       |
| Give a helpdesk user read-only access to a subscription.     | RBAC Reader role   |
| Prevent a production resource group from being deleted.      | Delete lock        |
| Collect VM metrics and configure alerts.                     | Azure Monitor      |
| See recommendations to reduce cost and improve reliability.  | Azure Advisor      |

## Check Yourself

1. Which tool estimates costs before deployment?
2. Which tool compares on-premises costs with Azure?
3. Which feature prevents accidental deletion of a resource?
4. Which tool enforces allowed Azure regions?
5. Which tool shows personalized Azure service issues affecting your resources?

## Answer Guide

1. Pricing Calculator.
2. TCO Calculator.
3. Resource lock, specifically a Delete lock.
4. Azure Policy.
5. Azure Service Health.
