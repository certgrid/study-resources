# Linux Foundation Certified System Administrator (LFCS) - Study Cheatsheet

The Linux Foundation Certified System Administrator (LFCS) is a hands-on, performance-based exam that validates the day-to-day skills of an entry- to mid-level Linux administrator: managing users and permissions, configuring networking and storage, operating running systems with systemd, and using essential shell commands. You work in a live terminal for 120 minutes, need 660/1000 to pass, and the tasks are practical (configure this service, fix this mount, grant that access) rather than multiple-choice. It suits sysadmins, DevOps engineers, and support staff who manage Linux servers.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | Linux Foundation Certified System Administrator (LFCS) |
| Credential | Linux Foundation Certified System Administrator (LFCS) |
| Level | Intermediate |
| Practice mock length | ~60 questions |
| Duration | ~120 minutes |
| Passing score | 660 out of 1000 |
| Notes reviewed | 2026-06-23 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Essential Commands | ~21% |
| 2 | Operation of Running Systems | ~23% |
| 3 | User and Group Management | ~20% |
| 4 | Networking | ~20% |
| 5 | Storage Management | ~16% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Essential Commands

- Permission mode 754 means owner rwx, group r-x, others r--; chmod accepts octal (chmod 755 file) or symbolic notation (chmod u=rwx,go=rx file or chmod g+s dir).
- chown changes the user owner (and group with user:group syntax); only root can give a file to another user, while a regular owner may only change a file's group to one they belong to.
- The setuid bit (chmod u+s, shown as 's' in the owner execute position) makes an executable run with the file owner's privileges, which is how unprivileged users run tools like passwd.
- The setgid bit on a directory (chmod g+s or chmod 2770) makes new files inside inherit the directory's group rather than the creator's primary group, which is key for shared project directories.
- The sticky bit on a directory (chmod 1770 or +t, as on /tmp) lets users delete only their own files, preventing one user from removing another's files in a shared writable directory.
- setfacl -m u:bob:rw file grants user bob read/write via POSIX ACLs beyond standard owner/group/other bits; getfacl displays them and the mode string shows a trailing '+' when ACLs are present.

### Domain 2 - Operation of Running Systems

- systemctl enable --now <unit> both enables a service at boot and starts it immediately; enable and start are otherwise independent (a unit can run now, be enabled for boot, or both).
- After editing or adding a unit file you must run systemctl daemon-reload so systemd rereads configuration; without it systemd keeps using the cached old definition.
- Prefer systemctl edit <unit> to create a drop-in override under /etc/systemd/system/<unit>.d/ rather than editing the vendor unit file, so changes survive package upgrades.
- systemctl set-default multi-user.target sets the boot target to non-graphical multi-user; systemctl isolate rescue.target switches to single-user rescue mode for maintenance.
- journalctl reads the systemd journal; cap its size by setting SystemMaxUse= (e.g., 500M) in /etc/systemd/journald.conf and reclaim space immediately with journalctl --vacuum-size=500M.
- df -h shows free space per filesystem and df -i shows inode usage; du -sh * summarizes which directories consume the most space, complementing df's per-filesystem view.

### Domain 3 - User and Group Management

- useradd is the low-level account tool (often needing -m to create a home and -s for shell) while adduser is an interactive higher-level wrapper on Debian/Ubuntu; both write to /etc/passwd and /etc/shadow.
- useradd -r -s /usr/sbin/nologin -M svcacct creates a system (service) account with no login shell and no home directory, the standard pattern for daemons.
- usermod -aG <group> <user> adds a supplementary group without removing existing ones; omitting -a (usermod -G) replaces all supplementary groups, a common accidental-removal gotcha.
- usermod -g <group> <user> changes the primary group; gpasswd -a <user> <group> also adds to a supplementary group and gpasswd manages group administrators.
- Supplementary group changes take effect only in new login sessions or after running newgrp; existing shells keep their old group membership.
- Files placed in /etc/skel are copied into each new user's home directory at creation; /etc/default/useradd sets the default shell, home base, and skel location.

### Domain 4 - Networking

- The iproute2 ip command is the modern tool: ip addr shows interface addresses, ip route shows the routing table, and ip link manages interfaces, replacing the deprecated ifconfig.
- ip addr add 192.168.1.50/24 dev eth0 and ip route add default via 10.0.0.1 configure addressing at runtime, but these changes are not persistent across reboots.
- Persistent network config comes from declarative files: systemd-networkd .network files or NetworkManager keyfiles (nmcli/nmtui), not from raw ip commands.
- hostnamectl set-hostname app-server01 sets the static hostname persistently; hostname -I and ip -4 addr show display the system's current IPv4 addresses.
- /etc/resolv.conf lists nameserver and search directives for DNS, but it is often a managed symlink regenerated by systemd-resolved or NetworkManager, so edit the manager's config instead.
- /etc/hosts provides static name-to-IP mappings, and /etc/nsswitch.conf's hosts line typically checks 'files' before 'dns', letting local entries override DNS.

### Domain 5 - Storage Management

- Debian/Ubuntu use APT over dpkg for .deb packages (apt update refreshes the index from /etc/apt/sources.list*, apt install resolves dependencies); RHEL/Fedora use DNF (successor to YUM) for RPMs.
- dpkg -S /path/file reports which installed package owns a file on Debian systems, and apt-file can search package contents not yet installed; rpm -qf is the RPM-side equivalent.
- Grow an LVM logical volume online with lvextend -L +5G /dev/vg/lv, then resize the filesystem: resize2fs for ext4 or xfs_growfs (mounted) for XFS; XFS cannot be shrunk.
- If a deleted file still consumes space, a running process is holding it open; find the holder with lsof and restart or signal it to truly free the space.
- When a partition reports full but has free bytes, it may have exhausted inodes; check df -i, then delete large numbers of tiny unneeded files to free inodes.
- Reference devices in /etc/fstab by UUID or LABEL rather than /dev/sdX names, since kernel device naming can change between boots.

## Study tips

- The exam is performance-based in a live terminal, so practice typing real commands fast; bookmark man pages and use --help, since documentation is available during the test but slow lookups cost time.
- After any unit-file or fstab change, immediately run systemctl daemon-reload (and verify with systemctl status or mount -a in a safe way) so your change actually takes effect before moving on.
- Make configuration persistent, not just runtime: ip addr/route, sysctl, and firewall-cmd without --permanent all revert, so confirm changes survive a reboot when the task implies permanence.
- Always reference storage by UUID/LABEL in fstab and test a new fstab entry with mount -a before relying on it, since a typo can leave the system unbootable.
- Read each task for whether it wants the change 'now', 'at boot', or 'both', and use enable --now or separate enable/start accordingly; partial credit is given per objective, so finish easy tasks first.

---

Want the full breakdown? See the complete **[Linux Foundation Certified System Administrator (LFCS) study guide](https://certgrid.app/study-guide/linux-foundation-certified-system-administrator-lfcs)** and **[free practice questions](https://certgrid.app/practice/linux-foundation-certified-system-administrator-lfcs)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

