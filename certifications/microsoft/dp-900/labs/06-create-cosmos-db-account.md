# Lab 06 - Create an Azure Cosmos DB Account

Cosmos DB is the exam's non-relational flagship. Creating an account and adding JSON items makes the API choice, containers, and partition keys concrete.

## Time Needed

20-25 minutes.

## What You Will Learn

- Why you must choose an API when creating the account
- What databases, containers, and items are
- What a partition key does
- How JSON items in one container can differ

## DP-900 Concepts Covered

| Concept              | Where you see it in the lab                  |
| -------------------- | -------------------------------------------- |
| Cosmos DB APIs       | You pick the API for NoSQL at creation       |
| Semi-structured data | You store JSON documents with varying fields |
| Partition key        | You choose one for the container             |
| Global distribution  | You see the replicate-data-globally options  |

## Cost Warning

Select the **Free tier discount** if your subscription allows it (one free-tier Cosmos DB account per subscription). Otherwise choose **Serverless** capacity mode so you pay only per operation. Delete the account in the cleanup lab.

## Steps

### 1. Create the account

1. Search for **Azure Cosmos DB** and select **Create**.
2. Select **Azure Cosmos DB for NoSQL**. Pause on this screen: the other tiles (MongoDB, Apache Cassandra, Apache Gremlin, Table, PostgreSQL) are the APIs from the study notes.
3. Resource group:

```text
rg-dp900-labs
```

4. Account name must be globally unique, for example `cosmos-dp900-<yourname>`.
5. Apply the **Free tier discount** if available; otherwise set Capacity mode to **Serverless**.
6. Select **Review + create**, then **Create**. Deployment takes a few minutes.

### 2. Create a database and container

1. Open the account and select **Data Explorer**.
2. Select **New Container** and enter:

| Setting       | Value     |
| ------------- | --------- |
| Database id   | appdata   |
| Container id  | products  |
| Partition key | /category |

### 3. Add JSON items

1. Open **appdata > products > Items** and select **New Item**.
2. Paste and save:

```json
{
  "id": "p1",
  "category": "bikes",
  "name": "Road Bike 200",
  "price": 799
}
```

3. Add a second item with a different shape:

```json
{
  "id": "p2",
  "category": "helmets",
  "name": "Aero Helmet",
  "price": 129,
  "sizes": ["S", "M", "L"]
}
```

Notice the second item has an extra array field. No schema change was needed.

### 4. Query the items

1. Select **New SQL Query** and run:

```sql
SELECT c.name, c.price FROM c WHERE c.price < 500
```

SQL-like syntax over JSON documents: this is why "Cosmos DB has a SQL API" does not make it relational.

### 5. Look at global distribution

1. Open **Replicate data globally** in the left menu.
2. Do not add regions (cost), but see how a single click would replicate your data to another region.

## Clean Up

Cosmos DB accounts should not linger. Delete in [09 - Clean Up Resources](09-clean-up-resources.md), or delete the account now if you are stopping here.

## Success Criteria

You are done when you can explain:

- Why the API choice happens at account creation
- The hierarchy: account, database, container, item
- What the partition key does for scale
- Why two items with different fields can share one container
