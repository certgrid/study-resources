# AZ-140: Microsoft Azure Virtual Desktop Specialty - Study Cheatsheet

AZ-140: Microsoft Azure Virtual Desktop Specialty validates your ability to plan, deploy, secure, and manage Azure Virtual Desktop (AVD) environments and published remote apps for any device. It targets administrators and platform engineers who design host pools, configure identity and FSLogix profiles, deliver applications, and monitor session host health. The exam is 120 minutes with a passing score of 700.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | AZ-140 |
| Credential | AZ-140: Microsoft Azure Virtual Desktop Specialty |
| Level | Specialty |
| Practice mock length | ~50 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Plan and Implement an Azure Virtual Desktop Infrastructure | ~30% |
| 2 | Plan and Implement Identity and Security | ~23% |
| 3 | Plan and Implement User Environments and Apps | ~23% |
| 4 | Monitor and Maintain an AVD Infrastructure | ~24% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Plan and Implement an Azure Virtual Desktop Infrastructure

- Pooled host pools share session host VMs across many users (best for cost when users run the same apps); personal host pools assign one dedicated VM per user.
- Load-balancing algorithms for pooled pools: breadth-first spreads sessions across hosts for performance, while depth-first packs sessions onto each host before using the next to maximize density and cut cost.
- A single host pool can publish both a Desktop application group (full desktop) and a RemoteApp application group (individual apps), but a given user can be assigned to only one application group type per host pool.
- Windows 11/10 Enterprise multi-session allows multiple concurrent users on one VM; single-session SKUs (Windows 11 Enterprise) serve one user at a time and are used for personal pools.
- FSLogix profile containers require SMB storage: Azure Files (Standard transaction-optimized or Premium) or Azure NetApp Files, which gives sub-millisecond latency for high-concurrency workloads.
- For Entra-ID-joined session hosts with no on-premises AD, use Microsoft Entra ID Kerberos authentication so Entra-joined VMs can request Kerberos tickets to mount the Azure Files SMB share.

### Domain 2 - Plan and Implement Identity and Security

- Enforce MFA for AVD with a Conditional Access policy targeting the Azure Virtual Desktop cloud app (app ID 9cdead84-a844-4324-93f2-b2e6bb768d07), which challenges users at the feed/connection stage.
- Enable single sign-on (SSO) to carry the authenticated session to the session host; this requires one-time admin consent for the Microsoft Remote Desktop and Windows Cloud Login service principals.
- Microsoft Remote Desktop client app ID is a4a365df-50f1-4397-bc59-1a1564b8bb9c; both it and the AVD app are referenced when scoping Conditional Access or configuring SSO consent.
- Restrict access to managed devices using a Conditional Access grant control 'require device to be marked as compliant' (evaluated by Intune) targeting the AVD cloud app.
- Use the Locations condition with named locations (corporate IP ranges) in Conditional Access to allow or block sign-ins based on network location.
- Key built-in RBAC roles: Desktop Virtualization Contributor (full AVD management), Desktop Virtualization User (end-user app group access), Desktop Virtualization Application Group Contributor (assign users to app groups only), and Desktop Virtualization User Session Operator (manage user sessions: message, disconnect, log off).

### Domain 3 - Plan and Implement User Environments and Apps

- MSIX app attach delivers apps without baking them into the image: package as MSIX, expand into a VHD/VHDX/CimFS image with msixmgr, store on an SMB share, then add the package to the host pool.
- CimFS (Composite Image File System) is the recommended modern container format for MSIX app attach images, offering better performance and lower overhead than VHD/VHDX.
- FSLogix Profile Container roams the full user profile (including Outlook OST and search index) in a VHD/VHDX; VHDLocations is set under HKLM\SOFTWARE\FSLogix\Profiles to the UNC path of the share.
- FSLogix Office Container (ODFC) splits large Microsoft 365 cache data (Outlook OST, OneDrive cache, Teams data, search index) into a separate container so it can use its own storage tier and capacity.
- Use FSLogix redirections.xml to exclude or redirect specific folders (such as Downloads or browser cache) out of the profile container to control profile size.
- Optimize Microsoft Teams in AVD by installing the Teams desktop client plus the Remote Desktop WebRTC Redirector Service, which offloads audio/video processing to the local client device.

### Domain 4 - Monitor and Maintain an AVD Infrastructure

- Azure Virtual Desktop Insights, built on Azure Monitor and Log Analytics, is the purpose-built dashboard for host pool performance, connection quality, and FSLogix profile diagnostics.
- AVD Insights requires the Azure Monitor Agent (AMA) on each session host plus a Data Collection Rule (DCR) defining which performance counters and event logs to send to the Log Analytics workspace.
- Key health metrics to track include average user input delay per session host (responsiveness) and available memory (MB); high input delay or low memory signals an over-loaded host.
- The WVDCheckpoints table in Log Analytics records FSLogix profile load timing, letting you measure sign-in/profile mount duration.
- An 'Unavailable' session host usually means the VM is stopped or the AVD agent / side-by-side (SxS) stack is unhealthy; first verify the VM is running and those services are healthy.
- Create custom Azure Monitor alert rules on host pool metrics (for example, active sessions exceeding 90% of the max session limit) and notify via action groups.

## Study tips

- Memorize the Desktop Virtualization RBAC roles and exactly what each grants - questions frequently ask for the least-privilege role to assign users to app groups (Application Group Contributor) or to manage sessions (User Session Operator).
- Know the MFA + SSO pattern cold: a Conditional Access policy on the Azure Virtual Desktop cloud app enforces MFA, and enabling SSO (with service principal consent) stops the second credential prompt at the host.
- When a scenario gives Entra-ID-joined (not hybrid) hosts, default to cloud-native answers: Entra ID Kerberos for Azure Files, Intune for management, and Entra-based RDP auth (enablerdsaadauth:i:1).
- For storage and profile questions, match the requirement to the option: lowest latency / high concurrency points to Azure NetApp Files; large Office cache points to a separate FSLogix Office Container (ODFC).
- For maintenance scenarios, the safe answer almost always involves drain mode plus deploying new hosts from an updated image - never patch or rebuild hosts that still have active user sessions.

---

Want the full breakdown? See the complete **[AZ-140 study guide](https://certgrid.app/study-guide/az-140-microsoft-azure-virtual-desktop-specialty)** and **[free practice questions](https://certgrid.app/practice/az-140-microsoft-azure-virtual-desktop-specialty)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

