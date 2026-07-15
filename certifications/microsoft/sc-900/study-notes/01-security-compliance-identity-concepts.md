# 01 - Describe the Concepts of Security, Compliance, and Identity

This domain is worth 10-15% of the exam. It covers the vocabulary that every other domain builds on: shared responsibility, defense in depth, Zero Trust, encryption and hashing, Governance, Risk, and Compliance (GRC), and the core identity concepts of authentication, authorization, identity providers, directory services, and federation.

## Mental model

Think of this domain as the "language lesson" before the product tour. The exam usually gives you a short scenario and asks which concept it describes. If you can match the wording to the concept, these questions are fast points.

| Scenario keyword                             | Likely concept                             |
| -------------------------------------------- | ------------------------------------------ |
| "Who secures what" in cloud vs on-premises   | Shared responsibility model                |
| Multiple layers of protection                | Defense in depth                           |
| "Never trust, always verify"                 | Zero Trust                                 |
| Data unreadable without a key                | Encryption                                 |
| One-way fingerprint of data, no key          | Hashing                                    |
| Rules, risk appetite, meeting regulations    | Governance, Risk, and Compliance           |
| Proving who you are                          | Authentication (AuthN)                     |
| What you are allowed to do                   | Authorization (AuthZ)                      |
| Service that creates and verifies identities | Identity provider (IdP)                    |
| Store of users, groups, and computers        | Directory service / Active Directory       |
| Trust between two identity providers         | Federation                                 |
| Identity is the new control plane            | Identity as the primary security perimeter |

## Shared responsibility model

The shared responsibility model defines what the cloud provider secures and what the customer secures. Responsibility shifts with the service model.

| Responsibility                        | On-premises | IaaS      | PaaS      | SaaS      |
| ------------------------------------- | ----------- | --------- | --------- | --------- |
| Information and data                  | Customer    | Customer  | Customer  | Customer  |
| Devices (mobile and PCs)              | Customer    | Customer  | Customer  | Customer  |
| Accounts and identities               | Customer    | Customer  | Customer  | Customer  |
| Identity and directory infrastructure | Customer    | Customer  | Shared    | Shared    |
| Applications                          | Customer    | Customer  | Shared    | Microsoft |
| Network controls                      | Customer    | Customer  | Shared    | Microsoft |
| Operating system                      | Customer    | Customer  | Microsoft | Microsoft |
| Physical hosts, network, datacenter   | Customer    | Microsoft | Microsoft | Microsoft |

Exam anchor: no matter the model, the customer ALWAYS retains responsibility for data, devices, and accounts and identities.

## Defense in depth

Defense in depth uses multiple layers of security so that if one layer is breached, another layer can slow or stop the attack. Confidentiality, integrity, and availability (the CIA triad) are the goals the layers protect.

| Layer               | Example protection                                  |
| ------------------- | --------------------------------------------------- |
| Physical security   | Datacenter access controls, cameras, guards         |
| Identity and access | MFA, Conditional Access, least privilege            |
| Perimeter           | DDoS protection, perimeter firewalls                |
| Network             | Segmentation, NSGs, deny by default                 |
| Compute             | Endpoint protection, patching, closing unused ports |
| Application         | Secure coding, no secrets in code, testing          |
| Data                | Encryption, access controls, classification         |

| CIA element     | Meaning                                      |
| --------------- | -------------------------------------------- |
| Confidentiality | Only authorized people can see the data      |
| Integrity       | Data is not tampered with or altered         |
| Availability    | Data and services are accessible when needed |

## Zero Trust model

Zero Trust assumes breach and treats every request as if it comes from an open, untrusted network. The slogan is "never trust, always verify."

### The three principles

| Principle              | Meaning                                                                 |
| ---------------------- | ----------------------------------------------------------------------- |
| Verify explicitly      | Always authenticate and authorize using all available signals           |
| Least privilege access | Give just-in-time and just-enough access (JIT/JEA), risk-based policies |
| Assume breach          | Segment access, encrypt end to end, use analytics to detect threats     |

### The six foundational pillars

| Pillar         | What Zero Trust asks of it                                   |
| -------------- | ------------------------------------------------------------ |
| Identities     | Verify with strong authentication and least privilege        |
| Devices        | Monitor health and compliance before granting access         |
| Applications   | Discover shadow IT, manage permissions in apps               |
| Data           | Classify, label, and encrypt; protect data wherever it lives |
| Infrastructure | Harden, detect anomalies, block risky behavior               |
| Networks       | Segment, encrypt in transit, avoid flat trusted networks     |

