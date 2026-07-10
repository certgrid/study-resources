# Lab 09 - Create a VM in an Availability Set

Availability options must be chosen at creation time, which makes this lab the place to see fault domains and update domains for real.

## Time Needed

35-40 minutes.

## What You Will Learn

- What an availability set's fault and update domains look like
- Which VM creation choices are permanent (set membership, region)
- What a VM deployment creates alongside the VM
- The difference between stopping and deallocating

## AZ-104 Concepts Covered

| Concept             | Where you see it in the lab        |
| ------------------- | ---------------------------------- |
| Availability set    | You create one with FD/UD counts   |
| VM creation         | You deploy a small VM into the set |
| Companion resources | You list NIC, disk, public IP, NSG |
| Stop vs deallocate  | You compare the two states         |
| SLA logic           | You reason about 99.95% vs 99.99%  |

## Cost Warning

THIS LAB COSTS MONEY WHILE THE VM RUNS. A B-series burstable VM costs roughly a cent or two per hour, plus disk storage. Rules:

- Use the smallest B-series size offered (e.g. B1s or B2ats_v2).
- DEALLOCATE the VM at the end of this lab (the next labs do not need it running).
- Never leave a VM running overnight "just in case."

## Steps

### 1. Create the availability set

1. Search **Availability sets > Create**.
2. Resource group `rg-az104-labs`, name `avset-lab`, same region as everything else.
3. Fault domains: 2, update domains: 5. Note the maximums while here: 3 FDs, 20 UDs.
4. Create it. Key rule: VMs join a set ONLY at creation.

### 2. Create the VM

1. Search **Virtual machines > Create > Azure virtual machine**.
2. Basics:
   - Resource group: `rg-az104-labs`; name: `vm-lab-01`.
   - Availability options: **Availability set** > `avset-lab`. Note the alternative in this dropdown: availability zone. You cannot pick both: that is the exam point.
   - Image: Ubuntu Server LTS (or Windows Server if you prefer; Linux is cheaper to license).
   - Size: smallest B-series available.
   - Authentication: SSH key (or password); username `azureuser`.
3. Disks: Standard SSD for the OS disk (note Premium SSD would be needed for the single-VM 99.9% SLA).
4. Networking: accept the new VNet/subnet defaults; public inbound ports: allow SSH only from your IP if offered, and note the NSG being created.
5. Review + create. While it deploys, answer: what SLA does ONE VM in a set have? (None from the set; the set needs 2+ VMs for 99.95%.)

### 3. Inventory what got created

Open **rg-az104-labs** and identify the companions: the VM, an OS disk, a NIC, a public IP, an NSG, and a VNet. Exam point: deleting the VM alone can orphan these unless delete-with-VM options were ticked.

### 4. Stop vs deallocate

1. Connect if you like (SSH from Cloud Shell: `ssh azureuser@<public-ip>`), then exit.
2. On the VM Overview, select **Stop**. Read the message: the portal Stop DEALLOCATES the VM (status: Stopped (deallocated)): compute billing stops, disks keep billing, and a dynamic public IP may change on restart.
3. Recognition: shutting down from INSIDE the OS gives status "Stopped" only: still billed. `az vm deallocate` / `Stop-AzVM` are the CLI/PowerShell equivalents of the portal Stop.

### 5. Check the set

Open `avset-lab`: the VM appears with its fault domain and update domain numbers. With a second VM, Azure would spread them across domains: that spread IS the 99.95% SLA mechanism.

## Clean Up

Leave `vm-lab-01` DEALLOCATED (labs 10 and 20 reuse it). Confirm the Overview says **Stopped (deallocated)**, not just Stopped. Deallocated VMs still bill small disk costs; that is acceptable for a few days, but if you will pause the series for long, delete the VM and its companions now and recreate later.

## Success Criteria

You are done when you can explain:

- Why availability set membership cannot be added later
- Fault domain vs update domain in one sentence each
- The SLA ladder: 99.9% single premium VM, 99.95% set, 99.99% zones
- Stopped vs Stopped (deallocated) and which one stops compute billing
