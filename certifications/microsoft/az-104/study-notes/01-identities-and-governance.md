# 01 - Manage Azure Identities and Governance

This domain is worth 20-25% of the exam. It covers Microsoft Entra users and groups, access to Azure resources through RBAC, and subscription governance with Policy, locks, tags, budgets, and management groups. Expect scenario questions that test whether you can pick the right control (role, policy, lock, tag) and the right scope.

## Mental model

Two separate permission worlds exist and the exam loves to mix them: Microsoft Entra ID controls the directory (users, groups, licenses), while Azure RBAC controls resources (subscriptions, resource groups, VMs). Governance tools (Policy, locks, tags, budgets) sit on top of the resource hierarchy and flow downward.

| Scenario keyword                         | Likely concept                       |
| ---------------------------------------- | ------------------------------------ |
| "Invite a partner or consultant"         | Guest user (B2B collaboration)       |
| "Users reset their own passwords"        | Self-service password reset (SSPR)   |
| "Membership updates automatically"       | Dynamic group                        |
| "Who can do what on a resource"          | Azure RBAC role assignment           |
| "Grant access with least privilege"      | Built-in role at the narrowest scope |
| "Enforce allowed regions or SKUs"        | Azure Policy                         |
| "Prevent deletion of a resource"         | Resource lock (CanNotDelete)         |
| "Report cost by department"              | Tags                                 |
| "Apply governance to many subscriptions" | Management group                     |
| "Notify when spend passes a threshold"   | Budget with cost alert               |
| "Reduce cost with recommendations"       | Azure Advisor                        |

## Microsoft Entra users and groups

### Users

| User type   | What it is                                                       | Typical exam wording                             |
| ----------- | ---------------------------------------------------------------- | ------------------------------------------------ |
| Member user | Account created in your tenant or synced from AD DS              | "An employee needs an account"                   |
| Guest user  | External identity invited via B2B; signs in with own credentials | "A consultant from another company needs access" |

Key facts:

- Users are created in the Microsoft Entra admin center, portal, PowerShell, CLI, or bulk-created via CSV upload.
- Bulk operations (create, invite, delete) use CSV templates.
- Guest users can be assigned Azure RBAC roles like any member user.
- User properties (department, usage location, job title) matter: usage location is required before assigning most licenses.

### Groups

| Group type          | Purpose                                    | Notes                                               |
| ------------------- | ------------------------------------------ | --------------------------------------------------- |
| Security group      | Grant access to resources and apps         | Members: users, devices, service principals, groups |
| Microsoft 365 group | Collaboration (mailbox, SharePoint, Teams) | Members: users only                                 |

| Membership type | How members are managed                         | Exam trigger                                            |
| --------------- | ----------------------------------------------- | ------------------------------------------------------- |
| Assigned        | Admin adds and removes members manually         | "Manually manage membership"                            |
| Dynamic user    | Rule based on user attributes (e.g. department) | "Automatically add users where department equals Sales" |
| Dynamic device  | Rule based on device attributes                 | "Automatically include all Windows devices"             |

Key facts:

- Dynamic membership requires Microsoft Entra ID P1 licensing.
- You cannot convert a Microsoft 365 group to a security group.
- Group-based licensing assigns licenses to all members of a group automatically.

### Licenses

- Licenses are managed in Microsoft Entra ID (per user or per group).
- A user must have a usage location set before a license can be assigned.
- Group-based licensing: add the user to the licensed group; removal removes the license.

### Self-service password reset (SSPR)

| Setting                | Meaning                                                          |
| ---------------------- | ---------------------------------------------------------------- |
| Enabled for            | None, Selected (specific group), or All                          |
| Authentication methods | Email, mobile phone, office phone, security questions, app codes |
| Number of methods      | How many methods a user must register and use to reset           |

Key facts:

- SSPR is enabled per group, not per individual user (use "Selected" with a group).
- Administrators always have a stricter, separate reset policy.
- Registration can be enforced at next sign-in.

