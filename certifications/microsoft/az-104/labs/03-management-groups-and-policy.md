# Lab 03 - Management Groups and Azure Policy Initiative

Governance at scale means assigning Policy and RBAC once, high in the hierarchy. This lab builds a management group, assigns a policy and an initiative, and reads compliance results.

## Time Needed

30-35 minutes (policy compliance scans can lag; you do not need to wait for them).

## What You Will Learn

- How management groups organize subscriptions
- How to assign a built-in policy (Allowed locations)
- What an initiative is and why definitions get grouped
- How compliance and remediation work

## AZ-104 Concepts Covered

| Concept           | Where you see it in the lab             |
| ----------------- | --------------------------------------- |
| Management groups | You create one and see the hierarchy    |
| Policy definition | You browse built-ins and read the JSON  |
| Policy assignment | You assign Allowed locations at a scope |
| Initiative        | You inspect a built-in initiative       |
| Compliance        | You read the compliance blade           |
| Remediation       | You find where remediation tasks live   |

## Cost Warning

Free. Management groups, policies, and assignments do not bill. Be careful only if you work in a shared/company tenant: scope everything to your own subscription or lab resource group, never the tenant root.

## Steps

### 1. Create a management group

1. Search for **Management groups**.
2. Select **Create**, ID: `mg-az104-lab`, display name: `AZ-104 Lab`.
3. After creation, note the hierarchy: Tenant Root Group > mg-az104-lab.
4. If this is your own tenant, move your subscription under `mg-az104-lab` (Details > Subscriptions > Add). Skip in a shared tenant.

### 2. Read a policy definition

1. Search for **Policy** and open **Definitions**.
2. Filter Category = General, open **Allowed locations**.
3. Read the JSON: find the `parameters` (listOfAllowedLocations), the `policyRule` if/then, and the `deny` effect.

### 3. Assign the policy

1. Select **Assign** on Allowed locations.
2. Scope: your lab resource group `rg-az104-labs` (or the subscription if it is yours alone).
3. Parameter: select ONLY your lab region.
4. Create the assignment.
5. Test it: try to create a resource group tagged resource (e.g. a storage account) in a DIFFERENT region inside the scope. The deployment should fail validation with a policy error. Do not complete the creation.

### 4. Inspect an initiative

1. Back in **Definitions**, filter Definition type = Initiative.
2. Open one (e.g. an Azure Security Benchmark / Microsoft cloud security benchmark initiative) and count how many policy definitions it contains.
3. Key idea: one assignment of an initiative = many policies managed as a unit with one compliance score.

### 5. Review compliance and remediation

1. Open **Policy > Compliance**: your assignment appears with a compliance state (it may show "Not started" at first; scans are periodic).
2. Open **Policy > Remediation**: this is where DeployIfNotExists/Modify policies get remediation tasks for EXISTING resources. Nothing to run here; know the location and the concept.

## Clean Up

1. Delete the policy assignment (Policy > Assignments > select > Delete assignment); leaving it can block later labs that use other regions.
2. Optionally move your subscription back to the Tenant Root Group and delete `mg-az104-lab` (a management group must be empty to delete).

## Success Criteria

You are done when you can explain:

- Why you assign policy at a management group in real environments
- What happens to existing non-compliant resources under a new Deny policy (flagged, not deleted)
- The difference between a definition, an initiative, and an assignment
- Which effects need remediation tasks (DeployIfNotExists, Modify)
