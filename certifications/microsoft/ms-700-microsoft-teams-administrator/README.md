# MS-700: Microsoft Teams Administrator - Study Cheatsheet

MS-700: Microsoft Teams Administrator validates your ability to plan, deploy, configure, manage, secure, and monitor Microsoft Teams across collaboration, meetings, and calling workloads. It targets Teams administrators who configure policies, governance, telephony (Teams Phone), and compliance for an organization, and who collaborate with networking, security, telephony, and identity teams. The 120-minute exam has a passing score of 700 and tests both portal-based configuration (Teams admin center) and PowerShell/Microsoft Graph administration.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | MS-700 |
| Credential | MS-700: Microsoft Teams Administrator |
| Level | Intermediate |
| Practice mock length | ~50 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-06-24 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Configure and Manage Teams | ~26% |
| 2 | Manage Chat, Calling, and Meetings | ~24% |
| 3 | Manage Teams and App Policies | ~24% |
| 4 | Monitor, Report, and Manage Compliance | ~25% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Configure and Manage Teams

- The Microsoft Teams admin center (https://admin.teams.microsoft.com) is the central portal for org-wide settings, policies, teams/channels, users, and app management; the Microsoft Teams PowerShell module (Connect-MicrosoftTeams) provides scripted and bulk administration.
- Teams has no identity store of its own - every user, group, and team membership is backed by Microsoft Entra ID, which handles authentication, MFA, Conditional Access, and group membership resolution.
- Every user must have a Microsoft 365 license that includes Teams (for example Business Basic/Standard or enterprise E3/E5) explicitly assigned to their account before they can use Teams.
- Policies can be assigned three ways: org-wide (Global default), direct per-user assignment, or group policy assignment to a security/M365 group; direct user assignment takes precedence over group assignment, and group assignment uses a ranking when a user is in multiple groups.
- Policy packages are bundles of predefined policies tailored to a role (for example Education Teacher, Healthcare Clinical Worker, Frontline Worker) to simplify assignment of multiple policy types at once.
- Creating a team automatically provisions a Microsoft 365 Group, a SharePoint site (team files live in the channel's document library), a shared mailbox, and a OneNote notebook; 1:1 and group chat files are stored in the sender's OneDrive.

### Domain 2 - Manage Chat, Calling, and Meetings

- A standard channel is visible to all members of the parent team; a private channel has its own membership roster (a subset of the team) and its own dedicated SharePoint site; a shared channel can be shared with people inside and outside the org without switching tenants or creating guest accounts.
- Shared channels use Microsoft Entra B2B direct connect (cross-tenant access settings) so external partners participate without guest accounts or extra licenses - the preferred approach for ongoing partner collaboration over creating guest accounts.
- External access (federation) lets users in external domains chat, call, and meet with your users without being added as guests; guest access invites external users into specific teams/channels with broader membership rights - these are two distinct, independently configured mechanisms.
- Messaging policies govern chat features such as editing/deleting sent messages, Giphy and sticker availability, read receipts, immersive reader, and chat permissions for users.
- App permission policies control which apps (Microsoft, third-party, custom) users can install; app setup policies control which apps are pinned and pre-installed and the app bar layout for users.
- Meeting policies control who can present, lobby/admit (bypass) behavior, cloud recording, transcription, live captions, and other meeting features; meeting recordings are stored in OneDrive (for ad-hoc/private meetings) or the channel SharePoint site (for channel meetings).

### Domain 3 - Manage Teams and App Policies

- Meeting policies are applied per user or org-wide and control cloud recording, who can present, lobby/access behavior, transcription/translation, and meeting feature availability; the policy assigned to the organizer often governs the meeting's behavior.
- Teams Phone combined with a Calling Plan or Direct Routing turns Teams into a full telephony client for making/receiving PSTN calls with assigned phone numbers.
- An auto attendant is a resource account providing an IVR voice menu; a call queue is a resource account distributing calls to agents using methods like attendant routing, serial, round robin, or longest idle, with options for hold music and overflow/timeout handling.
- App permission policies allow or block apps tenant-wide or per user (allow all, allow specific, block specific, block all); app setup policies pin and pre-install specific apps and set the order of pinned apps.
- Org-wide app settings control whether users can upload/sideload custom apps and whether third-party apps are allowed; these global toggles override what individual policies can enable.
- Assign app setup (and other) policies to a department's security/M365 group via group policy assignment so membership changes are handled automatically without per-user reassignment.

### Domain 4 - Monitor, Report, and Manage Compliance

- Teams usage reports in the Teams admin center and Microsoft 365 admin center report on adoption - active users, messages, meetings, calls, and device usage - and help identify inactive or non-active licensed users for license reclamation.
- The Call Quality Dashboard (CQD) aggregates data across millions of calls to surface organization-wide quality trends (latency, jitter, packet loss, codec) by subnet/building; per-call (per-user) analytics in Users > select user > Meetings & calls show per-session diagnostics for troubleshooting a specific user's call.
- Upload building/subnet/tenant data (the building data file) into CQD so reports can map subnets to physical locations, distinguishing wired versus Wi-Fi and inside versus outside the corporate network.
- Review CQD reports/templates on a schedule, including the CQD Power BI connector/templates, to track quality trends by location over time.
- Microsoft Purview retention policies can be scoped specifically to Teams chats and channel messages with retain, delete, or retain-then-delete actions; Teams retention is configured separately from Exchange/SharePoint locations.
- Use New-RetentionCompliancePolicy with -TeamsChannelLocation (channel messages) and -TeamsChatLocation (1:1 and group chats) to create Teams retention policies in PowerShell.

## Study tips

- Master the policy assignment hierarchy: Global (org-wide) default applies unless overridden; direct user assignment wins over group assignment; among multiple groups, the assignment ranking decides. Many questions hinge on which policy a specific user effectively receives.
- Know the right tool for the right scope: CQD for organization-wide quality trends by location, and per-user call analytics (Meetings & calls) for troubleshooting one user's specific call. Expect scenarios that ask you to pick between them.
- Memorize the three PSTN connectivity options (Calling Plan, Direct Routing, Operator Connect) and when each applies, plus that auto attendants and call queues both require resource accounts with a (free) Virtual User license.
- For compliance scenarios, distinguish retention policies (keep/delete), eDiscovery (search/hold), information barriers (block communication), DLP (block sensitive sharing), and compliance recording (certified partner) - match the requirement to the exact feature.
- Be comfortable with PowerShell cmdlet patterns: Connect-MicrosoftTeams, Set-TeamArchivedState, New-RetentionCompliancePolicy -TeamsChannelLocation, New-ComplianceSearch -ExchangeLocation, and New-CaseHoldPolicy/New-CaseHoldRule for case holds.

---

Want the full breakdown? See the complete **[MS-700 study guide](https://certgrid.app/study-guide/ms-700-microsoft-teams-administrator)** and **[free practice questions](https://certgrid.app/practice/ms-700-microsoft-teams-administrator)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

