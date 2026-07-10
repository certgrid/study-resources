# Lab 20 - Back Up a VM with Azure Backup

Backup questions are about vaults, policies, and what deletion requires. This lab protects the lab VM, runs a backup, explores restore options, and then does the fiddly part everyone fails: undoing it all.

## Time Needed

40-45 minutes (the initial backup job runs in the background; you do not need to watch it).

Uses `vm-lab-01` from lab 09.

## What You Will Learn

- Recovery Services vault creation and its redundancy rule
- How a backup policy schedules and retains restore points
- The restore options (new VM, disks, file-level)
- Why deleting a vault takes deliberate steps (soft delete)

## AZ-104 Concepts Covered

| Concept                 | Where you see it in the lab              |
| ----------------------- | ---------------------------------------- |
| Recovery Services vault | You create vault-az104-lab               |
| Vault redundancy        | You set LRS BEFORE protecting anything   |
| Backup policy           | You author schedule + retention          |
| On-demand backup        | You run Backup now                       |
| Restore options         | You review without restoring             |
| Soft delete / cleanup   | You stop protection and delete the vault |

## Cost Warning

Azure Backup bills per protected instance per month plus storage: a single small VM for a day or two costs cents, BUT a forgotten protected VM with GRS vault storage adds up. This lab sets vault redundancy to LRS (cheap) and the Clean Up section fully unwinds protection: do not skip it. The VM can stay DEALLOCATED the whole lab: backup works on stopped VMs.

## Steps

### 1. Create the vault

1. Search **Recovery Services vaults > Create**.
2. Resource group `rg-az104-labs`, name `vault-az104-lab`, region: THE SAME REGION AS THE VM: a vault only protects VMs in its own region.
3. After creation, IMMEDIATELY open **Properties > Backup Configuration** and set storage replication type to **LRS**. This is changeable only while nothing is protected: the exam point and the cost saver in one.

### 2. Create a backup policy

1. In the vault, open **Backup policies > Add**, policy type **Azure Virtual Machine**.
2. Note the policy sub-types: **Standard** (once daily) vs **Enhanced** (multiple per day, zone-resilient): pick Standard.
3. Name `policy-daily-lab`, schedule daily at a near time, retention: 7 days daily; expand weekly/monthly/yearly retention to see grandfather-father-son retention: set weekly to 2 weeks, leave the rest off.
4. Create.

### 3. Protect the VM

1. Vault > **Backup** (or +Backup): workload Azure / Virtual machine.
2. Policy `policy-daily-lab`; select `vm-lab-01`. Enable backup.
3. Open **Backup items > Azure Virtual Machine**: `vm-lab-01` appears with "Initial backup pending".

### 4. Run an on-demand backup

1. Select the backup item > **Backup now**, accept the retention date.
2. Watch progress under **Backup jobs**: a first backup of a small VM takes a while: continue reading, do not wait idle.

### 5. Review restore options (no restore needed)

Open the backup item and read the two buttons and their meaning:

| Option        | What it does                                              |
| ------------- | --------------------------------------------------------- |
| Restore VM    | Create a new VM, or replace existing disks                |
| File Recovery | Mount the restore point via script; copy individual files |

Exam mapping: "recover one deleted file" = File Recovery, not a full restore. "Cross-region restore" exists only on GRS vaults with the feature enabled.

### 6. Where Site Recovery lives

In the same vault, open **Site Recovery** on the Overview: replication of VMs to a secondary region, test failover, recovery plans. Same vault, different job: Backup restores data, ASR fails over workloads. Read, do not enable (ASR bills per protected instance).

## Clean Up

Unwinding backup has a strict order: learn it here:

1. Backup items > `vm-lab-01` > **Stop backup**, choose **Delete backup data**, type the item name, confirm.
2. Soft delete now holds the data ~14 days by default. To fully release the vault today: vault **Properties > Security Settings**, disable soft delete, then delete the item again from Backup items ("Undelete"/re-delete flow) if it shows soft-deleted.
3. When no protected items remain, delete `vault-az104-lab`.
4. Decide about `vm-lab-01`: the remaining lab is final cleanup, so you can leave it deallocated or delete it now.

## Success Criteria

You are done when you can explain:

- The vault-region rule and when redundancy can still be changed
- Standard vs Enhanced policy in one sentence
- All restore options and which one recovers a single file
- Why vault deletion fails at first attempt for most people (protected items + soft delete)
- Backup vs Site Recovery, living in the same vault
