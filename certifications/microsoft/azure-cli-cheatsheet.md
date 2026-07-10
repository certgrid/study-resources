# Azure CLI Cheatsheet

Use this as a recognition and lab-safety sheet for Microsoft Azure exams. You do not need to memorize every flag, but you should recognize command families, know where scope appears, and understand which command answers common administration scenarios.

Official docs: [Azure CLI documentation](https://learn.microsoft.com/en-us/cli/azure/).

## Command Shape

Azure CLI commands usually follow this pattern:

```bash
az <group> <subgroup> <verb> --name <name> --resource-group <rg> --location <region>
```

| Part               | Meaning              | Example                                        |
| ------------------ | -------------------- | ---------------------------------------------- |
| `az`               | Azure CLI executable | `az login`                                     |
| Command group      | Service family       | `group`, `vm`, `storage`, `network`, `monitor` |
| Verb               | Action               | `create`, `show`, `list`, `update`, `delete`   |
| `--resource-group` | Resource group scope | `--resource-group rg-lab`                      |
| `--location`       | Azure region         | `--location eastus`                            |
| `--query`          | JMESPath filter      | `--query "[].name"`                            |
| `--output`         | Output format        | `--output table`                               |

## Sign In and Context

| Task                                  | Command                                                        |
| ------------------------------------- | -------------------------------------------------------------- |
| Sign in interactively                 | `az login`                                                     |
| Show current account                  | `az account show --output table`                               |
| List subscriptions                    | `az account list --output table`                               |
| Set active subscription               | `az account set --subscription <subscription-id-or-name>`      |
| Show default values                   | `az config get defaults`                                       |
| Set default resource group and region | `az config set defaults.group=rg-lab defaults.location=eastus` |
| Clear defaults                        | `az config unset defaults.group defaults.location`             |

Exam hook: if a command creates or changes resources, make sure you know which subscription and resource group are active.

## Output and Filtering

| Need                 | Command pattern                        |
| -------------------- | -------------------------------------- |
| Human-readable table | `--output table`                       |
| Raw value only       | `--output tsv`                         |
| JSON for scripts     | `--output json`                        |
| Select one property  | `--query name --output tsv`            |
| List names           | `--query "[].name" --output table`     |
| Filter items         | `--query "[?location=='eastus'].name"` |

Common pattern:

```bash
az group list --query "[].{Name:name, Location:location}" --output table
```

## Resource Groups

| Task                    | Command                                           |
| ----------------------- | ------------------------------------------------- |
| Create a resource group | `az group create --name rg-lab --location eastus` |
| List resource groups    | `az group list --output table`                    |
| Show one resource group | `az group show --name rg-lab --output table`      |
| Delete a resource group | `az group delete --name rg-lab --yes`             |

Lab safety: deleting a resource group deletes the resources inside it. Check the resource group name twice.

## Resources, Tags, and Locks

| Task                      | Command                                                                                 |
| ------------------------- | --------------------------------------------------------------------------------------- |
| List resources in a group | `az resource list --resource-group rg-lab --output table`                               |
| Show a resource           | `az resource show --ids <resource-id>`                                                  |
| Add or update tags        | `az resource tag --ids <resource-id> --tags CostCenter=Training Owner=Student`          |
| Create delete lock        | `az lock create --name protect-delete --lock-type CanNotDelete --resource-group rg-lab` |
| List locks                | `az lock list --resource-group rg-lab --output table`                                   |
| Delete a lock             | `az lock delete --name protect-delete --resource-group rg-lab`                          |

## Identity and RBAC

| Task                                  | Command                                                                               |
| ------------------------------------- | ------------------------------------------------------------------------------------- |
| Show signed-in user                   | `az ad signed-in-user show`                                                           |
| List role assignments                 | `az role assignment list --scope <scope> --output table`                              |
| Assign a role                         | `az role assignment create --assignee <user-or-app-id> --role Reader --scope <scope>` |
| List built-in role definitions        | `az role definition list --name Reader --output table`                                |
| Show current user's access to a scope | `az role assignment list --assignee <object-id> --scope <scope>`                      |

Scope examples:

| Scope          | Shape                                                            |
| -------------- | ---------------------------------------------------------------- |
| Subscription   | `/subscriptions/<sub-id>`                                        |
| Resource group | `/subscriptions/<sub-id>/resourceGroups/<rg-name>`               |
| Resource       | Full resource ID from `az resource show --query id --output tsv` |

Exam hook: Azure RBAC controls who can manage Azure resources. Microsoft Entra roles control identity administration.

## Policy

| Task                         | Command                                                                            |
| ---------------------------- | ---------------------------------------------------------------------------------- |
| List policy assignments      | `az policy assignment list --output table`                                         |
| Show a policy assignment     | `az policy assignment show --name <assignment-name>`                               |
| List policy definitions      | `az policy definition list --output table`                                         |
| Trigger compliance scan      | `az policy state trigger-scan`                                                     |
| List non-compliant resources | `az policy state list --filter "complianceState eq 'NonCompliant'" --output table` |

Exam hook: RBAC can allow an action while Policy still denies the request content.

## Storage

| Task                   | Command                                                                                                                  |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| Create storage account | `az storage account create --name <unique-name> --resource-group rg-lab --location eastus --sku Standard_LRS`            |
| Show storage account   | `az storage account show --name <name> --resource-group rg-lab --output table`                                           |
| List storage keys      | `az storage account keys list --account-name <name> --resource-group rg-lab`                                             |
| Rotate a storage key   | `az storage account keys renew --account-name <name> --resource-group rg-lab --key key1`                                 |
| Create blob container  | `az storage container create --name data --account-name <name> --auth-mode login`                                        |
| Upload blob            | `az storage blob upload --account-name <name> --container-name data --file ./file.txt --name file.txt --auth-mode login` |
| Set blob tier          | `az storage blob set-tier --account-name <name> --container-name data --name file.txt --tier Cool --auth-mode login`     |
| Create file share      | `az storage share-rm create --resource-group rg-lab --storage-account <name> --name files`                               |

SAS recognition:

```bash
az storage container generate-sas \
  --account-name <name> \
  --name data \
  --permissions r \
  --expiry 2026-07-11T00:00Z \
  --auth-mode login \
  --as-user
```

Exam hook: `--as-user` means user delegation SAS, backed by Microsoft Entra ID rather than the account key.

## AzCopy

AzCopy is separate from Azure CLI. It is the bulk transfer tool.

| Task                    | Command                                                                                 |
| ----------------------- | --------------------------------------------------------------------------------------- |
| Sign in                 | `azcopy login`                                                                          |
| Copy one file           | `azcopy copy ./file.txt "https://<account>.blob.core.windows.net/data/file.txt?<sas>"`  |
| Copy folder recursively | `azcopy copy ./folder "https://<account>.blob.core.windows.net/data?<sas>" --recursive` |
| Sync folders            | `azcopy sync ./folder "https://<account>.blob.core.windows.net/data?<sas>" --recursive` |

Exam hook: Azure CLI manages Azure resources; AzCopy moves lots of data.

## Virtual Machines

| Task                      | Command                                                                                                                      |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| Create VM                 | `az vm create --resource-group rg-lab --name vm-lab --image Ubuntu2204 --admin-username azureuser --generate-ssh-keys`       |
| List VMs                  | `az vm list --resource-group rg-lab --output table`                                                                          |
| Show VM power state       | `az vm get-instance-view --resource-group rg-lab --name vm-lab --query instanceView.statuses[].displayStatus --output table` |
| Stop billing for compute  | `az vm deallocate --resource-group rg-lab --name vm-lab`                                                                     |
| Start VM                  | `az vm start --resource-group rg-lab --name vm-lab`                                                                          |
| Resize VM                 | `az vm resize --resource-group rg-lab --name vm-lab --size Standard_B2s`                                                     |
| Run command on VM         | `az vm run-command invoke --resource-group rg-lab --name vm-lab --command-id RunShellScript --scripts "hostname"`            |
| List VM sizes in a region | `az vm list-sizes --location eastus --output table`                                                                          |

Exam hook: `stop` stops the OS; `deallocate` stops compute billing.

## Disks and Snapshots

| Task                  | Command                                                                                |
| --------------------- | -------------------------------------------------------------------------------------- |
| List disks            | `az disk list --resource-group rg-lab --output table`                                  |
| Create managed disk   | `az disk create --resource-group rg-lab --name disk-data --size-gb 32`                 |
| Attach disk to VM     | `az vm disk attach --resource-group rg-lab --vm-name vm-lab --name disk-data`          |
| Create snapshot       | `az snapshot create --resource-group rg-lab --name snap-data --source disk-data`       |
| List unattached disks | `az disk list --query "[?managedBy==null].{Name:name,Size:diskSizeGb}" --output table` |

Lab safety: unattached disks still cost money.

## App Service

| Task                    | Command                                                                                                            |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------ |
| Create App Service plan | `az appservice plan create --name plan-lab --resource-group rg-lab --sku B1 --is-linux`                            |
| Create web app          | `az webapp create --resource-group rg-lab --plan plan-lab --name <unique-app-name> --runtime "NODE:20-lts"`        |
| List web apps           | `az webapp list --resource-group rg-lab --output table`                                                            |
| Scale up plan           | `az appservice plan update --name plan-lab --resource-group rg-lab --sku S1`                                       |
| Create deployment slot  | `az webapp deployment slot create --resource-group rg-lab --name <app-name> --slot staging`                        |
| Swap slots              | `az webapp deployment slot swap --resource-group rg-lab --name <app-name> --slot staging --target-slot production` |

Exam hook: deployment slots and autoscale require Standard tier or higher.

## Containers

| Task                              | Command                                                                                                                                                                                       |
| --------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Create Azure Container Registry   | `az acr create --resource-group rg-lab --name <uniqueacrname> --sku Basic`                                                                                                                    |
| List registries                   | `az acr list --resource-group rg-lab --output table`                                                                                                                                          |
| Create Azure Container Instance   | `az container create --resource-group rg-lab --name aci-lab --image mcr.microsoft.com/azuredocs/aci-helloworld --ports 80 --dns-name-label <unique-label>`                                    |
| Show container logs               | `az container logs --resource-group rg-lab --name aci-lab`                                                                                                                                    |
| Create Container Apps environment | `az containerapp env create --name cae-lab --resource-group rg-lab --location eastus`                                                                                                         |
| Create Container App              | `az containerapp create --name app-lab --resource-group rg-lab --environment cae-lab --image mcr.microsoft.com/azuredocs/containerapps-helloworld:latest --ingress external --target-port 80` |

Exam hook: ACI is quick single-container hosting; Container Apps supports microservices, revisions, and scale to zero.

## Virtual Networking

| Task                    | Command                                                                                                                                                                                                 |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Create VNet and subnet  | `az network vnet create --resource-group rg-lab --name vnet-lab --address-prefix 10.0.0.0/16 --subnet-name snet-app --subnet-prefix 10.0.1.0/24`                                                        |
| Add subnet              | `az network vnet subnet create --resource-group rg-lab --vnet-name vnet-lab --name snet-data --address-prefix 10.0.2.0/24`                                                                              |
| Create NSG              | `az network nsg create --resource-group rg-lab --name nsg-app`                                                                                                                                          |
| Add NSG rule            | `az network nsg rule create --resource-group rg-lab --nsg-name nsg-app --name allow-http --priority 100 --direction Inbound --access Allow --protocol Tcp --destination-port-ranges 80`                 |
| Associate NSG to subnet | `az network vnet subnet update --resource-group rg-lab --vnet-name vnet-lab --name snet-app --network-security-group nsg-app`                                                                           |
| Create route table      | `az network route-table create --resource-group rg-lab --name rt-app`                                                                                                                                   |
| Add UDR                 | `az network route-table route create --resource-group rg-lab --route-table-name rt-app --name default-to-fw --address-prefix 0.0.0.0/0 --next-hop-type VirtualAppliance --next-hop-ip-address 10.0.3.4` |
| Create peering          | `az network vnet peering create --resource-group rg-lab --name peer-a-to-b --vnet-name vnet-a --remote-vnet vnet-b --allow-vnet-access`                                                                 |

Exam hook: peering is not transitive, and address spaces cannot overlap.

## DNS and Private Connectivity

| Task                      | Command                                                                                                                                                                                                                 |
| ------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Create public DNS zone    | `az network dns zone create --resource-group rg-lab --name contoso.com`                                                                                                                                                 |
| Add A record              | `az network dns record-set a add-record --resource-group rg-lab --zone-name contoso.com --record-set-name www --ipv4-address 10.0.0.4`                                                                                  |
| Create private DNS zone   | `az network private-dns zone create --resource-group rg-lab --name privatelink.blob.core.windows.net`                                                                                                                   |
| Link private zone to VNet | `az network private-dns link vnet create --resource-group rg-lab --zone-name privatelink.blob.core.windows.net --name link-vnet-lab --virtual-network vnet-lab --registration-enabled false`                            |
| Create private endpoint   | `az network private-endpoint create --resource-group rg-lab --name pe-storage --vnet-name vnet-lab --subnet snet-data --private-connection-resource-id <resource-id> --group-id blob --connection-name pe-storage-conn` |

Exam hook: private endpoints usually require a matching `privatelink.*` private DNS zone.

## Load Balancing

| Task                 | Command                                                                                                                                                                                                             |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Create public IP     | `az network public-ip create --resource-group rg-lab --name pip-lb --sku Standard`                                                                                                                                  |
| Create load balancer | `az network lb create --resource-group rg-lab --name lb-web --sku Standard --public-ip-address pip-lb --frontend-ip-name fe-web --backend-pool-name be-web`                                                         |
| Create health probe  | `az network lb probe create --resource-group rg-lab --lb-name lb-web --name hp-http --protocol Tcp --port 80`                                                                                                       |
| Create LB rule       | `az network lb rule create --resource-group rg-lab --lb-name lb-web --name rule-http --protocol Tcp --frontend-port 80 --backend-port 80 --frontend-ip-name fe-web --backend-pool-name be-web --probe-name hp-http` |

Exam hook: Load Balancer is layer 4; Application Gateway is layer 7 HTTP/HTTPS with WAF and path/host routing.

## Monitoring

| Task                           | Command                                                                                                  |
| ------------------------------ | -------------------------------------------------------------------------------------------------------- |
| List metrics for a resource    | `az monitor metrics list --resource <resource-id> --metric "Percentage CPU"`                             |
| Create action group            | `az monitor action-group create --resource-group rg-lab --name ag-ops --short-name ops`                  |
| List activity log events       | `az monitor activity-log list --resource-group rg-lab --output table`                                    |
| Create Log Analytics workspace | `az monitor log-analytics workspace create --resource-group rg-lab --workspace-name law-lab`             |
| Query logs                     | `az monitor log-analytics query --workspace <workspace-id> --analytics-query "AzureActivity \| take 10"` |

Network Watcher:

| Task                | Command                                                                                                                                            |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| Verify NSG decision | `az network watcher test-ip-flow --resource-group rg-lab --vm vm-lab --direction Outbound --protocol TCP --local 10.0.1.4:* --remote 10.0.2.4:443` |
| Check next hop      | `az network watcher show-next-hop --resource-group rg-lab --vm vm-lab --source-ip 10.0.1.4 --dest-ip 10.0.2.4`                                     |

Exam hook: IP flow verify checks NSG allow/deny; next hop checks routing.

## Backup

| Task                           | Command                                                                                                                                                  |
| ------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Create Recovery Services vault | `az backup vault create --resource-group rg-lab --name rsv-lab --location eastus`                                                                        |
| Set vault context              | `az backup vault backup-properties set --resource-group rg-lab --name rsv-lab --backup-storage-redundancy LocallyRedundant`                              |
| List backup policies           | `az backup policy list --resource-group rg-lab --vault-name rsv-lab --output table`                                                                      |
| Enable VM backup               | `az backup protection enable-for-vm --resource-group rg-lab --vault-name rsv-lab --vm vm-lab --policy-name DefaultPolicy`                                |
| Start on-demand backup         | `az backup protection backup-now --resource-group rg-lab --vault-name rsv-lab --container-name <container> --item-name <item> --retain-until 2026-08-10` |

Exam hook: Azure Backup restores data; Azure Site Recovery fails over workloads to another region.

## ARM and Bicep

| Task                              | Command                                                                               |
| --------------------------------- | ------------------------------------------------------------------------------------- |
| Deploy Bicep to resource group    | `az deployment group create --resource-group rg-lab --template-file main.bicep`       |
| Deploy ARM JSON to resource group | `az deployment group create --resource-group rg-lab --template-file azuredeploy.json` |
| Validate deployment               | `az deployment group validate --resource-group rg-lab --template-file main.bicep`     |
| Preview changes                   | `az deployment group what-if --resource-group rg-lab --template-file main.bicep`      |
| Convert Bicep to ARM JSON         | `az bicep build --file main.bicep`                                                    |
| Convert ARM JSON to Bicep         | `az bicep decompile --file azuredeploy.json`                                          |

Exam hook: incremental mode is the default; complete mode can delete resources not in the template.

## Azure AI and Foundry Recognition

| Task                              | Command                                                                                                                  |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| Create Azure AI services resource | `az cognitiveservices account create --name ai-lab --resource-group rg-lab --location eastus --kind AIServices --sku S0` |
| Show endpoint                     | `az cognitiveservices account show --name ai-lab --resource-group rg-lab --query properties.endpoint --output tsv`       |
| List keys                         | `az cognitiveservices account keys list --name ai-lab --resource-group rg-lab`                                           |

Exam hook: CLI commands provision and inspect resources; SDK and REST calls interact with deployed models from application code.

## Data Service Recognition

| Task                          | Command                                                                                                                                       |
| ----------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| Create Azure SQL server       | `az sql server create --resource-group rg-lab --name <unique-sql-server> --location eastus --admin-user sqladmin --admin-password <password>` |
| Create Azure SQL database     | `az sql db create --resource-group rg-lab --server <server-name> --name db-lab --service-objective Basic`                                     |
| Create Cosmos DB account      | `az cosmosdb create --resource-group rg-lab --name <unique-cosmos-name>`                                                                      |
| Create Cosmos DB SQL database | `az cosmosdb sql database create --resource-group rg-lab --account-name <account-name> --name db-lab`                                         |

Exam hook: DP-900 tests service selection more than command syntax, but command names help you recognize the service family.

## Cost Safety Commands

| Task                             | Command                                                                                                           |
| -------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| List all resources in lab group  | `az resource list --resource-group rg-lab --output table`                                                         |
| List public IPs                  | `az network public-ip list --resource-group rg-lab --output table`                                                |
| List disks, including unattached | `az disk list --resource-group rg-lab --query "[].{Name:name,Attached:managedBy,Size:diskSizeGb}" --output table` |
| List App Service plans           | `az appservice plan list --resource-group rg-lab --output table`                                                  |
| List container groups            | `az container list --resource-group rg-lab --output table`                                                        |
| Delete lab resource group        | `az group delete --name rg-lab --yes`                                                                             |

Always remove locks before deleting a lab resource group:

```bash
az lock list --resource-group rg-lab --output table
az lock delete --name <lock-name> --resource-group rg-lab
```

## Exam Traps

| Trap                                       | Correct thinking                                                        |
| ------------------------------------------ | ----------------------------------------------------------------------- |
| Running commands in the wrong subscription | Check `az account show` before creating resources                       |
| Deleting the wrong resource group          | List resources first; resource group delete is broad                    |
| Stopping a VM but not deallocating it      | Use `az vm deallocate` to stop compute billing                          |
| Forgetting disks bill after VM deletion    | Check unattached disks with `az disk list`                              |
| Confusing Azure CLI and AzCopy             | CLI manages resources; AzCopy transfers data                            |
| Expecting RBAC to bypass Policy            | Both must pass; Policy can deny valid RBAC actions                      |
| Calling a model catalog name from code     | Apps call deployment names, not raw catalog names                       |
| Using service endpoints from on-premises   | Private endpoints are the private-IP option that works from on-premises |
