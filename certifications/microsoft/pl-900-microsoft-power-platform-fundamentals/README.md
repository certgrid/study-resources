# PL-900: Microsoft Power Platform Fundamentals - Study Cheatsheet

PL-900 (Microsoft Power Platform Fundamentals) validates foundational knowledge of the Power Platform: its business value plus the core products Power BI, Power Apps, Power Automate, Power Pages, Copilot Studio, and AI Builder, all built on Microsoft Dataverse. It is aimed at business users, citizen developers, and IT decision-makers who want to demonstrate they understand how low-code/no-code tools deliver business solutions. The exam is conceptual rather than hands-on, so focus on knowing what each product does, when to use it, and how the pieces fit together.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | PL-900 |
| Credential | PL-900: Microsoft Power Platform Fundamentals |
| Level | Beginner |
| Practice mock length | ~40 questions |
| Duration | ~45 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Describe the Business Value of Power Platform | ~18% |
| 2 | Identify Foundational Components of Power Platform | ~17% |
| 3 | Demonstrate Capabilities of Power BI | ~17% |
| 4 | Demonstrate Capabilities of Power Apps | ~17% |
| 5 | Demonstrate Capabilities of Power Automate | ~16% |
| 6 | Describe AI Builder | ~15% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Describe the Business Value of Power Platform

- Power Platform is a low-code/no-code suite (Power BI, Power Apps, Power Automate, Power Pages, Microsoft Copilot Studio) underpinned by Microsoft Dataverse; 'Power Server' is not a real product.
- The core business value is empowering 'citizen developers' (non-professional makers) to build apps, automations, and reports with visual designers and Excel-like formulas instead of traditional code.
- Connectors are pre-built integration points to hundreds of Microsoft and third-party data sources and services; Power Platform is not limited to Microsoft data.
- Standard connectors are included with most Microsoft 365/Dynamics 365 licenses; premium connectors (e.g. SQL Server, Azure, custom connectors, Dataverse in some plans) require additional per-user or per-app/per-flow licensing.
- Custom connectors let organizations integrate with any service exposing a REST API, including proprietary, legacy, or internal systems, without waiting for Microsoft to build a native connector.
- Data Loss Prevention (DLP) policies classify connectors into Business, Non-business, and Blocked groups; data cannot flow between connectors in different groups within the same app or flow.

### Domain 2 - Identify Foundational Components of Power Platform

- In Dataverse a table (formerly 'entity') stores data as rows (records) and columns (fields/attributes); each column has a defined data type.
- Each Dataverse environment contains a single database that holds all of that environment's tables and records.
- Relationships associate rows across tables: one-to-many (a customer with many orders), many-to-one, and many-to-many (students and courses, managed via an implicit junction table).
- A lookup column stores a reference to a row in another table, implementing the 'many' side of a one-to-many relationship.
- An Autonumber column auto-generates unique, sequential, human-readable identifiers (with optional prefix/format) on row creation, ideal for ticket or order numbers.
- Dataverse provides role-based access control through security roles, plus auditing/audit logging of data changes for compliance.

### Domain 3 - Demonstrate Capabilities of Power BI

- Power BI Desktop is a free Windows application used to connect to data, transform it with Power Query, build data models, and author reports and visualizations.
- The Power BI service (app.powerbi.com) is the cloud platform where reports are published, dashboards are created, and content is shared and consumed.
- A dataset (now called a semantic model) is the imported or connected data plus its model that reports are built on; one dataset can be shared and reused across multiple reports in a workspace.
- A report is a multi-page artifact built on a single dataset, where each page can contain many interactive visuals (goes 'deep').
- A dashboard exists only in the Power BI service and is a single-page canvas of tiles pinned from one or more reports, even across different datasets (goes 'broad').
- A workspace is a collaborative space in the service where teams create, publish, and manage datasets, reports, and dashboards with role-based access (Admin, Member, Contributor, Viewer).

