# PL-900: Microsoft Power Platform Fundamentals

PL-900 is the best first step for learning Microsoft Power Platform. It does not expect deep app-making or administration experience, but it does expect you to recognize what Power Apps, Power Automate, Microsoft Dataverse, connectors, Power Pages, and Microsoft Copilot Studio each do, how environments and governance work, and how AI and Copilot features help you build apps, flows, and agents.

These notes are built for fast revision and real understanding. Read the domain notes once, do the labs in a free developer environment, then use the cheatsheets to remove confusion before taking practice tests.

## Start Here

Pick the path that matches your timeline:

| If you have...               | Use this path                                                                                                                                                                                             |
| ---------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1 day                        | Read [Exam-Day Review](cheatsheets/pl-900-exam-day-review.md), then [Common Confusions](cheatsheets/pl-900-common-confusions.md)                                                                          |
| 3 days                       | Read the five study notes, review [Service Picker](cheatsheets/pl-900-service-picker.md), then do practice questions                                                                                      |
| 5 days                       | Follow the recommended plan below and complete the developer plan, Dataverse, canvas app, cloud flow, agent, and cleanup labs                                                                             |
| No Power Platform experience | Start with [00 - Get a Free Power Apps Developer Plan](labs/00-get-power-apps-developer-plan.md), then [01 - Explore the Maker Portal and Admin Center](labs/01-explore-maker-portal-and-admin-center.md) |

## What to Memorize vs Understand

| Memorize                                                                                           | Understand                                                             |
| -------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| The product family: Power Apps, Power Automate, Dataverse, connectors, Power Pages, Copilot Studio | Which business problem each product solves                             |
| Canvas app vs model-driven app vs Plan designer vs code apps                                       | Which app type fits a scenario and who builds it                       |
| Cloud flow vs desktop flow, trigger vs action                                                      | When automation needs an API connector vs UI recording                 |
| Dataverse building blocks: tables, columns, relationships, forms, views                            | Why Dataverse beats spreadsheets and plain databases for business apps |
| Environment types and the security layers                                                          | How environments, security roles, and DLP policies work together       |
| Agent building blocks: topics, knowledge, tools, channels                                          | When an agent answers from knowledge vs takes action with a tool       |

## Exam Snapshot

| Item           | Detail                                                      |
| -------------- | ----------------------------------------------------------- |
| Exam code      | PL-900                                                      |
| Certification  | Microsoft Certified: Power Platform Fundamentals            |
| Level          | Beginner                                                    |
| Passing score  | 700 out of 1000                                             |
| Question style | Conceptual and scenario-based fundamentals                  |
| Best for       | Business users, students, and low-code beginners            |
| Study approach | Learn concepts, compare components, build small things free |

## Official Skill Areas

Aligned to the official "Skills measured as of July 24, 2026" outline. Always confirm the active outline on the [official study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/pl-900) before booking.

Last verified: July 10, 2026.

Note the outline date: July 24, 2026 is in the future, so if you take the exam before that date you should re-check which outline version applies to your exam date - especially important here, because the older outline still included Power BI.

| Domain | Skill area                                                               | Weight |
| ------ | ------------------------------------------------------------------------ | ------ |
| 1      | Describe the business value of Microsoft Power Platform                  | 5-10%  |
| 2      | Manage the Microsoft Power Platform environment                          | 20-25% |
| 3      | Demonstrate the capabilities of Power Apps                               | 20-25% |
| 4      | Demonstrate the capabilities of Power Automate                           | 20-25% |
| 5      | Describe features and capabilities of agents in Microsoft Copilot Studio | 20-25% |

Important scope note: older PL-900 study material covers Power BI, AI Builder, Power Virtual Agents, and a dedicated Power Pages domain. None of those are in the current outline. Power Pages appears only as one business-value bullet, Power Virtual Agents is now Microsoft Copilot Studio, and Copilot Studio agents are a full 20-25% domain. Do not spend study time on removed topics.

## How to Use This Folder

