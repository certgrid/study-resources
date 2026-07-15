# Lab 09 - Clean Up Your Environment

Good makers leave environments tidy. Remove everything the labs created, in dependency order, and learn why deletion order matters.

## Time Needed

10-15 minutes.

## What You Will Learn

- How to delete flows, apps, agents, and tables
- Why dependent items must be removed before the table
- What stays (the environment itself) and why that is free
- Trial hygiene for Copilot Studio

## PL-900 Concepts Covered

| Concept               | Where you see it in the lab                              |
| --------------------- | -------------------------------------------------------- |
| Dependencies          | Apps and flows must go before the table they use         |
| Environment lifecycle | The developer environment persists; contents are removed |
| Maker hygiene         | Turning off and deleting unused automation               |

## Steps

### 1. Turn off and delete the flows

1. In Power Automate, open **My flows**.
2. Turn off, then delete the Lab 06 email flow and the Lab 07 approval flow.
3. Why first: flows reference the table; deleting them first avoids dependency errors.

### 2. Delete the apps

1. In the maker portal, open **Apps**.
2. Delete `Equipment Loans App` (canvas) and `Loan Management` (model-driven).

### 3. Delete the agent

1. In Copilot Studio, open your agent's settings and delete it.
2. If you started a trial only for the lab, simply let it expire.

### 4. Delete the custom table

1. In **Tables**, select **Equipment Loan**.
2. Delete it. If Dataverse blocks the deletion, it lists the remaining dependencies - a useful thing to have seen once before the exam.
3. Leave the standard tables (Contact, Account) alone; they are part of Dataverse.

### 5. Remove the test contact

If you added a test row to Contact in Lab 02, delete that row.

### 6. Keep the environment

The developer environment itself costs nothing and is worth keeping for future practice. If you ever want to start fresh, the admin center can delete a developer environment entirely.

## Clean Up

This lab is the cleanup.

## Success Criteria

You are done when you can explain:

- Why flows and apps are deleted before the table they depend on
- What a dependency error in Dataverse means
- What remains in your environment after cleanup
- Why the developer environment can be kept at no cost
