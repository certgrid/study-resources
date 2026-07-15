# 04 - Describe the Capabilities of Microsoft Compliance Solutions

This domain is worth 20-25% of the exam. It covers the Service Trust Portal and Microsoft's privacy principles, compliance management with Microsoft Purview (the Purview portal, Compliance Manager, compliance score), information protection and data lifecycle management (classification, Content explorer, Activity explorer, sensitivity labels, DLP, records management, retention), and the risk and investigation tools: insider risk management, eDiscovery, and audit.

## Mental model

Microsoft Purview is the compliance and data governance family. Sort every capability into one of four jobs:

1. PROVE trust: Service Trust Portal, privacy principles, Compliance Manager.
2. KNOW your data: classification, Content explorer, Activity explorer.
3. PROTECT and GOVERN data: sensitivity labels, DLP, retention, records management.
4. INVESTIGATE people and events: insider risk management, eDiscovery, audit.

| Scenario keyword                                      | Likely concept                                                    |
| ----------------------------------------------------- | ----------------------------------------------------------------- |
| Download Microsoft's audit reports and certifications | Service Trust Portal                                              |
| Microsoft's commitments on how it handles your data   | Privacy principles                                                |
| Assess compliance with GDPR, ISO, NIST                | Compliance Manager                                                |
| Risk-based percentage of compliance posture           | Compliance score                                                  |
| Find what sensitive data exists                       | Data classification (sensitive info types, trainable classifiers) |
| See labeled/classified items across the estate        | Content explorer                                                  |
| See activities on labeled items over time             | Activity explorer                                                 |
| Classify and protect a document wherever it goes      | Sensitivity labels                                                |
| Stop credit card numbers leaving via email/Teams      | Data loss prevention (DLP)                                        |
| Keep data for 7 years, then delete                    | Retention policies/labels                                         |
| Declare an item an immutable business record          | Records management                                                |
| Detect a departing employee stealing data             | Insider risk management                                           |
| Legal hold and search for a lawsuit                   | eDiscovery                                                        |
| Who accessed what, forensic log search                | Audit                                                             |

## Microsoft Service Trust Portal and privacy principles

### Service Trust Portal

The Service Trust Portal (STP) is Microsoft's public site for the content and tools organizations use to evaluate how Microsoft protects their data.

| Offering                        | What you get                                                                     |
| ------------------------------- | -------------------------------------------------------------------------------- |
| Certifications and attestations | ISO/IEC, SOC, FedRAMP, and similar third-party audit reports                     |
| Reports and whitepapers         | Audit reports, penetration test summaries, security assessments                  |
| Industry and regional resources | Compliance info for specific industries and countries                            |
| Resources for your review       | Save documents to a library (requires signing in with a Microsoft cloud account) |

Keyword: a customer, auditor, or regulator wants EVIDENCE about Microsoft's own compliance = Service Trust Portal.

### Microsoft's privacy principles

Six principles govern how Microsoft handles customer data:

| Principle                  | Meaning                                                                    |
| -------------------------- | -------------------------------------------------------------------------- |
| Control                    | You control your data and how it is used                                   |
| Transparency               | Microsoft is clear about data collection and use                           |
| Security                   | Data is protected with strong security and encryption                      |
| Strong legal protections   | Local privacy laws are respected; legal protection of privacy is supported |
| No content-based targeting | Email, chat, files are not used for targeted advertising                   |
| Benefits to you            | Data Microsoft collects is used to benefit you and improve your experience |

