# AZ-900 Common Confusions

Many AZ-900 questions are easy once you separate similar terms. Use this file after your first practice test and before the final review.

## Governance and Access

| This          | Not this     | How to remember                                     |
| ------------- | ------------ | --------------------------------------------------- |
| Azure Policy  | RBAC         | Policy controls what can be deployed or configured. |
| RBAC          | Azure Policy | RBAC controls who can perform actions.              |
| Resource lock | Azure Policy | Locks prevent deletion or modification.             |
| Tags          | RBAC         | Tags organize/report; they do not grant access.     |

## Availability and Resilience

| This              | Not this          | How to remember                                 |
| ----------------- | ----------------- | ----------------------------------------------- |
| Region            | Availability Zone | A region is a geographic Azure location.        |
| Availability Zone | Region Pair       | A zone is inside a region.                      |
| Region Pair       | Availability Zone | A region pair is two separate regions.          |
| High availability | Backup            | HA keeps service running; backup restores data. |
| Disaster recovery | High availability | DR focuses on recovery after major disruption.  |

## Scaling

| This        | Not this       | How to remember                             |
| ----------- | -------------- | ------------------------------------------- |
| Scale up    | Scale out      | Scale up means make one resource bigger.    |
| Scale out   | Scale up       | Scale out means add more instances.         |
| Scalability | Elasticity     | Scalability is ability to change capacity.  |
| Elasticity  | Manual scaling | Elasticity is automatic response to demand. |

## Service Models

| This       | Not this          | How to remember                                 |
| ---------- | ----------------- | ----------------------------------------------- |
| IaaS       | PaaS              | Customer manages OS and apps.                   |
| PaaS       | SaaS              | Customer manages app and data, not OS platform. |
| SaaS       | IaaS              | Customer uses finished software.                |
| Serverless | No responsibility | You still manage code, data, and access.        |

## Cost Tools

| This               | Not this           | How to remember                                    |
| ------------------ | ------------------ | -------------------------------------------------- |
| Pricing Calculator | TCO Calculator     | Estimate planned Azure services.                   |
| TCO Calculator     | Pricing Calculator | Compare on-premises cost with Azure migration.     |
| Cost Management    | Pricing Calculator | Analyze actual Azure spend.                        |
| Budgets            | Resource locks     | Budgets alert on spend; they do not stop deletion. |

## Monitoring and Health

| This            | Not this       | How to remember                                   |
| --------------- | -------------- | ------------------------------------------------- |
| Azure Monitor   | Azure Advisor  | Monitor collects metrics, logs, and alerts.       |
| Azure Advisor   | Azure Monitor  | Advisor recommends improvements.                  |
| Azure Status    | Service Health | Azure Status is public/global.                    |
| Service Health  | Azure Status   | Service Health is personalized to your resources. |
| Resource Health | Service Health | Resource Health is about one specific resource.   |

## Networking

| This                | Not this            | How to remember                                  |
| ------------------- | ------------------- | ------------------------------------------------ |
| VPN Gateway         | ExpressRoute        | VPN uses encrypted internet connectivity.        |
| ExpressRoute        | VPN Gateway         | ExpressRoute is private dedicated connectivity.  |
| Load Balancer       | Application Gateway | Load Balancer works at Layer 4.                  |
| Application Gateway | Load Balancer       | Application Gateway works at Layer 7 HTTP/HTTPS. |

## Identity

| This                       | Not this           | How to remember                                 |
| -------------------------- | ------------------ | ----------------------------------------------- |
| Microsoft Entra ID         | AD DS              | Cloud identity, SSO, Conditional Access.        |
| AD DS                      | Microsoft Entra ID | Domain join, Kerberos, LDAP, Group Policy.      |
| Multifactor authentication | RBAC               | MFA verifies identity; RBAC grants permissions. |

## Last-Minute Rule

If two answers both sound possible, ask:

1. Is the question about **permission**? Choose RBAC.
2. Is it about **allowed configuration**? Choose Azure Policy.
3. Is it about **cost estimate before deployment**? Choose Pricing Calculator.
4. Is it about **actual spend**? Choose Cost Management.
5. Is it about **logs/metrics/alerts**? Choose Azure Monitor.
6. Is it about **recommendations**? Choose Azure Advisor.
