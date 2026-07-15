# DP-900 Mock Review

28 original scenario drills in shuffled domain order, weighted roughly like the official outline. Work through all of them without notes, write your answer in one line each, then check the answer guide at the bottom. These are original practice drills, not real exam questions.

| Domain                                                                 | Official weight | Drills in this set |
| ---------------------------------------------------------------------- | --------------- | ------------------ |
| Describe core data concepts                                            | 25-30%          | 8                  |
| Identify considerations for relational data on Azure                   | 20-25%          | 7                  |
| Describe considerations for working with non-relational data on Azure  | 15-20%          | 5                  |
| Describe an analytics workload on Azure                                | 25-30%          | 8                  |

## Drills

1. A supermarket chain records every till sale the moment it happens, and a payment must never be lost or half-applied when the network drops mid-checkout. What kind of workload is this, and what property set protects each sale?

2. An analyst must show how monthly revenue has moved over the past three years so leadership can spot seasonality. Which visualization fits best?

3. A manufacturer is retiring an on-premises Windows file server. Dozens of legacy desktop apps expect to open documents from a mapped drive letter over SMB. Which Azure service replaces the file server with the least disruption?

4. A team is moving an on-premises SQL Server estate to PaaS. Their nightly jobs depend on SQL Server Agent and several procedures run cross-database queries, but nobody wants to patch an operating system. Which Azure service fits?

5. A fleet of delivery vans sends telemetry as JSON documents. Newer van models add extra fields that older models do not send, yet every document still carries named fields and values. What shape of data is this?

6. A payments provider must flag a suspicious card transaction within a few seconds of it happening, not at the end of the day. What processing style is required, and name one Microsoft service that provides it?

7. A junior developer runs CREATE TABLE and DROP INDEX scripts during a release. Which category of SQL statement are they using?

8. A global retailer needs a product catalog where each category carries different attributes, reads must return in single-digit milliseconds, and shoppers on three continents should hit a nearby replica. Which Azure service fits?

9. A company is hiring someone to configure database backups and restores, manage availability, apply patches, and grant users access to the database. Which data role is this?

10. A mid-size company wants pipelines, a lakehouse, a warehouse, real-time event analysis, and Power BI reporting in a single SaaS product where all workloads share one built-in data lake. Which Microsoft product fits?

11. An analytics team stores billions of rows as files and their queries usually read only three or four columns at a time. They want a file format that minimizes how much data each query scans. Which format should they pick?

12. In an order-entry database, customer addresses are copied into every order row, and fixing one customer's address means updating hundreds of rows. What database design technique removes this duplication, and why do transactional systems apply it?

13. An operations manager wants one page showing the most important tiles pinned from several different reports, visible every morning without opening each report. What should the analyst build, and where does it live?

14. A hospital must keep seven years of MRI and X-ray image files. They are rarely opened after the first month but must be retained cheaply. Which Azure service and feature fit?

15. A data team wants one place to land raw CSV, JSON, and Parquet files for future analytics, with a hierarchical namespace so files can be organized in directories. Which Azure service is the standard choice?

16. A group of data scientists wants collaborative notebooks in Python and SQL running on Apache Spark to train machine learning models over very large datasets. Which Azure service fits best?

17. A startup runs its app on PostgreSQL on-premises and wants a managed Azure service where the app keeps working with minimal code change while Azure handles patching and backups. Which service fits?

18. A warehouse team lands raw source data into the analytical store first, then uses the store's own compute to transform it into modeled tables. Which integration pattern is this?

19. A legal team stores scanned consent forms as PDFs and courtroom audio recordings. The files have no fields you can query directly. What shape of data is this, and where does it usually live in Azure?

20. An internal app needs to store millions of simple entities looked up only by a partition key and a row key. Cost must stay as low as possible and no complex queries or multiple APIs are needed. Which Azure service fits?

21. Millions of sensors must stream events into Azure at massive scale, and operators also need to send configuration commands back down to individual devices. Which ingestion service fits?

22. A DBA wants report writers to query a simplified, pre-joined presentation of several tables without duplicating any data or granting access to the base tables. Which database object should the DBA create?

23. A job posting asks for someone to build ingestion pipelines, clean and combine raw data from many sources, and prepare it for analysts. Which data role is this?

24. In Power BI, an analyst wants users to double-click a yearly sales column and drill from Year to Quarter to Month, and also needs a total-sales calculation that recalculates under any filter. Which two data model features does the analyst need?

25. A company runs an application written against MongoDB drivers and wants to move the database to a managed Azure service without rewriting the data access code. Which service fits?

26. A vendor's application is only certified against one specific SQL Server version with a custom agent installed on the database server itself, so the team needs full control of the operating system. Which Azure option fits?

27. In an orders database, every order row must reference a customer that actually exists in the Customers table, and the database should reject orders pointing at missing customers. Which relational feature enforces this?

28. A reporting store is loaded once nightly and serves heavy aggregating queries over five years of history. The designer proposes a fact table of sales measures surrounded by dimension tables. What workload is this, and what is the schema style called?

## Answer guide

