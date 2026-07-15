# Lab 09 - Clean Up Your Learning Environment

Cleanup is a skill the exam rewards indirectly: knowing what creates cost and what holds access is exactly the shared responsibility and least privilege mindset. This lab removes everything the series created.

## Time Needed

10-15 minutes.

## What You Will Learn

- Which lab artifacts can create cost (Sentinel workspace)
- Which artifacts hold access (users, groups)
- How to verify a tenant is back to a clean state

## SC-900 Concepts Covered

| Concept            | Where you see it in the lab                                  |
| ------------------ | ------------------------------------------------------------ |
| Cost awareness     | Deleting the Sentinel resource group stops ingestion billing |
| Identity lifecycle | Removing the lab user mirrors the "leaver" process           |
| Least privilege    | Stale accounts and groups are access liabilities             |
| Auditing           | You review sign-in logs to see your own lab activity         |

## Steps

### 1. Delete Azure resources (cost)

1. In the Azure portal, open **Resource groups**.
2. If you created **rg-sc900-sentinel** in Lab 05, delete it. This removes Microsoft Sentinel and its Log Analytics workspace and stops any ingestion charges.
3. Check for any other resource groups you created and delete them.
4. Open **Cost Management** and confirm no unexpected charges are accruing.

### 2. Remove lab identities (access)

1. In the Microsoft Entra admin center, open **Identity** > **Groups**, select **sc900-lab-group**, and delete it.
2. Open **Users**, select **Lab User1**, and delete the user.
3. If you invited any guests during exploration, remove them too.

### 3. Verify no policies were left behind

1. Open **Protection** > **Conditional Access** and confirm the policy list matches what existed before Lab 03 (nothing new enabled).
2. In the Purview portal, confirm no DLP or retention policies were actually created (wizards were cancelled).

### 4. Review your own audit trail (bonus concept)

1. In the Entra admin center, open **Identity** > **Monitoring & health** > **Sign-in logs**.
2. Find your own sign-ins from the labs. This is the "auditing" pillar of identity infrastructure in action.

### 5. Decide the tenant's future

| If you...                         | Do this                                                                         |
| --------------------------------- | ------------------------------------------------------------------------------- |
| Plan more study                   | Keep the tenant; it costs nothing while idle                                    |
| Used a time-limited M365/E5 trial | Let it expire; do not attach payment methods                                    |
| Are fully done                    | Consider closing the trial subscription per Microsoft's account closure process |

## Clean Up

This lab IS the cleanup. Nothing further.

## Success Criteria

You are done when you can explain:

- Which single deletion stopped potential Sentinel costs and why
- Why deleting stale users and groups matters for security
- Where you can see a record of everything you did (sign-in and audit logs)
- What remains in the tenant and confirms it is cost-free
