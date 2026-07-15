# 02 - Manage the Microsoft Power Platform Environment

This domain is worth 20-25% of the exam. It covers two big areas: Microsoft Dataverse (the data platform) and Power Platform administration and governance (environments, security, privacy, monitoring, and application lifecycle management). Expect vocabulary questions and "which feature controls this" scenarios.

## Mental model

Picture an office building. The environment is the building: everything inside it (apps, flows, agents, data) lives together and is separated from other buildings. Dataverse is the filing system inside the building: tables are drawers, columns are the fields on each record card, relationships are cross-references between drawers. Security roles are badges that decide which doors a person can open, and DLP policies are building rules about which services are allowed to be used together. Pipelines are the moving service that transports finished work from the development building to the production building.

| Scenario keyword                                     | Likely concept                                     |
| ---------------------------------------------------- | -------------------------------------------------- |
| Separate development from production                 | Environments                                       |
| Store customers, orders, products with relationships | Dataverse tables and relationships                 |
| Different layouts for entering vs listing records    | Forms vs views                                     |
| Enforce a rule like "discount cannot exceed 10%"     | Dataverse business logic                           |
| Formula language used across Power Platform          | Power Fx                                           |
| Control who can read or edit rows                    | Security roles                                     |
| Stop makers mixing business and personal connectors  | Data loss prevention (DLP) policy                  |
| Meet GDPR or accessibility requirements              | Microsoft compliance and accessibility commitments |
| See who is using which apps                          | Admin center analytics and monitoring              |
| Move a solution from dev to test to prod             | ALM with Power Platform pipelines                  |

## Describe Microsoft Dataverse

Dataverse is a cloud data platform that stores business data in tables. It is more than a database: it includes security, business logic, forms, views, and auditing on top of the data.

### Dataverse vs traditional databases

| Aspect            | Traditional database (such as SQL Server) | Microsoft Dataverse                                     |
| ----------------- | ----------------------------------------- | ------------------------------------------------------- |
| Setup             | Install, configure, and maintain servers  | Software as a service, provisioned per environment      |
| Security          | Managed separately at database level      | Built-in role-based security to row and column level    |
| Business logic    | Written in code or stored procedures      | Business rules, Power Fx, and low-code options built in |
| UI                | None; apps built separately               | Forms and views included with every table               |
| Data types        | Basic column types                        | Rich types: choices, lookups, files, images, currency   |
| Who works with it | Database administrators and developers    | Makers through the maker portal, plus developers        |

Exam tip: if a question contrasts "just storing data" with "storing data plus security, logic, and UI," the second one is Dataverse.

### Tables, columns, and relationships

| Building block | Meaning                                       | Example                            |
| -------------- | --------------------------------------------- | ---------------------------------- |
| Table          | A collection of records for one kind of thing | Customer, Order, Product           |
| Column         | One field stored for each record in a table   | Customer Name, Email, Credit Limit |
| Row (record)   | One entry in a table                          | The customer "Contoso Ltd"         |
| Relationship   | A defined link between tables                 | One Customer has many Orders       |

Relationship types to recognize:

| Relationship type | Meaning                                        | Example                            |
| ----------------- | ---------------------------------------------- | ---------------------------------- |
| One-to-many       | One parent row relates to many child rows      | One Customer, many Orders          |
| Many-to-one       | The same link seen from the child side         | Each Order belongs to one Customer |
| Many-to-many      | Rows on both sides relate to many on the other | Products and Suppliers             |

Dataverse ships with standard tables (such as Account and Contact) and lets you create custom tables. Lookup columns are how one-to-many relationships appear on a form.

### Table forms and views

| Element | What it is                                       | When users see it              |
| ------- | ------------------------------------------------ | ------------------------------ |
| Form    | A layout for viewing and editing a single record | Opening or creating one record |
| View    | A filtered, sorted list of multiple records      | Browsing a grid of records     |

| Common form types | Purpose                                               |
| ----------------- | ----------------------------------------------------- |
| Main form         | Full create/edit experience for a record              |
| Quick create form | Short form for fast record entry from anywhere        |
| Quick view form   | Read-only summary of a related record on another form |
| Card form         | Compact layout used in dashboards and mobile          |

Views are saved queries: "Active Customers," "Orders Created This Month." Model-driven apps are built directly from forms and views, which is why they need little UI design.

### Business logic options in Dataverse

Dataverse can enforce logic at the data layer so every app and flow using the data gets the same rules.

