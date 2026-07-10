# 02 - Implement and Manage Storage

This domain is worth 15-20% of the exam. It covers storage account creation and configuration, redundancy, secure access (firewalls, SAS, access keys, identity-based access), object replication, encryption, tools (Storage Explorer, AzCopy), Azure Files, and Blob Storage features like tiers, lifecycle management, versioning, snapshots, and soft delete.

## Mental model

A storage account is a security and billing boundary around four services: blobs (objects), files (SMB/NFS shares), queues, and tables. AZ-104 tests three decisions again and again: how the data survives failures (redundancy), who can reach it (network + auth), and how it gets cheaper over time (tiers + lifecycle).

| Scenario keyword                                    | Likely concept                           |
| --------------------------------------------------- | ---------------------------------------- |
| "Survive a region outage"                           | GRS / GZRS (geo redundancy)              |
| "Survive a datacenter (zone) failure"               | ZRS                                      |
| "Read from the secondary region"                    | RA-GRS / RA-GZRS                         |
| "Temporary limited access to a blob"                | SAS token                                |
| "Revoke SAS access quickly"                         | Stored access policy (or rotate the key) |
| "Only allow access from a VNet"                     | Storage firewall + virtual network rules |
| "Lift-and-shift file server / mapped drive"         | Azure Files (SMB share)                  |
| "Cache files on-premises with cloud tiering"        | Azure File Sync                          |
| "Rarely accessed data, instant access when needed"  | Cool or cold tier                        |
| "Compliance archive, hours to retrieve"             | Archive tier                             |
| "Move blobs to cooler tiers automatically"          | Lifecycle management policy              |
| "Recover an overwritten blob"                       | Blob versioning (or snapshots)           |
| "Recover a deleted blob or container"               | Soft delete                              |
| "Copy terabytes from the command line"              | AzCopy                                   |
| "Copy blobs to an account in another region/tenant" | Object replication                       |

## Storage accounts

### Account types and naming

| Setting       | Rule or options                                                           |
| ------------- | ------------------------------------------------------------------------- |
| Name          | 3-24 characters, lowercase letters and numbers only, globally unique      |
| Performance   | Standard (HDD-backed) or Premium (SSD-backed)                             |
| Standard kind | StorageV2 (general purpose v2) is the default and exam answer             |
| Premium kinds | Premium block blobs, premium file shares, premium page blobs              |
| Region        | Chosen at creation; data lives in that region (plus paired region if geo) |

Key facts:

- General purpose v2 (StorageV2) supports all services, tiers, and lifecycle management.
- Premium accounts do not support access tiers (hot/cool/cold/archive).
- The default access tier setting (hot or cool) applies to blobs without an explicit tier.

### Redundancy: the table you must know cold

| Option  | Copies | Where                                  | Survives                                         |
| ------- | ------ | -------------------------------------- | ------------------------------------------------ |
| LRS     | 3      | One datacenter in one region           | Disk/rack failure                                |
| ZRS     | 3      | Three availability zones in one region | Entire zone (datacenter) failure                 |
| GRS     | 6      | LRS in primary + LRS in paired region  | Region failure (after failover)                  |
| RA-GRS  | 6      | GRS + read access to secondary         | Region failure, with read access before failover |
| GZRS    | 6      | ZRS in primary + LRS in paired region  | Zone failure and region failure                  |
| RA-GZRS | 6      | GZRS + read access to secondary        | Zone + region failure, readable secondary        |

Key facts:

- The secondary region is always the paired region and cannot be chosen freely.
- Data in the secondary is not readable unless you pick an RA- option or fail over.
- Failover (customer-initiated or Microsoft-initiated) makes the secondary the new primary.
- Premium storage supports only LRS and ZRS.

### Encryption

- All storage is encrypted at rest with Storage Service Encryption (SSE); it cannot be disabled.
- Default: Microsoft-managed keys. Options: customer-managed keys (CMK) in Azure Key Vault, or infrastructure (double) encryption enabled at creation.
- Encryption scopes let different containers/blobs use different keys in one account.

### Object replication

- Asynchronously copies block blobs from a source account/container to a destination account/container.
- Source and destination can be in different regions, subscriptions, or tenants.
- Requires blob versioning enabled on both source and destination; change feed on the source.
- Use cases: reduce read latency in another region, distribute data, or an extra copy beyond redundancy.

## Configure access to storage

### The three authorization paths

