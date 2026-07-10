# Lab 04 - Locks, Tags, and Moving Resources

Three small governance features, three predictable exam questions. This lab applies both lock types, tags resources, and walks a resource move so you know what validation happens.

## Time Needed

25-30 minutes.

## What You Will Learn

- How CanNotDelete and ReadOnly locks behave differently
- How lock inheritance works
- How tags are applied and why they do not inherit by default
- How moving a resource between resource groups works

## AZ-104 Concepts Covered

| Concept          | Where you see it in the lab                   |
| ---------------- | --------------------------------------------- |
| Resource locks   | You apply and test both types                 |
| Lock inheritance | You lock the group and test a resource inside |
| Tags             | You tag at group and resource level           |
| Resource moves   | You move a resource and watch validation      |

## Cost Warning

Nearly free: one standard LRS storage account is created as a test subject (fractions of a cent for an hour). Delete it in Clean Up.

## Steps

### 1. Create a test resource

In Cloud Shell (replace `<unique>` with random lowercase letters/numbers):

```bash
az group create --name rg-az104-move --location <your-region>
az storage account create --name staz104lock<unique> --resource-group rg-az104-labs --sku Standard_LRS --location <your-region>
```

Note the storage name rules while you pick one: 3-24 characters, lowercase and digits only, globally unique.

### 2. Apply a CanNotDelete lock

1. Open the new storage account, select **Locks**, then **Add**.
2. Name `lock-nodelete`, type **Delete** (CanNotDelete). Save.
3. Try to delete the storage account: the portal refuses and names the lock.
4. Change something harmless (e.g. add a tag): allowed. CanNotDelete blocks only deletion.

### 3. Test a ReadOnly lock

1. Replace the lock: delete `lock-nodelete`, add `lock-readonly` with type **Read-only**.
2. Try to add another tag now: blocked. ReadOnly freezes modifications too.
3. Delete `lock-readonly` so the rest of the lab works.

### 4. Lock inheritance check

1. Open **rg-az104-labs > Locks** and add a Delete lock at the GROUP level.
2. Try deleting the storage account inside: blocked by the inherited lock.
3. Remove the group-level lock.

### 5. Tags

1. On the storage account, open **Tags** and add `CostCenter = IT`.
2. Open **rg-az104-labs > Tags** and note the group's tags from lab 00: the storage account did NOT get them automatically. Tags do not inherit; a Policy with Modify effect is the enforcement answer.
3. Search for **Tags** in the portal search bar to see the tag-centric view across resources.

### 6. Move a resource

1. On the storage account Overview, next to Resource group, select **(move)** > **Move to another resource group**.
2. Target: `rg-az104-move`.
3. Watch the validation step: Azure checks the resource type supports moves and that no locks block it.
4. Note the warning about tools/scripts using old resource IDs: the ID changes when the group changes.
5. Complete the move, then move it back (or just delete in Clean Up).

## Clean Up

```bash
az storage account delete --name staz104lock<unique> --resource-group rg-az104-move --yes
az group delete --name rg-az104-move --yes --no-wait
```

(Adjust the group if you moved it back.) Verify no locks remain on `rg-az104-labs`.

## Success Criteria

You are done when you can explain:

- CanNotDelete vs ReadOnly, with one example each of what still works
- Why a group-level lock affected the resource inside
- Why tags on a resource group do not appear on its resources
- Two things validated before a resource move, and what happens to resource IDs
