# AZ-104 Objective Coverage Matrix

Every skill bullet from the official "Skills measured as of April 17, 2026" outline, mapped to the file(s) in this pack that cover it. Use this to verify nothing in the official outline is left unstudied, and to jump straight to the material for a weak objective.

Last verified against the [official study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/az-104): July 10, 2026.

## Domain 1: Manage Azure identities and governance (20-25%)

### Manage Microsoft Entra users and groups

| Official objective                           | Covered in                                                                                                 |
| -------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| Create users and groups                      | [Study note 01](study-notes/01-identities-and-governance.md), [Lab 01](labs/01-create-users-and-groups.md) |
| Manage user and group properties             | [Study note 01](study-notes/01-identities-and-governance.md), [Lab 01](labs/01-create-users-and-groups.md) |
| Manage licenses in Microsoft Entra ID        | [Study note 01](study-notes/01-identities-and-governance.md), [Lab 01](labs/01-create-users-and-groups.md) |
| Manage external users                        | [Study note 01](study-notes/01-identities-and-governance.md), [Lab 01](labs/01-create-users-and-groups.md) |
| Configure self-service password reset (SSPR) | [Study note 01](study-notes/01-identities-and-governance.md), [Lab 01](labs/01-create-users-and-groups.md) |

### Manage access to Azure resources

| Official objective               | Covered in                                                                                                                                                                      |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Manage built-in Azure roles      | [Study note 01](study-notes/01-identities-and-governance.md), [Lab 02](labs/02-rbac-built-in-and-custom-roles.md)                                                               |
| Assign roles at different scopes | [Study note 01](study-notes/01-identities-and-governance.md), [Lab 02](labs/02-rbac-built-in-and-custom-roles.md)                                                               |
| Interpret access assignments     | [Study note 01](study-notes/01-identities-and-governance.md), [Lab 02](labs/02-rbac-built-in-and-custom-roles.md), [Common Confusions](cheatsheets/az-104-common-confusions.md) |

### Manage Azure subscriptions and governance

| Official objective                                                       | Covered in                                                                                                                                                            |
| ------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Implement and manage Azure Policy                                        | [Study note 01](study-notes/01-identities-and-governance.md), [Lab 03](labs/03-management-groups-and-policy.md)                                                       |
| Configure resource locks                                                 | [Study note 01](study-notes/01-identities-and-governance.md), [Lab 04](labs/04-locks-tags-and-moving-resources.md)                                                    |
| Apply and manage tags on resources                                       | [Study note 01](study-notes/01-identities-and-governance.md), [Lab 04](labs/04-locks-tags-and-moving-resources.md)                                                    |
| Manage resource groups                                                   | [Study note 01](study-notes/01-identities-and-governance.md), [Lab 00](labs/00-set-up-az104-lab-environment.md), [Lab 04](labs/04-locks-tags-and-moving-resources.md) |
| Manage subscriptions                                                     | [Study note 01](study-notes/01-identities-and-governance.md), [Lab 03](labs/03-management-groups-and-policy.md)                                                       |
| Manage costs by using alerts, budgets, and Azure Advisor recommendations | [Study note 01](study-notes/01-identities-and-governance.md), [Lab 00](labs/00-set-up-az104-lab-environment.md), [Lab 21](labs/21-clean-up-all-lab-resources.md)      |
| Configure management groups                                              | [Study note 01](study-notes/01-identities-and-governance.md), [Lab 03](labs/03-management-groups-and-policy.md)                                                       |

## Domain 2: Implement and manage storage (15-20%)

### Configure access to storage

| Official objective                                     | Covered in                                                                                      |
| ------------------------------------------------------ | ----------------------------------------------------------------------------------------------- |
| Configure Azure Storage firewalls and virtual networks | [Study note 02](study-notes/02-storage.md)                                                      |
| Create and use shared access signature (SAS) tokens    | [Study note 02](study-notes/02-storage.md), [Lab 06](labs/06-sas-and-stored-access-policies.md) |
| Configure stored access policies                       | [Study note 02](study-notes/02-storage.md), [Lab 06](labs/06-sas-and-stored-access-policies.md) |
| Manage access keys                                     | [Study note 02](study-notes/02-storage.md), [Lab 06](labs/06-sas-and-stored-access-policies.md) |
| Configure identity-based access for Azure Files        | [Study note 02](study-notes/02-storage.md), [Lab 07](labs/07-azure-files-and-file-sync.md)      |

### Configure and manage storage accounts

