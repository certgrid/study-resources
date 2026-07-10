# Lab 02 - Explore Built-in Roles and Build a Custom Role

RBAC questions decide several marks on every AZ-104 sitting. This lab assigns built-in roles at different scopes, checks effective access, and dissects a role definition so custom roles stop being abstract.

## Time Needed

25-30 minutes.

## What You Will Learn

- How role assignments combine principal + role + scope
- How assignments inherit from resource group to resources
- How to read Actions, NotActions, and AssignableScopes in a role definition
- How to check what access a user actually has

## AZ-104 Concepts Covered

| Concept              | Where you see it in the lab                 |
| -------------------- | ------------------------------------------- |
| Built-in roles       | You assign Reader and Contributor           |
| Scope                | You assign at resource group level          |
| Inheritance          | You verify access flows to resources inside |
| Role definition JSON | You read Actions/NotActions                 |
| Custom roles         | You clone a role and trim its permissions   |
| Check access         | You interpret an access assignment          |

## Cost Warning

Free. Role assignments and definitions do not bill.

## Steps

### 1. Assign built-in roles

1. Open **rg-az104-labs** and select **Access control (IAM)**.
2. Select **Add > Add role assignment**.
3. Assign **Reader** to the group `grp-az104-viewers`.
4. Repeat and assign **Virtual Machine Contributor** to `grp-az104-admins`.
5. On the **Role assignments** tab, note the Scope column: this resource group.

### 2. Check effective access

1. Still in IAM, open **Check access**.
2. Search for `Lab User1` and review the result: membership in `grp-az104-admins` grants Virtual Machine Contributor here.
3. Question to answer for yourself: could Lab User1 create a VNet in this resource group? (No: Virtual Machine Contributor manages VMs, not networks.)

### 3. Read a role definition

1. In IAM, open the **Roles** tab, find **Virtual Machine Contributor**, then **View** its definition (JSON view).
2. Identify the parts:

| Field            | What it means                                                |
| ---------------- | ------------------------------------------------------------ |
| Actions          | Allowed operations, e.g. Microsoft.Compute/virtualMachines/* |
| NotActions       | Subtractions from Actions, not explicit denies               |
| AssignableScopes | Where the role can be assigned                               |

3. Note the wildcard pattern: `Microsoft.Compute/*` covers all compute operations.

### 4. Clone into a custom role

1. On the Roles tab, select **Virtual Machine Contributor > Clone** (or Add > Add custom role at subscription IAM).
2. Name it `Custom VM Operator (lab)`.
3. On Permissions, remove broad permissions and keep only start/restart/deallocate style actions, for example:

```text
Microsoft.Compute/virtualMachines/read
Microsoft.Compute/virtualMachines/start/action
Microsoft.Compute/virtualMachines/restart/action
Microsoft.Compute/virtualMachines/deallocate/action
```

4. Review the JSON tab: this is exactly what New-AzRoleDefinition / az role definition create would take as input.
5. Create it (or cancel at Review if you do not want it saved; reading the JSON is the learning goal).

### 5. CLI recognition

Run in Cloud Shell to see the command shapes:

```bash
az role definition list --name "Reader" --output json
az role assignment list --resource-group rg-az104-labs --output table
```

## Clean Up

Remove the two role assignments from the resource group IAM if you created them for the lab only, and delete `Custom VM Operator (lab)` if you saved it (IAM > Roles > filter CustomRole). Assignments are free, but stale access is bad hygiene.

## Success Criteria

You are done when you can explain:

- The three parts of a role assignment
- Why NotActions is not a deny (it just subtracts from Actions)
- When you need a custom role instead of a built-in one
- Which roles can create role assignments (Owner, User Access Administrator)
