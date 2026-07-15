# Lab 01 - Create an Azure SQL Database

Azure SQL Database is the exam's flagship PaaS relational service. Creating one shows you exactly what Microsoft manages for you and what stays your responsibility.

## Time Needed

20-25 minutes (plus a few minutes of deployment time).

## What You Will Learn

- What a logical SQL server is and why a database needs one
- How service tiers and the serverless option affect cost
- What the AdventureWorksLT sample data gives you
- Which management tasks disappear with PaaS

## DP-900 Concepts Covered

| Concept            | Where you see it in the lab                      |
| ------------------ | ------------------------------------------------ |
| PaaS               | Microsoft handles OS, patching, and backups      |
| Azure SQL Database | You deploy a single managed database             |
| Structured data    | The sample database is tables with fixed schemas |
| Authentication     | You set an admin login for the logical server    |

## Cost Warning

If your subscription shows the "Apply free offer" banner for Azure SQL Database, use it. Otherwise pick **General Purpose - Serverless** with the minimum size and enable auto-pause. Delete the database in the cleanup lab either way.

## Steps

### 1. Start the create flow

1. In the Azure portal, search for **SQL databases**.
2. Select **Create**.
3. Choose subscription and the resource group:

```text
rg-dp900-labs
```

### 2. Name the database and create a server

1. Database name:

```text
sqldb-dp900-lab
```

2. Under Server, select **Create new**:
   - Server name must be globally unique, for example `sql-dp900-<yourname>`.
   - Location: your lab region.
   - Authentication method: **Use SQL authentication**.
   - Set an admin login and a strong password. Save these; you need them in Lab 02.

### 3. Choose cheap compute

1. If offered, apply the **free offer** for Azure SQL Database.
2. Otherwise select **Configure database**:
   - Service tier: **General Purpose**.
   - Compute tier: **Serverless**.
   - Set minimum vCores and enable auto-pause.

### 4. Load sample data

1. Go to the **Additional settings** tab.
2. For "Use existing data", select **Sample**. This loads the AdventureWorksLT sample database.

### 5. Create and explore

1. Select **Review + create**, then **Create**, and wait for deployment.
2. Open the database resource and look at:
   - **Overview**: server name, pricing tier, region.
   - **Compute + storage**: what scaling means in PaaS.
   - Notice there is no OS, no VM, and no patching anywhere.

## Clean Up

Keep the database for Lab 02. Cleanup happens in [09 - Clean Up Resources](09-clean-up-resources.md).

## Success Criteria

You are done when you can explain:

- Why Azure SQL Database is PaaS and not IaaS
- What the logical server provides (name, region, admin login)
- What the serverless tier does when the database is idle
- Which responsibilities you kept (schema, data, access) and which Microsoft took (OS, patching, backups)
