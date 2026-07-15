# Lab 02 - Create a User and a Group

Creating a user and a group makes the identity types from domain 2 concrete. This is the only Entra lab where you create objects; Lab 09 removes them.

## Time Needed

15-20 minutes.

## What You Will Learn

- How cloud identities are created in Microsoft Entra ID
- Member vs guest users
- Security groups vs Microsoft 365 groups
- Assigned vs dynamic membership

## SC-900 Concepts Covered

| Concept         | Where you see it in the lab                       |
| --------------- | ------------------------------------------------- |
| Cloud identity  | You create a user that exists only in Entra ID    |
| User types      | Member (created) vs guest (invite option)         |
| Groups          | You create a security group                       |
| Authorization   | Group membership is how access is usually granted |
| Least privilege | You avoid granting any admin roles                |

## Steps

### 1. Create a user

1. In the Microsoft Entra admin center, open **Identity** > **Users**.
2. Select **New user** > **Create new user**.
3. Use values like:

```text
User principal name: lab.user1@<yourtenant>.onmicrosoft.com
Display name: Lab User1
```

4. Let the portal auto-generate the password and note it somewhere temporary.
5. On the assignments step, do NOT assign any roles. Create the user.

### 2. Observe the invite option

1. Back on **Users**, open **New user** again and look at **Invite external user**.
2. Read the fields, then CANCEL without inviting. This is B2B collaboration: the guest would sign in with their own credentials.

### 3. Create a security group

1. Open **Identity** > **Groups** > **All groups** > **New group**.
2. Choose:

| Setting         | Value           |
| --------------- | --------------- |
| Group type      | Security        |
| Group name      | sc900-lab-group |
| Membership type | Assigned        |

3. Add Lab User1 as a member and create the group.

### 4. Look at dynamic membership

1. Open **New group** again and switch **Membership type** to see **Dynamic user** (may require P1; view only).
2. Cancel without creating.

### 5. Test the new user (optional)

1. In a private browser window, sign in as lab.user1 with the temporary password.
2. Complete the forced password change. You have just experienced authentication as a standard user with no admin rights (authorization).

## Clean Up

Keep the user and group for Lab 03 and Lab 09. If you are stopping the lab series entirely, delete both now: open each object and select **Delete**.

## Success Criteria

You are done when you can explain:

- The difference between creating a member user and inviting a guest
- Why access is usually granted to groups instead of individual users
- Assigned vs dynamic membership
- Why the lab user was created without any admin roles
