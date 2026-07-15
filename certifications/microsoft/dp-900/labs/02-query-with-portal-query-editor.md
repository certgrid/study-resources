# Lab 02 - Query with the Portal Query Editor

The built-in query editor lets you run T-SQL against your Azure SQL Database from the browser. This makes the DML and DDL vocabulary from the study notes real.

## Time Needed

20-25 minutes.

## What You Will Learn

- How to connect to a database with SQL authentication
- What SELECT, INSERT, UPDATE, and DELETE actually do
- How a view differs from a table
- Why firewall rules matter for PaaS databases

## DP-900 Concepts Covered

| Concept          | Where you see it in the lab                  |
| ---------------- | -------------------------------------------- |
| DML statements   | You run SELECT, INSERT, UPDATE, DELETE       |
| DDL statements   | You create and drop a table                  |
| Database objects | You query a table and create a view          |
| Firewall rules   | You allow your client IP to reach the server |

## Steps

### 1. Open the query editor

1. Open the **sqldb-dp900-lab** database from Lab 01.
2. Select **Query editor (preview)** in the left menu.
3. Sign in with the SQL admin login and password from Lab 01.
4. If you see a firewall error, select the link to **allowlist your IP** (or add your client IP under the server's Networking settings) and try again.

### 2. Run SELECT queries

Run these one at a time and look at the results:

```sql
SELECT TOP 10 * FROM SalesLT.Product;

SELECT Name, ListPrice
FROM SalesLT.Product
WHERE ListPrice > 1000
ORDER BY ListPrice DESC;
```

### 3. Create a table (DDL) and add rows (DML)

```sql
CREATE TABLE dbo.StudyLog (
    Id INT IDENTITY PRIMARY KEY,
    Topic NVARCHAR(50) NOT NULL,
    Minutes INT NOT NULL
);

INSERT INTO dbo.StudyLog (Topic, Minutes)
VALUES ('Core data concepts', 45), ('Relational data', 30);

SELECT * FROM dbo.StudyLog;
```

### 4. Update and delete rows (DML)

```sql
UPDATE dbo.StudyLog SET Minutes = 60 WHERE Topic = 'Relational data';

DELETE FROM dbo.StudyLog WHERE Topic = 'Core data concepts';

SELECT * FROM dbo.StudyLog;
```

### 5. Create and use a view

```sql
CREATE VIEW dbo.ExpensiveProducts AS
SELECT Name, ListPrice
FROM SalesLT.Product
WHERE ListPrice > 2000;
```

```sql
SELECT * FROM dbo.ExpensiveProducts;
```

Notice the view behaves like a table but stores only the query.

### 6. Drop your objects (DDL)

```sql
DROP VIEW dbo.ExpensiveProducts;
DROP TABLE dbo.StudyLog;
```

Notice the difference: DELETE removed rows; DROP removed the objects themselves.

## Clean Up

Dropping the view and table above is enough. The database itself is removed in [09 - Clean Up Resources](09-clean-up-resources.md).

## Success Criteria

You are done when you can explain:

- Which statements are DML and which are DDL in this lab
- The difference between DELETE and DROP that you just observed
- What the view contained and where its data actually lived
- Why the firewall blocked you at first
