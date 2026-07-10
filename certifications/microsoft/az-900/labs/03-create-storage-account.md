# Lab 03 - Create a Storage Account

This beginner lab helps make AZ-900 storage concepts practical.

## Goal

Create an Azure Storage account and identify the core settings that appear in AZ-900 questions.

## Time Needed

15-25 minutes.

## What you will learn

- What a storage account is
- How region and redundancy are selected
- Where Blob Storage fits
- How access tiers affect cost
- Why tags are useful

## AZ-900 Concepts Covered

| Concept        | Where you see it in the lab                |
| -------------- | ------------------------------------------ |
| Resource group | You create one to hold the lab resources   |
| Region         | You choose where the storage account lives |
| Blob Storage   | You create a container and upload a file   |
| Redundancy     | You compare LRS, ZRS, GRS, and GZRS        |
| Tags           | You tag the storage account for reporting  |
| Cost control   | You delete the resource group at the end   |

## Prerequisites

- Azure account or Microsoft Learn sandbox
- Basic access to the Azure portal

## Steps

### 1. Create a resource group

1. Open the Azure portal.
2. Search for **Resource groups**.
3. Create a new resource group.
4. Choose a nearby region.
5. Name it something like `rg-az900-storage-lab`.

### 2. Create a storage account

1. Search for **Storage accounts**.
2. Select **Create**.
3. Choose your subscription and resource group.
4. Enter a globally unique storage account name.
5. Select a region.
6. Choose a performance option such as Standard.
7. Choose a redundancy option.

### 3. Review redundancy

Look at the redundancy options.

| Option | Meaning                              |
| ------ | ------------------------------------ |
| LRS    | Copies data within one datacenter    |
| ZRS    | Copies data across zones in a region |
| GRS    | Copies data to a paired region       |
| GZRS   | Zone redundancy plus geo-replication |

For AZ-900, know that geo-redundant options help protect from regional failure.

### 4. Create a blob container

1. Open the storage account.
2. Go to **Containers**.
3. Create a container.
4. Keep public access disabled unless you specifically need public anonymous access.

### 5. Upload a test file

Upload a small file and review its properties.

Notice:

- Blob URL
- Access tier
- Last modified time
- Size

### 6. Add tags

Add tags such as:

| Name        | Value    |
| ----------- | -------- |
| Environment | Lab      |
| Exam        | AZ-900   |
| Owner       | YourName |

Tags help with organization and cost reporting.

## Clean up

Delete the resource group when finished. Deleting the resource group removes the storage account and container.

## Exam takeaways

- Blob Storage is for unstructured object data.
- Azure Files is for managed file shares.
- Storage redundancy affects availability and durability.
- Tags help organize and report costs.
- Resource groups help manage lifecycle.

## Success Criteria

You are done when you can explain:

- Why this storage account belongs to one resource group
- Why the selected region matters
- What redundancy option you selected and what it protects against
- Why Blob Storage is different from Azure Files
- Why cleanup matters for cloud cost control

