# 03 - Describe Considerations for Working with Non-Relational Data on Azure

This domain is worth 15-20% of the exam. It covers the Azure Storage services (Blob, Files, Table) and Azure Cosmos DB with its APIs. It is the smallest domain, but the service-choice questions are very predictable, so it is easy scoring once the pairs are clear.

## Mental model

Non-relational questions almost always give you a data shape or an access pattern and ask which store fits. Decide first: is it files/objects (Azure Storage) or database items (Cosmos DB)? Then match the keyword.

| Scenario keyword                                     | Likely service                     |
| ---------------------------------------------------- | ---------------------------------- |
| Images, video, backups, log files, any binary object | Azure Blob Storage                 |
| Mount a shared drive over SMB or NFS                 | Azure Files                        |
| Cheap key-value rows with partition and row key      | Azure Table Storage                |
| Global distribution, millisecond latency, JSON items | Azure Cosmos DB                    |
| Existing MongoDB app moving to Azure                 | Azure Cosmos DB for MongoDB        |
| Graph data with nodes and edges                      | Azure Cosmos DB for Apache Gremlin |
| Analytics files with a folder hierarchy              | Azure Data Lake Storage Gen2       |

## Azure Storage overview

An Azure storage account is the container for Blob, Files, Table, and Queue services. One account gives you a unique namespace, redundancy settings, and access keys shared by the services inside it.

| Service       | Data shape                | Access style                          |
| ------------- | ------------------------- | ------------------------------------- |
| Blob storage  | Objects (any binary/text) | REST/HTTPS, SDKs, URL per blob        |
| Azure Files   | Files in folders          | Mounted shares over SMB or NFS        |
| Table storage | Key-value entities        | REST/SDK queries by partition/row key |
| Queue storage | Messages                  | Enqueue and dequeue between app parts |

Redundancy options to recognize: LRS (copies within one datacenter), ZRS (copies across availability zones), GRS (copies to a paired region), GZRS (zones plus paired region).

## Azure Blob storage

Blob storage is object storage for massive amounts of unstructured data. Blobs live inside containers, and each blob is addressable by URL.

| Blob type   | Optimized for                                               |
| ----------- | ----------------------------------------------------------- |
| Block blob  | General files uploaded in blocks: media, documents, backups |
| Page blob   | Random read/write access: virtual machine disks             |
| Append blob | Append-only writes: logging scenarios                       |

Access tiers balance storage cost against access cost and speed:

| Tier    | Use for                      | Cost pattern                            |
| ------- | ---------------------------- | --------------------------------------- |
| Hot     | Frequently accessed data     | Higher storage cost, lowest access cost |
| Cool    | Infrequently accessed data   | Lower storage cost, higher access cost  |
| Cold    | Rarely accessed data         | Lower still, higher access cost         |
| Archive | Long-term retention, offline | Lowest storage cost, hours to rehydrate |

Key Blob facts:

- Flat namespace by default: "folders" are just name prefixes inside a container.
- Lifecycle management rules can move blobs to cooler tiers or delete them automatically.
- Azure Data Lake Storage Gen2 is Blob storage with a hierarchical namespace enabled, adding real directories and POSIX-style permissions for analytics workloads.

## Azure Files

Azure Files provides fully managed file shares in the cloud.

| Feature   | Detail                                                                         |
| --------- | ------------------------------------------------------------------------------ |
| Protocols | SMB (Windows, Linux, macOS) and NFS (Linux)                                    |
| Mounting  | Shares mount like a normal network drive                                       |
| Use cases | Lift and shift apps that expect a file share, shared configs, home directories |
| Sync      | Azure File Sync caches shares on Windows Server for fast local access          |

Choose Azure Files over Blob storage when applications expect file system semantics (drive letters, paths, file locking) rather than object URLs.

## Azure Table storage

Table storage is a NoSQL key-value store for large amounts of structured, non-relational data.

| Concept       | Meaning                                                      |
| ------------- | ------------------------------------------------------------ |
| Entity        | One item (like a row), up to 1 MB, with up to 252 properties |
| Partition key | Groups related entities; enables scale-out and fast lookups  |
| Row key       | Unique ID within a partition                                 |
| Schemaless    | Entities in the same table can have different properties     |

Facts to recognize:

- Lookups by partition key plus row key are extremely fast; there are no joins, foreign keys, or stored procedures.
- It is a low-cost option for simple, huge tables such as device data or user profiles.
- Denormalization is normal here: store data the way you read it.

## Azure Cosmos DB

Azure Cosmos DB is Microsoft's globally distributed, multi-model NoSQL database.

| Capability          | Detail                                                            |
| ------------------- | ----------------------------------------------------------------- |
| Global distribution | Replicate data to any Azure region with multi-region writes       |
| Latency             | Single-digit millisecond reads and writes at any scale            |
| Elastic scale       | Throughput and storage scale horizontally via partitioning        |
| Schema flexibility  | Items in a container can have different structures                |
| SLAs                | Guarantees for availability, latency, throughput, and consistency |

Common use cases: IoT telemetry ingestion, retail product catalogs, gaming leaderboards and state, web session data, and any global app needing low-latency reads and writes near its users.

