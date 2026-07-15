# 02 - Describe the Capabilities of Microsoft Entra

This domain is worth 25-30% of the exam. It covers Microsoft Entra ID and its identity types (including agent ID), hybrid identity, authentication methods and MFA, password protection, Conditional Access, Entra roles and RBAC, and the identity protection and governance family: Microsoft Entra ID Governance, access reviews, Privileged Identity Management (PIM), and Microsoft Entra ID Protection.

## Mental model

Microsoft Entra is the identity product family. Microsoft Entra ID is the core cloud identity and access management service inside it. Almost every question in this domain follows the pattern "which Entra capability solves this identity problem?"

| Scenario keyword                              | Likely concept                                          |
| --------------------------------------------- | ------------------------------------------------------- |
| Cloud identity and access management service  | Microsoft Entra ID                                      |
| Sign in without a password                    | Passwordless (Windows Hello, FIDO2, Authenticator)      |
| Something you know, have, and are             | Multifactor authentication (MFA)                        |
| Users reset their own passwords               | Self-service password reset (SSPR)                      |
| Block commonly used weak passwords            | Microsoft Entra Password Protection                     |
| If/then access policy using signals           | Conditional Access                                      |
| Grant admin rights just-in-time               | Privileged Identity Management (PIM)                    |
| Periodically confirm who still needs access   | Access reviews                                          |
| Detect leaked credentials and risky sign-ins  | Microsoft Entra ID Protection                           |
| Manage identity lifecycle joiner-mover-leaver | Microsoft Entra ID Governance                           |
| Identity for an app or service                | Workload identity (service principal, managed identity) |
| Identity for an AI agent                      | Agent ID                                                |
| Partner user in your directory                | External identity (B2B collaboration)                   |
| Sync on-premises AD accounts to the cloud     | Hybrid identity                                         |

## Microsoft Entra ID

Microsoft Entra ID is Microsoft's cloud-based identity and access management service. Organizations use it to let employees, partners, and customers sign in and access resources.

What it secures access to:

| Resource type         | Examples                                               |
| --------------------- | ------------------------------------------------------ |
| Microsoft cloud apps  | Microsoft 365, Azure portal, Dynamics 365              |
| Third-party SaaS apps | Thousands of pre-integrated gallery applications       |
| Internal apps         | Line-of-business and on-premises apps (via connectors) |

Each organization gets a tenant: a dedicated instance of Microsoft Entra ID that holds its users, groups, devices, and app registrations.

## Identity types

Microsoft Entra ID manages several identity types. Know which identity fits which actor.

| Identity type     | Represents                                   | Notes                                                             |
| ----------------- | -------------------------------------------- | ----------------------------------------------------------------- |
| User              | A person (employee, guest)                   | Internal or external, member or guest                             |
| Workload identity | An application or service                    | Includes applications, service principals, and managed identities |
| Managed identity  | An Azure resource that needs to authenticate | Credentials managed automatically; no secrets in code             |
| Device            | A physical device                            | Entra registered, Entra joined, or hybrid joined                  |
| External identity | A user from outside the organization         | B2B collaboration guests, B2B direct connect, customer identities |
| Agent ID          | An AI agent acting in the organization       | Gives agents their own governed, auditable identity in Entra      |

Managed identity flavors:

| Type            | Lifecycle                                   | Sharing                         |
| --------------- | ------------------------------------------- | ------------------------------- |
| System-assigned | Tied to one Azure resource, deleted with it | Cannot be shared                |
| User-assigned   | Standalone resource with its own lifecycle  | Can be shared by many resources |

Device identity options:

| Option           | Typical use                                              |
| ---------------- | -------------------------------------------------------- |
| Entra registered | Personal/BYOD devices signing in with a personal account |
| Entra joined     | Organization-owned devices signed in with a work account |
| Hybrid joined    | Devices joined to on-premises AD and registered in Entra |

Exam anchor: agent ID is called out in the current outline. If a scenario involves giving an AI agent its own identity so its access can be controlled and audited, the answer is agent ID.

