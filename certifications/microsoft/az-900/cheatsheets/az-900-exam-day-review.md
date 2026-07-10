# AZ-900 Exam-Day Review

Use this page in the final 30-45 minutes before the exam. It is intentionally short and focused on high-frequency decisions.

## The Exam Mindset

AZ-900 is a fundamentals exam. Most questions are not asking you to configure Azure. They are asking whether you can recognize the right concept, service category, or management tool from the wording.

When stuck, ask:

1. Is this about cloud benefits?
2. Is this about service model responsibility?
3. Is this about Azure hierarchy?
4. Is this about choosing a service?
5. Is this about governance, cost, monitoring, or security?

## Must-Know Pairs

| Pair                                   | Difference                                                      |
| -------------------------------------- | --------------------------------------------------------------- |
| CapEx vs OpEx                          | Buy upfront vs pay as you use                                   |
| Scalability vs elasticity              | Capacity can change vs capacity changes automatically           |
| High availability vs disaster recovery | Keep running during failure vs recover after disruption         |
| IaaS vs PaaS                           | Customer manages OS vs Microsoft manages platform/OS            |
| Region vs availability zone            | Geographic area vs separate datacenter location inside a region |
| Availability zone vs region pair       | Datacenter-level resilience vs regional recovery planning       |
| Subscription vs resource group         | Billing/access boundary vs lifecycle container                  |
| Azure Policy vs RBAC                   | What is allowed vs who can do actions                           |
| Resource lock vs Azure Policy          | Prevent deletion/update vs enforce standards                    |
| Pricing Calculator vs TCO Calculator   | Planned Azure estimate vs on-premises comparison                |
| Azure Monitor vs Azure Advisor         | Telemetry and alerts vs recommendations                         |
| Service Health vs Azure Status         | Personalized issues vs public status page                       |
| VPN Gateway vs ExpressRoute            | Encrypted internet tunnel vs private dedicated connectivity     |
| Blob Storage vs Azure Files            | Object storage vs managed file shares                           |

## Service Model Responsibility

| Model | Customer manages most | Microsoft manages most | Memory                            |
| ----- | --------------------- | ---------------------- | --------------------------------- |
| IaaS  | Yes                   | No                     | Most control, most responsibility |
| PaaS  | Some                  | Yes                    | Deploy apps, not servers          |
| SaaS  | Least                 | Most                   | Use the finished application      |

Exam shortcut: the higher you go from IaaS to SaaS, the less the customer manages.

## Azure Hierarchy

```text
Management Group
  Subscription
    Resource Group
      Resource
```

Memory:

- Management group: govern many subscriptions.
- Subscription: billing, access boundary, quotas.
- Resource group: lifecycle container.
- Resource: actual Azure service.

## Final Service Picker

| Keyword                              | Answer                 |
| ------------------------------------ | ---------------------- |
| Web app without OS patching          | Azure App Service      |
| Event-driven code                    | Azure Functions        |
| Full OS control                      | Azure Virtual Machines |
| Object data: images, logs, backups   | Blob Storage           |
| Shared file folder                   | Azure Files            |
| Private network                      | Virtual Network        |
| Traffic filtering                    | Network Security Group |
| Private dedicated hybrid connection  | ExpressRoute           |
| Encrypted internet hybrid connection | VPN Gateway            |
| Cloud identity and SSO               | Microsoft Entra ID     |
| Secrets and keys                     | Azure Key Vault        |
| Required tags or allowed regions     | Azure Policy           |
| Read-only access for a user          | RBAC Reader            |
| Prevent accidental deletion          | Delete lock            |
| Metrics, logs, alerts                | Azure Monitor          |
| Best-practice recommendations        | Azure Advisor          |
| Personalized Azure outage impact     | Azure Service Health   |

## Last-Minute Traps

| Trap wording                                | Better answer                                           |
| ------------------------------------------- | ------------------------------------------------------- |
| "Cloud is always cheaper"                   | Cloud can reduce cost, but only with good management    |
| "SaaS means customer has no responsibility" | Customer still manages users, data, and access settings |
| "Resource group is for billing"             | Subscription is the billing boundary                    |
| "Tags secure resources"                     | Tags organize and report; they do not secure            |
| "RBAC enforces allowed regions"             | Azure Policy enforces allowed regions                   |
| "Advisor collects logs"                     | Azure Monitor collects logs                             |
| "Azure Status is personalized"              | Service Health is personalized                          |

## Final Confidence Checklist

You are ready when you can explain these without looking:

- Why cloud shifts spending from CapEx to OpEx
- The difference between IaaS, PaaS, and SaaS
- What the customer still manages in cloud
- Region vs availability zone vs region pair
- Subscription vs resource group
- Blob Storage vs Azure Files
- VPN Gateway vs ExpressRoute
- Policy vs RBAC vs locks vs tags
- Pricing Calculator vs TCO Calculator vs Cost Management
- Monitor vs Advisor vs Service Health
