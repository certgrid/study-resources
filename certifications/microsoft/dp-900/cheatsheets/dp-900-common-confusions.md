# DP-900 Common Confusions

Many DP-900 questions are easy once you separate similar terms. Use this file after your first practice test and before the final review.

## Data Shapes and Formats

| This            | Not this        | How to remember                                     |
| --------------- | --------------- | --------------------------------------------------- |
| Semi-structured | Unstructured    | JSON/XML carry field names inside the data.         |
| Unstructured    | Semi-structured | Images, video, and audio have no queryable fields.  |
| Structured      | Semi-structured | Fixed columns defined before the data arrives.      |
| Parquet/ORC     | Avro            | Column-based formats are for analytical reads.      |
| Avro            | Parquet         | Row-based format, efficient for writes and streams. |
| CSV             | JSON            | Flat delimited rows; no hierarchy, no data types.   |

## Workloads

| This          | Not this          | How to remember                                      |
| ------------- | ----------------- | ---------------------------------------------------- |
| OLTP          | OLAP              | Records business events now; small fast writes.      |
| OLAP          | OLTP              | Analyzes history; big aggregating reads.             |
| Normalization | Denormalization   | Store each fact once; protects transactional writes. |
| Star schema   | Normalized schema | Denormalized facts and dimensions for analytics.     |
| ACID          | High availability | Transaction guarantees, not uptime.                  |

## Roles

| This                   | Not this               | How to remember                                |
| ---------------------- | ---------------------- | ---------------------------------------------- |
| Database administrator | Data engineer          | Backups, security, availability of databases.  |
| Data engineer          | Database administrator | Builds pipelines; ingests and transforms data. |
| Data analyst           | Data engineer          | Models data and builds reports and visuals.    |

## SQL

| This             | Not this         | How to remember                                  |
| ---------------- | ---------------- | ------------------------------------------------ |
| DDL              | DML              | Defines structure: CREATE, ALTER, DROP.          |
| DML              | DDL              | Works with rows: SELECT, INSERT, UPDATE, DELETE. |
| DCL              | DML              | Controls access: GRANT, DENY, REVOKE.            |
| DELETE           | DROP             | DELETE removes rows; the table stays.            |
| DROP             | DELETE           | DROP removes the object itself.                  |
| View             | Stored procedure | A view is a saved query you select from.         |
| Stored procedure | View             | A procedure is saved code you execute.           |
| Index            | Primary key      | An index speeds lookups; a key defines identity. |

## Relational Azure Services

| This                          | Not this                   | How to remember                                        |
| ----------------------------- | -------------------------- | ------------------------------------------------------ |
| Azure SQL Database            | Azure SQL Managed Instance | Single database, least admin, newest cloud apps.       |
| Azure SQL Managed Instance    | Azure SQL Database         | Near-full SQL Server instance features in PaaS.        |
| SQL Server on Azure VMs       | Azure SQL Managed Instance | Only option with OS access; IaaS.                      |
| Elastic pool                  | Single database            | Multiple databases share one pool of resources.        |
| Azure Database for PostgreSQL | Cosmos DB for PostgreSQL   | Managed single-server engine vs distributed scale-out. |

## Non-Relational Azure Services

| This                  | Not this                | How to remember                                            |
| --------------------- | ----------------------- | ---------------------------------------------------------- |
| Blob storage          | Azure Files             | Objects behind URLs: media, backups, logs.                 |
| Azure Files           | Blob storage            | Mounted SMB/NFS shares; file system semantics.             |
| Table storage         | Cosmos DB for Table     | Cheap single-region tables vs global distribution.         |
| ADLS Gen2             | Blob storage            | Blob plus hierarchical namespace for analytics.            |
| Archive tier          | Cool/Cold tier          | Offline; must rehydrate before reading.                    |
| Block blob            | Page blob               | Files and media vs VM disks with random access.            |
| Partition key         | Row key                 | Groups entities for scale vs unique ID inside a partition. |
| Cosmos DB for NoSQL   | Cosmos DB for MongoDB   | Native document API vs MongoDB compatibility.              |
| Cosmos DB for Gremlin | Cosmos DB for Cassandra | Graph (nodes/edges) vs column-family (CQL).                |

## Analytics

| This                   | Not this               | How to remember                                      |
| ---------------------- | ---------------------- | ---------------------------------------------------- |
| ETL                    | ELT                    | Transform in the pipeline, then load.                |
| ELT                    | ETL                    | Load raw first, transform inside the store.          |
| Data lake              | Data warehouse         | Raw files, any shape, schema-on-read.                |
| Data warehouse         | Data lake              | Curated relational tables, T-SQL, schema-on-write.   |
| Lakehouse              | Data warehouse         | Open lake files with a table/SQL layer.              |
| Batch                  | Streaming              | Wait, then process a group on a schedule.            |
| Streaming              | Batch                  | Process each event within seconds of arrival.        |
| Azure Databricks       | Microsoft Fabric       | Spark-first platform for engineering and ML.         |
| Microsoft Fabric       | Azure Databricks       | All-in-one SaaS suite on OneLake, includes Power BI. |
| Azure Event Hubs       | Azure Stream Analytics | Ingests event streams; does not analyze them.        |
| Azure Stream Analytics | Azure Event Hubs       | Queries and processes streams with SQL-like jobs.    |
| Azure IoT Hub          | Azure Event Hubs       | Adds device management and two-way communication.    |
| KQL                    | T-SQL                  | Queries event/log stores; T-SQL queries warehouses.  |

## Power BI

| This             | Not this         | How to remember                                       |
| ---------------- | ---------------- | ----------------------------------------------------- |
| Report           | Dashboard        | Multi-page, interactive, built on one model.          |
| Dashboard        | Report           | One page of pinned tiles; exists only in the service. |
| Power BI Desktop | Power BI service | Create and model on Windows, free.                    |
| Power BI service | Power BI Desktop | Publish, share, and build dashboards in the cloud.    |
| Measure          | Column           | A calculation (DAX), not stored data.                 |
| Line chart       | Pie chart        | Trends over time.                                     |
| Pie/donut chart  | Line chart       | Part-to-whole at a point in time.                     |
| Scatter chart    | Bar chart        | Relationship between two numeric measures.            |
| Card/KPI         | Table            | One headline number, not a grid.                      |