## Manage access to Azure resources (RBAC)

### The four roles you must know cold

| Role                      | Can manage resources | Can assign roles | Typical use                                    |
| ------------------------- | -------------------- | ---------------- | ---------------------------------------------- |
| Owner                     | Yes                  | Yes              | Full control including access management       |
| Contributor               | Yes                  | No               | Create and manage everything, no access grants |
| Reader                    | View only            | No               | Auditors, viewers                              |
| User Access Administrator | No                   | Yes              | Manage access without touching resources       |

Other built-in roles worth recognizing:

| Role                          | Scope of power                                     |
| ----------------------------- | -------------------------------------------------- |
| Virtual Machine Contributor   | Manage VMs, but not the VNet or storage they use   |
| Network Contributor           | Manage networking resources                        |
| Storage Blob Data Contributor | Read/write/delete blob data (data plane, not keys) |
| Billing Reader                | View billing and cost data                         |

### Scopes and inheritance

```text
Management group
  Subscription
    Resource group
      Resource
```

- A role assigned at a scope is inherited by every child scope.
- Assign at the narrowest scope that meets the requirement (least privilege).
- An assignment = security principal + role definition + scope.
- Deny assignments (rare, created by Azure, e.g. Blueprints/managed apps) override role assignments.

### Interpreting access

| Question pattern                                        | How to answer it                                                   |
| ------------------------------------------------------- | ------------------------------------------------------------------ |
| "User has Reader on subscription, Contributor on RG"    | Effective access is the union: Contributor inside that RG          |
| "Can a Contributor at subscription scope assign roles?" | No; role assignment needs Owner or User Access Administrator       |
| "Where do I check why a user has access?"               | Access control (IAM) blade, Role assignments and Check access tabs |

### Azure RBAC vs Microsoft Entra roles

| Aspect       | Azure RBAC                                                                             | Microsoft Entra roles                        |
| ------------ | -------------------------------------------------------------------------------------- | -------------------------------------------- |
| Controls     | Azure resources (VMs, storage, VNets)                                                  | Directory objects (users, groups, licenses)  |
| Example role | Contributor, Reader                                                                    | Global Administrator, User Administrator     |
| Scope        | Management group to resource                                                           | Tenant (or administrative unit)              |
| Crossover    | Global Administrator can elevate to get User Access Administrator on all subscriptions | Not automatic; must be elevated deliberately |

## Manage subscriptions and governance

### Azure Policy

| Concept             | Meaning                                                              |
| ------------------- | -------------------------------------------------------------------- |
| Policy definition   | A rule: allowed locations, allowed SKUs, require a tag, etc.         |
| Initiative          | A group of policy definitions assigned together                      |
| Assignment          | A definition or initiative applied at a scope                        |
| Exclusion/exemption | A child scope carved out of an assignment                            |
| Effects             | Deny, Audit, Append, Modify, DeployIfNotExists, AuditIfNotExists     |
| Remediation task    | Applies DeployIfNotExists/Modify to existing non-compliant resources |

Key facts:

- Policy evaluates what is created or changed; RBAC evaluates who acts. Both must allow an action.
- Existing resources that violate a new Deny policy are marked non-compliant, not deleted.
- Assign at a management group to cover many subscriptions at once.

### Resource locks

| Lock type    | Effect                                       |
| ------------ | -------------------------------------------- |
| CanNotDelete | Read and modify allowed; delete blocked      |
| ReadOnly     | Only read allowed; modify and delete blocked |

Key facts:

- Locks apply to the control plane, not data (a ReadOnly lock on a storage account does not stop blob reads, but it can block key listing operations).
- Locks are inherited by child resources.
- Owner or User Access Administrator can manage locks (Microsoft.Authorization/locks actions).

### Tags

