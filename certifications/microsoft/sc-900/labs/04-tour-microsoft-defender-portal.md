# Lab 04 - Tour the Microsoft Defender Portal

The Microsoft Defender portal (security.microsoft.com) is the home of Microsoft Defender XDR. This read-only tour helps you recognize the portal features named in the official outline.

## Time Needed

20-25 minutes.

## What You Will Learn

- The layout of the Microsoft Defender portal
- Where incidents and alerts are unified
- Where advanced hunting, threat intelligence, and threat analytics live
- Where Microsoft Secure Score is found

## SC-900 Concepts Covered

| Concept                   | Where you see it in the lab                  |
| ------------------------- | -------------------------------------------- |
| Microsoft Defender portal | The portal itself                            |
| Defender XDR incidents    | Incidents & alerts menu                      |
| Advanced hunting          | Hunting menu (KQL)                           |
| Threat intelligence       | Threat intelligence / Threat analytics menus |
| Microsoft Secure Score    | Exposure management / Secure score           |
| Defender member services  | Settings and menu areas per service          |

## Access Note

A plain Azure free account may show a limited portal. A Microsoft 365 Business Premium or E5 trial (Lab 00 options) shows the full experience. Everything in this lab is view-only either way.

## Steps

### 1. Sign in

1. Go to security.microsoft.com with your lab account.
2. Skim the left navigation top to bottom before clicking anything.

### 2. Incidents and alerts

1. Open **Incidents & alerts**.
2. Note the idea: one INCIDENT groups related ALERTS from email, endpoints, identities, and apps. This correlation is the core Defender XDR exam point.

### 3. Hunting

1. Open **Hunting** > **Advanced hunting**.
2. Look at the schema tables (email, device, identity data). Queries use KQL, the same language as Sentinel. Do not run anything large; just recognize the surface.

### 4. Threat intelligence

1. Open **Threat intelligence** > **Threat analytics**.
2. Read one report title: these are Microsoft researcher writeups on active threats.
3. If visible, open the **Intel profiles** area: threat actors and their tooling (Defender TI).

### 5. Secure Score

1. Open **Exposure management** (or search Secure Score in the portal).
2. Open **Microsoft Secure Score**. Note that this score covers the Microsoft 365 environment; Defender for Cloud has a SEPARATE secure score for Azure workloads (Lab 08 compares them).

### 6. Map the member services

1. Open **Settings** and note the per-service areas: **Endpoints** (Defender for Endpoint), **Email & collaboration** (Defender for Office 365), **Cloud apps** (Defender for Cloud Apps), **Identities** (Defender for Identity).
2. For each, say out loud which asset it protects.

## Clean Up

Nothing was created.

## Success Criteria

You are done when you can explain:

- What an incident is compared to an alert
- Which four asset classes Defender XDR spans
- Where advanced hunting and threat analytics live
- Which Secure Score this portal shows, and which product holds the other secure score
