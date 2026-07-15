# 04 - Describe an Analytics Workload on Azure

This domain is worth 25-30% of the exam. It covers how large-scale analytics works (ingestion, processing, analytical stores), the Microsoft services for it (Azure Databricks and Microsoft Fabric), real-time versus batch analytics, and data visualization with Microsoft Power BI.

## Mental model

Every analytics scenario follows the same pipeline: ingest data from sources, store it, process and model it, then visualize it. Place the question on that pipeline, then decide if the data moves in scheduled batches or as a continuous stream.

| Scenario keyword                                | Likely concept or service       |
| ----------------------------------------------- | ------------------------------- |
| Move and transform data on a schedule           | Batch pipeline (ETL/ELT)        |
| Transform before loading into the destination   | ETL                             |
| Load raw data first, transform inside the store | ELT                             |
| Central store of modeled, query-ready history   | Data warehouse                  |
| Store raw files of any format cheaply at scale  | Data lake                       |
| Files in a lake plus tables and SQL on top      | Lakehouse                       |
| Spark, notebooks, data science and ML           | Azure Databricks                |
| All-in-one SaaS analytics with OneLake          | Microsoft Fabric                |
| Insights seconds after events happen            | Real-time / streaming analytics |
| Reports, dashboards, interactive visuals        | Microsoft Power BI              |

## Data ingestion and processing

Ingestion means capturing data from sources (databases, files, APIs, devices) and landing it where analytics can use it. Processing cleans, combines, and reshapes that data.

| Approach | Order of steps           | Transform happens                      | Typical home                           |
| -------- | ------------------------ | -------------------------------------- | -------------------------------------- |
| ETL      | Extract, Transform, Load | Before loading, in the pipeline tool   | Traditional warehouses, smaller data   |
| ELT      | Extract, Load, Transform | After loading, using the store's power | Data lakes and modern cloud warehouses |

Pipelines are the orchestration unit: a series of activities that move and transform data, run on schedules or triggers. Azure Data Factory and Microsoft Fabric pipelines are the recognition answers for "build and schedule data movement".

| Ingestion concern             | What to think                               |
| ----------------------------- | ------------------------------------------- |
| Many sources, scheduled loads | Batch pipeline with connectors              |
| Continuous events             | Streaming ingestion (event capture)         |
| Cleansing and shaping         | Transformation activities, Spark, or SQL    |
| Orchestration and retries     | Pipeline control flow, triggers, monitoring |

## Analytical data stores

| Store          | Holds                                        | Strength                                          |
| -------------- | -------------------------------------------- | ------------------------------------------------- |
| Data warehouse | Modeled relational tables (star schema)      | Fast SQL over curated, structured history         |
| Data lake      | Raw files of any format (Parquet, CSV, JSON) | Cheap scale for all data shapes, schema-on-read   |
| Lakehouse      | Lake files plus table/SQL layer on top       | One copy of data serving both engineering and SQL |

Supporting ideas:

- A star schema puts numeric facts in a fact table and descriptive attributes in dimension tables, which makes aggregating queries fast and simple.
- Data lakes typically use Azure Data Lake Storage Gen2. Files are often stored in Parquet for efficient analytics.
- In Microsoft Fabric, OneLake is the single built-in data lake that all Fabric workloads share.

## Microsoft cloud services for large-scale analytics

The current outline names two services to know well: Azure Databricks and Microsoft Fabric.

| Service          | What it is                                                                                                        | Strongest when...                                                     |
| ---------------- | ----------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------- |
| Azure Databricks | Apache Spark based analytics platform with collaborative notebooks                                                | Spark skills, big data engineering, data science and machine learning |
| Microsoft Fabric | All-in-one SaaS analytics platform: pipelines, lakehouse, warehouse, real-time intelligence, Power BI, on OneLake | End-to-end analytics in one product with minimal infrastructure       |

Microsoft Fabric experiences worth recognizing:

| Fabric workload        | Purpose                                            |
| ---------------------- | -------------------------------------------------- |
| Data Factory           | Pipelines and dataflows for ingestion and movement |
| Data Engineering       | Spark notebooks and lakehouses                     |
| Data Warehouse         | Full T-SQL warehouse over OneLake                  |
| Real-Time Intelligence | Eventstreams and KQL queries over streaming data   |
| Data Science           | Machine learning model development                 |
| Power BI               | Reports and dashboards over the same OneLake data  |

