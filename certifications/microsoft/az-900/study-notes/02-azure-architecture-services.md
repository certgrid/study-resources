# 02 - Describe Azure Architecture and Services

This domain covers Azure's global structure and the major service families. For AZ-900, you do not need deep configuration knowledge. You need to recognize which Azure component or service fits a scenario.

## Mental Model

Azure architecture questions usually ask one of two things:

1. Where does this resource live in Azure?
2. Which Azure service should be used for this requirement?

Learn the hierarchy first, then map common workload needs to the right service.

| If the scenario needs...               | Think of               |
| -------------------------------------- | ---------------------- |
| Billing and access boundary            | Subscription           |
| Container for related resources        | Resource group         |
| Governance across many subscriptions   | Management group       |
| Protection from datacenter failure     | Availability zone      |
| Recovery planning across two regions   | Region pair            |
| Full operating system control          | Azure Virtual Machines |
| Web app without server management      | Azure App Service      |
| Object storage for images/logs/backups | Blob Storage           |
| Cloud identity and single sign-on      | Microsoft Entra ID     |

## Azure Global Infrastructure

Azure is organized into geographies, regions, availability zones, and datacenters.

| Term              | Meaning                                                      |
| ----------------- | ------------------------------------------------------------ |
| Geography         | Large market area, often tied to data residency needs        |
| Region            | Geographic area containing Azure datacenters                 |
| Region pair       | Two regions in the same geography used for recovery planning |
| Availability zone | Physically separate datacenter location inside a region      |

## Regions

An Azure region is a geographic area containing one or more datacenters connected by low-latency networking.

Use regions to:

- Place workloads near users
- Meet data residency requirements
- Improve performance
- Support disaster recovery planning

## Availability Zones

Availability zones are physically separate locations within a region. Each zone has independent power, cooling, and networking.

Use availability zones when you need protection from a datacenter-level failure within the same region.

Example: deploy multiple VM instances across zones behind a load balancer.

## Region Pairs

Azure pairs many regions within the same geography. Region pairs help with disaster recovery planning because Azure can sequence platform updates and prioritize recovery across paired regions.

Do not confuse:

| Concept           | Scope                                            |
| ----------------- | ------------------------------------------------ |
| Availability zone | Separate datacenter location inside one region   |
| Region pair       | Two separate Azure regions in the same geography |

## Azure Management Hierarchy

Azure resources are organized like this:

```text
Management Group
  Subscription
    Resource Group
      Resource
```

| Scope            | What it is best for                                                    |
| ---------------- | ---------------------------------------------------------------------- |
| Management group | Organizing many subscriptions and applying governance broadly          |
| Subscription     | Billing, access boundary, quotas, and environment separation           |
| Resource group   | Lifecycle container for related resources                              |
| Resource         | Individual service instance such as a VM, storage account, or database |

Important exam points:

- A resource belongs to one resource group at a time.
- Deleting a resource group deletes the resources inside it.
- Role assignments and policies can be inherited from higher scopes.
- Subscriptions are commonly used to separate billing, environments, or business units.

## Core Compute Services

| Service                    | Best for                                           |
| -------------------------- | -------------------------------------------------- |
| Azure Virtual Machines     | Full control over OS and installed software        |
| Virtual Machine Scale Sets | Many identical VMs that scale together             |
| Azure App Service          | Hosting web apps and APIs without managing servers |
| Azure Functions            | Event-driven serverless code                       |
| Azure Container Instances  | Running containers without orchestration           |
| Azure Kubernetes Service   | Managed Kubernetes for orchestrated containers     |

## Compute Decision Table

| Requirement                                 | Best fit                   |
| ------------------------------------------- | -------------------------- |
| Lift-and-shift an existing server           | Azure Virtual Machines     |
| Automatically scale identical VMs           | Virtual Machine Scale Sets |
| Host a web app/API without managing servers | Azure App Service          |
| Run code in response to an event            | Azure Functions            |
| Run a container quickly without Kubernetes  | Azure Container Instances  |
| Manage many containers with orchestration   | Azure Kubernetes Service   |

## Core Networking Services

| Service                | Purpose                                         |
| ---------------------- | ----------------------------------------------- |
| Virtual Network        | Private network in Azure                        |
| Subnet                 | Segment inside a virtual network                |
| Network Security Group | Allow or deny inbound and outbound traffic      |
| VPN Gateway            | Encrypted connection over the internet          |
| ExpressRoute           | Private dedicated connection to Microsoft cloud |
| Azure DNS              | Host DNS domains                                |
| Azure Load Balancer    | Distribute Layer 4 TCP/UDP traffic              |
| Application Gateway    | Distribute Layer 7 HTTP/HTTPS web traffic       |

