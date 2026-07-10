# 03 - Deploy and Manage Azure Compute Resources

This domain is worth 20-25% of the exam, tied with identities for the biggest share. It covers ARM templates and Bicep, virtual machines (creation, encryption, moving, sizes, disks, availability), Virtual Machine Scale Sets, containers (Azure Container Registry, Container Instances, Container Apps), and Azure App Service.

## Mental model

Compute questions are almost always "pick the right level of abstraction and the right resilience option." VMs give control, scale sets give elastic identical VMs, containers give packaged apps without full VMs, and App Service gives managed web hosting. Resilience climbs from availability set (rack) to availability zone (datacenter) to region pair (region).

| Scenario keyword                                      | Likely concept                               |
| ----------------------------------------------------- | -------------------------------------------- |
| "Repeatable, declarative deployment"                  | ARM template or Bicep file                   |
| "Protect against rack/host failure in one datacenter" | Availability set                             |
| "Protect against datacenter failure, 99.99% SLA"      | Availability zones (2+ VMs)                  |
| "Automatically add VMs under load"                    | Virtual Machine Scale Set with autoscale     |
| "Run a container in seconds without servers"          | Azure Container Instances                    |
| "Microservices with scale to zero and revisions"      | Azure Container Apps                         |
| "Store private container images"                      | Azure Container Registry                     |
| "Web app without managing the OS"                     | Azure App Service                            |
| "Test in production-like slot, swap with no downtime" | Deployment slots (Standard tier or higher)   |
| "Encrypt VM disks including temp/cache at the host"   | Encryption at host                           |
| "Custom domain with HTTPS on a web app"               | Custom DNS mapping + TLS certificate binding |

## ARM templates and Bicep

### What they are

| Aspect       | ARM template                              | Bicep                                    |
| ------------ | ----------------------------------------- | ---------------------------------------- |
| Language     | JSON                                      | Domain-specific language, cleaner syntax |
| Relationship | The deployment format Azure understands   | Transpiles to ARM JSON at deployment     |
| Sections     | parameters, variables, resources, outputs | param, var, resource, output keywords    |
| Reuse        | Linked/nested templates                   | Modules                                  |

Deployments are declarative (describe the end state) and idempotent (re-running produces the same result).

### Deployment modes

| Mode        | Behavior                                                                 |
| ----------- | ------------------------------------------------------------------------ |
| Incremental | Default. Adds/updates resources in the template; leaves others untouched |
| Complete    | Deletes resources in the resource group that are not in the template     |

### Reading a template (recognition level)

- parameters: values supplied at deployment time (allowedValues, defaultValue).
- variables: computed values reused in the template.
- resources: each has type (Microsoft.Compute/virtualMachines), apiVersion, name, location, properties.
- outputs: values returned after deployment (e.g. a public IP).
- dependsOn (ARM) controls ordering; Bicep infers most dependencies from symbolic references.

### Export and convert

