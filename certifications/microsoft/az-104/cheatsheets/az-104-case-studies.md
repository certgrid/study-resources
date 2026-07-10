# AZ-104 Case Studies

Six original mini case studies for multi-step admin judgement. AZ-104 case questions rarely test one fact: they chain identity, networking, storage, monitoring, and cost decisions around a single company. Read the setup, answer the numbered questions in order, then check your reasoning (not just your final answer) against the answer guide.

These are original scenarios written for this pack. They are not real exam case studies and do not reproduce exam content.

How to work a case: read the constraints twice (budget, compliance, SLA), answer with the setup's exact resource names, and for every answer be able to say which blade or command proves it.

## Case 1 - Northwind Freight: VM cannot reach storage after a security hardening sprint

| Item          | Detail                                                                                     |
| ------------- | ------------------------------------------------------------------------------------------ |
| Subscriptions | One production subscription, sub-nwf-prod, under management group mg-nwf                   |
| Network       | vnet-prod (10.10.0.0/16) with snet-app (10.10.1.0/24) and snet-data (10.10.2.0/24)         |
| Compute       | vm-app-01 in snet-app runs a dispatch service writing manifests to blob storage            |
| Storage       | stnwfmanifests, GPv2, public network access disabled, private endpoint in snet-data        |
| Recent change | Security added NSG nsg-app to snet-app with a custom outbound rule set, and a new UDR      |
| Constraint    | Compliance requires all storage traffic to stay on private IPs; no public access re-enable |
| Symptom       | Since the change, vm-app-01 gets connection timeouts to stnwfmanifests                     |

Questions:

1. What is the fastest way to prove whether nsg-app is blocking vm-app-01's traffic to the private endpoint's IP, and what exactly do you enter?
2. The NSG turns out to allow the traffic. Name resolution on vm-app-01 returns the storage account's public IP, not the private endpoint IP. What is misconfigured, and how do you fix it without touching the VM's hosts file?
3. The new UDR on snet-app sends 0.0.0.0/0 to a firewall NVA that is still being provisioned. Why can this break the storage flow even with correct DNS, and which Network Watcher tool shows the route actually chosen?
4. Security proposes re-enabling public network access "temporarily" with the storage firewall limited to snet-app. Why does this violate the stated compliance constraint even though it feels safer than open access?
5. After the fix, how do you make sure a silent regression of this path pages the on-call within minutes next time?

## Case 2 - Fabrikam Robotics: a policy wall stops the release

| Item          | Detail                                                                                                                                      |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| Subscriptions | sub-fab-dev and sub-fab-prod under management group mg-fabrikam                                                                             |
| Governance    | Initiative "fab-baseline" assigned at mg-fabrikam: allowed locations (westeurope), allowed VM SKUs (D2s_v5, D4s_v5), require CostCenter tag |
| Deployment    | Release pipeline deploys a Bicep file: one D8s_v5 VM plus a storage account in northeurope                                                  |
| Identity      | The pipeline's service principal has Contributor on sub-fab-prod                                                                            |
| Constraint    | The release is contractually due this week; the baseline initiative cannot be removed                                                       |
| Symptom       | The deployment fails with policy denial errors before any resource is created                                                               |

Questions:

1. The pipeline owner insists "Contributor should be enough". Explain why the deployment still fails, and in which order RBAC and Policy are relevant here.
2. Which two specific properties of the Bicep deployment violate fab-baseline, and where in the portal do you confirm exactly which policy definitions denied it?
3. The robotics team genuinely needs a D8s_v5 in this one subscription. Without weakening the baseline for the whole company, what are the two clean options, and which scope does each apply at?
4. The storage account also fails the CostCenter tag requirement. The team wants existing and future resources fixed automatically instead of blocked. Which policy effect and follow-up action does that, and what identity does it need?
5. After the fixes, deployments succeed but compliance shows the subscription at 82%. Are the remaining non-compliant resources broken or blocked? What do you tell the release manager?

