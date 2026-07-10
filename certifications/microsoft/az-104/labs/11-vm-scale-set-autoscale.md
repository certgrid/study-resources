# Lab 11 - VM Scale Set with Autoscale

Scale sets are the "automatically add identical VMs" answer. This lab creates a tiny scale set, writes a real autoscale rule pair, and deletes everything at the end.

## Time Needed

35-40 minutes.

## What You Will Learn

- What a scale set model is and how instances follow it
- Uniform vs Flexible orchestration
- How to configure scale-out AND scale-in rules with limits
- Why scale sets can span availability zones

## AZ-104 Concepts Covered

| Concept            | Where you see it in the lab          |
| ------------------ | ------------------------------------ |
| Scale set creation | You deploy with 2 small instances    |
| Orchestration mode | You pick Flexible and note Uniform   |
| Autoscale rules    | You build CPU-based out and in rules |
| Instance limits    | You set min/max/default              |
| Upgrade policy     | You see how model changes roll out   |

## Cost Warning

THIS IS THE MOST EXPENSIVE LAB: multiple VMs bill simultaneously. Mitigations:

- 2 instances maximum, smallest B-series size.
- Set the autoscale MAXIMUM to 3 so a runaway rule cannot create a fleet.
- DELETE THE ENTIRE SCALE SET at the end of this lab: it is not reused later.
- If anything goes wrong, delete the scale set first and debug afterwards.

## Steps

### 1. Create the scale set

1. Search **Virtual machine scale sets > Create**.
2. Resource group `rg-az104-labs`, name `vmss-lab`, your usual region.
3. Availability zones: select 2 zones if offered (this is how scale sets beat sets: elastic AND zone-spread).
4. Orchestration mode: **Flexible** (note Uniform exists for identical, large-scale workloads).
5. Image: Ubuntu Server LTS, size: smallest B-series, authentication: SSH key.
6. Scaling: initial instance count 2; leave "Manual" for now (autoscale comes next).
7. Networking: accept defaults; no load balancer needed for this lab (or accept one if the wizard insists; it gets deleted with the group anyway).
8. Review + create.

### 2. Inspect the model and instances

1. On `vmss-lab`, open **Instances**: two instances exist, created from one model.
2. Open **Availability + scale > Upgrade policy**: note the modes (Manual / Automatic / Rolling): how instances receive model changes.

### 3. Configure autoscale

1. Open **Availability + scale > Scaling** and switch to **Custom autoscale**.
2. Instance limits: minimum 1, maximum 3, default 2.
3. Add a scale-OUT rule: metric = Percentage CPU, condition: average > 70% over 10 minutes, action: increase count by 1, cooldown 5 minutes.
4. Add a scale-IN rule: average CPU < 25% over 10 minutes, decrease count by 1.
5. Save. Exam point: a scale set with only an out rule never shrinks: always pair the rules and set limits.
6. Since B-series VMs idle near 0% CPU, the scale-IN rule will kick in after ~10 minutes and trim you to 1 instance: free cost control and proof autoscale works. You do not need to force a scale-out.

### 4. Recognition checks

Read, do not run:

```bash
az vmss create --resource-group rg-az104-labs --name vmss-lab --image Ubuntu2204 --instance-count 2 --orchestration-mode Flexible
az vmss scale --resource-group rg-az104-labs --name vmss-lab --new-capacity 3
```

PowerShell equivalents: `New-AzVmss`, `Update-AzVmss`.

## Clean Up

DELETE THE SCALE SET NOW - it is not used again:

```bash
az vmss delete --name vmss-lab --resource-group rg-az104-labs
```

Then open `rg-az104-labs` and delete any leftovers the wizard created for it (extra VNet, load balancer, public IP, NSG named after vmss-lab). Check Cost analysis tomorrow to confirm nothing from this lab still bills.

## Success Criteria

You are done when you can explain:

- What the scale set model is and how the upgrade policy applies changes
- Uniform vs Flexible orchestration in one sentence
- The five parts of an autoscale rule (metric, threshold, duration, action, cooldown)
- Why min/max limits and paired in/out rules are mandatory in practice
- Why a scale set across zones beats an availability set