| Official objective                                     | Covered in                                                                                               |
| ------------------------------------------------------ | -------------------------------------------------------------------------------------------------------- |
| Create and configure storage accounts                  | [Study note 02](study-notes/02-storage.md), [Lab 05](labs/05-storage-account-tiers-lifecycle.md)         |
| Configure Azure Storage redundancy                     | [Study note 02](study-notes/02-storage.md), [Lab 05](labs/05-storage-account-tiers-lifecycle.md)         |
| Configure object replication                           | [Study note 02](study-notes/02-storage.md), [Quick Reference](cheatsheets/az-104-quick-reference.md)     |
| Configure storage account encryption                   | [Study note 02](study-notes/02-storage.md)                                                               |
| Manage data by using Azure Storage Explorer and AzCopy | [Study note 02](study-notes/02-storage.md), [Common Confusions](cheatsheets/az-104-common-confusions.md) |

### Configure Azure Files and Azure Blob Storage

| Official objective                                     | Covered in                                                                                       |
| ------------------------------------------------------ | ------------------------------------------------------------------------------------------------ |
| Create and configure a file share in Azure Files       | [Study note 02](study-notes/02-storage.md), [Lab 07](labs/07-azure-files-and-file-sync.md)       |
| Create and configure a container in Azure Blob Storage | [Study note 02](study-notes/02-storage.md), [Lab 05](labs/05-storage-account-tiers-lifecycle.md) |
| Configure storage tiers                                | [Study note 02](study-notes/02-storage.md), [Lab 05](labs/05-storage-account-tiers-lifecycle.md) |
| Configure soft delete for blobs and containers         | [Study note 02](study-notes/02-storage.md), [Lab 05](labs/05-storage-account-tiers-lifecycle.md) |
| Configure snapshots and soft delete for Azure Files    | [Study note 02](study-notes/02-storage.md), [Lab 07](labs/07-azure-files-and-file-sync.md)       |
| Configure blob lifecycle management                    | [Study note 02](study-notes/02-storage.md), [Lab 05](labs/05-storage-account-tiers-lifecycle.md) |
| Configure blob versioning                              | [Study note 02](study-notes/02-storage.md), [Lab 05](labs/05-storage-account-tiers-lifecycle.md) |

## Domain 3: Deploy and manage Azure compute resources (20-25%)

### Automate deployment of resources by using Azure Resource Manager (ARM) templates or Bicep files

| Official objective                                                                                                      | Covered in                                                                               |
| ----------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| Interpret an Azure Resource Manager template or a Bicep file                                                            | [Study note 03](study-notes/03-compute.md), [Lab 08](labs/08-arm-templates-and-bicep.md) |
| Modify an existing Azure Resource Manager template                                                                      | [Study note 03](study-notes/03-compute.md), [Lab 08](labs/08-arm-templates-and-bicep.md) |
| Modify an existing Bicep file                                                                                           | [Study note 03](study-notes/03-compute.md), [Lab 08](labs/08-arm-templates-and-bicep.md) |
| Deploy resources by using an Azure Resource Manager template or a Bicep file                                            | [Study note 03](study-notes/03-compute.md), [Lab 08](labs/08-arm-templates-and-bicep.md) |
| Export a deployment as an Azure Resource Manager template or convert an Azure Resource Manager template to a Bicep file | [Study note 03](study-notes/03-compute.md), [Lab 08](labs/08-arm-templates-and-bicep.md) |

### Create and configure virtual machines

| Official objective                                                        | Covered in                                                                                               |
| ------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| Create a virtual machine                                                  | [Study note 03](study-notes/03-compute.md), [Lab 09](labs/09-create-vm-availability-set.md)              |
| Configure encryption at host for Azure virtual machines                   | [Study note 03](study-notes/03-compute.md), [Common Confusions](cheatsheets/az-104-common-confusions.md) |
| Move a virtual machine to another resource group, subscription, or region | [Study note 03](study-notes/03-compute.md), [Lab 04](labs/04-locks-tags-and-moving-resources.md)         |
| Manage virtual machine sizes                                              | [Study note 03](study-notes/03-compute.md), [Lab 10](labs/10-vm-resize-and-disks.md)                     |
| Manage virtual machine disks                                              | [Study note 03](study-notes/03-compute.md), [Lab 10](labs/10-vm-resize-and-disks.md)                     |
| Deploy virtual machines to availability zones and availability sets       | [Study note 03](study-notes/03-compute.md), [Lab 09](labs/09-create-vm-availability-set.md)              |
| Deploy and configure an Azure Virtual Machine Scale Sets                  | [Study note 03](study-notes/03-compute.md), [Lab 11](labs/11-vm-scale-set-autoscale.md)                  |

### Provision and manage containers in the Azure portal

