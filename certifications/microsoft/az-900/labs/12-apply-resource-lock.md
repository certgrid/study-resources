# Lab 12 - Apply a Resource Lock

Goal: understand how resource locks protect important resources from accidental deletion or modification.

Use a test resource group only. Do not apply locks to production resources unless you know the operational impact.

## What you learn

- Difference between Delete and ReadOnly locks
- Why locks are not the same as RBAC
- How locks can protect a resource group

## Steps

1. Open the Azure portal.
2. Open your AZ-900 lab resource group.
3. Select **Locks**.
4. Select **Add**.
5. Enter a name such as `protect-lab-rg`.
6. Choose **Delete** as the lock type.
7. Add a note such as `AZ-900 learning lock`.
8. Save the lock.
9. Review how the lock appears in the list.
10. Remove the lock after you understand the behavior.

## Lock types

| Lock     | What it does                                 |
| -------- | -------------------------------------------- |
| Delete   | Users can read and modify, but cannot delete |
| ReadOnly | Users can read, but cannot update or delete  |

## Exam memory

If the scenario says "prevent accidental deletion", choose a resource lock.

Do not choose:

- Tags: tags organize resources.
- RBAC: RBAC grants permissions.
- Azure Policy: Policy enforces configuration rules.

## Cleanup

Remove the lock before deleting the lab resource group.