## Case 3 - Tailspin Media: the bill tripled overnight

| Item          | Detail                                                                                    |
| ------------- | ----------------------------------------------------------------------------------------- |
| Subscriptions | One subscription, sub-tsm-prod, monthly budget 8,000 with alerts at 80% and 100%          |
| Compute       | vmss-render: VM scale set for video rendering, D8s_v5, autoscale enabled, max 40          |
| Autoscale     | Scale out +5 instances at CPU > 65% for 10 minutes; no other rules configured             |
| Storage       | strender with a render-output container; lifecycle rule moves blobs to cool after 30 days |
| Monitoring    | Log Analytics workspace law-tsm; VM insights was recently onboarded to all instances      |
| Symptom       | Three days after a viral campaign, daily cost is triple the normal run rate               |
| Constraint    | Rendering must keep working during business hours; the budget cannot move                 |

Questions:

1. The budget alerts fired days ago but spending continued. Was cost management misconfigured, and what is the first blade you open to see which resources are actually driving the spike?
2. Cost analysis shows vmss-render at 40 instances since the campaign ended. Explain the root cause in the autoscale configuration and the exact fix, including the safety setting that prevents rule flapping.
3. Which immediate manual action reduces cost right now without deleting the scale set or breaking business-hours rendering, and what do you check before running it?
4. Cost analysis also shows law-tsm ingestion costs rose sharply. Connect this to the setup and name two controls that cap or reduce that cost without abandoning VM monitoring.
5. Leadership wants this failure mode to be structurally impossible next quarter. Name one governance control and one monitoring control you put in place, with their scopes.

## Case 4 - Woodgrove Bank: the file share broke after the identity cleanup

| Item          | Detail                                                                                                                              |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| Identity      | Microsoft Entra tenant with AD DS sync; identity-based access (AD DS) on Azure Files                                                |
| Storage       | stwgbfinance with share fin-reports, mounted by the finance team over SMB from the office                                           |
| Access model  | Share level: RBAC role "Storage File Data SMB Share Contributor" assigned to group grp-finance; file level: NTFS ACLs               |
| Recent change | An identity cleanup deleted "stale" groups and re-created grp-finance with the same name; several users were also moved to a new OU |
| Network       | Office connects via site-to-site VPN; nothing changed on the network this week                                                      |
| Symptom       | Since the cleanup, most finance users get "access denied" on fin-reports; two can still write                                       |
| Constraint    | Least privilege must be preserved; no share-wide Everyone permissions allowed                                                       |

Questions:

1. Why did re-creating grp-finance with the same name break access even though the name matches everywhere?
2. What explains the two users who can still write, and why is that detail diagnostic gold rather than noise?
3. In what order do you repair access, and at which of the two permission layers (RBAC share level, NTFS file level) does each step act?
4. A manager suggests assigning the RBAC role to each finance user individually "so groups can never break it again". Give two reasons to refuse, one operational and one audit/least-privilege.
5. Which check proves the fix end to end from an office machine, and what would you script to catch silent permission drift monthly?

## Case 5 - Proseware Health: backup strategy under a hard RPO

| Item          | Detail                                                                                                                 |
| ------------- | ---------------------------------------------------------------------------------------------------------------------- |
| Subscriptions | sub-psw-prod in region West Europe; regulator requires a documented regional DR plan                                   |
| Compute       | vm-ehr-01 and vm-ehr-02 run the patient records app; vm-batch-01 runs nightly reporting                                |
| Data          | SQL data disks on the EHR VMs; report outputs land in stpswreports (GRS)                                               |
| Requirements  | EHR VMs: RPO 15 minutes and recovery in a second region within 1 hour; batch VM: RPO 24 hours, no regional requirement |
| Current state | One Recovery Services vault, daily backup policy at 02:00 applied to all three VMs                                     |
| Constraint    | Budget allows continuous replication for at most two VMs; auditors want restore evidence                               |

