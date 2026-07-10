# AZ-900: Microsoft Azure Fundamentals

AZ-900 is the best first step for learning Microsoft Azure. It does not expect deep hands-on administration, but it does expect you to understand cloud vocabulary, Azure service categories, pricing, governance, identity, security, and the tools Microsoft uses to manage resources.

These notes are built for fast revision and real understanding. Read the domain notes once, do the labs, then use the cheatsheets to remove confusion before taking practice tests.

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

| Domain | Skill area                               | Weight |
| ------ | ---------------------------------------- | ------ |
| 1      | Describe cloud concepts                  | 25-30% |
| 2      | Describe Azure architecture and services | 35-40% |
| 3      | Describe Azure management and governance | 30-35% |

## How to Use This Folder

1. Read the three study notes in order.
2. Open the common-confusions file and check every pair you mix up.
3. Complete the two small labs so the terms become real.
4. Review the architecture diagram before practice tests.
5. Use the quick reference on the final day.

## Contents

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

### Hands-On Labs

| Lab                                                | What it teaches                                                      |
| -------------------------------------------------- | -------------------------------------------------------------------- |
| [Storage Account Lab](labs/storage-account-lab.md) | Resource groups, storage accounts, Blob containers, redundancy, tags |
| [Virtual Machine Basic Lab](labs/vm-basic-lab.md)  | IaaS, VM size, region, networking, NSG, cleanup                      |

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

## Note on Exam Content

These are original study notes. They do not contain real exam questions or leaked content. Use them to understand the concepts, then practice with scenario-based questions and hands-on tasks.

---

Maintained by the team behind [CertGrid](https://certgrid.app). Free practice is available on CertGrid, but these notes are useful on their own.
