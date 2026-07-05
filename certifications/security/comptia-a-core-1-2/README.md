# CompTIA A+ (Core 1/2) - Study Cheatsheet

CompTIA A+ (Core 1/2) validates the foundational skills an entry-level IT support technician needs: installing and troubleshooting hardware, mobile devices, networking, operating systems, and security, plus following operational procedures. It is the standard starting credential for help desk, desktop support, and field service roles, and requires passing two exams (Core 1 and Core 2). The scaled passing score is 700-750 out of 900 depending on the exam, with up to 90 questions in 90 minutes per exam.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | CompTIA A+ (Core 1/2) |
| Credential | CompTIA A+ (Core 1/2) |
| Level | Intermediate |
| Practice mock length | ~90 questions |
| Duration | ~90 minutes |
| Passing score | 750 out of 1000 |
| Notes reviewed | 2026-06-23 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Mobile Devices and Hardware | ~11% |
| 2 | Networking | ~20% |
| 3 | Hardware and Network Troubleshooting | ~20% |
| 4 | Operating Systems | ~23% |
| 5 | Security | ~26% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Mobile Devices and Hardware

- SSDs use NAND flash with no moving parts, giving sub-millisecond random access and far better shock resistance than spinning HDDs; NVMe SSDs run over PCIe lanes and reach several GB/s versus SATA's ~550 MB/s ceiling.
- M.2 slots can be keyed B (SATA only), M (PCIe NVMe), or B+M; an NVMe (M-key) drive will not work in a SATA-only (B-key) slot, and on many boards populating an M.2 NVMe slot disables one or more SATA ports because they share lanes.
- DisplayPort and HDMI are digital video/audio interfaces; converting digital HDMI/DisplayPort to analog VGA requires an active (powered) adapter that performs digital-to-analog conversion, not a simple passive pin adapter.
- DDR4 desktop DIMMs have 288 pins; DDR4 laptop SODIMMs have 260 pins and are about half the length. DDR generations are not interchangeable (the notch differs).
- Dual-channel memory requires matched modules installed in the correct same-color (paired) slots per the motherboard manual; placing sticks in the wrong slots drops the system to single-channel and halves bandwidth.
- FAT32 has a 4 GB maximum single-file size and ~2 TB volume limit; exFAT removes those limits (files up to 16 EB) and is the cross-platform choice for large removable media; NTFS is required for the Windows system volume.

### Domain 2 - Networking

- RJ45 (8P8C) connectors terminate twisted-pair Ethernet; Cat5e supports 1 Gbps and Cat6 supports 10GBASE-T over short runs. Twisted-pair Ethernet has a 100-meter (328 ft) maximum run length; exceeding it requires fiber or a repeater/switch.
- RFC 1918 private address ranges are 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16; NAT/PAT (port address translation, overloading) lets many private hosts share one public IP.
- 169.254.0.0/16 is APIPA (link-local), self-assigned when no DHCP server responds and never routed; 127.0.0.0/8 is loopback and never appears on the wire.
- DHCP uses the DORA exchange (Discover, Offer, Request, Acknowledge) over UDP ports 67 (server) and 68 (client) to hand out IP, subnet mask, default gateway, DNS, and lease.
- Key well-known ports: HTTP 80, HTTPS 443, RDP 3389, SSH 22, Telnet 23, FTP 20/21, SMTP 25, DNS 53, DHCP 67/68, SMB 445, RDP 3389; HTTPS wraps HTTP in TLS.
- Wi-Fi co-channel interference in the crowded 2.4 GHz band is avoided by using only the non-overlapping channels 1, 6, and 11 and assigning neighboring access points different channels.

### Domain 3 - Hardware and Network Troubleshooting

