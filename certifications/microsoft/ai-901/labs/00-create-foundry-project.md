# Lab 00 - Create a Microsoft Foundry Project

Everything in AI-901's biggest domain happens inside a Foundry project. This lab creates one safely, with cost awareness from the start.

## Time Needed

15-20 minutes.

## What You Will Learn

- What Microsoft Foundry is and where it lives
- What a project contains
- How Foundry relates to your Azure subscription and resource group
- Where costs come from before you deploy anything

## AI-901 Concepts Covered

| Concept            | Where you see it in the lab                         |
| ------------------ | --------------------------------------------------- |
| Foundry portal     | You sign in and create the project                  |
| Project            | You create the workspace that will hold deployments |
| Connected resource | The project is backed by an Azure resource          |
| Cost awareness     | You check what is billable before deploying         |

## Before You Start

You need an Azure account. If you do not have one, create a free account first and set a budget alert (the AZ-900 pack has a lab for exactly this). Nothing in this lab itself incurs cost until you deploy a model.

## Steps

### 1. Open the Foundry portal

1. Go to the Microsoft Foundry portal and sign in with your Azure account.
2. Notice the home page: projects, model catalog, and documentation entry points.

### 2. Create a project

1. Select **Create project**.
2. Use a name like:

```text
proj-ai901-labs
```

3. Let the portal create the backing Azure resource, or pick an existing resource group such as `rg-ai901-labs` so cleanup stays easy.
4. Choose a region close to you. Model availability can differ by region; any major region works for these labs.

### 3. Explore the project

Look for these areas in the project navigation:

- Model catalog
- Deployments
- Playgrounds
- Agents
- Connected resources and settings

### 4. Check the cost surface

1. Note that the empty project has no model deployed, so there is no per-token cost yet.
2. Find where deployments will be listed; this is the page you will return to during cleanup.

## Clean Up

Keep the project; every later lab uses it. Lab 11 deletes everything.

## Success Criteria

You are done when you can explain:

- What a Foundry project is and what it will contain
- How the project relates to an Azure resource group
- Where you would look to see what is currently billable
