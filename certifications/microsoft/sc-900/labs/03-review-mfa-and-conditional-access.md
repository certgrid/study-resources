# Lab 03 - Review MFA and Conditional Access Options

Conditional Access is one of the most tested SC-900 topics. This lab walks the policy builder without turning anything on, so you can see signals, decisions, and enforcement with zero risk.

## Time Needed

20-25 minutes.

## What You Will Learn

- Where authentication methods and MFA settings live
- The anatomy of a Conditional Access policy: assignments, conditions, grant controls
- What report-only mode is
- Where security defaults are configured

## SC-900 Concepts Covered

| Concept                | Where you see it in the lab                            |
| ---------------------- | ------------------------------------------------------ |
| Authentication methods | Authentication methods policy list                     |
| MFA                    | Require multifactor authentication grant control       |
| Conditional Access     | The policy builder: signals to decision to enforcement |
| Security defaults      | Tenant properties toggle                               |
| Zero Trust             | Verify explicitly appears as policy logic              |

## Cost / Safety Warning

Do NOT enable any Conditional Access policy in this lab. A misconfigured policy can lock you out of your own tenant. Keep every policy in **Report-only** or discard it. Creating policies requires P1; on a free tenant this may be view-only, which is fine.

## Steps

### 1. Review authentication methods

1. In the Microsoft Entra admin center, open **Protection** > **Authentication methods** > **Policies**.
2. For each method (Microsoft Authenticator, FIDO2 security key, SMS, Temporary Access Pass, third-party OATH tokens), note whether it can satisfy MFA, passwordless, or both.

### 2. Review security defaults

1. Open **Identity** > **Overview** > **Properties**.
2. Find **Security defaults** and read what it enables (MFA registration, admin MFA, blocking legacy authentication). Do not change it.

### 3. Walk the Conditional Access policy builder

1. Open **Protection** > **Conditional Access** > **Create new policy**.
2. Map each blade to the exam model WITHOUT saving:

| Builder section  | Exam concept                        |
| ---------------- | ----------------------------------- |
| Users            | Signal: who is signing in           |
| Target resources | Signal: which app is requested      |
| Network          | Signal: location/IP                 |
| Conditions       | Signals: device platform, risk      |
| Grant            | Decision: block or grant + controls |
| Session          | Enforcement: limited experiences    |

3. In **Grant**, read the controls: require multifactor authentication, require device to be marked compliant, require password change.
4. In **Conditions**, open **Sign-in risk** and **User risk** to see where Entra ID Protection feeds in.
5. Set **Enable policy** to **Report-only** and then select **Discard** / close without creating.

### 4. Review policy templates

1. In Conditional Access, look at **New policy from template**.
2. Read the template names (e.g. require MFA for admins, block legacy authentication). These match common exam scenarios.

## Clean Up

Nothing should have been saved. Confirm the Conditional Access policies list is unchanged.

## Success Criteria

You are done when you can explain:

- The three stages of Conditional Access: signals, decision, enforcement
- Three signals a policy can evaluate and three grant controls it can require
- The difference between security defaults and Conditional Access
- How user risk and sign-in risk from ID Protection plug into a policy
