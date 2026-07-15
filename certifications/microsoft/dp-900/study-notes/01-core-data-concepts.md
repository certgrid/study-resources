# 01 - Describe Core Data Concepts

This domain is worth 25-30% of the exam. It covers how data is shaped, how it is stored, what transactional and analytical workloads look like, and who does what on a data team. Questions here are usually vocabulary-based: they describe some data or a job duty and ask you to name it.

## Mental model

Think of every DP-900 question in this domain as asking one of four things: what shape is the data, where should it live, what kind of workload is this, or whose job is this? Match the keywords in the scenario to the concept.

| Scenario keyword                              | Likely concept         |
| --------------------------------------------- | ---------------------- |
| Rows and columns with a fixed schema          | Structured data        |
| JSON documents with varying fields            | Semi-structured data   |
| Images, video, audio, free-form documents     | Unstructured data      |
| Many small reads and writes, must be reliable | Transactional (OLTP)   |
| Analyze large history for trends and reports  | Analytical (OLAP)      |
| Backup, security, availability of databases   | Database administrator |
| Build pipelines to ingest and transform data  | Data engineer          |
| Build reports and find insights               | Data analyst           |

## Ways to represent data

Data comes in three shapes. The exam expects you to classify examples instantly.

| Shape           | Definition                                                    | Schema                        | Typical examples                       |
| --------------- | ------------------------------------------------------------- | ----------------------------- | -------------------------------------- |
| Structured      | Data that fits a fixed tabular model of rows and columns      | Fixed, defined before writing | Relational tables, spreadsheets        |
| Semi-structured | Data with some structure, but fields can vary between records | Flexible, defined per record  | JSON, XML, key-value pairs, graph data |
| Unstructured    | Data with no predefined structure to query directly           | None                          | Images, video, audio, PDFs, free text  |

Key ideas:

- Structured data is defined schema-on-write: the table design exists first, then data must fit it.
- Semi-structured data carries its own structure with it (like field names inside a JSON document), so two records in the same store can have different fields.
- Unstructured data is usually stored as files or blobs, and you analyze it with specialized tools rather than direct queries.

| If the question says...                              | Think...        |
| ---------------------------------------------------- | --------------- |
| "Each record must match the same column definitions" | Structured      |
| "Documents where some records have extra fields"     | Semi-structured |
| "Video footage from security cameras"                | Unstructured    |
| "Sensor readings sent as JSON"                       | Semi-structured |

## Common data file formats

| Format  | Type                 | Best known for                                                  |
| ------- | -------------------- | --------------------------------------------------------------- |
| CSV     | Delimited text       | Simple tabular exchange, human readable, no data types          |
| JSON    | Text, hierarchical   | Semi-structured documents, APIs, flexible attributes            |
| XML     | Text, hierarchical   | Older document exchange with tags and schemas                   |
| Avro    | Binary, row-based    | Efficient serialization, good for write-heavy and streaming use |
| ORC     | Binary, column-based | Optimized for analytical reads in big data systems              |
| Parquet | Binary, column-based | The common analytical format; efficient compression and reads   |
| BLOB    | Binary large object  | Images, video, audio, and other unstructured binary data        |

Memory hook: Avro is row-based (good for writing streams of records); ORC and Parquet are column-based (good for analytical queries that read a few columns from many rows).

## Data stores and databases

| Store type             | Model                                       | Example use                              |
| ---------------------- | ------------------------------------------- | ---------------------------------------- |
| Relational database    | Tables with rows, columns, keys             | Orders, customers, banking transactions  |
| Key-value store        | Unique key points to an opaque value        | Session state, caching, simple lookups   |
| Document database      | JSON-style documents grouped in collections | Product catalogs with varying attributes |
| Column-family database | Rows with column families, wide tables      | Large-scale telemetry, time-ordered data |
| Graph database         | Nodes and edges with relationships          | Social networks, recommendation engines  |
| Object/file storage    | Files and binary objects                    | Media, backups, data lake files          |

Relational databases enforce a schema and support joins and transactions. Non-relational (NoSQL) stores trade fixed schemas for flexibility and horizontal scale.

## Azure data stores for common use cases

| Use case                                           | Azure service                          |
| -------------------------------------------------- | -------------------------------------- |
| Managed relational database with T-SQL             | Azure SQL Database                     |
| Open-source relational database                    | Azure Database for PostgreSQL or MySQL |
| Globally distributed NoSQL, multiple APIs          | Azure Cosmos DB                        |
| Unstructured objects: media, backups, logs         | Azure Blob Storage                     |
| Data lake files for analytics                      | Azure Data Lake Storage Gen2           |
| Lift-and-shift SMB/NFS file shares                 | Azure Files                            |
| Simple key-value NoSQL tables                      | Azure Table Storage                    |
| Unified analytics: lakehouse, warehouse, real time | Microsoft Fabric                       |

## Transactional workloads (OLTP)

OLTP (online transaction processing) systems record business events as they happen: orders, payments, bookings, inventory changes.

| Characteristic | Transactional (OLTP)                             |
| -------------- | ------------------------------------------------ |
| Operations     | Many small reads and writes                      |
| Users          | Many concurrent users                            |
| Data volume    | Current operational data                         |
| Schema         | Highly normalized to avoid duplication           |
| Priority       | Data integrity, speed of individual transactions |
| Example        | Processing an online store checkout              |

Transactions follow the ACID properties:

