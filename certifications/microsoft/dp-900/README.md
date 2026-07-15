# DP-900: Microsoft Azure Data Fundamentals

DP-900 is the best first step for learning how data works in Microsoft Azure. It does not expect you to administer databases or write complex queries, but it does expect you to understand data vocabulary, relational and non-relational concepts, the Azure data service families, and how analytics workloads flow from ingestion to visualization.

These notes are built for fast revision and real understanding. Read the domain notes once, do the labs, then use the cheatsheets to remove confusion before taking practice tests.

## Start Here

Pick the path that matches your timeline:

| If you have...      | Use this path                                                                                                                                                    |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1 day               | Read [Exam-Day Review](cheatsheets/dp-900-exam-day-review.md), then [Common Confusions](cheatsheets/dp-900-common-confusions.md)                                 |
| 3 days              | Read the four study notes, review [Service Picker](cheatsheets/dp-900-service-picker.md), then do practice questions                                             |
| 5 days              | Follow the recommended plan below and complete the SQL, storage, Cosmos DB, Fabric, and cleanup labs                                                             |
| No Azure experience | Start with [00 - Set Up Your Lab Environment](labs/00-set-up-lab-environment.md), then [01 - Create an Azure SQL Database](labs/01-create-azure-sql-database.md) |

## What to Memorize vs Understand

| Memorize                                                              | Understand                                                        |
| --------------------------------------------------------------------- | ----------------------------------------------------------------- |
| Structured, semi-structured, unstructured data definitions            | Why storage and query options change with data shape              |
| OLTP vs OLAP characteristics                                          | Why transactional and analytical systems are designed differently |
| SQL statement categories: DDL, DML, DCL                               | What each statement type actually does to a database              |
| Azure SQL family: Database, Managed Instance, SQL Server on VM        | Which option fits migration, compatibility, and control needs     |
| Blob vs Files vs Table storage                                        | Which data shape and access pattern each one serves               |
| Cosmos DB APIs: NoSQL, MongoDB, Cassandra, Gremlin, Table, PostgreSQL | Which API fits which existing application or data model           |
| ETL vs ELT, batch vs streaming                                        | Where transformation happens and when data arrives                |
| Power BI building blocks: Desktop, service, reports, dashboards       | Which visualization fits which question about the data            |

## Exam Snapshot

| Item           | Detail                                          |
| -------------- | ----------------------------------------------- |
| Exam code      | DP-900                                          |
| Certification  | Microsoft Azure Data Fundamentals               |
| Level          | Beginner                                        |
| Passing score  | 700 out of 1000                                 |
| Question style | Conceptual and scenario-based fundamentals      |
| Best for       | Data beginners, students, and career switchers  |
| Study approach | Learn concepts, compare services, do small labs |

## Official Skill Areas

Aligned to the official "Skills measured as of July 21, 2026" outline. Always confirm the active outline on the [official study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/dp-900) before booking.

Last verified: July 10, 2026.

Note that the July 21, 2026 outline is not yet in effect: if your exam date is before July 21, 2026, re-check the official study guide to confirm which outline version applies to your exam date.

| Domain | Skill area                                                            | Weight |
| ------ | --------------------------------------------------------------------- | ------ |
| 1      | Describe core data concepts                                           | 25-30% |
| 2      | Identify considerations for relational data on Azure                  | 20-25% |
| 3      | Describe considerations for working with non-relational data on Azure | 15-20% |
| 4      | Describe an analytics workload on Azure                               | 25-30% |

## How to Use This Folder

1. Read the four study notes in order.
2. Open the common-confusions file and check every pair you mix up.
3. Complete the beginner labs so the services become real in the Azure portal.
4. Review the data landscape diagrams before practice tests.
5. Use the quick reference on the final day.

## Contents

### Study Notes

