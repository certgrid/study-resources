# Lab 05 - Storage Account Redundancy, Tiers, and Lifecycle

This lab creates the storage account you will reuse for the SAS and Files labs, then works the money topics: redundancy, blob access tiers, and lifecycle management.

## Time Needed

30-35 minutes.

## What You Will Learn

- The storage account creation options that matter (performance, redundancy)
- How to change redundancy after creation
- How blob access tiers work per blob and per account default
- How to build a lifecycle management rule

## AZ-104 Concepts Covered

| Concept              | Where you see it in the lab         |
| -------------------- | ----------------------------------- |
| Account creation     | You pick StorageV2, Standard, LRS   |
| Redundancy           | You view/change LRS to GRS and back |
| Containers and blobs | You upload test blobs               |
| Access tiers         | You set hot/cool/archive per blob   |
| Lifecycle management | You author a tiering rule           |
| Soft delete          | You verify data protection defaults |

## Cost Warning

Cheap but not zero: a standard LRS account with a few KB of blobs costs cents per month. Archive-tier blobs have a 180-day early deletion charge: use only a tiny test file, and expect a tiny early-delete fee (fractions of a cent for a KB-sized blob). Delete everything in the final cleanup lab or keep it for labs 06-07.

## Steps

### 1. Create the account

1. Search **Storage accounts > Create**.
2. Resource group: `rg-az104-labs`; name: `staz104lab<unique>` (3-24 chars, lowercase+digits).
3. Performance: **Standard**; Redundancy: **LRS** (note the other options in the dropdown: ZRS, GRS, RA-GRS...).
4. On the Advanced tab, note the default access tier setting (Hot) and that "Cool" is the other account-level choice; archive is per blob only.
5. Create.

### 2. Change redundancy

1. Open the account, go to **Data management > Redundancy**.
2. Switch LRS to **GRS**, save, and note the secondary region shown: it is the paired region and not selectable.
3. Switch back to **LRS** to keep cost minimal.

### 3. Upload blobs and set tiers

1. Open **Containers**, create container `docs` (private access).
2. Create three small text files locally (or in Cloud Shell) and upload them: `hot.txt`, `cool.txt`, `archive.txt`.
3. For each blob, open it and use **Change tier**:
   - `cool.txt` -> Cool
   - `archive.txt` -> Archive; read the warning: archive is offline and needs rehydration to read.
4. Try to download `archive.txt`: blocked until rehydrated. That delay (up to ~15 hours standard) is the exam point; you do not need to wait.

### 4. Build a lifecycle rule

1. Go to **Data management > Lifecycle management > Add a rule**.
2. Name: `rule-tier-down`, apply to block blobs, base blobs.
3. Conditions:
   - Move to cool: 30 days after last modification
   - Move to archive: 90 days after last modification
   - Delete: 365 days after last modification
4. Review the equivalent JSON on the Code view tab; recognize the shape (filters + actions).
5. Save the rule.

### 5. Check protection defaults

1. Open **Data protection** and note what is enabled: soft delete for blobs and containers (default 7 days, configurable 1-365) and where versioning would be enabled.
2. Delete `hot.txt`, then use **Show deleted blobs** in the container view and **Undelete** it.

## Clean Up

Keep the account for labs 06 and 07. Delete the `archive.txt` blob now if you want; the early-deletion fee on a KB file is negligible. If you are stopping the series here instead, delete the whole storage account.

## Success Criteria

You are done when you can explain:

- Which redundancy options exist and which one adds a readable secondary
- Why you cannot choose the secondary region for GRS
- The minimum retention days for cool, cold, and archive
- What a lifecycle rule can do besides changing tiers (delete blobs, handle versions/snapshots)
- How soft delete saved `hot.txt`
