# Lab 07 - Create a Basic Virtual Network

Virtual networks are the foundation of Azure networking. This lab keeps networking simple and AZ-900 focused.

## Time Needed

15-20 minutes.

## What You Will Learn

- What a virtual network is
- What a subnet is
- How address spaces are used
- Why network security groups matter

## AZ-900 Concepts Covered

| Concept         | Where you see it in the lab           |
| --------------- | ------------------------------------- |
| Virtual Network | You create a private Azure network    |
| Subnet          | You divide the address space          |
| Region          | You choose where the network exists   |
| NSG             | You identify where traffic rules live |

## Steps

### 1. Open Virtual networks

1. Go to the Azure portal.
2. Search for **Virtual networks**.
3. Select **Create**.

### 2. Enter basics

Use:

```text
Name: vnet-az900-lab
Resource group: rg-az900-labs
Region: your lab region
```

### 3. Configure address space

Use a private range such as:

```text
10.10.0.0/16
```

### 4. Create a subnet

Create a subnet:

```text
Name: subnet-workloads
Range: 10.10.1.0/24
```

### 5. Review and create

Create the virtual network.

### 6. Review the VNet

Open the VNet and inspect:

- Address space
- Subnets
- Connected devices
- DNS servers

## Clean Up

If you are done with networking labs, delete the virtual network or delete the entire lab resource group.

## Success Criteria

You are done when you can explain:

- What a virtual network is
- What a subnet is
- Why private address ranges are used
- How NSGs relate to network traffic control

