# AZ-104 Mock Review

30 original scenario drills in shuffled order, weighted to match the official domain weights: roughly 7 identity/governance, 5 storage, 7 compute, 6 networking, 5 monitoring. Answer each in your head (or on paper) before opening the answer guide, and treat every constraint in the scenario (cost, SLA, least privilege) as binding.

These are original practice drills written for this pack. They are not real exam questions and do not reproduce exam content.

## How to use this file

| Situation                  | How to run it                                                            |
| -------------------------- | ------------------------------------------------------------------------ |
| First full pass            | All 30 in one sitting, 60-90 seconds each, score yourself honestly       |
| After a weak practice test | Do only the drills in your weak domain (map them from the answer guide)  |
| Final week                 | Redo every drill you missed, then reread the matching study note section |

Scoring guide: 26+ correct means you are close to ready; below 22, go back to the study notes for the domains you missed before booking.

## Drills

1. A helpdesk team at a logistics firm must start, stop, and resize the 14 VMs in resource group rg-fleet, but the security team requires that they cannot touch the VNet, NSGs, or role assignments. You must follow least privilege. Which role and scope do you assign?

2. Contoso-style setup: VNet-Hub is peered to VNet-App, and VNet-App is peered to VNet-Data. A VM in VNet-Hub cannot reach a SQL VM in VNet-Data, although NSGs allow the traffic. What is the cause and the cheapest fix that does not add new appliances?

3. A contractor was given a service SAS URL for a container of design files, valid for 90 days. The contract ends today and security wants the URL dead within the hour, without breaking the SAS tokens other vendors use on the same account. What should have been configured, and what is the least disruptive action now?

4. A retail API runs on two VMs and the business has signed a 99.99% availability SLA with a partner. The region supports availability zones. The finance team rejects any third VM. What deployment change meets the SLA at the current VM count?

5. During last week's outage, an NSG change was suspected of blocking SQL traffic from an app VM on port 1433. You need a one-time check of whether current NSG rules allow that specific flow, without deploying agents or waiting on data collection. Which tool do you use?

6. An auditor reviewing your subscription finds 60 resources violating a new "allowed locations" Deny policy that was assigned yesterday. A manager panics that Azure will delete them. What actually happens to those existing resources, and what does the policy block going forward?

7. A dev team stops their build VM from inside the guest OS every evening to save money, but the monthly bill barely moves. The VM uses a Premium SSD and a Standard public IP. Why is the saving so small, and what should they do instead?

8. A healthcare company must keep 8 TB of scan archives for 7 years at the lowest possible storage cost. Regulators occasionally audit and expect a requested file to open during the same working session, within minutes at most. Which blob access tier fits, and which one is the trap?

9. Admins currently RDP to production VMs over public IPs, and a new security baseline bans all public IPs on VMs by Friday. The team wants browser-based access with no client VPN software and minimal ongoing management. What do you deploy?

10. A project manager must be able to grant teammates access to resources in the rg-analytics resource group, but compliance insists she must not be able to create, modify, or delete any resource herself. Which built-in role satisfies both requirements?

11. A metric alert on CPU fired correctly during a weekend incident, and the alert shows in the portal, but no one was emailed or paged. The alert rule shows state "Fired". What two configurations do you check first?

12. A new compliance rule says VM temp disks and disk caches must be encrypted, not just the OS and data disks at rest. The team proposes Azure Disk Encryption with BitLocker. Why does that fail the requirement, and what is the correct feature?

13. A fintech startup needs its transaction blobs to survive a complete regional outage, and the reporting team must be able to read (not write) the data from the secondary region even while the primary is healthy. Which redundancy option is the minimum that satisfies this?

14. An NSG has an inbound custom rule "Deny-All-Inbound" at priority 100 and "Allow-HTTPS" (TCP 443 from Internet) at priority 200. Users cannot reach the web VM on 443. Explain the behavior and the fix.

15. Finance wants every resource to carry a CostCenter tag copied from its resource group so chargeback reports work. An engineer says tags inherit automatically from resource groups. Is he right, and what is the correct enforcement mechanism including fixing existing resources?

16. A web team on an App Service Basic (B1) plan wants staged deployments: push to a staging slot, warm it up, then swap to production with instant rollback. The swap option is missing in the portal. What is the smallest change that unlocks it?

17. An e-commerce company can tolerate at most 15 minutes of data loss for its order-processing VMs if the primary region fails, and must be able to run the workload in a second region within the hour. The team proposes daily Azure Backup to a Recovery Services vault. Why is that wrong, and what meets the requirement?

18. Office users must mount an Azure file share over SMB using their existing domain identities, with per-folder permissions. Mounting works from an Azure VM but fails from the office network with a connection timeout. What is the most likely blocker, and name two ways around it?

19. A deployment engineer reruns an ARM template into an existing resource group to add one storage account, using deployment mode Complete "because it sounded thorough". Three unrelated test VMs in that resource group disappear. Explain what happened and which mode should have been used.

