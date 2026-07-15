# CompTIA Linux+ (XK0-006) - Study Cheatsheet

CompTIA Linux+ (XK0-006), the V8 release, validates the skills needed to configure, manage, secure, automate, and troubleshoot Linux systems across distributions. It is a 90-minute exam (up to 90 questions, passing score 720 on a 100-900 scale) aimed at early-career sysadmins, DevOps engineers, and cloud/Linux support technicians with about 12 months of hands-on experience. Compared with XK0-005, V8 reorganizes the objectives into five domains and adds explicit coverage of containers, orchestration with Ansible, infrastructure as code, and the responsible use of AI tools.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | CompTIA Linux+ (XK0-006) |
| Credential | CompTIA Linux+ (XK0-006) |
| Level | Intermediate |
| Practice mock length | ~90 questions |
| Duration | ~90 minutes |
| Passing score | 720 out of 900 |
| Notes reviewed | 2026-07-15 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | System Management | 23% |
| 2 | Services and User Management | 20% |
| 3 | Security | 18% |
| 4 | Automation, Orchestration, and Scripting | 17% |
| 5 | Troubleshooting | 22% |

_Weightings reflect the official XK0-006 objective domains. Confirm the current objectives on the vendor site._

## Key concepts by domain

### Domain 1 - System Management

- systemd/systemctl controls services: 'start/stop/restart' act on a running unit, 'enable' sets autostart, 'disable' removes it, and 'mask' blocks the unit entirely. 'systemctl enable --now <svc>' enables and starts in one step.
- Storage is layered: partitions (fdisk/parted, GPT vs MBR) hold physical volumes, LVM groups them into volume groups and carves out logical volumes you can grow with lvextend + resize2fs/xfs_growfs, and a filesystem (mkfs.xfs/ext4) is mounted via /etc/fstab using a UUID.
- NetworkManager is the standard stack: 'nmcli con add/mod/up' configures connections persistently, while 'ip addr' and 'ip route' show live state; resolution flows through /etc/nsswitch.conf, /etc/resolv.conf (or systemd-resolved), and /etc/hosts.
- tar archives: 'tar -czf archive.tar.gz dir' creates a gzip archive, '-cJf' uses xz, '-cjf' uses bzip2; extract with '-xzf'. rsync -avz syncs efficiently (including over SSH), and dd makes block-level copies.
- Package managers by family: apt/dpkg on Debian/Ubuntu (.deb), dnf/yum and rpm on RHEL/Fedora (.rpm), plus universal flatpak and snap. Query a file's owning package with 'rpm -qf' or 'dpkg -S'.
- Virtualization centers on KVM with libvirt ('virsh' manages guests, 'virt-install' builds them, cloud-init customizes first boot); containers share the host kernel and are lighter than full VMs.

### Domain 2 - Services and User Management

- Permissions combine rwx for user/group/other. chmod sets them in octal (755 = rwxr-xr-x) or symbolic (u+x, g-w); read=4, write=2, execute=1. On directories, execute grants traversal and read grants listing.
- Special bits: SUID (4) runs a file as its owner, SGID (2) runs as the group or forces group inheritance on directories, and the sticky bit (1) on a shared directory like /tmp lets only the owner delete their files.
- User admin uses useradd/usermod/userdel and groupadd; account data lives in /etc/passwd, encrypted passwords and aging in /etc/shadow, and groups in /etc/group. 'usermod -aG group user' appends a supplementary group without dropping existing ones.
- sudo grants controlled privilege escalation - edit policy only with visudo (which validates syntax) in /etc/sudoers or a file under /etc/sudoers.d; this is safer than sharing the root password.
- Containers are managed with podman (or docker): 'podman run -d -p 8080:80 image' launches one, 'podman ps' lists running containers, and 'podman build -t name .' builds from a Containerfile. Rootless podman and Quadlet units run containers as systemd services.
- Package and service state: dnf/apt install/remove software, and systemctl plus journald manage and log the resulting services.

### Domain 3 - Security

