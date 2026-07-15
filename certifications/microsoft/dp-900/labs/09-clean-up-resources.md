# Lab 09 - Clean Up Resources

Cleanup is a real skill. Azure SQL and Cosmos DB accounts left running are the most common source of surprise bills for learners. This lab removes everything the pack created.

## Time Needed

10-15 minutes.

## What You Will Learn

- How deleting a resource group removes everything inside it
- Which resources bill even when "idle"
- How to verify nothing is left billing
- Why budgets and alerts still matter after cleanup

## DP-900 Concepts Covered

| Concept            | Where you see it in the lab                   |
| ------------------ | --------------------------------------------- |
| Resource lifecycle | You delete a resource group and its contents  |
| Cost management    | You verify spend and keep the budget alert    |
| PaaS billing       | You see which services billed during the labs |

## Steps

### 1. Review what exists

1. Open **Resource groups** and select `rg-dp900-labs`.
2. You should see some or all of: a SQL database and its logical server, a storage account, and a Cosmos DB account.

### 2. Delete the resource group

1. Select **Delete resource group**.
2. Type the resource group name to confirm:

```text
rg-dp900-labs
```

3. Confirm the deletion. Everything inside is removed together: this is the lifecycle benefit of grouping lab resources.

### 3. Check for strays

1. Open **All resources** and confirm nothing DP-900 related remains.
2. If you created anything outside the resource group by accident, delete it individually.

### 4. Clean up non-Azure items

| Item                      | Where                    | Action                                     |
| ------------------------- | ------------------------ | ------------------------------------------ |
| Fabric workspace          | app.fabric.microsoft.com | Workspace settings > Remove this workspace |
| Power BI report/dashboard | app.powerbi.com          | Delete from your workspace                 |
| Local CSV files           | Your computer            | Delete                                     |

### 5. Verify cost

1. Open **Cost Management > Cost analysis**.
2. Check what the labs actually cost (usually close to zero with free tiers and serverless options).
3. Keep the budget alert from Lab 00; it costs nothing and protects future experiments.

## Clean Up

This lab is the cleanup.

## Success Criteria

You are done when you can explain:

- Why deleting one resource group removed the server, database, and accounts together
- Which of your lab resources would have billed if left running
- Where you would check next month that spend is actually zero
- Why the budget alert is worth keeping