| Option                           | What it does                                               | Example                                       |
| -------------------------------- | ---------------------------------------------------------- | --------------------------------------------- |
| Business rules                   | No-code conditions that set, require, show, or hide fields | Require "Reason" when status is "Rejected"    |
| Power Fx (formula columns)       | Excel-like formulas that calculate values                  | Total = Price * Quantity                      |
| Calculated and rollup columns    | Computed values and aggregations over related rows         | Sum of all open Order amounts on the Customer |
| Real-time workflows and plug-ins | Advanced logic added by developers                         | Complex validation written in code            |

Power Fx is the low-code formula language of Power Platform. It appears in canvas apps, Dataverse formula columns, and other maker experiences. If the question says "Excel-like formula language," the answer is Power Fx.

### Using AI to create and edit tables

Copilot in the maker portal can create and edit Dataverse structures from natural language.

| You say                                   | Copilot does                                |
| ----------------------------------------- | ------------------------------------------- |
| "Create a table to track equipment loans" | Drafts a table with sensible columns        |
| "Add a column for return date"            | Adds a date column to the table             |
| "Relate loans to employees"               | Creates a lookup / one-to-many relationship |
| Upload a file or describe existing data   | Generates tables that match the data        |

The maker reviews and confirms; Copilot drafts, humans approve.

## Describe Power Platform administration and governance

### Environments

An environment is a container for apps, flows, agents, connections, and (optionally) a Dataverse database. Environments provide separation for security, region, and lifecycle.

| Environment type | Purpose                                                         |
| ---------------- | --------------------------------------------------------------- |
| Default          | Created automatically per tenant; shared by all users           |
| Production       | Live business solutions                                         |
| Sandbox          | Development and testing; can be copied and reset                |
| Trial            | Short-term evaluation; expires automatically                    |
| Developer        | Free single-user environment from the Power Apps Developer Plan |

Managed Environments add extra governance features (such as usage insights, sharing limits, and stricter controls) for environments the admin activates them on.

Key facts:

- Environments are bound to a geographic region, which supports data residency.
- A Dataverse database is created per environment (one database per environment).
- Apps and flows in one environment cannot see data in another environment's Dataverse by default.

### The Power Platform security model

Security is layered. Recognize which layer answers the question:

| Layer                    | Controls                                                     | Managed with                               |
| ------------------------ | ------------------------------------------------------------ | ------------------------------------------ |
| Tenant sign-in           | Who can authenticate at all                                  | Microsoft Entra ID                         |
| Environment access       | Who can enter an environment and in which role               | Environment roles and security groups      |
| Dataverse security roles | What tables and rows a user can create, read, update, delete | Security roles assigned to users and teams |
| Record-level concepts    | Ownership and business units scope who sees which rows       | Row ownership, business units, teams       |
| Column-level security    | Hide specific sensitive columns                              | Column security profiles                   |
| Connector governance     | Which connectors can be used and combined                    | DLP policies                               |

Data loss prevention (DLP) policies classify connectors into groups (typically business, non-business, and blocked) and prevent connectors from different groups being combined in one app or flow. Classic example: stop a flow from sending Dataverse data to a personal social media connector.

### Data privacy and accessibility

| Commitment area | What to know for the exam                                                                                                                             |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| Privacy         | Microsoft publishes compliance and privacy commitments in the Microsoft Trust Center; Power Platform supports GDPR and similar regulations            |
| Compliance      | Service compliance certifications are documented centrally; admins can review audit and compliance offerings                                          |
| Data residency  | Environments are created in a region, keeping data in that geography                                                                                  |
| Accessibility   | Microsoft products target accessibility standards (such as WCAG); makers should build accessible apps using accessible controls, labels, and contrast |

You do not need to memorize regulation details; you need to know where these commitments live (Trust Center) and that accessibility is both a platform capability and a maker responsibility.

### Monitoring and analytics

| Tool / capability            | What it shows                                                         |
| ---------------------------- | --------------------------------------------------------------------- |
| Power Platform admin center  | Central portal for environments, capacity, policies, and analytics    |
| Admin center analytics       | Usage, capacity, and health for Dataverse, Power Apps, Power Automate |
| Flow run history             | Success and failure of individual cloud flow runs                     |
| App analytics                | Usage and performance of individual apps                              |
| Managed Environment insights | Extra usage and adoption insights for managed environments            |

