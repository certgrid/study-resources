# Citrix CCA-V: Certified Associate - Virtualization - Study Cheatsheet

The Citrix CCA-V (Certified Associate - Virtualization) exam validates the ability to install, configure, and manage a Citrix Virtual Apps and Desktops (CVAD) or Citrix DaaS environment, covering FMA architecture, site setup, machine catalogs and delivery groups, image provisioning with MCS and PVS, HDX policies, profile management, StoreFront and Citrix Gateway, and monitoring with Director. It is aimed at administrators and engineers responsible for deploying and operating Citrix virtualization environments. The exam is 90 minutes long with a passing score of 620 on a scaled scale.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | Citrix CCA-V |
| Credential | Citrix CCA-V: Certified Associate - Virtualization |
| Level | Associate |
| Practice mock length | ~65 questions |
| Duration | ~90 minutes |
| Passing score | 620 out of 1000 |
| Notes reviewed | 2026-06-23 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | CVAD Architecture and Components | ~13% |
| 2 | Site Setup and Administration | ~13% |
| 3 | Delivering Resources: Catalogs, Delivery Groups, and Applications | ~13% |
| 4 | Image Provisioning with MCS and PVS | ~13% |
| 5 | Citrix Policies and HDX | ~13% |
| 6 | Profile Management and Workspace Environment Management | ~13% |
| 7 | StoreFront, Workspace App, and Citrix Gateway | ~12% |
| 8 | Monitoring, Troubleshooting, and Printing | ~12% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - CVAD Architecture and Components

- The FMA (FlexCast Management Architecture) launch path is Citrix Workspace app -> StoreFront -> Delivery Controller -> VDA, with the HDX session ultimately established directly to the VDA.
- StoreFront authenticates users, queries the Delivery Controller's XML/Broker service for entitlements (enumeration), aggregates resources into a store, and delivers the ICA file at launch - but it does not itself broker sessions.
- The Broker Service on the Delivery Controller makes the brokering decision: it selects an appropriate registered VDA based on Delivery Group entitlement, load, and session-sharing rules, and returns its address.
- Only VDAs that are currently registered with a Delivery Controller can be assigned sessions; powered-on but unregistered VDAs are treated as unavailable, so launches fail even when enumeration succeeds.
- VDA registration requires correct Controller discovery (typically Active Directory-based auto-update or a registry/policy list), accurate time sync, and the registration port (TCP 80/443 to the Controller) being open.
- Enumeration is the listing of apps and desktops a user is entitled to; launch is the act of establishing the HDX session to a brokered VDA.

### Domain 2 - Site Setup and Administration

- A hosting connection stores the management address and credentials of the hypervisor or cloud; the associated resources (resource pool) object maps the cluster, storage repositories, and guest networks used for provisioning.
- Supported hosting platforms include VMware vSphere (vCenter), Microsoft Hyper-V via System Center Virtual Machine Manager (SCVMM), Nutanix AHV, Microsoft Azure, Amazon AWS (EC2), and Google Cloud.
- A VMware vSphere hosting connection uses the vCenter Server SDK endpoint as its address, in the form https://<vcenter-fqdn>/sdk, with a vCenter service account.
- You must install or trust the vCenter Server certificate on the Delivery Controllers (or Cloud Connectors) managing a vSphere connection, or the connection will fail.
- An Azure hosting connection authenticates with a Microsoft Entra ID app registration (service principal) using its application ID and client secret, assigned a role such as Contributor scoped to the subscription or resource group.
- An AWS hosting connection uses an IAM access key ID and secret access key with the required EC2 permissions; a Google Cloud connection uses a service account key (JSON) with the required IAM roles.

### Domain 3 - Delivering Resources: Catalogs, Delivery Groups, and Applications

- A Single-session OS catalog uses a desktop OS (Windows 10/11), serves one user per machine at a time, and supports either random (pooled) or static (dedicated) assignment - this is the model for full VDI desktops.
- A Multi-session OS catalog uses a server OS (e.g., Windows Server 2022 with the RDS role) and hosts many concurrent sessions per machine - the model for shared hosted apps and shared hosted desktops.
- A Remote PC Access catalog installs the VDA on existing physical office PCs and brokers users back to the same workstation they use on-site, often via automatic assignment on first connection.
- Random (pooled) assignment hands out any available machine at logon and resets non-persistent machines to the master image at logoff - the most storage-efficient, stateless model.
- Static (dedicated) assignment permanently binds each user to one VM where all changes (apps, files, settings) persist across reboots - the model for developers and power users.
- MCS with dedicated static machines saves persistent user changes to a separate identity disk and differencing disk so each dedicated machine retains its state.

### Domain 4 - Image Provisioning with MCS and PVS

- MCS provisions VMs from a snapshot of the master image; if you select a powered-off VM, MCS automatically takes a snapshot of it before provisioning.
- Each MCS VM is attached three disks: the shared read-only base disk, a small identity (ID) disk holding the unique computer name, machine account password, and SID information, and a differencing (delta) disk capturing all writes.
- MCS copies a full base disk (consolidated from the snapshot) to each storage location the catalog uses.
- For pooled (non-persistent) MCS machines, the differencing disk is reset on restart, returning the VM to the base image and discarding session changes; for dedicated machines the differencing disk persists across reboots.
- MCSIO (MCS I/O storage optimization) caches writes in RAM first and overflows to a temporary write-cache disk, reducing IOPS against the shared base image - a common default is 256 MB RAM cache with a 20 GB temporary write-cache disk.
- Update Machines (rollout of a new master image snapshot) builds a new base disk and transitions VMs to it; each machine switches individually on its next shutdown or scheduled restart, avoiding a forced mass reboot.

