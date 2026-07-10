# 01 - Describe Cloud Concepts

This domain explains why cloud computing exists, how cloud services are consumed, and how to compare cloud models. AZ-900 questions in this area are usually concept-based and often test wording differences.

## Mental model

Think of cloud computing as renting reliable, secure, globally available IT building blocks instead of buying and maintaining everything yourself. The exam usually tests whether you can identify the right cloud benefit or service model from a short business scenario.

| Scenario keyword                      | Likely concept                  |
| ------------------------------------- | ------------------------------- |
| Avoid buying servers                  | OpEx / consumption-based        |
| Add capacity during seasonal demand   | Scalability                     |
| Automatically add/remove capacity     | Elasticity                      |
| Keep app running during failures      | High availability               |
| Recover after an outage               | Reliability / disaster recovery |
| Microsoft manages the finished app    | SaaS                            |
| Customer manages the operating system | IaaS                            |

## What you must know

Cloud computing is the delivery of compute, storage, networking, databases, analytics, security, and other IT services over the internet. Instead of buying and maintaining physical servers, organizations rent capacity from a cloud provider and pay for what they use.

Azure is Microsoft's cloud platform. For AZ-900, you do not need to design complex solutions, but you must understand the language Azure uses: regions, elasticity, availability, scalability, service models, deployment models, and shared responsibility.

## Exam-ready summary

| Learn deeply                                                              | Memorize clearly                                                        |
| ------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| Why organizations move from datacenters to cloud                          | CapEx means upfront purchase; OpEx means ongoing usage cost             |
| How cloud changes responsibility between customer and provider            | IaaS, PaaS, and SaaS responsibility order                               |
| Why scaling, elasticity, high availability, and reliability are different | Scalability changes capacity; elasticity changes capacity automatically |
| Why hybrid cloud is common in real companies                              | Public, private, and hybrid deployment models                           |

If you only remember one idea from this domain, remember this: cloud gives flexible access to IT resources, but the customer still has responsibilities.

## CapEx vs OpEx

| Term  | Meaning                                                                 | Example                                                               |
| ----- | ----------------------------------------------------------------------- | --------------------------------------------------------------------- |
| CapEx | Capital expenditure. Large upfront purchase that depreciates over time. | Buying servers, storage arrays, networking hardware, datacenter space |
| OpEx  | Operational expenditure. Ongoing cost based on usage.                   | Paying monthly for Azure VMs, storage, databases, bandwidth           |

Cloud usually shifts spending from CapEx to OpEx. This is one of the biggest business reasons organizations move to cloud.

## Consumption-based model

The consumption-based model means you pay only for what you consume.

Key ideas:

- No large upfront hardware purchase is required.
- You can increase or decrease resources as demand changes.
- You can stop paying for resources when you delete or shut them down.
- You should monitor usage because unused resources can still create cost.

Common exam wording:

| If the question says...          | Think...                  |
| -------------------------------- | ------------------------- |
| Pay only for what you use        | Consumption-based pricing |
| Avoid buying datacenter hardware | Move from CapEx to OpEx   |
| Scale down after demand drops    | Elasticity                |
| Estimate planned Azure costs     | Pricing Calculator        |

## Cloud benefits

### High availability

High availability means keeping a service running even when part of the system fails. In Azure, high availability can involve availability zones, redundant storage, load balancing, and service-level agreements.

### Scalability

Scalability means the ability to increase or decrease resources.

| Type               | Meaning                                             | Example                                        |
| ------------------ | --------------------------------------------------- | ---------------------------------------------- |
| Vertical scaling   | Scale up or down by changing the size of a resource | Move a VM from 2 CPUs to 4 CPUs                |
| Horizontal scaling | Scale out or in by adding/removing instances        | Add more web server VMs behind a load balancer |

### Elasticity

Elasticity is automatic scaling based on real-time demand. It is closely related to scalability, but the keyword is automatic adjustment.

Example: an e-commerce site automatically adds more instances during a sale and removes them afterward.

### Reliability

Reliability means a system can recover from failures and continue operating. It includes backup, disaster recovery, replication, and resilient architecture.

### Predictability

Predictability has two sides:

- Performance predictability: consistent application performance
- Cost predictability: understanding and forecasting cloud spend

### Manageability

Manageability also has two sides:

- Management of the cloud: the tools you use to manage cloud resources, such as templates, automation, autoscaling, self-healing based on health checks, and monitoring with alerts
- Management in the cloud: how you interact with those tools, such as the web portal, command line, APIs, and PowerShell

Exam wording hint: "automatically scale, redeploy from a template, or get alerted on health" points to management of the cloud; "use the portal, CLI, or scripts" points to management in the cloud.

### Security and governance

Cloud providers secure the physical datacenters and offer security tools. Customers still need to configure access, protect data, monitor threats, and follow governance standards.

## Exam keywords to recognize

