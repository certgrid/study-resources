# LPIC-1: Linux Administrator - Study Cheatsheet

LPIC-1: Linux Administrator validates the ability to perform maintenance tasks on the command line, install and configure a Linux workstation, and configure basic networking. It is a vendor-neutral certification earned by passing two 90-minute exams (101 and 102), each scored 200-800 with a 500 pass mark, aimed at junior administrators and anyone working at the Linux command line regardless of distribution.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | LPIC-1 |
| Credential | LPIC-1: Linux Administrator |
| Level | Intermediate |
| Practice mock length | ~60 questions |
| Duration | ~90 minutes |
| Passing score | 625 out of 1000 |
| Notes reviewed | 2026-06-23 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | System Architecture | ~20% |
| 2 | Linux Installation and Package Management | ~17% |
| 3 | GNU and Unix Commands | ~17% |
| 4 | Devices, Linux Filesystems, FHS | ~17% |
| 5 | Shells and Shell Scripting | ~16% |
| 6 | User Interfaces and Desktops, Admin Tasks, Networking | ~14% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - System Architecture

- On legacy BIOS systems the firmware loads the boot loader from the Master Boot Record (MBR) in the first 512 bytes of the disk; on UEFI systems the firmware reads boot entries and loads an EFI executable from the EFI System Partition (ESP).
- Check for the directory /sys/firmware/efi to determine whether a system booted in UEFI mode; if it exists the system is UEFI, otherwise it booted via legacy BIOS.
- dmesg prints the kernel ring buffer, a fixed-size in-memory log of kernel messages from boot onward (hardware detection, driver init); on systemd systems journalctl -k shows the same kernel messages.
- /proc/cpuinfo is a kernel-generated pseudo-file showing per-core CPU details: model name, cache size, flags, and core count; /proc/meminfo shows memory and /proc/interrupts shows per-CPU IRQ counts.
- /sys (sysfs) exposes the kernel device model as a navigable tree of buses, devices, and drivers and allows reading/writing kernel parameters at runtime; USB devices appear under /sys/bus/usb/devices/.
- lsmod lists currently loaded kernel modules (reading /proc/modules) with name, size, use count, and dependents; modinfo shows details about a specific module.

### Domain 2 - Linux Installation and Package Management

- The boot loader's job is to load and start the Linux kernel; GRUB 2 is configured by editing /etc/default/grub and templates in /etc/grub.d/, then regenerating /boot/grub/grub.cfg with grub-mkconfig (or update-grub on Debian).
- A minimal UEFI install needs a Linux root (/) partition plus an EFI System Partition (ESP), typically a FAT32 partition mounted at /boot/efi; partition tables are MBR (max ~2 TiB, 4 primary) or GPT (GUID Partition Table) for larger disks.
- dpkg is the low-level Debian tool: dpkg -i package.deb installs a local .deb but does NOT fetch dependencies; running apt-get install -f afterward resolves and installs missing dependencies.
- dpkg -P (purge) removes a package and deletes its configuration files, whereas dpkg -r (remove) leaves config files behind; dpkg -l lists installed packages and dpkg -L lists files owned by a package.
- apt update refreshes the local package index from configured repositories (it installs nothing); apt upgrade then installs newer versions; install a specific version with apt-get install pkg=version.
- APT repositories are defined in /etc/apt/sources.list and files under /etc/apt/sources.list.d/; these tell APT where to download packages and index metadata.

### Domain 3 - GNU and Unix Commands

- The pipe operator | connects the stdout of one command to the stdin of the next; for example ls -la | grep '.txt' filters the listing line by line.
- Redirection: > overwrites a file, >> appends, < feeds a file as stdin; file descriptor 2 is stderr so 2> redirects errors and command > out.log 2>&1 merges stderr into stdout.
- tee writes its input to a file AND passes it through to stdout simultaneously (command | tee output.txt), useful for logging while still seeing or piping output.
- grep searches text for patterns; grep -r searches recursively through a directory tree, grep -i ignores case, grep -v inverts the match, and grep -E enables extended regular expressions.
- find locates files by criteria: find /etc -name '*.conf' matches by name, -size +100M by size, -mtime -7 by modification time within 7 days, and -type f/d by type; quote glob patterns to stop the shell expanding them.
- xargs builds and runs command lines from standard input, commonly paired with find (find ... | xargs rm) to act on each result; find -exec is the in-place alternative.

