# 02 - Identify Considerations for Relational Data on Azure

This domain is worth 20-25% of the exam. It covers relational concepts (tables, keys, normalization), the SQL language at a recognition level, common database objects, and the Azure relational services: the Azure SQL family plus the open-source database options.

## Mental model

Relational questions split into two groups: concept questions (what is a key, what does normalization do, which SQL statement does X) and service questions (which Azure SQL option fits this scenario). For service questions, the deciding keywords are almost always about compatibility, control, and management effort.

| Scenario keyword                                   | Likely concept or service             |
| -------------------------------------------------- | ------------------------------------- |
| Uniquely identifies each row                       | Primary key                           |
| Column that references another table's key         | Foreign key                           |
| Remove duplicated data into separate tables        | Normalization                         |
| Retrieve rows from a table                         | SELECT (DML)                          |
| Create or change a table definition                | CREATE / ALTER (DDL)                  |
| Fully managed single database, least admin effort  | Azure SQL Database                    |
| Near 100% SQL Server compatibility in PaaS         | Azure SQL Managed Instance            |
| Full OS and instance control, lift and shift as-is | SQL Server on Azure Virtual Machines  |
| Managed open-source relational database            | Azure Database for PostgreSQL / MySQL |

## Features of relational data

Relational databases store data in tables. Each table represents one entity type; each row is one instance; each column is one attribute with a defined data type.

| Term        | Meaning                                                     |
| ----------- | ----------------------------------------------------------- |
| Table       | A set of rows and columns representing one entity type      |
| Row (tuple) | One instance of the entity, for example one customer        |
| Column      | One attribute with a fixed data type, for example OrderDate |
| Primary key | Column(s) that uniquely identify each row                   |
| Foreign key | Column(s) that reference a primary key in another table     |
| Index       | Structure that speeds up finding rows by column values      |
| View        | A saved query that behaves like a virtual table             |

Key relational properties:

- All rows in a table share the same columns (fixed schema).
- Relationships between tables are made through key columns, not embedded data.
- Queries can join tables together on those keys.

## Normalization

Normalization is the process of designing tables so each fact is stored once. It splits data into related tables and links them with keys.

| Normalization does                         | Which helps with                    |
| ------------------------------------------ | ----------------------------------- |
| Separates entities into their own tables   | Clear structure, one place per fact |
| Removes duplicated data                    | Less storage, no conflicting copies |
| Links tables with primary and foreign keys | Enforced relationships and lookups  |
| Keeps updates small (change a value once)  | Fast, safe transactional writes     |

Basic rules to recognize: one table per entity, one column per attribute, a unique primary key per row, and non-key facts stored only once.

| Normalized (OLTP)         | Denormalized (analytics)            |
| ------------------------- | ----------------------------------- |
| Many small related tables | Fewer, wider tables (star schema)   |
| No duplicated facts       | Duplication accepted for read speed |
| Fast, safe writes         | Fast aggregating reads              |
| More joins needed to read | Fewer joins needed to read          |

Exam tip: if a question says data integrity and avoiding duplicate updates, the answer is normalization. If it says faster analytical queries with fewer joins, the answer is denormalization.

## SQL statements

SQL statements fall into three categories. DP-900 tests recognition, not query writing.

| Category | Full name                  | Purpose                      | Statements                     |
| -------- | -------------------------- | ---------------------------- | ------------------------------ |
| DDL      | Data Definition Language   | Define and change structure  | CREATE, ALTER, DROP, RENAME    |
| DML      | Data Manipulation Language | Work with the data in tables | SELECT, INSERT, UPDATE, DELETE |
| DCL      | Data Control Language      | Control access permissions   | GRANT, DENY, REVOKE            |

| Statement | What it does                                      |
| --------- | ------------------------------------------------- |
| SELECT    | Reads rows (optionally filtered with WHERE)       |
| INSERT    | Adds new rows                                     |
| UPDATE    | Changes values in existing rows                   |
| DELETE    | Removes rows                                      |
| CREATE    | Creates an object such as a table or view         |
| ALTER     | Changes an object's definition                    |
| DROP      | Removes an object entirely                        |
| GRANT     | Gives a permission                                |
| DENY      | Explicitly blocks a permission                    |
| REVOKE    | Removes a previously granted or denied permission |

Watch the classic trap: DELETE removes rows from a table (DML); DROP removes the table itself (DDL). TRUNCATE quickly removes all rows but keeps the table.

## Common database objects

| Object           | What it is                                              | Why it is used                                 |
| ---------------- | ------------------------------------------------------- | ---------------------------------------------- |
| Table            | The core structure holding rows of data                 | Store entity data                              |
| View             | A saved SELECT query presented as a virtual table       | Simplify or secure access to data              |
| Stored procedure | Saved SQL code that runs as a unit, can take parameters | Reuse logic, encapsulate multi-step operations |
| Index            | A lookup structure over one or more columns             | Speed up searches and joins                    |

Memory hook: a view stores a query, not data. A stored procedure stores code that performs actions. An index stores a sorted lookup so the engine avoids scanning whole tables.

## The Azure SQL family

The Azure SQL family gives three ways to run SQL Server engine workloads, from most managed to most control.

| Option                               | Type | You manage                          | Best for                                                      |
| ------------------------------------ | ---- | ----------------------------------- | ------------------------------------------------------------- |
| Azure SQL Database                   | PaaS | Just the database and its data      | New cloud apps; single databases with least management effort |
| Azure SQL Managed Instance           | PaaS | Databases within a managed instance | Migrating on-premises SQL Server with near 100% compatibility |
| SQL Server on Azure Virtual Machines | IaaS | OS, SQL Server, patching, backups   | Full control, legacy features, exact on-premises parity       |

