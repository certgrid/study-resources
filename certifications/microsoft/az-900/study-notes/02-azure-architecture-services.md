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

## Exam-ready summary

| Learn deeply                                                               | Memorize clearly                                                         |
| -------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| How Azure organizes resources from broad governance to individual services | Management group, subscription, resource group, resource                 |
| Which failure scope each resiliency feature handles                        | Zone is inside one region; region pair is two regions                    |
| Which compute service fits each workload style                             | VM, VM Scale Sets, App Service, Functions, ACI, AKS                      |
| Which storage service fits each data type                                  | Blob, Files, Queue, Table, Managed Disks                                 |
| Which network service fits each connectivity requirement                   | VNet, NSG, VPN Gateway, ExpressRoute, Load Balancer, Application Gateway |
| Which security wording points to which concept                             | Zero Trust, defense-in-depth, authentication, authorization              |

If you only remember one idea from this domain, remember this: AZ-900 service questions are usually matching questions disguised as scenarios.

## Azure Global Infrastructure

Azure is organized into geographies, regions, availability zones, and datacenters.

| Term              | Meaning                                                      |
| ----------------- | ------------------------------------------------------------ |
| Geography         | Large market area, often tied to data residency needs        |
| Region            | Geographic area containing Azure datacenters                 |
| Region pair       | Two regions in the same geography used for recovery planning |
| Availability zone | Physically separate datacenter location inside a region      |
| Sovereign region  | Isolated region for government or regulated workloads, e.g. Azure Government or Azure China |

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
| Azure Virtual Desktop      | Cloud-hosted Windows desktops and apps             |

## Compute Decision Table

| Requirement                                 | Best fit                   |
| ------------------------------------------- | -------------------------- |
| Lift-and-shift an existing server           | Azure Virtual Machines     |
| Automatically scale identical VMs           | Virtual Machine Scale Sets |
| Host a web app/API without managing servers | Azure App Service          |
| Run code in response to an event            | Azure Functions            |
| Run a container quickly without Kubernetes  | Azure Container Instances  |
| Manage many containers with orchestration   | Azure Kubernetes Service   |
| Deliver cloud-hosted Windows desktops/apps  | Azure Virtual Desktop      |

## VM Resiliency Options

For virtual machines, AZ-900 expects you to separate three similar-sounding options.

| Option                    | Protects against                                | How                                                            |
| ------------------------- | ----------------------------------------------- | -------------------------------------------------------------- |
| Availability set          | Hardware, rack, or host failure in a datacenter | Spreads VMs across fault and update domains in one datacenter  |
| Availability zone         | A full datacenter failure within a region       | Spreads VMs across physically separate datacenters (zones)     |
| Virtual Machine Scale Set | Changing load                                   | Runs many identical VMs that scale together, and can span zones |

Exam hook: availability **set** = inside one datacenter; availability **zone** = separate datacenters in a region; scale **set** = scaling identical VMs.

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
| VNet peering           | Connect Azure virtual networks privately        |

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
| Connect two Azure virtual networks                               | VNet peering           |

### Public vs private endpoints

| Term             | Meaning                                                                                                                     |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------- |
| Public endpoint  | The service is reachable over the public internet on a public IP address                                                    |
| Private endpoint | The service gets a private IP inside your virtual network (via Azure Private Link), so traffic stays off the public internet |

Exam hook: private endpoint = reach an Azure service privately from your VNet, with no public internet exposure.

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

## Blob Storage Access Tiers

Blob access tiers help balance storage cost and access cost based on how often data is used.

| Tier    | Best for                                                     | Memory hook                                       |
| ------- | ------------------------------------------------------------ | ------------------------------------------------- |
| Hot     | Frequently accessed data                                     | Highest storage cost, lowest access cost          |
| Cool    | Infrequently accessed data stored for around 30 days or more | Lower storage cost than Hot                       |
| Cold    | Rarely accessed data stored for around 90 days or more       | Lower storage cost than Cool                      |
| Archive | Long-term archival data rarely accessed                      | Offline tier; lowest storage cost, delayed access |

Exam tip: if data must be accessed immediately, avoid Archive. Archive is for long-term retention where delayed retrieval is acceptable.

## Moving and Migrating Data

AZ-900 names a few tools for getting data and workloads into Azure.

| Tool                   | Use it to                                                                |
| ---------------------- | ------------------------------------------------------------------------ |
| AzCopy                 | Command-line copy of blobs and files to or from Azure storage            |
| Azure Storage Explorer | Desktop app to browse and move storage data through a GUI                |
| Azure File Sync        | Sync on-premises Windows file servers with Azure Files                   |
| Azure Migrate          | Assess and migrate servers, databases, and apps to Azure                 |
| Azure Data Box         | Physically ship very large datasets when network transfer is impractical |

Exam hook: Data Box = physical device for huge or offline transfers; Azure Migrate = guided migration of servers and apps; AzCopy, Storage Explorer, and File Sync = ongoing file/data movement.

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

Other identity terms AZ-900 may name:

| Item                            | What to remember                                                                                           |
| ------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| Single sign-on (SSO)            | One sign-in that unlocks many applications                                                                 |
| Multifactor authentication      | Requires a second factor (phone, app, or key) in addition to a password                                    |
| Passwordless                    | Sign in without a password, e.g. Windows Hello, the Microsoft Authenticator app, or a FIDO2 security key    |
| Conditional Access              | Allows, blocks, or challenges a sign-in based on user, device, location, or risk                           |
| External identities (B2B / B2C) | B2B invites external partners into your tenant; B2C provides identity for customer-facing apps             |
| Microsoft Entra Domain Services | Managed domain services (domain join, LDAP, Kerberos) in Azure without running your own domain controllers |