## Hybrid identity

Hybrid identity means one user identity works for both on-premises and cloud resources. Accounts are created in on-premises AD DS and synchronized to Microsoft Entra ID using Microsoft Entra Connect (or Entra Cloud Sync).

| Authentication approach       | Where the password is verified                     | Key point                                   |
| ----------------------------- | -------------------------------------------------- | ------------------------------------------- |
| Password hash synchronization | In the cloud (hash of the password hash is synced) | Simplest; works even if on-premises is down |
| Pass-through authentication   | On-premises via lightweight agents                 | Password never stored in the cloud          |
| Federation (AD FS)            | On-premises federation server                      | Most complex; full on-premises control      |

Exam anchor: password hash synchronization does not sync plaintext passwords. It syncs a hash of the hash.

## Authentication methods

Microsoft Entra ID supports a range of authentication methods used for sign-in, MFA, and self-service password reset.

| Method                          | Type                     | Notes                                                 |
| ------------------------------- | ------------------------ | ----------------------------------------------------- |
| Password                        | Something you know       | Weakest on its own                                    |
| Microsoft Authenticator app     | Something you have       | Push notifications, passwordless phone sign-in, codes |
| Windows Hello for Business      | Passwordless / biometric | PIN or biometric tied to the device                   |
| FIDO2 security keys             | Passwordless             | Hardware key, phishing resistant                      |
| Passkeys                        | Passwordless             | FIDO2-based credentials, including in Authenticator   |
| OATH tokens (hardware/software) | Something you have       | Time-based one-time codes                             |
| SMS and voice call              | Something you have       | Weaker; acceptable for some MFA/SSPR scenarios        |
| Temporary Access Pass           | Time-limited code        | For onboarding or recovering passwordless users       |

Factor categories to recognize:

| Category           | Examples                         |
| ------------------ | -------------------------------- |
| Something you know | Password, PIN                    |
| Something you have | Phone, hardware token, FIDO2 key |
| Something you are  | Fingerprint, face (biometrics)   |

## Multifactor authentication (MFA)

MFA requires two or more of the factor categories above. A password plus a code from the same phone still counts as MFA because the categories differ (know + have). Two passwords do not.

| Statement                                           | True or false                               |
| --------------------------------------------------- | ------------------------------------------- |
| Password + SMS code is MFA                          | True (know + have)                          |
| Password + security questions is MFA                | False (both are something you know)         |
| Windows Hello satisfies strong authentication       | True (device + biometric/PIN)               |
| Security defaults enable MFA for all users for free | True (basic protection preset by Microsoft) |

Security defaults are Microsoft's preconfigured baseline: they require MFA registration for all users, enforce MFA for admins, and block legacy authentication. Conditional Access replaces security defaults when finer control is needed.

## Password protection and management

| Capability                          | What it does                                                            |
| ----------------------------------- | ----------------------------------------------------------------------- |
| Self-service password reset (SSPR)  | Users reset their own passwords after verifying with registered methods |
| Microsoft Entra Password Protection | Blocks known weak passwords via a global banned password list           |
| Custom banned password list         | Organization adds its own terms (brand names, locations) to block       |
| On-premises integration             | Password Protection can extend to on-premises AD DS via agents          |

Exam anchor: Password Protection reduces weak passwords; it does not replace MFA or detect leaked credentials (that is ID Protection).

## Conditional Access

Conditional Access is the Zero Trust policy engine of Microsoft Entra ID: if/then statements that evaluate signals and apply access controls. It requires Microsoft Entra ID P1 (or P2) licensing.

| Stage       | Examples                                                                       |
| ----------- | ------------------------------------------------------------------------------ |
| Signals     | User/group, location (IP), device and its state, application, real-time risk   |
| Decision    | Block access, grant access, grant with requirements                            |
| Enforcement | Require MFA, require compliant device, require password change, limit sessions |

Common policy patterns:

