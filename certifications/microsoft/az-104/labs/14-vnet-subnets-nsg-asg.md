# Lab 14 - Create a VNet with Subnets, NSGs, and ASGs

Networking questions demand precision: CIDR math, rule priorities, and evaluation order. This lab builds the VNet used by the remaining network labs and proves the NSG rules you write.

## Time Needed

35-40 minutes.

## What You Will Learn

- Address space and subnet planning (and the 5 reserved IPs)
- NSG rules: priority, direction, default rules
- How subnet-level and NIC-level NSGs combine
- What an application security group changes

## AZ-104 Concepts Covered

| Concept         | Where you see it in the lab                  |
| --------------- | -------------------------------------------- |
| VNet + subnets  | You create 10.10.0.0/16 with two /24 subnets |
| Reserved IPs    | You count usable addresses                   |
| NSG rules       | You write allow/deny rules with priorities   |
| ASG             | You create asg-web and use it in a rule      |
| Effective rules | You read the merged result on a NIC          |

## Cost Warning

VNets, subnets, NSGs, and ASGs are FREE. The optional test VM in step 5 bills while running: deallocate or delete it the same hour.

## Steps

### 1. Create the VNet

1. Search **Virtual networks > Create**.
2. Resource group `rg-az104-labs`, name `vnet-lab`, your region.
3. Address space: `10.10.0.0/16`.
4. Subnets:

| Name     | Range        |
| -------- | ------------ |
| snet-web | 10.10.1.0/24 |
| snet-db  | 10.10.2.0/24 |

5. Create. Quiz yourself: usable IPs per /24 in Azure = 251 (Azure reserves .0, .1, .2, .3 and .255).

### 2. Create an NSG with rules

1. Search **Network security groups > Create**: name `nsg-web`, same group/region.
2. Open it; read the DEFAULT rules first: AllowVnetInBound (65000), AllowAzureLoadBalancerInBound (65001), DenyAllInBound (65500), and the outbound trio. They cannot be deleted, only overridden by lower priorities.
3. Add inbound rules:

| Priority | Name            | Source  | Destination | Port | Action |
| -------- | --------------- | ------- | ----------- | ---- | ------ |
| 100      | allow-https     | Any     | Any         | 443  | Allow  |
| 200      | allow-ssh-admin | Your IP | Any         | 22   | Allow  |
| 300      | deny-all-ssh    | Any     | Any         | 22   | Deny   |

4. Reasoning check: SSH from your IP hits 200 (allow) before 300 (deny): lower number wins, first match stops evaluation.

### 3. Associate the NSG

1. In `nsg-web`, open **Subnets > Associate** and attach it to `vnet-lab / snet-web`.
2. Exam point: an NSG can associate to many subnets and NICs, but each subnet/NIC has at most one NSG.

### 4. Create an ASG and reference it

1. Search **Application security groups > Create**: name `asg-web`, same group/region.
2. In `nsg-web`, add an inbound rule: priority 150, source **Application security group** = `asg-web`, destination Any, port 8080, Allow.
3. The point: the rule follows VM membership of `asg-web`, not IP addresses. NICs join the ASG in their NIC settings.

### 5. (Optional but recommended) Prove it with the lab VM

1. Start `vm-lab-01` (from lab 09) briefly, open its NIC (**Networking** tab), and attach the NIC to `asg-web` (Application security groups section). Its subnet is different, which is fine for viewing config; ASG+NSG rules require same-VNet NICs to take real effect - note that as the constraint.
2. On the NIC's Networking tab, open **Effective security rules**: the merged subnet + NIC NSG result, exactly what the exam means by "evaluate effective security rules".
3. DEALLOCATE the VM again now.

## Clean Up

Keep `vnet-lab`, `nsg-web`, and `asg-web`: labs 15-17 use them. Ensure `vm-lab-01` is deallocated. Nothing else here bills.

## Success Criteria

You are done when you can explain:

- Why a /24 subnet yields 251 usable IPs in Azure
- The default NSG rules and their priority band
- Evaluation order for inbound traffic (subnet NSG then NIC NSG, both must allow)
- What an ASG replaces in a rule and its same-VNet constraint
- Where to see effective security rules