1. Read the five study notes in order.
2. Open the common-confusions file and check every pair you mix up.
3. Complete the beginner labs so the terms become real in the maker portal.
4. Review the platform map diagram before practice tests.
5. Use the quick reference on the final day.

## Contents

Every bullet of the official outline is mapped to these files in the [Coverage Matrix](coverage-matrix.md).

### Study Notes

| File                                                                                       | Use it for                                                                |
| ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------- |
| [01 - Business Value of Power Platform](study-notes/01-business-value.md)                  | What each product is for, connectors, generative AI value, agents         |
| [02 - Manage the Power Platform Environment](study-notes/02-power-platform-environment.md) | Dataverse, environments, security, privacy, monitoring, ALM and pipelines |
| [03 - Power Apps Capabilities](study-notes/03-power-apps.md)                               | Canvas, model-driven, Plan designer, code apps, building apps with AI     |
| [04 - Power Automate Capabilities](study-notes/04-power-automate.md)                       | Cloud and desktop flows, triggers and actions, building flows with AI     |
| [05 - Copilot Studio Agents](study-notes/05-copilot-studio-agents.md)                      | Topics, knowledge, tools, channels, Agent 365, monitoring, evaluations    |

### Cheatsheets

| File                                                                                      | Use it for                                                     |
| ----------------------------------------------------------------------------------------- | -------------------------------------------------------------- |
| [PL-900 Quick Reference](cheatsheets/pl-900-quick-reference.md)                           | Last-day revision                                              |
| [PL-900 Common Confusions](cheatsheets/pl-900-common-confusions.md)                       | Fixing the trap pairs that cause wrong answers                 |
| [PL-900 Service Picker](cheatsheets/pl-900-service-picker.md)                             | Choosing the right Power Platform component                    |
| [PL-900 Exam-Day Review](cheatsheets/pl-900-exam-day-review.md)                           | Final 30-45 minute review before the exam                      |
| [PL-900 Mock Review](cheatsheets/pl-900-mock-review.md)                                   | Mixed scenario drills across all five domains                  |
| [PL-900 Governance and Security Matrix](cheatsheets/pl-900-governance-security-matrix.md) | One-page map of environments, roles, DLP, solutions, pipelines |

### Hands-On Labs

All labs run on free plans. Lab 00 explains the free options and what could cost money.

| Lab                                                                                                | What it teaches                                                 |
| -------------------------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| [00 - Get a Free Power Apps Developer Plan](labs/00-get-power-apps-developer-plan.md)              | Free developer environment, licensing awareness, sign-in        |
| [01 - Explore the Maker Portal and Admin Center](labs/01-explore-maker-portal-and-admin-center.md) | Maker portal, admin center, environments, where things live     |
| [02 - Explore a Dataverse Table](labs/02-explore-a-dataverse-table.md)                             | Tables, columns, relationships, forms, views                    |
| [03 - Create a Dataverse Table](labs/03-create-a-dataverse-table.md)                               | Creating tables and columns, using Copilot to describe a table  |
| [04 - Build a Canvas App from Data](labs/04-build-a-canvas-app-from-data.md)                       | Canvas apps, screens, controls, connecting to Dataverse         |
| [05 - Explore a Model-Driven App](labs/05-explore-a-model-driven-app.md)                           | Model-driven apps, forms, views, sitemap, data-first design     |
| [06 - Build a Simple Cloud Flow](labs/06-build-a-simple-cloud-flow.md)                             | Triggers, actions, connectors, testing a flow                   |
| [07 - Build an Approval Flow](labs/07-build-an-approval-flow.md)                                   | Approvals, Teams and Outlook integration, conditions            |
| [08 - Create an Agent in Copilot Studio](labs/08-create-an-agent-in-copilot-studio.md)             | Agents, topics, knowledge sources, testing, publishing concepts |
| [09 - Clean Up Your Environment](labs/09-clean-up-environment.md)                                  | Deleting apps, flows, agents, tables, trial hygiene             |

### Diagrams