## Azure Cosmos DB APIs

Cosmos DB exposes several APIs so teams can use existing skills and tools. Picking the right API is a favorite exam question.

| API                                  | Data model             | Choose when...                                                 |
| ------------------------------------ | ---------------------- | -------------------------------------------------------------- |
| Azure Cosmos DB for NoSQL            | JSON documents         | New projects; native API with SQL-like queries over documents  |
| Azure Cosmos DB for MongoDB          | BSON documents         | Existing MongoDB apps and tools should keep working            |
| Azure Cosmos DB for Apache Cassandra | Column-family          | Existing Cassandra apps using CQL                              |
| Azure Cosmos DB for Apache Gremlin   | Graph (nodes/edges)    | Relationship-heavy data: social graphs, recommendations        |
| Azure Cosmos DB for Table            | Key-value entities     | Table storage apps needing global scale and better performance |
| Azure Cosmos DB for PostgreSQL       | Distributed relational | Scale-out PostgreSQL with distributed tables (Citus)           |

Decision shortcut: "new app, documents" means NoSQL API; any named engine (MongoDB, Cassandra, Gremlin, PostgreSQL) means the matching API; "Table storage but global" means the Table API.

## Common confusions

| Confusion                              | Correct idea                                                                                   |
| -------------------------------------- | ---------------------------------------------------------------------------------------------- |
| Blob storage vs Azure Files            | Blobs are objects behind URLs; Files are shares you mount over SMB/NFS                         |
| Table storage vs Cosmos DB for Table   | Same programming model; Cosmos DB adds global distribution, latency SLAs, and throughput scale |
| Blob storage vs Data Lake Storage Gen2 | Data Lake Gen2 is Blob storage plus a hierarchical namespace for analytics                     |
| Cool tier vs Archive tier              | Cool is online with instant access; Archive is offline and needs rehydration                   |
| Cosmos DB for NoSQL vs for MongoDB     | NoSQL is the native document API; MongoDB API exists for MongoDB compatibility                 |
| Partition key vs row key               | Partition key groups entities for scale; row key uniquely identifies within the partition      |

## Exam traps

| Trap                                               | Why people miss it                                                           |
| -------------------------------------------------- | ---------------------------------------------------------------------------- |
| "Use Azure Files for website images"               | Static objects served by URL belong in Blob storage                          |
| "Archive tier data is instantly readable"          | Archive blobs must be rehydrated first, which can take hours                 |
| "Cosmos DB is relational because it has a SQL API" | The NoSQL API uses SQL-like syntax over JSON documents; it is not relational |
| "Table storage supports joins"                     | No joins, no foreign keys; design for lookup by partition and row key        |
| "Page blobs are for media files"                   | Page blobs back VM disks; media files are block blobs                        |
| "One storage account only holds one service"       | An account can hold blobs, files, tables, and queues together                |

## Mini scenarios

| Scenario                                                                          | Best answer                                |
| --------------------------------------------------------------------------------- | ------------------------------------------ |
| A media company stores thousands of video files for streaming.                    | Azure Blob Storage (block blobs, Hot tier) |
| An old Windows app needs its shared drive when moving to Azure.                   | Azure Files over SMB                       |
| Compliance data must be kept 7 years, is almost never read, and must be cheapest. | Blob Storage Archive tier                  |
| A global game needs player profile reads in milliseconds worldwide.               | Azure Cosmos DB                            |
| A team migrates a MongoDB app and wants no code changes.                          | Azure Cosmos DB for MongoDB                |
| A recommendation engine models users, products, and their relationships.          | Azure Cosmos DB for Apache Gremlin         |
| A simple IoT logging app needs cheap key-value rows in one region.                | Azure Table Storage                        |

## Check yourself

1. What are the three Azure Storage services this exam names, and what data shape does each hold?
2. When do you pick Azure Files instead of Blob storage?
3. What is the difference between the Cool and Archive blob tiers?
4. What do partition key and row key do in Table storage?
5. Name four Azure Cosmos DB APIs and when you would choose each.
6. Which service is Blob storage with a hierarchical namespace for analytics?
7. What capabilities make Cosmos DB attractive for a globally used app?
8. Which blob type is used for virtual machine disks?

## Answer guide

1. Blob storage holds objects/unstructured data; Azure Files holds mounted file shares; Table storage holds key-value entities.
2. When the workload expects file system semantics: mounting a share over SMB/NFS, paths, and file locking, such as lift-and-shift apps.
3. Cool is online with immediate access but higher access cost; Archive is the cheapest storage but offline, requiring rehydration that can take hours.
4. Partition key groups related entities and enables scale-out; row key uniquely identifies an entity within its partition.
5. NoSQL for new document apps; MongoDB for MongoDB compatibility; Cassandra for CQL apps; Gremlin for graph data; Table for globally scaled Table storage apps; PostgreSQL for distributed relational PostgreSQL.
6. Azure Data Lake Storage Gen2.
7. Global distribution with multi-region writes, single-digit millisecond latency, elastic scale, flexible schemas, and strong SLAs.
8. Page blobs.