Exam anchor: if a question says "verify every request regardless of network location," the answer is Zero Trust, not defense in depth.

## Encryption and hashing

| Concept               | Key idea                                  | Reversible?        | Example use                         |
| --------------------- | ----------------------------------------- | ------------------ | ----------------------------------- |
| Symmetric encryption  | Same key encrypts and decrypts            | Yes, with the key  | Encrypting a disk or database       |
| Asymmetric encryption | Public key encrypts, private key decrypts | Yes, with key pair | TLS/HTTPS, digital signatures       |
| Hashing               | One-way fixed-length fingerprint of data  | No                 | Storing passwords, integrity checks |
| Salted hash           | Random value added before hashing         | No                 | Defeating precomputed hash attacks  |

| Encryption state      | Meaning                                   | Example                             |
| --------------------- | ----------------------------------------- | ----------------------------------- |
| Encryption at rest    | Data stored on disk is encrypted          | Encrypted storage account, database |
| Encryption in transit | Data moving across a network is encrypted | HTTPS, TLS, VPN                     |

Exam anchor: hashing is NOT encryption. Hashing has no decryption key and is used for passwords and integrity, not for hiding data you need back.

## Governance, Risk, and Compliance (GRC)

GRC is how organizations align their actions with rules, manage uncertainty, and prove they meet obligations.

| Term       | Meaning                                                            | Example                                       |
| ---------- | ------------------------------------------------------------------ | --------------------------------------------- |
| Governance | The rules, policies, and processes an organization sets for itself | A policy requiring MFA for all admin accounts |
| Risk       | Identifying, assessing, and responding to threats to the business  | Ranking the impact of a data breach           |
| Compliance | Meeting external laws, regulations, and standards                  | Complying with GDPR or HIPAA                  |

Related compliance vocabulary that appears on the exam:

| Term             | Meaning                                                       |
| ---------------- | ------------------------------------------------------------- |
| Data residency   | Where data can be stored geographically                       |
| Data sovereignty | Data is subject to the laws of the country where it is stored |
| Data privacy     | Notice and control over how personal data is used             |

## Identity as the primary security perimeter

Traditional security relied on a network perimeter: everything inside the firewall was trusted. Cloud services, remote work, and personal devices broke that model. Today identity is the primary security perimeter: access decisions are made per identity, per request, not per network location.

The four pillars of an identity infrastructure:

| Pillar         | Question it answers                               |
| -------------- | ------------------------------------------------- |
| Administration | How are identities created, updated, and removed? |
| Authentication | How does the identity prove who it is?            |
| Authorization  | What is the verified identity allowed to do?      |
| Auditing       | Who did what, when, and can we prove it?          |

## Authentication vs authorization

| Concept                | Question answered            | Happens | Example                                         |
| ---------------------- | ---------------------------- | ------- | ----------------------------------------------- |
| Authentication (AuthN) | Are you who you say you are? | First   | Entering a password and approving an MFA prompt |
| Authorization (AuthZ)  | What are you allowed to do?  | Second  | Being granted Reader access to a resource       |

Memory hook: AuthN = kNow who you are. AuthZ = your authoriZed rights.

## Identity providers

An identity provider (IdP) creates, maintains, and manages identity information and provides authentication services to applications. Microsoft Entra ID is an example of a cloud-based identity provider.

Key ideas:

- The IdP authenticates the user once and issues a security token to applications.
- This enables single sign-on (SSO): sign in once, access many applications.
- Modern authentication uses open standards such as OAuth 2.0, OpenID Connect, and SAML (recognition only, no protocol depth needed).

| Term                 | Meaning                                                  |
| -------------------- | -------------------------------------------------------- |
| Identity provider    | Central service that verifies identity and issues tokens |
| Single sign-on (SSO) | One sign-in gives access to multiple applications        |
| Security token       | Proof of authentication handed to applications           |

## Directory services and Active Directory

A directory is a hierarchical store of objects such as users, groups, and computers. A directory service stores that data and makes it available to users and administrators.

| Service                                  | Type                   | Best for                                           |
| ---------------------------------------- | ---------------------- | -------------------------------------------------- |
| Active Directory Domain Services (AD DS) | On-premises directory  | Traditional domain-joined Windows networks         |
| Microsoft Entra ID                       | Cloud identity service | Cloud and hybrid apps, SaaS, modern authentication |