Azure Databricks facts: built on Apache Spark, uses workspaces and notebooks (Python, Scala, SQL, R), handles massive parallel processing, and is a common choice for machine learning and lakehouse engineering. It runs in Azure but is also available on other clouds.

Context note: Azure Synapse Analytics served many of these needs previously; Microsoft's current fundamentals outline emphasizes Microsoft Fabric, which brings the warehouse, pipeline, and real-time capabilities together as SaaS.

## Batch vs streaming data

| Aspect       | Batch                                       | Streaming                                      |
| ------------ | ------------------------------------------- | ---------------------------------------------- |
| Data arrives | Collected, then processed in groups         | Processed continuously as events occur         |
| Latency      | Minutes to hours after collection           | Seconds or less                                |
| Scope        | Complete datasets, complex heavy processing | Rolling windows over recent events             |
| Examples     | Nightly sales load, monthly billing         | Fraud detection, live telemetry, stock tickers |

Many architectures combine both: stream for immediate signals, batch for complete historical analysis.

## Real-time analytics services

| Service                                       | Role in real-time analytics                                         |
| --------------------------------------------- | ------------------------------------------------------------------- |
| Microsoft Fabric Real-Time Intelligence       | Capture eventstreams, store events in an eventhouse, query with KQL |
| Azure Stream Analytics                        | SQL-like queries over event streams with windowing                  |
| Azure Event Hubs                              | High-scale event ingestion front door                               |
| Azure IoT Hub                                 | Event ingestion plus device management for IoT                      |
| Azure Databricks (Spark Structured Streaming) | Spark-based stream processing in notebooks/jobs                     |

Recognition shortcuts: Event Hubs and IoT Hub ingest events (IoT Hub adds two-way device management). Stream Analytics and Fabric Real-Time Intelligence process and query the streams. KQL (Kusto Query Language) is the query language for real-time event data in Fabric eventhouses and Azure Data Explorer.

## Data visualization with Microsoft Power BI

Power BI is Microsoft's business intelligence suite for modeling and visualizing data.

| Component        | Purpose                                                       |
| ---------------- | ------------------------------------------------------------- |
| Power BI Desktop | Free Windows app where you connect, model, and design reports |
| Power BI service | Cloud service (app.powerbi.com) to publish, share, and view   |
| Power BI Mobile  | Phone and tablet apps for consuming reports and dashboards    |

Typical workflow: connect and model data in Power BI Desktop, publish the report to the Power BI service, share with consumers who view it in the browser or mobile app.

### Data models in Power BI

A data model (semantic model) defines tables, relationships, and calculations that reports are built on.

| Model feature             | What it does                                                          |
| ------------------------- | --------------------------------------------------------------------- |
| Relationships             | Link tables (typically facts to dimensions in a star schema)          |
| Measures                  | Calculations (often written in DAX) such as totals and ratios         |
| Hierarchies               | Drill-down paths such as Year to Quarter to Month, or Country to City |
| Data types and categories | Control formatting, aggregation, and map behavior                     |

Exam tip: analytical models are usually built as star schemas: fact tables hold numeric measures, dimension tables hold the attributes you slice by.

### Choosing the right visualization

| You want to show...                     | Use                         |
| --------------------------------------- | --------------------------- |
| Comparison across categories            | Bar or column chart         |
| Trends over time                        | Line or area chart          |
| Part-to-whole proportions               | Pie or donut chart, treemap |
| Relationship between two numeric values | Scatter chart               |
| A single important number               | Card or KPI                 |
| Geographic data                         | Map visuals                 |
| Detailed values in rows and columns     | Table or matrix             |
| Filtering the rest of the report page   | Slicer                      |

Report vs dashboard: a report is a multi-page, interactive set of visuals built on one semantic model; a dashboard is a single page of tiles pinned from one or more reports in the Power BI service.

## Common confusions

