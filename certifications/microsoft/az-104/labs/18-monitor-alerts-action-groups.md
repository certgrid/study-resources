# Lab 18 - Azure Monitor Metrics, Alerts, and Action Groups

Alerting questions decompose into scope + condition + action group. This lab builds each piece by hand so the decomposition sticks.

## Time Needed

30-35 minutes.

## What You Will Learn

- How to explore metrics with aggregations and dimensions
- How to build a metric alert rule
- What an action group contains
- Where activity log alerts and alert processing rules live

## AZ-104 Concepts Covered

| Concept                | Where you see it in the lab               |
| ---------------------- | ----------------------------------------- |
| Metrics Explorer       | You chart VM and storage metrics          |
| Metric alert rule      | You alert on CPU percentage               |
| Action group           | You create email + (optional) SMS actions |
| Activity log alert     | You alert on VM deallocation events       |
| Alert processing rules | You locate the suppression feature        |

## Cost Warning

Small: metric alert rules cost ~0.10 per month each, action group emails are free, SMS costs cents. The VM must run briefly to emit metrics; deallocate it at the end. Delete the alert rules in Clean Up to stop their monthly trickle.

## Steps

### 1. Explore metrics

1. Start `vm-lab-01` (it needs to run to emit fresh metrics).
2. Open **Monitor > Metrics**.
3. Scope: `vm-lab-01`; metric: **Percentage CPU**; aggregation: Avg. Change the time range and granularity.
4. Add a second chart scoped to your lab storage account: metric **Transactions**, then **Apply splitting** by API name: dimensions splitting is an exam keyword.
5. Note what is NOT here: memory inside the guest OS. That needs the Azure Monitor agent + a data collection rule.

### 2. Create an action group

1. Open **Monitor > Alerts > Action groups > Create**.
2. Resource group `rg-az104-labs`, name `ag-lab-ops`, display name `LabOps`.
3. Notifications: Email = your address (add SMS if you accept the cents).
4. Actions tab: read the automation options without adding one: webhook, Azure Function, Logic App, Automation runbook, ITSM, Event Hub. Recognizing this list is exam material.
5. Create. You will receive a confirmation email: action groups verify their targets.

### 3. Create a metric alert rule

1. Open `vm-lab-01` > **Monitoring > Alerts > Create > Alert rule**.
2. Condition: signal **Percentage CPU**, threshold Static, aggregation Average, operator Greater than, value **5**, check every 1 minute over 5 minutes. (5% so it actually fires; production would use 80-90.)
3. Actions: select `ag-lab-ops`.
4. Details: severity **Sev 3**, name `alert-vm1-cpu`. Create.
5. Generate load or just wait: a running VM usually idles above 5% occasionally; when it fires you get the email, and the alert appears in **Monitor > Alerts** with state Fired (stateful alerts auto-resolve when the condition clears).

### 4. Create an activity log alert

1. **Monitor > Alerts > Create > Alert rule**; scope: your subscription.
2. Condition: signal category **Activity log**, pick **Deallocate Virtual Machine** (or Delete resource group for drama).
3. Action group `ag-lab-ops`; name `alert-vm-deallocate`. Create.
4. This is the "email me when someone deletes/stops X" answer: control-plane events come from the activity log, not metrics.

### 5. Find alert processing rules

Open **Monitor > Alerts > Alert processing rules**: read the create screen: scope + filter + "suppress notifications" or "apply action group", with schedules (e.g. every weekend). This is the maintenance-window answer. Cancel without creating.

### 6. Trigger and observe

Deallocate `vm-lab-01` now: this both cleans up AND fires your activity log alert within minutes: two birds, one stone. Check the email and **Monitor > Alerts**.

## Clean Up

Delete alert rules `alert-vm1-cpu` and `alert-vm-deallocate`, then the action group `ag-lab-ops` (Monitor > Alerts > Action groups). Confirm `vm-lab-01` shows Stopped (deallocated).

## Success Criteria

You are done when you can explain:

- The parts of an alert rule (scope, condition, severity, action group)
- Metric alert vs activity log alert vs log search alert
- Everything an action group can do besides email
- What alert processing rules add (suppression/attachment at scale)
- Why in-guest memory metrics need an agent
