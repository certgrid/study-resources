# Lab 13 - Explore Azure Policy

Goal: understand how Azure Policy enforces standards such as allowed regions, required tags, and approved resource types.

This lab is review-first. You can explore built-in policies without assigning them.

## What you learn

- Azure Policy controls what is allowed
- Policy can audit, deny, or modify resource deployments
- Policy is different from RBAC

## Steps

1. Open the Azure portal.
2. Search for **Policy**.
3. Open **Definitions**.
4. Search for these examples:
   - Allowed locations
   - Require a tag on resources
   - Allowed virtual machine size SKUs
5. Open each definition and read what it checks.
6. Open **Compliance** to see how policy compliance is reported.
7. Do not assign policies in a personal account unless you understand the effect.

## Policy decision table

| Requirement                                 | Policy example                    |
| ------------------------------------------- | --------------------------------- |
| Only allow resources in approved regions    | Allowed locations                 |
| Require every resource to have an Owner tag | Require a tag on resources        |
| Restrict VM sizes                           | Allowed virtual machine size SKUs |
| Audit public network access                 | Audit policy definitions          |

## Exam memory

Azure Policy answers: "What is allowed to be deployed or configured?"

RBAC answers: "Who has permission to perform an action?"

## Cleanup

No cleanup is required if you only reviewed built-in policy definitions.