- SSH key authentication beats passwords: generate a keypair with ssh-keygen, copy the public key with ssh-copy-id, then harden sshd_config with 'PermitRootLogin no' and 'PasswordAuthentication no'.
- Mandatory Access Control: SELinux (label/context-based, default on RHEL/Fedora) and AppArmor (path-based, default on Debian/SUSE). Check SELinux mode with getenforce, fix mislabeled files with 'restorecon -Rv', and toggle booleans with 'setsebool -P'; translate denials with ausearch + audit2allow.
- Host firewalls: firewalld uses 'firewall-cmd --add-service/--add-port --permanent' then '--reload' with zones; nftables is the modern packet framework; ufw is the simple Debian/Ubuntu front-end ('ufw allow 22/tcp').
- Authentication policy runs through PAM (/etc/pam.d): pam_pwquality enforces password complexity and pam_faillock locks accounts after repeated failures; chage sets password aging.
- Cryptography: GPG encrypts/signs files with public/private keys, OpenSSL generates keys/CSRs/self-signed certs, LUKS (cryptsetup) encrypts whole disks, and sha256sum verifies file integrity.
- Compliance and auditing: auditd records security events (ausearch/aureport), AIDE detects file tampering against a baseline, and OpenSCAP/Lynis assess systems against benchmarks such as CIS.

### Domain 4 - Automation, Orchestration, and Scripting

- A Bash script starts with a shebang (#!/bin/bash); variables are set without spaces (name=value) and expanded as "$name". $? holds the last exit status, where 0 means success. Always quote variables to prevent word-splitting.
- Control flow uses if/elif/else with test brackets ([ ] or [[ ]]) and operators like -f, -z, and -eq; loops include for, while, and until; case handles multiple patterns. Robust scripts use 'set -euo pipefail'.
- Scheduling: cron runs jobs on a five-field schedule (min hour day-of-month month day-of-week), 'at' runs a one-off job, and systemd timers (OnCalendar) are a modern, journald-integrated alternative.
- Ansible is agentless orchestration driven by YAML playbooks over SSH. An inventory lists hosts; plays map modules (copy, file, package, service, user) to tasks; idempotency means re-running changes nothing if the system already matches the desired state.
- Git provides version control for scripts and IaC: 'git add' stages, 'git commit -m' records, 'git push/pull' sync with a remote, and .gitignore excludes files. Infrastructure as code (Terraform, cloud-init) describes desired state rather than steps.
- Responsible AI use (new in V8): always review and test AI-generated commands or scripts before running them, never paste secrets, credentials, or personal data into external AI tools, and keep a human in the loop because models can produce confident but incorrect output.

### Domain 5 - Troubleshooting

- Start with top/htop for live CPU and memory, free -h for memory and swap, and uptime for load average (compare it against CPU cores). vmstat and iostat expose CPU, memory, and I/O pressure over time.
- journalctl is the primary log tool: '-u <unit>' filters by service, '-b' shows the current boot, '-p err' filters by priority, and '-f' follows live; dmesg shows the kernel ring buffer for hardware and driver messages.
- Storage problems have distinct signatures: 'df -h' shows a full filesystem, but 'df -i' reveals inode exhaustion when space appears free yet writes fail. Repair unmounted filesystems with fsck (ext) or xfs_repair, and check RAID with /proc/mdstat.
- Network troubleshooting works layer by layer: ping tests reachability, ip route checks the default gateway, 'ss -tulpn' lists listening ports, dig/resolvectl isolates DNS from connectivity, and tcpdump captures packets when needed.
- Security-related failures often trace to SELinux or permissions: a service that works in permissive mode but fails when enforcing points to a labeling issue fixed with restorecon or a boolean; 'Permission denied' points to ownership/mode.
- Performance: high swap (si/so in vmstat) suggests memory pressure, the OOM killer logs "Out of memory: Killed process" in dmesg, and renice/ionice or tuned profiles adjust priority and workload tuning.

## Study tips

- Practice on both an RHEL-family (dnf, firewalld, SELinux) and a Debian-family (apt, ufw, AppArmor) system - XK0-006 is deliberately distribution-neutral.
- Memorize octal-to-symbolic permission mapping cold (4=r, 2=w, 1=x) and umask math - conversion and special-bit (setuid/setgid/sticky) questions are common, quick points.
- Be fluent with podman basics (run, -p, -v, build, ps) and Quadlet/systemd-managed containers, since containers are now a first-class topic.
- For scripting, read a short Bash snippet and predict its output or exit status, and recognize idempotency in an Ansible task; learn the responsible-AI guardrails (validate output, protect secrets, human review).
- When a service fails, follow the standard order - check status, read journalctl/log, verify config, check permissions/ownership, then resources - and choose the diagnostic step before any destructive fix.

---

Want the full breakdown? See the complete **[CompTIA Linux+ (XK0-006) study guide](https://certgrid.app/study-guide/comptia-linux-xk0-006)** and **[free practice questions](https://certgrid.app/practice/comptia-linux-xk0-006)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_