| Task                               | How                                                                 |
| ---------------------------------- | ------------------------------------------------------------------- |
| Export a deployed RG as a template | Resource group > Export template (or a deployment's template blade) |
| Convert ARM JSON to Bicep          | az bicep decompile (or bicep decompile)                             |
| Convert Bicep to ARM JSON          | az bicep build (or bicep build)                                     |
| Deploy to a resource group         | az deployment group create / New-AzResourceGroupDeployment          |
| Deploy to a subscription           | az deployment sub create / New-AzDeployment                         |

## Virtual machines

### Creating a VM: what gets created

A portal VM deployment typically creates the VM, an OS disk, a NIC, and optionally a public IP, an NSG, and a VNet if none exists. Deleting the VM does not automatically delete all companions unless you selected delete-with-VM options.

### Sizes

| Size family examples | Optimized for                |
| -------------------- | ---------------------------- |
| B                    | Burstable, low-cost dev/test |
| D                    | General purpose              |
| E                    | Memory optimized             |
| F                    | Compute (CPU) optimized      |
| L                    | Storage optimized            |
| N                    | GPU                          |

Key facts:

- Resizing a VM restarts it if the new size is available on the current hardware cluster; if not, it must be deallocated first.
- A deallocated (stopped from the portal/CLI) VM stops compute billing; disks still bill. A VM shut down only from inside the OS keeps billing.

### Disks

| Disk           | Notes                                                       |
| -------------- | ----------------------------------------------------------- |
| OS disk        | Boot disk; one per VM                                       |
| Data disk      | Attach as many as the VM size allows                        |
| Temporary disk | Local, non-persistent scratch (lost on deallocate/redeploy) |

| Managed disk type | Use                                      |
| ----------------- | ---------------------------------------- |
| Standard HDD      | Dev/test, backups                        |
| Standard SSD      | Light production, web servers            |
| Premium SSD       | Production, low latency, SLA-backed      |
| Premium SSD v2    | High performance with tunable IOPS       |
| Ultra Disk        | Extreme IOPS (databases); data disk only |

Key facts:

- Managed disks are the default; Azure handles the storage accounts behind them.
- Snapshots create a point-in-time copy of a disk; a snapshot can seed a new disk.
- Disks can be resized larger; shrinking is not supported.

### VM encryption options

| Option                           | What it covers                                                      |
| -------------------------------- | ------------------------------------------------------------------- |
| Server-side encryption (default) | All managed disks at rest, platform or customer-managed keys        |
| Encryption at host               | Data encrypted on the VM host itself: temp disk and disk caches too |
| Azure Disk Encryption (ADE)      | In-guest BitLocker (Windows) / DM-Crypt (Linux) with Key Vault keys |
| Confidential disk encryption     | For confidential VMs (recognition only)                             |

Encryption at host must be enabled on the subscription feature and the VM; it is the exam answer for "encrypt temp disks and caches."

### Moving VMs

| Move                             | How                                                               |
| -------------------------------- | ----------------------------------------------------------------- |
| Another resource group           | Move operation (Resource Mover / portal Move)                     |
| Another subscription             | Move (same tenant); dependent resources must move together        |
| Another region                   | Azure Resource Mover or Azure Site Recovery                       |
| Another zone/availability option | Requires recreation from disks/snapshots (cannot toggle in place) |

### Availability options: the classic table

| Option             | Protects against                   | SLA (recognition)           | Notes                                          |
| ------------------ | ---------------------------------- | --------------------------- | ---------------------------------------------- |
| Single premium VM  | Nothing extra                      | 99.9%                       | Needs premium SSD for the SLA                  |
| Availability set   | Rack/host failure, planned updates | 99.95% (2+ VMs)             | Fault domains + update domains, one datacenter |
| Availability zones | Datacenter failure                 | 99.99% (2+ VMs in 2+ zones) | Zone = separate power/cooling/network          |
| VM Scale Set       | Scale + can span zones             | Depends on layout           | Elastic capacity, identical instances          |

| Availability set term | Meaning                                            | Limits               |
| --------------------- | -------------------------------------------------- | -------------------- |
| Fault domain (FD)     | Shared power/network (a rack)                      | Up to 3              |
| Update domain (UD)    | Group rebooted together during planned maintenance | Up to 20 (5 default) |

Key facts:

- A VM must be added to an availability set at creation time.
- You cannot combine an availability set and availability zones for the same VM.
- Zones beat sets when the region supports them and you need the higher SLA.

## Virtual Machine Scale Sets

| Concept              | Detail                                                              |
| -------------------- | ------------------------------------------------------------------- |
| What it is           | A set of identical VMs from one image/model, managed as a group     |
| Orchestration modes  | Uniform (identical instances) or Flexible (mixed, more control)     |
| Scaling              | Manual instance count or autoscale rules                            |
| Autoscale rule parts | Metric (e.g. CPU > 70%), duration, action (increase by 1), cooldown |
| Zones                | A scale set can spread instances across availability zones          |
| Capacity             | Up to 1,000 instances (100 with custom images, uniform)             |

Key facts:

- Always define scale-out AND scale-in rules, plus instance limits (min/max/default).
- Upgrade policy (manual/automatic/rolling) controls how model changes reach instances.
- Scale sets are the exam answer for "automatically add/remove identical VMs."

## Containers

### Azure Container Registry (ACR)

| Item       | Detail                                                                |
| ---------- | --------------------------------------------------------------------- |
| What it is | Private registry for container images (like private Docker Hub)       |
| SKUs       | Basic, Standard, Premium (Premium adds geo-replication, private link) |
| Push/pull  | docker push/pull with <registry>.azurecr.io, or az acr build          |
| Auth       | Entra ID, admin account (discouraged), tokens                         |

### Compare the container services

| Service                   | Best for                                               | Scaling                              |
| ------------------------- | ------------------------------------------------------ | ------------------------------------ |
| Azure Container Instances | Single containers, quick jobs, burst work              | Manual; per-second billing           |
| Azure Container Apps      | Microservices, event-driven apps, background jobs      | Autoscale incl. scale to zero (KEDA) |
| Azure Kubernetes Service  | Full orchestration control (out of AZ-104 scope depth) | Cluster/pod autoscalers              |

### Azure Container Instances (ACI)

- Fastest way to run a container: no VM, no orchestrator, per-second billing.
- Container group: containers scheduled together on one host, sharing network and volumes (like a pod).
- Sizing: specify CPU cores and memory per container; restart policy Always/OnFailure/Never.
- Can mount Azure Files shares for persistent storage.

### Azure Container Apps

- Serverless container platform on managed Kubernetes (you never see the cluster).
- Revisions for versioned deployments, traffic splitting, ingress out of the box.
- Scale rules on HTTP traffic, events, CPU/memory; can scale to zero (ACI cannot).

## Azure App Service

### Plans and tiers

| Tier          | Highlights                                                        |
| ------------- | ----------------------------------------------------------------- |
| Free / Shared | Try-out; no custom domain SSL binding, no SLA, shared workers     |
| Basic         | Custom domains, manual scale up to 3 instances, no slots          |
| Standard      | Autoscale (up to 10), 5 deployment slots, daily backups           |
| Premium (v3)  | More/faster instances, up to 30, 20 slots, VNet integration scale |
| Isolated      | App Service Environment: dedicated, network-isolated              |

Key facts:

- The plan defines the compute (region, size, count); apps in one plan share its instances.
- Scale up = change tier/size (vertical). Scale out = more instances (horizontal, autoscale needs Standard+).
- The plan bills even with zero apps running on it.

### Deployment slots

- Separate app instances with their own content and (optionally) settings, e.g. a staging slot.
- Swap exchanges slots with warmed instances: near-zero downtime deploys and instant rollback (swap back).
- Slot-specific ("sticky") settings such as connection strings can stay with the slot during a swap.
- Requires Standard tier or higher.

### Certificates, TLS, and custom domains

| Task                     | Key facts                                                                                   |
| ------------------------ | ------------------------------------------------------------------------------------------- |
| Map a custom domain      | Add domain in portal; verify with CNAME (subdomain) or A record + TXT (apex)                |
| Secure it                | Bind a certificate: App Service managed certificate (free), uploaded PFX, or Key Vault cert |
| Enforce encryption       | HTTPS Only setting; set minimum TLS version                                                 |
| Free managed certificate | No wildcard, no apex support on some setups, auto-renews                                    |

### Networking and backup

| Feature             | What it does                                                          |
| ------------------- | --------------------------------------------------------------------- |
| VNet integration    | Outbound calls from the app into your VNet                            |
| Private endpoint    | Inbound: app reachable on a private IP in your VNet                   |
| Access restrictions | Allow/deny inbound by IP/subnet/service tag                           |
| Hybrid connections  | Reach a specific on-premises host:port                                |
| Backup (Standard+)  | Scheduled or manual backups of app content + configuration + database |

## Limits and numbers to memorize

| Item                                             | Value                              |
| ------------------------------------------------ | ---------------------------------- |
| Availability set fault domains                   | Up to 3                            |
| Availability set update domains                  | Up to 20 (default 5)               |
| VM SLA: zones / set / single premium             | 99.99% / 99.95% / 99.9%            |
| Scale set max instances (uniform)                | 1,000 (100 with custom image)      |
| App Service slots: Standard / Premium            | 5 / 20                             |
| App Service max instances: Standard / Premium v3 | 10 / 30                            |
| Data disks                                       | Depends on VM size (bigger = more) |
| Deployment modes                                 | Incremental (default), Complete    |
| ACR SKUs                                         | Basic, Standard, Premium           |

## CLI and PowerShell recognition

| Task                        | Azure CLI                      | PowerShell                       |
| --------------------------- | ------------------------------ | -------------------------------- |
| Create a VM                 | az vm create                   | New-AzVM                         |
| Deallocate a VM             | az vm deallocate               | Stop-AzVM                        |
| Resize a VM                 | az vm resize                   | Update-AzVM (after setting size) |
| List VM sizes in a region   | az vm list-sizes               | Get-AzVMSize                     |
| Attach a data disk          | az vm disk attach              | Add-AzVMDataDisk                 |
| Create a scale set          | az vmss create                 | New-AzVmss                       |
| Scale a scale set           | az vmss scale                  | Update-AzVmss                    |
| Create a container registry | az acr create                  | New-AzContainerRegistry          |
| Run a container instance    | az container create            | New-AzContainerGroup             |
| Create an App Service plan  | az appservice plan create      | New-AzAppServicePlan             |
| Create a web app            | az webapp create               | New-AzWebApp                     |
| Swap deployment slots       | az webapp deployment slot swap | Switch-AzWebAppSlot              |
| Deploy a template to an RG  | az deployment group create     | New-AzResourceGroupDeployment    |
| Build Bicep to ARM JSON     | az bicep build                 | bicep build (same tool)          |

## Common confusions

| Confusion                                   | Correct idea                                                                     |
| ------------------------------------------- | -------------------------------------------------------------------------------- |
| Availability set vs availability zone       | Racks in one datacenter vs separate datacenters in one region                    |
| Fault domain vs update domain               | Hardware failure boundary vs planned maintenance reboot group                    |
| Incremental vs complete deployment mode     | Leave extra resources vs delete resources not in the template                    |
| ARM template vs Bicep                       | Same engine; Bicep is the friendlier language that compiles to ARM JSON          |
| Stop vs deallocate                          | OS shutdown keeps billing; deallocate releases compute and stops compute billing |
| Encryption at host vs Azure Disk Encryption | Host-level (incl. temp/cache) vs in-guest BitLocker/DM-Crypt                     |
| ACI vs Container Apps                       | Single quick containers vs microservices with autoscale/scale to zero            |
| ACI container group vs single container     | Group shares host, network, volumes (pod-like)                                   |
| Scale up vs scale out (App Service)         | Bigger tier/instance vs more instances                                           |
| App Service plan vs web app                 | The compute (billed) vs the app running on it                                    |
| Slot swap vs redeploy                       | Instant exchange with rollback vs new deployment                                 |

## Exam traps

| Trap                                                             | Why people miss it                                       |
| ---------------------------------------------------------------- | -------------------------------------------------------- |
| Wanting 99.99% SLA from an availability set                      | Sets top out at 99.95%; zones give 99.99%                |
| Adding an existing VM to an availability set                     | Not possible; the set is chosen at VM creation           |
| Using complete mode casually                                     | It deletes resources missing from the template           |
| Forgetting a deallocated VM still bills for disks and public IPs | Compute stops; storage and some IPs continue             |
| Choosing ADE when the requirement mentions temp disk encryption  | Encryption at host covers temp disks and caches          |
| Autoscale configured with only a scale-out rule                  | Without a scale-in rule, instance count never drops      |
| Expecting deployment slots on Basic tier                         | Slots need Standard or higher                            |
| Expecting scale to zero on ACI                                   | Container Apps scales to zero; ACI does not              |
| Custom domain added without DNS verification                     | CNAME/TXT records must exist before the domain validates |
| Moving a VM to another region with a simple "move"               | Region moves need Resource Mover or Site Recovery        |

## Mini scenarios

| Scenario                                                                                                  | Best answer                                              |
| --------------------------------------------------------------------------------------------------------- | -------------------------------------------------------- |
| Two web VMs must keep running during planned host maintenance and rack failures; the region has no zones. | Availability set (2 fault domains or more, multiple UDs) |
| A production workload needs the highest VM SLA in a zone-enabled region.                                  | Two or more VMs across availability zones (99.99%)       |
| A nightly batch job needs a container for 20 minutes, cheapest and simplest.                              | Azure Container Instances                                |
| An API with spiky traffic should scale to zero at night.                                                  | Azure Container Apps                                     |
| The same 3-tier environment must be deployed identically to dev, test, and prod.                          | Parameterized ARM template or Bicep file                 |
| Ops must ensure re-running a deployment never deletes manually added resources.                           | Incremental deployment mode (default)                    |
| A web app must be updated with zero downtime and instant rollback.                                        | Deployment slots with swap (Standard tier or higher)     |
| A VM's disk latency is too high on Standard SSD for a database.                                           | Move to Premium SSD (or Ultra Disk for extreme IOPS)     |
| Compliance requires VM temp disks and disk caches encrypted.                                              | Enable encryption at host                                |
| Web tier VMs must automatically grow from 2 to 10 instances when CPU passes 75%.                          | VM Scale Set with an autoscale rule (min 2, max 10)      |

## Check yourself

1. What SLA do two VMs in an availability set have vs two VMs across availability zones?
2. How many fault domains and update domains can an availability set have?
3. What does complete deployment mode do that incremental does not?
4. Which encryption option covers the VM temp disk and disk caches?
5. A VM was stopped from inside Windows. Is compute still billed?
6. What is the difference between az vm deallocate and Stop-AzVM in effect?
7. Which container service supports scale to zero?
8. Which App Service tier first unlocks deployment slots, and how many does it give?
9. What must be true before you can bind a free App Service managed certificate to a domain?
10. Which command deploys a Bicep file to a resource group?

## Answer guide

1. 99.95% for the set, 99.99% for zones.
2. Up to 3 fault domains and up to 20 update domains (5 by default).
3. Deletes resources in the resource group that are not defined in the template.
4. Encryption at host.
5. Yes; the VM is stopped but not deallocated, so the compute allocation still bills.
6. Both deallocate the VM (Stop-AzVM defaults to deallocation), releasing compute billing.
7. Azure Container Apps.
8. Standard, with 5 slots (Premium gives 20).
9. The custom domain must be added and verified on the app first (DNS CNAME/TXT records).
10. az deployment group create (or New-AzResourceGroupDeployment); Bicep files deploy directly.
