# CompTIA Linux+ (XK0-005) - Study Cheatsheet

CompTIA Linux+ (XK0-005) validates the skills needed to administer Linux systems across distributions, covering system management, scripting and automation, security, and troubleshooting. It is a 90-minute exam (up to 90 questions, passing score 720 on a 100-900 scale) aimed at early-career sysadmins, DevOps engineers, and cloud/Linux support technicians with about 12 months of hands-on experience.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | CompTIA Linux+ (XK0-005) |
| Credential | CompTIA Linux+ (XK0-005) |
| Level | Intermediate |
| Practice mock length | ~90 questions |
| Duration | ~90 minutes |
| Passing score | 720 out of 1000 |
| Notes reviewed | 2026-06-23 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | System Management | ~26% |
| 2 | Scripting and Automation | ~24% |
| 3 | Security | ~25% |
| 4 | Troubleshooting | ~25% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - System Management

- systemctl is the front-end to systemd: 'systemctl start/stop/restart' controls a running service, 'enable' sets autostart at boot, 'disable' removes it, and 'mask' prevents the unit from starting at all. 'systemctl enable --now <svc>' enables and starts in one step.
- chmod sets permission bits using octal (e.g. 755 = rwxr-xr-x) or symbolic notation (e.g. u+x, g-w, o=r). It changes only permissions, never ownership; use chown for ownership and chgrp for group.
- Standard permission digits: read=4, write=2, execute=1. On directories, execute (x) means the ability to enter/traverse, and read (r) means the ability to list contents.
- Package managers by family: apt/dpkg on Debian/Ubuntu (.deb), dnf/yum and rpm on RHEL/Fedora/CentOS (.rpm), and zypper on SUSE. 'dnf autoremove' and 'apt autoremove' reclaim space from orphaned dependencies.
- tar archives: 'tar -czf archive.tar.gz dir' creates a gzip archive, '-cJf' uses xz compression, '-cjf' uses bzip2; extract with '-xzf'. The 'f' flag must immediately precede the filename.
- Hard links (ln source target) point multiple names to the same inode and cannot cross filesystems; symbolic links (ln -s target link) store a path and can span filesystems but break if the target moves.

### Domain 2 - Scripting and Automation

- The shebang on line 1 (e.g. #!/bin/bash) tells the kernel which interpreter to run the script with; the script must also have execute permission (chmod +x) to run as ./script.sh.
- Positional parameters: $0 is the script name, $1..$9 are arguments, $# is the argument count, $@ and $* expand to all arguments, and $? holds the exit status of the last command.
- By Unix convention exit code 0 means success and any non-zero value means failure; set an explicit status with 'exit N' and test it via $? or directly in 'if cmd; then'.
- Capture command output with command substitution: var=$(command) (preferred over legacy backticks because it nests cleanly). Arithmetic uses $(( ... )).
- Control flow: for/do/done iterates a list, while/do/done loops while a condition holds, if/then/elif/else/fi branches, and case/esac matches patterns with *) as the default clause.
- Read a file line by line safely with 'while IFS= read -r line; do ...; done < file' - the -r flag prevents backslash interpretation and IFS= preserves leading/trailing whitespace.

### Domain 3 - Security

- SSH provides an encrypted channel for remote login and command execution, replacing cleartext Telnet/rsh. Harden /etc/ssh/sshd_config with 'PermitRootLogin no' and 'PasswordAuthentication no' to enforce key-only access.
- Mandatory Access Control: SELinux (label/context-based, default on RHEL/Fedora) and AppArmor (path-based, default on Debian/SUSE) confine processes beyond standard owner permissions. Check SELinux mode with getenforce; modes are Enforcing, Permissive, Disabled.
- Fix a mislabeled file's SELinux context with restorecon, view contexts with 'ls -Z', and toggle policy booleans with setsebool -P. SELinux denials are logged in the audit log (ausearch/sealert).
- sudo grants per-command elevated privileges per /etc/sudoers and logs every invocation for accountability; always edit the policy with visudo (syntax checking) rather than editing /etc/sudoers directly.
- Firewall front-ends: firewalld uses 'firewall-cmd --permanent --add-port=443/tcp' then --reload; ufw uses 'ufw allow 22' and 'ufw status'; both manage the kernel netfilter rules (nftables/iptables underneath).
- Best practice is a default-deny inbound firewall policy with explicit allow rules only for required ports, combined with installing only needed packages and disabling unused services to shrink the attack surface.

### Domain 4 - Troubleshooting

- When a service fails, start with 'systemctl status <svc>' for state and recent errors, then 'journalctl -u <svc>' for full logs; -f follows live, -n N shows the last N lines, and -b limits to the current boot.
- Disk space: 'df -h' shows per-filesystem usage in human-readable units, while 'df -i' shows inode usage - a filesystem can report space free yet still fail writes if inodes are exhausted.
- Find what is consuming space with 'du -sh */ | sort -h' to rank directories by size; combine with find to locate large or old files.
- A file deleted while still held open by a running process keeps consuming space until the process closes it; find such files with 'lsof | grep deleted' and reclaim space by restarting the process.
- Memory diagnosis: 'free -h' shows total/used/free/buffers/cache, and vmstat reveals swapping (si/so columns) that indicates memory pressure; steadily climbing usage suggests an application memory leak.
- The kernel ring buffer (dmesg) records hardware and kernel events; 'dmesg -T | grep -i oom' reveals Out-Of-Memory killer activity when the kernel terminates processes under memory exhaustion.

## Study tips

- Watch for distribution-specific commands: the exam tests both families, so know apt/dpkg (Debian/Ubuntu) versus dnf/yum/rpm (RHEL/Fedora) and firewalld versus ufw, and pick the tool that matches the stated distro.
- Memorize octal-to-symbolic permission mapping cold (4=r, 2=w, 1=x) - you will be asked to convert both directions and to predict the effect of setuid/setgid/sticky bits.
- Performance-based questions (PBQs) ask you to type real commands or fill in config files; practice in an actual terminal so syntax like tar flags, fstab fields, and cron schedules is muscle memory.
- Prefer modern tools in answers when both appear: ip over ifconfig, ss over netstat, systemctl/journalctl over service/legacy logs, and systemd timers over cron when scheduling features matter.
- When a scenario describes a failing service, follow the standard order - check status, read journalctl/log, verify config, check permissions/ownership, then resources - and choose the diagnostic step before any destructive fix.

---

Want the full breakdown? See the complete **[CompTIA Linux+ (XK0-005) study guide](https://certgrid.app/study-guide/comptia-linux-xk0-005)** and **[free practice questions](https://certgrid.app/practice/comptia-linux-xk0-005)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

