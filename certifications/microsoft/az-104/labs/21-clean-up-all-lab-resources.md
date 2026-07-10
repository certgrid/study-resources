# Lab 21 - Clean Up All Lab Resources

The final lab is real admin work: sweep the subscription, kill every cost source, and verify with Cost analysis. Deleting well is an AZ-104 skill: locks, vaults, and hidden resources all resist naive deletion.

## Time Needed

20-30 minutes (plus a next-day cost check).

## What You Will Learn

- The deletion order that dependencies force on you
- Which leftovers silently bill (disks, IPs, plans, vaults)
- How to verify a subscription is actually clean

## AZ-104 Concepts Covered

| Concept            | Where you see it in the lab             |
| ------------------ | --------------------------------------- |
| Resource lifecycle | You delete a whole environment safely   |
| Locks              | You remove blockers before deletion     |
| Vault dependencies | You confirm backup teardown from lab 20 |
| Cost verification  | You prove spend goes to zero            |

## Cost Warning

This lab SAVES money. Everything here is deletion; the only mistake available is skipping it.

## Steps

### 1. Hunt the classic silent billers first

Check each of these exists-and-deletes before the big group delete:

| Leftover                                | Why it bills                     | Where                    |
| --------------------------------------- | -------------------------------- | ------------------------ |
| Running/stopped (not deallocated) VMs   | Compute                          | Virtual machines         |
| Unattached managed disks                | Storage per GiB                  | Disks                    |
| Standard public IPs                     | Per hour while they exist        | Public IP addresses      |
| App Service plans (any tier above Free) | Per hour even with no apps       | App Service plans        |
| Scale sets / load balancers / gateways  | Per hour                         | Their blades             |
| Container instances                     | Per second while running         | Container instances      |
| Recovery Services vaults                | Per protected instance + storage | Recovery Services vaults |

### 2. Clear deletion blockers

1. **Locks**: open `rg-az104-labs` > Locks and every child resource with locks: remove them (lab 04 should already be clean).
2. **Vault**: if lab 20's vault still exists, finish its Clean Up first (stop protection, delete data, handle soft delete): a vault with protected items will block group deletion.
3. **Policy assignments**: remove any lab policy assignments (lab 03) so they do not confuse later deployments.

### 3. Delete the resource groups

```bash
az group delete --name rg-az104-labs --yes --no-wait
az group list --output table
```

Delete any other lab groups the list reveals (e.g. `rg-az104-move` from lab 04, groups auto-created by wizards like `NetworkWatcherRG` can stay: it is free and Azure recreates it anyway).

### 4. Sweep the directory objects

Free but tidy: delete lab users (`Lab User1`, the guest invite), groups (`grp-az104-admins`, `grp-az104-viewers`), the custom role `Custom VM Operator (lab)` if saved, and the management group `mg-az104-lab` (must be empty; move the subscription out first).

### 5. Verify

1. **All resources** filtered to your subscription: expect nothing lab-related (Cloud Shell's small storage account may remain: delete it too if you are done with Cloud Shell).
2. **Cost Management > Cost analysis**: today's accumulated cost curve should flatten.
3. TOMORROW: open Cost analysis again and confirm daily cost is at (or near) zero. Charges lag by hours: only the next-day check is proof.
4. Keep the budget `budget-az104-labs` alive until the next-day check passes, then delete it or leave it as a tripwire.

## Clean Up

This lab IS the cleanup. The only follow-up is the next-day cost verification in step 5.

## Success Criteria

You are done when you can explain:

- The three classic deletion blockers (locks, vault contents, dependencies)
- Five leftovers that bill even when "nothing is running"
- Why the next-day cost check matters
- Why deleting the resource group was the fastest correct move (lifecycle container)