| Keyword in question              | Think of                       |
| -------------------------------- | ------------------------------ |
| "No upfront hardware purchase"   | CapEx to OpEx                  |
| "Pay only while resources run"   | Consumption-based pricing      |
| "Scale automatically"            | Elasticity                     |
| "Add more servers"               | Horizontal scaling / scale out |
| "Increase VM CPU or memory"      | Vertical scaling / scale up    |
| "Provider hosts the application" | SaaS                           |
| "Customer controls the OS"       | IaaS                           |
| "No server management"           | PaaS or serverless             |

## Cloud service models

| Model | You manage                                 | Provider manages                             | Example                               |
| ----- | ------------------------------------------ | -------------------------------------------- | ------------------------------------- |
| IaaS  | OS, runtime, apps, data                    | Physical hosts, networking, storage hardware | Azure Virtual Machines                |
| PaaS  | Apps and data                              | OS, runtime, platform, infrastructure        | Azure App Service, Azure SQL Database |
| SaaS  | Usually just your data and access settings | Application and everything underneath        | Microsoft 365, Dynamics 365           |

Memory hook:

- IaaS gives the most control.
- PaaS reduces infrastructure management.
- SaaS gives the least management responsibility.

## Cloud deployment models

| Model         | Meaning                                                                        |
| ------------- | ------------------------------------------------------------------------------ |
| Public cloud  | Services delivered over the public internet and shared provider infrastructure |
| Private cloud | Cloud-like environment dedicated to one organization                           |
| Hybrid cloud  | Combines public and private/on-premises environments                           |

Most real organizations are hybrid for a long time because they still have existing datacenters, legacy apps, or regulatory constraints.

## Shared responsibility model

The shared responsibility model defines what the cloud provider manages and what the customer manages.

| Responsibility                | Usually Microsoft | Usually customer |
| ----------------------------- | ----------------- | ---------------- |
| Physical datacenter security  | Yes               | No               |
| Physical servers and cooling  | Yes               | No               |
| User accounts and permissions | No                | Yes              |
| Data                          | No                | Yes              |
| Application configuration     | No                | Yes              |
| OS patching on Azure VMs      | No                | Yes              |
| OS patching on PaaS services  | Yes               | Mostly no        |

Exam tip: the higher you go from IaaS to SaaS, the less the customer manages.

## Common confusions

| Confusion                              | Correct idea                                                                          |
| -------------------------------------- | ------------------------------------------------------------------------------------- |
| Scalability vs elasticity              | Scalability is capacity change; elasticity is automatic capacity change               |
| High availability vs disaster recovery | HA keeps services running during failure; DR restores service after larger disruption |
| IaaS vs PaaS                           | IaaS includes OS management; PaaS abstracts OS/runtime management                     |
| Public cloud vs hybrid cloud           | Hybrid includes on-prem/private plus public cloud                                     |

## Exam traps

| Trap                                      | Why people miss it                                                                                                                  |
| ----------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| "Cloud is always cheaper"                 | Cloud can be cheaper, but only when resources are managed and optimized. The exam usually says cost can be reduced, not guaranteed. |
| "SaaS means no responsibility"            | Customers still manage users, data, access, and configuration choices.                                                              |
| "Elasticity and scalability are the same" | Elasticity emphasizes automatic response to demand.                                                                                 |
| "High availability means backup"          | Backup helps recovery. High availability is about keeping service available during failure.                                         |

## Fast elimination method

When two answers both look possible, eliminate by keyword:

| Keyword              | Usually eliminates                                                          |
| -------------------- | --------------------------------------------------------------------------- |
| Automatic            | Eliminates basic scalability; points to elasticity                          |
| Full OS control      | Eliminates PaaS and SaaS; points to IaaS                                    |
| Finished application | Eliminates IaaS and PaaS; points to SaaS                                    |
| Recover after outage | Eliminates high availability alone; points to reliability/disaster recovery |
| No upfront hardware  | Eliminates CapEx; points to OpEx/consumption-based                          |

## Real-world example

A company hosts a seasonal ticketing website. Traffic is low most of the year but spikes during event launches. In a traditional datacenter, the company must buy enough hardware for peak usage. In Azure, the company can scale out during peak demand and scale back in afterward. This improves elasticity and cost efficiency.

## Mini scenarios

| Scenario                                                                                      | Best answer                    |
| --------------------------------------------------------------------------------------------- | ------------------------------ |
| A startup wants to avoid buying servers and pay monthly for resources it uses.                | OpEx / consumption-based model |
| A retailer wants the website to add more instances during Black Friday and remove them later. | Elasticity                     |
| A company wants full control over the operating system and installed software.                | IaaS                           |
| A department wants email and collaboration without managing servers.                          | SaaS                           |
| A developer wants to deploy code without patching the server OS.                              | PaaS or serverless             |

## Check yourself

1. Which model gives the customer the most control: IaaS, PaaS, or SaaS?
2. What is the difference between vertical and horizontal scaling?
3. Which cloud benefit is most closely tied to automatic scaling?
4. Who is responsible for physical datacenter security in Azure?
5. Why does cloud usually move spending from CapEx to OpEx?

## Answer guide

1. IaaS.
2. Vertical scaling changes the size of one resource; horizontal scaling adds or removes instances.
3. Elasticity.
4. Microsoft.
5. You rent and consume services instead of buying physical infrastructure upfront.

