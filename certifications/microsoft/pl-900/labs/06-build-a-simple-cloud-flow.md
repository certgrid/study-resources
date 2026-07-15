# Lab 06 - Build a Simple Cloud Flow

Automate your first process: when a new Equipment Loan row is added, send yourself an email. One trigger, one action - the pattern behind almost every cloud flow.

## Time Needed

20-25 minutes.

## What You Will Learn

- The difference between a trigger and an action, hands-on
- How connectors and connections work
- How to test a flow and read its run history
- Where Copilot can build the flow for you

## PL-900 Concepts Covered

| Concept              | Where you see it in the lab                   |
| -------------------- | --------------------------------------------- |
| Automated cloud flow | The flow starts on a Dataverse event          |
| Trigger              | "When a row is added" starts the flow         |
| Action               | "Send an email" is performed by the flow      |
| Connections          | You authenticate the connectors the flow uses |
| Run history          | You verify success and inspect a run          |

## Steps

### 1. Create the flow (Copilot option)

1. Go to `make.powerautomate.com` and check your developer environment is selected.
2. In the Copilot box on the home page, describe the flow:

```text
When a row is added to the Equipment Loan table in Dataverse,
send me an email with the equipment name.
```

3. Review the suggested trigger and action, then continue.

### 2. Or create it manually

1. Select **Create** > **Automated cloud flow**.
2. Trigger: search Dataverse and pick **When a row is added, modified or deleted**; set change type to **Added** and table to **Equipment Loan**.
3. Action: add **Send an email (V2)** (Office 365 Outlook connector), to yourself, with the equipment name inserted as dynamic content in the body.

### 3. Set up connections

When prompted, sign in for the Dataverse and Outlook connectors. Note for the exam: the connector is the service wrapper; your signed-in account is the connection.

### 4. Test the flow

1. Save the flow, then add a new Equipment Loan row (use the canvas app from Lab 04 or the table editor).
2. Wait for the run, then check your inbox.

### 5. Read the run history

1. Open the flow's detail page.
2. Check **28-day run history**: find your run, open it, and see the trigger output and action output step by step. This is where makers debug failures.

### 6. Optional: ask Copilot to modify it

Try: "Only send the email when the status is Requested." Notice Copilot adds a condition - the branching building block.

## Clean Up

Turn the flow off if you do not want emails while doing other labs. Lab 09 deletes it.

## Success Criteria

You are done when you can explain:

- Which part of your flow is the trigger and which is the action
- Why a flow has exactly one trigger
- What a connection is compared to a connector
- Where to look when a flow fails
