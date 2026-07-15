# Salesforce Administrator (ADM-201) - Study Cheatsheet

The Salesforce Certified Administrator (ADM-201) exam validates the declarative, point-and-click skills needed to configure and manage a Salesforce org: users and security, the data model, automation, and the core Sales and Service apps. It is scenario-heavy and rewards hands-on experience far more than memorization. This guide distills the key concepts for every exam domain, with the official domain weightings in mind.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | Salesforce Administrator (ADM-201) |
| Credential | Salesforce Administrator (ADM-201) |
| Level | Intermediate |
| Practice mock length | ~60 questions |
| Duration | ~105 minutes |
| Passing score | 650 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Configuration and Setup | ~20% |
| 2 | Object Manager and Lightning App Builder | ~20% |
| 3 | Sales and Marketing Applications | ~12% |
| 4 | Service and Support Applications | ~11% |
| 5 | Productivity and Collaboration | ~7% |
| 6 | Data and Analytics Management | ~14% |
| 7 | Workflow and Process Automation | ~16% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Configuration and Setup

- Company Information, business hours, fiscal year, and the difference between org-wide settings and personal settings
- User management: activating users, profiles vs roles, and granting extra access with permission sets and permission set groups
- The 'minimum profile plus permission sets' model for least-privilege access
- Login and identity security: password policies, session settings, login IP ranges and login hours, and multi-factor authentication (MFA)
- The sharing model foundation: organization-wide defaults (OWD), the role hierarchy, sharing rules, and manual sharing
- Setup Audit Trail for tracking configuration changes, and declarative vs programmatic customization

### Domain 2 - Object Manager and Lightning App Builder

- Standard vs custom objects and how to choose the right custom field type
- Relationships: lookup, master-detail (with roll-up summaries and cascade delete), many-to-many junction objects, and hierarchical
- Record types to offer different picklist values and page layouts to different users
- Page layouts, compact layouts, and field-level security (FLS) as the platform-wide field visibility control
- Lightning App Builder: app, home, and record pages, plus component visibility rules
- Dynamic Forms and Dynamic Actions for field- and action-level layout control

### Domain 3 - Sales and Marketing Applications

- Leads and lead conversion (mapping to Account, Contact, and Opportunity)
- Opportunities, stages, sales processes, and guiding reps with Path
- Products, price books (standard vs custom), and the one-price-book-per-opportunity rule
- Campaigns, campaign hierarchy (up to five levels), campaign members, and campaign influence
- Web-to-Lead for capturing leads from a website form, including reCAPTCHA
- Lead assignment and auto-response rules

### Domain 4 - Service and Support Applications

- Cases and the support lifecycle; assignment, auto-response, and escalation rules
- Web-to-Case and Email-to-Case (including On-Demand Email-to-Case) for capturing cases
- Queues for routing records to teams, and case teams for collaboration
- Entitlements and milestones for tracking service-level agreements
- Omni-Channel routing with presence statuses, service channels, and capacity
- Lightning Knowledge articles and the Service Console workspace

### Domain 5 - Productivity and Collaboration

- Activities: tasks and events, and Einstein Activity Capture for email/calendar sync
- Chatter, groups, and feed tracking for collaboration
- Email templates, Lightning email, and organization-wide email addresses
- Macros and Quick Text to speed up repetitive agent work
- List views, list view charts, and the Salesforce mobile app
- Notes and files versus attachments

### Domain 6 - Data and Analytics Management

- Import tools: Data Import Wizard (up to 50,000 records, dedup, no delete) vs Data Loader (large volumes, all operations including delete and upsert)
- Exporting data with the Data Export Service (scheduled backups) and Data Loader
- Duplicate rules and matching rules to protect data quality
- Report formats: tabular, summary, matrix, and joined, and when to use each
- Report features: bucket fields, row-level formulas, summary formulas, and custom report types
- Dashboards, dashboard components, and dynamic dashboards (which run as the viewer, with a limited count)

### Domain 7 - Workflow and Process Automation

- Validation rules to enforce data quality at save time
- Flow as the primary automation tool: screen, record-triggered (before-save and after-save), scheduled, and autolaunched flows
- Choosing before-save vs after-save record-triggered flows for performance
- Approval processes: entry criteria, steps, approvers, and approval/rejection actions
- When to use a flow versus an approval process
- Migration away from the retiring Workflow Rules and Process Builder toward Flow

## Study tips

- Master the sharing model order of increasing access: OWD, then role hierarchy, then sharing rules, then manual and team sharing, then Apex sharing. Many questions hinge on 'who can see this record and why'.
- Know master-detail vs lookup cold: master-detail supports roll-up summaries, inherits ownership and sharing, cascades deletes, and is required on the child; lookup is loose and optional.
- For data loads, pick the tool by volume and operation: Data Import Wizard for up to 50,000 records with de-duplication and no delete; Data Loader for larger volumes and all operations, including delete, upsert, and scheduled runs.
- Flow is the future of automation. Expect questions where the correct answer is a flow and the distractors are the retiring Workflow Rules or Process Builder.
- Grant baseline access with a lean profile and layer extra permissions with permission sets and permission set groups, rather than cloning many profiles.
- Practice in a free Developer Edition org or Trailhead Playground. The exam is scenario-based, so clicking through the real Setup menus beats rote memorization.

---

Want the full breakdown? See the complete **[Salesforce Administrator (ADM-201) study guide](https://certgrid.app/study-guide/salesforce-administrator-adm-201)** and **[free practice questions](https://certgrid.app/practice/salesforce-administrator-adm-201)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