| File                                                                                | Use it for                                                             |
| ----------------------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| [01 - Core Data Concepts](study-notes/01-core-data-concepts.md)                     | Data shapes, file formats, data stores, workloads, data roles          |
| [02 - Relational Data on Azure](study-notes/02-relational-data-on-azure.md)         | Relational concepts, normalization, SQL, Azure SQL family, open source |
| [03 - Non-Relational Data on Azure](study-notes/03-non-relational-data-on-azure.md) | Blob, Files, Table storage, Cosmos DB use cases and APIs               |
| [04 - Analytics Workload on Azure](study-notes/04-analytics-workload.md)            | Ingestion, analytical stores, Databricks, Fabric, streaming, Power BI  |

### Cheatsheets

| File                                                                | Use it for                                    |
| ------------------------------------------------------------------- | --------------------------------------------- |
| [DP-900 Quick Reference](cheatsheets/dp-900-quick-reference.md)     | Last-day revision                             |
| [DP-900 Common Confusions](cheatsheets/dp-900-common-confusions.md) | Fixing the traps that cause wrong answers     |
| [DP-900 Service Picker](cheatsheets/dp-900-service-picker.md)       | Choosing the right Azure data service quickly |
| [DP-900 Exam-Day Review](cheatsheets/dp-900-exam-day-review.md)     | Final 30-45 minute review before the exam     |
| [DP-900 Mock Review](cheatsheets/dp-900-mock-review.md)             | Mixed scenario drills across all four domains |
| [Azure CLI Cheatsheet](../azure-cli-cheatsheet.md)                  | Recognizing storage, SQL, Cosmos DB, and cleanup command patterns |

### Hands-On Labs

| Lab                                                                                            | What it teaches                                                   |
| ---------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| [00 - Set Up Your Lab Environment](labs/00-set-up-lab-environment.md)                          | Free account safety, resource group, budget alert, cost awareness |
| [01 - Create an Azure SQL Database](labs/01-create-azure-sql-database.md)                      | PaaS relational database, service tiers, sample data              |
| [02 - Query with the Portal Query Editor](labs/02-query-with-portal-query-editor.md)           | SELECT, INSERT, UPDATE, DELETE, database objects                  |
| [03 - Create a Storage Account](labs/03-create-storage-account.md)                             | Storage accounts, redundancy, performance tiers                   |
| [04 - Explore Blob Storage](labs/04-explore-blob-storage.md)                                   | Containers, block blobs, access tiers, unstructured data          |
| [05 - Explore Azure Files and Table Storage](labs/05-explore-azure-files-and-table-storage.md) | File shares, tables, partition and row keys                       |
| [06 - Create an Azure Cosmos DB Account](labs/06-create-cosmos-db-account.md)                  | NoSQL documents, containers, partition keys, APIs                 |
| [07 - Explore Microsoft Fabric](labs/07-explore-microsoft-fabric.md)                           | Fabric trial, workspaces, lakehouse, OneLake                      |
| [08 - Explore Power BI](labs/08-explore-power-bi.md)                                           | Reports, visuals, data models, dashboards                         |
| [09 - Clean Up Resources](labs/09-clean-up-resources.md)                                       | Resource lifecycle, cleanup, cost control                         |

### Diagrams

| Diagram                                                    | What it teaches                                                       |
| ---------------------------------------------------------- | --------------------------------------------------------------------- |
| [DP-900 Data Landscape](diagrams/dp-900-data-landscape.md) | Relational vs non-relational map, storage options, analytics pipeline |

### Coverage

| File                                  | Use it for                                                  |
| ------------------------------------- | ----------------------------------------------------------- |
| [Coverage Matrix](coverage-matrix.md) | Mapping every official objective to the files that cover it |

## What Usually Decides Pass or Fail

Most DP-900 mistakes come from confusing similar terms:

