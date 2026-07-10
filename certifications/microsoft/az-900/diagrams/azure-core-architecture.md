# Azure Core Architecture

This page gives a simple visual overview of Azure organization and core services.

Use these diagrams as memory anchors before practice tests. AZ-900 rarely asks you to draw architecture, but it often asks where a service fits in the Azure hierarchy or which service belongs in a simple solution.

## Azure management hierarchy

```mermaid
flowchart TD
    MG[Management Group]
    SUB[Subscription]
    RG[Resource Group]
    VM[Virtual Machine]
    SA[Storage Account]
    SQL[Azure SQL Database]
    VNET[Virtual Network]

    MG --> SUB
    SUB --> RG
    RG --> VM
    RG --> SA
    RG --> SQL
    RG --> VNET
```

Key idea: governance and RBAC assigned higher in the hierarchy can be inherited by lower levels.

Exam memory hook:

```text
Management group = many subscriptions
Subscription     = billing/access boundary
Resource group  = lifecycle container
Resource        = actual Azure service
```

## Cloud service model responsibility

```mermaid
flowchart LR
    I[IaaS<br/>Virtual Machines]
    P[PaaS<br/>App Service / Azure SQL]
    S[SaaS<br/>Microsoft 365]
    C1[Customer manages more]
    M1[Microsoft manages more]

    C1 --> I --> P --> S --> M1
```

Exam memory hook: IaaS gives the most control, SaaS gives the least management responsibility.

## Region, zone, and resource placement

```mermaid
flowchart LR
    GEO[Geography]
    R1[Azure Region]
    R2[Paired Region]
    Z1[Availability Zone 1]
    Z2[Availability Zone 2]
    Z3[Availability Zone 3]
    VM1[VM Instance]
    VM2[VM Instance]
    VM3[VM Instance]

    GEO --> R1
    GEO --> R2
    R1 --> Z1
    R1 --> Z2
    R1 --> Z3
    Z1 --> VM1
    Z2 --> VM2
    Z3 --> VM3
```

Use availability zones for protection from datacenter failure inside one region. Use paired regions when thinking about regional disaster recovery.

Do not mix these up:

| Term              | Best memory                                  |
| ----------------- | -------------------------------------------- |
| Region            | City/area where Azure services are hosted    |
| Availability Zone | Separate datacenter location inside a region |
| Region Pair       | Two regions used for recovery planning       |

## Basic web app pattern

```mermaid
flowchart LR
    USER[Users]
    DNS[Azure DNS]
    APP[Azure App Service]
    DB[Azure SQL Database]
    MON[Azure Monitor]
    ID[Microsoft Entra ID]

    USER --> DNS
    DNS --> APP
    APP --> DB
    APP --> MON
    USER --> ID
    ID --> APP
```

For AZ-900, focus on what each part does:

- Azure DNS resolves names.
- App Service hosts the web app.
- Azure SQL Database stores relational data.
- Azure Monitor collects metrics and logs.
- Microsoft Entra ID provides identity and access.

## Governance decision flow

```mermaid
flowchart TD
    Q[What is the requirement?]
    WHO[Control who can perform actions]
    WHAT[Control what can be deployed]
    DELETE[Prevent accidental deletion]
    GROUP[Organize or report cost]

    Q --> WHO --> RBAC[Use RBAC]
    Q --> WHAT --> POLICY[Use Azure Policy]
    Q --> DELETE --> LOCK[Use resource locks]
    Q --> GROUP --> TAGS[Use tags]
```

This is one of the most useful AZ-900 decision patterns. Policy, RBAC, locks, and tags appear similar to beginners, but they solve different problems.

## Cost and monitoring lifecycle

```mermaid
flowchart LR
    PLAN[Before deployment]
    RUN[After deployment]
    IMPROVE[Optimize]
    ALERT[Detect issues]

    PLAN --> PC[Pricing Calculator]
    PLAN --> TCO[TCO Calculator]
    RUN --> CM[Cost Management]
    RUN --> MON[Azure Monitor]
    IMPROVE --> ADV[Azure Advisor]
    ALERT --> SH[Service Health]
```

Memory hook:

- Pricing Calculator estimates planned Azure services.
- TCO Calculator compares on-premises cost with Azure.
- Cost Management tracks actual spend.
- Azure Monitor collects metrics, logs, and alerts.
- Azure Advisor gives recommendations.
- Service Health shows personalized service issues.

