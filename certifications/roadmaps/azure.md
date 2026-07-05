# Microsoft Azure Certification Roadmap

A clear path through Microsoft's Azure and role-based certifications - where to start, what comes next, and which track fits your role. Each exam links to its study cheatsheet. Always confirm current exams and objectives on Microsoft Learn, since Microsoft updates the catalog regularly.

## How Microsoft certifications are tiered

| Level | What it means | Examples |
|---|---|---|
| **Fundamentals** | Entry level, conceptual, no experience needed | AZ-900, AI-901, DP-900, SC-900, PL-900 |
| **Associate** | Role-based, hands-on skills | AZ-104, AZ-204, AI-102, DP-300, SC-200 |
| **Expert** | Advanced, usually builds on an associate | AZ-305, AZ-400, SC-100 |
| **Specialty** | Deep focus in one area | AZ-140 (Virtual Desktop) |

## Start here

If you are new to Azure, start with **[AZ-900: Azure Fundamentals](../microsoft/az900/)**. It teaches cloud concepts, core services, and pricing/governance, and it makes every later exam easier. From there, pick the track that matches your role.

## Role-based paths

```
                         AZ-900 (Azure Fundamentals)
                                   |
     ---------------------------------------------------------------
     |              |               |              |               |
 Administrator   Developer         AI            Data           Security
     |              |               |              |               |
  AZ-104         AZ-204          AI-901         DP-900          SC-900
     |              |               |              |               |
  AZ-305         AZ-400          AI-102     DP-100 / DP-300 /   SC-200 / SC-300 /
 (Architect)   (DevOps Expert)               DP-700              SC-400
                                                                    |
                                                                 SC-100
                                                            (Cybersecurity Architect)
```

## Tracks in detail

### Infrastructure / Administrator
For sysadmins and cloud engineers who manage Azure resources.
- **[AZ-900](../microsoft/az900/)** (Fundamentals) -> **[AZ-104: Azure Administrator](../microsoft/az104/)** (Associate) -> **[AZ-305: Solutions Architect Expert](../microsoft/az305/)**
- Related: **[AZ-700: Network Engineer](../microsoft/az700/)**, **[AZ-800](../microsoft/az800/)** + **[AZ-801](../microsoft/az801/)** (Windows Server hybrid), **[AZ-140: Virtual Desktop Specialty](../microsoft/az140/)**

### Developer
For software engineers building on Azure.
- **[AZ-900](../microsoft/az900/)** -> **[AZ-204: Azure Developer](../microsoft/az204/)** (Associate) -> **[AZ-400: DevOps Engineer Expert](../microsoft/az400/)**

### AI
For anyone working with Azure AI services and generative AI.
- **[AI-901: Azure AI Fundamentals](../microsoft/ai901/)** (Fundamentals, replaced the retired AI-900) -> **[AI-102: Azure AI Engineer](../microsoft/ai102/)** (Associate)

### Data
For data professionals.
- **[DP-900: Azure Data Fundamentals](../microsoft/dp900/)** -> then by focus:
  - **[DP-100: Data Scientist](../microsoft/dp100/)** (machine learning)
  - **[DP-300: Database Administrator](../microsoft/dp300/)** (operational databases)
  - **[DP-700: Fabric Data Engineer](../microsoft/dp700/)** (analytics engineering)

### Security
For security and identity professionals.
- **[SC-900: Security, Compliance & Identity Fundamentals](../microsoft/sc900/)** -> then by focus:
  - **[SC-200: Security Operations Analyst](../microsoft/sc200/)**
  - **[SC-300: Identity and Access Administrator](../microsoft/sc300/)**
  - **[SC-400: Information Protection & Compliance](../microsoft/sc400/)**
- Expert: **[SC-100: Cybersecurity Architect](../microsoft/sc100/)** (builds on a security associate)

### Power Platform
For low-code makers, analysts, and consultants.
- **[PL-900: Power Platform Fundamentals](../microsoft/pl900/)** -> **[PL-200](../microsoft/pl200/)** / **[PL-300: Power BI Data Analyst](../microsoft/pl300/)** / **[PL-400: Developer](../microsoft/pl400/)** -> **[PL-600: Solution Architect](../microsoft/pl600/)**

### Modern Work (Microsoft 365)
- **[MD-102: Endpoint Administrator](../microsoft/md102/)**, **[MS-102: Microsoft 365 Administrator](../microsoft/ms102/)**

## How to choose

- **Totally new?** AZ-900 first, always. It is the cheapest way to learn the vocabulary the other exams assume.
- **In a job already?** Skip to the associate that matches your role (AZ-104 for admins, AZ-204 for devs, SC-200 for SOC analysts).
- **Fundamentals are optional prerequisites**, not required - but they make associate exams much easier.
- **Expert exams** (AZ-305, AZ-400, SC-100) assume real experience; take them after the associate in that track.

---

Ready to test yourself? Every exam above has **free practice questions with full explanations** on **[CertGrid](https://certgrid.app)** - each question explains why every wrong answer is wrong, not just the right one.

Maintained by the team behind **[CertGrid](https://certgrid.app)**. Free plan to start. _(Disclosure: we build CertGrid.)_
