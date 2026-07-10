# Lab 00 - Set Up Your AZ-104 Lab Environment

AZ-104 labs create real resources, and some (VMs, scale sets, load balancers) cost real money. This lab builds the safety net first: a dedicated resource group, a budget with alerts, and cost rules you will follow in every later lab.

## Time Needed

15-20 minutes.

## What You Will Learn

- How to isolate all lab work in one resource group for easy cleanup
- How to create a budget and cost alert before spending anything
- The cost-safety habits that make associate-level labs safe
- Where Cloud Shell lives, since many labs use CLI commands

## AZ-104 Concepts Covered

| Concept         | Where you see it in the lab                    |
| --------------- | ---------------------------------------------- |
| Resource groups | You create the container for all lab resources |
| Tags            | You tag the group for identification           |
| Cost Management | You create a budget and an alert               |
| Cloud Shell     | You verify CLI and PowerShell access           |

## Cost Warning

This lab itself is free. But set the budget NOW: later labs deploy VMs and load balancers that bill by the hour. The golden rules for this whole series:

1. Always deploy into the lab resource group.
2. Always pick the cheapest SKU the lab names.
3. Delete or deallocate expensive resources at the END of each lab, not "later".
4. If you stop mid-lab, run the lab's Clean Up section before walking away.

## Steps

### 1. Create the lab resource group

1. Sign in to the Azure portal.
2. Search for **Resource groups** and select **Create**.
3. Name it:

```text
rg-az104-labs
```

4. Choose a region close to you and remember it; use the same region in every lab.
5. Add tags:

| Name        | Value  |
| ----------- | ------ |
| Environment | Lab    |
| Exam        | AZ-104 |

6. Select **Review + create**, then **Create**.

### 2. Create a budget with alerts

1. Search for **Cost Management**, open **Budgets**, and select **Add**.
2. Scope it to your subscription.
3. Name: `budget-az104-labs`, monthly reset, amount: an amount you are comfortable with (e.g. 20).
4. Add alert conditions at 50%, 80%, and 100% of actual cost, plus 100% forecasted.
5. Enter your email as the alert recipient and create the budget.

### 3. Verify Cloud Shell

1. Select the Cloud Shell icon in the portal top bar.
2. Choose **Bash** (or PowerShell) and let it create its small storage account if prompted.
3. Run both commands to confirm the two tool styles:

```bash
az group show --name rg-az104-labs --output table
```

```powershell
Get-AzResourceGroup -Name rg-az104-labs
```

Notice the naming patterns: `az noun verb` for CLI, `Verb-AzNoun` for PowerShell. The exam tests recognition of both.

### 4. Bookmark the cost page

Open **Cost Management > Cost analysis**, filter by resource group `rg-az104-labs`, and pin or bookmark it. Check it after every VM lab.

## Clean Up

Keep the resource group and budget; every later lab uses them. Nothing in this lab generates meaningful cost (the Cloud Shell storage account is a few cents per month; you can delete it in the final cleanup lab).

## Success Criteria

You are done when you can explain:

- Why all labs share one resource group
- What a budget does and does not do (alerts, never blocks spending)
- The difference between the az and Az command styles
- Which later resources will need immediate cleanup (VMs, scale sets, load balancers, gateways)
