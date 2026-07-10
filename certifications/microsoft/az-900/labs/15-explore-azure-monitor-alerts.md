# Lab 15 - Explore Azure Monitor Alerts

Goal: understand how Azure Monitor collects telemetry and can trigger alerts.

This lab can be done as a review exercise. You do not need to create a paid workload.

## What you learn

- Azure Monitor collects metrics and logs
- Alerts are based on signals and conditions
- Action groups define who or what gets notified

## Steps

1. Open the Azure portal.
2. Search for **Monitor**.
3. Open **Metrics**.
4. Choose a resource if you have one, such as a storage account or virtual machine.
5. Review available metrics.
6. Open **Alerts**.
7. Select **Create** and review the alert rule flow:
   - Scope
   - Condition
   - Action group
   - Details
8. Cancel before creating the alert if you only want to learn the workflow.

## Monitoring terms

| Term                 | Meaning                                    |
| -------------------- | ------------------------------------------ |
| Metric               | Numeric measurement such as CPU percentage |
| Log                  | Detailed event or diagnostic record        |
| Alert rule           | Condition that triggers an alert           |
| Action group         | Notification or action target              |
| Application Insights | Application performance monitoring         |
| Log Analytics        | Workspace for querying logs                |

## Exam memory

If the question says "collect metrics", "collect logs", "configure alerts", or "monitor performance", choose Azure Monitor.

## Cleanup

If you created an alert rule or action group, delete it after the lab.