| Confusion                            | Correct idea                                                                             |
| ------------------------------------ | ---------------------------------------------------------------------------------------- |
| ETL vs ELT                           | ETL transforms before loading; ELT loads raw data then transforms in the store           |
| Data lake vs data warehouse          | Lake stores raw files of any shape; warehouse stores curated relational tables           |
| Lakehouse vs warehouse               | Lakehouse keeps data as open lake files with table access; warehouse is fully relational |
| Batch vs streaming                   | Scheduled groups of data vs continuous event-by-event processing                         |
| Azure Databricks vs Microsoft Fabric | Spark-first platform for engineers/scientists vs all-in-one SaaS analytics suite         |
| Event Hubs vs Stream Analytics       | Event Hubs ingests streams; Stream Analytics queries and processes them                  |
| Power BI report vs dashboard         | Report: multi-page from one model; dashboard: pinned tiles from many reports             |
| Power BI Desktop vs service          | Desktop creates and models; the service publishes, shares, and hosts dashboards          |

## Exam traps

| Trap                                                | Why people miss it                                                              |
| --------------------------------------------------- | ------------------------------------------------------------------------------- |
| "Use Power BI to move data between stores"          | Power BI visualizes; pipelines (Data Factory or Fabric) move and transform data |
| "Streaming means very fast batch jobs"              | Streaming processes each event as it arrives; batch waits and processes groups  |
| "A data lake requires structured data"              | Lakes accept raw data of any shape; structure is applied when read              |
| "Dashboards are created in Power BI Desktop"        | Dashboards exist only in the Power BI service; Desktop creates reports          |
| "KQL is used to query relational warehouses"        | KQL queries event/log stores (eventhouses); warehouses use T-SQL                |
| "Fabric is an IaaS product you must size and patch" | Fabric is SaaS; capacity is assigned, not infrastructure you manage             |
| "Pie charts show trends over time"                  | Time trends need a line chart; pie shows part-to-whole at one point             |

## Mini scenarios

| Scenario                                                                              | Best answer                                         |
| ------------------------------------------------------------------------------------- | --------------------------------------------------- |
| A retailer loads sales from 40 stores every night into a central store for reporting. | Batch ingestion into a data warehouse               |
| A team wants raw JSON, CSV, and image files stored cheaply for future analytics.      | Data lake (Azure Data Lake Storage Gen2)            |
| Data scientists need Spark notebooks for machine learning over huge datasets.         | Azure Databricks                                    |
| A company wants pipelines, a warehouse, and Power BI in one SaaS platform.            | Microsoft Fabric                                    |
| A bank must flag suspicious card transactions within seconds.                         | Real-time / streaming analytics                     |
| An analyst must show revenue trend by month for three years.                          | Line chart                                          |
| A manager wants one page of the most important tiles from several reports.            | Power BI dashboard in the service                   |
| Millions of device events per second need a scalable ingestion entry point.           | Azure Event Hubs (or IoT Hub for device management) |

## Check yourself

1. What are the four broad stages of an analytics pipeline?
2. What is the difference between ETL and ELT?
3. How does a data lake differ from a data warehouse, and what is a lakehouse?
4. Which two services does the current outline name for large-scale analytics, and how do they differ?
5. What is OneLake?
6. Give two examples each of batch and streaming workloads.
7. Which components make up Power BI, and what does each do?
8. Which visualization fits: trend over time, part-to-whole, correlation of two measures, one key number?

## Answer guide

1. Ingest, store, process/model, visualize.
2. ETL transforms data before loading it into the destination; ELT loads raw data first and transforms it inside the destination store.
3. A lake stores raw files of any format (schema-on-read); a warehouse stores curated relational tables (schema-on-write); a lakehouse layers table structure and SQL over lake files so one copy serves both.
4. Azure Databricks (Apache Spark platform for data engineering, data science, ML) and Microsoft Fabric (all-in-one SaaS analytics platform on OneLake).
5. Microsoft Fabric's single, built-in data lake that all Fabric workloads share.
6. Batch: nightly sales load, monthly billing run. Streaming: fraud detection, live IoT telemetry.
7. Power BI Desktop (create and model reports), Power BI service (publish, share, dashboards), Power BI Mobile (consume on devices).
8. Line chart; pie/donut chart; scatter chart; card or KPI.
