# PL-900 Quick Reference

Last-day revision sheet. Everything here is recognition-level: read it slowly once, then skim it again right before practice questions.

## The Product Family

| Product                  | One-line job                                                   |
| ------------------------ | -------------------------------------------------------------- |
| Power Apps               | Build custom business apps with little or no code              |
| Power Automate           | Automate processes: cloud flows (APIs) and desktop flows (RPA) |
| Microsoft Dataverse      | Secure data platform: tables, columns, relationships, logic    |
| Connectors               | Prebuilt triggers and actions for over a thousand services     |
| Power Pages              | External-facing business websites on Dataverse                 |
| Microsoft Copilot Studio | Build agents that answer questions and take actions            |
| Copilot / generative AI  | Describe what you want; AI drafts apps, flows, tables, agents  |

Current names: Microsoft Copilot Studio (not Power Virtual Agents) and Microsoft Dataverse (not Common Data Service). Older prep material using the old names is out of date.

## Power Apps in One Table

| App experience   | Start from            | Control     | Data          | Best for                                    |
| ---------------- | --------------------- | ----------- | ------------- | ------------------------------------------- |
| Canvas app       | Blank screen or data  | Total       | Any connector | Task and mobile apps, custom UI             |
| Model-driven app | Dataverse data model  | Generated   | Dataverse     | Complex, process-driven business apps       |
| Plan designer    | Business problem (AI) | AI-proposed | Dataverse     | Whole-solution design: tables, apps, agents |
| Code apps        | Professional code     | Full code   | Connectors    | Pro-dev apps with platform governance       |

AI building: Copilot generates canvas and model-driven apps from descriptions; the vibe experience is conversational, iterative refinement of AI-powered apps.

## Power Automate in One Table

| Flow concept        | Remember                                                       |
| ------------------- | -------------------------------------------------------------- |
| Cloud flow          | Connector/API automation in the cloud                          |
| Desktop flow        | UI automation (RPA) on a Windows machine, for apps with no API |
| Automated flow      | Starts on an event ("when an item is created")                 |
| Instant flow        | Starts when a user presses a button                            |
| Scheduled flow      | Starts on a timetable                                          |
| Trigger             | Starts the flow; exactly one per cloud flow                    |
| Action              | A step the flow performs; many per flow                        |
| Attended RPA        | User present at the machine                                    |
| Unattended RPA      | Runs with no user present                                      |
| Approvals           | Approve/reject in Teams, Outlook, or the Approvals app         |
| Document automation | AI extracts data from documents such as invoices               |

Named use cases to recognize: approvals, Teams, Outlook, SharePoint, Forms, document automation.

## Dataverse in One Table

| Concept       | Remember                                                             |
| ------------- | -------------------------------------------------------------------- |
| Table         | One kind of thing (Customer, Order)                                  |
| Column        | One field on a record                                                |
| Relationship  | One-to-many (lookup) or many-to-many between tables                  |
| Form          | Layout to view/edit ONE record                                       |
| View          | Filtered, sorted list of MANY records                                |
| Business rule | No-code field logic (require, show/hide, set values)                 |
| Power Fx      | Excel-like formula language (canvas apps, formula columns)           |
| vs SQL/Excel  | Dataverse adds security, logic, forms, views, rich types, SaaS       |
| Copilot       | Creates and edits tables, columns, relationships from plain language |

## Environments and Governance in One Table

| Concept              | Remember                                                                        |
| -------------------- | ------------------------------------------------------------------------------- |
| Environment          | Container for apps, flows, agents, and one Dataverse database                   |
| Types                | Default, production, sandbox, trial, developer                                  |
| Managed Environments | Extra governance and insights switched on by admins                             |
| Security role        | What a user can do with Dataverse data                                          |
| Column security      | Hides sensitive columns                                                         |
| DLP policy           | Which connectors may be used and combined (business vs non-business vs blocked) |
| Entra ID             | Authentication (who can sign in)                                                |
| Admin center         | Environments, capacity, policies, tenant analytics                              |
| Trust Center         | Microsoft privacy and compliance commitments                                    |
| Solution             | Package to transport apps/flows/tables between environments                     |
| Unmanaged / managed  | Editable in dev / locked in test and prod                                       |
| Pipelines            | Guided ALM deployment dev -> test -> prod                                       |

## Copilot Studio Agents in One Table

| Concept          | Remember                                                               |
| ---------------- | ---------------------------------------------------------------------- |
| Agent            | AI assistant that answers questions and takes actions                  |
| Topic            | Scripted conversation path with trigger phrases and nodes              |
| Knowledge source | Content the agent answers from: websites, SharePoint, files, Dataverse |
| Tool             | Lets the agent act: agent flows, MCP servers, connector actions        |
| MCP server       | Standard way to expose external tools and data to the agent            |
| Channel          | Where users meet the agent: Teams, Microsoft 365 Copilot, website      |
| Test pane        | Maker-side testing before publishing                                   |
| Agent 365        | Org-wide agent registry, identity, security, observability             |
| Analytics        | Usage and adoption: sessions, outcomes, top topics                     |
| Evaluations      | Structured quality testing of agent answers                            |

## Ten-Second Decision Rules

| Hear this...                                   | Answer this                    |
| ---------------------------------------------- | ------------------------------ |
| Pixel-perfect / blank screen / mobile          | Canvas app                     |
| Generated UI from Dataverse                    | Model-driven app               |
| AI proposes tables + apps + agents             | Plan designer                  |
| Pro developers, real code, platform governance | Code apps                      |
| No API, legacy desktop app                     | Desktop flow (RPA)             |
| "When X happens, do Y" across services         | Automated cloud flow           |
| External-facing website                        | Power Pages                    |
| Conversational assistant                       | Copilot Studio agent           |
| Answer from documents                          | Knowledge source               |
| Agent takes an action                          | Tool (agent flow / MCP server) |
| Control connector combinations                 | DLP policy                     |
| Move solution between environments             | Solutions + pipelines          |
| On-premises data from the cloud                | On-premises data gateway       |

## Out of Scope (Old Material Warning)

These appear in older PL-900 prep but are NOT in the current outline: Power BI (entire domain removed), AI Builder, Power Virtual Agents (renamed to Copilot Studio), and the dedicated Power Pages domain (only its business value remains). Skip them.
