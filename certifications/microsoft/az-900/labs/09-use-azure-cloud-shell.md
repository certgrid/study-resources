# Lab 09 - Use Azure Cloud Shell

Cloud Shell gives you browser-based access to Azure CLI and PowerShell without installing tools locally.

## Time Needed

15-20 minutes.

## What You Will Learn

- What Azure Cloud Shell is
- Difference between Bash and PowerShell modes
- How to list basic Azure resources
- Why Cloud Shell is useful for automation

## AZ-900 Concepts Covered

| Concept          | Where you see it in the lab                |
| ---------------- | ------------------------------------------ |
| Cloud Shell      | You open browser-based command-line access |
| Azure CLI        | You run basic `az` commands                |
| Azure PowerShell | You identify PowerShell as an alternative  |
| Automation       | You learn why command-line tools matter    |

## Steps

### 1. Open Cloud Shell

1. Open the Azure portal.
2. Select the Cloud Shell icon in the top bar.
3. Choose Bash or PowerShell.

If prompted to create storage for Cloud Shell, read the prompt carefully. Some environments require a storage account for persisted files.

### 2. Check your account

In Bash mode, run:

```bash
az account show
```

This shows the current subscription context.

### 3. List resource groups

Run:

```bash
az group list --output table
```

### 4. List storage accounts

Run:

```bash
az storage account list --output table
```

### 5. Switch to PowerShell

Use the Cloud Shell menu to switch to PowerShell. Notice that Azure supports both Azure CLI and Azure PowerShell for automation.

## Clean Up

If Cloud Shell created storage and you no longer need it, review the storage account and remove it when safe. Do not delete shared or production resources.

## Success Criteria

You are done when you can explain:

- What Cloud Shell is
- Why Azure CLI and Azure PowerShell are useful
- What a subscription context means
- How command-line tools help automate Azure tasks

