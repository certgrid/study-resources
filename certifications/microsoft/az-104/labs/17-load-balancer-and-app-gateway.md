# Lab 17 - Load Balancer and Application Gateway Review

Layer 4 vs layer 7 is a guaranteed exam decision. This lab builds a Standard Load Balancer's full component set, then reviews Application Gateway through its create wizard without deploying it.

## Time Needed

35-40 minutes.

## What You Will Learn

- The Load Balancer component chain: frontend, pool, probe, rule
- Public vs internal load balancers, and inbound NAT rules
- Why health probes fail (and the NSG service tag involved)
- Application Gateway parts: listeners, backend pools, rules, WAF

## AZ-104 Concepts Covered

| Concept             | Where you see it in the lab             |
| ------------------- | --------------------------------------- |
| Standard SKU LB     | You create one with a public frontend   |
| Backend pool        | You add/point at lab resources          |
| Health probe        | You configure TCP port 80               |
| LB rule vs NAT rule | You create both types                   |
| Application Gateway | You walk the wizard: listener/rule/pool |
| WAF                 | You see where the WAF tier is chosen    |

## Cost Warning

A Standard Load Balancer bills per hour (~small but real) plus its public IP; DELETE IT at the end of this lab. Do NOT create the Application Gateway: it is one of the most expensive lab mistakes (it bills per hour at a much higher rate plus capacity units): we only read its wizard and cancel.

## Steps

### 1. Create a Standard Load Balancer

1. Search **Load balancers > Create**.
2. Resource group `rg-az104-labs`, name `lb-lab`, region as usual, SKU **Standard**, type **Public**. Note the **Internal** option: same service with a private frontend for tier-to-tier traffic.
3. Frontend IP: create a new Standard public IP `pip-lb-lab`.
4. Backend pool: name `pool-web`, VNet `vnet-lab`; add `vm-lab-01`'s NIC/IP if offered (the VM can stay deallocated; config still works).
5. Inbound rule: create a load balancing rule:

| Setting       | Value                         |
| ------------- | ----------------------------- |
| Name          | rule-http                     |
| Frontend port | 80                            |
| Backend port  | 80                            |
| Protocol      | TCP                           |
| Health probe  | new: probe-http, TCP, port 80 |

6. Create the LB.

### 2. Add an inbound NAT rule

1. On `lb-lab`, open **Inbound NAT rules > Add**: name `nat-ssh-vm1`, frontend port 2222, target `vm-lab-01`, backend port 22.
2. Meaning: LB rules DISTRIBUTE across the pool; NAT rules forward one frontend port to ONE machine: the classic "RDP/SSH to a specific VM behind the LB" answer.

### 3. Reason about probe failures

With the VM deallocated, **Insights/Monitoring** would show the probe failing: exactly what the exam describes. The checklist for "LB marks backends unhealthy":

1. Is the app listening on the probe port?
2. Does an NSG allow the probe? Probes come from the **AzureLoadBalancer** service tag (allowed by a default rule: did someone override it?).
3. Is the VM running and in the pool?

### 4. Walk the Application Gateway wizard (DO NOT CREATE)

1. Search **Application gateways > Create** and fill nothing permanent:
   - Tier: Standard V2 vs **WAF V2**: where OWASP protection is chosen.
   - Note it demands its OWN subnet in a VNet.
   - Frontends: public/private IP.
   - Backends: backend pools (can be IPs, VMs, scale sets, App Services).
   - Configuration: a ROUTING RULE ties a **listener** (port/protocol/hostname) to a backend pool with HTTP settings: this is where path-based routing lives.
2. CANCEL at Review. Do not deploy.
3. Decision table to carry out of this lab:

| Requirement                      | Pick                    |
| -------------------------------- | ----------------------- |
| TCP/UDP, any protocol, regional  | Load Balancer           |
| HTTP URL-path or host routing    | Application Gateway     |
| TLS termination, cookie affinity | Application Gateway     |
| OWASP/WAF protection             | Application Gateway WAF |
| Port-forward to one VM           | LB inbound NAT rule     |

## Clean Up

DELETE NOW: `lb-lab` and `pip-lb-lab` (Standard public IPs bill while they exist):

```bash
az network lb delete --name lb-lab --resource-group rg-az104-labs
az network public-ip delete --name pip-lb-lab --resource-group rg-az104-labs
```

Verify in the resource group that no application gateway exists (you cancelled, but check).

## Success Criteria

You are done when you can explain:

- The four LB components and what each does
- LB rule vs inbound NAT rule
- The three-step unhealthy-probe checklist and the AzureLoadBalancer tag
- Which requirements force Application Gateway over Load Balancer
- Why this lab refused to actually deploy an Application Gateway
