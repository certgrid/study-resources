# Lab 10 - Clean Up Azure Resources

Cleanup is a core Azure habit. Beginners should learn it early because unused resources can keep generating cost.

## Time Needed

10-15 minutes.

## What You Will Learn

- How to identify lab resources
- How to delete a resource group
- Why cleanup controls cost
- Why production cleanup requires caution

## AZ-900 Concepts Covered

| Concept         | Where you see it in the lab                     |
| --------------- | ----------------------------------------------- |
| Resource group  | You delete related lab resources together       |
| Cost management | You reduce unnecessary spend                    |
| Tags            | You identify lab resources                      |
| Governance      | You practice safe resource lifecycle management |

## Steps

### 1. Review your lab resources

Open the lab resource group, such as:

```text
rg-az900-labs
```

Review all resources inside it.

### 2. Confirm it is safe to delete

Before deleting, confirm:

- The resource group is only for labs.
- No production resources are inside it.
- You no longer need the VM, storage account, VNet, or other resources.

### 3. Delete the resource group

1. Open the resource group.
2. Select **Delete resource group**.
3. Type the resource group name if prompted.
4. Confirm deletion.

### 4. Verify deletion

Refresh the Resource groups page and confirm the lab resource group is gone.

### 5. Review costs

Open Cost Management later to confirm spend stops increasing for deleted resources.

## Clean Up

This lab is the cleanup step.

## Success Criteria

You are done when you can explain:

- Why resource groups make cleanup easier
- Why unused resources can still cost money
- Why tags help identify lab resources
- Why cleanup should be done carefully in real environments