| Requirement                                               | Conditional Access answer                         |
| --------------------------------------------------------- | ------------------------------------------------- |
| Require MFA when signing in from outside the office       | Location signal + require MFA                     |
| Block access from specific countries                      | Location signal + block                           |
| Only allow managed, compliant devices for a sensitive app | Device state signal + require compliant device    |
| Force password change on high-risk users                  | Risk signal (from ID Protection) + require change |

Exam anchor: Conditional Access ENFORCES decisions. Entra ID Protection DETECTS risk and feeds it to Conditional Access as a signal.

## Microsoft Entra roles and RBAC

Microsoft Entra roles control permissions to manage identity resources (users, groups, licenses, applications).

| Role concept    | Detail                                                                           |
| --------------- | -------------------------------------------------------------------------------- |
| Built-in roles  | Predefined, e.g. Global Administrator, User Administrator, Billing Administrator |
| Custom roles    | Organization-defined sets of permissions (requires P1)                           |
| Least privilege | Assign the narrowest role that does the job; avoid Global Administrator          |

Entra roles vs Azure RBAC roles:

| Aspect        | Microsoft Entra roles                    | Azure RBAC roles                              |
| ------------- | ---------------------------------------- | --------------------------------------------- |
| Scope         | Entra identity resources (users, groups) | Azure resources (VMs, storage, subscriptions) |
| Examples      | Global Administrator, User Administrator | Owner, Contributor, Reader                    |
| Managed where | Microsoft Entra admin center             | Azure portal (IAM blade)                      |

## Microsoft Entra ID Governance

ID Governance answers: which users should have access to which resources, what are they doing with it, and are the right controls in place? It manages the identity lifecycle: joiner, mover, leaver.

| Capability                     | What it does                                                                                     |
| ------------------------------ | ------------------------------------------------------------------------------------------------ |
| Lifecycle workflows            | Automate joiner/mover/leaver tasks (e.g. disable account on leaving)                             |
| Entitlement management         | Access packages bundle groups, apps, and sites; users request, approvers approve, access expires |
| Access reviews                 | Periodically recertify who still needs group, app, or role access                                |
| Privileged Identity Management | Just-in-time, time-bound elevation for privileged roles                                          |

## Access reviews

Access reviews let organizations regularly confirm that only the right people keep access to groups, applications, and privileged roles. Reviewers can be the users themselves, their managers, or resource owners, and stale access can be removed automatically.

Use an access review when the keyword is "periodically verify" or "recertify" access.

## Privileged Identity Management (PIM)

PIM protects privileged roles in Microsoft Entra ID and Azure. It requires Microsoft Entra ID P2.

| PIM feature       | Meaning                                                  |
| ----------------- | -------------------------------------------------------- |
| Just-in-time      | Role is activated only when needed, not permanently held |
| Time-bound        | Activation expires automatically                         |
| Approval-based    | Activation can require approval                          |
| MFA on activation | Enforce strong authentication to elevate                 |
| Audit and alerts  | Full history of activations; notifications on activation |

Memory hook: PIM = temporary admin. Access reviews = periodic recheck. Entitlement management = packaged, requestable access.

## Microsoft Entra ID Protection

ID Protection automates the detection and remediation of identity-based risks. It requires Microsoft Entra ID P2.

| Risk type    | Question it answers                        | Examples of detections                                                       |
| ------------ | ------------------------------------------ | ---------------------------------------------------------------------------- |
| User risk    | Is this ACCOUNT likely compromised?        | Leaked credentials, anomalous user activity                                  |
| Sign-in risk | Is this SIGN-IN likely not from the owner? | Anonymous IP, atypical travel, unfamiliar sign-in properties, password spray |

What it can do:

- Detect risks using Microsoft's threat intelligence signals.
- Feed risk levels (low, medium, high) into Conditional Access policies for automated response (require MFA, require password change, block).
- Export risk data to a SIEM such as Microsoft Sentinel for investigation.

## Common confusions

