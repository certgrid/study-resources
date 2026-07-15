# PL-900 Service Picker

PL-900 questions often describe a business need and ask which Power Platform component fits. Use these tables to decide fast.

## Step 1: Which product?

| The business needs...                                    | Pick                     |
| -------------------------------------------------------- | ------------------------ |
| A custom application for staff                           | Power Apps               |
| A repetitive process automated                           | Power Automate           |
| A secure place to store structured business data         | Microsoft Dataverse      |
| Integration with another service without custom code     | A connector              |
| A website for customers, citizens, or partners           | Power Pages              |
| A conversational assistant that answers and acts         | Microsoft Copilot Studio |
| AI to draft the app, flow, table, or agent for the maker | Copilot / generative AI  |

## Step 2: Which Power Apps experience?

| Scenario                                                    | Pick                      | Because                                 |
| ----------------------------------------------------------- | ------------------------- | --------------------------------------- |
| Mobile field app with custom layout and camera              | Canvas app                | Design-first, any connector, mobile     |
| Case management over many related Dataverse tables          | Model-driven app          | Data-first, generated forms and views   |
| "Describe the business problem, propose the whole solution" | Plan designer             | AI proposes roles, tables, apps, agents |
| Developers want to write code but keep platform governance  | Code apps                 | Pro-code on Power Platform              |
| Maker wants AI to draft an app, then refine it by chatting  | Copilot + vibe experience | Conversational, iterative building      |

## Step 3: Which flow?

| Scenario                                              | Pick                             | Because                   |
| ----------------------------------------------------- | -------------------------------- | ------------------------- |
| "When an item/email/response arrives, do steps"       | Automated cloud flow             | Event trigger             |
| User taps a button (in an app or on mobile) to run it | Instant cloud flow               | Manual trigger            |
| Runs every day/week at a set time                     | Scheduled cloud flow             | Time trigger              |
| Legacy desktop application, no API                    | Desktop flow                     | RPA / UI automation       |
| RPA that must run overnight with nobody signed in     | Unattended desktop flow          | No user present           |
| Manager sign-off inside Teams or Outlook              | Cloud flow with Approvals        | Built-in approval actions |
| Pull totals out of PDF invoices automatically         | Document automation              | AI document processing    |
| Reach an on-premises database or file share           | Add the on-premises data gateway | Bridge to local network   |

## Step 4: Which data store?

| Scenario                                                    | Pick                                         | Because                             |
| ----------------------------------------------------------- | -------------------------------------------- | ----------------------------------- |
| Business data with security roles, relationships, and logic | Dataverse                                    | Purpose-built platform, premium     |
| Lightweight team list already living in SharePoint          | SharePoint list                              | Simple, standard connector          |
| Existing enterprise database must stay where it is          | SQL via connector (+ gateway if on-premises) | Reuse what exists                   |
| Data for a model-driven app                                 | Dataverse                                    | Model-driven apps require Dataverse |

## Step 5: Which agent capability?

| Scenario                                                        | Pick                          | Because                            |
| --------------------------------------------------------------- | ----------------------------- | ---------------------------------- |
| Answer open questions from websites, SharePoint, or files       | Knowledge source              | Grounded generative answers        |
| Walk the user through fixed questions in order                  | Topic                         | Scripted conversation path         |
| Create a ticket / update a record / call a system               | Tool: agent flow or connector | Actions need tools                 |
| Use tools exposed by an external system via a standard protocol | MCP server                    | Model Context Protocol integration |
| Make the agent available in Teams and on the website            | Publish to channels           | One agent, many channels           |
| Inventory, identity, and security for all agents in the org     | Microsoft Agent 365           | Org-scale agent management         |
| See sessions, outcomes, and adoption                            | Copilot Studio analytics      | Monitoring usage                   |
| Grade answer quality with structured test question sets         | Agent evaluations             | Quality testing                    |

## Step 6: Which admin/governance feature?

| Scenario                                                   | Pick                        |
| ---------------------------------------------------------- | --------------------------- |
| Separate dev, test, and production work                    | Environments                |
| Free personal environment for learning                     | Developer environment       |
| Control what a user can do with Dataverse data             | Security roles              |
| Hide the salary column from most users                     | Column-level security       |
| Block or separate risky connectors                         | DLP policy                  |
| Review tenant-wide usage, capacity, and policies           | Power Platform admin center |
| Read Microsoft's privacy and compliance commitments        | Microsoft Trust Center      |
| Transport apps, flows, tables, agents between environments | Solutions                   |
| Guided deployment dev -> test -> prod                      | Power Platform pipelines    |

## Common Head-to-Head Calls

| If torn between...          | Choose...    | When the question says...                               |
| --------------------------- | ------------ | ------------------------------------------------------- |
| Canvas vs model-driven      | Canvas       | Layout control, mobile, mixed data sources              |
| Canvas vs model-driven      | Model-driven | Generated UI, Dataverse-centric, complex process        |
| Power Apps vs Power Pages   | Power Pages  | Audience is outside the organization                    |
| Cloud flow vs desktop flow  | Desktop flow | "No API," "legacy," "manual data entry into an old app" |
| Flow vs agent               | Agent        | Users converse; questions get answered                  |
| Dataverse vs SharePoint     | Dataverse    | Security roles, relationships, business logic           |
| Connector vs gateway        | Both         | Cloud reaching on-premises data                         |
| Copilot Studio vs Agent 365 | Agent 365    | "All agents across the organization"                    |

Note on scope: Power BI and AI Builder are not in the current PL-900 outline, so they should not be the answer to current-exam questions. If a practice question's only sensible answer is Power BI, the question is from an older outline.
