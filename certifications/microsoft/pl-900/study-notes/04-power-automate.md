# 04 - Demonstrate the Capabilities of Power Automate

This domain is worth 20-25% of the exam. It tests two things: recognizing the right flow type and use case (cloud vs desktop, approvals, Teams, Outlook, SharePoint, Forms, document automation), and understanding how flows are built (connector triggers and actions, plus using AI to create and modify cloud and desktop flows).

## Mental model

A flow is a recipe: "when this happens (trigger), do these steps (actions)." Cloud flows cook with APIs: they call services through connectors. Desktop flows cook with hands: they click and type in application UIs like a human would (robotic process automation). If the system has a connector, use a cloud flow; if it is a legacy app with no API, use a desktop flow.

| Scenario keyword                                    | Likely concept            |
| --------------------------------------------------- | ------------------------- |
| "When an item is created..." / "when email arrives" | Trigger (cloud flow)      |
| Send an email, create a row, post a message         | Actions                   |
| Legacy desktop app, no API, repetitive data entry   | Desktop flow (RPA)        |
| Manager must approve before the process continues   | Approvals                 |
| Run every Monday at 9 AM                            | Scheduled cloud flow      |
| Run when the user presses a button                  | Instant cloud flow        |
| Extract data from invoices and documents            | Document automation       |
| "Describe the flow and AI builds it"                | Copilot in Power Automate |

## Cloud flows vs desktop flows

| Aspect       | Cloud flow                            | Desktop flow                                         |
| ------------ | ------------------------------------- | ---------------------------------------------------- |
| How it works | Calls services through connector APIs | Automates the user interface of desktop and web apps |
| Category     | Digital process automation (DPA)      | Robotic process automation (RPA)                     |
| Runs         | In the cloud                          | On a Windows machine                                 |
| Built with   | Power Automate portal designer        | Power Automate for desktop (recorder and designer)   |
| Best for     | Modern services with connectors       | Legacy apps without APIs, repetitive UI tasks        |
| Example      | Save Forms responses to Dataverse     | Type invoice data into an old accounting program     |

Desktop flow modes to recognize:

| Mode       | Meaning                                                |
| ---------- | ------------------------------------------------------ |
| Attended   | Runs while a user is signed in and can watch or assist |
| Unattended | Runs on its own without a user present                 |

Cloud flows can trigger desktop flows, which is how cloud and legacy automation combine end to end.

### Types of cloud flows

| Cloud flow type | Starts when                             | Example                                      |
| --------------- | --------------------------------------- | -------------------------------------------- |
| Automated       | An event happens in a connected service | When a SharePoint item is created            |
| Instant         | A user manually triggers it (button)    | Run from the Power Apps button or mobile app |
| Scheduled       | A timetable is reached                  | Every weekday at 8 AM, send a summary        |

## High-frequency use cases

The outline names these use cases explicitly. Recognize each pattern:

| Use case            | Typical flow pattern                                                                                                         |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| Approvals           | Start an approval action; the approver responds in Teams, Outlook, or the Approvals app; the flow branches on approve/reject |
| Microsoft Teams     | Post messages to channels or chats, trigger flows from messages, notify people                                               |
| Outlook             | Trigger on incoming email, send emails, process attachments                                                                  |
| SharePoint          | Trigger on created or modified items and files, keep lists and libraries updated                                             |
| Microsoft Forms     | Trigger on new form response, store or route the response                                                                    |
| Document automation | Extract data from documents (such as invoices) with AI and push it into systems                                              |

Classic combined scenario: a Forms response triggers a flow, the flow starts an approval, the approver approves in Teams, and the flow writes the result to SharePoint and emails the requester with Outlook.

## Building blocks: connectors, triggers, actions

| Building block | Definition                                                    | Example                                          |
| -------------- | ------------------------------------------------------------- | ------------------------------------------------ |
| Connector      | Prebuilt wrapper for a service, exposing triggers and actions | SharePoint connector, Outlook connector          |
| Trigger        | The single event that starts a cloud flow                     | "When a new email arrives"                       |
| Action         | A step the flow performs after it starts                      | "Create item," "Send an email," "Post a message" |
| Condition      | Branching logic inside the flow                               | If amount > 1000, require approval               |
| Connection     | The signed-in account a connector uses                        | The flow sends email as the connected account    |

Rules to remember:

- Every cloud flow has exactly one trigger and one or more actions.
- Triggers come from connectors (or a schedule or manual button).
- Standard connectors are included with base licensing; premium connectors (such as SQL Server or HTTP) need premium licensing.
- The on-premises data gateway lets connectors reach on-premises data sources.