Feature deciders the exam loves:

| Requirement in the scenario                                                                       | Choose                               |
| ------------------------------------------------------------------------------------------------- | ------------------------------------ |
| Lowest administration, automatic patching and backups                                             | Azure SQL Database                   |
| SQL Server Agent, cross-database queries, linked servers, near-full instance features in PaaS     | Azure SQL Managed Instance           |
| Full control of the operating system and SQL Server version                                       | SQL Server on Azure Virtual Machines |
| Serverless compute that pauses when idle                                                          | Azure SQL Database (serverless tier) |
| Lift and shift an entire SQL Server instance without rewriting apps, still avoiding OS management | Azure SQL Managed Instance           |

Azure SQL Database options worth recognizing: single database (its own resources) and elastic pool (multiple databases sharing resources to smooth out variable usage).

All PaaS options include built-in high availability, automated backups, and automatic updates. The IaaS option puts patching, backups, and availability design on you (with some helper automation available).

## Open-source relational databases on Azure

Azure offers fully managed PaaS versions of the popular open-source engines.

| Service                       | Engine     | Known for                                                 |
| ----------------------------- | ---------- | --------------------------------------------------------- |
| Azure Database for MySQL      | MySQL      | Popular web app stack (LAMP), WordPress-style workloads   |
| Azure Database for PostgreSQL | PostgreSQL | Advanced open-source engine, extensions, hybrid workloads |

Both provide the PaaS benefits: automatic patching, backups, high availability options, and pay-as-you-go scaling, while keeping compatibility with the community engines so existing apps and tools work without rewrites.

Related option to recognize: Azure Cosmos DB for PostgreSQL provides distributed PostgreSQL for scale-out scenarios (it appears again in the Cosmos DB APIs).

## Common confusions

| Confusion                              | Correct idea                                                                                       |
| -------------------------------------- | -------------------------------------------------------------------------------------------------- |
| Primary key vs foreign key             | Primary key identifies rows in its own table; foreign key points at another table                  |
| DELETE vs DROP                         | DELETE removes rows (DML); DROP removes the object itself (DDL)                                    |
| View vs stored procedure               | A view is a saved query you select from; a procedure is saved code you execute                     |
| Index vs key                           | A key defines identity/relationships; an index speeds up lookups                                   |
| Azure SQL Database vs Managed Instance | Database is a single managed database; Managed Instance is a near-full SQL Server instance in PaaS |
| Managed Instance vs SQL Server on VM   | Managed Instance is still PaaS (no OS access); the VM option is IaaS with full control             |

## Exam traps

| Trap                                                 | Why people miss it                                                                |
| ---------------------------------------------------- | --------------------------------------------------------------------------------- |
| "PaaS means no responsibilities"                     | You still manage schemas, data, users, and query performance                      |
| "Managed Instance gives OS access"                   | It does not; only SQL Server on a VM gives OS-level control                       |
| "Normalization speeds up all queries"                | It speeds up and protects writes; heavy reads may need indexes or denormalization |
| "GRANT is part of DML"                               | GRANT, DENY, REVOKE are DCL (access control)                                      |
| "A view stores its own copy of the data"             | A standard view stores only the query definition                                  |
| "Open-source engines require managing a VM in Azure" | Azure Database for MySQL and PostgreSQL are fully managed PaaS services           |

## Mini scenarios

| Scenario                                                                            | Best answer                          |
| ----------------------------------------------------------------------------------- | ------------------------------------ |
| A startup wants a relational database for a new app with minimal management.        | Azure SQL Database                   |
| A company migrates on-premises SQL Server and needs SQL Server Agent jobs in PaaS.  | Azure SQL Managed Instance           |
| An ISV needs a specific SQL Server version with custom OS-level software installed. | SQL Server on Azure Virtual Machines |
| A web agency needs managed MySQL for customer sites.                                | Azure Database for MySQL             |
| A designer must ensure each order row is uniquely identifiable.                     | Add a primary key                    |
| A report should expose only three columns of a sensitive table to analysts.         | Create a view                        |
| Searches on the LastName column are slow.                                           | Create an index on LastName          |

## Check yourself

1. What does a foreign key do?
2. Which SQL category do CREATE, ALTER, and DROP belong to?
3. What is the difference between DELETE and DROP?
4. Why do OLTP systems use normalized designs?
5. Which Azure SQL option offers near 100% compatibility with on-premises SQL Server without managing an OS?
6. When would you pick SQL Server on Azure Virtual Machines over the PaaS options?
7. Which two open-source engines have their own Azure Database services?
8. What is the difference between a view and a stored procedure?

## Answer guide

1. It references the primary key of another table, creating and enforcing a relationship between rows.
2. DDL (Data Definition Language).
3. DELETE removes rows from a table; DROP removes the entire object (such as the table) from the database.
4. Normalization stores each fact once, so small frequent writes stay fast and cannot create conflicting copies.
5. Azure SQL Managed Instance.
6. When you need full control of the OS and SQL Server instance, specific versions, or OS-level software; you accept managing patching and backups.
7. MySQL and PostgreSQL (Azure Database for MySQL, Azure Database for PostgreSQL).
8. A view is a saved query used like a virtual table; a stored procedure is saved code that executes actions and can take parameters.
