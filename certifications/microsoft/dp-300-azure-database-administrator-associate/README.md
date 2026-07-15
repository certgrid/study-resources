# DP-300: Azure Database Administrator Associate - Study Cheatsheet

DP-300 (Azure Database Administrator Associate) validates your ability to plan and deploy Azure data platform resources, secure them, monitor and optimize performance, automate routine tasks, and design high availability and disaster recovery. It targets database administrators and infrastructure professionals who manage Azure SQL Database, Azure SQL Managed Instance, SQL Server on Azure VMs, and the open-source Azure Database services. You should know T-SQL, the Azure portal, PowerShell/CLI, and core SQL Server administration before sitting the exam.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | DP-300 |
| Credential | DP-300: Azure Database Administrator Associate |
| Level | Associate |
| Practice mock length | ~50 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Plan and Implement Data Platform Resources | ~21% |
| 2 | Implement a Secure Environment | ~20% |
| 3 | Monitor, Configure, and Optimize Resources | ~19% |
| 4 | Configure and Manage Automation of Tasks | ~19% |
| 5 | Plan and Configure HA and DR Environment | ~21% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Plan and Implement Data Platform Resources

- Azure SQL Managed Instance gives the highest compatibility with on-premises SQL Server because it supports instance-scoped features: SQL Server Agent, cross-database queries, linked servers, Service Broker, and CLR.
- Elastic pools let multiple Azure SQL databases share a common set of vCores/eDTUs, which lowers cost when databases have varying, non-overlapping usage peaks.
- The vCore purchasing model scales compute and storage independently and is the only model that supports Azure Hybrid Benefit (reuse of on-prem SQL Server licenses with Software Assurance).
- The DTU model bundles compute, storage, and I/O into fixed, pre-packaged units (Basic, Standard, Premium) and is simplest for predictable single-database workloads.
- Hyperscale supports databases up to 100 TB, fast backups/restores via snapshots, and rapid read scale-out using named replicas - it is the choice for very large databases.
- The Serverless compute tier (vCore only) auto-scales and auto-pauses during idle periods, billing per second of compute used - ideal for intermittent, unpredictable workloads with idle gaps.

### Domain 2 - Implement a Secure Environment

- Transparent Data Encryption (TDE) encrypts data at rest - data files, log files, and backups - with no application code changes; it is enabled by default on new Azure SQL databases.
- TDE with customer-managed keys (Bring Your Own Key) stores the TDE protector in Azure Key Vault, giving you control over key rotation and revocation.
- Always Encrypted keeps sensitive columns encrypted end-to-end including during query processing; encryption/decryption happen only on the client and the server never sees plaintext.
- Dynamic Data Masking obscures sensitive values for non-privileged users at query time (for example an email masking function) without changing the stored data.
- SQL Data Discovery and Classification automatically finds and labels sensitive columns (SSNs, credit cards) so you can track your sensitive-data footprint.
- Microsoft Defender for SQL provides advanced threat protection and surfaces SQL injection alerts when application queries contain potentially malicious SQL.

### Domain 3 - Monitor, Configure, and Optimize Resources

- Query Store continuously captures query plans, runtime statistics, and wait stats over time, letting you pinpoint when a regression started and force a previously good plan.
- Query Store plan forcing fixes plan-regression issues (for example after a statistics update chose a worse plan) without code changes.
- Key Query Store settings include STALE_QUERY_THRESHOLD_DAYS (retention) and DATA_FLUSH_INTERVAL_SECONDS (how often in-memory data is persisted).
- Automatic tuning in Azure SQL Database can apply FORCE PLAN (revert to last known good plan) and CREATE INDEX (add helpful indexes) automatically without manual approval.
- The PAGEIOLATCH_SH wait type means queries are waiting on data pages being read from disk into the buffer pool, indicating memory pressure or slow I/O.
- sys.dm_db_resource_stats shows recent CPU, data I/O, and log I/O percentage at ~15-second granularity for the current Azure SQL database.

### Domain 4 - Configure and Manage Automation of Tasks

- Elastic Jobs is the Azure-native way to run T-SQL on a schedule across many Azure SQL databases spanning different logical servers and pools; it requires a job database and an elastic job agent.
- Elastic Jobs target groups can include individual databases, elastic pools, or whole servers - add the elastic pool as a target group member to hit every database in it.
- SQL Server Agent is built into Azure SQL Managed Instance and supports T-SQL, OS command/PowerShell (CmdExec-style), SSIS package, and transactional replication job steps; unsupported items include Merge replication, Queue Reader, Analysis Services, and alerts.
- Azure SQL Database (single/pooled) has no SQL Server Agent; use Elastic Jobs or Azure Automation for scheduling instead.
- Azure Automation PowerShell runbooks with a schedule handle time-based operations such as scaling a database (Set-AzSqlDatabase) up before a peak window and back down after.
- Use Set-AzSqlDatabase in a runbook to change vCore count, service tier, or compute size on a schedule (for example 8 vCores normally, 16 every Friday evening).

### Domain 5 - Plan and Configure HA and DR Environment

- Auto-failover groups provide automatic cross-region failover and a single read-write listener endpoint, so applications connect once and Azure redirects to the current primary after failover.
- Auto-failover groups support both single databases and elastic pools, and the secondary server must be in a different Azure region from the primary.
- The GracePeriodWithDataLossHours parameter controls how long Azure waits before performing an automatic failover that could incur data loss.
- Active geo-replication supports up to four readable secondary replicas (same or different regions); failover must be initiated manually or via custom automation.
- With active geo-replication, each secondary lives on its own logical server with a unique name, so reporting apps connect directly to the secondary server's name for read-only queries.
- Point-in-time restore (PITR) uses automated full, differential, and log backups to restore to any second within the short-term retention window (configurable 1-35 days; default 7).

## Study tips

- Learn the decision tree for choosing a deployment option: SQL Database (PaaS, lowest management), Managed Instance (instance features/migration), or SQL on VM (full control). Many questions hinge on the unique feature that only one of them offers.
- Memorize the difference between active geo-replication (up to 4 readable secondaries, manual failover, per-server endpoints) and auto-failover groups (automatic failover, single read-write listener, supports pools).
- Know which DMV answers which question: sys.dm_db_resource_stats for resource usage, sys.dm_exec_requests for what is running now, sys.dm_exec_query_stats for historical top consumers, and the missing/unused index DMVs.
- For security scenarios, distinguish encryption at rest (TDE) from encryption in use (Always Encrypted) from masking (Dynamic Data Masking) - the wrong layer is a common trap answer.
- Watch for the automation boundary: SQL Server Agent exists on Managed Instance and SQL on VM but NOT on Azure SQL Database, where you must use Elastic Jobs or Azure Automation instead.

---

Want the full breakdown? See the complete **[DP-300 study guide](https://certgrid.app/study-guide/dp-300-azure-database-administrator-associate)** and **[free practice questions](https://certgrid.app/practice/dp-300-azure-database-administrator-associate)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