Memory hook: makers check their own app and flow history in the maker portal; admins check tenant-wide analytics in the Power Platform admin center.

### Application lifecycle management (ALM) with pipelines

ALM is how solutions move safely from development to production.

| Concept                  | Meaning                                                                     |
| ------------------------ | --------------------------------------------------------------------------- |
| Solution                 | A package that groups apps, flows, tables, and agents for transport         |
| Unmanaged solution       | Editable; used in development environments                                  |
| Managed solution         | Locked for editing; used in test and production environments                |
| Power Platform pipelines | Built-in feature that deploys solutions dev -> test -> prod in guided steps |

| ALM stage | Environment | Solution state |
| --------- | ----------- | -------------- |
| Build     | Development | Unmanaged      |
| Validate  | Test        | Managed        |
| Run       | Production  | Managed        |

Exam tip: "How do we move the app between environments in a controlled way" is answered by solutions and Power Platform pipelines, not by exporting data or re-creating the app.

## Common confusions

| Confusion                            | Correct idea                                                                        |
| ------------------------------------ | ----------------------------------------------------------------------------------- |
| Environment vs solution              | Environment is where things live; a solution is the package that moves them         |
| Form vs view                         | Form shows one record for editing; view lists many records                          |
| Business rule vs Power Fx            | Business rules are condition-based field logic; Power Fx is a formula language      |
| Security role vs DLP policy          | Security roles control data access; DLP controls which connectors can be combined   |
| Microsoft Entra ID vs security roles | Entra ID authenticates the user; security roles authorize what they do in Dataverse |
| Managed vs unmanaged solution        | Managed is locked for production; unmanaged is editable for development             |
| Dataverse vs the admin center        | Dataverse stores data; the admin center manages environments, policies, analytics   |

## Exam traps

| Trap                                                        | Why people miss it                                                                                    |
| ----------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| "Prevent users from seeing salary column" answered with DLP | Column-level security handles sensitive columns, DLP handles connectors                               |
| "One Dataverse database shared by all environments"         | Each environment has its own Dataverse database                                                       |
| "Views are for editing a record"                            | Views list records; forms edit a single record                                                        |
| "Move to production by exporting the app manually"          | Use solutions and pipelines for ALM                                                                   |
| "Power Fx is only for canvas apps"                          | Power Fx also powers Dataverse formula columns and other experiences                                  |
| "Trial and developer environments are the same"             | Trials expire for evaluation; developer environments are free, single-user, for learning and building |

## Mini scenarios

| Scenario                                                                                   | Best answer                                                  |
| ------------------------------------------------------------------------------------------ | ------------------------------------------------------------ |
| A company wants testers to work without touching live data.                                | Create a sandbox (or test) environment                       |
| A record of type Order must always belong to exactly one Customer.                         | One-to-many relationship (Customer to Order)                 |
| Sales staff should see their own opportunities but not other regions' rows.                | Dataverse security roles with row ownership / business units |
| Makers keep connecting company data to personal cloud storage in flows.                    | Apply a DLP policy                                           |
| The status reason field must become required when status is set to "Escalated."            | Business rule                                                |
| An admin needs to see which apps are most used across the tenant.                          | Power Platform admin center analytics                        |
| A tested solution must be promoted from the test environment to production with approvals. | Power Platform pipelines                                     |
| A maker wants Copilot to draft a new table for tracking assets.                            | Use AI (Copilot) in the maker portal to create the table     |

## Check yourself

1. Name three things Dataverse provides on top of raw data storage.
2. What is the difference between a form and a view?
3. Which formula language is used for formula columns in Dataverse and logic in canvas apps?
4. What does a DLP policy control?
5. Which environment type is free, single-user, and intended for learning and development?
6. What is the difference between a managed and an unmanaged solution?
7. Which portal does an admin use to review environments, capacity, and usage analytics?
8. What feature deploys solutions through development, test, and production in guided stages?

## Answer guide

1. Any three: role-based security, business logic (business rules, Power Fx), forms and views, rich data types, relationships, auditing.
2. A form displays and edits a single record; a view is a filtered, sorted list of many records.
3. Power Fx.
4. Which connectors can be used and combined in apps and flows (business vs non-business vs blocked groups).
5. A developer environment (Power Apps Developer Plan).
6. Unmanaged solutions are editable and used for development; managed solutions are locked and used for test and production.
7. The Power Platform admin center.
8. Power Platform pipelines.