## Networking Decision Table

| Requirement                                                      | Best fit               |
| ---------------------------------------------------------------- | ---------------------- |
| Create a private network in Azure                                | Virtual Network        |
| Divide a virtual network into smaller ranges                     | Subnet                 |
| Filter traffic to or from resources                              | Network Security Group |
| Connect on-premises to Azure over encrypted internet             | VPN Gateway            |
| Connect on-premises to Azure over private dedicated connectivity | ExpressRoute           |
| Distribute TCP/UDP traffic                                       | Azure Load Balancer    |
| Distribute HTTP/HTTPS web traffic                                | Application Gateway    |

## Core Storage Services

| Storage type  | Best for                                               |
| ------------- | ------------------------------------------------------ |
| Blob Storage  | Unstructured object data such as images, logs, backups |
| Azure Files   | Managed file shares using SMB/NFS                      |
| Queue Storage | Simple message storage                                 |
| Table Storage | NoSQL key-value data                                   |
| Managed Disks | Persistent disks for Azure VMs                         |

## Storage Redundancy

| Redundancy | Meaning                                      |
| ---------- | -------------------------------------------- |
| LRS        | Three copies in one datacenter               |
| ZRS        | Copies across availability zones in a region |
| GRS        | Copies to a paired region                    |
| GZRS       | Zone redundancy plus geo-replication         |

Exam tip: if a question mentions protection from a regional outage, look for geo-redundant options such as GRS or GZRS.

## Database Services

| Service                       | Use case                            |
| ----------------------------- | ----------------------------------- |
| Azure SQL Database            | Managed relational database         |
| Azure Cosmos DB               | Globally distributed NoSQL database |
| Azure Database for PostgreSQL | Managed PostgreSQL                  |
| Azure Database for MySQL      | Managed MySQL                       |

## Identity Services

Microsoft Entra ID is Azure's cloud identity and access management service.

It is used for:

- User sign-in
- Application access
- Conditional Access
- Multifactor authentication
- Single sign-on

Do not confuse Microsoft Entra ID with traditional Active Directory Domain Services. Entra ID is cloud identity. AD DS is traditional domain services for domain join, Kerberos, LDAP, and Group Policy.

## Common Confusions

| This                | Remember                                     |
| ------------------- | -------------------------------------------- |
| VPN Gateway         | Encrypted tunnel over the public internet    |
| ExpressRoute        | Private dedicated connection                 |
| Load Balancer       | Layer 4 TCP/UDP traffic                      |
| Application Gateway | Layer 7 HTTP/HTTPS traffic                   |
| Blob Storage        | Object storage                               |
| Azure Files         | Managed file shares                          |
| Availability Zone   | Separate datacenter location inside a region |
| Region Pair         | Two regions for recovery planning            |

## Exam Traps

| Trap                                                      | Correct thinking                                                                                  |
| --------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| "A resource group is a billing boundary"                  | A subscription is the billing boundary. A resource group is a lifecycle container.                |
| "Availability zones are the same as regions"              | Zones are inside a region. Regions are separate geographic locations.                             |
| "Blob Storage is for file shares"                         | Blob Storage is object storage. Azure Files provides managed file shares.                         |
| "ExpressRoute uses the public internet"                   | ExpressRoute is private dedicated connectivity. VPN Gateway uses encrypted internet connectivity. |
| "Azure SQL Database requires OS patching by the customer" | Azure SQL Database is PaaS, so Microsoft manages the platform and OS.                             |

## Mini Scenarios

| Scenario                                                                   | Best answer        |
| -------------------------------------------------------------------------- | ------------------ |
| A company wants to host a simple web app without managing Windows updates. | Azure App Service  |
| A team needs a private network for VMs in Azure.                           | Virtual Network    |
| A backup process stores large unstructured files.                          | Blob Storage       |
| An enterprise needs private connectivity from its datacenter to Azure.     | ExpressRoute       |
| A workload must survive a datacenter failure inside one Azure region.      | Availability Zones |

## Check Yourself

1. What is the correct Azure hierarchy from largest to smallest?
2. Which service hosts a web app without managing servers?
3. Which storage service is best for images, backups, and logs?
4. What is the difference between VPN Gateway and ExpressRoute?
5. What protects against a datacenter failure inside a region?

## Answer Guide

1. Management group, subscription, resource group, resource.
2. Azure App Service.
3. Blob Storage.
4. VPN Gateway uses encrypted internet connectivity; ExpressRoute uses private dedicated connectivity.
5. Availability Zones.
