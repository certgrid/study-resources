# AZ-900: Microsoft Azure Fundamentals

AZ-900 is the best first step for learning Microsoft Azure. It does not expect deep hands-on administration, but it does expect you to understand cloud vocabulary, Azure service categories, pricing, governance, identity, security, and the tools Microsoft uses to manage resources.

These notes are built for fast revision and real understanding. Read the domain notes once, do the labs, then use the cheatsheets to remove confusion before taking practice tests.

## Start Here

Pick the path that matches your timeline:

| If you have...      | Use this path                                                                                                                                                        |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1 day               | Read [Exam-Day Review](cheatsheets/az-900-exam-day-review.md), then [Common Confusions](cheatsheets/az-900-common-confusions.md)                                     |
| 3 days              | Read the three study notes, review [Service Picker](cheatsheets/az-900-service-picker.md), then do practice questions                                                |
| 5 days              | Follow the recommended plan below and complete the account, portal, resource group, budget, storage, VM, and cleanup labs                                            |
| No Azure experience | Start with [00 - Create an Azure Free Account Safely](labs/00-create-azure-free-account.md), then [01 - Navigate the Azure Portal](labs/01-navigate-azure-portal.md) |

## What to Memorize vs Understand

| Memorize                                                                  | Understand                                                |
| ------------------------------------------------------------------------- | --------------------------------------------------------- |
| Service model responsibilities: IaaS, PaaS, SaaS                          | Why responsibility decreases from IaaS to SaaS            |
| Azure hierarchy: management group, subscription, resource group, resource | How policy and RBAC inheritance works across scopes       |
| Region, availability zone, region pair                                    | Which failure each one protects against                   |
| Pricing Calculator, TCO Calculator, Cost Management                       | When each cost tool is used in the lifecycle              |
| Policy, RBAC, locks, tags                                                 | Governance vs permission vs protection vs organization    |
| Monitor, Advisor, Service Health, Resource Health                         | Telemetry vs recommendations vs service outage visibility |

## Exam Snapshot

| Item           | Detail                                        |
| -------------- | --------------------------------------------- |
| Exam code      | AZ-900                                        |
| Certification  | Microsoft Azure Fundamentals                  |
| Level          | Beginner                                      |
| Passing score  | 700 out of 1000                               |
| Question style | Conceptual and scenario-based fundamentals    |
| Best for       | Azure beginners, students, and cloud starters |
| Study approach | Learn concepts, compare tools, do small labs  |

## Official Skill Areas

Source: [Official AZ-900 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/az-900). Always confirm the active outline on the official study guide before booking.

Last verified: July 10, 2026

The official study guide lists skills measured as of July 20, 2026. If you are taking the exam before that date, re-check which outline version applies to your exam date, because the earlier outline may still be in effect.

| Domain | Skill area                               | Weight |
| ------ | ---------------------------------------- | ------ |
| 1      | Describe cloud concepts                  | 25-30% |
| 2      | Describe Azure architecture and services | 35-40% |
| 3      | Describe Azure management and governance | 30-35% |

## How to Use This Folder

1. Read the three study notes in order.
2. Open the common-confusions file and check every pair you mix up.
3. Complete the beginner labs so the terms become real in the Azure portal.
4. Review the architecture diagram before practice tests.
5. Use the quick reference on the final day.

## Contents

Every objective in the official outline is mapped to a local file in the [Coverage Matrix](coverage-matrix.md). Use it to confirm nothing in the official study guide is left unread.

### Study Notes

| File                                                                                  | Use it for                                                            |
| ------------------------------------------------------------------------------------- | --------------------------------------------------------------------- |
| [01 - Cloud Concepts](study-notes/01-cloud-concepts.md)                               | Cloud models, benefits, service types, shared responsibility          |
| [02 - Azure Architecture and Services](study-notes/02-azure-architecture-services.md) | Regions, hierarchy, compute, networking, storage, databases, identity |
| [03 - Azure Management and Governance](study-notes/03-management-governance.md)       | Cost, governance, monitoring, security posture, management tools      |

### Cheatsheets

| File                                                                | Use it for                                |
| ------------------------------------------------------------------- | ----------------------------------------- |
| [AZ-900 Quick Reference](cheatsheets/az-900-quick-reference.md)     | Last-day revision                         |
| [AZ-900 Common Confusions](cheatsheets/az-900-common-confusions.md) | Fixing the traps that cause wrong answers |
| [AZ-900 Service Picker](cheatsheets/az-900-service-picker.md)       | Choosing the right Azure service quickly  |
| [AZ-900 Exam-Day Review](cheatsheets/az-900-exam-day-review.md)     | Final 30-minute review before the exam    |
| [AZ-900 Mock Review](cheatsheets/az-900-mock-review.md)             | Final cumulative scenario pass            |
| [Azure CLI Cheatsheet](../azure-cli-cheatsheet.md)                  | Recognizing Cloud Shell, CLI, and management command patterns |

### Hands-On Labs

