# Lab 15 - VNet Peering and Network Watcher

Peering plus Network Watcher in one lab: connect two VNets, then use the diagnostic tools the exam names on the connection you just built.

## Time Needed

30-35 minutes.

## What You Will Learn

- How peering is created from both sides and what its options mean
- Why peering is not transitive
- Which Network Watcher tool answers which question
- How to read effective routes

## AZ-104 Concepts Covered

| Concept          | Where you see it in the lab           |
| ---------------- | ------------------------------------- |
| VNet peering     | You peer vnet-lab with a second VNet  |
| Non-overlap rule | You pick a non-overlapping range      |
| Gateway transit  | You read the options without enabling |
| Network Watcher  | You use IP flow verify and next hop   |
| Effective routes | You see the peering route appear      |

## Cost Warning

Peering itself has tiny per-GB charges only when traffic flows; this lab's config work is effectively free. Network Watcher tools used here are free or near-free. If you start `vm-lab-01` for the tool steps, deallocate it before leaving.

## Steps

### 1. Create a second VNet

1. Create `vnet-lab2`, resource group `rg-az104-labs`, address space `10.20.0.0/16`, one subnet `snet-app` = `10.20.1.0/24`.
2. Note WHY 10.20: peering refuses overlapping address spaces, and `vnet-lab` owns 10.10.0.0/16.

### 2. Peer the VNets

1. Open `vnet-lab > Peerings > Add`.
2. This one screen creates BOTH peering objects: name the local link `peer-lab1-to-lab2` and the remote link `peer-lab2-to-lab1`, remote VNet: `vnet-lab2`.
3. Read the checkboxes before creating:

| Option                                     | Meaning                                        |
| ------------------------------------------ | ---------------------------------------------- |
| Allow access to remote virtual network     | Basic connectivity (on)                        |
| Allow forwarded traffic                    | Accept traffic an NVA forwarded from elsewhere |
| Allow gateway transit / use remote gateway | Hub-spoke: spokes borrow the hub's VPN gateway |

4. Create, then check both VNets' Peerings blades: status **Connected** on both sides.
5. Say the exam fact out loud: if vnet-lab2 later peers with a vnet-lab3, vnet-lab does NOT reach vnet-lab3: not transitive.

### 3. Network Watcher: IP flow verify

1. Search **Network Watcher** (it auto-enables per region).
2. Open **IP flow verify**; target VM: `vm-lab-01` (start it if needed), direction inbound, protocol TCP, local port 22, remote IP: your public IP, remote port 40000.
3. Run it: the verdict names the exact NSG rule that allows/denies: this is the tool for "which rule blocks my traffic?".
4. Re-run with remote port/IP variations to hit your `deny-all-ssh` rule from lab 14.

### 4. Network Watcher: next hop

1. Open **Next hop**: source `vm-lab-01`, destination `10.20.1.10` (an address in vnet-lab2).
2. Result: next hop type **VNetPeering**: proof the peering route exists.
3. Try destination `8.8.8.8`: next hop **Internet** (the system default route).

### 5. Effective routes and the tool map

1. Open the VM's NIC > **Help > Effective routes** (or Networking): see Default routes plus the peering prefix 10.20.0.0/16.
2. Fix the tool map in memory:

| Question                               | Tool                    |
| -------------------------------------- | ----------------------- |
| Would this packet be allowed?          | IP flow verify          |
| Where does traffic go next?            | Next hop                |
| Can A reach B right now, where broken? | Connection troubleshoot |
| Watch a path continuously              | Connection monitor      |
| Record raw traffic                     | Packet capture          |

## Clean Up

DEALLOCATE `vm-lab-01` now if you started it. Keep both VNets and the peering for labs 16-17. Peerings at idle cost nothing.

## Success Criteria

You are done when you can explain:

- Why address spaces must not overlap and how both peering objects get created
- What gateway transit + use remote gateway achieve in hub-spoke
- Non-transitivity and its two fixes (direct peering, hub NVA + UDRs)
- Which Network Watcher tool matches each troubleshooting question
