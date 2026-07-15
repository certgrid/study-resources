# PL-900 Governance and Security Matrix

One page that sorts out the governance domain: which control does what, at which scope, and which scenario wording points to it. Most wrong answers in the "Manage the Microsoft Power Platform environment" domain come from picking a real control at the wrong layer. Read the master table, then drill the decision table until the mapping is automatic.

## Master table

| Control                     | What it governs                                                        | Scope                                        | Typical exam wording                                             |
| ---------------------------- | ----------------------------------------------------------------------- | --------------------------------------------- | ----------------------------------------------------------------- |
| Environment                 | Where apps, flows, agents, connections, and a Dataverse database live  | Container; one Dataverse database per environment | "Separate dev from prod," "keep data in a region," "isolate a team" |
| Managed Environments        | Extra governance: usage insights, sharing limits, stricter controls    | Per environment, activated by an admin        | "More governance and insights for key environments"               |
| Microsoft Entra ID          | Authentication: who can sign in to the tenant at all                   | Tenant                                        | "Verify the user's identity," "sign-in"                           |
| Security role               | What a user or team can create, read, update, delete in Dataverse      | Environment (Dataverse), down to row level via ownership and business units | "Users should only see/edit certain records"                      |
| Column-level security       | Access to specific sensitive columns                                   | Individual columns via column security profiles | "Hide the salary column from most users"                          |
| DLP policy                  | Which connectors may be used and combined (business / non-business / blocked) | Tenant or selected environments         | "Stop makers mixing business data with personal services"         |
| Solution                    | Packaging apps, flows, tables, and agents for transport                | Travels between environments                  | "Move these components together"                                  |
| Managed vs unmanaged solution | Whether the package is locked (test/prod) or editable (dev)          | Per solution, per environment                 | "Prevent edits in production"                                     |
| Power Platform pipelines    | Guided ALM deployment of solutions dev -> test -> prod                 | Across environments                           | "Promote to production in controlled stages"                      |
| Connector                   | Integration with a service: prebuilt triggers and actions              | Used inside apps and flows; governed by DLP   | "Connect to Outlook / SQL / Salesforce without code"              |
| On-premises data gateway    | Secure bridge from cloud services to on-premises data                  | Installed on a local machine, shared by makers | "Cloud flow must reach a local SQL Server or file share"          |
| Power Platform admin center | Managing environments, capacity, policies, tenant analytics            | Tenant                                        | "Admin reviews usage across the organization"                     |

## Which control answers which scenario

| Scenario says...                                                    | Answer with...                                             |
| -------------------------------------------------------------------- | ----------------------------------------------------------- |
| "Block connector X from being used in this environment"             | DLP policy                                                  |
| "Business data must never flow to personal cloud storage"           | DLP policy (connector group separation)                     |
| "Move the app from dev to prod in a controlled way"                 | Solutions deployed with Power Platform pipelines            |
| "Nobody should be able to edit the solution in production"          | Deploy it as a managed solution                             |
| "A salesperson sees only their own rows"                            | Security role with row-level (user-owned) scope             |
| "Only HR leadership can see the salary column"                      | Column-level security profile                               |
| "Isolate a department's apps and data from everyone else"           | A separate environment                                      |
| "Keep this project's data in a specific geographic region"          | Create the environment in that region                       |
| "Developers need a safe place to test without touching live data"   | Sandbox (or developer) environment                          |
| "Verify who the user is before anything else"                       | Microsoft Entra ID (authentication)                         |
| "Decide what an authenticated user may do with Dataverse data"      | Security role (authorization)                               |
| "A flow must read data from a server inside the company network"    | On-premises data gateway (plus the right connector)         |
| "Admins need tenant-wide usage, capacity, and policy management"    | Power Platform admin center                                 |
| "Turn on extra insights and sharing limits for key environments"    | Managed Environments                                        |
| "Where are Microsoft's privacy and compliance commitments published" | Microsoft Trust Center                                     |

## Common confusions

| Confused pair                 | The difference in one line                                                                        |
| ------------------------------ | --------------------------------------------------------------------------------------------------- |
| DLP policy vs security role   | DLP governs which connectors can be combined; a security role governs what users do with Dataverse data |
| Environment vs solution       | An environment is where things live; a solution is the package that moves things between environments |
| Managed vs unmanaged solution | Managed is locked, for test and production; unmanaged is editable, for development                  |
| Connector vs gateway          | A connector integrates with a service; the gateway is the secure bridge that lets cloud reach on-premises data |
| Entra ID vs security role     | Entra ID authenticates (who you are); the security role authorizes (what you can do in Dataverse)   |
| Column security vs DLP        | Column security hides sensitive columns from users; DLP has nothing to do with hiding data from users |

Memory hook: identity first (Entra ID), then the building (environment), then the badge (security role), then the building rules (DLP), then the moving service (solutions + pipelines).