| Lab                                                                                  | What it teaches                                                      |
| ------------------------------------------------------------------------------------ | -------------------------------------------------------------------- |
| [00 - Create an Azure Free Account Safely](labs/00-create-azure-free-account.md)     | Account setup, subscription, billing awareness, MFA, Cost Management |
| [01 - Navigate the Azure Portal](labs/01-navigate-azure-portal.md)                   | Portal basics, search, common services, Cloud Shell location         |
| [02 - Create a Resource Group](labs/02-create-resource-group.md)                     | Resource groups, region, tags, lifecycle                             |
| [03 - Create a Storage Account](labs/03-create-storage-account.md)                   | Storage accounts, Blob containers, redundancy, tags                  |
| [04 - Create a Virtual Machine](labs/04-create-virtual-machine.md)                   | IaaS, VM size, region, networking, NSG, cleanup                      |
| [05 - Configure a Budget and Cost Alert](labs/05-configure-budget-and-cost-alert.md) | Cost Management, budgets, alerts, spend awareness                    |
| [06 - Apply Tags to Resources](labs/06-apply-tags-to-resources.md)                   | Tags, cost reporting, organization                                   |
| [07 - Create a Basic Virtual Network](labs/07-create-basic-virtual-network.md)       | VNets, subnets, address space, NSG concept                           |
| [08 - Review Microsoft Entra ID](labs/08-review-microsoft-entra-id.md)               | Cloud identity, users, groups, MFA concepts                          |
| [09 - Use Azure Cloud Shell](labs/09-use-azure-cloud-shell.md)                       | Cloud Shell, Azure CLI, PowerShell, automation basics                |
| [10 - Clean Up Resources](labs/10-clean-up-resources.md)                             | Resource lifecycle, cleanup, cost control                            |
| [11 - Review RBAC Access](labs/11-review-rbac-access.md)                             | IAM blade, role assignments, Reader/Contributor/Owner                |
| [12 - Apply a Resource Lock](labs/12-apply-resource-lock.md)                         | Delete locks, ReadOnly locks, accidental deletion protection         |
| [13 - Explore Azure Policy](labs/13-explore-azure-policy.md)                         | Compliance, allowed locations, required tags                         |
| [14 - Review Azure Advisor](labs/14-review-azure-advisor.md)                         | Cost, reliability, security, performance recommendations             |
| [15 - Explore Azure Monitor Alerts](labs/15-explore-azure-monitor-alerts.md)         | Metrics, alerts, action groups, monitoring workflow                  |

### Diagrams

| Diagram                                                        | What it teaches                                                    |
| -------------------------------------------------------------- | ------------------------------------------------------------------ |
| [Azure Core Architecture](diagrams/azure-core-architecture.md) | Management hierarchy, regions/zones, and a basic Azure app pattern |

## What Usually Decides Pass or Fail

Most AZ-900 mistakes come from confusing similar terms:

| If you confuse...                     | Review                                           |
| ------------------------------------- | ------------------------------------------------ |
| Azure Policy and RBAC                 | Governance vs permissions                        |
| Availability zones and region pairs   | Local datacenter resilience vs regional recovery |
| Pricing Calculator and TCO Calculator | Future Azure estimate vs on-premises comparison  |
| Azure Monitor and Azure Advisor       | Telemetry vs recommendations                     |
| IaaS and PaaS                         | Who patches and manages the operating system     |
| Microsoft Entra ID and AD DS          | Cloud identity vs traditional domain services    |

## High-Value Exam Traps

| Trap                                          | Correct thinking                                            |
| --------------------------------------------- | ----------------------------------------------------------- |
| "Need to control who can create resources"    | Use RBAC for who can act. Use Policy for what is allowed.   |
| "Need to prevent accidental deletion"         | Use a resource lock, not RBAC or Policy.                    |
| "Need to estimate planned Azure spend"        | Use Pricing Calculator before deployment.                   |
| "Need to compare datacenter cost with Azure"  | Use TCO Calculator.                                         |
| "Need personalized outage alerts"             | Use Azure Service Health, not the public Azure Status page. |
| "Need private dedicated connectivity"         | Use ExpressRoute, not VPN Gateway.                          |
| "Need object storage for images/logs/backups" | Use Blob Storage, not Azure Files.                          |
| "Need managed file shares"                    | Use Azure Files.                                            |
| "Need to run code when an event happens"      | Use Azure Functions.                                        |
| "Need a web app without OS patching"          | Use Azure App Service.                                      |

## Recommended 5-Day Plan

| Day | Focus                                                    |
| --- | -------------------------------------------------------- |
| 1   | Cloud concepts, service models, shared responsibility    |
| 2   | Azure regions, hierarchy, compute, networking, storage   |
| 3   | Identity, security, governance, cost tools               |
| 4   | Labs plus common confusions                              |
| 5   | Quick reference, practice questions, wrong-answer review |

## Readiness Checklist

Before booking, you should be able to explain these without notes:

- The difference between IaaS, PaaS, and SaaS
- What Microsoft manages vs what the customer manages
- Management groups, subscriptions, resource groups, and resources
- Region vs availability zone vs region pair
- Azure Policy vs RBAC vs resource locks
- Pricing Calculator vs TCO Calculator vs Cost Management
- Azure Monitor vs Advisor vs Service Health
- Blob Storage vs Azure Files vs managed disks

## Score Booster Routine

Use this after each practice test:

1. Write down every wrong answer in one line.
2. Label the reason: vocabulary gap, service confusion, governance confusion, or cost/monitoring confusion.
3. Re-read only the matching section in this folder.
4. Add the confused pair to your own notes.
5. Retake a small focused quiz before doing another full mock.

The goal is not to memorize answers. The goal is to stop repeating the same type of mistake.

## Note on Exam Content

These are original study notes. They do not contain real exam questions or leaked content. Use them to understand the concepts, then practice with scenario-based questions and hands-on tasks.

---

Maintained by the team behind [CertGrid](https://certgrid.app). Free practice is available on CertGrid, but these notes are useful on their own.
