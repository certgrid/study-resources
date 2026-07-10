# Lab 07 - Azure Files Share and File Sync Concept

Azure Files is the lift-and-shift answer for file servers. This lab creates a share, takes a snapshot, restores a file, and walks the Azure File Sync architecture (without needing an on-premises server).

## Time Needed

25-30 minutes.

Uses the storage account from lab 05.

## What You Will Learn

- How to create and mount an SMB file share
- Why port 445 is the classic connection blocker
- How share snapshots restore files
- The Azure File Sync components and what cloud tiering does

## AZ-104 Concepts Covered

| Concept             | Where you see it in the lab                  |
| ------------------- | -------------------------------------------- |
| Azure Files         | You create a share and add files             |
| Mounting / port 445 | You read the connect scripts                 |
| Snapshots           | You take one and restore from it             |
| Soft delete         | You check share-level protection             |
| Azure File Sync     | You review Storage Sync Service architecture |

## Cost Warning

Cheap: a small standard file share bills per used GiB (cents). Delete test files in Clean Up. Do not create a premium file share; premium bills per PROVISIONED GiB even when empty.

## Steps

### 1. Create a file share

1. Open the lab storage account, select **File shares**.
2. Create share `teamfiles`, tier: Transaction optimized (note the tier options: also Hot, Cool for standard; Premium needs a premium account).
3. Open the share and upload any two small test files (create them in Cloud Shell or locally).

### 2. Review the connect experience

1. Select **Connect** on the share.
2. Read the Windows script: note `net use` mapping and the port test hint. Key exam fact: SMB needs TCP 445 outbound, and many ISPs block it: that is why "cannot mount from home" questions point at port 445.
3. Note the authentication choice in the script: storage account key vs identity-based. Identity-based (AD DS / Entra Domain Services / Entra Kerberos) is what enterprises use; share-level access then comes from RBAC roles and file-level from NTFS ACLs.

### 3. Snapshots and restore

1. On the share, open **Snapshots** and select **Add snapshot**.
2. Edit or delete one of your test files in the share.
3. Open the snapshot, browse to the file, and restore it (or download and re-upload).
4. Note: snapshots are read-only, share-level, and the basis of Azure Backup for Azure Files.

### 4. Check soft delete for shares

1. In the storage account, open **Data protection**.
2. Confirm soft delete for file shares (protects deleted SHARES, not individual files) and its retention setting.

### 5. Azure File Sync architecture (concept walk)

You need a Windows Server to actually use File Sync, so review the architecture instead:

1. Search the portal for **Azure File Sync** (Storage Sync Services) and open the create screen; read the fields, then cancel.
2. Memorize the component chain:

| Component            | Role                                               |
| -------------------- | -------------------------------------------------- |
| Storage Sync Service | Top-level Azure resource                           |
| Sync group           | Defines what syncs with what                       |
| Cloud endpoint       | The Azure file share                               |
| Server endpoint      | A path on a registered Windows Server              |
| Sync agent           | Installed on the server, registers it              |
| Cloud tiering        | Keeps hot files local, cold files cloud-only stubs |

## Clean Up

Delete the test files and snapshots from `teamfiles` (or delete the share) to keep billing near zero. Keep the storage account if you plan to redo storage labs; otherwise it goes in the final cleanup.

## Success Criteria

You are done when you can explain:

- Which port SMB needs and the classic symptom when it is blocked
- Share-level vs file-level permissions with identity-based access
- What a share snapshot protects vs what soft delete protects
- All six File Sync components in order, and what cloud tiering does
