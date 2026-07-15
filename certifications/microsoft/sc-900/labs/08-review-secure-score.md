# Lab 08 - Review Secure Score

SC-900 loves the "two secure scores" distinction: Microsoft Secure Score in the Defender portal and the secure score in Microsoft Defender for Cloud. This lab visits both.

## Time Needed

15-20 minutes.

## What You Will Learn

- What Microsoft Secure Score measures and where it lives
- What the Defender for Cloud secure score measures and where it lives
- How recommendations and improvement actions raise each score
- How these differ from compliance score

## SC-900 Concepts Covered

| Concept                                | Where you see it in the lab                      |
| -------------------------------------- | ------------------------------------------------ |
| Microsoft Secure Score                 | Defender portal exposure/secure score page       |
| Defender for Cloud / CSPM              | Azure portal Defender for Cloud overview         |
| Recommendations                        | Both portals list prioritized hardening actions  |
| Security posture vs compliance posture | You contrast secure scores with compliance score |

## Steps

### 1. Microsoft Secure Score (Defender portal)

1. Go to security.microsoft.com.
2. Open **Microsoft Secure Score** (under Exposure management, or via search).
3. Note the score percentage and browse **Improvement actions**.
4. Read one action: each shows points, the product area (identity, apps, devices), and implementation guidance.

### 2. Secure score in Defender for Cloud (Azure portal)

1. Go to portal.azure.com and open **Microsoft Defender for Cloud**.
2. On **Overview**, find the secure score for your subscription.
3. Open **Recommendations** and read two or three (e.g. MFA-related or storage hardening recommendations).
4. Open **Environment settings** briefly: note the foundational CSPM features are free, while Defender plans (workload protection) are paid. Do NOT enable paid plans.

### 3. Contrast the two scores

Fill this in from what you saw:

| Score                           | Portal                 | Measures                          |
| ------------------------------- | ---------------------- | --------------------------------- |
| Microsoft Secure Score          | security.microsoft.com | Microsoft 365 environment posture |
| Defender for Cloud secure score | portal.azure.com       | Azure/multicloud workload posture |

### 4. Add the third score

From Lab 06, recall compliance score in Compliance Manager. Three scores, three questions:

| Score                    | Question it answers                       |
| ------------------------ | ----------------------------------------- |
| Microsoft Secure Score   | How secure is my Microsoft 365 setup?     |
| Defender for Cloud score | How secure are my cloud workloads?        |
| Compliance score         | How am I progressing against regulations? |

## Clean Up

Nothing was created. Confirm you did not enable any paid Defender plans in Environment settings.

## Success Criteria

You are done when you can explain:

- Which portal holds each secure score
- What kind of items raise each score
- Why compliance score is not a security score
- Which Defender for Cloud features are free vs paid
