# Lab 01 - Explore the Maker Portal and Admin Center

Before building anything, learn where everything lives. This lab is a guided tour of the two portals PL-900 mentions constantly: the maker portal and the Power Platform admin center.

## Time Needed

15-20 minutes.

## What You Will Learn

- What lives in the maker portal (apps, flows, tables, solutions)
- What an environment is and how to see yours
- What the Power Platform admin center shows admins
- Where security and DLP policy settings live conceptually

## PL-900 Concepts Covered

| Concept                     | Where you see it in the lab                           |
| --------------------------- | ----------------------------------------------------- |
| Maker portal                | You tour Apps, Flows, Tables, and Solutions           |
| Environments                | You view your developer environment and its details   |
| Power Platform admin center | You open the admin view of environments               |
| Governance concepts         | You find where DLP policies and analytics are managed |

## Steps

### 1. Tour the maker portal

1. Go to `make.powerapps.com` and confirm your developer environment is selected in the top-right picker.
2. In the left navigation, open each area and note what it holds:

| Area      | What it holds                                     |
| --------- | ------------------------------------------------- |
| Home      | Copilot prompt to start building, recent items    |
| Apps      | Canvas and model-driven apps in this environment  |
| Tables    | Dataverse tables in this environment              |
| Flows     | Cloud flows (links into Power Automate)           |
| Solutions | Packages used to organize and transport your work |

### 2. Look at the environment picker

1. Select the environment name in the top-right.
2. Notice you may see other environments (such as your organization's default environment).
3. Confirm which environment is selected. Everything you build lands in the selected environment.

### 3. Open the Power Platform admin center

1. Go to `admin.powerplatform.microsoft.com`.
2. Select **Environments** and open your developer environment.
3. Review the details: type (developer), region, and Dataverse database.

### 4. Find the governance areas (read-only tour)

In the admin center navigation, locate but do not change:

- **Policies** > Data policies: where DLP policies are created.
- **Analytics** (or Reports): usage analytics for Dataverse, Power Apps, and Power Automate.
- **Security**: roles and access management areas.

### 5. Connect it to the exam

| If the exam asks...                          | You now know                      |
| -------------------------------------------- | --------------------------------- |
| Where do makers build apps and tables?       | Maker portal (make.powerapps.com) |
| Where do admins manage environments and DLP? | Power Platform admin center       |
| What contains apps, flows, and a database?   | An environment                    |

## Clean Up

Nothing was created. Sign out of the admin center if you are on a shared machine.

## Success Criteria

You are done when you can explain:

- The difference between the maker portal and the admin center
- What an environment contains
- Where DLP policies are created
- Where an admin would look for usage analytics
