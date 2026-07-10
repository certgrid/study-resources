# Lab 06 - SAS Tokens and Stored Access Policies

Shared access signatures appear in nearly every AZ-104 sitting, usually as "how do you revoke it?". This lab generates SAS tokens both ways and proves why the stored access policy is the revocation answer.

## Time Needed

25-30 minutes.

Uses the storage account from lab 05.

## What You Will Learn

- How account keys, SAS tokens, and Entra roles relate
- How to generate a service SAS for one blob
- How a stored access policy makes SAS revocable
- What key rotation breaks

## AZ-104 Concepts Covered

| Concept              | Where you see it in the lab                |
| -------------------- | ------------------------------------------ |
| Access keys          | You view key1/key2 and the rotate buttons  |
| Service SAS          | You generate one for a blob                |
| SAS parameters       | You read permissions, expiry, IP, protocol |
| Stored access policy | You create one and tie a SAS to it         |
| Revocation           | You revoke by deleting the policy          |

## Cost Warning

Free beyond the existing storage account. SAS tokens do not bill.

## Steps

### 1. Look at the access keys

1. Open `staz104lab<unique>` from lab 05, select **Security + networking > Access keys**.
2. Note: two keys (key1, key2) with **Rotate** actions. Two exist so apps move to key2 while you rotate key1.
3. Do not rotate yet: rotation kills every SAS signed with that key.

### 2. Generate an ad hoc service SAS

1. Open **Containers > docs**, select `cool.txt` (or any blob), then the **Generate SAS** tab.
2. Set permissions: **Read** only; expiry: 1 hour from now; signing key: key1.
3. Generate and copy the **Blob SAS URL**.
4. Open the URL in a private browser window: the blob downloads/displays.
5. Read the query string you pasted: `sv` (version), `se` (expiry), `sp` (permissions), `sig` (signature). Recognition of these parameters is exam-relevant.
6. Ask the exam question: how do you revoke THIS token right now? Only by rotating key1 (which breaks everything else signed by it). That is the problem the next step solves.

### 3. Create a stored access policy

1. Go back to the `docs` container, select **Access policy** (container level).
2. Add a stored access policy: identifier `policy-read`, permission Read, expiry next week. Save.
3. Now generate a new SAS on the blob, but this time pick the **Stored access policy** `policy-read` instead of manual settings.
4. Test the new SAS URL in a private window: works.

### 4. Revoke by deleting the policy

1. Delete (or edit the expiry of) `policy-read` in the container's Access policy blade and save.
2. Retry the second SAS URL: authentication fails (it can take a moment).
3. The first ad hoc SAS still works: nothing revokes it except key rotation or expiry. That contrast is the whole exam point.

### 5. CLI recognition

```bash
az storage container generate-sas --account-name staz104lab<unique> --name docs --permissions r --expiry 2030-01-01 --auth-mode key
az storage account keys renew --account-name staz104lab<unique> --key key1
```

Run the first if you like; only READ the second (renewing now invalidates your ad hoc SAS, which is fine, but understand why before running it).

## Clean Up

Delete any remaining stored access policies and treat all generated SAS URLs as dead (rotate key1 if you shared one anywhere). Keep the account for lab 07.

## Success Criteria

You are done when you can explain:

- The three ways to authorize storage access (keys, SAS, Entra ID roles)
- Why an ad hoc SAS cannot be revoked individually
- How a stored access policy fixes that, and where it lives (on the container)
- What breaks when you rotate an account key
- Which SAS type avoids account keys entirely (user delegation SAS)
