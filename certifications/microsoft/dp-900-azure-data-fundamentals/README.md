# DP-900: Azure Data Fundamentals - Study Cheatsheet

The DP-900: Azure Data Fundamentals exam validates foundational knowledge of core data concepts and how they are implemented using Microsoft Azure data services. It is aimed at candidates beginning to work with data in the cloud - including business stakeholders, students, and anyone preparing for role-based Azure data certifications - and requires no prior hands-on experience. The exam covers data concepts, relational data, non-relational data, and analytics workloads on Azure.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | DP-900 |
| Credential | DP-900: Azure Data Fundamentals |
| Level | Beginner |
| Practice mock length | ~40 questions |
| Duration | ~45 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-06-24 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Describe Core Data Concepts | ~27% |
| 2 | Identify Considerations for Relational Data | ~25% |
| 3 | Describe Considerations for Non-Relational Data | ~25% |
| 4 | Describe an Analytics Workload | ~22% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Describe Core Data Concepts

- Structured data conforms to a fixed schema with defined columns and data types (relational tables); semi-structured data has some organization via tags or keys but variable fields (JSON, XML, key-value); unstructured data has no predefined model (images, video, audio, PDFs, free-form text).
- OLTP (Online Transaction Processing) systems handle many short, atomic, real-time read/write transactions, use highly normalized schemas to minimize redundancy, and are optimized for fast inserts, updates, and deletes.
- OLAP (Online Analytical Processing) systems are optimized for complex analytical queries over large volumes of historical data, use denormalized schemas (star/snowflake), and support aggregation and trend analysis rather than frequent transactional updates.
- The ACID properties guarantee reliable transactions: Atomicity (all-or-nothing), Consistency (valid state to valid state), Isolation (concurrent transactions do not interfere), and Durability (committed transactions survive failures).
- Durability is achieved through transaction logs and write-ahead logging, ensuring committed changes persist even after power loss, hardware failure, or crashes.
- ETL (Extract, Transform, Load) transforms data before loading it into the target; ELT (Extract, Load, Transform) loads raw data first and transforms it using the target system's compute, which suits scalable cloud platforms and preserves raw data.

### Domain 2 - Identify Considerations for Relational Data

- Azure SQL Database is a fully managed PaaS offering for new cloud applications, with built-in high availability (99.99% SLA), automated backups with point-in-time restore, automatic patching, and no OS access.
- Azure SQL Managed Instance provides near 100% compatibility with on-premises SQL Server (SQL Server Agent, cross-database queries, SSIS, CLR) and is the best choice for lift-and-shift migrations with minimal code changes.
- SQL Server on Azure Virtual Machines is IaaS, giving full control over the OS and SQL Server instance; choose it when you need OS-level access or features not available in the managed offerings.
- Azure SQL Database elastic pools let multiple databases share a pool of compute (DTUs or vCores), optimizing cost when databases have varying, non-overlapping peak usage patterns.
- Azure offers managed open-source relational databases: Azure Database for MySQL and Azure Database for PostgreSQL - choose the one matching the application's existing engine for minimal migration changes. (Azure Database for MariaDB was retired on 19 September 2025; migrate MariaDB workloads to Azure Database for MySQL Flexible Server.)
- Purchasing/compute models include the DTU model and the vCore model; the provisioned compute tier reserves capacity for predictable workloads, while serverless auto-scales and can pause for intermittent workloads.

### Domain 3 - Describe Considerations for Non-Relational Data

- Azure Cosmos DB is a globally distributed, multi-model NoSQL database guaranteeing single-digit millisecond latency at the 99th percentile, automatic multi-region replication, and elastic horizontal scaling.
- Cosmos DB APIs include API for NoSQL (Core, the native API using SQL-like queries), API for MongoDB, API for Apache Cassandra, API for Apache Gremlin (graph), and API for Table - the API is chosen at account creation and cannot be changed afterward.
- Use the Cosmos DB API for MongoDB to migrate existing MongoDB apps with minimal change, and the Gremlin (graph) API for traversing relationships such as finding routes or connections between entities.
- Cosmos DB offers five consistency levels from strongest to weakest: Strong, Bounded Staleness, Session (default), Consistent Prefix, and Eventual - stronger consistency increases latency, weaker consistency improves performance and availability.
- A partition key determines how data is logically and physically distributed across partitions; choose one with high cardinality and even access distribution to avoid hot partitions and enable horizontal scale.
- Azure Blob Storage stores large unstructured objects (files, images, video, backups) in a flat namespace of containers and blobs - it is object storage, not tabular storage.

### Domain 4 - Describe an Analytics Workload

- Azure Synapse Analytics is an integrated analytics platform combining dedicated SQL pools (MPP - massively parallel processing - for data warehousing), serverless SQL pools (on-demand querying of data lake files), Apache Spark pools (big-data processing), and Synapse Pipelines for orchestration.
- Dedicated SQL pools use massively parallel processing to run large data-warehouse queries; serverless SQL pools let you query files in the data lake on demand without provisioning capacity, charging per data processed.
- Azure Data Factory is Azure's cloud ETL/ELT orchestration service for building, scheduling, and monitoring data pipelines that move and transform data between sources and destinations.
- A self-hosted integration runtime is a gateway installed on-premises that lets Azure Data Factory securely access on-premises data sources without exposing them to the public internet.
- Azure Stream Analytics is a fully managed real-time analytics engine that ingests continuous event streams (often from Azure Event Hubs or IoT Hub) and processes them with SQL-like queries and time windows.
- Azure Event Hubs is a big-data streaming ingestion service for high-throughput event data; IoT Hub adds bidirectional device communication for IoT telemetry.

## Study tips

- DP-900 is conceptual, not hands-on - focus on knowing what each Azure service does and when to choose it (for example SQL Database vs. Managed Instance vs. SQL on a VM, or Blob vs. Data Lake Gen2 vs. Table Storage).
- Memorize the mapping of workload type to service: OLTP relational to Azure SQL Database, big-data/document NoSQL to Cosmos DB, object/file storage to Blob/Data Lake Gen2, data warehousing to Synapse, ETL orchestration to Data Factory, and real-time streaming to Stream Analytics.
- Be precise on terminology that the exam tests as true/false or multiple-select: ACID properties, ETL vs. ELT order, structured vs. semi-structured vs. unstructured, star vs. snowflake, and DDL vs. DML vs. DCL.
- Watch for multiple-response questions (Select all / pick two or three) and case-style scenarios that describe a business need - read the requirement carefully and match it to the single best service or feature.
- You need a scaled score of 700 (out of 1000) to pass and have about 45 minutes; pace yourself, answer every question (there is no penalty for guessing), and flag uncertain items for review.

---

Want the full breakdown? See the complete **[DP-900 study guide](https://certgrid.app/study-guide/dp-900-azure-data-fundamentals)** and **[free practice questions](https://certgrid.app/practice/dp-900-azure-data-fundamentals)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