| Method                    | What it is                                                | Exam trigger                                        |
| ------------------------- | --------------------------------------------------------- | --------------------------------------------------- |
| Access keys               | Two full-control root keys per account                    | "Rotate keys", "key1/key2", connection strings      |
| Shared access signature   | Signed URL with permissions, expiry, optional IP/protocol | "Time-limited access without sharing keys"          |
| Microsoft Entra ID + RBAC | Data-plane roles like Storage Blob Data Reader            | "Use identities instead of keys", "least privilege" |

Key facts:

- Two keys exist so you can rotate one while apps use the other.
- Rotating a key invalidates every SAS signed with that key.
- Entra-based data access uses roles like Storage Blob Data Contributor; the control-plane Contributor role does not automatically grant data access (it can read keys though).

### SAS types

| SAS type            | Signed with          | Scope                                    | Notes                                |
| ------------------- | -------------------- | ---------------------------------------- | ------------------------------------ |
| Account SAS         | Account key          | Multiple services in the account         | Broadest                             |
| Service SAS         | Account key          | One service (e.g. one blob or container) | Can reference a stored access policy |
| User delegation SAS | Entra ID credentials | Blob service only                        | Most secure; no account key involved |

### Stored access policies

- Defined on a container (or share/queue/table); a service SAS can reference the policy.
- Change or delete the policy and every SAS tied to it is immediately modified or revoked.
- This is the exam answer for "revoke a SAS without rotating keys."
- Up to five stored access policies per container.

### Storage firewalls and virtual networks

| Setting                        | Effect                                                      |
| ------------------------------ | ----------------------------------------------------------- |
| Enabled from all networks      | Default; anyone with valid auth can connect                 |
| Enabled from selected networks | Only listed VNets/subnets (service endpoints) and IP ranges |
| Disabled (public access)       | Only private endpoints reach the account                    |
| Exceptions                     | Allow trusted Azure services, allow read of logs/metrics    |

Key facts:

- VNet rules use service endpoints (Microsoft.Storage) on the subnet.
- Private endpoints give the account a private IP inside your VNet and work with the public network disabled.
- Do not lock yourself out: portal access to data also flows through these rules.

### Identity-based access for Azure Files

| Option                                       | Use case                                           |
| -------------------------------------------- | -------------------------------------------------- |
| On-premises AD DS authentication             | Domain-joined machines accessing SMB shares        |
| Microsoft Entra Domain Services              | Cloud-managed domain for SMB auth                  |
| Microsoft Entra Kerberos (hybrid identities) | Entra-joined clients without line of sight to a DC |

Share-level permission comes from RBAC roles (Storage File Data SMB Share Reader/Contributor/Elevated Contributor); file/folder-level permission comes from NTFS ACLs.

## Azure Files and Azure File Sync

| Feature        | Azure Files                                     | Azure File Sync                                              |
| -------------- | ----------------------------------------------- | ------------------------------------------------------------ |
| What it is     | Managed SMB/NFS file shares in the cloud        | Syncs an on-premises Windows Server with an Azure file share |
| Access         | Mount from Windows, Linux, macOS (SMB port 445) | Users keep using the local server                            |
| Killer feature | Replace file servers, lift-and-shift apps       | Cloud tiering: keep hot files local, cold files in Azure     |
| Components     | Storage account + file share                    | Storage Sync Service, sync group, registered server, agent   |

Key facts:

- SMB uses port 445; many ISPs block it, which is the classic "cannot mount from home" trap.
- Snapshots are share-level, read-only, and support restoring individual files.
- Soft delete for file shares protects against deleted shares (not individual files).
- Standard file shares bill per used GiB; premium bill per provisioned GiB.

## Azure Blob Storage

### Blob types

| Blob type   | Use                                         |
| ----------- | ------------------------------------------- |
| Block blob  | Documents, images, backups, general objects |
| Append blob | Logging (append-only writes)                |
| Page blob   | VHD/disk files, random read/write           |

### Access tiers

| Tier    | Intended for                           | Minimum retention | Access                      |
| ------- | -------------------------------------- | ----------------- | --------------------------- |
| Hot     | Frequent access                        | None              | Instant                     |
| Cool    | Infrequent access, stored 30+ days     | 30 days           | Instant                     |
| Cold    | Rare access, stored 90+ days           | 90 days           | Instant                     |
| Archive | Compliance/long-term, stored 180+ days | 180 days          | Offline; rehydration needed |

