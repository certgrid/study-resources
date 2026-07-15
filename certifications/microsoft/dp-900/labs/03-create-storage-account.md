# Lab 03 - Create a Storage Account

A storage account is the container for blobs, files, tables, and queues. Creating one shows the redundancy and performance choices the exam mentions.

## Time Needed

10-15 minutes.

## What You Will Learn

- What a storage account contains
- What LRS, ZRS, and GRS redundancy mean
- Where the Blob, Files, Table, and Queue services live
- What the hierarchical namespace option is for

## DP-900 Concepts Covered

| Concept                | Where you see it in the lab                       |
| ---------------------- | ------------------------------------------------- |
| Storage account        | You create the container for all storage services |
| Redundancy             | You choose LRS for the lab                        |
| Azure Storage services | You see Blob, Files, Table, Queue in one account  |
| Data Lake Storage      | You see the hierarchical namespace option         |

## Cost Warning

An empty storage account costs almost nothing, but uploaded data and transactions bill per use. Use LRS (the cheapest redundancy) for labs.

## Steps

### 1. Start the create flow

1. Search for **Storage accounts** and select **Create**.
2. Resource group:

```text
rg-dp900-labs
```

3. Storage account name must be globally unique, lowercase, no hyphens, for example:

```text
stdp900<yourname>
```

4. Region: your lab region.

### 2. Choose performance and redundancy

1. Performance: **Standard**.
2. Redundancy: **Locally-redundant storage (LRS)**.
3. Open the dropdown once to read the other options: ZRS, GRS, GZRS. Note which failure each protects against.

### 3. Look at the Advanced tab

1. Find **Enable hierarchical namespace** under Data Lake Storage Gen2.
2. Leave it unchecked for this lab, but remember: this single checkbox is what turns Blob storage into Data Lake Storage Gen2.

### 4. Create and explore

1. Select **Review + create**, then **Create**.
2. Open the account and find the four data services in the left menu or on the overview page:
   - **Containers** (Blob service)
   - **File shares** (Azure Files)
   - **Tables** (Table storage)
   - **Queues** (Queue storage)

## Clean Up

Keep the account; Labs 04 and 05 use it. Cleanup happens in [09 - Clean Up Resources](09-clean-up-resources.md).

## Success Criteria

You are done when you can explain:

- What one storage account can contain
- The difference between LRS, ZRS, and GRS
- Which option turns a storage account into Data Lake Storage Gen2
- Why Standard performance and LRS are right for a lab
