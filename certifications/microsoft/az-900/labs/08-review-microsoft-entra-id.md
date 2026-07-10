# Lab 08 - Review Microsoft Entra ID

Microsoft Entra ID is central to Azure identity. This lab is read-only and safe for beginners.

## Time Needed

15-20 minutes.

## What You Will Learn

- Where Microsoft Entra ID lives in the portal
- What users and groups are
- Where MFA and Conditional Access concepts fit
- Why Entra ID is different from traditional AD DS

## AZ-900 Concepts Covered

| Concept            | Where you see it in the lab                   |
| ------------------ | --------------------------------------------- |
| Microsoft Entra ID | You open the tenant identity service          |
| Users              | You review identity objects                   |
| Groups             | You review access grouping                    |
| MFA                | You identify sign-in protection               |
| RBAC relationship  | You see that Azure permissions use identities |

## Steps

### 1. Open Microsoft Entra ID

1. Go to the Azure portal.
2. Search for **Microsoft Entra ID**.
3. Open the overview page.

### 2. Review tenant information

Look for:

- Tenant name
- Tenant ID
- Primary domain

### 3. Review users

Open **Users**.

Do not create users unless this is your own learning tenant and you understand the impact.

### 4. Review groups

Open **Groups** and observe how groups can organize users.

### 5. Find security features

Look for areas related to:

- Multifactor authentication
- Conditional Access
- Identity protection

Some features may require paid licenses. For AZ-900, you only need to understand the concept.

## Entra ID vs AD DS

| Service                          | Best memory                                           |
| -------------------------------- | ----------------------------------------------------- |
| Microsoft Entra ID               | Cloud identity, SSO, MFA, Conditional Access          |
| Active Directory Domain Services | Traditional domain join, Kerberos, LDAP, Group Policy |

## Clean Up

No cleanup required if you only reviewed settings.

## Success Criteria

You are done when you can explain:

- What Microsoft Entra ID is
- How users and groups relate to access
- Why MFA improves sign-in security
- Why Entra ID is not the same as traditional AD DS

