# 05 - Monitor and Maintain Azure Resources

This domain is worth 10-15% of the exam, the smallest share, but the questions are very predictable: which Azure Monitor piece does what, which Network Watcher tool solves which problem, and Backup vs Site Recovery. Easy points if you know the component boundaries.

## Mental model

Azure Monitor is a pipeline: resources emit metrics (numbers, near real-time) and logs (records, queryable with KQL in a Log Analytics workspace). Alert rules watch signals and fire action groups (who/what to notify). Insights are curated dashboards on top. Maintenance is two different jobs: Azure Backup restores data; Azure Site Recovery fails over whole workloads to another region.

| Scenario keyword                               | Likely concept                         |
| ---------------------------------------------- | -------------------------------------- |
| "CPU percentage chart, near real-time"         | Metrics (Metrics Explorer)             |
| "Query events with a query language"           | Log Analytics + KQL                    |
| "Send platform logs somewhere"                 | Diagnostic settings                    |
| "Notify the on-call team by SMS/email"         | Action group                           |
| "Suppress alerts during maintenance windows"   | Alert processing rules                 |
| "Deep VM performance: processes, dependencies" | VM insights                            |
| "Was traffic allowed between these VMs?"       | Network Watcher IP flow verify         |
| "Monitor a connection over time"               | Connection monitor                     |
| "Daily restore points for a VM"                | Azure Backup (Recovery Services vault) |
| "Fail over VMs to another region"              | Azure Site Recovery                    |
| "Central view of backup jobs and alerts"       | Backup center / backup reports         |

## Azure Monitor components

| Component                 | What it does                                                                               |
| ------------------------- | ------------------------------------------------------------------------------------------ |
| Metrics                   | Numeric time-series (CPU %, disk IOPS); stored 93 days; near real-time                     |
| Logs                      | Event/record data in a Log Analytics workspace; queried with KQL                           |
| Diagnostic settings       | Route platform metrics/logs to a workspace, storage account, or event hub                  |
| Activity log              | Subscription-level control-plane events (who created/deleted what); 90 days free           |
| Alerts                    | Rules on metrics, logs, or the activity log that trigger actions                           |
| Action groups             | Reusable notification/action lists (email, SMS, webhook, runbook, function, ITSM)          |
| Alert processing rules    | Post-fire handling: suppress alerts or attach action groups at scale                       |
| Insights                  | Curated experiences: VM insights, Storage insights, Network insights, Application Insights |
| Azure Monitor agent (AMA) | Collects guest OS data from VMs via data collection rules (DCRs)                           |

### Metrics vs logs

| Aspect  | Metrics                       | Logs                                                                      |
| ------- | ----------------------------- | ------------------------------------------------------------------------- |
| Data    | Numbers sampled over time     | Structured records/events                                                 |
| Latency | Near real-time                | Minutes                                                                   |
| Storage | Platform (93 days)            | Log Analytics workspace (retention configurable, 31-730 days interactive) |
| Query   | Metrics Explorer              | KQL                                                                       |
| Cost    | Included for platform metrics | Pay per GB ingested + retention                                           |

### Interpreting metrics

- Metrics Explorer: pick scope (resource), metric, aggregation (avg, min, max, sum, count), time range and granularity.
- Split by dimension (e.g. per LUN, per instance) to find the noisy component.
- Guest OS metrics (memory inside a VM) need the Azure Monitor agent; host metrics (CPU %, disk) come free.

### Log Analytics and KQL

Recognition-level KQL:

```kusto
Heartbeat
| where TimeGenerated > ago(1h)
| summarize count() by Computer
| sort by count_ desc
```

| KQL piece     | Meaning                                                     |
| ------------- | ----------------------------------------------------------- |
| Table name    | Source data (Heartbeat, Perf, AzureActivity, Event, Syslog) |
| where         | Filter rows                                                 |
| summarize     | Aggregate (count(), avg(), max()) by columns                |
| project       | Select/rename columns                                       |
| sort by / top | Order results / take first N                                |

Key facts:

- A Log Analytics workspace is a regional resource; one workspace can collect from many subscriptions/regions.
- Access modes: workspace-context vs resource-context (users with resource access can query that resource's logs).
- Data collection rules (DCRs) define what the Azure Monitor agent collects and where it lands.

### Alerts

| Alert rule part    | Meaning                                                    |
| ------------------ | ---------------------------------------------------------- |
| Scope              | The resource(s) to watch                                   |
| Condition (signal) | Metric threshold, log query result, or activity log event  |
| Severity           | Sev 0 (critical) to Sev 4 (verbose)                        |
| Action group       | Who is notified and what runs                              |
| Alert state        | Fired, acknowledged, closed (stateful alerts auto-resolve) |

| Alert type           | Fires on                                       | Example                                 |
| -------------------- | ---------------------------------------------- | --------------------------------------- |
| Metric alert         | Threshold on a metric                          | VM CPU > 85% for 15 minutes             |
| Log search alert     | KQL query result count/threshold on a schedule | More than 5 failed logons in 10 minutes |
| Activity log alert   | Control-plane event                            | Someone deleted a resource group        |
| Service Health alert | Azure service issues/maintenance               | Outage notification for your regions    |

Action group actions: email/SMS/push/voice notifications, plus automation: webhook, Azure Function, Logic App, Automation runbook, ITSM ticket, Event Hub.

Alert processing rules: apply/suppress action groups across many alerts (e.g. silence non-critical alerts every Saturday during patching).

### Azure Monitor Insights (know the names)

| Insight              | Monitors                                                      |
| -------------------- | ------------------------------------------------------------- |
| VM insights          | VM performance (CPU, memory, disk) and process dependency map |
| Storage insights     | Storage capacity, transactions, latency, availability         |
| Network insights     | Topology, NSG/LB health, Network Watcher integration          |
| Application Insights | Application-level telemetry (requests, failures, traces); APM |

## Network Watcher

Regional service for network diagnostics; enabled per region automatically when you create a VNet.

| Tool                           | Answers the question                                                 |
| ------------------------------ | -------------------------------------------------------------------- |
| IP flow verify                 | "Would this packet be allowed to/from this VM?" (names the NSG rule) |
| Next hop                       | "Where does traffic from this VM go next?" (routing problems)        |
| Connection troubleshoot        | "Can source reach destination right now, and where does it break?"   |
| Connection monitor             | "Track reachability/latency continuously over time"                  |
| Packet capture                 | "Record actual traffic on a VM for analysis"                         |
| NSG flow logs / VNet flow logs | "Log allowed/denied flows for audit and analysis"                    |
| Topology                       | "Show me a diagram of this VNet's resources"                         |
| Effective security rules       | "What is the combined NSG result on this NIC?"                       |

Memory hook: one-shot rule check = IP flow verify; routing = next hop; live path test = connection troubleshoot; ongoing = connection monitor; raw traffic = packet capture.

## Backup and recovery

### The two vaults

| Vault                   | Protects                                                                       |
| ----------------------- | ------------------------------------------------------------------------------ |
| Recovery Services vault | Azure VMs, SQL/SAP in VMs, Azure Files, on-premises (MARS/MABS), Site Recovery |
| Backup vault            | Newer workloads: Azure Disks, Azure Blobs, Azure Database for PostgreSQL       |

Both use vault-level redundancy (LRS/ZRS/GRS) chosen BEFORE the first backup; cross-region restore is an option on GRS vaults.

### Azure Backup for VMs

| Item                | Detail                                                                |
| ------------------- | --------------------------------------------------------------------- |
| Backup policy       | Schedule (frequency/time) + retention (daily/weekly/monthly/yearly)   |
| Policy types        | Standard (once daily) vs Enhanced (multiple per day, zone support)    |
| First step          | Create the vault in the SAME region as the VMs                        |
| Restore options     | Create new VM, replace disks, restore disks only, file-level recovery |
| File-level recovery | Mounts a restore point as a drive via script; copy individual files   |
| Soft delete         | Deleted backup data retained 14 days by default                       |
| Stop protection     | Options: retain data or delete backup data                            |

Key facts:

- A VM can only be backed up to a vault in the same region.
- To delete a vault you must first stop backups and remove all protected items and dependencies.
- Azure Files can be backed up (snapshot-based) into a Recovery Services vault.

### Azure Site Recovery (ASR)

| Item          | Detail                                                           |
| ------------- | ---------------------------------------------------------------- |
| Purpose       | Disaster recovery: replicate VMs to another region and fail over |
| Key metrics   | RPO (data loss window) and RTO (downtime window)                 |
| Test failover | Non-disruptive DR drill into an isolated network                 |
| Failover      | Planned/unplanned switch to the secondary region                 |
| Failback      | Re-protect and return to the primary after it recovers           |
| Recovery plan | Ordered groups of VMs + scripts for orchestrated failover        |

### Backup vs Site Recovery (the classic pair)

| Aspect   | Azure Backup                            | Azure Site Recovery                                    |
| -------- | --------------------------------------- | ------------------------------------------------------ |
| Goal     | Restore data (files, disks, VMs)        | Keep workloads RUNNING via failover                    |
| Scenario | Deletion, corruption, ransomware        | Region outage, DR requirements                         |
| Cadence  | Scheduled restore points                | Continuous replication                                 |
| Wording  | "Restore", "retention", "recover files" | "Failover", "replicate", "secondary region", "RTO/RPO" |

### Backup reports and alerts

- Backup center: single pane for jobs, policies, and alerts across vaults.
- Backup reports use Log Analytics (diagnostic settings on the vault) for historical analysis.
- Built-in Azure Monitor alerts fire for backup failures and security events (e.g. stop with delete).

## Limits and numbers to memorize

| Item                                     | Value                                             |
| ---------------------------------------- | ------------------------------------------------- |
| Platform metrics retention               | 93 days                                           |
| Activity log retention (free)            | 90 days                                           |
| Log Analytics interactive retention      | 31-730 days configurable (30/31 default by table) |
| Alert severity levels                    | Sev 0-4 (0 most severe)                           |
| Backup soft delete retention (default)   | 14 days                                           |
| Vault redundancy choice                  | Must be set before the first backup               |
| VM backup vault region rule              | Vault must be in the same region as VM            |
| Standard vs Enhanced VM backup frequency | Once daily vs multiple per day                    |

## CLI and PowerShell recognition

| Task                             | Azure CLI                                 | PowerShell                                |
| -------------------------------- | ----------------------------------------- | ----------------------------------------- |
| Create a Log Analytics workspace | az monitor log-analytics workspace create | New-AzOperationalInsightsWorkspace        |
| Query logs                       | az monitor log-analytics query            | Invoke-AzOperationalInsightsQuery         |
| Create a metric alert            | az monitor metrics alert create           | Add-AzMetricAlertRuleV2                   |
| Create an action group           | az monitor action-group create            | New-AzActionGroup                         |
| Create a diagnostic setting      | az monitor diagnostic-settings create     | New-AzDiagnosticSetting                   |
| Create a Recovery Services vault | az backup vault create                    | New-AzRecoveryServicesVault               |
| Enable VM backup                 | az backup protection enable-for-vm        | Enable-AzRecoveryServicesBackupProtection |
| Trigger a backup now             | az backup protection backup-now           | Backup-AzRecoveryServicesBackupItem       |
| List backup jobs                 | az backup job list                        | Get-AzRecoveryServicesBackupJob           |
| IP flow verify                   | az network watcher test-ip-flow           | Test-AzNetworkWatcherIPFlow               |
| Next hop                         | az network watcher show-next-hop          | Get-AzNetworkWatcherNextHop               |

## Common confusions

| Confusion                                      | Correct idea                                                    |
| ---------------------------------------------- | --------------------------------------------------------------- |
| Metrics vs logs                                | Numeric time-series vs queryable records (KQL)                  |
| Activity log vs resource logs                  | Control-plane "who did what" vs data-plane resource telemetry   |
| Alert rule vs action group                     | The condition that fires vs the people/automation notified      |
| Action group vs alert processing rule          | Notification list vs bulk suppress/attach behavior after firing |
| VM insights vs Application Insights            | VM OS/process view vs application request/dependency telemetry  |
| IP flow verify vs connection troubleshoot      | NSG rule simulation vs live end-to-end path test                |
| Connection troubleshoot vs connection monitor  | One-time test vs continuous monitoring                          |
| Recovery Services vault vs Backup vault        | VMs/Files/on-prem/ASR vs Disks/Blobs/PostgreSQL                 |
| Azure Backup vs Azure Site Recovery            | Restore data vs fail over workloads to another region           |
| Diagnostic settings vs the Azure Monitor agent | Platform resource logs routing vs in-guest OS data collection   |

## Exam traps

| Trap                                                             | Why people miss it                                                      |
| ---------------------------------------------------------------- | ----------------------------------------------------------------------- |
| Querying memory usage of a VM with no agent installed            | Guest OS metrics need the Azure Monitor agent + DCR                     |
| Trying to change vault redundancy after backups exist            | Redundancy locks once items are protected                               |
| Backing up a VM to a vault in a different region                 | The vault must be in the VM's region                                    |
| Deleting a vault that still contains backup items                | All protected items must be removed first (plus soft-deleted data)      |
| Answering "region failover" with Azure Backup                    | Backup restores data; Site Recovery fails over                          |
| Answering "recover one deleted file from a VM" with full restore | File-level recovery mounts the restore point; no full VM restore needed |
| Using the activity log to find performance data                  | Activity log is control-plane only; use metrics/logs                    |
| Setting only an alert rule and expecting notifications           | Notifications come from the action group attached to the rule           |
| Using packet capture to check if an NSG blocks a port            | IP flow verify answers rule questions instantly                         |
| Ignoring alert processing rules for maintenance windows          | They exist precisely to suppress alerts during planned work             |

## Mini scenarios

| Scenario                                                                                    | Best answer                                                              |
| ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| Ops needs a chart of average VM CPU over the last 24 hours split per VM.                    | Metrics Explorer with a dimension split                                  |
| Security must find all failed Linux logons across 50 VMs in the last day.                   | Log Analytics: query Syslog with KQL                                     |
| The NOC must get an SMS when any production VM's CPU exceeds 90% for 10 minutes.            | Metric alert rule + action group with SMS                                |
| During monthly patching, alert emails must stop for two hours.                              | Alert processing rule to suppress notifications on a schedule            |
| An admin must know which NSG rule is blocking RDP from a jump box to a VM.                  | Network Watcher IP flow verify                                           |
| Latency between an app VM and a database VM must be tracked continuously with alerts.       | Connection monitor                                                       |
| A team must be emailed whenever anyone deletes a resource group in the subscription.        | Activity log alert + action group                                        |
| Daily VM backups must be kept 30 days, with monthly restore points kept 12 months.          | Recovery Services vault + backup policy with daily and monthly retention |
| One accidentally deleted config file must be recovered from last night's VM backup.         | File-level recovery from the restore point                               |
| Compliance requires proof the company can run production in a second region within 4 hours. | Azure Site Recovery with a test failover (RTO evidence)                  |
| Blob data and Azure Disks need policy-based backup.                                         | Backup vault (not Recovery Services vault)                               |
| Backup failures across 12 vaults must appear in one dashboard.                              | Backup center (with backup reports via Log Analytics)                    |

## Check yourself

1. Which Azure Monitor component stores data you query with KQL?
2. What is the difference between the activity log and resource logs?
3. Name the four main parts of a metric alert rule.
4. Which tool tells you which NSG rule would deny a specific packet?
5. What is the difference between connection troubleshoot and connection monitor?
6. Which vault type backs up Azure Blobs and Azure Disks?
7. Why might you be unable to delete a Recovery Services vault?
8. A VM in West Europe must be backed up. Where must the vault be?
9. Which service provides failover to a secondary region: Azure Backup or Azure Site Recovery?
10. What does an alert processing rule do that an action group does not?

## Answer guide

1. Logs, stored in a Log Analytics workspace.
2. Activity log records control-plane operations (create/update/delete); resource logs record what happens inside a resource and need diagnostic settings to be collected.
3. Scope, condition (signal + threshold), severity, and action group (plus alert details).
4. Network Watcher IP flow verify.
5. Troubleshoot is a one-time test; connection monitor runs continuously and alerts over time.
6. Backup vault.
7. It still contains protected items, soft-deleted backup data, or registered servers; all must be removed first.
8. West Europe; the vault must be in the same region as the VM.
9. Azure Site Recovery.
10. It acts on fired alerts at scale: suppressing notifications (e.g. maintenance windows) or attaching action groups to many alerts.