20. A storage account holding order exports must only be reachable from your app subnet with traffic that never leaves the Microsoft backbone, and the app must resolve the account to a private IP inside the VNet. The architect suggests a service endpoint. Does that meet the stated requirement?

21. Marketing set a monthly budget of 2,000 on their subscription with an alert at 90%. The alert fired on the 20th, yet spending continued to 2,600 by month end, and a director asks why Azure "ignored the budget". What do budgets actually do, and what would genuinely restrict deployments?

22. Security asks who deleted a production NSG last Tuesday and wants this answerable with a KQL query going forward, retained for 180 days. Nothing has been configured yet. Which two things must exist before that query can ever return results?

23. A VM scale set was configured with a scale-out rule: add 2 instances when average CPU is above 70%. After a traffic spike three weeks ago, the instance count has stayed at maximum ever since and the bill tripled. What configuration is missing?

24. A nightly deployment overwrote 300 product-image blobs with corrupted versions. Soft delete for blobs is enabled with 14-day retention, but the operations team cannot find anything to undelete. Why does soft delete not help here, and what feature would have?

25. Users of a public web app need HTTPS with TLS terminated at the edge, path-based routing (/images to one pool, /api to another), and protection from common web exploits. The current Standard Load Balancer does none of this. Which service is required and why is the load balancer incapable?

26. A consultant from an outside firm with her own Microsoft account needs Contributor access to a single resource group for six weeks. A junior admin plans to create a new member user account and share the password by email. What is the correct approach following least privilege and standard practice?

27. A team needs to run a containerized report generator for about 20 minutes each night. It needs no orchestration, no load balancing, and must incur cost only while running. They are evaluating AKS, App Service, and one other option. What is the best fit and why?

28. A VM's backup succeeded last night, but a user deleted a single configuration file this morning and needs it back in minutes. A junior admin starts a full VM restore to a new VM. What faster restore option should be used instead, and where is it found?

29. An internal three-tier app sits behind an internal Standard Load Balancer. After a backend VM was moved to a new subnet, the LB marks it unhealthy even though the app responds locally on the VM. List the first two things you check, in order.

30. A new hire cannot be assigned a Microsoft 365 license in Microsoft Entra ID; the assignment fails with an error every time, although licenses are available. The account was bulk-created from a CSV last week. What property is missing?

## Answer guide

1. Virtual Machine Contributor at the rg-fleet resource group scope. It allows full VM management (including start, stop, resize) but no network or role assignment rights; the tempting answer, Contributor, fails least privilege because it also grants network and most other resource management.

2. VNet peering is not transitive, so Hub cannot reach Data through App. The cheapest fix is a direct peering between VNet-Hub and VNet-Data; routing through an NVA or VPN Gateway in the middle works but adds cost and management, which the question excludes.

3. The SAS should have been issued against a stored access policy, which can be deleted or shortened to kill dependent tokens instantly. Now, the least disruptive action is to create nothing worse: rotating the account key kills the contractor's token but also every other SAS signed with that key, so if no stored access policy exists, key rotation is the only revocation and the other vendors' tokens must be reissued; simply "deleting" an ad hoc SAS is impossible, which is the trap.

4. Deploy the two VMs across two availability zones (zone 1 and zone 2). Two or more VMs across zones carry the 99.99% SLA; an availability set only reaches 99.95%, so it is the tempting but insufficient answer, and adding a third VM is excluded by cost.

5. Network Watcher IP flow verify. It is the one-shot "would this 5-tuple be allowed by NSG rules" check and names the rule that blocks; Connection monitor is the trap because it is for continuous monitoring over time, not a quick rule test.

6. Existing resources are only marked non-compliant on the compliance dashboard; nothing is deleted. Going forward, the Deny effect blocks new deployments and non-compliant changes to existing resources; the trap is believing Deny is retroactive or destructive.

7. Stopping from inside the guest OS leaves the VM allocated, so compute continues to bill; only Stopped (deallocated) releases the compute charge. They should stop the VM from the portal/CLI (deallocate), and remember disks and the Standard public IP keep billing regardless, which is why the bill never reaches zero.

8. Cold tier. It is the cheapest tier that still serves reads online, so a requested file opens within the auditor's session; archive is the trap because archived blobs must be rehydrated first, which takes up to hours on standard priority and breaks the "within minutes" requirement despite the lower per-GB price.

9. Azure Bastion. It provides browser-based RDP/SSH through the portal over TLS with no public IPs on the VMs and no client software; a jump-box VM is the tempting answer but keeps a public IP and adds patching and management overhead.

10. User Access Administrator at the rg-analytics scope. It manages role assignments without granting any resource-modification rights; Owner is the trap because it grants both, violating the compliance requirement.

11. Check that the alert rule has an action group attached (with a valid email/SMS/push action), and check for an alert processing rule that may be suppressing notifications (for example a maintenance-window suppression left enabled). A fired alert only proves the condition logic worked; delivery is entirely the action group's job.