### Domain 4 - Devices, Linux Filesystems, FHS

- mkfs creates filesystems; mkfs.ext4 (a wrapper for mke2fs) writes the superblock, inode tables, and journal onto a partition, and mkswap formats a partition or file as swap.
- mount attaches a filesystem with the device first and mount point second (mount /dev/sdc1 /mnt/data); the type is auto-detected when -t is omitted; umount detaches it.
- /etc/fstab declares persistent mounts in six fields: device/UUID, mount point, type, options, dump (field 5), and fsck pass order (field 6); 0 in field 6 means never check, 1 is the root filesystem, 2 is other filesystems.
- An fstab NFS line looks like 192.168.1.10:/export/data /mnt/shared nfs defaults 0 0; running mount -a mounts everything in fstab that is not already mounted.
- fsck checks and repairs filesystems and dispatches to a helper such as fsck.ext4 (alias e2fsck); always unmount the partition before running fsck on it to avoid corruption.
- Swap is enabled with mkswap /dev/sdc2 then swapon /dev/sdc2, and disabled with swapoff; swapon -s or free -h shows active swap usage.

### Domain 5 - Shells and Shell Scripting

- A script's first line must be a shebang beginning with the exact two bytes #! followed by the interpreter path, for example #!/bin/bash; the kernel reads it and runs the script with that interpreter.
- chmod +x script.sh sets the execute bit so the script can run as ./script.sh; without execute permission the script must be invoked explicitly as bash script.sh.
- The special parameter $? holds the exit status of the last command (0 = success, non-zero = failure), and scripts test it to decide branching.
- Positional parameters: $1, $2, ... are arguments, $0 is the script name, $# is the argument count, and $@ / $* expand to all arguments.
- Variable assignment has no spaces around = (NAME="John"); a plain assignment is local to the shell, while export NAME="John" places it in the environment so child processes inherit it.
- Quoting matters: single quotes preserve every character literally, while double quotes still allow variable expansion ($VAR) and command substitution ($(cmd) or backticks).

### Domain 6 - User Interfaces and Desktops, Admin Tasks, Networking

- The X Window System is a client-server graphical stack: the X Server manages display and input hardware while a separate Window Manager (and clients) draws and controls windows; the DISPLAY variable names the target display (for example :0).
- Common desktop environments are GNOME, KDE Plasma, and Xfce, and a display manager (gdm, sddm, lightdm) provides graphical login; modern systems may use Wayland instead of the X11 protocol.
- useradd creates an account by writing /etc/passwd, /etc/shadow, and /etc/group; useradd -m creates the home directory and -s sets the login shell (useradd -m -s /bin/bash webadmin).
- /etc/passwd fields (colon-separated) are username, password placeholder x, UID, GID, GECOS comment, home directory, and login shell; encrypted passwords and aging live in /etc/shadow.
- Account maintenance: passwd sets or changes passwords (passwd -l locks, passwd -u unlocks), usermod modifies account attributes, userdel removes accounts, and chage manages password aging.
- cron schedules recurring jobs with five time fields: minute, hour, day-of-month, month, day-of-week (for example 0 3 * * * runs daily at 03:00, and 30 2 * * 0 runs at 02:30 every Sunday); crontab -e edits a user's crontab and /etc/crontab is the system-wide file.

## Study tips

- Master the two package-management families side by side: for every Debian apt/dpkg command know the Red Hat dnf/yum/rpm equivalent, since the exam tests both regardless of which distro you use day to day.
- Memorize the six fstab fields in order and the cron five-field time format cold; these structured-field questions are common and easy points once the column meanings are automatic.
- Practice building real pipelines (grep | sort | uniq | wc -l, find | xargs, sed -i) at an actual terminal rather than memorizing flags, because LPIC-1 favors questions that combine several commands.
- Know which tool is current versus deprecated: prefer ip over ifconfig, ss over netstat, journalctl over reading raw logs, and systemctl targets over numeric runlevels, but recognize the legacy commands too.
- Read each question for exact wording such as overwrite vs append (> vs >>), remove vs purge (dpkg -r vs -P), and isolate vs set-default; LPIC-1 distinguishes closely related commands by their precise behavior.

---

Want the full breakdown? See the complete **[LPIC-1 study guide](https://certgrid.app/study-guide/lpic-1-linux-administrator)** and **[free practice questions](https://certgrid.app/practice/lpic-1-linux-administrator)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