Key facts:

- Storage cost falls and access cost rises as you move hot -> cool -> cold -> archive.
- Deleting or moving a blob before the minimum retention incurs an early deletion charge.
- Archive rehydration takes up to 15 hours standard (high priority is faster, under 1 hour for small blobs).
- Archive is set per blob, not as the account default; the account default is hot or cool.

### Lifecycle management

- Rules on the account move blobs between tiers or delete them based on days since modification, creation, or last access.
- Example rule: move to cool after 30 days, to archive after 90 days, delete after 365 days.
- Can also manage previous versions and snapshots.
- This is the exam answer for "reduce storage cost automatically."

### Protecting blob data

| Feature         | Protects against              | How it works                                 |
| --------------- | ----------------------------- | -------------------------------------------- |
| Soft delete     | Deleted blobs/containers      | Retains deleted data 1-365 days for undelete |
| Blob versioning | Overwrites and deletions      | Automatically keeps previous versions        |
| Snapshots       | Point-in-time copies (manual) | Read-only copy taken on demand               |
| Immutability    | Any modification or deletion  | Time-based retention or legal hold (WORM)    |

Versioning is automatic per write; snapshots are manual. Soft delete for containers is separate from soft delete for blobs.

## Tools: Storage Explorer and AzCopy

| Tool                   | What it is                         | Best for                                                |
| ---------------------- | ---------------------------------- | ------------------------------------------------------- |
| Azure Storage Explorer | Free GUI app (Windows/macOS/Linux) | Browsing, uploading, managing blobs/files/queues/tables |
| AzCopy                 | Command-line copy tool             | Bulk/scripted transfers, sync, server migrations        |

AzCopy commands to recognize: azcopy login, azcopy copy <src> <dst> --recursive, azcopy sync. Auth via Entra ID (azcopy login) or SAS appended to the URL.

## Limits and numbers to memorize

| Item                                      | Value                                   |
| ----------------------------------------- | --------------------------------------- |
| Storage account name                      | 3-24 chars, lowercase letters + numbers |
| Max default storage account capacity      | 5 PiB per account                       |
| Access keys per account                   | 2 (for rotation)                        |
| Stored access policies per container      | 5                                       |
| Cool / cold / archive minimum retention   | 30 / 90 / 180 days                      |
| Soft delete retention range               | 1-365 days                              |
| Blob tiers with instant access            | Hot, cool, cold (archive is offline)    |
| SMB port for Azure Files                  | 445                                     |
| Redundancy copies: LRS/ZRS vs geo options | 3 vs 6                                  |

## CLI and PowerShell recognition

| Task                     | Azure CLI                                      | PowerShell                                 |
| ------------------------ | ---------------------------------------------- | ------------------------------------------ |
| Create a storage account | az storage account create                      | New-AzStorageAccount                       |
| Change redundancy        | az storage account update --sku Standard_GRS   | Set-AzStorageAccount -SkuName Standard_GRS |
| List access keys         | az storage account keys list                   | Get-AzStorageAccountKey                    |
| Rotate an access key     | az storage account keys renew                  | New-AzStorageAccountKey                    |
| Create a container       | az storage container create                    | New-AzStorageContainer                     |
| Upload a blob            | az storage blob upload                         | Set-AzStorageBlobContent                   |
| Set a blob tier          | az storage blob set-tier                       | $blob.ICloudBlob.SetStandardBlobTier()     |
| Generate a SAS           | az storage container generate-sas              | New-AzStorageContainerSASToken             |
| Create a file share      | az storage share-rm create                     | New-AzRmStorageShare                       |
| Bulk copy data           | azcopy copy <source> <destination> --recursive | azcopy (same tool from PowerShell)         |

## Common confusions

| Confusion                            | Correct idea                                                                         |
| ------------------------------------ | ------------------------------------------------------------------------------------ |
| ZRS vs GRS                           | Zones inside one region vs a copy in the paired region                               |
| GRS vs RA-GRS                        | Same copies; RA- adds read access to the secondary before failover                   |
| Service endpoint vs private endpoint | Subnet identity over Microsoft backbone vs a private IP for the account in your VNet |
| SAS vs stored access policy          | The token vs the server-side policy the token can reference (and be revoked through) |
| Account SAS vs user delegation SAS   | Signed by account key vs signed by Entra credentials (blob only)                     |
| Cool vs archive                      | Both cheap; cool is instant access, archive requires rehydration                     |
| Soft delete vs versioning            | Undelete for deletions vs automatic history of overwrites                            |
| Snapshot vs version                  | Manual point-in-time copy vs automatic per-write copy                                |
| Azure Files vs Blob Storage          | Mountable file shares (SMB/NFS) vs object storage over HTTPS                         |
| Storage Explorer vs AzCopy           | GUI management vs command-line bulk transfer                                         |

