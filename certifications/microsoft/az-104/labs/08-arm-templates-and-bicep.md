# Lab 08 - Export and Redeploy with ARM Templates and Bicep

The exam expects you to READ templates more than write them. This lab exports a real template, identifies its sections, converts it to Bicep, and redeploys it.

## Time Needed

30-35 minutes.

## What You Will Learn

- The sections of an ARM template and a Bicep file
- How to export a template from an existing resource
- How to decompile ARM JSON to Bicep and deploy it
- What incremental vs complete mode would do

## AZ-104 Concepts Covered

| Concept           | Where you see it in the lab                         |
| ----------------- | --------------------------------------------------- |
| Export template   | You export from a storage account                   |
| Template sections | You identify parameters/variables/resources/outputs |
| Bicep             | You decompile and read the Bicep version            |
| Deployment        | You deploy with az deployment group create          |
| Idempotency       | You redeploy and observe no changes                 |

## Cost Warning

Nearly free: the deployment creates one standard LRS storage account. Delete it in Clean Up.

## Steps

### 1. Export a template

1. Open the lab storage account (or any resource in `rg-az104-labs`).
2. Select **Automation > Export template**.
3. Read the JSON: find `parameters`, `resources`, the resource `type` (Microsoft.Storage/storageAccounts), `apiVersion`, and `properties`.
4. Also visit **rg-az104-labs > Deployments**: every portal creation was actually a template deployment; open one and view its template.

### 2. Save a working template

In Cloud Shell:

```bash
mkdir ~/lab08 && cd ~/lab08
az group export --name rg-az104-labs > exported.json
```

(If the export errors on unsupported resources, use the single-resource export from step 1: copy it into `exported.json` with the built-in editor `code exported.json`.)

### 3. Decompile to Bicep

```bash
az bicep decompile --file exported.json
code exported.bicep
```

Compare the two files:

| ARM JSON                 | Bicep                       |
| ------------------------ | --------------------------- |
| "parameters": { ... }    | param name type = default   |
| "variables": { ... }     | var name = value            |
| "resources": [ { ... } ] | resource sym 'type@version' |
| "outputs": { ... }       | output name type = value    |
| dependsOn explicit       | mostly inferred             |

### 4. Write and deploy a minimal Bicep file

Create `main.bicep` with the editor:

```bicep
param location string = resourceGroup().location
param name string = 'staz104bicep${uniqueString(resourceGroup().id)}'

resource sa 'Microsoft.Storage/storageAccounts@2023-01-01' = {
  name: name
  location: location
  sku: { name: 'Standard_LRS' }
  kind: 'StorageV2'
}

output accountName string = sa.name
```

Deploy it:

```bash
az deployment group create --resource-group rg-az104-labs --template-file main.bicep
```

Note the output value at the end: outputs return information from deployments.

### 5. Prove idempotency and know the modes

1. Run the exact same deployment command again: it succeeds with no changes. Declarative + idempotent.
2. Recognition check, do NOT run: `--mode Complete` would DELETE everything in the resource group not described by the template. Incremental (default) leaves extra resources alone.
3. PowerShell equivalent to recognize: `New-AzResourceGroupDeployment -ResourceGroupName rg-az104-labs -TemplateFile main.bicep`.

## Clean Up

```bash
az storage account delete --name <the-output-account-name> --resource-group rg-az104-labs --yes
rm -rf ~/lab08
```

## Success Criteria

You are done when you can explain:

- The four ARM template sections and their Bicep equivalents
- Two ways to get a template from existing resources (export, deployment history)
- What incremental vs complete mode does to resources not in the template
- Why running the same deployment twice is safe
