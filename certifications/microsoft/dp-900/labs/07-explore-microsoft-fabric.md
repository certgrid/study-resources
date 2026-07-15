# Lab 07 - Explore Microsoft Fabric

The current DP-900 outline names Microsoft Fabric as a large-scale analytics service. The free trial lets you see workspaces, the lakehouse, and OneLake without touching your Azure subscription.

## Time Needed

25-30 minutes.

## What You Will Learn

- How Fabric is SaaS: no servers, no resource groups
- What a workspace and a lakehouse are
- Where OneLake fits
- Which Fabric experiences map to which analytics jobs

## DP-900 Concepts Covered

| Concept          | Where you see it in the lab                                |
| ---------------- | ---------------------------------------------------------- |
| Microsoft Fabric | You use the all-in-one SaaS analytics platform             |
| Lakehouse        | You create one and load a file into a table                |
| OneLake          | Your lakehouse data lands in the shared lake automatically |
| Data ingestion   | You upload and convert a CSV file to a table               |

## Cost Warning

The Fabric trial is free for a limited period (currently around 60 days). It uses a work or school account, not your personal Azure subscription. If your organization blocks trials, read through the steps and screenshots on Microsoft Learn instead; the concepts still land.

## Steps

### 1. Start the Fabric trial

1. Go to app.fabric.microsoft.com and sign in with a work or school account.
2. Open the account manager (top right) and select **Start trial** (or **Free trial**) if offered.

### 2. Create a workspace

1. Select **Workspaces** in the left navigation, then **New workspace**.
2. Name:

```text
ws-dp900-lab
```

3. A workspace is the collaboration container for Fabric items, similar to how a resource group holds Azure resources.

### 3. Create a lakehouse

1. In the workspace, select **New item** and choose **Lakehouse**.
2. Name it `lh_dp900`.
3. Notice the lakehouse gets two sections: **Files** (raw files in OneLake) and **Tables** (managed tables you can query).

### 4. Ingest a small file

1. On your computer, create a file named `sales.csv` with this content:

```text
Region,Amount
West,100
East,150
West,200
```

2. In the lakehouse, use **Get data > Upload files** and upload `sales.csv` into Files.
3. Right-click (or use the ... menu on) the uploaded file and choose **Load to Tables**. Fabric converts the CSV into a queryable Delta table.

### 5. Query the table

1. Switch to the **SQL analytics endpoint** (top-right dropdown in the lakehouse).
2. Run:

```sql
SELECT Region, SUM(Amount) AS Total
FROM sales
GROUP BY Region;
```

You just did the pipeline in miniature: ingest (upload), store (OneLake files), process (load to table), and query (SQL). Power BI reporting over this same data is Lab 08.

### 6. Spot the other experiences

Use the workload switcher (bottom left) to see the experiences: Data Factory, Data Engineering, Data Warehouse, Real-Time Intelligence, Data Science, Power BI. Match each to its purpose from study note 04.

## Clean Up

Delete the workspace when finished (Workspace settings > General > Remove this workspace), or let the trial expire. Nothing here bills your Azure subscription.

## Success Criteria

You are done when you can explain:

- Why Fabric is SaaS while Azure SQL Database is PaaS
- What a lakehouse's Files and Tables sections each hold
- What OneLake is and which workloads share it
- Which Fabric experience you would use for pipelines, warehousing, and real-time queries
