# PL-900 Exam-Day Review

Use this page in the final 30-45 minutes before the exam. It is intentionally short and focused on high-frequency decisions.

## The Exam Mindset

PL-900 is a fundamentals exam. Most questions are not asking you to build anything. They are asking whether you can recognize the right product, app type, flow type, governance feature, or agent capability from the wording.

When stuck, ask:

1. Is this about which product in the family?
2. Is this about which kind of app?
3. Is this about which kind of flow, trigger, or action?
4. Is this about Dataverse structure or environment governance?
5. Is this about building, publishing, or managing an agent?

## Must-Know Pairs

| Pair                                    | Difference                                                         |
| --------------------------------------- | ------------------------------------------------------------------ |
| Canvas vs model-driven app              | Design-first pixel control vs data-first generated UI on Dataverse |
| Plan designer vs Copilot app generation | Whole solution proposal vs drafting one app                        |
| Code apps vs low-code apps              | Pro-dev code with platform governance vs maker-built apps          |
| Cloud flow vs desktop flow              | Connector/API automation vs UI recording (RPA)                     |
| Trigger vs action                       | Starts the flow (one) vs performed steps (many)                    |
| Automated vs instant vs scheduled       | Event vs button vs timetable                                       |
| Attended vs unattended RPA              | User at the machine vs runs alone                                  |
| Dataverse vs SharePoint list            | Relational platform with security and logic vs simple list         |
| Form vs view                            | One record edited vs many records listed                           |
| Business rule vs Power Fx               | Condition-based field logic vs formula language                    |
| Environment vs solution                 | Container where things live vs package that moves them             |
| Unmanaged vs managed solution           | Editable dev package vs locked test/prod package                   |
| Security role vs DLP policy             | User data permissions vs allowed connector combinations            |
| Connector vs on-premises data gateway   | Service integration vs bridge to local data                        |
| Topic vs knowledge source               | Scripted conversation vs content for generated answers             |
| Knowledge vs tools                      | Agent answers vs agent acts                                        |
| Copilot Studio vs Microsoft Agent 365   | Build agents vs manage all agents org-wide                         |
| Monitoring vs evaluations               | Live usage data vs structured quality tests                        |
| Power Apps vs Power Pages               | Internal apps vs external websites                                 |

## The Family in Ten Seconds

```text
Dataverse (data) + Connectors (reach other services)
  Power Apps        -> apps for people
  Power Automate    -> flows for processes
  Power Pages       -> websites for external users
  Copilot Studio    -> agents for conversations and actions
Copilot (AI) helps build all of them
```

## Final Component Picker

| Keyword                                  | Answer                         |
| ---------------------------------------- | ------------------------------ |
| Custom mobile app, camera, custom layout | Canvas app                     |
| UI generated from Dataverse              | Model-driven app               |
| AI proposes tables, apps, and agents     | Plan designer                  |
| Pro developers, real code, governed      | Code apps                      |
| Chat with AI to build and refine the app | Vibe experience                |
| Excel-like formulas                      | Power Fx                       |
| When email arrives, save attachment      | Automated cloud flow           |
| Button in an app runs steps              | Instant cloud flow             |
| Every Monday at 9                        | Scheduled cloud flow           |
| Legacy app, no API                       | Desktop flow (RPA)             |
| Manager approves in Teams                | Approvals                      |
| Extract invoice data                     | Document automation            |
| Reach on-premises SQL                    | On-premises data gateway       |
| Related tables with security and logic   | Microsoft Dataverse            |
| Edit one record / list many records      | Form / view                    |
| Dev, test, prod separation               | Environments                   |
| Free single-user learning environment    | Developer environment          |
| Which connectors can be combined         | DLP policy                     |
| Who can read or edit rows                | Security roles                 |
| Move solution dev -> test -> prod        | Power Platform pipelines       |
| Website for customers                    | Power Pages                    |
| Assistant that answers from documents    | Agent + knowledge source       |
| Scripted step-by-step conversation       | Topic                          |
| Agent creates a ticket                   | Tool (agent flow / MCP server) |
| Agent available in Teams and website     | Publish to channels            |
| Registry and security for all agents     | Microsoft Agent 365            |
| How many people used the agent           | Copilot Studio analytics       |
| Grade answer quality before relaunch     | Agent evaluations              |

## Last-Minute Traps

| Trap wording                                      | Better answer                                         |
| ------------------------------------------------- | ----------------------------------------------------- |
| "Model-driven app on SharePoint"                  | Model-driven apps are built on Dataverse              |
| "Cloud flow automates the legacy desktop app"     | Desktop flow does UI automation                       |
| "The email trigger is an action"                  | Whatever starts the flow is the trigger               |
| "DLP hides sensitive columns"                     | Column security hides columns; DLP governs connectors |
| "Export the app manually to production"           | Use solutions and pipelines                           |
| "Add a topic so the agent can answer from docs"   | Add a knowledge source                                |
| "Knowledge source lets the agent reset passwords" | Actions need tools                                    |
| "Power Virtual Agents"                            | Current name: Microsoft Copilot Studio                |
| "Pick Power BI for the reporting question"        | Power BI is not in the current PL-900 outline         |

## Weight Reminder

| Domain                 | Weight | Attention                            |
| ---------------------- | ------ | ------------------------------------ |
| Business value         | 5-10%  | Quick wins, know each product's job  |
| Manage the environment | 20-25% | Dataverse + governance vocabulary    |
| Power Apps             | 20-25% | App types and AI building            |
| Power Automate         | 20-25% | Flow types, triggers/actions, AI     |
| Copilot Studio agents  | 20-25% | Topics, knowledge, tools, management |

## Final Confidence Checklist

You are ready when you can explain these without looking:

- What each product in the family is for
- Canvas vs model-driven vs Plan designer vs code apps
- Cloud vs desktop flows, and trigger vs action
- Dataverse tables, columns, relationships, forms, views, business logic, Power Fx
- Environment types, security roles, column security, DLP policies
- Solutions, managed vs unmanaged, Power Platform pipelines
- Agent topics vs knowledge vs tools (agent flows, MCP servers)
- Publishing to channels, Agent 365, monitoring vs evaluations