Questions:

1. Evaluate the current setup against the EHR requirement: which number does daily backup actually deliver for RPO, and why does it also miss the recovery-time requirement?
2. Design the corrected protection per VM within the budget constraint, naming the service and target for each of the three VMs.
3. A junior admin asks whether Site Recovery replaces backup for the EHR VMs "since it copies everything anyway". What failure scenario does replication alone leave unprotected, and what does the combined design look like?
4. For the auditors, what is the difference between a test failover and a failover, and which one belongs in the quarterly DR evidence pack?
5. A single corrupted report file in stpswreports must be recoverable for 30 days without restoring anything VM-related. Which storage-native features cover this, and why is VM backup the wrong tool?

## Case 6 - Contoso Air: the outage nobody was paged for

| Item          | Detail                                                                                                           |
| ------------- | ---------------------------------------------------------------------------------------------------------------- |
| Subscriptions | sub-cta-prod; the booking API runs on vmss-book behind a public Standard Load Balancer                           |
| Monitoring    | Metric alerts exist on vmss-book CPU and memory; law-cta workspace collects some logs                            |
| Alert config  | CPU alert: severity 2, action group ag-ops (email to a shared mailbox nobody reads)                              |
| Incident      | Last Friday 22:10-23:40 the API was down: all LB health probes failed after a bad NSG push on the backend subnet |
| Aftermath     | No alert fired at all during the outage; leadership found out from social media                                  |
| Constraint    | On-call must be paged within 5 minutes for customer-facing outages; alert noise must stay low                    |

Questions:

1. CPU and memory alerts stayed green during the outage. Explain why those signals cannot catch this failure, and which two signals would have.
2. Design the alert that catches "the LB thinks all backends are dead", naming the resource, the metric, and a sensible threshold and window for the 5-minute paging requirement.
3. The bad NSG push was the root cause. Which Azure Monitor data source records that change, what must be configured for it to be KQL-queryable in law-cta, and what query concept finds "NSG writes in the hour before the outage"?
4. Fix the notification chain end to end so a fired alert actually pages a human in 5 minutes, and explain what alert processing rules add on top.
5. The team fears alert fatigue. Name two concrete design choices from this case that raise signal without raising noise.

## Answer guide

### Case 1 - Northwind Freight

