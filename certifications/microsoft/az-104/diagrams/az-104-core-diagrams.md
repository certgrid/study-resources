# AZ-104 Core Diagrams

This page gives visual anchors for the four structures AZ-104 tests most: governance inheritance, storage decisions, hub-spoke networking, and the monitoring pipeline.

Use these diagrams as memory anchors before practice tests. AZ-104 rarely asks you to draw architecture, but case studies assume you can see these structures in your head.

## Governance hierarchy with RBAC and Policy inheritance

```mermaid
flowchart TD
    ROOT[Tenant Root Management Group]
    MG1[Management Group: Corp]
    MG2[Management Group: Sandbox]
    SUB1[Subscription: Prod]
    SUB2[Subscription: Dev]
    SUB3[Subscription: Test]
    RG1[Resource Group: rg-app]
    RG2[Resource Group: rg-data]
    VM[Virtual Machine]
    SA[Storage Account]

    ROOT --> MG1
    ROOT --> MG2
    MG1 --> SUB1
    MG1 --> SUB2
    MG2 --> SUB3
    SUB1 --> RG1
    SUB1 --> RG2
    RG1 --> VM
    RG2 --> SA

    POLICY[Policy assigned at MG: Corp] -.applies to.-> SUB1
    POLICY -.applies to.-> SUB2
    RBAC[Reader assigned at Subscription: Prod] -.inherited by.-> RG1
    RBAC -.inherited by.-> RG2
```

Key idea: RBAC roles, Azure Policy, and locks assigned at a scope flow down to every child scope. Assign once at the management group to govern many subscriptions.

Exam memory hook:

```text
Root MG -> MG (up to 6 levels) -> Subscription -> Resource Group -> Resource
RBAC   = who can act        (inherited down)
Policy = what is allowed    (inherited down, Deny beats RBAC)
Lock   = keep it safe       (inherited down, ReadOnly beats CanNotDelete)
Tags   = organize and report (NOT inherited by default)
```

## Storage redundancy and access decision tree

```mermaid
flowchart TD
    Q1{Data must survive what?}
    Q1 -->|Disk or rack failure| LRS[LRS: 3 copies, one datacenter]
    Q1 -->|Zone failure, stay in region| ZRS[ZRS: 3 copies across zones]
    Q1 -->|Region outage| Q2{Read from secondary needed?}
    Q2 -->|No| GRS[GRS or GZRS]
    Q2 -->|Yes| RAGRS[RA-GRS or RA-GZRS]

    Q3{Who needs access?}
    Q3 -->|Time-limited external| SAS[SAS token + stored access policy]
    Q3 -->|Apps with identities| RBACD[Entra ID + Storage Blob Data roles]
    Q3 -->|Only my subnet, free| SE[Service endpoint + firewall rule]
    Q3 -->|Private IP, on-premises too| PE[Private endpoint + private DNS]

    Q4{How often is data read?}
    Q4 -->|Often| HOT[Hot tier]
    Q4 -->|Monthly, instant| COOL[Cool 30d min or Cold 90d min]
    Q4 -->|Almost never, can wait hours| ARC[Archive 180d min, rehydrate]
```

Exam memory hook:

```text
Redundancy ladder: LRS < ZRS < GRS < RA-GRS < GZRS < RA-GZRS
RA-  = readable secondary
Tiers: hot -> cool(30) -> cold(90) -> archive(180, offline)
Lifecycle rules move blobs down the ladder automatically
```

## Hub-spoke network pattern

```mermaid
flowchart TD
    ONPREM[On-premises network]
    GW[VPN Gateway or ExpressRoute<br/>in GatewaySubnet]
    HUB[Hub VNet<br/>Azure Firewall, Bastion, DNS]
    SPOKE1[Spoke VNet 1<br/>Web workload + NSG]
    SPOKE2[Spoke VNet 2<br/>Data workload + NSG]

    ONPREM === GW
    GW --- HUB
    HUB <-->|peering + gateway transit| SPOKE1
    HUB <-->|peering + gateway transit| SPOKE2
    SPOKE1 -. no direct peering:<br/>route via hub UDR .- SPOKE2
```

Key ideas:

- Peering is not transitive: spoke 1 cannot reach spoke 2 without a direct peering or a UDR sending traffic through the hub firewall.
- Gateway transit lets spokes use the hub's gateway ("allow gateway transit" on the hub, "use remote gateway" on spokes).
- Shared services (firewall, Bastion, DNS) live once in the hub.

Exam memory hook:

```text
Peering       = private backbone link, NOT transitive
Gateway transit = spokes borrow the hub's VPN/ExpressRoute
UDR 0.0.0.0/0 -> firewall = force all traffic through the hub
AzureBastionSubnet /26, GatewaySubnet = exact names required
```

## Monitoring and recovery data flow

```mermaid
flowchart LR
    RES[Resources: VMs, storage, apps, networks]
    MET[Metrics<br/>numeric, near real-time]
    LOGS[Log Analytics workspace<br/>KQL queries]
    DIAG[Diagnostic settings]
    AMA[Azure Monitor agent + DCR<br/>guest OS data]
    ALERT[Alert rules<br/>metric, log, activity log]
    AG[Action group<br/>email, SMS, webhook, runbook]
    APR[Alert processing rules<br/>suppress or attach]

    RES --> MET
    RES --> DIAG --> LOGS
    RES --> AMA --> LOGS
    MET --> ALERT
    LOGS --> ALERT
    ALERT --> APR --> AG
```

Recovery paths are separate from monitoring:

```mermaid
flowchart LR
    VM[Azure VM]
    RSV[Recovery Services vault<br/>backup policy + restore points]
    ASR[Azure Site Recovery<br/>replication to secondary region]
    RESTORE[Restore: new VM, disks, or single files]
    FAIL[Failover: run in secondary region]

    VM --> RSV --> RESTORE
    VM --> ASR --> FAIL
```

Exam memory hook:

```text
Metrics = numbers now          Logs = KQL later
Alert rule fires -> action group notifies -> processing rule can silence
Backup  = restore data   (Recovery Services vault, same region as VM)
ASR     = keep running   (failover, RPO/RTO wording)
Backup vault (newer) = Disks, Blobs, PostgreSQL
```