## Exam traps

| Trap                                                                             | Why people miss it                                                      |
| -------------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| Choosing GRS when the requirement says "survive a zone failure with no failover" | ZRS (or GZRS) covers zones; plain GRS is LRS in the primary region      |
| Choosing archive for "instant access when needed"                                | Archive is offline; cool or cold is the answer                          |
| Forgetting minimum retention charges                                             | Deleting from cool before 30 days / archive before 180 days costs extra |
| "Revoke a SAS" answered with "wait for expiry"                                   | Stored access policy deletion or key rotation revokes immediately       |
| Expecting Contributor role to read blob data via Entra auth                      | Data access needs a data-plane role like Storage Blob Data Reader       |
| Cannot mount an Azure file share from a home network                             | Port 445 is blocked by the ISP                                          |
| Enabling object replication without versioning                                   | Object replication requires blob versioning on both accounts            |
| Choosing premium storage and expecting access tiers                              | Premium accounts do not have hot/cool/cold/archive tiers                |
| Choosing LRS for the lowest cost when zone failure is in scope                   | LRS is cheapest but sits in a single datacenter                         |
| Assuming you pick the secondary region for GRS                                   | The paired region is fixed by Azure                                     |

## Mini scenarios

| Scenario                                                                                               | Best answer                                                                         |
| ------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------- |
| Logs must survive a complete region outage and be readable in the second region at all times.          | RA-GRS (or RA-GZRS)                                                                 |
| Data must survive the loss of one datacenter but must never leave the country's single region.         | ZRS                                                                                 |
| A partner needs upload-only access to one container for two weeks.                                     | Service SAS with write permission and an expiry, referencing a stored access policy |
| Security demands that a leaked SAS URL be killable at any moment without breaking other SAS tokens.    | Service SAS tied to a stored access policy                                          |
| Invoices are written once, read for a month, kept 7 years for compliance, and almost never read again. | Lifecycle rule: cool after 30 days, archive later, delete after 7 years             |
| An app must access blobs using managed identities with least privilege.                                | Assign Storage Blob Data Reader/Contributor to the identity                         |
| A storage account must only accept traffic from one subnet and one office IP.                          | Storage firewall: selected networks + service endpoint + IP rule                    |
| A branch office file server is full; users need all files visible but only hot files stored locally.   | Azure File Sync with cloud tiering                                                  |
| A blob was overwritten by a bad deployment and must be restored to yesterday's content.                | Blob versioning (restore a previous version)                                        |
| 40 TB of on-premises file data must be copied to blob storage with a scriptable, restartable tool.     | AzCopy                                                                              |

## Check yourself

1. How many copies of data does GZRS keep, and where?
2. Which redundancy options can you use with a premium storage account?
3. Which SAS type is signed with Microsoft Entra credentials instead of an account key?
4. How do you revoke a service SAS immediately without rotating account keys?
5. What is the minimum retention period for the cold tier before early deletion charges apply?
6. A blob in the archive tier must be read today. What must happen first, and roughly how long can it take?
7. Which two features must be enabled before object replication can be configured?
8. Which port must be open to mount an Azure file share with SMB?
9. What is the difference between soft delete and blob versioning?
10. Which command uploads a blob: az storage blob upload or Set-AzStorageBlobContent, and which tool does each belong to?

## Answer guide

1. Six: three across availability zones in the primary region, three (LRS) in the paired region.
2. LRS and ZRS only.
3. User delegation SAS (blob service only).
4. Delete or modify the stored access policy the SAS references.
5. 90 days (cool is 30, archive is 180).
6. It must be rehydrated to an online tier; standard priority can take up to about 15 hours.
7. Blob versioning (both accounts) and change feed (source).
8. TCP 445.
9. Soft delete lets you undelete deleted data within a retention window; versioning automatically keeps previous versions on every overwrite.
10. Both upload a blob; az storage blob upload is Azure CLI, Set-AzStorageBlobContent is Az PowerShell.
