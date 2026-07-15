# Lab 11 - Clean Up Resources

Cleanup is a skill the exam rewards indirectly: knowing what bills and what does not is deployment-option knowledge in disguise.

## Time Needed

10 minutes.

## What You Will Learn

- What in your Foundry project can generate cost
- The right deletion order
- How to confirm nothing is left billable

## AI-901 Concepts Covered

| Concept              | Where you see it in the lab                    |
| -------------------- | ---------------------------------------------- |
| Serverless API cost  | Stops when nothing calls it, gone when deleted |
| Managed compute cost | Bills while provisioned, so it must not linger |
| Resource lifecycle   | Deleting the resource group removes everything |

## Steps

### 1. Delete deployments

1. Open **Deployments** in your project.
2. Delete `chat-ai901-lab` and any vision or image models you deployed.
3. Serverless deployments cost nothing while idle, but deleting removes any risk of stray calls.

### 2. Delete the agent and its files

1. In the **Agents** area, delete `study-buddy`.
2. Remove any uploaded knowledge files.

### 3. Delete the project or resource group

- To keep practicing later: keep the project, it is not billable when empty.
- To remove everything: delete the backing resource group (for example `rg-ai901-labs`) in the Azure portal. Deleting a resource group removes all resources inside it.

### 4. Verify

1. Check the deployments list is empty.
2. In the Azure portal, open Cost Management once tomorrow and confirm no new charges.

## Success Criteria

You are done when you can explain:

- Which deployment option would have kept billing if you forgot it
- Why deleting the resource group is the definitive cleanup
- Where you would check for surprise costs
