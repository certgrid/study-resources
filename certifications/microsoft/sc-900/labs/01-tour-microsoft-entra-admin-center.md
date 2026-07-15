# Lab 01 - Tour the Microsoft Entra Admin Center

The Microsoft Entra admin center is where identity questions on SC-900 come to life. This lab is a read-only tour so you can recognize where every domain 2 capability lives.

## Time Needed

20-25 minutes.

## What You Will Learn

- The layout of the Microsoft Entra admin center
- Where users, groups, devices, and applications live
- Where Conditional Access, ID Protection, and ID Governance appear in the menu
- Which features show "upgrade" prompts because they need P1 or P2

## SC-900 Concepts Covered

| Concept             | Where you see it in the lab                       |
| ------------------- | ------------------------------------------------- |
| Microsoft Entra ID  | The whole admin center is its management surface  |
| Identity types      | Users, Groups, Devices, App registrations menus   |
| Conditional Access  | Protection section (view-only without P1)         |
| ID Protection       | Protection section (view-only without P2)         |
| ID Governance       | Identity governance section (PIM, access reviews) |
| External identities | External Identities menu (B2B collaboration)      |

## Steps

### 1. Sign in

1. Go to entra.microsoft.com with your lab account.
2. Notice the left navigation: **Identity**, **Protection**, **Identity governance** (naming can shift slightly over time).

### 2. Explore Identity

1. Open **Identity** > **Overview**. Note tenant name, tenant ID, and basic stats.
2. Open **Users**. This is where member and guest users appear.
3. Open **Groups**. Note the group types offered.
4. Open **Devices** > **Overview**. Look for the join types: Entra registered, Entra joined, hybrid joined.
5. Open **Applications** > **Enterprise applications** to see where SaaS apps integrate for SSO.

### 3. Explore Protection

1. Open **Protection** > **Conditional Access**. View the policies list (likely empty). Open **Create new policy** and READ the sections: users, target resources, conditions, grant controls. Do not save anything.
2. Open **Protection** > **Identity Protection** if visible. Note the risk report names: risky users, risky sign-ins, risk detections.
3. Open **Protection** > **Authentication methods** to see the methods you studied: Authenticator, FIDO2, SMS, Temporary Access Pass.
4. Open **Protection** > **Password reset** to see SSPR settings.

### 4. Explore Identity governance

1. Open **Identity governance** > **Privileged Identity Management**. Note the "upgrade to P2" message if unlicensed.
2. Open **Access reviews** and **Entitlement management** to see where they live.

### 5. Explore External Identities

1. Open **External Identities**. Note B2B collaboration settings and guest invite options.

## Clean Up

Nothing was created. Sign out if you are done for the day.

## Success Criteria

You are done when you can explain:

- Where you would create a user vs a group vs invite a guest
- Which menu holds Conditional Access and what its policy sections are
- Which features prompted for P1 or P2 licensing
- The difference between the Protection and Identity governance sections