| Official objective                                                                                     | Covered in                                                                                            |
| ------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------- |
| Create and manage an Azure Container Registry                                                          | [Study note 03](study-notes/03-compute.md), [Lab 13](labs/13-container-instances-and-aks-concepts.md) |
| Provision a container by using Azure Container Instances                                               | [Study note 03](study-notes/03-compute.md), [Lab 13](labs/13-container-instances-and-aks-concepts.md) |
| Provision a container by using Azure Container Apps                                                    | [Study note 03](study-notes/03-compute.md), [Lab 13](labs/13-container-instances-and-aks-concepts.md) |
| Manage sizing and scaling for containers, including Azure Container Instances and Azure Container Apps | [Study note 03](study-notes/03-compute.md), [Lab 13](labs/13-container-instances-and-aks-concepts.md) |

### Create and configure Azure App Service

| Official objective                                                           | Covered in                                                                                         |
| ---------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| Provision an App Service plan                                                | [Study note 03](study-notes/03-compute.md), [Lab 12](labs/12-app-service-plan-deployment-slots.md) |
| Configure scaling for an App Service plan                                    | [Study note 03](study-notes/03-compute.md), [Lab 12](labs/12-app-service-plan-deployment-slots.md) |
| Create an App Service                                                        | [Study note 03](study-notes/03-compute.md), [Lab 12](labs/12-app-service-plan-deployment-slots.md) |
| Configure certificates and Transport Layer Security (TLS) for an App Service | [Study note 03](study-notes/03-compute.md), [Lab 12](labs/12-app-service-plan-deployment-slots.md) |
| Map an existing custom DNS name to an App Service                            | [Study note 03](study-notes/03-compute.md), [Lab 12](labs/12-app-service-plan-deployment-slots.md) |
| Configure backup for an App Service                                          | [Study note 03](study-notes/03-compute.md), [Lab 12](labs/12-app-service-plan-deployment-slots.md) |
| Configure networking settings for an App Service                             | [Study note 03](study-notes/03-compute.md), [Lab 12](labs/12-app-service-plan-deployment-slots.md) |
| Configure deployment slots for an App Service                                | [Study note 03](study-notes/03-compute.md), [Lab 12](labs/12-app-service-plan-deployment-slots.md) |

## Domain 4: Implement and manage virtual networking (15-20%)

### Configure and manage virtual networks in Azure

| Official objective                                | Covered in                                                                                                                                                 |
| ------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Create and configure virtual networks and subnets | [Study note 04](study-notes/04-virtual-networking.md), [Lab 14](labs/14-vnet-subnets-nsg-asg.md)                                                           |
| Create and configure virtual network peering      | [Study note 04](study-notes/04-virtual-networking.md), [Lab 15](labs/15-vnet-peering-and-network-watcher.md)                                               |
| Configure public IP addresses                     | [Study note 04](study-notes/04-virtual-networking.md), [Lab 09](labs/09-create-vm-availability-set.md), [Lab 17](labs/17-load-balancer-and-app-gateway.md) |
| Configure user-defined routes                     | [Study note 04](study-notes/04-virtual-networking.md)                                                                                                      |
| Troubleshoot network connectivity                 | [Study note 04](study-notes/04-virtual-networking.md), [Lab 15](labs/15-vnet-peering-and-network-watcher.md)                                               |

### Configure secure access to virtual networks

| Official objective                                                                  | Covered in                                                                                                          |
| ----------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| Create and configure network security groups (NSGs) and application security groups | [Study note 04](study-notes/04-virtual-networking.md), [Lab 14](labs/14-vnet-subnets-nsg-asg.md)                    |
| Evaluate effective security rules in NSGs                                           | [Study note 04](study-notes/04-virtual-networking.md), [Lab 14](labs/14-vnet-subnets-nsg-asg.md)                    |
| Implement Azure Bastion                                                             | [Study note 04](study-notes/04-virtual-networking.md), [Service Picker](cheatsheets/az-104-service-picker.md)       |
| Configure service endpoints for Azure platform as a service (PaaS)                  | [Study note 04](study-notes/04-virtual-networking.md), [Common Confusions](cheatsheets/az-104-common-confusions.md) |
| Configure private endpoints for Azure PaaS                                          | [Study note 04](study-notes/04-virtual-networking.md), [Lab 16](labs/16-azure-dns-zones.md)                         |

### Configure name resolution and load balancing

| Official objective                            | Covered in                                                                                                |
| --------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| Configure Azure DNS                           | [Study note 04](study-notes/04-virtual-networking.md), [Lab 16](labs/16-azure-dns-zones.md)               |
| Configure an internal or public load balancer | [Study note 04](study-notes/04-virtual-networking.md), [Lab 17](labs/17-load-balancer-and-app-gateway.md) |
| Troubleshoot load balancing                   | [Study note 04](study-notes/04-virtual-networking.md), [Lab 17](labs/17-load-balancer-and-app-gateway.md) |

