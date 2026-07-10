# Lab 11 - Review RBAC Access

Goal: understand how Azure role-based access control decides who can manage resources.

This lab is mostly review-only. You do not need to grant access to another person to learn the concept.

## What you learn

- Where role assignments live in the portal
- The difference between Reader, Contributor, Owner, and User Access Administrator
- Why RBAC answers "who can do this?"
- How scope affects permissions

## Steps

1. Open the Azure portal.
2. Open the resource group you created for AZ-900 labs.
3. Select **Access control (IAM)**.
4. Open **Role assignments**.
5. Review the users, groups, or service principals that already have access.
6. Select **Roles** and search for these built-in roles:
   - Reader
   - Contributor
   - Owner
   - User Access Administrator
7. Read the description of each role.
8. Do not add a role assignment unless you are intentionally testing with a separate account.

## Scope checkpoint

RBAC can be assigned at different scopes:

| Scope            | Example                                    |
| ---------------- | ------------------------------------------ |
| Management group | Broad governance across many subscriptions |
| Subscription     | Access to all resources in a subscription  |
| Resource group   | Access to resources inside one group       |
| Resource         | Access to one specific resource            |

## Exam memory

| If the question asks...                         | Think...                  |
| ----------------------------------------------- | ------------------------- |
| Who can view resources?                         | RBAC Reader               |
| Who can manage resources but not assign access? | RBAC Contributor          |
| Who can manage resources and access?            | RBAC Owner                |
| Who can manage access only?                     | User Access Administrator |

## Cleanup

No cleanup is required if you only reviewed settings.