### Domain 4 - Demonstrate Capabilities of Power Apps

- Canvas apps give the maker full pixel-level control over screen layout, starting from a blank canvas or template, and can connect to many data sources (Dataverse, SharePoint, Excel/OneDrive, SQL, and more).
- Model-driven apps derive their UI, forms, views, and navigation automatically from the underlying Dataverse data model and require Dataverse as the data source.
- Power Apps formulas use Power Fx, a low-code expression language similar in syntax to Excel formulas, making it accessible to spreadsheet users.
- Common Power Fx functions include Filter(), LookUp(), Patch() (create/update records), Navigate() (move between screens), and Collect() (build collections).
- Navigate() moves between canvas-app screens, e.g. Navigate(Screen2, ScreenTransition.Fade), with transitions like Fade, Cover, UnCover, and None.
- A Gallery control displays a scrollable list of multiple records using a repeating template layout.

### Domain 5 - Demonstrate Capabilities of Power Automate

- A cloud flow runs in the cloud and connects services and data sources; the three trigger types are automated (event), instant (manual/button), and scheduled (recurrence).
- Automated cloud flows start when a specific event occurs, such as an email arriving in Outlook, a record created in Dataverse, a file added to OneDrive, or an item created in SharePoint.
- Instant (button) flows are triggered manually on demand, including being called from a Power Apps canvas app button or a mobile/Teams button.
- Scheduled flows run on a recurring time-based schedule (e.g. daily at 8:00 AM, hourly, or weekly) using a recurrence trigger.
- Every flow is built from a trigger (the event that starts it) plus one or more actions (the operations it performs).
- Desktop flows provide Robotic Process Automation (RPA) to automate legacy desktop applications by recording mouse clicks, keyboard input, and screen interactions when no API exists.

### Domain 6 - Describe AI Builder

- AI Builder is a low-code AI capability that adds intelligence to Power Apps and Power Automate without requiring data science expertise or writing code.
- AI Builder offers two model categories: prebuilt models (ready to use immediately, no training) and custom models (you train them on your own data).
- Prebuilt models include text recognition/OCR, sentiment analysis, key phrase extraction, language detection, text translation, business card reader, category classification, and invoice/receipt/ID processing.
- The document processing model (formerly 'form processing') extracts structured key-value pairs and tabular data from documents like invoices, receipts, purchase orders, and forms.
- Training a custom document processing model requires a minimum of five sample documents of the same type/layout.
- Object detection identifies, locates, and counts specific objects within images, useful for inventory, retail shelf, or warehouse scenarios.

## Study tips

- Master the four pillars plus their split: Power BI = analyze/visualize, Power Apps = build apps, Power Automate = automate workflows, AI Builder = add AI; Dataverse is the common data store underneath. Many questions test which tool fits a described scenario.
- Know the canvas vs model-driven distinction cold: canvas = full layout control and many data sources; model-driven = data-first, Dataverse-required. Likewise know report (multi-page, one dataset) vs dashboard (single page, pinned tiles from many reports).
- Memorize the three cloud-flow trigger types (automated/event, instant/manual, scheduled/recurrence) and that desktop flows = RPA for apps without APIs.
- Distinguish the admin centers: Power Platform admin center manages environments and DLP; Microsoft 365 admin center manages users, groups, and licenses. DLP classifies connectors into Business/Non-business/Blocked.
- Watch for true/false and 'select all that apply' wording. Read carefully for distractors like fake products ('Power Server') and licensing nuances (standard connectors free, premium connectors require extra licensing).
- The exam is 45 minutes with a passing score of 700/1000; pace yourself, flag uncertain items for review, and answer every question since there is no penalty for guessing.

---

Want the full breakdown? See the complete **[PL-900 study guide](https://certgrid.app/study-guide/pl-900-microsoft-power-platform-fundamentals)** and **[free practice questions](https://certgrid.app/practice/pl-900-microsoft-power-platform-fundamentals)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

