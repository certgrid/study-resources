# DP-900 Data Landscape

This page gives a simple visual overview of the Azure data landscape.

Use these diagrams as memory anchors before practice tests. DP-900 rarely asks you to draw architecture, but it constantly asks which service fits a data shape or where a service sits in an analytics pipeline.

## Relational vs non-relational landscape

```mermaid
flowchart TD
    DATA[What shape is the data?]
    REL[Relational: tables, fixed schema]
    NONREL[Non-relational: flexible or binary]

    SQLDB[Azure SQL Database]
    SQLMI[Azure SQL Managed Instance]
    SQLVM[SQL Server on Azure VMs]
    OSS[Azure Database for MySQL / PostgreSQL]

    COSMOS[Azure Cosmos DB]
    BLOB[Blob Storage]
    FILES[Azure Files]
    TABLE[Table Storage]

    DATA --> REL
    DATA --> NONREL
    REL --> SQLDB
    REL --> SQLMI
    REL --> SQLVM
    REL --> OSS
    NONREL --> COSMOS
    NONREL --> BLOB
    NONREL --> FILES
    NONREL --> TABLE
```

Exam memory hook:

```text
Fixed rows and columns  = relational family
JSON documents / global = Cosmos DB
Objects behind URLs     = Blob Storage
Mounted shares          = Azure Files
Cheap key-value rows    = Table Storage
```

## Azure SQL family control ladder

```mermaid
flowchart LR
    LESS[Least management effort]
    MORE[Most control]

    DB[Azure SQL Database<br/>PaaS single database]
    MI[Azure SQL Managed Instance<br/>PaaS near-full instance]
    VM[SQL Server on Azure VMs<br/>IaaS full control]

    LESS --> DB --> MI --> VM --> MORE
```

Exam memory hook: management effort and control move in opposite directions. New app means SQL Database; migration needing instance features means Managed Instance; OS access means the VM.

## Storage options by data shape

```mermaid
flowchart TD
    Q[What do you need to store?]
    OBJ[Objects: media, backups, logs]
    SHR[Shared folder over SMB/NFS]
    KV[Key-value entities]
    LAKE[Analytics files with hierarchy]

    Q --> OBJ --> B[Blob Storage<br/>Hot / Cool / Cold / Archive]
    Q --> SHR --> F[Azure Files]
    Q --> KV --> T[Table Storage<br/>PartitionKey + RowKey]
    Q --> LAKE --> D[Data Lake Storage Gen2<br/>Blob + hierarchical namespace]
```

Exam memory hook:

```text
Hot     = frequent access
Cool    = infrequent, online
Cold    = rare, online
Archive = offline, rehydrate first
```

## Analytics pipeline

```mermaid
flowchart LR
    SRC[Sources<br/>databases, files, APIs, devices]
    ING[Ingest<br/>Data Factory / Fabric pipelines<br/>Event Hubs for streams]
    STORE[Store<br/>Data lake / lakehouse / warehouse<br/>OneLake in Fabric]
    PROC[Process and model<br/>Databricks Spark / Fabric<br/>Stream Analytics for real time]
    VIZ[Visualize<br/>Power BI reports and dashboards]

    SRC --> ING --> STORE --> PROC --> VIZ
```

Exam memory hook: ingest, store, process, visualize. Pipelines move data, Databricks and Fabric process it at scale, Power BI shows it. If the scenario says "within seconds", swap the batch pieces for streaming ones (Event Hubs or IoT Hub in, Stream Analytics or Fabric Real-Time Intelligence to process).

## Batch vs streaming paths

```mermaid
flowchart TD
    EVENTS[Data is generated]
    BATCH[Batch path]
    STREAM[Streaming path]

    EVENTS --> BATCH
    EVENTS --> STREAM

    BATCH --> BP[Collect over time]
    BP --> BL[Scheduled pipeline load]
    BL --> BW[Warehouse or lakehouse]
    BW --> BR[Reports on history]

    STREAM --> SI[Event Hubs / IoT Hub]
    SI --> SP[Stream Analytics / Fabric Real-Time Intelligence]
    SP --> SD[Live dashboards and alerts]
```

Exam memory hook: batch waits and processes groups (latency in minutes or hours); streaming handles each event as it arrives (latency in seconds). Fraud alerts and live telemetry are streaming; nightly loads and monthly billing are batch.