Related product to recognize: Microsoft Priva helps organizations manage privacy risk and handle subject rights requests for the personal data THEY hold (distinct from Microsoft's own privacy principles).

## Compliance management with Microsoft Purview

### The Microsoft Purview portal

The Microsoft Purview portal (purview.microsoft.com) is the single home for Purview solutions across compliance and data governance: Information Protection, Data Loss Prevention, Data Lifecycle Management, Records Management, Insider Risk Management, eDiscovery, Audit, Compliance Manager, and data governance capabilities like Data Map and Data Catalog.

Access requires appropriate roles (e.g. compliance roles) rather than full Microsoft 365 admin rights, supporting least privilege.

### Compliance Manager

Compliance Manager is the Purview solution that helps you manage your organization's compliance requirements.

| Element              | Meaning                                                                 |
| -------------------- | ----------------------------------------------------------------------- |
| Assessments          | Groupings of controls for a specific regulation or standard (e.g. GDPR) |
| Controls             | Individual requirements, managed by you, by Microsoft, or shared        |
| Improvement actions  | Concrete steps that implement controls and earn points                  |
| Regulatory templates | Prebuilt assessments for many laws and standards                        |

### Compliance score

Compliance score is the risk-based percentage inside Compliance Manager that measures progress on improvement actions. Points are weighted by risk: mandatory/preventative actions score higher than discretionary ones.

| Score                  | Measures                          | Found in                     |
| ---------------------- | --------------------------------- | ---------------------------- |
| Compliance score       | Compliance posture vs regulations | Compliance Manager (Purview) |
| Microsoft Secure Score | Security posture of M365          | Microsoft Defender portal    |

Benefit summary: compliance score helps prioritize which compliance work reduces the most risk first.

## Information protection, data lifecycle management, and data governance

Microsoft's model: know your data, protect your data, prevent data loss, govern your data.

### Data classification

| Capability                         | How it identifies data                                                                                            |
| ---------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| Sensitive information types (SITs) | Pattern-based: regex, keywords, checksums (credit card numbers, passport numbers); many built in, custom possible |
| Trainable classifiers              | Machine learning trained on example content (contracts, resumes, source code); for content patterns cannot match  |
| Exact data match                   | Matches exact values from your own uploaded sensitive data tables                                                 |

### Content explorer and Activity explorer

| Tool              | Shows                                                                                     | Benefit                                  |
| ----------------- | ----------------------------------------------------------------------------------------- | ---------------------------------------- |
| Content explorer  | A current snapshot of items with labels or SIT matches, and where they are                | See WHAT sensitive data exists and WHERE |
| Activity explorer | Historical activities on labeled content (label changed, file copied to USB, DLP matches) | See what is being DONE with the data     |

Memory hook: Content = what and where (noun). Activity = what happened (verb).

### Sensitivity labels and label policies

Sensitivity labels classify AND protect content. The label travels with the file.

| Property     | Detail                                                                        |
| ------------ | ----------------------------------------------------------------------------- |
| Customizable | You define names like Public, General, Confidential                           |
| Clear text   | Label is stored in file metadata, readable by other systems                   |
| Persistent   | Protection follows the file wherever it goes                                  |
| Effects      | Encryption, content markings (watermark, header, footer), access restrictions |
| Scope        | Files, emails, meetings, groups and sites, and schematized data assets        |

Label POLICIES publish labels to users and can require a default label, mandatory labeling, or justification for downgrading a label. Auto-labeling can apply labels based on detected sensitive content.

### Data loss prevention (DLP)

DLP policies detect and prevent risky sharing or transfer of sensitive information across Exchange, SharePoint, OneDrive, Teams, endpoints (Endpoint DLP for Windows/macOS), and cloud apps.

| Policy part | Example                                                                |
| ----------- | ---------------------------------------------------------------------- |
| Conditions  | Email contains credit card numbers AND is sent outside the org         |
| Actions     | Block the share, block with override, show a policy tip, notify, audit |
| Locations   | Exchange, SharePoint, OneDrive, Teams, devices, cloud apps             |

Keyword: PREVENT sensitive data from LEAVING = DLP. (Labels classify and protect; DLP stops movement.)

### Retention policies, retention labels, and retention label policies

Retention governs how long content is KEPT and what happens afterward (retain, delete, or retain then delete).

| Tool                   | Applies to                                                                 | Granularity                   |
| ---------------------- | -------------------------------------------------------------------------- | ----------------------------- |
| Retention policy       | Whole locations (all Exchange mailboxes, SharePoint sites, Teams messages) | Site/mailbox level, broad     |
| Retention label        | Individual items (a document, an email)                                    | Item level, can vary per item |
| Retention label policy | Publishes labels to locations so users or auto-rules can apply them        | Distribution mechanism        |

Principles to recognize: retention wins over deletion; the longest retention period wins; explicit (label) wins over implicit (policy).

### Records management

Records management is for items that must be declared RECORDS for legal, business, or regulatory reasons.

| Mark as           | Effect                                                            |
| ----------------- | ----------------------------------------------------------------- |
| Record            | Item is restricted: certain edits/deletes are blocked             |
| Regulatory record | Strictest: even admins cannot remove the label or delete the item |

Extras: file plans for managing retention labels at scale, event-based retention (start the clock when an employee leaves), and disposition review (a human approves final deletion).

Memory hook: retention = keep/delete schedule. Records = lock it as evidence.

## Insider risk, eDiscovery, and audit

### Insider risk management

Insider risk management detects, investigates, and acts on risky activities BY PEOPLE INSIDE the organization: data theft by departing employees, data leaks, security policy violations.

| Element    | Detail                                                                          |
| ---------- | ------------------------------------------------------------------------------- |
| Triggers   | Events like a resignation date that start watching a user                       |
| Indicators | Signals such as downloading masses of files, copying to USB, sharing externally |
| Privacy    | Pseudonymization by default; role-based access; investigations are gated        |
| Workflow   | Policy, alerts, triage, investigate, act (case, notice, escalate)               |

Keyword: EMPLOYEE or insider misusing data = insider risk management (not DLP alone, not Defender).

### eDiscovery solutions in Microsoft Purview

eDiscovery identifies and delivers electronic information for legal cases and investigations.

| Solution              | Capabilities                                                                                   |
| --------------------- | ---------------------------------------------------------------------------------------------- |
| Content search        | Search across mailboxes, sites, Teams; export results; no case management                      |
| eDiscovery (Standard) | Content search PLUS cases and legal hold                                                       |
| eDiscovery (Premium)  | End-to-end workflow: custodians, communications, review sets, analytics, ML-assisted relevance |

Keyword ladder: just search = Content search. Search + hold + case = Standard. Custodians, review, analytics = Premium.

### Audit solutions in Microsoft Purview

Audit records user and admin activities across Microsoft 365 for search and investigation.

| Solution         | Capabilities                                                                                                                                              |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Audit (Standard) | Thousands of searchable events, default 180-day retention                                                                                                 |
| Audit (Premium)  | Longer retention (1 year, up to 10 years with add-on), intelligent insights, higher-value events like when a mail item was accessed, faster API bandwidth |

Keyword: "who did what and when" or forensic investigation of ACTIVITIES = audit. (eDiscovery finds CONTENT; audit finds ACTIONS.)

## Common confusions

| Confusion                                  | Correct idea                                                                          |
| ------------------------------------------ | ------------------------------------------------------------------------------------- |
| Sensitivity labels vs retention labels     | Classify and protect content vs keep/delete content on a schedule                     |
| DLP vs sensitivity labels                  | Stop data leaving vs classify and protect data wherever it goes                       |
| Content explorer vs Activity explorer      | Snapshot of classified items vs history of actions on them                            |
| Compliance Manager vs compliance score     | The solution vs the risk-based metric inside it                                       |
| Compliance score vs Microsoft Secure Score | Compliance posture (Purview) vs security posture (Defender portal)                    |
| Retention policy vs retention label        | Broad location-level rule vs per-item rule                                            |
| Records management vs retention            | Immutable declaration for regulated items vs keep/delete scheduling                   |
| Insider risk management vs DLP             | Watching risky user behavior patterns vs blocking sensitive content movement          |
| eDiscovery vs audit                        | Find and preserve content for legal cases vs search activity logs                     |
| Service Trust Portal vs Compliance Manager | Microsoft's own compliance evidence vs YOUR organization's compliance posture         |
| Microsoft Priva vs privacy principles      | Product for managing your privacy obligations vs Microsoft's commitments to customers |

## Exam traps

| Trap                                                                | Why people miss it                                                                                                   |
| ------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| "Use Compliance Manager to check Microsoft's certifications"        | Microsoft's own audit reports live in the Service Trust Portal.                                                      |
| "Retention labels encrypt documents"                                | Encryption and markings come from SENSITIVITY labels; retention only governs keep/delete.                            |
| "DLP classifies your data estate"                                   | Classification is done by SITs, trainable classifiers, and labels; DLP uses those classifications to block movement. |
| "A higher compliance score means you are compliant"                 | It measures progress on risk-weighted actions; it is not a legal guarantee of compliance.                            |
| "Admins can always delete regulatory records"                       | Regulatory records cannot be removed even by admins; that is their purpose.                                          |
| "eDiscovery (Standard) includes ML-assisted review"                 | Analytics, custodians, and review sets are Premium features.                                                         |
| "Audit (Standard) retains logs for years"                           | Standard is 180 days; longer retention needs Audit (Premium).                                                        |
| "Insider risk management shows investigator real names immediately" | Users are pseudonymized by default to protect privacy.                                                               |

## Mini scenarios

| Scenario                                                                                     | Best answer                                     |
| -------------------------------------------------------------------------------------------- | ----------------------------------------------- |
| An auditor asks for Microsoft's ISO 27001 audit report.                                      | Service Trust Portal                            |
| Track your organization's progress against GDPR requirements with prebuilt templates.        | Compliance Manager                              |
| Automatically find credit card numbers stored across SharePoint.                             | Sensitive information types (classification)    |
| See a current snapshot of which sites hold items labeled Confidential.                       | Content explorer                                |
| Watermark and encrypt a document so protection follows it outside the company.               | Sensitivity label                               |
| Block emails containing patient records from being sent externally, with an override option. | Data loss prevention (DLP)                      |
| Keep project files for 7 years, then delete them automatically.                              | Retention label/policy                          |
| A contract must be locked so nobody, including admins, can delete it before its date.        | Regulatory record (records management)          |
| Get alerted when a resigning employee mass-downloads customer lists.                         | Insider risk management                         |
| Place a legal hold on three custodians' mailboxes and review the content with analytics.     | eDiscovery (Premium)                            |
| Determine which admin deleted a SharePoint site last month.                                  | Audit                                           |
| Confirm Microsoft does not use your email content for advertising.                           | Privacy principles (no content-based targeting) |

## Check yourself

1. What kinds of documents does the Service Trust Portal offer, and who typically needs them?
2. Name Microsoft's six privacy principles.
3. What is the relationship between Compliance Manager and compliance score?
4. What are the three main ways Purview classifies data?
5. What is the difference between Content explorer and Activity explorer?
6. Compare sensitivity labels, retention labels, and DLP in one sentence each.
7. What extra protection does a regulatory record have over a normal record?
8. Which eDiscovery tier adds custodians, review sets, and analytics, and what is the default retention difference between Audit Standard and Premium?

## Answer guide

1. Third-party audit reports, certifications (ISO, SOC, FedRAMP), whitepapers, and compliance resources about Microsoft's cloud services; used by auditors, regulators, and customers evaluating Microsoft.
2. Control, transparency, security, strong legal protections, no content-based targeting, and benefits to you.
3. Compliance Manager is the Purview solution for managing compliance via assessments and improvement actions; compliance score is the risk-based percentage inside it that measures progress.
4. Sensitive information types (pattern matching), trainable classifiers (machine learning), and exact data match.
5. Content explorer shows a current snapshot of classified/labeled items and their locations; Activity explorer shows the history of activities performed on that content.
6. Sensitivity labels classify and protect content (encryption, markings) wherever it travels; retention labels control how long items are kept and whether they are deleted; DLP prevents sensitive content from being shared or moved inappropriately.
7. A regulatory record cannot have its label removed or the item deleted by anyone, including administrators; normal records block edits/deletes but with fewer absolute restrictions.
8. eDiscovery (Premium); Audit (Standard) retains logs for 180 days while Audit (Premium) provides 1-year retention by default with an option up to 10 years.