| Diagram                                              | What it teaches                                                     |
| ---------------------------------------------------- | ------------------------------------------------------------------- |
| [Power Platform Map](diagrams/power-platform-map.md) | Product family map, Dataverse-centered data flow, solution patterns |

## What Usually Decides Pass or Fail

Most PL-900 mistakes come from confusing similar components:

| If you confuse...                              | Review                                                        |
| ---------------------------------------------- | ------------------------------------------------------------- |
| Canvas apps and model-driven apps              | Design-first pixel control vs data-first generated UI         |
| Cloud flows and desktop flows                  | API connector automation vs UI recording (RPA)                |
| Dataverse and SharePoint lists                 | Relational business data platform vs simple list storage      |
| Copilot Studio agents and Power Automate flows | Conversations with users vs background process automation     |
| Connectors and the on-premises data gateway    | Service integration vs secure bridge to local data            |
| Environments and solutions                     | Container for data and apps vs package for transporting them  |
| Security roles and DLP policies                | Who can do what in an environment vs which connectors can mix |
| Topics, knowledge sources, and tools           | Scripted conversation vs answer source vs action taken        |

## High-Value Exam Traps

| Trap                                                         | Correct thinking                                            |
| ------------------------------------------------------------ | ----------------------------------------------------------- |
| "Automate a legacy desktop app with no API"                  | Use a desktop flow (RPA), not a cloud flow.                 |
| "Need pixel-perfect control over the app layout"             | Canvas app, not model-driven app.                           |
| "App UI should be generated from Dataverse data"             | Model-driven app.                                           |
| "Flow should start when an email arrives"                    | That is a trigger, not an action.                           |
| "Cloud flow needs data from an on-premises SQL Server"       | Add the on-premises data gateway, not just the connector.   |
| "Agent must answer questions from a SharePoint site"         | Add a knowledge source in Copilot Studio.                   |
| "Agent must create a ticket in another system"               | Give the agent a tool, such as an agent flow or MCP server. |
| "Stop makers combining business data with personal services" | Use a data loss prevention (DLP) policy.                    |
| "Move an app from dev to test to production"                 | Use solutions with Power Platform pipelines (ALM).          |
| "Describe the app you want and let AI draft it"              | Copilot / Plan designer / vibe experience in Power Apps.    |

## Recommended 5-Day Plan

| Day | Focus                                                                   |
| --- | ----------------------------------------------------------------------- |
| 1   | Business value of the product family, connectors, generative AI, agents |
| 2   | Dataverse, environments, security model, governance, ALM and pipelines  |
| 3   | Power Apps types and Power Automate flows, building with AI             |
| 4   | Copilot Studio agents, labs, common confusions                          |
| 5   | Quick reference, practice questions, wrong-answer review                |

## Readiness Checklist

Before booking, you should be able to explain these without notes:

- What each family member does: Power Apps, Power Automate, Dataverse, connectors, Power Pages, Copilot Studio
- Canvas app vs model-driven app vs Plan designer vs code apps
- Cloud flow vs desktop flow, and trigger vs action
- Why Dataverse is more than a database: forms, views, business logic, security
- Environment types and what security roles and DLP policies each control
- Solutions, managed vs unmanaged, and Power Platform pipelines
- Topics vs knowledge sources vs tools in a Copilot Studio agent
- How agents are published to channels and managed with Microsoft Agent 365

## Score Booster Routine

Use this after each practice test:

1. Write down every wrong answer in one line.
2. Label the reason: product confusion, app-type confusion, flow confusion, governance confusion, or agent confusion.
3. Re-read only the matching section in this folder.
4. Add the confused pair to your own notes.
5. Retake a small focused quiz before doing another full mock.

The goal is not to memorize answers. The goal is to stop repeating the same type of mistake.

## Note on Exam Content

These are original study notes. They do not contain real exam questions or leaked content. Use them to understand the concepts, then practice with scenario-based questions and hands-on tasks.

---

Maintained by the team behind [CertGrid](https://certgrid.app). Free practice is available on CertGrid, but these notes are useful on their own.
