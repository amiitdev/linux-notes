# Linux from Zero to Hero

A complete beginner's guide to Linux - learning everything from the ground up.

---

## Table of Contents

1. [Linux History](#1-linux-history)
2. [Linux Distributions](#2-linux-distributions)
3. [Kernel vs OS](#3-kernel-vs-os)
4. [Linux File System](#4-linux-file-system)
5. [Absolute vs Relative Paths](#5-absolute-vs-relative-paths)

---

## 1. Linux History

### Who created Linux?

- **Linus Torvalds** - A Finnish computer science student
- Created Linux in **1991** as a hobby project
- Started as a free alternative to UNIX
- First announcement was on a Usenet group (comp.os.minix)

### Key Timeline

| Year | Event |
|------|-------|
| 1969 | UNIX created at Bell Labs by Ken Thompson & Dennis Ritchie |
| 1983 | Richard Stallman starts GNU Project (free OS) |
| 1991 | Linus Torvalds releases Linux kernel v0.01 |
| 1992 | Linux becomes licensed under GNU GPL |
| 1993 | Debian and Slackware - first Linux distributions |
| 1994 | Linux kernel v1.0 released |
| 1996 | Linux v2.0 - multiprocessor support |
| 2004 | Ubuntu released (made Linux user-friendly) |
| 2011 | Linux v3.0 - Android runs on Linux |
| 2022 | Linux powers 100% of top 500 supercomputers |

### Why is Linux Important?

- **Free and Open Source** - anyone can view, modify, and distribute the code
- **Runs everywhere** - servers, phones (Android), cars, satellites, routers, IoT devices
- **Secure** - strong permissions model, open source means many eyes review the code
- **Stable** - servers can run for years without rebooting
- **Powers the internet** - over 90% of cloud servers run Linux

---

## 2. Linux Distributions

A **distribution** (distro) = Linux Kernel + Package Manager + Desktop Environment + Utilities

### Popular Distributions

| Distro | Based On | Best For | Package Manager |
|--------|----------|----------|-----------------|
| **Ubuntu** | Debian | Beginners, Desktop, Servers | apt (dpkg) |
| **Debian** | (Original) | Servers, Stability | apt (dpkg) |
| **Linux Mint** | Ubuntu | Beginners, Desktop | apt (dpkg) |
| **Fedora** | (Original) | Developers, Cutting-edge | dnf (rpm) |
| **CentOS/RHEL** | Fedora | Enterprise Servers | yum/dnf (rpm) |
| **Arch Linux** | (Original) | Advanced users, DIY | pacman |
| **Manjaro** | Arch | Beginners who want Arch | pacman |
| **Kali Linux** | Debian | Security/Penetration Testing | apt (dpkg) |
| **openSUSE** | (Original) | Desktop, Servers | zypper (rpm) |

### My System Info

```
$ hostnamectl
 Static hostname: amit
       Icon name: computer-laptop
         Chassis: laptop
Operating System: Linux Mint 22.3
          Kernel: Linux 6.8.0-90-generic
    Architecture: x86-64
 Hardware Vendor: Lenovo
  Hardware Model: IdeaPad Gaming 3 15ACH6
```

I'm using **Linux Mint 22.3** (based on Ubuntu/Debian) with kernel **6.8.0-90-generic**.

---

## 3. Kernel vs OS

### What is a Kernel?

The kernel is the **core** of the operating system. It:
- Manages hardware (CPU, RAM, disk, USB, etc.)
- Manages processes (which program runs when)
- Manages memory (how much RAM each program gets)
- Handles security and permissions
- Acts as a bridge between software and hardware

### What is an Operating System?

OS = **Kernel** + **System Libraries** + **System Utilities** + **Desktop Environment** + **Applications**

```
+--------------------------------------------------+
|              User Applications                   |
+--------------------------------------------------+
|         Desktop Environment (GNOME/KDE)          |
+--------------------------------------------------+
|              System Utilities                     |
+--------------------------------------------------+
|              GNU C Library (glibc)                |
+--------------------------------------------------+
|                  LINUX KERNEL                     |
+--------------------------------------------------+
|            Hardware (CPU, RAM, Disk)              |
+--------------------------------------------------+
```

| Component | Examples |
|-----------|----------|
| Kernel | Linux 6.8.0-90-generic |
| Shell | Bash, Zsh, Fish |
| Desktop | Cinnamon, GNOME, KDE |
| Package Manager | apt, yum, pacman |
| Init System | systemd |

---

## 4. Linux File System

Linux uses a **single tree** structure. Everything starts from `/` (root).

### The Tree Structure

```
/                        <-- Root (everything starts here)
├── bin/                 <-- Essential user commands (ls, cp, mv)
├── boot/                <-- Boot files (kernel, bootloader)
├── dev/                 <-- Device files (hard drives, USB, etc.)
├── etc/                 <-- System configuration files
├── home/                <-- User home directories
│   └── amit/           <-- My home directory (/home/amit)
├── lib/                 <-- Essential shared libraries
├── media/               <-- Mount points for removable devices
├── mnt/                 <-- Temporary mount points
├── opt/                 <-- Optional/third-party software
├── proc/                <-- Process information (virtual)
├── root/                <-- Root user's home directory
├── run/                 <-- Runtime data
├── sbin/                <-- System administration commands
├── srv/                 <-- Service data (web, FTP)
├── sys/                 <-- System information (virtual)
├── tmp/                 <-- Temporary files (deleted on reboot)
├── usr/                 <-- User programs and data
│   ├── bin/             <-- User commands
│   ├── lib/             <-- Libraries
│   ├── local/           <-- Locally installed software
│   ├── sbin/            <-- System commands
│   └── share/           <-- Shared data (icons, docs)
└── var/                 <-- Variable data
    ├── cache/           <-- Package cache
    ├── lib/             <-- Variable state info
    ├── log/             <-- Log files
    └── tmp/             <-- Temporary (persists across reboots)
```

### Key Directories Explained

#### `/` (Root)
The top of the filesystem. Every file and directory starts here.

#### `/home` - User Home Directories
```
$ ls /home
amit
```
Each user gets their own directory: `/home/username`

#### `/etc` - Configuration Files
Contains all system-wide configuration files.
```
$ ls /etc
adduser.conf       bash.bashrc       docker/          hostname
apt/               bluetooth/        fstab            hosts
crontab            cups/             nginx/           passwd
ssh/               sudoers           systemd/         ufw/
```

**Important files in `/etc`:**
| File | Purpose |
|------|---------|
| `/etc/passwd` | User account information |
| `/etc/hostname` | System hostname |
| `/etc/hosts` | Host name resolution |
| `/etc/fstab` | Filesystem mount table |
| `/etc/ssh/` | SSH configuration |

#### `/var` - Variable Data
```
$ ls /var
backups    cache    lib    local    lock
log        mail     opt    run      snap
spool      tmp      www
```

**Key subdirectories:**
| Directory | Purpose |
|-----------|---------|
| `/var/log/` | System and application logs |
| `/var/cache/` | Package manager cache |
| `/var/lib/` | Variable state information |
| `/var/tmp/` | Temporary files (persists) |

#### `/tmp` - Temporary Files
```
$ ls /tmp
cline                      opencode
gemini                     postman-collections-*.md
jenkins-project            ssh-XXXXX
```
Deleted on reboot. Anyone can write here.

#### `/usr` - User Programs
```
$ ls /usr
bin    games    include    lib
lib64  libexec  local      sbin
share  src
```
Contains the majority of user-installed software and libraries.

#### `/bin` - Essential Commands
```
$ ls /bin | head -20
bash      chgrp     chmod     chown     cp
dash      dd        df        dir       dmesg
echo      false     fgrep     grep      gunzip
gzip      hostname  kill      kmod      ln
login     ls        mkdir     mknod     more
mount     mv        nano      networkctl  nice
```
Contains commands needed for single-user mode and system recovery.

#### `/sbin` - System Commands
```
$ ls /sbin | head -20
aa-load              addgroup             adduser
apparmor_parser      aptd                 blkid
brctl                chroot               cron
cryptdisks_start     fdisk                fsck
getty                grub-install         halt
ifconfig             init                 insmod
iptables             ldconfig             reboot
```
Commands for system administration (usually need root/sudo).

#### `/opt` - Optional Software
```
$ ls /opt
android-studio      BurpSuiteCommunity    containerd
google              OpenCode
```
Third-party software that doesn't follow the standard directory layout.

---

## 5. Absolute vs Relative Paths

### Absolute Path
- Starts from `/` (root)
- Always gives the exact location
- Works from anywhere

```
$ pwd
/home/amit

$ cd /home/amit
$ pwd
/home/amit

$ cd /
$ pwd
/
```

### Relative Path
- Starts from your current location
- Uses shortcuts: `.` (current dir), `..` (parent dir), `~` (home)

```
/home/amit$ ls ~/linux-notes/       # ~ = home directory
/home/amit$ cd ../                 # Go up one directory
/home/amit$ cd ../../              # Go up two directories
```

### Path Comparison Table

| Path | Type | Meaning |
|------|------|---------|
| `/home/amit` | Absolute | From root, go to home, then amit |
| `/etc/passwd` | Absolute | From root, go to etc, then passwd |
| `~/linux-notes` | Absolute | Home directory, then linux-notes |
| `../documents` | Relative | Go up one level, then into documents |
| `./script.sh` | Relative | Current directory, script.sh |
| `../../file.txt` | Relative | Go up two levels, then file.txt |

---

## Summary

| Concept | Key Takeaway |
|---------|--------------|
| Linux | Free, open-source OS kernel created in 1991 |
| Distro | Kernel + tools + desktop (Ubuntu, Mint, Fedora, etc.) |
| Kernel | Core that manages hardware and processes |
| `/` | Root - everything starts here |
| `/home` | Your personal directory |
| `/etc` | Configuration files |
| `/var` | Logs, cache, variable data |
| `/tmp` | Temporary files |
| `/bin` | Essential user commands |
| `/sbin` | System admin commands |
| `/opt` | Third-party software |
| Absolute path | Starts with `/` - exact location |
| Relative path | Starts from current directory |

---

*Last updated: Sep 21, 2025*
