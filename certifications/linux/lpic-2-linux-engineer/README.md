# LPIC-2: Linux Engineer - Study Cheatsheet

LPIC-2: Linux Engineer validates the advanced administration skills needed to manage small-to-medium mixed networks, covering the kernel, capacity planning, system startup, storage, networking, and core network services (web, file, DNS, email). It is aimed at experienced administrators who already hold LPIC-1 and run production Linux systems. The certification is split across two exams (201 and 202) and tests both command-line fluency and architectural judgment.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | LPIC-2 |
| Credential | LPIC-2: Linux Engineer |
| Level | Intermediate |
| Practice mock length | ~60 questions |
| Duration | ~90 minutes |
| Passing score | 625 out of 1000 |
| Notes reviewed | 2026-06-23 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Capacity Planning | ~16% |
| 2 | Linux Kernel | ~16% |
| 3 | System Startup | ~17% |
| 4 | Filesystem and Devices | ~17% |
| 5 | Networking Configuration | ~18% |
| 6 | System Services | ~16% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Capacity Planning

- vmstat reports paging activity, run/blocked process counts, block I/O, and CPU time; the si/so columns show pages swapped in/out per second and should normally read 0.
- free -m distinguishes 'used', 'free', and 'available' memory; because buffers/cache are reclaimable, the 'available' column is the true indicator of memory pressure, not 'free'.
- Sustained nonzero si/so in vmstat combined with growing used swap and near-zero available memory signals a genuine memory shortage rather than normal caching.
- iostat -x shows per-device %util (approaching 100% means saturation) plus await (average I/O service time); high values indicate the disk is the bottleneck.
- High %iowait in top/iostat means the CPU is idle waiting on I/O; processes stuck in the D (uninterruptible sleep) state are blocked on disk or network I/O.
- sysstat provides sar for historical trend analysis; sadc (the data collector, run via sa1) writes binary records under /var/log/sa/saNN, read back with sar -u -f.

### Domain 2 - Linux Kernel

