# SC-300: Microsoft Identity and Access Administrator - Study Cheatsheet

SC-300 (Microsoft Identity and Access Administrator) validates your ability to design and operate identity and access in Microsoft Entra ID, covering identity provisioning, authentication, application access, and identity governance. It targets identity administrators, security engineers, and IT professionals who manage Entra ID tenants, Conditional Access, and privileged access. The exam is 120 minutes, scored 1000 with 700 to pass, and draws from roughly 644 question scenarios.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | SC-300 |
| Credential | SC-300: Microsoft Identity and Access Administrator |
| Level | Intermediate |
| Practice mock length | ~50 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Implement Identities in Microsoft Entra ID | ~26% |
| 2 | Implement Authentication and Access Management | ~25% |
| 3 | Implement Access Management for Applications | ~24% |
| 4 | Plan and Implement Identity Governance | ~25% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Implement Identities in Microsoft Entra ID

- A UPN suffix used for cloud sign-in must be a verified, internet-routable domain; non-routable suffixes such as contoso.local cannot be used, so add an alternate routable UPN suffix in Active Directory Domains and Trusts, update users, then resync.
- Entra Connect has three sign-in options: Password Hash Synchronization (PHS), Pass-through Authentication (PTA), and Federation with AD FS; Seamless SSO can be layered on PHS or PTA but not on federation.
- PHS stores a hash-of-a-hash of the on-prem password in Entra ID and is the recommended default; it also enables leaked-credential detection in Identity Protection.
- Federation with AD FS keeps credential validation entirely on-premises (no password material in the cloud) and returns only a token; PHS can be enabled alongside AD FS as a backup authentication method and for disaster recovery.
- When an on-prem account disable is not reflected in the cloud, the most common cause is a stalled sync scheduler; check the Synchronization Service Manager for errors and confirm the delta sync is running (default sync cycle is every 30 minutes).
- Microsoft Entra Cloud Sync uses a lightweight provisioning agent and supports multiple disconnected AD forests; a single classic Entra Connect server can also use multiple AD connectors to sync multiple forests.

### Domain 2 - Implement Authentication and Access Management

- Conditional Access policies combine assignments (users, target resources, conditions) with access controls (grant/session); a policy with no matching condition simply does not apply and imposes no requirement.
- Authentication strength is a grant control that requires a specific credential class; the built-in Phishing-resistant MFA strength permits only FIDO2 security keys, Windows Hello for Business, and certificate-based authentication.
- Sign-in frequency is a session control; pairing a named location with a longer sign-in frequency (e.g., 12 hours) reduces MFA-fatigue prompts on trusted shared kiosks.
- Conditional Access conditions include sign-in risk and user risk (Identity Protection), device platform, client apps, locations, and risk-based controls; risk policies require Entra ID P2.
- To block legacy authentication, target client apps = Exchange ActiveSync clients and Other clients with Grant = Block access, because legacy protocols cannot perform modern MFA.
- Self-Service Password Reset (SSPR): enable for the target scope, set 'number of methods required to reset' (1 or 2), and offer multiple available methods; office phone is only selectable as an SSPR method when populated and enabled by admin.

### Domain 3 - Implement Access Management for Applications

- An app registration is the global, single definition of an application (object lives in the home tenant); a service principal is the per-tenant local instance created when the app is added or consented to in a tenant.
- Delegated permissions act on behalf of a signed-in user and are limited to that user's rights; application permissions (app-only) operate at tenant scope and always require admin consent.
- Low-impact delegated permissions such as User.Read can be self-consented by users; higher-impact permissions like Mail.Send typically require admin consent under tenant consent policy.
- A daemon or background service with no signed-in user uses the OAuth 2.0 client credentials flow with application permissions (e.g., Calendars.Read) and authenticates with a client secret or, preferably, a client certificate.
- Certificate credentials are more secure than client secrets because the private key never leaves the client and is not transmitted; secrets and certificates are managed under App registration > Certificates & secrets.
- Microsoft Entra modern auth protocols are OpenID Connect and OAuth 2.0 (OIDC for authentication/identity, OAuth 2.0 for authorization/access tokens).

### Domain 4 - Plan and Implement Identity Governance

- Entitlement management bundles resources (groups, Teams, SharePoint sites, apps) into an access package; users request it from a self-service catalog, governed by assignment policies, approval workflows, and expiration.
- An access-package assignment policy with a fixed expiration (e.g., 6 months) automatically removes all of the package's access when the term ends; managed under Identity Governance > Entitlement management > Catalogs > Access packages.
- Connected organizations define external Entra/partner directories whose users are allowed to request access packages, enabling governed B2B collaboration.
- Access reviews recertify membership/access on a schedule (e.g., quarterly or 90-day recurrence); choosing reviewers as group owners or self-review, with auto-apply results, automatically removes access when reviewers decline or do not respond.
- For guest governance, combine a recurring access review of inactive guests (auto-remove) with a terms of use policy enforced via a Conditional Access grant control requiring ToU acceptance for the target app.
- Privileged Identity Management (PIM) makes roles eligible rather than permanently assigned; users activate just-in-time, and PIM requires Entra ID P2.

## Study tips

- Read each scenario for the explicit constraint that eliminates options - phrases like 'passwords must never be stored in the cloud' (forces federation over PHS) or 'no inbound firewall ports' (forces Application Proxy) are the deciding clue.
- Know the licensing tiers cold: Conditional Access and dynamic groups need Entra ID P1, while Identity Protection risk policies, PIM, and access reviews need Entra ID P2 - wrong-tier answers are common distractors.
- Distinguish app registration vs service principal, and delegated vs application permissions, before answering any app-access question; these two pairs underpin most Domain 3 items.
- For Conditional Access questions, evaluate assignments and conditions first - if no condition matches, the policy does not apply and requires nothing, which is frequently the correct trap answer.
- When two requirements appear in one scenario (e.g., recertify guests AND require ToU acceptance), expect a two-part answer using two distinct features rather than a single control.

---

Want the full breakdown? See the complete **[SC-300 study guide](https://certgrid.app/study-guide/sc-300-microsoft-identity-and-access-administrator)** and **[free practice questions](https://certgrid.app/practice/sc-300-microsoft-identity-and-access-administrator)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