## Domain 5: Monitor and maintain Azure resources (10-15%)

### Monitor resources in Azure

| Official objective                                                                                                     | Covered in                                                                                                           |
| ---------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| Interpret metrics in Azure Monitor                                                                                     | [Study note 05](study-notes/05-monitoring-and-maintenance.md), [Lab 18](labs/18-monitor-alerts-action-groups.md)     |
| Configure log settings in Azure Monitor                                                                                | [Study note 05](study-notes/05-monitoring-and-maintenance.md), [Lab 19](labs/19-log-analytics-and-kql.md)            |
| Query and analyze logs in Azure Monitor                                                                                | [Study note 05](study-notes/05-monitoring-and-maintenance.md), [Lab 19](labs/19-log-analytics-and-kql.md)            |
| Set up alert rules, action groups, and alert processing rules in Azure Monitor                                         | [Study note 05](study-notes/05-monitoring-and-maintenance.md), [Lab 18](labs/18-monitor-alerts-action-groups.md)     |
| Configure and interpret monitoring of virtual machines, storage accounts, and networks by using Azure Monitor Insights | [Study note 05](study-notes/05-monitoring-and-maintenance.md), [Lab 19](labs/19-log-analytics-and-kql.md)            |
| Use Azure Network Watcher and Connection monitor                                                                       | [Study note 05](study-notes/05-monitoring-and-maintenance.md), [Lab 15](labs/15-vnet-peering-and-network-watcher.md) |

### Implement backup and recovery

| Official objective                                              | Covered in                                                                                                  |
| --------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| Create a Recovery Services vault                                | [Study note 05](study-notes/05-monitoring-and-maintenance.md), [Lab 20](labs/20-back-up-vm-azure-backup.md) |
| Create an Azure Backup vault                                    | [Study note 05](study-notes/05-monitoring-and-maintenance.md), [Lab 20](labs/20-back-up-vm-azure-backup.md) |
| Create and configure a backup policy                            | [Study note 05](study-notes/05-monitoring-and-maintenance.md), [Lab 20](labs/20-back-up-vm-azure-backup.md) |
| Perform backup and restore operations by using Azure Backup     | [Study note 05](study-notes/05-monitoring-and-maintenance.md), [Lab 20](labs/20-back-up-vm-azure-backup.md) |
| Configure Azure Site Recovery for Azure resources               | [Study note 05](study-notes/05-monitoring-and-maintenance.md), [Lab 20](labs/20-back-up-vm-azure-backup.md) |
| Perform a failover to a secondary region by using Site Recovery | [Study note 05](study-notes/05-monitoring-and-maintenance.md)                                               |
| Configure and interpret reports and alerts for backups          | [Study note 05](study-notes/05-monitoring-and-maintenance.md), [Lab 20](labs/20-back-up-vm-azure-backup.md) |

## Gaps

Every official objective is covered by at least one study note. The objectives below have no dedicated hands-on lab, mostly because the resources involved are expensive or need a second region/tenant; the study notes cover them at exam depth, but consider a portal read-through if any feels weak:

| Objective without a hands-on lab                                | Where it is covered instead                                   | Why no lab                                                  |
| --------------------------------------------------------------- | ------------------------------------------------------------- | ----------------------------------------------------------- |
| Configure Azure Storage firewalls and virtual networks          | [Study note 02](study-notes/02-storage.md)                    | Risk of locking yourself out of the lab storage account     |
| Configure object replication                                    | [Study note 02](study-notes/02-storage.md)                    | Needs a second storage account and versioning both sides    |
| Configure storage account encryption                            | [Study note 02](study-notes/02-storage.md)                    | Platform default; customer-managed keys need Key Vault      |
| Manage data by using Azure Storage Explorer and AzCopy          | [Study note 02](study-notes/02-storage.md)                    | Local tooling install; recognition depth is what is tested  |
| Configure encryption at host for Azure virtual machines         | [Study note 03](study-notes/03-compute.md)                    | Requires a subscription feature registration                |
| Configure user-defined routes                                   | [Study note 04](study-notes/04-virtual-networking.md)         | Lab 15 diagnoses routes with next hop but creates no UDR    |
| Implement Azure Bastion                                         | [Study note 04](study-notes/04-virtual-networking.md)         | Bastion bills per hour and is a common cost trap            |
| Configure service endpoints for Azure PaaS                      | [Study note 04](study-notes/04-virtual-networking.md)         | Concept comparison (vs private endpoints) is what is tested |
| Perform a failover to a secondary region by using Site Recovery | [Study note 05](study-notes/05-monitoring-and-maintenance.md) | ASR bills per protected instance; lab 20 reads the blade    |