- The CompTIA troubleshooting methodology: 1) identify the problem, 2) establish a theory of probable cause, 3) test the theory, 4) establish a plan of action, 5) implement the solution, 6) verify full functionality and apply preventive measures, 7) document findings, actions, and outcomes.
- POST errors (bad RAM or GPU) are signaled by beep codes when the display is not yet initialized; consult the motherboard/BIOS vendor's beep-code chart to interpret them.
- Always wear an ESD anti-static wrist strap and use proper grounding before handling components; electrostatic discharge can silently damage sensitive chips.
- Slow boot/performance troubleshooting: check S.M.A.R.T. drive health and free disk space, disable unnecessary startup programs in Task Manager, and confirm the memory channel mode in BIOS/UEFI.
- Repair tools to know: chkdsk /f /r fixes file-system errors and recovers bad sectors; sfc /scannow repairs corrupted Windows system files; DISM /Online /Cleanup-Image /RestoreHealth repairs the component store backing SFC.
- Performance bottlenecks: a process blocked on slow disk I/O points to the storage subsystem; sustained high CPU temperatures that drop clock speeds indicate thermal throttling from inadequate cooling.

### Domain 4 - Operating Systems

- NTFS is the required default Windows file system, supporting file-level ACL permissions, journaling, encryption (EFS), and compression; exFAT and FAT32 are used mainly for removable media.
- icacls manages NTFS permissions from the command line; e.g., icacls C:\Data /grant jdoe:F grants user jdoe Full Control. Standard NTFS rights are Read, Write, Modify, and Full Control.
- Run as administrator triggers UAC (User Account Control) elevation; least privilege means users run as standard accounts by default and elevate only when an admin task requires it.
- Do not defragment an SSD - it has no seek penalty and the writes only add wear; Windows instead runs TRIM to maintain write performance, and Optimize Drives recognizes SSDs automatically.
- Free up disk space with Disk Cleanup or Storage Sense (removes temp files and old Windows Update files), uninstall unused apps, and move large data files to another volume.
- Process management on Windows: taskkill /IM notepad.exe /F force-ends a process by image name; sc query spooler checks a service state and net stop spooler stops it.

### Domain 5 - Security

- The three authentication factor categories are something you know (password/PIN), something you have (token/phone/smart card), and something you are (biometric). Combining two different categories is multi-factor authentication (MFA).
- Defense in depth layers multiple overlapping controls so one failed control does not cause full compromise; Zero Trust never implicitly trusts based on network location and continuously verifies identity and authorization for every request.
- BitLocker provides full-volume encryption (AES-128/256) in Windows Pro/Enterprise/Education and protects data at rest if a drive is removed; pair encryption at rest with TLS for data in transit.
- Apply least privilege and role-based access control (RBAC) tied to job functions so accounts get only the access required; admins should use separate dedicated admin accounts distinct from daily-use accounts and require MFA for all admin logins.
- Phishing is a social-engineering attack that tricks users into revealing credentials via fraudulent messages; defenses include user training, strong unique passwords, and MFA.
- Ransomware encrypts the victim's files (and often deletes shadow copies and exfiltrates data) then demands payment; offline/immutable backups with tested restores are the primary recovery defense.

## Study tips

- Master the seven-step CompTIA troubleshooting methodology in order and the steps of change management - scenario questions frequently ask for the next step or the first action to take.
- Memorize the common port numbers and RFC 1918 private ranges cold; they appear across both Core 1 and Core 2 and are quick points if you have them instantly.
- Watch for PBQs (performance-based questions) early in the exam - they take the most time, so consider flagging and returning to them so you do not run out of time on the multiple-choice questions.
- Read for the BEST answer when several options are technically valid - questions often hinge on the first/safest step (e.g., isolate before investigate, back up before changing, ESD precautions before touching hardware).
- Know the exact command-line syntax (chkdsk /f /r, sfc /scannow, DISM /RestoreHealth, icacls, taskkill, net user, ipconfig /all) because Core 2 tests literal command knowledge.

---

Want the full breakdown? See the complete **[CompTIA A+ (Core 1/2) study guide](https://certgrid.app/study-guide/comptia-a-core-1-2)** and **[free practice questions](https://certgrid.app/practice/comptia-a-core-1-2)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

