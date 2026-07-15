# Power Platform Map

This page gives a simple visual overview of the Power Platform family and how the pieces combine into solutions.

Use these diagrams as memory anchors before practice tests. PL-900 rarely asks you to draw architecture, but it often asks which component fits a scenario or how components work together.

## The Power Platform family

```mermaid
flowchart TD
    PP[Microsoft Power Platform]
    PA[Power Apps<br/>build apps]
    AUTO[Power Automate<br/>automate processes]
    PG[Power Pages<br/>external websites]
    CS[Microsoft Copilot Studio<br/>build agents]
    DV[Microsoft Dataverse<br/>business data]
    CON[Connectors<br/>reach other services]
    AI[Copilot / generative AI<br/>helps build everything]

    PP --> PA
    PP --> AUTO
    PP --> PG
    PP --> CS
    PA --> DV
    AUTO --> DV
    PG --> DV
    CS --> DV
    PA --> CON
    AUTO --> CON
    CS --> CON
    AI -.-> PA
    AI -.-> AUTO
    AI -.-> CS
    AI -.-> DV
```

Exam memory hook:

```text
Power Apps      = apps for people
Power Automate  = flows for processes
Power Pages     = websites for external users
Copilot Studio  = agents for conversations and actions
Dataverse       = the shared data platform
Connectors      = bridges to everything else
Copilot         = AI that drafts all of the above
```

## Dataverse-centered data flow

```mermaid
flowchart LR
    SP[SharePoint / Microsoft 365]
    SQL[On-premises SQL Server]
    GW[On-premises data gateway]
    CON[Connectors]
    DV[Microsoft Dataverse<br/>tables, columns, relationships<br/>forms, views, business logic]
    APP[Power Apps]
    FLOW[Power Automate]
    AGENT[Copilot Studio agent]
    ROLES[Security roles<br/>row and column security]

    SP --> CON
    SQL --> GW --> CON
    CON --> DV
    DV --> APP
    DV --> FLOW
    DV --> AGENT
    ROLES --> DV
```

Key idea: Dataverse sits in the middle. Connectors (plus the gateway for on-premises sources) bring data in and out, security roles guard the data, and apps, flows, and agents all work against the same tables.

Exam memory hook:

```text
Connector = the plug into a service
Gateway   = the extension cord into the on-premises network
Dataverse = data + security + logic + forms + views in one platform
```

## Solution pattern: app + flow + agent

```mermaid
flowchart LR
    USER[Employee]
    APP[Canvas app<br/>submit a request]
    DV[Dataverse<br/>Request table]
    FLOW[Cloud flow<br/>approval + notification]
    MGR[Manager<br/>approves in Teams]
    AGENT[Copilot Studio agent<br/>answers status questions]
    KNOW[Knowledge source<br/>policy documents]

    USER --> APP --> DV
    DV --> FLOW --> MGR
    MGR --> FLOW
    USER --> AGENT
    AGENT --> DV
    KNOW --> AGENT
```

This is the classic PL-900 combined scenario: an app collects data into Dataverse, an automated flow routes the approval to Teams, and an agent answers questions using the same data plus knowledge documents.

Exam memory hook:

```text
App    = collects and shows data
Flow   = moves the process forward
Agent  = answers questions and takes actions on request
All three share one Dataverse
```

## Governance and ALM flow

```mermaid
flowchart LR
    DEV[Development environment<br/>unmanaged solution]
    TEST[Test environment<br/>managed solution]
    PROD[Production environment<br/>managed solution]
    PIPE[Power Platform pipelines]
    ADMIN[Power Platform admin center<br/>environments, DLP, analytics]

    DEV --> PIPE --> TEST --> PIPE2[Pipelines] --> PROD
    ADMIN -.-> DEV
    ADMIN -.-> TEST
    ADMIN -.-> PROD
```

Key idea: work is built unmanaged in development, packaged into a solution, and deployed managed through pipelines into test and production. The admin center governs all environments with DLP policies, security, and analytics.

Exam memory hook:

```text
Environment = the container (dev, test, prod, sandbox, trial, developer)
Solution    = the package (unmanaged in dev, managed in test/prod)
Pipelines   = the guided path dev -> test -> prod
Admin center = where admins watch and govern all of it
```
