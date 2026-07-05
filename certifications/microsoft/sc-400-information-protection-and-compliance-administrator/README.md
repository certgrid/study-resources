# SC-400: Information Protection and Compliance Administrator - Study Cheatsheet

Microsoft SC-400 validates your ability to plan and implement information protection, data loss prevention, retention, and compliance investigations across Microsoft 365 using Microsoft Purview. It targets information protection administrators who classify and protect data, build DLP policies, govern data lifecycle, and support eDiscovery and insider-risk work, typically alongside security, compliance, and Microsoft 365 administrators. The exam is 120 minutes, passing score is 700, and it expects hands-on familiarity with the Purview compliance portal and PowerShell.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | SC-400 |
| Credential | SC-400: Information Protection and Compliance Administrator |
| Level | Intermediate |
| Practice mock length | ~50 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-06-24 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Implement Information Protection | ~26% |
| 2 | Implement Data Loss Prevention | ~24% |
| 3 | Implement Information Governance | ~23% |
| 4 | Monitor and Investigate | ~27% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Implement Information Protection

- Sensitivity labels are the core Purview classification mechanism; a label can apply visual markings (header, footer, watermark), encryption with usage rights, and content-marking, and the protection travels with the file even after it leaves the tenant.
- Label encryption uses Azure Rights Management (Azure RMS); usage rights such as View, Edit, Copy, Print, and Reply are bound to specified users or groups, so an unauthorized user who obtains the file still cannot open it.
- A label policy publishes labels to users/groups and sets behaviors like a default label, mandatory labeling, justification for lowering a label, and the order labels appear; auto-labeling policies apply labels without user action.
- Auto-labeling exists in two forms: client-side (in Office apps, can recommend or apply as users work) and service-side auto-labeling (applies to data at rest in Exchange, SharePoint, and OneDrive without opening the file).
- Sensitive information types (SITs) are pattern-matching detectors (e.g., credit card number with Luhn check, U.S. SSN in XXX-XX-XXXX format) using primary patterns, supporting elements, proximity, and confidence levels.
- Trainable classifiers use machine learning to categorize content by example rather than pattern (e.g., resumes, source code, contracts); they require seed and test data and are useful where SITs cannot define a fixed pattern.

### Domain 2 - Implement Data Loss Prevention

- DLP policies detect sensitive content and prevent its unauthorized disclosure; actions include blocking/restricting sharing, notifying with a policy tip, generating admin alerts, allowing user override with justification, and encrypting.
- DLP locations span Exchange email, SharePoint sites, OneDrive accounts, Teams chat and channel messages, and managed devices via Endpoint DLP, plus on-premises repositories through the Purview data scanner.
- Endpoint DLP runs on Windows and macOS devices enrolled in Intune or onboarded with the agent; it can restrict copy to USB, copy to network share, print, paste to browser, and upload to unsanctioned cloud or restricted apps.
- Always deploy a new DLP policy in simulation (test) mode first; it logs matches without blocking or notifying, so you can review Activity Explorer, assess business impact, and tune rules to reduce false positives before enforcing.
- DLP rules combine conditions (e.g., content contains a SIT at or above an instance-count threshold, shared externally), exceptions, and actions; instance count and confidence level are the primary tuning levers.
- Use a policy tip with user override and justification where business needs vary, and audit the overrides, rather than fully blocking or disabling the policy and breaking legitimate work.

### Domain 3 - Implement Information Governance

- Retention controls how long content is kept and what happens at the end: retain only, retain then delete, or delete only; the retention period can be based on content creation, last modification, or when labeled.
- Retention policies apply broadly to locations (mailboxes, sites, Teams, Yammer) without user action; retention labels apply to individual items/folders/libraries and can trigger record declaration and disposition.
- Records management lets you declare content a record (editable metadata but locked content, can be relabeled) or a regulatory record (fully immutable, cannot be relabeled or unlocked) to meet legal recordkeeping obligations.
- Retention principles of precedence resolve conflicts: retention wins over deletion, the longest retention period wins, explicit labels beat policies, and the shortest deletion is applied only after all retention is satisfied.
- Disposition review inserts a manual approval step at end of retention so designated reviewers approve deletion, relabeling, or extension, producing an audit trail; reserve it for high-value records and use automatic deletion for routine content.
- Adaptive scopes target retention dynamically using an attribute query (e.g., Department, country, or a site URL), so membership updates automatically as people and sites change, unlike static scopes that you maintain by hand.

### Domain 4 - Monitor and Investigate

- eDiscovery searches for and preserves content across Exchange, SharePoint, OneDrive, and Teams for legal matters; eDiscovery (Standard) provides case management, search, hold, and export, while eDiscovery (Premium) adds custodian management, legal hold notifications, review sets, analytics, and predictive coding.
- An eDiscovery hold preserves potentially relevant content from deletion or alteration while a matter is active; holds are scoped to specific locations and can be narrowed with a content match query.
- Key eDiscovery cmdlets: New-ComplianceCase creates a case; New-CaseHoldPolicy plus New-CaseHoldRule place and define a hold; New-ComplianceSearch, Start-ComplianceSearch, and New-ComplianceSearchAction run and export searches.
- New-ComplianceSearchAction with -Export exports results; with -Purge -PurgeType HardDelete it permanently removes matching items (used for remediating phishing/malware); Get-ComplianceSearchAction -Details checks status.
- Litigation hold is set per mailbox with Set-Mailbox -LitigationHoldEnabled $true and preserves all mailbox content; it differs from case/eDiscovery holds, which are query-scoped across multiple workloads.
- The unified audit log records actions across M365 (mailbox operations, file access, sharing, policy and admin changes, eDiscovery activity); query it with Search-UnifiedAuditLog filtered by -StartDate, -EndDate, -Operations, -UserIds.

## Study tips

- Always run new DLP and auto-labeling policies in simulation/test mode first, review Activity Explorer, and tune instance count and confidence before enforcing; expect several questions framed around reducing false positives without disabling protection.
- Memorize the retention precedence rules cold: retention wins over deletion, longest retention wins, explicit labels beat policies, and deletion applies only after all retention is satisfied.
- Know the PowerShell cmdlets verbatim, especially New-ComplianceCase, New-CaseHoldPolicy/New-CaseHoldRule, New-ComplianceSearchAction (-Export vs -Purge -PurgeType HardDelete), Set-Mailbox -LitigationHoldEnabled, and Search-UnifiedAuditLog parameters.
- Distinguish overlapping features by their unique purpose: SIT vs trainable classifier vs EDM; sensitivity label vs retention label; record vs regulatory record; eDiscovery Standard vs Premium; DKE vs BYOK; adaptive vs static scopes.
- When a scenario stresses scale or noise, prefer adaptive scopes, targeted locations/groups, high-confidence SITs, and disposition review only for high-value records rather than broad, tenant-wide enforcement.

---

Want the full breakdown? See the complete **[SC-400 study guide](https://certgrid.app/study-guide/sc-400-information-protection-and-compliance-administrator)** and **[free practice questions](https://certgrid.app/practice/sc-400-information-protection-and-compliance-administrator)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

