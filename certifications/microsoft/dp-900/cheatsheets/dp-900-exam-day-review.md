# DP-900 Exam-Day Review

Use this page in the final 30-45 minutes before the exam. It is intentionally short and focused on high-frequency decisions.

## The Exam Mindset

DP-900 is a fundamentals exam. Most questions are not asking you to configure or query anything. They are asking whether you can recognize the right data concept, workload type, or Azure data service from the wording.

When stuck, ask:

1. Is this about the shape of the data?
2. Is this about transactional vs analytical work?
3. Is this about choosing a relational service?
4. Is this about choosing a storage or Cosmos DB option?
5. Is this about the analytics pipeline or visualization?

## Must-Know Pairs

| Pair                                   | Difference                                                       |
| -------------------------------------- | ---------------------------------------------------------------- |
| Structured vs semi-structured          | Fixed schema tables vs flexible records like JSON                |
| Semi-structured vs unstructured        | Fields inside the data vs no queryable fields at all             |
| OLTP vs OLAP                           | Run the business now vs analyze the history                      |
| Normalized vs denormalized             | Write integrity for OLTP vs read speed for analytics             |
| DDL vs DML                             | Define structure vs work with rows                               |
| DELETE vs DROP                         | Remove rows vs remove the object                                 |
| View vs stored procedure               | Saved query vs saved executable code                             |
| Azure SQL Database vs Managed Instance | Single managed database vs near-full SQL Server instance in PaaS |
| Managed Instance vs SQL Server on VM   | PaaS without OS access vs IaaS with full control                 |
| Blob storage vs Azure Files            | Objects behind URLs vs mounted SMB/NFS shares                    |
| Table storage vs Cosmos DB             | Cheap single-region key-value vs global multi-model NoSQL        |
| Cool tier vs Archive tier              | Online instant access vs offline, rehydrate first                |
| ETL vs ELT                             | Transform then load vs load then transform                       |
| Data lake vs data warehouse            | Raw files, schema-on-read vs curated tables, schema-on-write     |
| Batch vs streaming                     | Scheduled groups vs event-by-event within seconds                |
| Azure Databricks vs Microsoft Fabric   | Spark platform for engineers/ML vs all-in-one SaaS analytics     |
| Event Hubs vs Stream Analytics         | Ingest the stream vs query/process the stream                    |
| Report vs dashboard                    | Multi-page from one model vs single page of pinned tiles         |

## Data Shape Decision

| The data is...                       | Answer          |
| ------------------------------------ | --------------- |
| Rows and columns, fixed schema       | Structured      |
| JSON/XML, fields vary per record     | Semi-structured |
| Images, audio, video, free documents | Unstructured    |

## Workload Decision

| Wording                                     | Answer               |
| ------------------------------------------- | -------------------- |
| Many small reads/writes, integrity, current | OLTP (transactional) |
| Aggregate history, trends, reports          | OLAP (analytical)    |
| All-or-nothing transaction guarantees       | ACID                 |
| Fact and dimension tables                   | Star schema          |

## Relational Service Decision

| Wording                                                             | Answer                                |
| ------------------------------------------------------------------- | ------------------------------------- |
| New app, least management                                           | Azure SQL Database                    |
| SQL Server Agent / cross-database / near-full compatibility in PaaS | Azure SQL Managed Instance            |
| OS access, exact version control                                    | SQL Server on Azure Virtual Machines  |
| Managed MySQL / PostgreSQL                                          | Azure Database for MySQL / PostgreSQL |

## Storage and Cosmos DB Decision

| Wording                                          | Answer                       |
| ------------------------------------------------ | ---------------------------- |
| Media, backups, logs, objects by URL             | Blob Storage                 |
| Mounted share, SMB, NFS, lift and shift          | Azure Files                  |
| Cheap key-value rows, partition + row key        | Table Storage                |
| Analytics files, hierarchical namespace          | Azure Data Lake Storage Gen2 |
| Global, milliseconds, JSON documents             | Azure Cosmos DB for NoSQL    |
| MongoDB / Cassandra / Gremlin / PostgreSQL named | The matching Cosmos DB API   |
| Rarely read, cheapest, retrieval can wait        | Blob Archive tier            |

## Analytics Decision

| Wording                               | Answer                           |
| ------------------------------------- | -------------------------------- |
| Move/transform data on schedule       | Pipeline (Data Factory / Fabric) |
| Spark notebooks, data science, ML     | Azure Databricks                 |
| All-in-one SaaS analytics, OneLake    | Microsoft Fabric                 |
| Events queried with KQL               | Fabric Real-Time Intelligence    |
| Ingest millions of events per second  | Azure Event Hubs                 |
| Ingest events and manage devices      | Azure IoT Hub                    |
| SQL-like windowed queries on a stream | Azure Stream Analytics           |

## Visualization Decision

| Wording                     | Answer              |
| --------------------------- | ------------------- |
| Trend over time             | Line chart          |
| Compare categories          | Bar or column chart |
| Part of a whole             | Pie or donut chart  |
| Two measures, correlation   | Scatter chart       |
| One headline number         | Card or KPI         |
| By country/region           | Map                 |
| Build and model reports     | Power BI Desktop    |
| Share, view, pin dashboards | Power BI service    |

## Last-Minute Traps

| Trap wording                               | Better answer                                  |
| ------------------------------------------ | ---------------------------------------------- |
| "JSON is unstructured"                     | JSON is semi-structured                        |
| "Use a warehouse for order processing"     | OLTP needs a transactional database            |
| "Managed Instance gives OS access"         | Only SQL Server on a VM gives OS access        |
| "Use Azure Files for website images"       | Blob Storage serves objects by URL             |
| "Archive blobs are instantly readable"     | Archive is offline; rehydration can take hours |
| "Power BI moves data between stores"       | Pipelines move data; Power BI visualizes       |
| "Dashboards are built in Power BI Desktop" | Dashboards exist only in the Power BI service  |
| "Streaming is just faster batch"           | Streaming processes each event as it arrives   |
| "KQL queries the data warehouse"           | KQL is for event stores; warehouses use T-SQL  |
| "Pie chart for a monthly trend"            | Line chart shows trends over time              |

## Final Confidence Checklist

You are ready when you can explain these without looking:

- Structured vs semi-structured vs unstructured, with examples
- OLTP vs OLAP and the ACID properties
- DDL vs DML vs DCL, and DELETE vs DROP
- The three Azure SQL family options and their deciders
- Blob vs Files vs Table storage, and the blob access tiers
- The six Cosmos DB APIs and their trigger words
- ETL vs ELT, lake vs warehouse vs lakehouse
- Azure Databricks vs Microsoft Fabric, and what OneLake is
- Batch vs streaming, and which services ingest vs process streams
- Power BI Desktop vs service, report vs dashboard, and chart choices
