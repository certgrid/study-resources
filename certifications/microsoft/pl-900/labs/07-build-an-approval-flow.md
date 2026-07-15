# Lab 07 - Build an Approval Flow

Approvals are one of the most-named Power Automate use cases on PL-900. Build a flow where a new loan request needs your approval, and respond to it in Teams or Outlook.

## Time Needed

25-30 minutes.

## What You Will Learn

- How the Approvals capability works inside a cloud flow
- How a flow waits for a human decision and then branches
- How approvals surface in Teams, Outlook, and the Approvals center
- How conditions route approved vs rejected outcomes

## PL-900 Concepts Covered

| Concept                     | Where you see it in the lab                     |
| --------------------------- | ----------------------------------------------- |
| Approvals                   | You add a Start and wait for an approval action |
| Condition                   | The flow branches on Approve vs Reject          |
| Teams and Outlook use cases | You respond to the approval where you work      |
| Dataverse action            | The flow updates the row's status               |

## Steps

### 1. Create the flow

1. In Power Automate, select **Create** > **Automated cloud flow**.
2. Trigger: Dataverse **When a row is added** for the **Equipment Loan** table.

### 2. Add the approval

1. Add the action **Start and wait for an approval** (Approvals connector).
2. Approval type: **Approve/Reject - First to respond**.
3. Title: `Equipment loan request`. Assigned to: your own email (you are both requester and approver in a single-user environment).
4. Details: insert the equipment name and due date as dynamic content.

### 3. Branch on the outcome

1. Add a **Condition**: `Outcome` is equal to `Approve`.
2. In the **If yes** branch: add a Dataverse **Update a row** action setting Status to **Checked Out**.
3. In the **If no** branch: add **Send an email (V2)** telling the requester the loan was rejected.

### 4. Test it end to end

1. Save the flow and add a new Equipment Loan row.
2. Respond to the approval wherever you like:

| Place                 | What you see                            |
| --------------------- | --------------------------------------- |
| Microsoft Teams       | Approvals app shows the pending request |
| Outlook               | Actionable approval email               |
| Power Automate portal | Approvals area lists received requests  |

3. Approve it, then confirm the row's status changed to Checked Out.
4. Run it again and reject, then confirm the rejection email.

### 5. Connect it to the exam

This one flow demonstrates four named outline items: approvals, Teams, Outlook, and Dataverse-connected automation. Document automation would be the same pattern with an AI step extracting data from a file first.

## Clean Up

Turn the flow off after testing. Lab 09 deletes it.

## Success Criteria

You are done when you can explain:

- What "start and wait for an approval" does to the flow's execution
- Where an approver can respond
- How a condition routes the two outcomes
- Which PL-900 use cases this lab demonstrated
