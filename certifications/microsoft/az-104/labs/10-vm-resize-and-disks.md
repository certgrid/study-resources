# Lab 10 - Resize a VM and Manage Disks

Sizes and disks are everyday admin work and reliable exam points. This lab resizes the lab VM, adds and detaches a data disk, and takes a snapshot.

## Time Needed

30-35 minutes.

Uses `vm-lab-01` from lab 09 (deallocated).

## What You Will Learn

- How resizing works and when a restart or deallocation is needed
- How to attach, initialize, and detach a data disk
- Disk types and what each is for
- What a disk snapshot gives you

## AZ-104 Concepts Covered

| Concept        | Where you see it in the lab                |
| -------------- | ------------------------------------------ |
| VM sizes       | You resize between B-series sizes          |
| Disk types     | You choose Standard SSD vs others          |
| Data disks     | You attach and detach one                  |
| Snapshots      | You snapshot the OS disk                   |
| Billing states | You keep the VM deallocated where possible |

## Cost Warning

Do the disk steps while the VM is DEALLOCATED where possible; only start it for the in-OS check, and deallocate again immediately. A 10 GiB Standard SSD data disk costs cents per month; the snapshot similar. Delete both in Clean Up.

## Steps

### 1. Resize the VM

1. Open `vm-lab-01` (deallocated), select **Availability + scale > Size**.
2. Note the list is filtered to sizes available in your region/cluster. Pick another small B-series size and apply.
3. Exam point: resizing a RUNNING VM restarts it; if the target size is not on the current hardware cluster, the VM must be deallocated first. A deallocated VM can resize to anything the region offers.
4. Resize back to the smallest size (stay cheap).

### 2. Attach a data disk

1. Go to **Settings > Disks > Create and attach a new disk**.
2. Name `disk-lab-data1`, Standard SSD, size 10 GiB (resize the default down; disks can grow later but never shrink).
3. Note Host caching options (None/Read-only/Read/write) and the max data disk count: it depends on the VM size.
4. Save.

### 3. See it inside the OS (brief start)

1. Start the VM, SSH in from Cloud Shell, and run:

```bash
lsblk
```

2. The new disk appears (e.g. sdc) unformatted: attaching does not format. In production you would partition/format and mount it; that OS-side work is not tested deeply, so skip it.
3. Exit and **deallocate the VM now** (Stop in the portal). Verify "Stopped (deallocated)".

### 4. Snapshot the OS disk

1. Open **Disks**, select the OS disk of `vm-lab-01`.
2. Select **Create snapshot**: name `snap-lab-os`, snapshot type Full, Standard HDD storage.
3. Uses to remember: seed a new managed disk, recover from a bad change, or move a VM across zones/regions by recreating from snapshots.

### 5. Detach the data disk

1. On the VM's **Disks** blade, detach `disk-lab-data1` and save.
2. The disk still exists (and bills) as an unattached managed disk: a classic source of silent cost. Find it in the **Disks** service list to prove it survived.

## Clean Up

Delete `disk-lab-data1` and `snap-lab-os` now:

```bash
az disk delete --name disk-lab-data1 --resource-group rg-az104-labs --yes
az snapshot delete --name snap-lab-os --resource-group rg-az104-labs
```

Confirm `vm-lab-01` is deallocated. Labs 20 (backup) will reuse it.

## Success Criteria

You are done when you can explain:

- When a resize needs deallocation first
- Why disks can be expanded but not shrunk
- The disk type ladder (Standard HDD / Standard SSD / Premium SSD / Premium v2 / Ultra) and one use for each
- Why unattached managed disks are a cost trap
- Two uses for a disk snapshot
