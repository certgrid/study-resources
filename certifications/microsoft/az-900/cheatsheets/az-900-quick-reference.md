# AZ-900 Quick Reference

Use this on the final day. It is intentionally compact and exam-focused.

## One-Page Mental Model

| Question asks about...        | Think of...                                              |
| ----------------------------- | -------------------------------------------------------- |
| Cloud value/business benefit  | CapEx to OpEx, consumption, scalability, elasticity      |
| Who manages what              | Shared responsibility model                              |
| Where resources live          | Management group, subscription, resource group, resource |
| Azure datacenter resilience   | Region, availability zone, region pair                   |
| Which service to choose       | Compute, storage, networking, database, identity         |
| Cost or governance            | Calculator, Cost Management, Policy, RBAC, locks         |
| Monitoring or recommendations | Monitor, Advisor, Service Health                         |

## Cloud Basics

| Concept           | Remember                             |
| ----------------- | ------------------------------------ |
| CapEx             | Upfront hardware/datacenter purchase |
| OpEx              | Ongoing operational spend            |
| Consumption-based | Pay only for what you use            |
| High availability | Keep service running during failures |
| Scalability       | Increase or decrease capacity        |
| Elasticity        | Automatic scaling based on demand    |
| Reliability       | Recover from failure                 |

## Service Models

| Model | Example                         | Customer manages             |
| ----- | ------------------------------- | ---------------------------- |
| IaaS  | Azure Virtual Machines          | OS, apps, data               |
| PaaS  | App Service, Azure SQL Database | Apps, data                   |
| SaaS  | Microsoft 365                   | Users, data, access settings |

## Azure Hierarchy

```text
Management Groups
  Subscriptions
    Resource Groups
      Resources
```

| Scope            | Remember                         |
| ---------------- | -------------------------------- |
| Management group | Governance across subscriptions  |
| Subscription     | Billing, quotas, access boundary |
| Resource group   | Lifecycle container              |
| Resource         | Actual Azure service instance    |

## Global Infrastructure

| Concept           | Remember                                     |
| ----------------- | -------------------------------------------- |
| Region            | Geographic Azure location                    |
| Availability Zone | Separate datacenter location inside a region |
| Region Pair       | Two regions used for recovery planning       |
| Geography         | Large area tied to residency/compliance      |

## Core Services

| Need                         | Service                   |
| ---------------------------- | ------------------------- |
| Full OS control              | Azure Virtual Machines    |
| Host web app                 | Azure App Service         |
| Event-driven code            | Azure Functions           |
| Simple container             | Azure Container Instances |
| Kubernetes                   | Azure Kubernetes Service  |
| Cloud-hosted Windows desktop | Azure Virtual Desktop     |
| Object storage               | Blob Storage              |
| File share                   | Azure Files               |
| NoSQL global database        | Azure Cosmos DB           |
| Managed relational database  | Azure SQL Database        |
| Cloud identity               | Microsoft Entra ID        |

## Networking

| Service                | Purpose                            |
| ---------------------- | ---------------------------------- |
| Virtual Network        | Private network in Azure           |
| Subnet                 | Segment of a virtual network       |
| Network Security Group | Allow/deny network traffic         |
| VPN Gateway            | Encrypted connection over internet |
| ExpressRoute           | Private dedicated connection       |
| Load Balancer          | Layer 4 traffic distribution       |
| Application Gateway    | Layer 7 web traffic distribution   |
| VNet peering           | Private VNet-to-VNet connectivity  |

## Storage Tiers

| Tier    | Use when...                                   |
| ------- | --------------------------------------------- |
| Hot     | Data is accessed frequently                   |
| Cool    | Data is accessed infrequently                 |
| Cold    | Data is rarely accessed                       |
| Archive | Data is kept long term and retrieval can wait |

## Governance and Management

| Need                            | Tool               |
| ------------------------------- | ------------------ |
| Estimate Azure cost             | Pricing Calculator |
| Compare on-prem vs Azure cost   | TCO Calculator     |
| Track actual cloud spend        | Cost Management    |
| Enforce standards               | Azure Policy       |
| Assign permissions              | RBAC               |
| Prevent deletion                | Resource locks     |
| Monitor metrics/logs            | Azure Monitor      |
| Get recommendations             | Azure Advisor      |
| Security posture                | Defender for Cloud |
| Personalized service issue view | Service Health     |

## Security Basics

| Concept              | Remember                                      |
| -------------------- | --------------------------------------------- |
| Zero Trust           | Verify explicitly; do not trust by default    |
| Defense-in-depth     | Use multiple layers of security               |
| Authentication       | Proves who someone is                         |
| Authorization        | Decides what someone can do                   |
| Service Trust Portal | Compliance, audit, privacy, and trust reports |
| Azure Marketplace    | Microsoft and partner solutions catalog       |

## Final Reminders

- Policy answers "what is allowed?"
- RBAC answers "who can do it?"
- Locks protect resources from deletion or changes.
- Tags help with cost reporting and organization.
- Entra ID is cloud identity.
- AD DS is traditional domain services.
- Monitor collects telemetry.
- Advisor recommends improvements.
- Service Health is personalized.
- Azure Status is public.
- Authentication happens before authorization.
- Archive tier is not for data that must be accessed immediately.
