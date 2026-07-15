# PL-900 Common Confusions

Most wrong answers on PL-900 come from mixing up similar-sounding components. Work through each pair until the difference is obvious, then re-test yourself with the mini checks at the bottom.

## Canvas Apps vs Model-Driven Apps

| Question             | Canvas app                                | Model-driven app                                            |
| -------------------- | ----------------------------------------- | ----------------------------------------------------------- |
| Design approach      | Design-first: you place every control     | Data-first: UI generated from Dataverse                     |
| Layout control       | Total, pixel-level                        | Limited, consistent, responsive                             |
| Data sources         | Any connector                             | Dataverse                                                   |
| Typical scope        | Focused task apps, mobile                 | Full business applications                                  |
| Keyword in questions | "Custom layout," "blank canvas," "mobile" | "Generated from data," "forms and views," "complex process" |

Rule: control over the screen = canvas; UI from the data model = model-driven.

## Power Automate Cloud Flows vs Desktop Flows

| Question  | Cloud flow                        | Desktop flow                                 |
| --------- | --------------------------------- | -------------------------------------------- |
| Automates | Services through connector APIs   | Application user interfaces (clicks, typing) |
| Category  | Digital process automation        | Robotic process automation (RPA)             |
| Runs      | In the cloud                      | On a Windows machine                         |
| Fits when | The system has a connector or API | Legacy app with no API                       |
| Modes     | Automated, instant, scheduled     | Attended, unattended                         |

Rule: "no API" or "legacy desktop application" = desktop flow. Everything else defaults to cloud flow.

## Dataverse vs SharePoint Lists vs SQL Database

| Question              | Microsoft Dataverse                             | SharePoint list                   | SQL database                   |
| --------------------- | ----------------------------------------------- | --------------------------------- | ------------------------------ |
| What it is            | Business data platform built for Power Platform | Simple list storage in SharePoint | Raw relational database        |
| Relationships         | Full relational model with lookups              | Basic lookups only                | Full, but you build everything |
| Security              | Roles, row and column level, business units     | Site/list permissions             | Managed separately by DBAs     |
| Business logic and UI | Business rules, Power Fx, forms, views built in | None beyond list forms            | None; code required            |
| Licensing note        | Premium                                         | Standard connector                | Premium connector              |
| Best for              | Business apps that need security and logic      | Lightweight lists and team data   | Existing enterprise databases  |

Rule: if the scenario needs role-based security, relationships, and business logic in one platform, the answer is Dataverse.

## Copilot Studio Agents vs Power Automate Flows

| Question       | Copilot Studio agent                                  | Power Automate flow                     |
| -------------- | ----------------------------------------------------- | --------------------------------------- |
| Interface      | Conversation with a person                            | No conversation; runs in the background |
| Starts when    | A user chats (or agent triggers fire)                 | Trigger event, button, or schedule      |
| Strength       | Answering questions, collecting details interactively | Multi-step process automation           |
| Works together | Agents call agent flows as tools                      | Flows can serve agents as actions       |

Rule: dialogue = agent; background process = flow. They combine: the agent talks, the flow acts.

## Power BI Desktop vs Power BI Service (Scope Warning)

Power BI was removed from the PL-900 outline. If your practice source still asks Power BI Desktop vs Service questions, that source is outdated for this exam. Do not spend revision time here; know only that Power BI is Microsoft's analytics product and is no longer measured on PL-900 as of July 24, 2026.

## Copilot Studio vs Power Automate for "Automation"

| Scenario wording                                        | Correct product                        |
| ------------------------------------------------------- | -------------------------------------- |
| "Users ask questions and get answers"                   | Copilot Studio                         |
| "Collect request details in a chat, then open a ticket" | Copilot Studio agent + agent flow tool |
| "When a form is submitted, route for approval"          | Power Automate                         |
| "Nightly transfer between systems"                      | Power Automate                         |

## Connectors vs On-Premises Data Gateway

| Question   | Connector                                                  | On-premises data gateway                                       |
| ---------- | ---------------------------------------------------------- | -------------------------------------------------------------- |
| What it is | Prebuilt wrapper exposing a service's triggers and actions | Secure bridge between cloud and local network                  |
| Solves     | "How do I talk to service X?"                              | "How do I reach data inside our building?"                     |
| Example    | SharePoint, Outlook, SQL Server connectors                 | Cloud flow reads an on-premises SQL Server through the gateway |

Rule: the connector is the plug; the gateway is the extension cord into the on-premises network. On-premises sources need both.

## More Pairs Worth One Minute Each

| Pair                                  | Difference in one line                                                      |
| ------------------------------------- | --------------------------------------------------------------------------- |
| Trigger vs action                     | Starts the flow (one) vs steps performed (many)                             |
| Standard vs premium connector         | Included with base licensing vs requires premium licensing                  |
| Environment vs solution               | Where things live vs the package that transports them                       |
| Unmanaged vs managed solution         | Editable in dev vs locked in test/prod                                      |
| Security role vs DLP policy           | Data access for users vs allowed connector combinations                     |
| Microsoft Entra ID vs security roles  | Signs the user in vs decides what they can do with Dataverse data           |
| Form vs view                          | Edit one record vs list many records                                        |
| Business rule vs Power Fx             | Condition-based field logic vs Excel-like formula language                  |
| Topic vs knowledge source             | Scripted conversation path vs content for AI-generated answers              |
| Knowledge vs tools (agents)           | Answers questions vs takes actions                                          |
| Agent flow vs cloud flow              | Run by an agent as a tool vs runs on its own trigger or schedule            |
| Copilot Studio vs Microsoft Agent 365 | Build one agent vs manage all agents (registry, identity, security)         |
| Monitoring vs evaluations (agents)    | Live usage and adoption vs structured answer-quality testing                |
| Plan designer vs vibe experience      | AI proposes a whole solution plan vs conversational, iterative app building |
| Power Apps vs Power Pages             | Apps for internal users vs external-facing websites                         |
| Copilot (feature) vs Copilot Studio   | AI assistance inside maker tools vs the product for building agents         |

## Mini Checks

Cover the right column and answer:

| Prompt                                                         | Answer                                     |
| -------------------------------------------------------------- | ------------------------------------------ |
| App with generated UI over Dataverse forms and views           | Model-driven app                           |
| Automate an app that has no API                                | Desktop flow                               |
| Stop makers pairing Dataverse with personal storage connectors | DLP policy                                 |
| Agent must look up an order status in another system           | Tool (agent flow / MCP server / connector) |
| Reach an on-premises database from a cloud flow                | On-premises data gateway                   |
| Package an app and its tables for deployment to production     | Solution (managed) via pipelines           |
| Let the agent answer from the HR policy library                | SharePoint knowledge source                |
| One place to inventory and secure every agent in the company   | Microsoft Agent 365                        |
