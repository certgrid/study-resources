# MS-102: Microsoft 365 Administrator - Study Cheatsheet

MS-102: Microsoft 365 Administrator validates your ability to deploy and manage a Microsoft 365 tenant, implement and manage identity and access with Microsoft Entra ID, and manage security, threats, and compliance across the platform. It is aimed at administrators who plan, deploy, and operate Microsoft 365 services for an organization and who coordinate with specialist administrators for workloads such as Exchange, SharePoint, and Teams. Expect roughly 40-60 questions in 120 minutes, including case studies, with a passing score of 700 out of 1000.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | MS-102 |
| Credential | MS-102: Microsoft 365 Administrator |
| Level | Intermediate |
| Practice mock length | ~50 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-06-24 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Deploy and Manage a Microsoft 365 Tenant | ~27% |
| 2 | Implement and Manage Identity and Access | ~24% |
| 3 | Manage Security and Threats | ~25% |
| 4 | Manage Compliance | ~23% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Deploy and Manage a Microsoft 365 Tenant

- Custom domain ownership is verified by adding a TXT (or alternatively MX) DNS record containing the unique verification token Microsoft generates; TXT is preferred because it does not interfere with existing mail flow.
- A subdomain (for example, sales.contoso.com) can only be added after the parent domain (contoso.com) has been added and verified in the same tenant.
- A domain can belong to only one Microsoft 365 tenant at a time; you must remove it from any other tenant before adding it to yours.
- The Service health dashboard shows real-time incidents and advisories affecting your tenant's services; the Message center notifies admins about upcoming changes, new features, and planned maintenance with advance notice.
- The Office Customization Tool (OCT) at config.office.com is the web-based tool for building the configuration.xml used by the Office Deployment Tool (ODT) to install and customize Microsoft 365 Apps.
- Microsoft 365 Apps update channels include Current Channel (frequent updates), Monthly Enterprise Channel (predictable monthly cadence), and Semi-Annual Enterprise Channel (features about every six months for maximum stability and testing time).

### Domain 2 - Implement and Manage Identity and Access

- Dynamic membership groups use attribute-based rules (for example, department or location) to add or remove members automatically; dynamic groups require Microsoft Entra ID P1 and a group can be dynamic for users OR for devices, not both.
- Microsoft Entra Connect synchronizes on-premises AD objects to Entra ID; password hash synchronization (PHS) syncs password hashes to the cloud, while pass-through authentication (PTA) validates passwords against on-premises AD without storing hashes in the cloud.
- Common sync errors include duplicate (conflicting) attribute values such as a duplicated proxyAddress or userPrincipalName between objects.
- Conditional Access policies enforce access controls based on signals (user, location, device, app, risk); a named location defines trusted IP ranges so you can require MFA for users outside the corporate network.
- Always exclude break-glass (emergency access) and service accounts from a Conditional Access policy by adding them to the policy's exclusion list to avoid lockout.
- Security defaults provide baseline tenant-wide MFA enforcement for free; Conditional Access (requires Entra ID P1) offers granular control but cannot be used at the same time as security defaults.

### Domain 3 - Manage Security and Threats

- Exchange Online Protection (EOP) is included with every plan that has Exchange Online mailboxes and provides baseline anti-malware, anti-spam, and anti-spoofing (spoof intelligence) at no extra cost.
- Anti-phishing policies in Defender for Office 365 add user (and domain) impersonation protection plus mailbox intelligence; add high-value recipients such as the CEO to the impersonation protection list.
- Safe Attachments detonates attachments in a sandbox before delivery; Dynamic Delivery delivers the message body immediately with a placeholder and reattaches the file after scanning to avoid delays.
- Safe Links rewrites and scans URLs at time-of-click in email and Office documents, checking against Microsoft threat intelligence and blocking newly malicious sites.
- Defender for Office 365 Plan 1 includes Safe Attachments, Safe Links, and anti-phishing; Plan 2 adds Threat Explorer, Attack simulation training, and Automated Investigation and Response (AIR).
- Email authentication uses SPF (authorized senders, configured first), DKIM (cryptographic signing enabled per domain in the Defender portal), and DMARC; a DMARC record with p=reject tells receivers to reject messages that fail authentication.

### Domain 4 - Manage Compliance

- Data Loss Prevention (DLP) policies detect sensitive data (using built-in or custom sensitive information types) across Exchange, SharePoint, OneDrive, Teams, and endpoints, then block, warn, or encrypt; a policy can block with user override requiring business justification that is logged.
- Sensitive information types (SITs) match patterns such as credit card numbers; you can create a custom SIT when built-in types do not match your data (for example, an internal employee ID format).
- Retention policies (location-based) and retention labels (item-level) govern how long content is kept and what happens after; auto-apply retention label policies can apply a label automatically based on a keyword query or SIT match.
- When retention and deletion settings conflict, retention always wins: content is retained for the full period before any deletion takes effect (for example, retain 5 years then delete).
- Retention settings apply across Exchange Online mailboxes, SharePoint Online sites, OneDrive, Microsoft 365 group sites/Teams, and Teams chat and channel messages.
- Sensitivity labels classify and protect content with metadata that travels with the file; a single label can apply Azure Rights Management encryption and visual markings (headers, footers, watermarks) at once.

## Study tips

- Read case studies twice: identify the tenant's licensing (Entra ID P1 vs P2, Defender Plan 1 vs Plan 2, E3 vs E5) first, because the correct tool often depends on which features the subscription actually includes.
- Memorize the DNS record map for Microsoft 365: TXT for domain verification, MX to <tenant>.mail.protection.outlook.com, SPF TXT including spf.protection.outlook.com, and CNAME/TXT for DKIM and autodiscover.
- Know which admin center owns each task: Microsoft 365 admin center (tenant, users, licenses), Entra admin center (identity, Conditional Access, PIM), Defender portal (threats, Safe Links/Attachments), and Purview portal (DLP, retention, eDiscovery, Audit).
- Distinguish look-alike features under pressure: PHS vs PTA, Security defaults vs Conditional Access, Safe Attachments vs Safe Links, retention policy vs retention label, and eDiscovery Standard vs Premium.
- Watch for the 'first/immediate step' phrasing: for compromised accounts reset password and revoke sessions; for email auth configure SPF first; and always exclude break-glass accounts before enforcing Conditional Access.

---

Want the full breakdown? See the complete **[MS-102 study guide](https://certgrid.app/study-guide/ms-102-microsoft-365-administrator)** and **[free practice questions](https://certgrid.app/practice/ms-102-microsoft-365-administrator)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