## Building flows with AI

### Use AI to create and modify cloud flows

| Step              | What happens                                                            |
| ----------------- | ----------------------------------------------------------------------- |
| Describe the flow | "When a form is submitted, get manager approval, then email the result" |
| Copilot drafts    | Copilot proposes the trigger and actions and builds the flow            |
| Connect           | The maker signs into the connectors the flow needs                      |
| Refine            | Ask Copilot to add, remove, or change steps; or edit manually           |

Copilot can also explain what an existing flow does and answer questions about it, which helps when inheriting flows from others.

### Use AI to create and modify desktop flows

| Capability            | What it does                                                     |
| --------------------- | ---------------------------------------------------------------- |
| Describe and generate | Describe the desktop task and let Copilot draft the desktop flow |
| Recorder plus AI      | Record the UI steps; AI helps turn them into a reliable flow     |
| Modify with prompts   | Ask Copilot to adjust steps in Power Automate for desktop        |

Memory hook: Copilot is the same idea in both flavors - natural language in, draft automation out, maker reviews and refines.

## Common confusions

| Confusion                              | Correct idea                                                                  |
| -------------------------------------- | ----------------------------------------------------------------------------- |
| Cloud flow vs desktop flow             | API/connector automation vs UI recording (RPA) for apps without connectors    |
| Trigger vs action                      | Trigger starts the flow (one per flow); actions are the steps that follow     |
| Automated vs instant vs scheduled      | Event-started vs user-started vs time-started                                 |
| Attended vs unattended desktop flow    | User present at the machine vs fully autonomous run                           |
| Power Automate vs Copilot Studio agent | Flows automate processes in the background; agents converse with people       |
| Connector vs connection                | Connector is the service wrapper; connection is your signed-in account for it |
| Standard vs premium connector          | Included with base licensing vs requires premium licensing                    |

## Exam traps

| Trap                                                       | Why people miss it                                              |
| ---------------------------------------------------------- | --------------------------------------------------------------- |
| Choosing a cloud flow to automate a legacy app with no API | No connector means UI automation: desktop flow                  |
| Calling "when an email arrives" an action                  | Anything that starts the flow is the trigger                    |
| Thinking a flow can have several triggers                  | One trigger per cloud flow; multiple actions are fine           |
| Assuming desktop flows run in the cloud                    | Desktop flows run on a Windows machine                          |
| Forgetting the gateway for on-premises data                | Cloud flows need the on-premises data gateway for local sources |
| Assuming Copilot-built flows need no connections           | Makers still authenticate each connector the flow uses          |

## Mini scenarios

| Scenario                                                                                        | Best answer                        |
| ----------------------------------------------------------------------------------------------- | ---------------------------------- |
| When a customer submits a Microsoft Forms survey, save the response to a SharePoint list.       | Automated cloud flow               |
| Every Friday at 4 PM, email a status summary to the team.                                       | Scheduled cloud flow               |
| A field worker taps a button in a canvas app to log an incident and notify the office.          | Instant cloud flow                 |
| Copy data nightly from an old desktop ERP with no API into a web system, with no user present.  | Unattended desktop flow            |
| Purchases over 5000 need manager sign-off inside Teams before the order is placed.              | Cloud flow with an approval action |
| Extract supplier, date, and total from incoming PDF invoices and write them to Dataverse.       | Document automation                |
| A maker types "when a Dataverse row is added, post to Teams" and wants the flow built for them. | Copilot in Power Automate          |

## Check yourself

1. What is the difference between a cloud flow and a desktop flow?
2. How many triggers can one cloud flow have?
3. Name the three types of cloud flows and what starts each.
4. What is the difference between attended and unattended desktop flows?
5. Which capability extracts data from documents like invoices?
6. What extra component do cloud flows need to reach an on-premises SQL Server?
7. Give two things Copilot can do with an existing cloud flow.
8. In an approval scenario, where can the approver respond?

## Answer guide

1. Cloud flows automate services through connector APIs in the cloud; desktop flows automate application UIs on a Windows machine (RPA).
2. Exactly one.
3. Automated (started by an event), instant (started manually by a user), scheduled (started by a timetable).
4. Attended runs with a user signed in and present; unattended runs without a user.
5. Document automation (AI-powered document processing in Power Automate).
6. The on-premises data gateway.
7. Modify it from natural-language prompts, and explain what the flow does.
8. In Microsoft Teams, Outlook, or the Power Automate Approvals experience.