1. Transactional (OLTP) workload protected by ACID transactions. A data warehouse is the tempting wrong answer, but warehouses serve analytical reads, not many small reliable writes.

2. A line chart. A pie or donut chart is tempting because it looks summary-friendly, but pie charts show part-to-whole at one point in time, not movement across time.

3. Azure Files. Blob Storage is the tempting wrong answer because both hold files, but blobs are objects behind an HTTP API and cannot be mounted as an SMB drive the way a file share can.

4. Azure SQL Managed Instance. Azure SQL Database is tempting because it is also PaaS, but it does not provide SQL Server Agent or cross-database queries; Managed Instance offers near-full SQL Server compatibility without OS management.

5. Semi-structured data. "Unstructured" is the tempting wrong answer because the schema varies, but JSON carries named fields and values inside each document, which is exactly what semi-structured means.

6. Streaming (real-time) processing, using Microsoft Fabric Real-Time Intelligence or Azure Stream Analytics. A faster batch job is the tempting wrong answer, but batch always waits to process groups, so it can never guarantee results within seconds of each event.

7. DDL (Data Definition Language). DML is the tempting wrong answer, but DML statements (SELECT, INSERT, UPDATE, DELETE) work on rows of data, while DDL defines and removes the objects themselves.

8. Azure Cosmos DB. Azure SQL Database is tempting for a catalog, but varying attributes per category, guaranteed low-latency reads, and multi-region distribution are the classic Cosmos DB signals.

9. Database administrator. Data engineer is the tempting wrong answer, but engineers move and transform data; backups, availability, patching, and access control are the DBA's core duties.

10. Microsoft Fabric. Azure Databricks is the tempting wrong answer for "big analytics platform", but Databricks is Spark-first and does not bundle pipelines, a warehouse, real-time analysis, and Power BI as one SaaS product over OneLake.

11. Parquet. Avro is the tempting wrong answer because it is also an efficient binary format, but Avro is row-based and suits write-heavy streams; column-based Parquet lets queries read only the needed columns.

12. Normalization, applied because removing duplication protects integrity and keeps small writes fast. "It speeds up reporting queries" is the tempting wrong idea; analytics usually prefers denormalized schemas.

13. A Power BI dashboard in the Power BI service. Building it in Power BI Desktop is the tempting wrong answer, but Desktop creates reports; dashboards exist only in the service, as pinned tiles from one or more reports.

14. Azure Blob Storage using access tiers, moving the images to the archive tier after the active month. Azure Files is tempting because these are "files", but shares cost more and the images need object storage with tiering, not an SMB mount.

15. Azure Data Lake Storage Gen2. Plain Blob Storage is the tempting near-miss; Data Lake Storage Gen2 builds on it and adds the hierarchical namespace that analytics engines expect.

16. Azure Databricks. Microsoft Fabric is the tempting wrong answer since it also runs Spark, but "collaborative Spark notebooks for data science and machine learning" is the signature Databricks scenario in the outline.

17. Azure Database for PostgreSQL. Azure SQL Database is the tempting wrong answer for "managed relational PaaS", but it runs the SQL Server engine, which would force the app to be rewritten.

18. ELT (extract, load, transform). ETL is the tempting wrong answer, but in ETL the transformation happens in the pipeline before loading; here raw data lands first and the destination store does the transforming.

19. Unstructured data, usually stored in Azure Blob Storage. Semi-structured is the tempting wrong answer, but PDFs and audio carry no queryable field structure inside the data.

20. Azure Table storage. Azure Cosmos DB for Table is the tempting wrong answer because it exposes the same API, but when the requirements are only key lookups at minimal cost, plain Table storage is the fit; Cosmos DB adds global distribution and guarantees at higher cost.

21. Azure IoT Hub. Azure Event Hubs is the tempting wrong answer because it also ingests events at massive scale, but only IoT Hub adds two-way communication and device management.

22. A view. A new table is the tempting wrong answer, but a table would duplicate and desynchronize data; a view is a saved query that presents rows without storing them.

23. Data engineer. Data analyst is the tempting wrong answer because the work feeds analytics, but analysts model and visualize prepared data; building pipelines and transforming raw data is engineering.

24. A hierarchy (Year to Quarter to Month) and a measure (typically written in DAX). Calculated columns are the tempting wrong answer for the total, but a measure recalculates under any filter context instead of storing a value per row.

25. Azure Cosmos DB for MongoDB. Azure Database for PostgreSQL or MySQL is the tempting wrong family, but those are relational engines; the MongoDB API in Cosmos DB lets existing drivers keep working.

26. SQL Server on Azure Virtual Machines. Azure SQL Managed Instance is the tempting wrong answer because it offers high compatibility, but it never exposes the operating system; full OS control means IaaS.

27. A foreign key constraint. A primary key is the tempting wrong answer, but the primary key only makes customer rows unique; the foreign key on the Orders table is what forces each order to reference an existing customer.

28. An analytical (OLAP) workload using a star schema. Normalizing the design is the tempting wrong instinct, but denormalized fact and dimension tables are preferred for fast aggregating reads over history.
