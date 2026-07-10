# Lab 01 - Create Users and Groups with Bulk Operations

Identity is the biggest AZ-104 domain. This lab creates users the three ways the exam mentions (portal, bulk CSV, guest invite) and builds the group types you must tell apart.

## Time Needed

25-30 minutes.

## What You Will Learn

- How to create member users and what properties matter (usage location)
- How bulk create with a CSV works
- How guest (B2B) invitations work
- The difference between assigned and dynamic membership

## AZ-104 Concepts Covered

| Concept              | Where you see it in the lab                     |
| -------------------- | ----------------------------------------------- |
| Member vs guest user | You create one of each                          |
| Bulk operations      | You download and inspect the CSV template       |
| Usage location       | You set it and see why licenses need it         |
| Security groups      | You create assigned membership groups           |
| Dynamic membership   | You review the rule builder (needs Entra ID P1) |
| SSPR                 | You locate the reset policy settings            |

## Cost Warning

Free. Users and groups do not bill. If your tenant lacks Entra ID P1, view the dynamic membership screens without saving.

## Steps

### 1. Create a user in the portal

1. Search for **Microsoft Entra ID** and open **Users**.
2. Select **New user > Create new user**.
3. User principal name: `lab.user1`, display name: `Lab User1`, auto-generate the password.
4. Under Properties, set **Usage location** to your country. Remember: no usage location, no license assignment.
5. Create the user.

### 2. Inspect bulk create

1. In **Users**, select **Bulk operations > Bulk create**.
2. Download the CSV template and open it: note the required columns (name, user principal name, initial password, block sign in).
3. You do not need to upload anything; the exam tests that bulk create/invite/delete work through CSV templates here.

### 3. Invite a guest user

1. Select **New user > Invite external user**.
2. Use a personal email address you control.
3. Note the user type after creation: **Guest**. Guests sign in with their own credentials and can still receive RBAC roles.

### 4. Create security groups

1. Open **Groups > New group**.
2. Group type: **Security**, name: `grp-az104-admins`, membership type: **Assigned**, add `Lab User1` as a member.
3. Create a second group `grp-az104-viewers` the same way.
4. Start creating a third group and switch membership type to **Dynamic User** (if licensed): open the rule builder and read a sample rule like `user.department -eq "Sales"`. Cancel without saving if you prefer.

### 5. Locate SSPR settings

1. In Microsoft Entra ID, open **Password reset**.
2. Note the three scopes: **None**, **Selected** (a group), **All**.
3. Open **Authentication methods** and count how many methods can be required. Do not enable anything tenant-wide in a work tenant.

## Clean Up

Keep `grp-az104-admins`, `grp-az104-viewers`, and `Lab User1`; the RBAC lab uses them. Delete the guest invitation if you used a real external address you will not need again.

## Success Criteria

You are done when you can explain:

- Why usage location must be set before assigning a license
- How a guest user differs from a member user, and what a guest can still receive (RBAC roles)
- Assigned vs dynamic membership, and which license dynamic requires
- How SSPR is scoped (None / Selected group / All)
