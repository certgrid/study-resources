# PL-200: Power Platform Functional Consultant - Study Cheatsheet

The PL-200: Microsoft Power Platform Functional Consultant exam validates your ability to configure Microsoft Dataverse, build apps with Power Apps, automate processes with Power Automate, create chatbots in Copilot Studio, and analyze data with Power BI. It targets functional consultants who gather requirements, design and configure solutions, and manage Power Platform implementations. Expect 40-60 questions over 120 minutes with a passing score of 700 (on a 1000-point scale).

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | PL-200 |
| Credential | PL-200: Power Platform Functional Consultant |
| Level | Intermediate |
| Practice mock length | ~50 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-06-24 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Configure Microsoft Dataverse | ~23% |
| 2 | Create Apps with Power Apps | ~21% |
| 3 | Automate with Power Automate | ~21% |
| 4 | Implement Power Virtual Agents / Copilot Studio | ~18% |
| 5 | Analyze Data with Power BI | ~17% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Configure Microsoft Dataverse

- Dataverse is the foundational, secure, scalable relational data platform for Power Platform; it stores data in tables (rows/columns) and enforces enterprise-grade security and server-side business logic.
- Security roles define privileges (Create, Read, Write, Delete, Append, Append To, Assign, Share) per table; each privilege has an access level scope: None, User (own), Business Unit, Parent:Child BU, or Organization (full circle).
- Column-level (field-level) security controls which COLUMNS a user can see/edit, not which ROWS - row visibility is governed by security-role access levels and record ownership/sharing.
- If a security role grants no Delete privilege on a table, delete is blocked for that user regardless of who owns the record.
- Business rules run on the form (client) AND can run server-side; they validate data, set/clear field values, show error messages, and set fields required - without code. Real-time/synchronous workflows and Dataverse plug-ins handle more complex synchronous logic.
- Relationship types: one-to-many (1:N) and many-to-many (N:N). A lookup column implements the 'many' side of a 1:N relationship; N:N uses an intersect (relationship) table.

### Domain 2 - Create Apps with Power Apps

- Model-driven apps are metadata-driven: they auto-generate responsive UI from the Dataverse schema, surfacing the site map (navigation), tables, forms, views, dashboards, and business process flows - ideal for data-centric, process-driven scenarios.
- Canvas apps give pixel-level control over layout and styling with Power Fx formulas bound to controls; ideal for task-specific or role-specific experiences and can connect to many data sources (Dataverse, SharePoint, SQL, connectors).
- Choose model-driven when you need rich relationships, role-based security, standardized forms/views, and scalability; choose canvas for a custom, tailored UI.
- Delegation: use delegable functions and operators (Filter, Search, LookUp with supported operators) so query work is pushed to the data source; non-delegable functions cap results at the delegation row limit (default 500, max 2000).
- Improve canvas performance: reduce controls and data sources on the first screen, minimize OnStart data loads, select only needed columns, and cache data once in a collection/variable for reuse.
- Patch(Accounts, Defaults(Accounts), {Name: txtName.Text}) creates a new record; Patch with an existing record updates it. Filter(Accounts, Revenue > 50000) returns matching rows.

### Domain 3 - Automate with Power Automate

- Power Automate automates workflows with triggers (events/schedules) and actions across services; flows connect to hundreds of connectors for tasks like notifications, approvals, and data sync.
- Three cloud flow trigger types: automated (event-triggered, e.g., a Dataverse row is added/modified/deleted), scheduled (recurring on a defined cadence), and instant (manually run via button or from an app).
- Connectors are proxies/definitions that expose a service's API to flows and apps, handling authentication and data formatting through a standardized interface.
- Environment variables parameterize configuration (URLs, site IDs, connection references) so a solution moves between dev/test/prod without hard-coding values.
- Error handling: configure 'Configure run after' settings (run on succeeded/failed/skipped/timed out), wrap actions in Scopes, and set retry policies (default, fixed interval, or exponential backoff) on individual actions.
- The Approvals action is a built-in workflow that requests and captures approve/reject decisions from users and waits for the response.

### Domain 4 - Implement Power Virtual Agents / Copilot Studio

- Microsoft Copilot Studio (formerly Power Virtual Agents) is a no-code/low-code platform for building chatbots that answer questions and trigger actions through a visual topic-based interface.
- Topics are conversation units triggered by trigger phrases; add varied trigger phrases and define entities so a topic matches diverse user phrasing and extracts data from utterances.
- Generative answers ground chatbot responses in knowledge sources (websites, SharePoint, documents, Dataverse) so the bot can answer questions you did not author as explicit topics.
- Use authored topics with explicit trigger phrases for governed, deterministic processes; use generative answers for broad, open-ended FAQ coverage.
- A 'Call an action' node lets a topic call a Power Automate flow or connector to perform tasks like creating a Dataverse record, passing inputs and returning outputs into the conversation.
- A flow called from a topic must be in the same solution/environment and use the Power Apps V2 trigger with a Respond action so inputs/outputs map correctly.

### Domain 5 - Analyze Data with Power BI

- A Power BI dataset (semantic model) is the core artifact containing the data model: table relationships, calculated columns, and DAX measures; reports and dashboards query against it.
- Power Query (M language) is the transformation/cleaning layer that runs before data reaches the model - remove columns, change types, merge, filter; Table.SelectRows(Source, each [Status] <> "Cancelled") filters rows.
- Query folding pushes Power Query transformation steps down to the source as native queries; preserve folding to minimize data transferred and refresh time.
- Reduce model size and improve performance by removing unused columns and reducing high-cardinality columns (e.g., split or round full-precision timestamps) in Power Query before import.
- Incremental refresh refreshes only new/changed partitions instead of the whole dataset, dramatically reducing refresh time for large fact tables.
- Storage modes: Import caches data in-memory for fast visuals (with scheduled refresh latency); DirectQuery queries the source live for large/fresh data; Composite mixes both.

## Study tips

- Watch the privilege-vs-access-level distinction: privileges (Create/Read/Write/Delete) decide WHAT actions, while access levels (User/BU/Org) decide WHICH records. Column-level security is a separate, field-scoped control.
- On 'choose the right tool' questions, default to the lowest-effort native option: business rules before flows before code; Dataverse trigger before scheduled poll; model-driven for data-centric, canvas for custom UI.
- Memorize the delegation rule: non-delegable functions silently cap at the row limit (default 500). If a question describes missing records in a large data source, the fix is to redesign with delegable functions/filters.
- For performance questions in any product, the answer almost always reduces work at the source: query folding and incremental refresh (Power BI), Filter rows OData and column selection (Power Automate), fewer controls/columns and collections (Power Apps).
- Read case-study and yes/no questions carefully - they often hinge on one detail (a missing privilege, wrong scope, gateway requirement, or solution/environment mismatch). Eliminate options that violate a hard rule rather than picking the first plausible one.

---

Want the full breakdown? See the complete **[PL-200 study guide](https://certgrid.app/study-guide/pl-200-power-platform-functional-consultant)** and **[free practice questions](https://certgrid.app/practice/pl-200-power-platform-functional-consultant)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

