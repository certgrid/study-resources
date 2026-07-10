# Lab 04 - Create a Basic Azure Virtual Machine

This beginner lab helps connect AZ-900 compute, networking, identity, and cost concepts.

## Goal

Create a small Azure Virtual Machine and identify the main settings that map to AZ-900 topics.

## Time Needed

20-30 minutes.

## What you will learn

- Why a VM is IaaS
- How VM size affects cost
- How networking is attached to a VM
- Why NSGs matter
- How to avoid unnecessary charges

## AZ-900 Concepts Covered

| Concept         | Where you see it in the lab                    |
| --------------- | ---------------------------------------------- |
| IaaS            | You choose and manage a virtual machine        |
| Region          | You choose where the VM is deployed            |
| VM size/SKU     | You see how compute size affects cost          |
| Virtual network | The VM is connected to a private Azure network |
| NSG             | Inbound and outbound rules control traffic     |
| Resource group  | You clean up all related resources together    |

## Prerequisites

- Azure account or Microsoft Learn sandbox
- Basic access to the Azure portal

## Steps

### 1. Create a resource group

Create a resource group named something like:

```text
rg-az900-vm-lab
```

This keeps all lab resources together.

### 2. Create a virtual machine

1. Search for **Virtual machines**.
2. Select **Create**.
3. Choose the resource group.
4. Pick a region.
5. Select a small VM size.
6. Choose an operating system image.
7. Configure an admin username and authentication method.

For AZ-900, remember that VMs are IaaS because you manage the operating system, patches, installed software, and data.

### 3. Review networking

During VM creation, Azure can create:

- Virtual network
- Subnet
- Public IP address
- Network interface
- Network security group

The NSG controls allowed inbound and outbound traffic.

### 4. Review cost settings

Look at:

- VM size
- Region
- Disk type
- Public IP
- Estimated monthly cost

VMs can keep costing money while running. Stop or delete them when not needed.

### 5. Connect briefly

If your lab environment allows it, connect to the VM using SSH or RDP. If not, just review the connection options.

### 6. Stop or delete the VM

For a short lab, deleting the resource group is the cleanest option.

## Clean up

Delete the resource group:

```text
rg-az900-vm-lab
```

This removes the VM, disk, public IP, NIC, and related resources.

## Exam takeaways

- Azure VMs are IaaS.
- VM size affects performance and cost.
- NSGs control network traffic.
- Resource groups help clean up related resources.
- Stopping/deleting unused resources helps control cost.

## Success Criteria

You are done when you can explain:

- Why Azure Virtual Machines are IaaS
- Which resources Azure created alongside the VM
- What an NSG does
- Why VM size affects cost
- Why deleting the resource group is the safest cleanup step for a lab