| Confusion                                   | Correct idea                                                                    |
| ------------------------------------------- | ------------------------------------------------------------------------------- |
| Conditional Access vs ID Protection         | Conditional Access enforces policy; ID Protection detects risk                  |
| User risk vs sign-in risk                   | Account probably compromised vs this specific sign-in looks suspicious          |
| PIM vs access reviews                       | Just-in-time elevation vs periodic recertification of access                    |
| Entra roles vs Azure RBAC                   | Manage identity resources vs manage Azure resources                             |
| Managed identity vs service principal       | Managed identity is a service principal whose credentials Azure manages for you |
| SSPR vs Password Protection                 | Users reset forgotten passwords vs banning weak passwords                       |
| Federation vs password hash synchronization | Trust-based sign-in on-premises vs verifying a synced hash in the cloud         |
| Security defaults vs Conditional Access     | Free fixed baseline vs licensed, customizable policies                          |

## Exam traps

| Trap                                              | Why people miss it                                                                           |
| ------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| "Password + security questions counts as MFA"     | Both are something you know; MFA needs two different categories.                             |
| "ID Protection blocks risky sign-ins by itself"   | It detects and scores risk; enforcement typically flows through Conditional Access policies. |
| "Password hash sync sends passwords to the cloud" | Only a hash of the password hash is synchronized, never the plaintext.                       |
| "Global Administrator is needed to manage users"  | User Administrator suffices; least privilege is always the exam's preference.                |
| "Guests need new credentials in your tenant"      | B2B collaboration lets guests use their own organization's credentials.                      |
| "Managed identities need stored secrets"          | Their whole point is that Azure manages credentials; no secrets in code.                     |
| "Conditional Access is free"                      | It requires Microsoft Entra ID P1; ID Protection and PIM require P2.                         |

## Mini scenarios

| Scenario                                                                         | Best answer                                       |
| -------------------------------------------------------------------------------- | ------------------------------------------------- |
| Require MFA only when users sign in from outside trusted locations.              | Conditional Access                                |
| Detect that a user's credentials appeared in a public breach dump.               | Microsoft Entra ID Protection (user risk)         |
| Give a helpdesk engineer admin rights for two hours with approval.               | Privileged Identity Management                    |
| Every quarter, managers confirm team members still need access to a finance app. | Access reviews                                    |
| An Azure web app must read secrets from Key Vault without storing credentials.   | Managed identity                                  |
| A partner consultant needs access to a Teams site using their own work account.  | B2B collaboration (external identity)             |
| An AI agent needs a governed, auditable identity to access company data.         | Agent ID                                          |
| Stop employees from choosing passwords containing the company name.              | Custom banned password list (Password Protection) |

## Check yourself

1. What is Microsoft Entra ID and what was it formerly called?
2. Name four identity types Microsoft Entra ID can manage.
3. What are the three hybrid identity authentication approaches?
4. Give three passwordless authentication methods.
5. Why is "password plus security questions" not MFA?
6. What are the three parts of a Conditional Access policy flow?
7. What is the difference between user risk and sign-in risk in ID Protection?
8. Which Entra capability provides just-in-time privileged access, and which license does it need?

## Answer guide

1. Microsoft's cloud-based identity and access management service for users, devices, applications, and external identities.
2. Users, workload identities (applications/service principals/managed identities), devices, external identities (B2B guests), and agent ID for AI agents. (Any four.)
3. Password hash synchronization, pass-through authentication, and federation (AD FS).
4. Windows Hello for Business, FIDO2 security keys (passkeys), and Microsoft Authenticator passwordless phone sign-in.
5. Both factors are "something you know"; MFA requires two or more different factor categories.
6. Signals (user, location, device, app, risk), decision (block or grant), enforcement (require MFA, compliant device, etc.).
7. User risk means the account itself is likely compromised (e.g. leaked credentials); sign-in risk means a specific authentication attempt looks suspicious (e.g. anonymous IP, atypical travel).
8. Privileged Identity Management (PIM); it requires Microsoft Entra ID P2.