12. Azure Disk Encryption runs BitLocker/DM-Crypt inside the guest against OS and data disks; it does not cover the temp disk and host caches. Encryption at host encrypts data at the hypervisor host, including temp disks and caches, which is exactly what the requirement names.

13. RA-GRS. Geo-redundant storage survives a regional outage, and the RA- prefix adds read access to the secondary while the primary is healthy; plain GRS is the trap because the secondary is unreadable until Microsoft or you initiate failover. RA-GZRS also qualifies but is more than the minimum.

14. NSG rules are evaluated in priority order, lowest number first, and evaluation stops at the first match; the Deny at 100 matches before the Allow at 200 ever gets a chance. Renumber so the Allow-HTTPS rule has a lower priority value (for example 100) than the deny-all rule (for example 4096, or rely on the default deny).

15. He is wrong: tags do not inherit from resource groups by default. Assign an Azure Policy with the Modify effect that copies the CostCenter tag from the resource group, and run a remediation task to stamp existing resources; requiring the tag with Deny is the trap because it blocks deployments instead of fixing them and does nothing for existing resources.

16. Scale the plan up to Standard (S1) or higher. Deployment slots are a plan-tier feature that starts at Standard; the trap is scaling out (adding instances), which changes capacity but never unlocks tier-gated features.

17. Daily backup gives an RPO of up to 24 hours and restores take too long for a one-hour recovery-time goal in another region. Azure Site Recovery replicates the VMs continuously to a secondary region (RPO of minutes) and fails over on demand; Backup is for restoring data, ASR is for failing over workloads.

18. Outbound TCP port 445 is blocked, which most ISPs and many corporate firewalls do; it works from the Azure VM because Azure-internal traffic does not cross that block. Workarounds: a site-to-site or point-to-site VPN (or ExpressRoute) so SMB flows privately, or a private endpoint reached over that tunnel; identity-based access (with NTFS ACLs) handles the per-folder permissions once connectivity exists.

19. Complete mode deletes every resource in the resource group that is not defined in the template, so the three VMs were removed as "not in the template". Incremental mode (the default) only adds or updates what the template defines and should have been used; the trap is assuming Complete is just "more thorough".

20. No. A service endpoint keeps traffic on the backbone but the storage account still resolves to its public IP and is reached over its public endpoint (restricted to the subnet); the requirement to resolve to a private IP inside the VNet is exactly what a private endpoint provides, together with a privatelink private DNS zone.

21. Budgets and their alerts only notify (or trigger an action group); they never stop spending or block deployments. To genuinely restrict what can be deployed, use Azure Policy (for example allowed SKUs or allowed resource types) or remove the deployers' RBAC rights; expecting a budget to act as a hard cap is the classic trap.

22. The Activity log must be exported via a diagnostic setting to a Log Analytics workspace, and that workspace must have retention set to at least 180 days (the default portal retention is shorter and Activity log data is only KQL-queryable once it lands in a workspace). Without the diagnostic setting, the delete event exists only in the 90-day Activity log and cannot be queried with workspace KQL.

23. A matching scale-in rule (for example remove 2 instances when average CPU drops below 30%). Autoscale rules must be authored in pairs; with only a scale-out rule the set ratchets up to maximum and stays there, which is precisely the cost failure described.

24. Soft delete protects deleted blobs; these blobs were overwritten, not deleted, so there is nothing in the soft-delete state to recover. Blob versioning would have kept the previous version of each blob automatically on every overwrite, ready to be promoted back; snapshots also work but are manual.

25. Application Gateway (with WAF enabled, or the WAF_v2 SKU). It operates at layer 7, so it can terminate TLS, route by URL path, and apply web application firewall rules; Azure Load Balancer is layer 4 and only distributes TCP/UDP flows, so it cannot see paths, certificates, or HTTP attacks.

26. Invite her as a guest user (B2B collaboration) so she signs in with her own credentials and MFA, then assign Contributor scoped to that single resource group, and set an end date on the assignment or review it at contract end. Creating a shared member account is the trap: it breaks auditability, violates credential hygiene, and grants access under your tenant's identity lifecycle instead of hers.

27. Azure Container Instances. ACI runs a container on demand with per-second billing and no cluster or plan to keep warm, matching "cost only while running" and "no orchestration"; AKS is the trap because the node pool bills continuously, and App Service requires an always-on plan.

28. Use File Recovery from the recovery point: in the Recovery Services vault (or the VM's Backup blade), choose File Recovery, which mounts the recovery point as a local drive via a downloaded script so the single file can be copied out in minutes. A full VM restore is the slow trap: it provisions new disks and a new VM for one file.

29. First, check the health probe configuration against the app's actual listening port and path (a moved VM often gets a new NIC/IP while the probe or backend pool still references old settings). Second, check the NSG on the new subnet allows the probe source (AzureLoadBalancer service tag) and the app port; probes silently fail when the new subnet's NSG never allowed them.

30. Usage location. Microsoft 365 license assignment requires the user's usage location to be set (service availability is country-dependent), and CSV bulk creation does not set it; the trap is hunting for group-based licensing errors when a one-field user property is the blocker.
