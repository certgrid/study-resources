# Lab 00 - Set Up Your Lab Environment

Before the data labs, set up a safe environment: confirm your subscription, create one resource group for everything, and add a budget alert so nothing surprises you.

## Time Needed

15-20 minutes.

## What You Will Learn

- How to confirm you have a usable Azure subscription
- Why one resource group makes data labs easy to clean up
- How a budget alert protects you from unexpected cost
- Where the data services live in the Azure portal

## DP-900 Concepts Covered

| Concept        | Where you see it in the lab                              |
| -------------- | -------------------------------------------------------- |
| Azure portal   | You navigate to the data service categories              |
| Resource group | You create a single container for all lab resources      |
| Cost awareness | You create a budget with an alert                        |
| Data services  | You preview the SQL, storage, and Cosmos DB entry points |

## Cost Warning

Most labs in this pack use free tiers or the cheapest options, but Azure SQL, Cosmos DB, and storage can all bill if left running with paid settings. Always finish with [09 - Clean Up Resources](09-clean-up-resources.md).

## Steps

### 1. Sign in and check your subscription

1. Go to the Azure portal at portal.azure.com.
2. Search for **Subscriptions**.
3. Confirm you see an active subscription (free account, Pay-As-You-Go, or a sponsored one).

If you do not have an account yet, create a free account at azure.microsoft.com/free. The free account includes credits and 12 months of popular free services, including an Azure SQL Database free offer.

### 2. Create the lab resource group

1. Search for **Resource groups** and select **Create**.
2. Use this name:

```text
rg-dp900-labs
```

3. Choose a region close to you and remember it; use the same region in every lab.
4. Add tags:

| Name        | Value    |
| ----------- | -------- |
| Environment | Lab      |
| Exam        | DP-900   |
| Owner       | YourName |

5. Select **Review + create**, then **Create**.

### 3. Create a budget alert

1. Search for **Cost Management** and open **Budgets**.
2. Select **Add**.
3. Create a small monthly budget (for example 10 in your billing currency).
4. Add an alert at 80% of the budget with your email address.

### 4. Preview the data service categories

Search for each of these in the portal search bar so you know where they live:

- **SQL databases**
- **Storage accounts**
- **Azure Cosmos DB**

You do not need to create anything yet.

## Clean Up

Nothing to clean up yet. Keep the resource group; every following lab uses it.

## Success Criteria

You are done when you can explain:

- Which subscription your labs will bill against
- Why all lab resources go into rg-dp900-labs
- What happens when your budget alert threshold is crossed
- Where to find SQL databases, storage accounts, and Cosmos DB in the portal