| Property    | Meaning                                                          |
| ----------- | ---------------------------------------------------------------- |
| Atomicity   | A transaction fully succeeds or fully fails; no partial updates  |
| Consistency | A transaction moves the database from one valid state to another |
| Isolation   | Concurrent transactions do not interfere with each other         |
| Durability  | Once committed, changes survive failures                         |

## Analytical workloads (OLAP)

OLAP (online analytical processing) systems answer questions about large volumes of historical data: trends, aggregations, comparisons.

| Characteristic | Analytical (OLAP)                                 |
| -------------- | ------------------------------------------------- |
| Operations     | Large reads, few bulk writes (loads)              |
| Users          | Fewer users: analysts, data scientists, reports   |
| Data volume    | Large historical data, often from many sources    |
| Schema         | Often denormalized (star schema) for fast reads   |
| Priority       | Query performance over huge datasets              |
| Example        | A yearly sales trend dashboard across all regions |

A typical analytical architecture: ingest data from sources, store it in a data lake or data warehouse, process and model it, then visualize it in reports.

| OLTP vs OLAP | OLTP                  | OLAP                       |
| ------------ | --------------------- | -------------------------- |
| Purpose      | Run the business      | Analyze the business       |
| Writes       | Constant small writes | Periodic bulk loads        |
| Queries      | Short, targeted       | Long, aggregating          |
| Data age     | Current               | Historical                 |
| Schema style | Normalized            | Denormalized (star schema) |

## Data roles and responsibilities

| Role                   | Core responsibilities                                                                                        |
| ---------------------- | ------------------------------------------------------------------------------------------------------------ |
| Database administrator | Install, configure, back up, restore, secure databases; manage availability and performance; grant access    |
| Data engineer          | Build and manage data pipelines; ingest, clean, and transform data; manage data stores and privacy           |
| Data analyst           | Explore and model data; build reports and visualizations; find insights and communicate them to the business |

| If the task is...                          | The role is...         |
| ------------------------------------------ | ---------------------- |
| Configure database backups and restores    | Database administrator |
| Implement security and grant user access   | Database administrator |
| Build an ingestion pipeline from sources   | Data engineer          |
| Clean and transform raw data for analytics | Data engineer          |
| Build a Power BI report for sales trends   | Data analyst           |
| Choose the right chart to show the data    | Data analyst           |

## Common confusions

| Confusion                               | Correct idea                                                                    |
| --------------------------------------- | ------------------------------------------------------------------------------- |
| Semi-structured vs unstructured         | JSON and XML carry structure inside the data; images and video carry none       |
| Structured vs relational                | Structured means tabular shape; relational is the database model that stores it |
| OLTP vs OLAP                            | OLTP records events now; OLAP analyzes history                                  |
| Avro vs Parquet                         | Avro is row-based (write friendly); Parquet is column-based (read friendly)     |
| Data engineer vs database administrator | Engineers move and transform data; DBAs run and protect database systems        |
| Data engineer vs data analyst           | Engineers prepare data; analysts explore it and build reports                   |

## Exam traps

| Trap                                             | Why people miss it                                                                  |
| ------------------------------------------------ | ----------------------------------------------------------------------------------- |
| "JSON is unstructured"                           | JSON is semi-structured; it has fields and values, just not a fixed schema          |
| "A data warehouse is good for OLTP"              | Warehouses are for analytics; OLTP needs a transactional database                   |
| "Normalization helps analytical queries"         | Normalization helps write integrity; analytics usually prefers denormalized schemas |
| "The data analyst builds the ingestion pipeline" | Pipelines are data engineer work; analysts model and visualize                      |
| "CSV stores data types"                          | CSV is plain text; types are inferred by whatever reads it                          |

## Mini scenarios

| Scenario                                                                            | Best answer                             |
| ----------------------------------------------------------------------------------- | --------------------------------------- |
| A retailer must record thousands of small purchases per minute with full integrity. | Transactional (OLTP) workload           |
| An airline wants to analyze five years of bookings for seasonal trends.             | Analytical (OLAP) workload              |
| Product records share common fields but each category adds its own attributes.      | Semi-structured (document) data         |
| A hospital stores MRI scan images.                                                  | Unstructured data in Blob Storage       |
| A team needs someone to configure backups and manage database security.             | Database administrator                  |
| Sensor data lands as files that must be cleaned and combined nightly.               | Data engineer building a batch pipeline |

## Check yourself

1. What are the three shapes of data, and which one does a JSON document belong to?
2. Which file formats are column-based and why does that matter for analytics?
3. What do the four ACID properties guarantee?
4. Name three differences between OLTP and OLAP workloads.
5. Which Azure service is the default choice for unstructured files like video?
6. Who is responsible for database backups: the DBA, the data engineer, or the data analyst?
7. Why do transactional databases use normalized schemas?
8. Which store type fits a social network of people connected to other people?

## Answer guide

1. Structured, semi-structured, unstructured. JSON is semi-structured.
2. ORC and Parquet. Column storage lets analytical queries read only the needed columns, which is faster and compresses better.
3. Atomicity (all or nothing), consistency (valid state to valid state), isolation (transactions do not interfere), durability (committed changes survive failure).
4. OLTP: many small reads/writes, current data, normalized schema, many users. OLAP: bulk loads and big reads, historical data, denormalized schema, fewer users.
5. Azure Blob Storage.
6. The database administrator.
7. Normalization removes duplication, which protects integrity and keeps small writes fast.
8. A graph database (nodes and edges).
