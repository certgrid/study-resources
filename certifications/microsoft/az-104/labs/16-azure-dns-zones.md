# Lab 16 - Azure DNS Zones

DNS questions are short and factual: zone types, record types, delegation, auto-registration. This lab creates both zone types and the records the exam names.

## Time Needed

20-25 minutes.

## What You Will Learn

- Public vs private DNS zones
- Record types and TTL basics
- What delegation to Azure DNS name servers means
- How private zone VNet links and auto-registration work

## AZ-104 Concepts Covered

| Concept           | Where you see it in the lab             |
| ----------------- | --------------------------------------- |
| Public DNS zone   | You create a zone and records           |
| NS records        | You read the four assigned name servers |
| Record types      | You create A and CNAME records          |
| Private DNS zone  | You create one and link vnet-lab        |
| Auto-registration | You enable it on the link               |

## Cost Warning

Nearly free: a DNS zone costs about half a dollar per MONTH prorated, so an hour of lab time is negligible. Delete both zones in Clean Up anyway.

## Steps

### 1. Create a public DNS zone

1. Search **DNS zones > Create**.
2. Resource group `rg-az104-labs`, name: a domain you can invent, e.g. `az104lab-example.com` (you do not need to own it for the mechanics; without delegation it just will not resolve publicly).
3. Create and open it: note the automatically created **NS** and **SOA** records. The four name servers listed are what you would enter AT YOUR REGISTRAR to delegate the domain: Azure DNS hosts zones, it does not sell domains.

### 2. Add records

1. Add an **A** record set: name `www`, TTL 3600, IP `203.0.113.10` (a documentation IP).
2. Add a **CNAME**: name `app`, alias to `www.az104lab-example.com`.
3. Note the other types in the dropdown (MX, TXT, AAAA, SRV) and the **Alias record set** toggle on the A record: alias records can track an Azure public IP resource automatically: that is its exam hook.

### 3. Query the zone directly

Cloud Shell (query Azure's name server directly, since the domain is not delegated):

```bash
nslookup www.az104lab-example.com <name-server-1-from-the-zone>
```

The A record answers even though the public internet cannot resolve it: delegation is what makes a zone live.

### 4. Create a private DNS zone

1. Search **Private DNS zones > Create**: name `corp.internal`, same resource group.
2. After creation, open **Virtual network links > Add**:
   - Link name `link-vnet-lab`, virtual network `vnet-lab`.
   - Enable **auto registration**.
3. Auto-registration meaning: VMs in vnet-lab automatically get A records here on deploy. If `vm-lab-01` is (briefly) running in that VNet, its record appears within minutes; starting it just for this is optional.
4. Add a manual A record too: `db` -> `10.10.2.10`.

### 5. Know the resolution stack

| Need                                 | Answer                          |
| ------------------------------------ | ------------------------------- |
| Default VM name resolution in a VNet | Azure-provided DNS (built in)   |
| Internet-facing domain records       | Public DNS zone + delegation    |
| Cross-VNet internal names            | Private DNS zone + VNet links   |
| Private endpoint name resolution     | privatelink.* private DNS zones |
| Use my own DNS servers               | Custom DNS setting on the VNet  |

## Clean Up

Delete both zones (`az104lab-example.com` and `corp.internal`) now; remove the VNet link first if prompted.

## Success Criteria

You are done when you can explain:

- What delegation to Azure DNS requires at the registrar (NS records)
- A vs CNAME vs alias record in one sentence each
- What a private zone VNet link does with and without auto-registration
- Why private endpoints need privatelink zones
