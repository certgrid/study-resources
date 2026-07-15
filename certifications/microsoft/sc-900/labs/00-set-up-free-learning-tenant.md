# Lab 00 - Set Up a Free Learning Tenant

SC-900 labs are mostly read-only portal tours, but you need a Microsoft Entra tenant to explore. This lab sets one up safely with cost awareness from the start.

## Time Needed

20-30 minutes.

## What You Will Learn

- What a Microsoft Entra tenant is
- Free options for getting a learning tenant
- Which SC-900 features need paid licenses (and how to avoid surprise costs)
- How to protect your learning account with MFA

## SC-900 Concepts Covered

| Concept               | Where you see it in the lab                             |
| --------------------- | ------------------------------------------------------- |
| Tenant                | You create a dedicated Entra ID instance                |
| Identity provider     | Entra ID authenticates your new account                 |
| MFA                   | You register a second factor for your admin account     |
| Shared responsibility | Your account security is your responsibility            |
| Licensing (P1/P2)     | You learn which features are view-only without licenses |

## Cost Warning

- An Azure free account requires a credit card for verification but nothing in these labs needs to create paid resources unless a lab explicitly warns you (Sentinel in Lab 05).
- Free trials of Microsoft Entra ID P2 or Microsoft 365 E5 exist but auto-expire; do NOT add payment methods to them.
- Never use a production or employer tenant for labs.

## Steps

### 1. Choose a tenant option

| Option                                                | Good for                                     | Cost                     |
| ----------------------------------------------------- | -------------------------------------------- | ------------------------ |
| Azure free account                                    | Entra ID, Defender for Cloud, Sentinel trial | Free tier + card on file |
| Microsoft 365 Developer Program (if available to you) | Defender portal, Purview                     | Free when eligible       |
| Microsoft 365 Business Premium trial                  | Full Defender + Purview experience           | Free for trial period    |

For most SC-900 labs, an Azure free account is enough. The Defender and Purview tours (Labs 04, 06, 08) are richer with a Microsoft 365 trial; you can still follow along with screenshots in Microsoft Learn if you skip the trial.

### 2. Create the account

1. Go to the Azure free account page and sign up with a NEW email dedicated to learning.
2. Complete identity verification.
3. Sign in to the Azure portal to confirm the subscription exists.

### 3. Find your tenant

1. Go to the Microsoft Entra admin center: entra.microsoft.com.
2. Sign in with your new account.
3. Select **Identity** > **Overview** and note your tenant name and tenant ID.

### 4. Register MFA

1. Go to My Security Info (mysignins.microsoft.com/security-info).
2. Add the Microsoft Authenticator app as a sign-in method.
3. Test a sign-out and sign-in to see the MFA prompt.

### 5. Record your lab notes

Write down:

```text
Tenant name:
Tenant ID:
Admin account:
MFA method registered:
```

## Clean Up

Nothing to clean up yet. Keep this tenant for all remaining labs.

## Success Criteria

You are done when you can explain:

- What a Microsoft Entra tenant is
- Why you should never run labs in a production tenant
- Which factor categories your sign-in now uses (something you know + something you have)
- Which labs may involve cost if you go beyond view-only steps