### Domain 5 - Citrix Policies and HDX

- Citrix policies can be authored in two independent places: the Site database (managed in Web Studio's Policies node) or Active Directory GPOs (managed in GPMC with the Citrix Group Policy extension).
- Web Studio displays and edits only Site-database policies; settings defined in a GPO are invisible in Web Studio and vice versa.
- In policy resolution, Active Directory GPOs carry the highest precedence, so when the same setting conflicts across sources, the AD GPO value wins over the Site (Web Studio) value, with the standard LSDOU order applying within AD.
- Among policies of the same scope, the policy with the higher priority (lower priority number, where 1 is highest) wins for any conflicting setting.
- A setting left in the Not Configured state is ignored by that policy; its effective value comes from other policies or the system default.
- Citrix policy filters include User or Group, Access Control (e.g., connections via Citrix Gateway), Client IP Address, Tag, Client Name, and more; an unfiltered policy applies to all connections in the site.

### Domain 6 - Profile Management and Workspace Environment Management

- The user store is the central network location (SMB file share or Azure Files) where Profile Management keeps the master copy of each user's profile, loaded at logon and merged back at logoff.
- Citrix Profile Management requires at minimum that you Enable Profile management and configure the Path to user store before it takes effect.
- Profile streaming fetches files and registry entries from the user store only on first access, leaving a local placeholder with metadata - this significantly reduces logon time.
- Active write-back synchronizes modified files and folders to the user store during the session (not just at logoff), protecting against data loss if a session ends abnormally.
- With concurrent sessions sharing one standard profile, last write wins: the session that logs off and writes a given file back to the store last overwrites the other session's version.
- Use variables such as !CTX_OSNAME! and !CTX_OSBITNESS! in the user store path to separate profiles by OS version and architecture so incompatible profiles are not mixed.

### Domain 7 - StoreFront, Workspace App, and Citrix Gateway

- When adding a Delivery Controller to a StoreFront store you supply the Controller's FQDN or IP address, the transport type (HTTP, HTTPS, or SSL Relay), and the matching port; StoreFront uses the XML Service to enumerate resources and request launches.
- List multiple servers within a single Delivery Controller entry (treated as one Site) so StoreFront can fail over to the next listed server if the first is unavailable.
- For multiple separate Sites/farms, create a separate Delivery Controller entry per Site, each listing that Site's controllers; the entry's friendly name should match the farm name where aggregation requires it.
- Configuring HTTPS to the Controllers requires a valid server certificate bound on each Controller and the Citrix XML Service configured to listen on the HTTPS port.
- A Workspace for Web (Receiver for Web) site is the browser-accessible front end tied to a store; without one, users cannot reach the store from a web browser.
- You can create two Workspace for Web sites pointing to the same store and customize each independently (for example, different branding for different user groups).

### Domain 8 - Monitoring, Troubleshooting, and Printing

- Citrix Director (the Monitor tab in DaaS) reads from the Monitoring database via the Monitor Service OData API exposed by the Delivery Controllers; the data is collected from the VDAs.
- The Director Dashboard is the real-time landing page showing connected session counts, recent connection failures, machines in failed/unregistered state, and infrastructure alerts.
- The Logon Duration drill-down decomposes a session logon into discrete phases - brokering, VM start, HDX connection, authentication, GPO processing, logon scripts, and profile load.
- The Trends view presents historical data over selectable time ranges (Sessions tab charts concurrent sessions; Filters/Machines views break down failures by Failure Type or other criteria).
- Monitoring data grooming (retention) periods are governed by the license edition: Premium (formerly Platinum) edition unlocks extended detailed retention up to 365 days.
- Change Monitor Service data retention with the Set-MonitorConfiguration PowerShell cmdlet, subject to the limits allowed by the license edition.

## Study tips

- Memorize the FMA launch path cold (Workspace app -> StoreFront -> Controller/Broker -> VDA) and be able to say exactly which component does enumeration, brokering, and HDX session hosting - many questions are scenario-based on which component failed.
- Know the three site databases (Site/Configuration, Configuration Logging, Monitoring) and what each stores; also know the SQL permission needed to create them (sysadmin, or dbcreator + securityadmin).
- Be precise on the MCS disk model (base + identity + differencing) and on the difference between pooled (reset on reboot) and dedicated (persistent) assignment - and contrast MCS (no streaming infra) against PVS (vDisk streaming, PXE/TFTP).
- For policy questions, apply the precedence rules deterministically: AD GPO beats Site, lower priority number wins, and Not Configured defers to other policies/defaults; remember Web Studio cannot see GPO-based policies.
- Watch for the on-premises CVAD vs. Citrix DaaS distinction throughout: in DaaS the Controllers are Citrix-managed in the cloud and Cloud Connectors (deploy two per resource location) bridge to local resources.

---

Want the full breakdown? See the complete **[Citrix CCA-V study guide](https://certgrid.app/study-guide/citrix-cca-v-certified-associate-virtualization)** and **[free practice questions](https://certgrid.app/practice/citrix-cca-v-certified-associate-virtualization)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