| If you confuse...                           | Review                                                        |
| ------------------------------------------- | ------------------------------------------------------------- |
| OLTP and OLAP                               | Transactional processing vs analytical processing             |
| Structured and semi-structured data         | Fixed schema tables vs flexible JSON-style documents          |
| Azure SQL Database and SQL Managed Instance | Single PaaS database vs near-full SQL Server compatibility    |
| Blob Storage and Azure Files                | Object storage vs mounted SMB/NFS file shares                 |
| Table storage and Cosmos DB                 | Simple key-value tables vs globally distributed multi-model   |
| ETL and ELT                                 | Transform before loading vs transform after loading           |
| Batch and streaming                         | Process data in scheduled groups vs process as it arrives     |
| Azure Databricks and Microsoft Fabric       | Spark-first platform vs all-in-one SaaS analytics platform    |
| Power BI report and dashboard               | Multi-page visuals from one model vs pinned single-page tiles |

## High-Value Exam Traps

| Trap                                                      | Correct thinking                                                   |
| --------------------------------------------------------- | ------------------------------------------------------------------ |
| "Need to run many small reads and writes reliably"        | OLTP workload with ACID transactions, not a data warehouse.        |
| "Need to analyze years of history for trends"             | OLAP / analytical workload, not a transactional database.          |
| "Need SQL Server Agent or cross-database queries in PaaS" | Azure SQL Managed Instance, not Azure SQL Database.                |
| "Need full OS access for the database server"             | SQL Server on Azure Virtual Machines (IaaS).                       |
| "Need to store images, video, or backups cheaply"         | Azure Blob Storage, not Azure Files or a database.                 |
| "Need to lift and shift an on-premises file share"        | Azure Files, not Blob Storage.                                     |
| "Need a MongoDB-compatible managed database"              | Azure Cosmos DB for MongoDB.                                       |
| "Need to move data on a schedule between stores"          | A pipeline (Azure Data Factory or Microsoft Fabric), not Power BI. |
| "Need insights within seconds of events happening"        | Streaming / real-time analytics, not batch processing.             |
| "Need to show part-to-whole proportions"                  | Pie or donut chart. Trends over time use a line chart.             |

## Recommended 5-Day Plan

| Day | Focus                                                                  |
| --- | ---------------------------------------------------------------------- |
| 1   | Core data concepts: data shapes, formats, workloads, roles             |
| 2   | Relational concepts, SQL basics, Azure SQL family, open-source options |
| 3   | Azure Storage services and Cosmos DB, plus storage labs                |
| 4   | Analytics: ingestion, Databricks, Fabric, streaming, Power BI, labs    |
| 5   | Quick reference, practice questions, wrong-answer review               |

## Readiness Checklist

Before booking, you should be able to explain these without notes:

- Structured vs semi-structured vs unstructured data with an example of each
- OLTP vs OLAP and which Azure services serve each
- What normalization does and why transactional databases use it
- DDL vs DML vs DCL and the common statements in each
- Azure SQL Database vs SQL Managed Instance vs SQL Server on Azure VMs
- Blob Storage vs Azure Files vs Table storage
- The Cosmos DB APIs and when each is the right choice
- ETL vs ELT and batch vs streaming
- What Azure Databricks and Microsoft Fabric each bring to large-scale analytics
- Power BI Desktop vs the Power BI service, and report vs dashboard

## Score Booster Routine

Use this after each practice test:

1. Write down every wrong answer in one line.
2. Label the reason: vocabulary gap, service confusion, workload confusion, or visualization confusion.
3. Re-read only the matching section in this folder.
4. Add the confused pair to your own notes.
5. Retake a small focused quiz before doing another full mock.

The goal is not to memorize answers. The goal is to stop repeating the same type of mistake.

## Note on Exam Content

These are original study notes. They do not contain real exam questions or leaked content. Use them to understand the concepts, then practice with scenario-based questions and hands-on tasks.

---

Maintained by the team behind [CertGrid](https://certgrid.app). Free practice is available on CertGrid, but these notes are useful on their own.
