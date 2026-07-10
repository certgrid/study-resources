# Lab 19 - Log Analytics and KQL Basics

The exam shows KQL snippets and asks what they return. This lab creates a workspace, routes real data into it, and runs the query patterns those questions use.

## Time Needed

30-35 minutes.

## What You Will Learn

- What a Log Analytics workspace is and its retention settings
- How diagnostic settings route data into it
- The KQL pattern: table | where | summarize | sort
- Where VM insights and data collection rules fit

## AZ-104 Concepts Covered

| Concept             | Where you see it in the lab              |
| ------------------- | ---------------------------------------- |
| Workspace           | You create law-az104-lab                 |
| Diagnostic settings | You route activity log + storage logs    |
| KQL                 | You query AzureActivity and AzureMetrics |
| Retention           | You find the retention setting           |
| VM insights / DCR   | You locate them for recognition          |

## Cost Warning

Log Analytics bills per GB ingested; this lab's data volume is tiny (well under a cent), and the first 5 GB per month are free on the default plan. Do not onboard VM insights on many machines in a paid tenant; here we only look at the screens.

## Steps

### 1. Create the workspace

1. Search **Log Analytics workspaces > Create**.
2. Resource group `rg-az104-labs`, name `law-az104-lab`, usual region.
3. After creation, open **Settings > Usage and estimated costs > Data retention**: interactive retention is configurable (default around 30 days, up to 730). Recognition only; leave defaults.

### 2. Route data with diagnostic settings

1. Open **Monitor > Activity log > Export activity logs**: add a diagnostic setting on your subscription: send **Administrative** and **Policy** categories to `law-az104-lab`.
2. Open your lab storage account > **Diagnostic settings** (under Monitoring) > add a setting on the **blob** service: send transaction metrics/logs to the workspace.
3. Pattern to memorize: resource -> diagnostic setting -> destination (workspace, storage account, or event hub).

### 3. Generate some activity

Do a few control-plane actions so AzureActivity has rows: add a tag somewhere, create and delete a dummy container in the storage account, upload a blob.

### 4. Query with KQL

Open `law-az104-lab` > **Logs** (close the query gallery). Data can lag 5-15 minutes; run these as it arrives:

```kusto
AzureActivity
| where TimeGenerated > ago(1h)
| project TimeGenerated, OperationNameValue, ActivityStatusValue, Caller
| sort by TimeGenerated desc
```

```kusto
AzureActivity
| where TimeGenerated > ago(24h)
| summarize count() by OperationNameValue
| sort by count_ desc
```

```kusto
AzureMetrics
| where TimeGenerated > ago(1h)
| summarize avg(Average) by MetricName, bin(TimeGenerated, 5m)
```

For each, name the pattern out loud: TABLE, filter with WHERE, shape with PROJECT/SUMMARIZE, order with SORT. That reading skill is what the exam tests: given a query, what does it return?

### 5. Recognition stops

1. **Monitor > Insights > Virtual machines**: the VM insights onboarding screen: performance + dependency map, powered by the Azure Monitor agent. Do not onboard.
2. **Monitor > Data Collection Rules**: DCRs define WHAT the agent collects and WHERE it lands. Read the create screen; cancel.
3. Log search alerts: in Logs, note the **New alert rule** button above a query: that is how a KQL result becomes an alert.

## Clean Up

Delete the two diagnostic settings (subscription activity log export and the storage blob setting), then delete `law-az104-lab` if you are not redoing this lab; the workspace itself is the ingestion point and tiny lab volumes cost effectively nothing while it exists.

## Success Criteria

You are done when you can explain:

- What a workspace stores and how data gets into it (diagnostic settings, agents/DCRs)
- The role of each KQL operator used above
- The difference between AzureActivity and AzureMetrics tables
- How a KQL query becomes an alert
- Where retention is configured and its range
