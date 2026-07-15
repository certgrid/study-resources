# DP-900 Service Picker

Use this page when a question asks: "Which Azure data service should you choose?"

DP-900 usually gives a short business requirement and expects you to map it to the right service. Do not overthink advanced configuration. Pick the service that best matches the keyword.

## Relational Databases

| Requirement                                                                   | Choose                               | Why                                              |
| ----------------------------------------------------------------------------- | ------------------------------------ | ------------------------------------------------ |
| New cloud app needs a managed relational database, least admin                | Azure SQL Database                   | PaaS single database, automatic patching/backups |
| Variable usage across many databases, share resources                         | Azure SQL Database elastic pool      | Databases share one pool                         |
| Database that pauses when idle to save cost                                   | Azure SQL Database serverless        | Auto-pause and auto-scale compute                |
| Migrate on-premises SQL Server, need SQL Server Agent, cross-database queries | Azure SQL Managed Instance           | Near 100% instance compatibility in PaaS         |
| Full control of OS, SQL Server version, custom software                       | SQL Server on Azure Virtual Machines | IaaS; you manage everything                      |
| Managed MySQL for a web app stack                                             | Azure Database for MySQL             | PaaS community MySQL                             |
| Managed PostgreSQL with extensions                                            | Azure Database for PostgreSQL        | PaaS community PostgreSQL                        |
| PostgreSQL that scales out across nodes                                       | Azure Cosmos DB for PostgreSQL       | Distributed PostgreSQL                           |

## Azure Storage

| Requirement                                     | Choose                       | Why                              |
| ----------------------------------------------- | ---------------------------- | -------------------------------- |
| Store images, video, backups, logs, documents   | Azure Blob Storage           | Object storage, URL per blob     |
| Files behind a URL for a website or app         | Azure Blob Storage           | Objects, not mounted shares      |
| Mount a shared folder over SMB or NFS           | Azure Files                  | Managed file shares              |
| Lift and shift an app that expects a file share | Azure Files                  | File system semantics preserved  |
| Cache file shares on a local Windows Server     | Azure File Sync              | Local cache of Azure Files       |
| Cheap key-value NoSQL rows, one region          | Azure Table Storage          | Simple partition/row key store   |
| Raw files for analytics with folder hierarchy   | Azure Data Lake Storage Gen2 | Blob plus hierarchical namespace |
| Frequently accessed blobs                       | Hot tier                     | Lowest access cost               |
| Infrequently accessed blobs, instant access     | Cool or Cold tier            | Lower storage cost, online       |
| Long-term archive, hours to retrieve is fine    | Archive tier                 | Cheapest storage, offline        |
| Virtual machine disk                            | Page blob (managed disk)     | Random read/write                |
| Append-only log files                           | Append blob                  | Optimized for appends            |

## Azure Cosmos DB API Picker

| Requirement                                          | Choose                               | Why                                   |
| ---------------------------------------------------- | ------------------------------------ | ------------------------------------- |
| New app storing JSON documents, global low latency   | Azure Cosmos DB for NoSQL            | Native API, SQL-like document queries |
| Existing MongoDB app, keep drivers and tools         | Azure Cosmos DB for MongoDB          | Wire-protocol compatibility           |
| Existing Cassandra app using CQL                     | Azure Cosmos DB for Apache Cassandra | Cassandra compatibility               |
| Social graph, recommendations, nodes and edges       | Azure Cosmos DB for Apache Gremlin   | Graph traversal queries               |
| Table storage app that now needs global distribution | Azure Cosmos DB for Table            | Same model, global scale and SLAs     |
| Relational PostgreSQL distributed across nodes       | Azure Cosmos DB for PostgreSQL       | Scale-out relational                  |

## Analytics and Pipelines

| Requirement                                                    | Choose                                   | Why                                         |
| -------------------------------------------------------------- | ---------------------------------------- | ------------------------------------------- |
| Move and transform data between stores on a schedule           | Azure Data Factory (or Fabric pipelines) | Orchestrated ETL/ELT pipelines              |
| Spark notebooks for big data engineering and machine learning  | Azure Databricks                         | Apache Spark platform                       |
| End-to-end SaaS analytics: pipelines, lakehouse, warehouse, BI | Microsoft Fabric                         | All-in-one platform on OneLake              |
| Single shared data lake for all Fabric workloads               | OneLake                                  | Fabric's built-in lake                      |
| Full T-SQL data warehouse experience in Fabric                 | Fabric Data Warehouse                    | Relational warehouse over OneLake           |
| Lake files plus notebooks and SQL in Fabric                    | Fabric Lakehouse                         | Files with table layer                      |
| Legacy Azure analytics platform in existing environments       | Azure Synapse Analytics                  | Predecessor; capabilities now led by Fabric |

## Real-Time and Streaming

| Requirement                                         | Choose                                  | Why                              |
| --------------------------------------------------- | --------------------------------------- | -------------------------------- |
| Ingest millions of events per second                | Azure Event Hubs                        | High-throughput event front door |
| Ingest IoT events plus manage the devices           | Azure IoT Hub                           | Two-way device communication     |
| SQL-like queries with time windows over a stream    | Azure Stream Analytics                  | Streaming query jobs             |
| Capture, store, and query events with KQL in Fabric | Fabric Real-Time Intelligence           | Eventstreams and eventhouse      |
| Spark-based stream processing in notebooks          | Azure Databricks (Structured Streaming) | Spark streaming                  |

## Visualization

| Requirement                                     | Choose                 | Why                         |
| ----------------------------------------------- | ---------------------- | --------------------------- |
| Build a data model and design reports           | Power BI Desktop       | Free authoring app          |
| Publish, share, and view reports in the browser | Power BI service       | Cloud distribution          |
| One-page summary of tiles from several reports  | Power BI dashboard     | Pinned tiles in the service |
| View reports on a phone                         | Power BI Mobile        | Mobile consumption          |
| Show a trend over time                          | Line chart             | Time on the axis            |
| Compare categories                              | Bar or column chart    | Category comparison         |
| Show proportions of a whole                     | Pie, donut, or treemap | Part-to-whole               |
| Show correlation of two measures                | Scatter chart          | Two numeric axes            |
| Highlight one number (total sales)              | Card or KPI            | Single value focus          |
| Show values by country or region                | Map visual             | Geographic data             |
| Let users filter the report page                | Slicer                 | On-page filtering           |
