# Red Hat Certified System Administrator (RHCSA, EX200-style) - Study Cheatsheet

The Red Hat Certified System Administrator (RHCSA, EX200) is a 2.5-hour, entirely hands-on performance exam that validates core Red Hat Enterprise Linux administration skills with no multiple-choice questions. Candidates must complete real tasks on live systems covering the shell, file systems, storage, users and permissions, SELinux, services, software management, and basic security. It is intended for system administrators who manage RHEL servers and is the prerequisite foundation for the RHCE certification.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | Red Hat Certified System Administrator (RHCSA, EX200-style) |
| Credential | Red Hat Certified System Administrator (RHCSA, EX200-style) |
| Level | Intermediate |
| Practice mock length | ~60 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-06-23 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Operate Running Systems | ~22% |
| 2 | Local Storage and File Systems | ~21% |
| 3 | Users and Groups | ~21% |
| 4 | Deploy and Manage Software | ~20% |
| 5 | Manage Security | ~16% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Operate Running Systems

- systemctl get-default shows the persistent default boot target; systemctl set-default multi-user.target changes it, and systemctl isolate <target> switches the running system immediately without persisting across reboot.
- To reset a lost root password: interrupt GRUB and append rd.break to the kernel line, then mount -o remount,rw /sysroot, chroot /sysroot, passwd root, and create /.autorelabel before exiting so SELinux contexts are fixed on next boot.
- Common systemd targets are multi-user.target (text, like old runlevel 3), graphical.target (GUI, runlevel 5), rescue.target (single-user with most services), and emergency.target (minimal, root filesystem mounted read-only).
- hostnamectl set-hostname server1.example.com sets the static hostname persistently in /etc/hostname; hostnamectl status also shows transient and pretty hostnames plus OS and kernel info.
- journalctl -u <unit> filters the systemd journal by service unit; -b limits to the current boot, -f follows live, -p err filters by priority, and --since/--until filter by time.
- The systemd journal is volatile by default; create /var/log/journal (and restart systemd-journald or set Storage=persistent in journald.conf) to make it persist across reboots.

### Domain 2 - Local Storage and File Systems

- Standard MBR partitioning uses fdisk and GPT-aware tasks use gdisk or parted; after partitioning a running disk run partprobe or udevadm settle so the kernel re-reads the partition table.
- Create swap with mkswap /dev/vdb2 then activate with swapon /dev/vdb2; make it persistent with an /etc/fstab entry using type swap, and verify with swapon --show or free -h.
- Always reference filesystems in /etc/fstab by UUID= or LABEL= rather than device names like /dev/vdb1, because kernel device naming can change between boots.
- After editing /etc/fstab run mount -a to mount everything and catch syntax errors; a bad fstab entry can drop the system into emergency mode at boot, so always test before rebooting.
- Use the nofail option (and _netdev for network filesystems) on non-critical or NFS mounts so a missing device does not block boot; _netdev defers the mount until networking is up.
- mkfs.xfs creates the default RHEL filesystem; XFS can grow online with xfs_growfs but cannot be shrunk; ext4 (mkfs.ext4) can be shrunk offline with resize2fs.

### Domain 3 - Users and Groups

- useradd creates accounts and updates /etc/passwd, /etc/shadow, /etc/group, and /etc/gshadow; useradd -u 1500 -d /home/sara -s /bin/bash sara sets a specific UID, home, and shell.
- usermod -aG wheel bob appends a supplementary group; omitting -a with -G replaces all supplementary groups, so usermod -G wheel alice removes alice from every other secondary group.
- Lock an account with usermod -L user (or passwd -l), unlock with -U; a non-login service account uses a shell of /sbin/nologin so it cannot log in interactively.
- Members of the wheel group get sudo access by default in RHEL; add a user with usermod -aG wheel <user>, and group membership only takes effect at next login or after newgrp.
- chage manages password aging: chage -E 2026-12-31 user sets account expiration, -M sets max password age, -m sets minimum, and chage -l user lists current settings.
- Systemwide account defaults come from /etc/login.defs (UID/GID ranges, password aging) and /etc/default/useradd (default shell, home base, skel directory).

### Domain 4 - Deploy and Manage Software

- dnf is the RHEL 8/9 package manager: dnf install/remove/update manage packages and resolve dependencies from repos, while rpm -i installs a single local file without resolving dependencies.
- Install a local RPM with its dependencies using dnf install ./package.rpm; dnf provides /usr/sbin/httpd and rpm -qf <path> identify which package supplies a file.
- Add a repository by creating a .repo file in /etc/yum.repos.d/ or running dnf config-manager --add-repo <url>; each repo needs a unique id, baseurl, and enabled setting.
- Enable GPG signature checking by importing the key and setting gpgcheck=1 in the repo definition so dnf verifies package authenticity before installing.
- DNF application streams (modules) let you pick a software version: dnf module list shows streams, dnf module enable nodejs:18 selects one, then dnf install nodejs installs it.
- Only one stream of a module can be enabled at a time; switching to a different stream often requires dnf module reset <name> first to clear the prior selection.

### Domain 5 - Manage Security

- SELinux enforces Mandatory Access Control by labeling processes and files with security contexts (user:role:type:level) and applying policy, independent of standard user/group DAC permissions.
- getenforce shows the current mode (Enforcing, Permissive, or Disabled); setenforce 0/1 changes it at runtime, and the persistent mode is set in /etc/selinux/config; sestatus gives a full summary.
- Set persistent SELinux file contexts with semanage fcontext -a -t httpd_sys_content_t '/web(/.*)?' then apply with restorecon -Rv /web; restorecon resets labels to the policy-defined value.
- chcon changes a context immediately but the change is reverted by a relabel or restorecon; only a semanage fcontext rule survives a filesystem relabel, so prefer semanage for permanence.
- SELinux booleans toggle policy behavior: getsebool -a lists them, setsebool httpd_can_network_connect on sets it at runtime, and the -P flag (setsebool -P) makes it persist.
- Diagnose SELinux denials by reading AVC messages with ausearch -m AVC or sealert; never disable SELinux to fix a service - adjust the context, boolean, or port instead.

## Study tips

- RHCSA is 100% hands-on with no multiple-choice; practice executing real tasks in a RHEL 9 VM until commands are muscle memory, since you are graded on the resulting system state, not on theory.
- Make every change persistent and verify it survives a reboot - the most common point loss is configuring something at runtime (mounts, firewall rules, SELinux booleans) but forgetting to make it permanent.
- Reboot your exam machine at least once midway through to confirm nothing you changed breaks boot; a broken /etc/fstab or default target can cost you multiple tasks at the end if discovered too late.
- Lean on built-in documentation: man -k <keyword>, the examples in man pages, /usr/share/doc, and command --help are all available during the exam, so know how to search them quickly.
- Use UUIDs or LABELs in /etc/fstab, run mount -a to validate before rebooting, and remember to run restorecon and daemon-reload after changes that affect SELinux labels or unit files.

---

Want the full breakdown? See the complete **[Red Hat Certified System Administrator (RHCSA, EX200-style) study guide](https://certgrid.app/study-guide/red-hat-certified-system-administrator-rhcsa-ex200-style)** and **[free practice questions](https://certgrid.app/practice/red-hat-certified-system-administrator-rhcsa-ex200-style)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