- Name/value pairs for organization and cost reporting.
- Not inherited by default from resource group to resources (a policy with Modify effect can enforce inheritance).
- Maximum 50 tag name/value pairs per resource.
- Tags on a resource group do not automatically appear on billing for resources inside it; tag the resources (or enforce with policy).

### Resource groups and subscriptions

| Task                                  | Key rule                                                                               |
| ------------------------------------- | -------------------------------------------------------------------------------------- |
| Move resources between RGs            | Supported for most types; source and target are locked during the move                 |
| Move resources between subscriptions  | Supported for many types; both subscriptions must be in the same tenant                |
| Delete a resource group               | Deletes everything inside it                                                           |
| Resource group region                 | Stores metadata only; resources inside can live in other regions                       |
| Change subscription offer or transfer | Billing ownership can be transferred; subscriptions can move between management groups |

### Cost management

| Tool                 | What it does                                                               |
| -------------------- | -------------------------------------------------------------------------- |
| Budgets              | Set a spend threshold per scope; trigger alerts (and action groups)        |
| Cost alerts          | Notify when actual or forecasted spend crosses a budget threshold          |
| Cost analysis        | Explore actual spend by service, RG, tag, region                           |
| Azure Advisor (cost) | Recommendations: right-size or shut down underused VMs, reserved instances |

Key fact: budgets alert, they do not stop spending by themselves.

### Management groups

- Organize subscriptions into a hierarchy for policy and RBAC inheritance.
- Up to six levels of depth (not counting root and subscription level).
- A management group can contain management groups and subscriptions.
- Each subscription has exactly one parent management group.
- The tenant root group sits above everything; assignments there hit every subscription.

## Limits and numbers to memorize

| Item                                      | Limit                                                       |
| ----------------------------------------- | ----------------------------------------------------------- |
| Management group depth                    | 6 levels (excluding root and subscription)                  |
| Management groups per tenant              | 10,000                                                      |
| Role assignments per subscription         | 4,000                                                       |
| Custom RBAC roles per tenant              | 5,000                                                       |
| Tags per resource or resource group       | 50 name/value pairs                                         |
| Tag name length / value length            | 512 characters / 256 characters                             |
| RBAC scope levels                         | 4: management group, subscription, resource group, resource |
| Subscriptions per management group parent | 1 parent per subscription                                   |

## CLI and PowerShell recognition

You do not need to write these from memory, but you must recognize which tool and command family does what.

| Task                      | Azure CLI                          | PowerShell               |
| ------------------------- | ---------------------------------- | ------------------------ |
| Create a user             | az ad user create                  | New-AzADUser             |
| Create a group            | az ad group create                 | New-AzADGroup            |
| Add group member          | az ad group member add             | Add-AzADGroupMember      |
| Assign an RBAC role       | az role assignment create          | New-AzRoleAssignment     |
| List role assignments     | az role assignment list            | Get-AzRoleAssignment     |
| Create a custom role      | az role definition create          | New-AzRoleDefinition     |
| Assign a policy           | az policy assignment create        | New-AzPolicyAssignment   |
| Create a resource lock    | az lock create                     | New-AzResourceLock       |
| Apply tags                | az tag create / az resource tag    | New-AzTag / Update-AzTag |
| Create a resource group   | az group create                    | New-AzResourceGroup      |
| Move a resource           | az resource move                   | Move-AzResource          |
| Create a management group | az account management-group create | New-AzManagementGroup    |

Recognition rules: Azure CLI uses lowercase az noun verb; Az PowerShell uses Verb-AzNoun. "ad" in the CLI or "AzAD" in PowerShell means a directory (Entra) object, not an Azure resource.

## Common confusions

