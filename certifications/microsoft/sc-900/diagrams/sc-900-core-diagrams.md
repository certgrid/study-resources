# SC-900 Core Diagrams

This page gives a simple visual overview of the Zero Trust model, the Microsoft security portfolio, and the identity flow.

Use these diagrams as memory anchors before practice tests. SC-900 rarely asks you to draw architecture, but it constantly asks which product family owns a problem and what order things happen in.

## Zero Trust model

```mermaid
flowchart TD
    REQ[Every access request]
    P1[Verify explicitly]
    P2[Least privilege access]
    P3[Assume breach]
    ID[Identities]
    DEV[Devices]
    APP[Applications]
    DATA[Data]
    INFRA[Infrastructure]
    NET[Networks]

    REQ --> P1
    REQ --> P2
    REQ --> P3
    P1 --> ID
    P1 --> DEV
    P2 --> APP
    P2 --> DATA
    P3 --> INFRA
    P3 --> NET
```

Key idea: no request is trusted because of its network location. Every request is authenticated, authorized, and scoped to least privilege, and the environment is designed as if a breach has already happened.

Exam memory hook:

```text
3 principles = verify explicitly, least privilege, assume breach
6 pillars    = identities, devices, applications, data, infrastructure, networks
```

## Microsoft security portfolio map

```mermaid
flowchart TD
    Q[Which family owns the problem?]
    ENTRA[Microsoft Entra<br/>Identity and access]
    DEF[Microsoft Defender<br/>Threat protection]
    SEN[Microsoft Sentinel<br/>SIEM + SOAR]
    PUR[Microsoft Purview<br/>Compliance and data]

    Q --> ENTRA
    Q --> DEF
    Q --> SEN
    Q --> PUR

    ENTRA --> CA[Conditional Access]
    ENTRA --> PIM[PIM / Governance]
    ENTRA --> IDP[ID Protection]

    DEF --> DFC[Defender for Cloud<br/>cloud posture + workloads]
    DEF --> XDR[Defender XDR<br/>email, endpoint, apps, identity]

    SEN --> SIEM[Collect all logs]
    SEN --> SOAR[Automate response]

    PUR --> IP[Labels + DLP]
    PUR --> RET[Retention + records]
    PUR --> INV[Insider risk, eDiscovery, audit]
```

Exam memory hook:

```text
Entra    = who gets in
Defender = who is attacking
Sentinel = what do all the logs say, and auto-respond
Purview  = how data is classified, protected, kept, and investigated
```

## Identity flow: authentication to access

```mermaid
flowchart LR
    USER[User or workload identity]
    IDP[Microsoft Entra ID<br/>identity provider]
    RISK[ID Protection<br/>risk signals]
    CA[Conditional Access<br/>policy decision]
    MFA[Require MFA /<br/>compliant device]
    APP[Application or resource]
    RBAC[Roles / RBAC<br/>authorization]

    USER --> IDP
    RISK --> CA
    IDP --> CA
    CA --> MFA
    MFA --> APP
    CA --> APP
    APP --> RBAC
```

Order matters on the exam:

1. Authentication: Entra ID verifies the identity (password, passwordless, MFA).
2. Risk evaluation: ID Protection scores user risk and sign-in risk as signals.
3. Policy decision: Conditional Access decides block, grant, or grant with controls.
4. Authorization: roles and RBAC decide what the identity can DO once inside.

Exam memory hook:

```text
AuthN first (prove who), policy next (should we allow), AuthZ last (what can you do)
Detect = ID Protection, Enforce = Conditional Access
```

## Threat signal flow: Defender to Sentinel

```mermaid
flowchart LR
    O365[Defender for Office 365<br/>email]
    EP[Defender for Endpoint<br/>devices]
    CAPPS[Defender for Cloud Apps<br/>SaaS apps]
    DI[Defender for Identity<br/>on-prem AD]
    XDR[Microsoft Defender XDR<br/>unified incidents]
    DFC[Defender for Cloud<br/>cloud workloads]
    THIRD[Third-party sources<br/>firewalls, AWS, syslog]
    SEN[Microsoft Sentinel<br/>SIEM + SOAR]
    PLAY[Playbooks<br/>automated response]

    O365 --> XDR
    EP --> XDR
    CAPPS --> XDR
    DI --> XDR
    XDR --> SEN
    DFC --> SEN
    THIRD --> SEN
    SEN --> PLAY
```

Key idea: the four Defender XDR services correlate into unified incidents; Sentinel sits above everything and can ingest Defender XDR, Defender for Cloud, AND third-party sources, then automate response with playbooks.

Exam memory hook:

```text
Email -> Defender for Office 365
Device -> Defender for Endpoint
SaaS app -> Defender for Cloud Apps
On-prem AD -> Defender for Identity
All of it + third party -> Sentinel
```
