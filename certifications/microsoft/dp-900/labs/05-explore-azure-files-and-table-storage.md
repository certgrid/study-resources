# Lab 05 - Explore Azure Files and Table Storage

One storage account, two very different services. This lab shows why Azure Files answers "shared drive" questions and Table storage answers "cheap key-value" questions.

## Time Needed

15-20 minutes.

## What You Will Learn

- How a file share differs from a blob container
- What SMB mounting means
- How Table storage entities use PartitionKey and RowKey
- Why entities in one table can have different properties

## DP-900 Concepts Covered

| Concept               | Where you see it in the lab              |
| --------------------- | ---------------------------------------- |
| Azure Files           | You create a file share with folders     |
| SMB access            | You view the connect script for mounting |
| Table storage         | You create a table and add entities      |
| Partition and row key | You set both keys on every entity        |

## Steps

### 1. Create a file share

1. Open the storage account from Lab 03.
2. Select **File shares**, then **+ File share**.
3. Name:

```text
lab-share
```

4. Keep the default (transaction optimized) tier and create it.

### 2. Use the file share like a drive

1. Open the share and select **Browse**.
2. Select **+ Add directory** and create a folder named `team-docs`.
3. Upload a small file into the folder.
4. Select **Connect** and look at the generated script for Windows. You are looking at an SMB mount: this share can appear as a drive letter on a machine. That is the difference from blobs.

### 3. Create a table

1. Back in the storage account, select **Tables**.
2. Select **+ Table** and name it:

```text
devices
```

### 4. Add entities with the browser

1. Open **Storage browser** in the left menu, then **Tables**, then **devices**.
2. Select **Add entity** and enter:

| Property     | Value      |
| ------------ | ---------- |
| PartitionKey | sensors    |
| RowKey       | device-001 |
| Temperature  | 21 (Int32) |

3. Add a second entity with the same PartitionKey, RowKey `device-002`, and add a different extra property, for example `Humidity` = 55.
4. Notice both entities live in the same table with different properties: Table storage is schemaless.

## Clean Up

Keep the account until [09 - Clean Up Resources](09-clean-up-resources.md).

## Success Criteria

You are done when you can explain:

- When an app needs Azure Files instead of Blob storage
- What the Connect script would do on a Windows machine
- What PartitionKey and RowKey each do
- Why two entities in one table can have different properties
