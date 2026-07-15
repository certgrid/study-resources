# MD-102: Microsoft Endpoint Administrator - Study Cheatsheet

MD-102: Microsoft Endpoint Administrator validates your ability to deploy Windows clients, manage identity and compliance, protect and maintain devices, and deliver applications using Microsoft Intune and the broader Microsoft 365 stack. It is aimed at endpoint administrators who manage and secure an organization's devices, apps, and identities in a cloud or hybrid Microsoft Entra ID environment. The 120-minute exam has roughly 647 questions in the bank, requires a scaled score of 700 to pass, and spans four objective domains.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | MD-102 |
| Credential | MD-102: Microsoft Endpoint Administrator |
| Level | Intermediate |
| Practice mock length | ~50 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Deploy Windows Client | ~26% |
| 2 | Manage Identity and Compliance | ~24% |
| 3 | Manage, Maintain, and Protect Devices | ~26% |
| 4 | Manage Applications | ~24% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Deploy Windows Client

- Windows Autopilot requires each device to be registered in the Autopilot service by its hardware hash (a unique device identifier) before the device can be auto-provisioned during OOBE; you can obtain the hash from the OEM/vendor or run Get-WindowsAutopilotInfo (PowerShell) to export it to CSV.
- Autopilot pre-provisioning (white glove) has two phases: a technician phase that applies device-targeted apps and policies, and a user phase; if the technician phase fails, reboot and press the Windows key five times at the OOBE language screen to return to the pre-provisioning/troubleshooting menu.
- Automatic MDM enrollment requires a Microsoft Entra ID Premium P1 or P2 license, and Autopilot deployment requires the device to be registered with its hardware hash.
- The Windows Configuration Designer (WCD) builds provisioning packages that have the .ppkg file extension, used to apply settings to Windows devices without full reimaging.
- Windows subscription activation upgrades Windows 10/11 Pro to Enterprise in-place using a Microsoft 365 E3/E5 license, with no product key and no reimaging required.
- In Intune Windows Update rings, deferral periods delay how long a device waits after release before installing; feature update deferral can be set (e.g., 30 days) separately from quality update deferral (e.g., 7 days).

### Domain 2 - Manage Identity and Compliance

- Microsoft Entra registered devices are best for personal/BYOD scenarios: the device is known to Entra ID (enabling Conditional Access) but is not joined to the directory, giving minimal organizational control.
- Microsoft Entra hybrid joined describes a device joined to on-premises Active Directory and also synced into Entra ID, bridging on-prem Group Policy/Kerberos with cloud Conditional Access and Intune.
- Conditional Access enforces compliance: a policy with the grant control 'Require device to be marked as compliant' checks Intune compliance status before allowing access to Microsoft 365 resources.
- Valid Conditional Access grant controls include require device marked as compliant, require Entra hybrid joined device, require approved client app, and require multifactor authentication.
- An Intune compliance policy grace period defines how many days a device may stay non-compliant before being formally marked non-compliant; the countdown starts when the compliance engine detects the violation (for example 5 days from detection).
- The tenant-wide setting 'Mark devices with no compliance policy assigned as' (Compliant or Not compliant) determines how Intune treats devices that have no compliance policy assigned.

### Domain 3 - Manage, Maintain, and Protect Devices

- Use an endpoint security disk encryption policy to silently enable BitLocker on Microsoft Entra joined Windows devices, with automatic recovery key escrow to Entra ID and no user interaction required.
- To integrate Microsoft Defender for Endpoint with Intune you must enable the connector in both portals: turn on the Microsoft Defender for Endpoint connector in the Intune admin center and enable the Intune connection in the Defender portal (security.microsoft.com).
- Attack Surface Reduction (ASR) rules are configured in Intune endpoint security; common rules include 'Block Office applications from creating child processes' and 'Block executable content from email client and webmail'.
- The Wipe remote action performs a full factory reset, removing all data and apps and returning the device to its out-of-box state; use it for corporate-owned devices needing a complete reset.
- The Retire remote action removes the device from Intune management and deletes corporate apps/data while leaving the user's personal apps and data intact; use it for personal/BYOD devices.
- Device configuration profile types that mirror on-premises Group Policy are the Settings catalog (modern, searchable, thousands of settings) and Administrative templates (ADMX-backed).

### Domain 4 - Manage Applications

- To deploy a Win32 app (including .exe installers) you must first wrap it with the Microsoft Win32 Content Prep Tool to produce a single .intunewin package containing the app and its metadata.
- Win32 app detection rules verify a successful install; options include a file detection rule (checking for the app's executable) and a registry detection rule (checking for a specific key/value); the most common cause of a 'failed' status on a successfully installed app is a misconfigured detection rule.
- Intune app assignment intents are Required (installs automatically), Available for enrolled devices (shown in Company Portal for optional install), and Uninstall (removes the app from assigned devices).
- Use the built-in 'Microsoft 365 Apps for Windows 10 and later' app type to deploy Office; you can choose the update channel, exclude unwanted apps in the app suite configuration, and manage settings under App suite settings.
- Win32 app dependencies let one app require another: add, for example, .NET Framework 4.8 as a dependency so Intune automatically installs the dependency first, then the main app.
- For Win32 app updates you create a supersedence relationship; the 'Uninstall the previous version' option controls behavior - set to No (the common default) the new version installs over the existing one (the installer handles the upgrade), while Yes makes Intune uninstall the old version first before installing the new one.

## Study tips

- Master the join states and what each enables: Entra registered (BYOD, light control), Entra joined (cloud-only corporate), and Entra hybrid joined (on-prem AD + cloud). Many identity and Conditional Access questions hinge on choosing the correct join type and the prerequisites (such as the Intune Connector for AD for hybrid Autopilot).
- Memorize the Wipe vs Retire vs Fresh Start distinction. Wipe = full factory reset of corporate devices; Retire = remove only corporate data on personal devices and keep personal data; this single distinction appears repeatedly.
- Know the Win32 app lifecycle cold: wrap with the Content Prep Tool to make a .intunewin, configure install/uninstall commands, set detection rules (file/registry/MSI), use dependencies and supersedence. A 'failed install' that is actually installed almost always points to a bad detection rule.
- Understand Windows Update for Business in Intune: deferral periods, deadlines, grace periods, restart behavior, feature update policies targeting a specific OS, and Delivery Optimization (download mode and bandwidth %). Watch for the trap that WUfB requires the update source to be Windows Update, not WSUS.
- For Conditional Access and compliance, trace the full chain: compliance policy evaluation, the grace period before a device is marked non-compliant, sync timing to Entra ID, then the CA grant control that blocks or allows access. Sync delays are a frequent 'why is this device non-compliant' answer.

---

Want the full breakdown? See the complete **[MD-102 study guide](https://certgrid.app/study-guide/md-102-microsoft-endpoint-administrator)** and **[free practice questions](https://certgrid.app/practice/md-102-microsoft-endpoint-administrator)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