1. Network Watcher IP flow verify: target vm-app-01, direction outbound, protocol TCP, local IP 10.10.1.x, remote IP = the private endpoint's IP in snet-data (10.10.2.x), remote port 443. It answers in seconds whether the effective NSG rules allow the flow and names the exact rule if denied. Check this first because it is the cheapest test that either convicts or acquits the newest suspect (the NSG change).
2. The private DNS zone privatelink.blob.core.windows.net is missing, unlinked from vnet-prod, or missing the A record for stnwfmanifests, so the VM resolves the public endpoint. Fix at the DNS layer: link the privatelink zone to vnet-prod (or recreate the private endpoint's DNS zone group so the A record is managed automatically). Hosts-file edits do not scale and hide the misconfiguration.
3. The UDR overrides system routes, so even traffic destined for the private endpoint subnet can be pulled to the NVA if the prefix match sends it there, and a half-provisioned NVA blackholes it. Network Watcher next hop against the private endpoint IP shows the route actually selected (expected: VirtualNetwork or InterfaceEndpoint, not VirtualAppliance). Route intent is proven by next hop, not by reading the route table.
4. The compliance constraint is that storage traffic stays on private IPs; a storage firewall exception with public network access enabled still serves traffic on the public endpoint, so the constraint fails even though the source is restricted. Restricting sources is access control, not private connectivity: those are different requirements.
5. Create a Connection monitor test from vm-app-01 to stnwfmanifests on port 443 (continuous reachability and latency), and attach an alert rule with an action group that pages on-call. IP flow verify was the right one-shot tool; continuous coverage is Connection monitor's job.

### Case 2 - Fabrikam Robotics

1. RBAC decides whether the caller may perform the action; Azure Policy then decides whether the request's content is allowed. Both gates must pass independently, so Contributor (RBAC) cannot override a Deny policy: the denial happens at template validation regardless of the caller's role.
2. The VM SKU D8s_v5 violates the allowed-SKUs policy, and northeurope violates allowed locations (westeurope only). Confirm in the deployment's error details (each denial links the policy assignment) or in Policy > Compliance, opening the assignment to see which definitions evaluated Deny for that request.
3. Option one: a policy exemption for the specific assignment scoped to sub-fab-prod (or the target resource group), documented with an expiry. Option two: assign a modified allowed-SKUs parameter value at the sub-fab-prod scope; a more specific assignment can extend the allowed list there if the initiative is parameterized per scope. Both leave mg-fabrikam untouched for every other subscription.
4. Modify effect (to add or replace the CostCenter tag), plus a remediation task to stamp resources that already exist. Remediation runs under a managed identity that the assignment creates, and that identity needs the role its policy demands (typically Contributor or Tag Contributor) at the assignment scope.
5. Non-compliant means marked, not broken or blocked: existing resources that violate Deny policies keep running and are only reported. Tell the release manager the release is unaffected, and the 82% is a cleanup backlog to drive down with remediation tasks and resource changes, not an outage risk.

### Case 3 - Tailspin Media

1. Cost management worked as designed: budgets alert (or trigger an action group) but never stop spending, so nothing was "ignored". Open Cost Management > Cost analysis on sub-tsm-prod, group by resource, to see the spike drivers before touching anything; act on data, not on the loudest guess.
2. Autoscale has a scale-out rule but no scale-in rule, so the set ratcheted to the 40-instance maximum and stayed. Add a paired scale-in rule (for example remove 5 instances when average CPU < 30% for 10 minutes) and keep a gap between the out and in thresholds (65/30, not 65/60) so instances do not flap; the cool-down/duration windows are the anti-flapping safety.
3. Manually scale vmss-render down (set instance count toward the normal baseline) during a low-load window, after checking current CPU/queue metrics and that in-flight render jobs drain (scale-in policies/termination notification). Deallocating the whole set or deleting instances blindly could kill running business-hours jobs, which the constraint forbids.
4. VM insights was onboarded to every instance, so 40 instances streamed performance and dependency data into law-tsm, and log ingestion bills per GB. Controls: set a daily cap on the workspace (hard stop on runaway ingestion) and tune data collection rules to collect fewer counters/less frequency or only from a sample of instances; also review retention so old data does not accrue cost.
5. Governance: an Azure Policy at the subscription (or management group) scope constraining scale set SKU and maximum instance count (or requiring autoscale profiles with scale-in rules). Monitoring: a cost anomaly alert plus a metric alert on vmss-render instance count (for example instances > 20 for 2 hours pages ops). Budgets stay as the safety net that tells humans; policy is the wall.

### Case 4 - Woodgrove Bank

1. Group identity is the SID/objectId, not the display name. The re-created grp-finance is a new object with a new SID and objectId, so the RBAC share-level assignment and the NTFS ACL entries still reference the deleted group's identifiers; a matching name repairs nothing.
2. The two working users almost certainly have direct entries somewhere: an individual NTFS ACL entry or a direct RBAC assignment left from the past. It is diagnostic gold because it proves the network path, SMB, port 445, VPN, and the storage account itself are all healthy: the failure domain collapses to identity and ACLs only.
3. First re-create the RBAC share-level assignment: assign Storage File Data SMB Share Contributor to the new grp-finance at the share (or account) scope; without share-level access nobody gets in regardless of NTFS. Then repair NTFS ACLs on the folders to reference the new group (mount with the storage account key as an admin to edit ACLs, since key access bypasses identity ACLs). Finally confirm the moved-OU users still sync to Microsoft Entra ID so their Kerberos tickets carry the new group SID.
4. Operational: individual assignments do not scale; every joiner/leaver becomes a manual storage change, and Azure also has role-assignment limits per subscription. Audit/least-privilege: group-based access gives one reviewable grant tied to HR-driven membership; hundreds of direct assignments make access reviews and revocation error-prone, which is worse for least privilege, not better.
5. End-to-end proof: from an office machine, as a regular finance user, map the share (net use to stwgbfinance.file.core.windows.net over the VPN) and create/edit a file in a folder the ACLs permit. Monthly drift check: script a comparison of the share's RBAC assignments and folder ACLs (Get-AzRoleAssignment plus icacls output) against a stored baseline and alert on differences.

### Case 5 - Proseware Health

1. A daily 02:00 backup means the worst-case data loss is up to 24 hours: nowhere near the 15-minute RPO. It also fails recovery time: restoring VMs from a vault into another region (cross-region restore, rebuild, reconfigure) realistically exceeds 1 hour, and backup restores data rather than standing up a running regional workload.
2. vm-ehr-01 and vm-ehr-02: Azure Site Recovery replication to a paired/second region (continuous replication, RPO in minutes, failover well inside 1 hour): exactly the two continuous-replication slots the budget allows. vm-batch-01: keep Azure Backup with the daily policy in the Recovery Services vault: a 24-hour RPO and no regional requirement is precisely what daily backup delivers.
3. Replication faithfully copies corruption, deletion, and ransomware damage to the secondary within minutes, so ASR alone cannot return you to "last Tuesday before the bad write". The combined design is ASR for regional failover plus Azure Backup for point-in-time restore on the same EHR VMs: two different questions ("where can it run" vs "which past state can I get back"), two tools.
4. A test failover brings up the replicated VMs in an isolated network in the target region without touching production or replication; a (real) failover moves production. The quarterly evidence pack uses test failovers: they prove recoverability and produce screenshots/job logs while carrying no production risk.
5. Blob soft delete (with at least 30-day retention) covers deletions, and blob versioning covers overwrites of individual report files; both restore a single blob in minutes with no compute involved. VM backup is the wrong tool because the reports live in a storage account, not on a VM disk, and restoring a whole VM (or even file recovery from a VM point) cannot recover blob-only data.

### Case 6 - Contoso Air

1. The outage was a connectivity failure: the backends were healthy machines (normal CPU/memory) that traffic could not reach after the NSG push, so guest-level metrics stayed green. The right signals are the Load Balancer health probe status metric (backend availability collapsing to zero) and a synthetic availability check on the API endpoint from outside (URL availability test), both of which measure what customers experience.
2. A metric alert on the Standard Load Balancer's Health Probe Status (average) scoped to the LB: for example average probe status < 50% over a 1-minute granularity with a 5-minute evaluation window, severity 1. All-backends-down drives the metric to 0 immediately, so the alert fires within the paging budget while short single-instance blips stay below the threshold.
3. The Activity log records the NSG write operations (who, what, when). It becomes KQL-queryable only after a diagnostic setting exports the subscription Activity log to law-cta. Query concept: filter AzureActivity for OperationNameValue containing networkSecurityGroups write operations in the 22:00-23:00 window and project caller, resource, and timestamp.
4. Point the alert at an action group whose actions actually page: SMS/voice/push to the on-call rotation or a webhook into the incident tool, not a shared mailbox; verify with the action group's test feature. Alert processing rules then manage behavior at scale: suppress notifications during planned maintenance windows and attach the paging action group to whole scopes so new alert rules cannot ship with a dead-end mailbox again.
5. First, alert on customer-facing symptoms (probe status, availability tests) at high severity and keep per-VM resource metrics at lower severity with longer windows, so pages map to outages rather than blips. Second, use alert processing rules for maintenance suppression and severity-based routing (severity 1 pages, severity 3 emails), which cuts noise without deleting coverage.