## Core Security Concepts

AZ-900 does not require deep security design, but it does expect you to recognize common security principles.

| Concept          | Meaning                                                                                               | Exam memory                                                        |
| ---------------- | ----------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------ |
| Zero Trust       | Never automatically trust a user, device, network, or app. Verify explicitly and use least privilege. | "Verify first, trust nothing by default"                           |
| Defense-in-depth | Use multiple layers of security so one failed control does not expose everything.                     | Physical, identity, perimeter, network, compute, application, data |
| Authentication   | Proves who a user or system is.                                                                       | Sign-in, password, MFA                                             |
| Authorization    | Decides what an authenticated user or system can do.                                                  | RBAC role assignment, permissions                                  |

Simple example:

| Step                                                             | Concept          |
| ---------------------------------------------------------------- | ---------------- |
| A user signs in with password and MFA                            | Authentication   |
| Azure checks whether the user has Reader access                  | Authorization    |
| Azure requires MFA, uses RBAC, monitors logs, and protects data  | Defense-in-depth |
| Access is evaluated continuously instead of trusting the network | Zero Trust       |

## Other Named Services to Recognize

These are light AZ-900 recognition items. You do not need advanced configuration depth.

| Service               | What to remember                                                      |
| --------------------- | --------------------------------------------------------------------- |
| Azure Virtual Desktop | Cloud-hosted Windows desktops and remote apps                         |
| Azure Marketplace     | Catalog for Microsoft and partner solutions, images, and SaaS offers  |
| VNet peering          | Privately connects two Azure virtual networks                         |
| Service Trust Portal  | Microsoft portal for compliance, privacy, security, and audit reports |

## Common Confusions

| This                  | Remember                                     |
| --------------------- | -------------------------------------------- |
| VPN Gateway           | Encrypted tunnel over the public internet    |
| ExpressRoute          | Private dedicated connection                 |
| Load Balancer         | Layer 4 TCP/UDP traffic                      |
| Application Gateway   | Layer 7 HTTP/HTTPS traffic                   |
| Blob Storage          | Object storage                               |
| Azure Files           | Managed file shares                          |
| Hot/Cool/Cold/Archive | Blob access tiers based on access frequency  |
| Availability Zone     | Separate datacenter location inside a region |
| Region Pair           | Two regions for recovery planning            |
| Authentication        | Proves identity                              |
| Authorization         | Grants allowed actions                       |

## Exam Traps

| Trap                                                      | Correct thinking                                                                                  |
| --------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| "A resource group is a billing boundary"                  | A subscription is the billing boundary. A resource group is a lifecycle container.                |
| "Availability zones are the same as regions"              | Zones are inside a region. Regions are separate geographic locations.                             |
| "Blob Storage is for file shares"                         | Blob Storage is object storage. Azure Files provides managed file shares.                         |
| "ExpressRoute uses the public internet"                   | ExpressRoute is private dedicated connectivity. VPN Gateway uses encrypted internet connectivity. |
| "Azure SQL Database requires OS patching by the customer" | Azure SQL Database is PaaS, so Microsoft manages the platform and OS.                             |
| "Authentication and authorization are the same"           | Authentication proves identity. Authorization decides what the identity can access.               |
| "Archive tier is best for data needed immediately"        | Archive is for long-term data that can tolerate delayed retrieval.                                |

## Fast elimination method

| Keyword                             | Usually points to      |
| ----------------------------------- | ---------------------- |
| Full OS control                     | Azure Virtual Machines |
| Web app without managing servers    | Azure App Service      |
| Event-driven code                   | Azure Functions        |
| Object files, images, logs, backups | Blob Storage           |
| Shared file system                  | Azure Files            |
| Private dedicated connection        | ExpressRoute           |
| Encrypted tunnel over internet      | VPN Gateway            |
| HTTP/HTTPS routing                  | Application Gateway    |
| TCP/UDP load distribution           | Azure Load Balancer    |
| Cloud-hosted Windows desktops       | Azure Virtual Desktop  |
| Frequently accessed blob data       | Hot tier               |
| Long-term rarely accessed blob data | Archive tier           |
| Prove user identity                 | Authentication         |
| Decide allowed actions              | Authorization          |

## Mini Scenarios

| Scenario                                                                   | Best answer           |
| -------------------------------------------------------------------------- | --------------------- |
| A company wants to host a simple web app without managing Windows updates. | Azure App Service     |
| A team needs a private network for VMs in Azure.                           | Virtual Network       |
| A backup process stores large unstructured files.                          | Blob Storage          |
| An enterprise needs private connectivity from its datacenter to Azure.     | ExpressRoute          |
| A workload must survive a datacenter failure inside one Azure region.      | Availability Zones    |
| A company needs cloud-hosted Windows desktops for remote workers.          | Azure Virtual Desktop |
| A company stores old compliance files that are rarely read.                | Archive tier          |
| A user signs in with MFA before accessing the portal.                      | Authentication        |
| A signed-in user is allowed to read a resource group but not edit it.      | Authorization         |

## Check Yourself

1. What is the correct Azure hierarchy from largest to smallest?
2. Which service hosts a web app without managing servers?
3. Which storage service is best for images, backups, and logs?
4. What is the difference between VPN Gateway and ExpressRoute?
5. What protects against a datacenter failure inside a region?
6. What is the difference between authentication and authorization?
7. Which Blob Storage tier is best for long-term data that is rarely accessed?

## Answer Guide

1. Management group, subscription, resource group, resource.
2. Azure App Service.
3. Blob Storage.
4. VPN Gateway uses encrypted internet connectivity; ExpressRoute uses private dedicated connectivity.
5. Availability Zones.
6. Authentication proves identity; authorization determines allowed actions.
7. Archive tier.