- modprobe loads a module by name and automatically resolves dependencies via modules.dep, unlike the low-level insmod which loads only one explicit file; modprobe -r unloads modules.
- lsmod formats /proc/modules into a table of loaded modules with their size and the modules that depend on each one.
- depmod scans installed modules and rebuilds modules.dep, the dependency map modprobe consults; run it after adding new modules.
- Module options are set persistently in a file under /etc/modprobe.d/ ending in .conf, using the syntax 'options <module> <param>=<value>'.
- To prevent a module from auto-loading, add 'blacklist <module>' in /etc/modprobe.d/*.conf; to fully block manual loading too, also set 'install <module> /bin/true'.
- To force a module to load early at boot, list it in a file under /etc/modules-load.d/; modprobe behavior and options stay in /etc/modprobe.d/.

### Domain 3 - System Startup

- systemd starts units in parallel based on declared dependencies and supports socket and D-Bus activation to launch services on demand.
- systemctl is the primary control tool: start, stop, restart, enable (autostart), disable, mask, and status; it is dependency-aware and logs to the journal.
- disable removes autostart but still permits manual start; mask symlinks the unit to /dev/null so it cannot be started by any means until unmasked.
- Ordering and requirements are separate: After=/Before= set sequence, while Wants= (soft) and Requires= (hard) set dependency strength; a network service should use After= and Wants= on network-online.target.
- systemctl set-default <target> sets the boot target (e.g., multi-user.target or graphical.target); systemctl list-dependencies <target> shows what it pulls in.
- rescue.target (formerly runlevel 1) gives a minimal single-user maintenance environment; emergency.target is even more minimal with only the root filesystem mounted read-only.

### Domain 4 - Filesystem and Devices

- Reference filesystems in /etc/fstab by UUID= or LABEL= rather than kernel device names like /dev/sdb1, because device names can change between boots while UUIDs are stable.
- Growing an ext filesystem on LVM is a two-step process: lvextend -L +10G /dev/vg/lv to enlarge the logical volume, then resize2fs /dev/vg/lv to grow the filesystem onto it.
- XFS can be grown online with xfs_growfs but cannot be shrunk; repair is done offline with xfs_repair on an unmounted device, and fsck.xfs is effectively a no-op.
- df reports space usage but a filesystem can report full while df shows free space if it has exhausted its inodes; check inode usage with df -i.
- LVM snapshots create an online point-in-time copy of a volume, ideal for consistent backups of a live filesystem without taking it offline.
- mount -o ro mounts a filesystem read-only, useful for safe inspection or recovery; mount -o remount,rw changes it back without unmounting.

### Domain 5 - Networking Configuration

- ip route from iproute2 prints the kernel routing table (destination, via gateway, dev); the legacy route -n shows the same data numerically.
- ip route add default via <gateway> sets the default route and ip route add 10.0.0.0/24 via 192.168.1.1 dev eth0 adds a static route; both are non-persistent and lost on reboot.
- ip addr add <ip>/<mask> dev <iface> assigns an address live; persistence requires a NetworkManager profile (nmcli) or the distro's interface config files.
- nmcli con add type ethernet with ipv4.method manual and a static ipv4.addresses entry creates a persistent connection profile under NetworkManager.
- ss -tlnp lists listening TCP sockets numerically with the owning PID and program, replacing the older netstat -tlnp for identifying which daemon owns a port.
- tcpdump uses BPF filter syntax: tcpdump -i eth0 tcp port 443 captures only HTTPS traffic on eth0, and -n disables name resolution for speed and clarity.

### Domain 6 - System Services

- OpenSSH server config is /etc/ssh/sshd_config; harden with PermitRootLogin no (or prohibit-password) and PasswordAuthentication no using key-based authentication, effective after reload.
- StrictModes in sshd rejects key auth if ~/.ssh or ~/.ssh/authorized_keys is group- or other-writable, or the user's home directory is writable by group/other; fix the permissions.
- Apache config lives under /etc/httpd (Red Hat) or /etc/apache2 (Debian); validate syntax with apachectl configtest or httpd -t before reloading.
- The DocumentRoot directive sets the directory served for a host or virtual host; the first-listed virtual host serves requests whose Host header matches no ServerName or ServerAlias.
- BIND's named reads named.conf; validate with named-checkconf and validate zone files with named-checkzone; forgetting to increment the SOA serial means secondaries never pull the update.
- A secondary (slave) DNS zone receives updates via zone transfers triggered by NOTIFY from the primary, providing redundancy without manual zone editing.

## Study tips

- Know the persistence boundary cold: ip addr/ip route, sysctl -w, and modprobe options are all volatile, while /etc/sysctl.d/, /etc/modprobe.d/, NetworkManager profiles, and iptables-save make them survive a reboot. The exam loves to ask which command persists a change.
- For each network service, memorize the daemon name, its main config file, and its syntax-check command: sshd_config, httpd/apache2 + apachectl configtest, named.conf + named-checkconf/named-checkzone, main.cf for Postfix. Wrong config path by distro is a common trap.
- Distinguish systemd verbs precisely: enable vs start, disable vs mask, Wants vs Requires, After vs network-online.target. These nuanced differences appear repeatedly.
- Practice the LVM grow workflow end to end (pvresize, vgextend, lvextend -L +N, then resize2fs for ext or xfs_growfs for XFS) and remember XFS cannot shrink and uses xfs_repair, not fsck.
- Read interpretation of monitoring output is heavily tested: nonzero si/so means swapping, high %iowait plus D-state processes means I/O bottleneck, and 'available' (not 'free') memory is the real metric. Be ready to diagnose from sample vmstat/iostat/free output.

---

Want the full breakdown? See the complete **[LPIC-2 study guide](https://certgrid.app/study-guide/lpic-2-linux-engineer)** and **[free practice questions](https://certgrid.app/practice/lpic-2-linux-engineer)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