AD DS uses protocols like Kerberos and LDAP and does not natively manage mobile devices or SaaS apps. Microsoft Entra ID is not simply "AD in the cloud"; it is a different service designed for internet-based apps and devices.

## Federation

Federation establishes a trust relationship between identity providers so users in one domain can access resources in another domain without creating a second set of credentials.

| Idea                     | Detail                                                           |
| ------------------------ | ---------------------------------------------------------------- |
| Trust                    | The resource's IdP trusts the user's home IdP                    |
| No duplicate credentials | Users sign in with their own IdP; the token is trusted elsewhere |
| Common example           | Signing in to a third-party site with a social or work account   |
| Direction                | Trust is not always bidirectional; it can be one-way             |

Exam anchor: federation = trust between different identity providers. Hybrid identity synchronization (covered in domain 2) = copying account information from on-premises AD to Entra ID. They are not the same thing.

## Common confusions

| Confusion                          | Correct idea                                                                                                     |
| ---------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| Zero Trust vs defense in depth     | Zero Trust is a trust model (verify every request); defense in depth is layered controls                         |
| Authentication vs authorization    | AuthN proves identity first; AuthZ grants rights afterward                                                       |
| Encryption vs hashing              | Encryption is reversible with a key; hashing is one-way with no key                                              |
| Governance vs compliance           | Governance is your own rules; compliance is meeting external rules                                               |
| Federation vs SSO                  | Federation is trust between IdPs; SSO is one sign-in for many apps (federation enables SSO across organizations) |
| Data residency vs data sovereignty | Where data sits vs whose laws apply to it                                                                        |

## Exam traps

| Trap                                                 | Why people miss it                                                             |
| ---------------------------------------------------- | ------------------------------------------------------------------------------ |
| "In SaaS, Microsoft manages everything"              | The customer always keeps data, devices, and accounts and identities.          |
| "Hashing protects data you need to read later"       | Hashing is one-way. Use encryption when data must be recovered.                |
| "Zero Trust means trusting the corporate network"    | Zero Trust treats every network, including corporate, as untrusted.            |
| "Authorization verifies the user's password"         | Password checks are authentication. Authorization happens after.               |
| "Active Directory and Entra ID are the same product" | AD DS is on-premises with Kerberos/LDAP; Entra ID is a cloud identity service. |
| "Federation copies user accounts between systems"    | Federation is a trust relationship; no accounts are duplicated.                |

## Mini scenarios

| Scenario                                                                                | Best answer                       |
| --------------------------------------------------------------------------------------- | --------------------------------- |
| A company wants every access request verified regardless of where it originates.        | Zero Trust model                  |
| An architect stacks MFA, firewalls, NSGs, and encryption so no single failure is fatal. | Defense in depth                  |
| Passwords must be stored so they can be verified but never read back.                   | Hashing (with salt)               |
| A regulator requires customer data to stay within national borders.                     | Data residency / data sovereignty |
| Users of a partner organization access your app using their own credentials.            | Federation                        |
| After signing in, a user is granted permission to read but not delete files.            | Authorization                     |
| A company defines its own policy that all admins must use MFA.                          | Governance                        |
| A directory of users, groups, and computers runs on domain controllers on-premises.     | Active Directory Domain Services  |

## Check yourself

1. In the shared responsibility model, which three things does the customer always retain responsibility for?
2. What are the three principles of Zero Trust?
3. What are the six foundational pillars of Zero Trust?
4. What is the key difference between encryption and hashing?
5. Which comes first in a sign-in flow: authentication or authorization?
6. What does an identity provider do?
7. How is federation different from synchronizing accounts to the cloud?
8. What does "identity is the primary security perimeter" mean?

## Answer guide

1. Data (information), devices, and accounts and identities.
2. Verify explicitly, use least privilege access, and assume breach.
3. Identities, devices, applications, data, infrastructure, and networks.
4. Encryption is reversible with a key; hashing is a one-way function with no key.
5. Authentication. Authorization only happens after identity is proven.
6. It creates, maintains, and manages identities and authenticates them, issuing security tokens that applications trust (enabling SSO).
7. Federation creates a trust between two identity providers so no duplicate credentials are needed; synchronization copies account objects from on-premises AD to Microsoft Entra ID.
8. Access decisions are made per identity and per request instead of trusting anything inside a network boundary, because cloud apps and remote work broke the traditional network perimeter.
