# DP-900 Quick Reference

Use this on the final day. It is intentionally compact and exam-focused.

## One-Page Mental Model

| Question asks about...         | Think of...                                             |
| ------------------------------ | ------------------------------------------------------- |
| The shape of some data         | Structured, semi-structured, unstructured               |
| A file format                  | CSV, JSON, XML, Avro (row), ORC/Parquet (column)        |
| A workload type                | OLTP (run the business) vs OLAP (analyze the business)  |
| A job duty                     | DBA, data engineer, data analyst                        |
| A relational service           | Azure SQL family or open-source Azure Database services |
| Files, shares, key-value rows  | Blob, Files, Table storage                              |
| Global NoSQL or a named engine | Azure Cosmos DB and its APIs                            |
| Moving and transforming data   | Pipelines: Azure Data Factory or Microsoft Fabric       |
| Large-scale analytics platform | Azure Databricks or Microsoft Fabric                    |
| Charts, reports, dashboards    | Microsoft Power BI                                      |

## Data Shapes

| Shape           | Remember                                | Example                    |
| --------------- | --------------------------------------- | -------------------------- |
| Structured      | Fixed rows and columns, schema-on-write | Relational tables          |
| Semi-structured | Structure travels with the record       | JSON, XML, key-value       |
| Unstructured    | No queryable structure                  | Images, video, audio, PDFs |

## File Formats

| Format      | Remember                                 |
| ----------- | ---------------------------------------- |
| CSV         | Plain text rows, no data types           |
| JSON        | Hierarchical documents, APIs             |
| XML         | Tag-based documents, older exchange      |
| Avro        | Binary, row-based, write/stream friendly |
| ORC/Parquet | Binary, column-based, analytics friendly |

## Workloads

| Concept     | Remember                                                |
| ----------- | ------------------------------------------------------- |
| OLTP        | Many small reads/writes, current data, normalized       |
| OLAP        | Big reads over history, denormalized, star schema       |
| ACID        | Atomicity, Consistency, Isolation, Durability           |
| Star schema | Fact table (numbers) plus dimension tables (attributes) |

## Roles

| Role                   | Remember                                  |
| ---------------------- | ----------------------------------------- |
| Database administrator | Backups, restores, security, availability |
| Data engineer          | Pipelines, ingestion, transformation      |
| Data analyst           | Models, reports, visualizations, insights |

## SQL in One Table

| Category | Statements                     | Purpose          |
| -------- | ------------------------------ | ---------------- |
| DDL      | CREATE, ALTER, DROP, RENAME    | Define structure |
| DML      | SELECT, INSERT, UPDATE, DELETE | Work with data   |
| DCL      | GRANT, DENY, REVOKE            | Control access   |

| Object           | Remember                              |
| ---------------- | ------------------------------------- |
| View             | Saved query, virtual table, no data   |
| Stored procedure | Saved executable code with parameters |
| Index            | Faster lookups on chosen columns      |

## Azure SQL Family

| Option                               | Type | Pick when...                                         |
| ------------------------------------ | ---- | ---------------------------------------------------- |
| Azure SQL Database                   | PaaS | New apps, single database, least management          |
| Azure SQL Managed Instance           | PaaS | Migration needing near-full SQL Server compatibility |
| SQL Server on Azure Virtual Machines | IaaS | Full OS and instance control                         |

Open source: Azure Database for MySQL, Azure Database for PostgreSQL (both fully managed PaaS).

## Azure Storage

| Service       | Data               | Pick when...                           |
| ------------- | ------------------ | -------------------------------------- |
| Blob storage  | Objects            | Media, backups, logs, any files by URL |
| Azure Files   | File shares        | Mount over SMB/NFS, lift and shift     |
| Table storage | Key-value entities | Cheap simple NoSQL rows, single region |

| Blob detail   | Remember                                       |
| ------------- | ---------------------------------------------- |
| Block blob    | Normal files and media                         |
| Page blob     | VM disks, random access                        |
| Append blob   | Logs, append-only                              |
| Hot/Cool/Cold | Online tiers from frequent to rare access      |
| Archive       | Offline, cheapest, needs rehydration           |
| ADLS Gen2     | Blob plus hierarchical namespace for analytics |

## Cosmos DB APIs

| API        | Pick when...                            |
| ---------- | --------------------------------------- |
| NoSQL      | New document apps (native API)          |
| MongoDB    | Existing MongoDB apps                   |
| Cassandra  | Existing Cassandra/CQL apps             |
| Gremlin    | Graph data: nodes and edges             |
| Table      | Table storage apps needing global scale |
| PostgreSQL | Distributed, scale-out PostgreSQL       |

## Analytics

| Concept        | Remember                                   |
| -------------- | ------------------------------------------ |
| ETL            | Transform before load                      |
| ELT            | Load raw, transform in the store           |
| Data warehouse | Curated relational history, T-SQL          |
| Data lake      | Raw files, any format, schema-on-read      |
| Lakehouse      | Lake files with table/SQL layer on top     |
| OneLake        | Fabric's single built-in data lake         |
| Batch          | Scheduled groups, latency in minutes/hours |
| Streaming      | Event by event, latency in seconds         |
| KQL            | Query language for real-time event stores  |

| Service                       | Remember                               |
| ----------------------------- | -------------------------------------- |
| Azure Data Factory            | Pipelines that move and transform data |
| Azure Databricks              | Apache Spark platform, notebooks, ML   |
| Microsoft Fabric              | All-in-one SaaS analytics on OneLake   |
| Fabric Real-Time Intelligence | Eventstreams, eventhouse, KQL          |
| Azure Stream Analytics        | SQL-like queries over event streams    |
| Azure Event Hubs              | High-scale event ingestion             |
| Azure IoT Hub                 | Event ingestion plus device management |

## Power BI

| Item             | Remember                                |
| ---------------- | --------------------------------------- |
| Power BI Desktop | Free app: connect, model, build reports |
| Power BI service | Publish, share, dashboards, apps        |
| Power BI Mobile  | Consume on phone/tablet                 |
| Semantic model   | Tables, relationships, measures (DAX)   |
| Report           | Multi-page visuals from one model       |
| Dashboard        | One page of pinned tiles, service only  |

| Show...                  | Use...              |
| ------------------------ | ------------------- |
| Category comparison      | Bar/column chart    |
| Trend over time          | Line chart          |
| Part-to-whole            | Pie, donut, treemap |
| Two-measure relationship | Scatter chart       |
| Single number            | Card or KPI         |
| Geographic data          | Map                 |
| Exact values grid        | Table or matrix     |