| Confusion                             | Correct idea                                                                                      |
| ------------------------------------- | ------------------------------------------------------------------------------------------------- |
| Entra roles vs Azure RBAC roles       | Directory administration vs resource permissions; Global Administrator is not automatically Owner |
| Contributor vs Owner                  | Contributor does everything except manage access and locks assignments                            |
| Security group vs Microsoft 365 group | Access control vs collaboration workloads                                                         |
| Assigned vs dynamic membership        | Manual vs attribute-rule based (needs P1)                                                         |
| Policy non-compliance vs deny         | Audit marks it; Deny blocks new/changed deployments; existing resources are not removed           |
| CanNotDelete vs ReadOnly lock         | Block delete only vs block delete and changes                                                     |
| Tags vs Policy                        | Tags organize; Policy can require or inherit tags                                                 |
| Budget vs Policy for cost control     | Budgets alert on spend; Policy restricts what can be deployed (e.g. allowed VM SKUs)              |

## Exam traps

| Trap                                                       | Why people miss it                                            |
| ---------------------------------------------------------- | ------------------------------------------------------------- |
| Giving Contributor when the task includes "assign access"  | Only Owner or User Access Administrator can assign roles      |
| Assigning a license without setting usage location         | License assignment fails until usage location is set          |
| Expecting a guest user to be blocked from RBAC             | Guests can receive role assignments like members              |
| Assuming tags flow from resource group to resources        | They do not by default; use a Modify policy to inherit        |
| Assuming a new Deny policy deletes existing resources      | Existing resources become non-compliant only                  |
| Forgetting locks are inherited                             | A ReadOnly lock on an RG freezes changes to everything inside |
| Moving resources across subscriptions in different tenants | Cross-tenant moves are not supported this way                 |
| Assigning SSPR to one user directly                        | SSPR "Selected" targets a group                               |

## Mini scenarios

| Scenario                                                                                               | Best answer                                             |
| ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------- |
| A helpdesk team must manage all VMs in one resource group but must not change networking.              | Virtual Machine Contributor at the resource group scope |
| An auditor needs to view every resource in every subscription.                                         | Reader at the management group scope                    |
| Marketing users should be added to a group automatically when their department attribute is Marketing. | Dynamic user group (requires Entra ID P1)               |
| A consultant with a Gmail account needs Contributor on one resource group.                             | Invite as guest user, assign Contributor at RG scope    |
| All new resources in three subscriptions must be created only in West Europe.                          | Allowed locations policy assigned at a management group |
| A production database resource must never be deleted, but admins still change settings.                | CanNotDelete lock                                       |
| Finance wants a monthly email when subscription spend is forecasted to exceed 5,000.                   | Budget with a forecasted cost alert                     |
| A manager should grant access to resources without being able to modify them.                          | User Access Administrator                               |
| 200 new employees must be created as users from an HR spreadsheet.                                     | Bulk create users with a CSV in Microsoft Entra ID      |
| Every resource in the Finance subscription must carry a CostCenter tag copied from its resource group. | Policy with Modify effect and a remediation task        |

## Check yourself

1. Which built-in role can create resources but cannot grant other users access?
2. What must be set on a user before you can assign a Microsoft 365 license?
3. A user has Reader at subscription scope and Contributor on resource group RG1. What can they do inside RG1?
4. Which policy effect automatically fixes non-compliant existing resources when a remediation task runs?
5. What is the difference between a CanNotDelete lock and a ReadOnly lock?
6. How many levels of management group depth does Azure support below the root?
7. Can you convert a Microsoft 365 group into a security group?
8. A budget alert fired at 100% of the budget. Does Azure stop new deployments?
9. Which command family creates a role assignment: az role assignment create or az ad user create?
10. What licensing level do dynamic groups require?

## Answer guide

1. Contributor.
2. Usage location.
3. Everything Contributor allows, because the more permissive assignment applies in that scope; permissions are additive.
4. DeployIfNotExists (or Modify) via a remediation task.
5. CanNotDelete blocks only deletion; ReadOnly blocks both changes and deletion.
6. Six levels (not counting root and subscriptions).
7. No; group types cannot be converted after creation.
8. No; budgets alert but do not block spending or deployments.
9. az role assignment create; az ad commands manage directory objects.
10. Microsoft Entra ID P1 (or higher).
