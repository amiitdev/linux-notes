# Linux from Zero to Hero

A complete beginner's guide to Linux - learning everything from the ground up.

---

## Table of Contents

1. [Linux History](#1-linux-history)
2. [Linux Distributions](#2-linux-distributions)
3. [Kernel vs OS](#3-kernel-vs-os)
4. [Linux File System](#4-linux-file-system)
5. [Absolute vs Relative Paths](#5-absolute-vs-relative-paths)
6. [Basic Commands - Navigation](#6-basic-commands---navigation)
7. [Basic Commands - Directories](#7-basic-commands---directories)
8. [Basic Commands - Files](#8-basic-commands---files)
9. [Basic Commands - Reading Files](#9-basic-commands---reading-files)
10. [Getting Help](#10-getting-help)
11. [File Permissions](#11-file-permissions)
12. [Links](#12-links)
13. [File Searching](#13-file-searching)
14. [Text Utilities](#14-text-utilities)
15. [Redirection and Pipes](#15-redirection-and-pipes)
16. [Process Management](#16-process-management)
17. [Process Control](#17-process-control)
18. [System Monitoring](#18-system-monitoring)
19. [Package Management - Debian](#19-package-management---debian)
20. [Package Management - Red Hat](#20-package-management---red-hat)
21. [User Administration](#21-user-administration)
22. [Group Management](#22-group-management)
23. [Sudo](#23-sudo)
24. [Disk Management](#24-disk-management)
25. [Filesystems and Mounting](#25-filesystems-and-mounting)
26. [LVM - Logical Volume Management](#26-lvm---logical-volume-management)

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

## 6. Basic Commands - Navigation

### pwd - Print Working Directory

Shows you WHERE you are right now.

```
$ pwd
/home/amit

$ cd /etc && pwd
/etc
```

| Flag | What it does |
|------|-------------|
| `pwd` | Shows current directory |

**Think of it as:** GPS for your terminal - always tells you your location.

---

### ls - List Directory Contents

Shows you WHAT is in a directory.

```
$ ls
AGENTS.md    Desktop    Documents    Downloads    Music
Pictures     Public     Templates    Videos       linux-notes
```

#### Common ls Flags

| Flag | What it does | Example |
|------|-------------|---------|
| `ls` | Simple list | `ls` |
| `ls -l` | Long format (permissions, size, date) | `ls -l` |
| `ls -a` | Show hidden files (starts with `.`) | `ls -a` |
| `ls -la` | Long format + hidden files | `ls -la` |
| `ls -lh` | Human readable sizes (KB, MB, GB) | `ls -lh` |
| `ls -lt` | Sort by time (newest first) | `ls -lt` |
| `ls -lS` | Sort by size (biggest first) | `ls -lS` |

#### Real Output Examples

```
$ ls -l
total 25184
-rw-rw-r--  1 amit amit  130048 Apr 26 10:36 002 - Your First HTML Website.mp4.part
-rw-rw-r--  1 amit amit    4730 Sep 12 11:37 AGENTS.md
drwxrwxr-x  5 amit amit     4096 Dec  7  2025 amit-venv
drwxrwxr-x  3 amit amit     4096 Mar 11  2026 Android
-rwxr-xr-x  1 amit amit 20441648 Aug 25 21:51 chromedriver
```

**Reading the long format:**
```
-rw-rw-r--  1  amit  amit  20441648  Aug 25 21:51  chromedriver
|__________|  |_____|_____|_________|______________|____________|
    |            |      |       |          |              |
 Permissions  Links  Owner  Group    Size          Name
```

```
$ ls -la | head -5
total 26752
drwxr-x--- 116 amit    amit    16384 Sep 21 12:04 .
drwxr-xr-x   3 root    root     4096 Dec 22  2025 ..
-rw-rw-r--   1 amit    amit   130048 Apr 26 10:36 002 - Your First HTML Website.mp4.part
-rw-rw-r--   1 amit    amit     4730 Sep 12 11:37 AGENTS.md
```

```
$ ls -lh | head -5
total 25M
-rw-rw-r--  1 amit amit 127K Apr 26 10:36 002 - Your First HTML Website.mp4.part
-rw-rw-r--  1 amit amit 4.7K Sep 12 11:37 AGENTS.md
-rw-rw-r--  1 amit amit  17K Sep 14 09:03 all_packages_backup.txt
drwxrwxr-x  5 amit amit 4.0K Dec  7  2025 amit-venv
```

```
$ ls -lt | head -5
total 25184
drwxrwxr-x  3 amit amit     4096 Sep 21 12:01 linux-notes
-rw-rw-r--  1 amit amit    18308 Sep 21 11:55 opencode.json
drwxrwxr-x  9 amit amit     4096 Sep 17 19:40 Desktop
drwxrwxr-x 11 amit amit    12288 Sep 17 16:34 Downloads
```

```
$ ls -lS | head -5
total 25184
-rwxr-xr-x  1 amit amit 20441648 Aug 25 21:51 chromedriver
-rw-rw-r--  1 amit amit  2418106 Sep 14 16:03 index.html
-rw-rw-r--  1 amit amit   490679 Jul 22 11:20 llm-deep-notes-final.png
-rw-rw-r--  1 amit amit   455174 Jul 22 11:14 llm-notes-preview.png
```

#### Permission Characters Explained

| Character | Meaning |
|-----------|---------|
| `d` | Directory |
| `-` | Regular file |
| `r` | Read permission |
| `w` | Write permission |
| `x` | Execute permission |

Example: `drwxrwxr-x` means:
- `d` = directory
- `rwx` = owner can read, write, execute
- `rwx` = group can read, write, execute
- `r-x` = others can read and execute (no write)

---

### cd - Change Directory

Moves you from one directory to another.

```
$ cd ~ && pwd        # Go to home directory
/home/amit

$ cd / && pwd        # Go to root directory
/

$ cd - && pwd        # Go to previous directory
/home/amit

$ cd ~/linux-notes && pwd   # Go to specific folder
/home/amit/linux-notes

$ cd .. && pwd       # Go up one level
/home/amit

$ cd                 # No argument = go home
/home/amit
```

| Command | What it does |
|---------|-------------|
| `cd` | Go to home directory |
| `cd ~` | Go to home directory |
| `cd /` | Go to root |
| `cd -` | Go to previous directory |
| `cd ..` | Go up one level |
| `cd ../..` | Go up two levels |
| `cd ~/dir` | Go to dir in home |

**Think of it as:** Walking between rooms in a house.

---

## 7. Basic Commands - Directories

### mkdir - Make Directory

Creates new directories (folders).

```
$ mkdir mydir && ls -la | grep mydir
drwxrwxr-x  2 amit amit  4096 Sep 21 12:09 mydir
```

#### mkdir Flags

| Flag | What it does | Example |
|------|-------------|---------|
| `mkdir dir` | Create single directory | `mkdir projects` |
| `mkdir -p a/b/c` | Create nested directories | `mkdir -p projects/web/css` |
| `mkdir dir1 dir2` | Create multiple directories | `mkdir docs images` |

#### Real Output - Nested Directories

```
$ mkdir -p a/b/c && ls -R a/
a/:
b

a/b/:
c

a/b/c/:
(empty)
```

#### Real Output - Multiple Directories

```
$ mkdir dir1 dir2 dir3 && ls -la | grep -E "dir[123]"
drwxrwxr-x  2 amit amit  4096 Sep 21 12:09 dir1
drwxrwxr-x  2 amit amit  4096 Sep 21 12:09 dir2
drwxrwxr-x  2 amit amit  4096 Sep 21 12:09 dir3
```

**Think of it as:** Creating new folders in your file manager.

---

### rmdir - Remove Directory

Deletes **empty** directories only.

```
$ mkdir empty_dir && rmdir empty_dir && echo "Success"
Success
```

#### rmdir vs rm -r

| Command | What it does |
|---------|-------------|
| `rmdir dir` | Only works on empty directories |
| `rm -r dir` | Removes directory AND everything inside |

#### Real Output - rmdir Fails on Non-Empty

```
$ mkdir nonempty && touch nonempty/file.txt && rmdir nonempty
rmdir: failed to remove 'nonempty': Directory not empty
```

#### Real Output - rm -r Force Removes

```
$ rm -rf nonempty && ls nonempty
ls: cannot access 'nonempty': No such file or directory
```

**Warning:** `rm -rf` is powerful and dangerous. It deletes without asking. Double-check before using!

---

## 8. Basic Commands - Files

### touch - Create Empty File / Update Timestamp

```
$ touch newfile.txt && ls -la newfile.txt
-rw-rw-r--  1 amit amit  0 Sep 21 12:11 newfile.txt
```

| Use case | Command |
|----------|---------|
| Create empty file | `touch file.txt` |
| Update timestamp | `touch existing_file.txt` |
| Create multiple files | `touch a.txt b.txt c.txt` |

**Think of it as:** Creating a blank page, or stamping a file with today's date.

---

### cp - Copy Files and Directories

```
$ echo "hello" > original.txt && cp original.txt copy.txt && cat copy.txt
hello
```

#### Common cp Flags

| Flag | What it does | Example |
|------|-------------|---------|
| `cp file dest` | Copy file | `cp notes.txt backup.txt` |
| `cp file dir/` | Copy to directory | `cp notes.txt backup/` |
| `cp -r dir/ dest/` | Copy directory recursively | `cp -r project/ backup/` |
| `cp -i file dest` | Ask before overwrite | `cp -i notes.txt existing.txt` |
| `cp -v file dest` | Show what's happening | `cp -v notes.txt backup/` |

#### Real Output - cp to Directory

```
$ mkdir dest && cp original.txt dest/ && ls dest/
original.txt
```

#### Real Output - cp -r (Recursive Copy)

```
$ mkdir -p source/sub && echo "file1" > source/file1.txt
$ echo "file2" > source/sub/file2.txt
$ cp -r source copied_dir && ls -R copied_dir
copied_dir:
file1.txt
sub

copied_dir/sub:
file2.txt
```

#### Real Output - cp -v (Verbose)

```
$ cp -v original.txt verbose_copy.txt
'original.txt' -> 'verbose_copy.txt'
```

**Think of it as:** Copy-paste in your file manager.

---

### mv - Move or Rename Files

```
$ echo "test" > oldname.txt && mv oldname.txt newname.txt && ls newname.txt
newname.txt
```

#### Common mv Uses

| What you want | Command |
|---------------|---------|
| Rename file | `mv oldname.txt newname.txt` |
| Move to directory | `mv file.txt directory/` |
| Move + rename | `mv file.txt directory/newname.txt` |

#### Real Output - Rename

```
$ ls oldname.txt
oldname.txt

$ mv oldname.txt newname.txt && ls oldname.txt
ls: cannot access 'oldname.txt': No such file or directory

$ ls newname.txt
newname.txt
```

#### Real Output - Move to Directory

```
$ mkdir archive && mv newname.txt archive/ && ls archive/
newname.txt

$ ls newname.txt
ls: cannot access 'newname.txt': No such file or directory
```

**Think of it as:** Cut-paste, or renaming a file in your file manager.

---

### rm - Remove Files and Directories

```
$ echo "delete me" > todelete.txt && rm todelete.txt && ls todelete.txt
ls: cannot access 'todelete.txt': No such file or directory
```

#### Common rm Flags

| Flag | What it does | Example |
|------|-------------|---------|
| `rm file` | Delete file | `rm notes.txt` |
| `rm -i file` | Ask before delete | `rm -i important.txt` |
| `rm -v file` | Show what's deleted | `rm -v oldfile.txt` |
| `rm -r dir` | Delete directory + contents | `rm -r old_project/` |
| `rm -rf dir` | Force delete (no asking) | `rm -rf old_project/` |

#### Real Output - rm -i (Interactive)

```
$ echo "careful" > careful.txt && rm -i careful.txt
rm: remove regular file 'careful.txt'?
```

#### Real Output - rm -v (Verbose)

```
$ echo "verbose delete" > verbose_del.txt && rm -v verbose_del.txt
removed 'verbose_del.txt'
```

#### Real Output - rm -r (Recursive)

```
$ mkdir -p todelete_dir/sub && echo "data" > todelete_dir/file.txt
$ echo "data2" > todelete_dir/sub/file2.txt
$ ls -R todelete_dir
todelete_dir:
file.txt
sub

todelete_dir/sub:
file2.txt

$ rm -r todelete_dir && ls todelete_dir
ls: cannot access 'todelete_dir': No such file or directory
```

**DANGER ZONE:**
| Command | Danger Level |
|---------|-------------|
| `rm file` | Safe - asks for confirmation |
| `rm -f file` | Dangerous - no confirmation |
| `rm -r dir` | Careful - deletes everything |
| `rm -rf dir` | EXTREME - deletes everything, no asking |

---

## 9. Basic Commands - Reading Files

### cat - Show Entire File

```
$ cat demo.txt
Line 1: Hello
Line 2: World
Line 3: Linux is fun
Line 4: Learning commands
Line 5: Practice makes perfect
```

#### cat Flags

| Flag | What it does | Example |
|------|-------------|---------|
| `cat file` | Show file content | `cat notes.txt` |
| `cat -n file` | Show with line numbers | `cat -n notes.txt` |
| `cat -b file` | Number non-blank lines only | `cat -b notes.txt` |
| `cat -s file` | Squeeze multiple blank lines | `cat -s notes.txt` |

#### Real Output - cat -n (Line Numbers)

```
$ cat -n demo.txt
     1  Line 1: Hello
     2  Line 2: World
     3  Line 3: Linux is fun
     4  Line 4: Learning commands
     5  Line 5: Practice makes perfect
```

#### Real Output - cat -b (Non-blank Numbers)

```
$ cat -b blank_demo.txt
     1  First

     2  Third

     3  Fifth
```

**Think of it as:** Reading a whole book at once.

---

### head - Show First Lines of File

```
$ head numbers.txt
1
2
3
4
5
6
7
8
9
10
```

#### head Flags

| Flag | What it does | Example |
|------|-------------|---------|
| `head file` | First 10 lines (default) | `head largefile.txt` |
| `head -5 file` | First 5 lines | `head -5 largefile.txt` |
| `head -20 file` | First 20 lines | `head -20 largefile.txt` |

#### Real Output

```
$ head -5 numbers.txt
1
2
3
4
5
```

**Think of it as:** Reading just the first page of a book.

---

### tail - Show Last Lines of File

```
$ tail numbers.txt
11
12
13
14
15
16
17
18
19
20
```

#### tail Flags

| Flag | What it does | Example |
|------|-------------|---------|
| `tail file` | Last 10 lines (default) | `tail largefile.txt` |
| `tail -5 file` | Last 5 lines | `tail -5 largefile.txt` |
| `tail -f file` | Follow (watch for new lines) | `tail -f /var/log/syslog` |

#### Real Output

```
$ tail -5 numbers.txt
16
17
18
19
20
```

**Think of it as:** Reading the last page of a book. `tail -f` is like watching a live news feed.

---

### less - View File Page by Page

```
$ less demo.txt
```

| Key | What it does |
|-----|-------------|
| `Space` | Next page |
| `b` | Previous page |
| `q` | Quit |
| `/text` | Search for "text" |
| `n` | Next search result |
| `N` | Previous search result |
| `g` | Go to beginning |
| `G` | Go to end |

**Think of it as:** A comfortable book reader - you can go forward, backward, search, and jump around.

---

### Quick Comparison: cat vs head vs tail vs less

| Command | Best for |
|---------|----------|
| `cat` | Small files, or when you want the whole thing |
| `head` | Peek at the beginning of a file |
| `tail` | Peek at the end of a file |
| `tail -f` | Watch a log file in real-time |
| `less` | Read large files comfortably |

---

## 10. Getting Help

Linux has built-in help systems. You'll never be stuck!

### --help - Quick Help

Most commands have a `--help` flag that shows a summary.

```
$ ls --help
Usage: ls [OPTION]... [FILE]...
List information about the FILEs (the current directory by default).
Sort entries alphabetically if none of -cftuvSUX nor --sort is specified.

  -a, --all                  do not ignore entries starting with .
  -A, --almost-all           do not list implied . and ..
  -l                         use a long listing format
  -h, --human-readable       with -l, print sizes in human readable format
  ...
```

```
$ mkdir --help
Usage: mkdir [OPTION]... DIRECTORY...
Create the DIRECTORY(ies), if they do not already exist.

  -m, --mode=MODE   set file mode (as in chmod)
  -p, --parents     no error if existing, make parent directories as needed
  -v, --verbose     print a message for each created directory
```

| When to use | Command |
|-------------|---------|
| Quick reminder of flags | `command --help` |
| See all options | `command --help` |

---

### man - Manual Pages

The `man` command shows the full manual for any command.

```
$ man ls
LS(1)                            User Commands                           LS(1)

NAME
       ls - list directory contents

SYNOPSIS
       ls [OPTION]... [FILE]...

DESCRIPTION
       List information about the FILEs (the current directory by default).

       -a, --all
              do not ignore entries starting with .

       -A, --almost-all
              do not list implied . and ..
       ...
```

#### man Navigation

| Key | What it does |
|-----|-------------|
| `Space` | Next page |
| `b` | Previous page |
| `q` | Quit |
| `/word` | Search for "word" |
| `n` | Next search result |
| `N` | Previous search result |

#### man Sections

| Section | Content |
|---------|---------|
| 1 | User commands (ls, cp, mv) |
| 2 | System calls (open, read, write) |
| 3 | Library functions (printf, malloc) |
| 4 | Special files (/dev/*) |
| 5 | File formats (/etc/passwd) |
| 6 | Games |
| 7 | Miscellaneous |
| 8 | System admin commands (mount, fdisk) |

```
$ man man
MAN(1)                        Manual pager utils                        MAN(1)

NAME
       man - an interface to the system reference manuals
```

---

### info - Detailed Documentation

`info` provides more detailed, hyperlinked documentation.

```
$ info coreutils
File: coreutils.info,  Node: Top,  Next: Introduction,  Up: (dir)

GNU Coreutils
*************

This manual documents version 9.4 of the GNU core utilities, including
the standard programs for text and file manipulation.

* Menu:
* Introduction::                 Caveats, overview, and authors
* Common options::               Common options
* Output of entire files::       cat tac nl od base32 base64
* Output of parts of files::     head tail split csummarizing files::            wc sum cksum
* Basic operations::             cp dd install mv rm shred
* Special file types::           mkdir rmdir unlink
* Working context::              pwd stty printenv tty
```

#### info Navigation

| Key | What it does |
|-----|-------------|
| `Space` | Next page |
| `b` | Previous page |
| `q` | Quit |
| `Enter` | Follow a link |
| `u` | Go up one level |

---

### Other Help Commands

| Command | What it does | Example |
|---------|-------------|---------|
| `whatis command` | One-line description | `whatis ls` |
| `type command` | Shows where command is | `type ls` |
| `which command` | Shows command path | `which ls` |

#### Real Output

```
$ whatis ls
ls (1)               - list directory contents

$ type ls
ls is /usr/bin/ls

$ which ls
/usr/bin/ls
```

---

### Help Comparison Table

| Tool | Best for | Detail level |
|------|----------|-------------|
| `--help` | Quick reminder | Low (summary) |
| `man` | Full reference | High (complete) |
| `info` | Detailed with links | Highest (tutorial) |
| `whatis` | Quick description | Very low (one line) |
| `type` | Find command location | Low |
| `which` | Find command path | Low |

**Pro tip:** Start with `--help`, use `man` when you need details, and `info` for tutorials.

---

## 11. File Permissions

Every file and directory in Linux has permissions that control who can read, write, and execute it.

### Understanding Permission String

When you run `ls -l`, you see a permission string:

```
$ ls -la perm_demo.txt
-rw-rw-r-- 1 amit amit 5 Sep 21 13:20 perm_demo.txt
```

#### Breaking Down the Permission String

```
-rw-rw-r-- 1 amit amit 5 Sep 21 13:20 perm_demo.txt
|__________| |_|____|____|
    |          |     |
 Permissions  Owner Group
```

| Position | Meaning |
|----------|---------|
| 1st char | File type (`-` = file, `d` = directory, `l` = link) |
| 2nd-4th chars | **Owner** permissions |
| 5th-7th chars | **Group** permissions |
| 8th-10th chars | **Others** permissions |

### The Three Permission Types

| Permission | Symbol | Numeric Value | What it allows |
|------------|--------|---------------|----------------|
| Read | `r` | 4 | View file contents, list directory |
| Write | `w` | 2 | Modify file, create/delete files in directory |
| Execute | `x` | 1 | Run as program, enter directory |
| No permission | `-` | 0 | Nothing |

### Real Output - Permission Anatomy

```
-rw-rw-r-- 1 amit amit 5 Sep 21 13:20 perm_demo.txt

The permission string: -rw-rw-r--
|   |   |   |
|   |   |   +-- Others: r-- (read only = 4)
|   |   +------ Group:  rw- (read+write = 6)
|   +---------- Owner:  rw- (read+write = 6)
+-------------- Type:   - (regular file)
```

---

### Three Types of Users

| User Type | Who | Notation |
|-----------|-----|----------|
| **Owner (User)** | The person who owns the file | `u` |
| **Group** | Users who share the group | `g` |
| **Others** | Everyone else | `o` |
| **All** | All three combined | `a` |

```
$ whoami
amit

$ id
uid=1000(amit) gid=1000(amit) groups=1000(amit),4(adm),24(cdrom),27(sudo)...
```

---

### chmod - Change File Permissions

#### Method 1: Symbolic Mode (letters)

| Command | What it does |
|---------|-------------|
| `chmod u+x file` | Add execute for **user** |
| `chmod g+w file` | Add write for **group** |
| `chmod o=r file` | Set others to read-only |
| `chmod a+r file` | Add read for **everyone** |
| `chmod u+rwx,g+rx,o-rwx file` | Mixed permissions |

#### Real Output - Symbolic Mode

```
$ ls -la perm_demo.txt
-rw-rw-r-- 1 amit amit 5 Sep 21 13:20 perm_demo.txt

$ chmod u+x perm_demo.txt
$ ls -la perm_demo.txt
-rwxrw-r-- 1 amit amit 5 Sep 21 13:20 perm_demo.txt

$ chmod g+w perm_demo.txt
$ ls -la perm_demo.txt
-rwxrw-rw- 1 amit amit 5 Sep 21 13:20 perm_demo.txt

$ chmod o=rwx perm_demo.txt
$ ls -la perm_demo.txt
-rwxrw-rwx 1 amit amit 5 Sep 21 13:20 perm_demo.txt

$ chmod a-x perm_demo.txt
$ ls -la perm_demo.txt
-rw-rw-rw- 1 amit amit 5 Sep 21 13:20 perm_demo.txt
```

| Symbol | Meaning |
|--------|---------|
| `u` | User (owner) |
| `g` | Group |
| `o` | Others |
| `a` | All (u+g+o) |
| `+` | Add permission |
| `-` | Remove permission |
| `=` | Set exact permission |

---

#### Method 2: Numeric Mode (Octal)

Each permission has a number:

| Permission | Number |
|------------|--------|
| `r` (read) | 4 |
| `w` (write) | 2 |
| `x` (execute) | 1 |
| `-` (nothing) | 0 |

**How to calculate:** Add the numbers for each user type.

| Permission String | Owner | Group | Others | Numeric |
|-------------------|-------|-------|--------|---------|
| `rwxr-xr-x` | rwx (7) | r-x (5) | r-x (5) | **755** |
| `rw-r--r--` | rw- (6) | r-- (4) | r-- (4) | **644** |
| `rw-------` | rw- (6) | --- (0) | --- (0) | **600** |
| `rwxrwxrwx` | rwx (7) | rwx (7) | rwx (7) | **777** |
| `r--r--r--` | r-- (4) | r-- (4) | r-- (4) | **444** |
| `rwx------` | rwx (7) | --- (0) | --- (0) | **700** |

#### Real Output - Numeric Mode

```
$ chmod 755 perm_demo.txt
$ ls -la perm_demo.txt
-rwxr-xr-x 1 amit amit 5 Sep 21 13:20 perm_demo.txt
Owner: rwx (7) | Group: r-x (5) | Others: r-x (5)

$ chmod 644 perm_demo.txt
$ ls -la perm_demo.txt
-rw-r--r-- 1 amit amit 5 Sep 21 13:20 perm_demo.txt
Owner: rw- (6) | Group: r-- (4) | Others: r-- (4)

$ chmod 600 perm_demo.txt
$ ls -la perm_demo.txt
-rw------- 1 amit amit 5 Sep 21 13:20 perm_demo.txt
Owner: rw- (6) | Group: --- (0) | Others: --- (0)

$ chmod 777 perm_demo.txt
$ ls -la perm_demo.txt
-rwxrwxrwx 1 amit amit 5 Sep 21 13:20 perm_demo.txt
Owner: rwx (7) | Group: rwx (7) | Others: rwx (7)

$ chmod 444 perm_demo.txt
$ ls -la perm_demo.txt
-r--r--r-- 1 amit amit 5 Sep 21 13:20 perm_demo.txt
Owner: r-- (4) | Group: r-- (4) | Others: r-- (4)
```

---

#### Common Permission Sets

| Number | Permission | Use Case |
|--------|------------|----------|
| `755` | `rwxr-xr-x` | Scripts, executables, directories |
| `644` | `rw-r--r--` | Web pages, config files |
| `600` | `rw-------` | Private files, SSH keys, passwords |
| `700` | `rwx------` | Private directories |
| `444` | `r--r--r--` | Read-only files |
| `777` | `rwxrwxrwx` | **NEVER USE THIS!** |

---

#### Recursive chmod (-R)

Apply permissions to directory and all contents inside:

```
$ mkdir -p perm_dir/sub && echo "data" > perm_dir/file.txt

$ ls -laR perm_dir/
perm_dir/:
-rw-rw-r--  1 amit amit  5 Sep 21 13:20 file.txt

$ chmod -R 755 perm_dir/

$ ls -laR perm_dir/
perm_dir/:
-rwxr-xr-x  1 amit amit  5 Sep 21 13:20 file.txt
```

---

### chown - Change File Owner

**Requires sudo** (only root can change ownership to another user)

#### Syntax

```
chown user:group file        # Change both
chown user file              # Change owner only
chown :group file            # Change group only
chown -R user:group dir/     # Recursive
```

#### Real Output

```
$ ls -la ownership_demo.txt
-rw-rw-r-- 1 amit amit 5 Sep 21 13:19 ownership_demo.txt

# Change both owner and group (requires sudo)
$ sudo chown root:root ownership_demo.txt
$ ls -la ownership_demo.txt
-rw-rw-r-- 1 root root 5 Sep 21 13:19 ownership_demo.txt

# Change back to amit
$ sudo chown amit:amit ownership_demo.txt
$ ls -la ownership_demo.txt
-rw-rw-r-- 1 amit amit 5 Sep 21 13:19 ownership_demo.txt
```

---

### chgrp - Change Group

**No sudo needed** if you're a member of the group.

#### Syntax

```
chgrp group file             # Change group
chgrp -R group dir/          # Recursive
```

#### Real Output

```
$ ls -la chgrp_test.txt
-rw-rw-r-- 1 amit amit 5 Sep 21 13:21 chgrp_test.txt

$ chgrp adm chgrp_test.txt
$ ls -la chgrp_test.txt
-rw-rw-r-- 1 amit adm 5 Sep 21 13:21 chgrp_test.txt

$ chgrp amit chgrp_test.txt
$ ls -la chgrp_test.txt
-rw-rw-r-- 1 amit amit 5 Sep 21 13:21 chgrp_test.txt
```

#### Check Your Groups

```
$ groups amit
amit : amit adm cdrom sudo dip plugdev users kvm lpadmin sambashare docker ollama libvirt
```

---

### chmod vs chown vs chgrp

| Command | What it changes | Needs sudo? |
|---------|----------------|-------------|
| `chmod` | Permissions (read/write/execute) | No |
| `chown` | Owner (and optionally group) | Yes (to change to another user) |
| `chgrp` | Group only | No (if you're in the group) |

---

### File Type Indicators

| Character | Meaning |
|-----------|---------|
| `-` | Regular file |
| `d` | Directory |
| `l` | Symbolic link |
| `c` | Character device |
| `b` | Block device |
| `p` | Named pipe (FIFO) |
| `s` | Socket |

---

### Special Permissions (Advanced)

| Permission | Number | What it does | Example |
|------------|--------|--------------|---------|
| SetUID (s) | 4000 | Run as file **owner** | `/usr/bin/passwd` |
| SetGID (s) | 2000 | Run with file **group** | Shared directories |
| Sticky bit (t) | 1000 | Only owner can delete | `/tmp` |

```
$ ls -ld /tmp
drwxrwxrwt 34 root root 28672 Sep 21 13:20 /tmp
                                              ^
                                         Sticky bit (t)
```

---

### Permission Examples by Use Case

| Use Case | Recommended Permission | Command |
|----------|----------------------|---------|
| Shell script | `755` | `chmod 755 script.sh` |
| Web page | `644` | `chmod 644 index.html` |
| SSH private key | `600` | `chmod 600 ~/.ssh/id_rsa` |
| Password file | `600` | `chmod 600 .env` |
| Shared directory | `775` | `chmod 775 shared/` |
| Public directory | `755` | `chmod 755 public/` |
| Config file | `644` | `chmod 644 config.json` |
| Log file | `640` | `chmod 640 /var/log/app.log` |

---

### Permission Cheat Sheet

```
Number  Binary  Permission
------  ------  ----------
  0     000     --- (nothing)
  1     001     --x (execute)
  2     010     -w- (write)
  3     011     -wx (write+execute)
  4     100     r-- (read)
  5     101     r-x (read+execute)
  6     110     rw- (read+write)
  7     111     rwx (full)

Common combos:
  755 = rwxr-xr-x  (executables, directories)
  644 = rw-r--r--  (regular files)
  600 = rw-------  (private/sensitive)
  700 = rwx------  (private directories)
```

---

## 12. Links

Links let you access the same file from multiple locations.

### Hard Link

A hard link is **another name for the same file**. Both names point to the same data on disk.

```
$ echo "Hello World" > original.txt && ln original.txt hardlink.txt

$ ls -li original.txt hardlink.txt
6029788 -rw-rw-r-- 2 amit amit 12 Sep 21 13:35 hardlink.txt
6029788 -rw-rw-r-- 2 amit amit 12 Sep 21 13:35 original.txt
```

**Notice:** Same inode number (6029788) = same file on disk.

| Feature | Hard Link |
|---------|-----------|
| Command | `ln file link` |
| Inode | Same as original |
| Edit one, other changes | Yes |
| Delete original, link works | Yes |
| Can link to directories | No |
| Can link across partitions | No |

#### Real Output - Edit Hard Link

```
$ echo "Hello Modified" > hardlink.txt && cat original.txt
Hello Modified
```

#### Real Output - Delete Original, Hard Link Survives

```
$ rm original.txt && cat hardlink.txt
Hello Modified
```

---

### Soft Link (Symbolic Link)

A soft link is a **shortcut** that points to another file by path.

```
$ echo "Original Data" > original.txt && ln -s original.txt softlink.txt

$ ls -la original.txt softlink.txt
-rw-rw-r-- 1 amit amit 14 Sep 21 13:35 original.txt
lrwxrwxrwx 1 amit amit 12 Sep 21 13:35 softlink.txt -> original.txt
```

**Notice:** `l` at the start = link. Shows `-> original.txt` (points to original).

| Feature | Soft Link |
|---------|-----------|
| Command | `ln -s file link` |
| Inode | Different from original |
| Edit one, other changes | Yes |
| Delete original, link breaks | Yes (becomes broken) |
| Can link to directories | Yes |
| Can link across partitions | Yes |

#### Real Output - Read Soft Link

```
$ cat softlink.txt
Original Data
```

#### Real Output - Delete Original, Soft Link Breaks

```
$ rm original.txt && cat softlink.txt
cat: softlink.txt: No such file or directory
```

---

### Hard Link vs Soft Link

| Feature | Hard Link | Soft Link |
|---------|-----------|-----------|
| Command | `ln file link` | `ln -s file link` |
| Inode | Same | Different |
| Shows in `ls -l` | Normal file | Shows `->` pointer |
| Delete original | Link still works | Link breaks |
| Link to directory | Not allowed | Allowed |
| Cross partition | Not allowed | Allowed |

---

### When to Use Which?

| Use Case | Use |
|----------|-----|
| Backup important file | Hard link |
| Shortcut to file | Soft link |
| Link to directory | Soft link |
| Link across drives | Soft link |
| Shorten long path | Soft link |

---

### System Links You'll See

```
$ ls -la /usr/bin/python3
lrwxrwxrwx 1 root root 9 Mar 21  2024 /usr/bin/python3 -> python3.12
```

This is a soft link - `/usr/bin/python3` points to `/usr/bin/python3.12`.

---

## 13. File Searching

### find - Search by Criteria

The most powerful search tool. Searches in real-time.

```
$ find search_demo -name 'file.txt'
search_demo/sub1/sub2/file.txt
search_demo/sub1/file.txt
search_demo/file.txt
```

#### Common find Options

| Option | What it does | Example |
|--------|-------------|---------|
| `-name` | Search by name | `find . -name "*.txt"` |
| `-type f` | Files only | `find . -type f` |
| `-type d` | Directories only | `find . -type d` |
| `-size` | By size | `find . -size +1M` |
| `-mtime` | Modified time | `find . -mtime -7` |
| `-exec` | Run command on results | `find . -name "*.txt" -exec echo {} \;` |

#### Real Output - Search by Name

```
$ find search_demo -name '*.txt'
search_demo/sub1/sub2/file.txt
search_demo/sub1/file.txt
search_demo/file.txt
search_demo/notes.txt
```

#### Real Output - Files Only

```
$ find search_demo -type f
search_demo/sub1/sub2/file.txt
search_demo/sub1/file.txt
search_demo/file.txt
search_demo/notes.txt
```

#### Real Output - Directories Only

```
$ find search_demo -type d
search_demo
search_demo/sub1
search_demo/sub1/sub2
```

#### Real Output - Execute Command on Results

```
$ find search_demo -name '*.txt' -exec echo "Found: {}" \;
Found: search_demo/bigfile.txt
Found: search_demo/sub1/sub2/file.txt
Found: search_demo/sub1/file.txt
Found: search_demo/file.txt
Found: search_demo/notes.txt
```

---

### locate - Fast Search from Database

Searches from a pre-built database. Much faster than `find`.

```
$ locate passwd
/etc/passwd
/etc/passwd-
/etc/pam.d/chpasswd
/etc/pam.d/passwd
/etc/security/opasswd
```

| Feature | find | locate |
|---------|------|--------|
| Speed | Slow (real-time) | Fast (database) |
| Freshness | Always current | May be outdated |
| Flexibility | Very flexible | Limited options |
| Update | Not needed | `sudo updatedb` |

**Tip:** Run `sudo updatedb` to update the locate database.

---

### which - Find Command Location

Shows where a command is located.

```
$ which ls
/usr/bin/ls

$ which python3
/usr/bin/python3

$ which git
/usr/bin/git

$ which node
/home/amit/.nvm/versions/node/v24.19.0/bin/node
```

**Use when:** You want to know which version of a command you're running.

---

### whereis - Find Binary, Source, Manual

Shows binary, source, and manual page locations.

```
$ whereis ls
ls: /usr/bin/ls /usr/share/man/man1/ls.1.gz

$ whereis python3
python3: /usr/bin/python3 /usr/lib/python3 /etc/python3 /usr/share/python3

$ whereis gcc
gcc: /usr/bin/gcc /usr/lib/gcc /usr/libexec/gcc /usr/share/gcc

$ whereis git
git: /usr/bin/git /usr/share/man/man1/git.1.gz
```

| Output Part | Meaning |
|-------------|---------|
| First | Binary location |
| Second | Source files |
| Third | Manual pages |

---

### Search Tools Comparison

| Tool | Best for | Speed | Usage |
|------|----------|-------|-------|
| `find` | Complex searches | Slow | `find . -name "*.txt"` |
| `locate` | Quick filename search | Fast | `locate filename` |
| `which` | Find command path | Instant | `which command` |
| `whereis` | Find all related files | Instant | `whereis command` |

| When to use | Command |
|-------------|---------|
| Find all `.py` files modified today | `find . -name "*.py" -mtime -1` |
| Quick find a file by name | `locate filename` |
| Where is `python3` installed? | `which python3` |
| Find binary + man page for `gcc` | `whereis gcc` |

---

## 14. Text Utilities

Linux has powerful tools for processing text. You can combine them with pipes (`|`) to build complex commands.

### grep - Search Text

Search for patterns in files or output.

```
$ grep 'apple' sample.txt
apple
apple pie
```

#### Common grep Flags

| Flag | What it does | Example |
|------|-------------|---------|
| `-i` | Case insensitive | `grep -i 'apple' file` |
| `-n` | Show line numbers | `grep -n 'banana' file` |
| `-c` | Count matches | `grep -c 'cherry' file` |
| `-v` | Invert (show non-matching) | `grep -v 'apple' file` |
| `-r` | Search recursively | `grep -r 'error' /var/log/` |
| `-w` | Whole word match | `grep -w 'apple' file` |

#### Real Output

```
$ grep -i 'apple' sample.txt
apple
apple pie
 APPLE

$ grep -n 'banana' sample.txt
2:banana
5:banana split

$ grep -c 'cherry' sample.txt
2

$ grep -v 'apple' sample.txt
banana
cherry
banana split
cherry tart
 APPLE
Banana
CHERRY
```

#### Regex Patterns

| Pattern | Meaning | Example |
|---------|---------|---------|
| `^word` | Starts with | `grep '^a' file` |
| `word$` | Ends with | `grep 'e$' file` |
| `.` | Any character | `grep 'a.ple' file` |
| `[abc]` | Character set | `grep '[ab]' file` |
| `[0-9]` | Number range | `grep '[0-9]' file` |

```
$ grep '^a' sample.txt
apple
apple pie

$ grep 'e$' sample.txt
apple
apple pie
```

---

### sed - Stream Editor

Find and replace text. Edit files without opening them.

```
$ sed 's/apple/orange/' sample.txt
orange
banana
cherry
orange pie
```

#### Common sed Operations

| Operation | What it does | Example |
|-----------|-------------|---------|
| `s/old/new/` | Replace first occurrence | `sed 's/apple/orange/' file` |
| `s/old/new/g` | Replace ALL occurrences | `sed 's/apple/orange/g' file` |
| `-i` | Edit file in-place | `sed -i 's/old/new/g' file` |
| `2,4p` | Print lines 2-4 | `sed -n '2,4p' file` |
| `3d` | Delete line 3 | `sed '3d' file` |
| `/^$/d` | Delete blank lines | `sed '/^$/d' file` |

#### Real Output

```
$ sed 's/apple/orange/' sample.txt
orange
banana
cherry
orange pie
banana split
cherry tart

$ sed -n '2,4p' sample.txt
banana
cherry
apple pie

$ sed '3d' sample.txt
apple
banana
apple pie
banana split
cherry tart
```

#### sed with -i (Edit File In-Place)

```
$ cp sample.txt sed_test.txt

$ sed -i 's/banana/grape/g' sed_test.txt

$ cat sed_test.txt
apple
grape
cherry
apple pie
grape split
cherry tart
```

**Warning:** `-i` modifies the original file. Make a backup first!

---

### awk - Pattern Scanning

More powerful than sed. Great for columns and data processing.

```
$ awk '{print $1}' data.txt
John
Sarah
Mike
Lisa
```

#### awk Basics

| Syntax | What it does |
|--------|-------------|
| `{print $1}` | Print first column |
| `{print $1, $3}` | Print columns 1 and 3 |
| `$2 > 28` | Filter rows where column 2 > 28 |
| `{print NR, $0}` | Print with line numbers |
| `-F:` | Set delimiter (default is space) |
| `{sum+=$2} END {print sum}` | Calculate sum |

#### Real Output

```
$ cat data.txt
John 25 Engineer
Sarah 30 Designer
Mike 28 Developer
Lisa 35 Manager

$ awk '{print $1}' data.txt
John
Sarah
Mike
Lisa

$ awk '{print $1, $3}' data.txt
John Engineer
Sarah Designer
Mike Developer
Lisa Manager

$ awk '$2 > 28' data.txt
Sarah 30 Designer
Lisa 35 Manager

$ awk '{sum+=$2} END {print "Total age:", sum}' data.txt
Total age: 118
```

#### awk with Custom Delimiter

```
$ awk -F: '{print $1}' /etc/passwd | head -5
root
daemon
bin
sys
sync
```

---

### sort - Sort Lines

```
$ sort fruits.txt
apple
apple
banana
banana
cherry
cherry
```

#### Common sort Options

| Option | What it does | Example |
|--------|-------------|---------|
| (none) | Alphabetical sort | `sort file` |
| `-r` | Reverse order | `sort -r file` |
| `-n` | Numeric sort | `sort -n file` |
| `-u` | Sort + remove duplicates | `sort -u file` |
| `-k2` | Sort by column 2 | `sort -k2 file` |
| `-t','` | Set delimiter | `sort -t',' -k2 file` |

#### Real Output

```
$ sort -r fruits.txt
cherry
cherry
cherry
banana
banana
apple
apple

$ sort -n
10
2
1
20
3

$ sort -k2 -n
John 25
Mike 28
Sarah 30
Lisa 35
```

---

### uniq - Remove Duplicates

**Important:** `uniq` only removes ADJACENT duplicates. Always `sort` first!

```
$ sort fruits.txt | uniq
apple
banana
cherry
```

#### Common uniq Options

| Option | What it does | Example |
|--------|-------------|---------|
| (none) | Remove duplicates | `sort file \| uniq` |
| `-c` | Count duplicates | `sort file \| uniq -c` |
| `-d` | Show only duplicates | `sort file \| uniq -d` |
| `-u` | Show only unique lines | `sort file \| uniq -u` |

#### Real Output

```
$ sort fruits.txt | uniq -c
      2 apple
      2 banana
      3 cherry

$ sort fruits.txt | uniq -d
apple
banana
cherry

$ sort fruits.txt | uniq -u
(no output - all items have duplicates)
```

---

### cut - Extract Columns

Extract specific columns or characters from text.

```
$ cut -d',' -f1 employees.csv
John
Sarah
Mike
Lisa
```

#### Common cut Options

| Option | What it does | Example |
|--------|-------------|---------|
| `-d','` | Set delimiter | `cut -d',' -f1 file` |
| `-f1` | Column 1 | `cut -f1 file` |
| `-f1,3` | Columns 1 and 3 | `cut -f1,3 file` |
| `-f2-` | Column 2 to end | `cut -f2- file` |
| `-c1-5` | Characters 1-5 | `cut -c1-5 file` |

#### Real Output

```
$ cat employees.csv
John,25,Engineer,New York
Sarah,30,Designer,San Francisco
Mike,28,Developer,Chicago
Lisa,35,Manager,Boston

$ cut -d',' -f1 employees.csv
John
Sarah
Mike
Lisa

$ cut -d',' -f1,3 employees.csv
John,Engineer
Sarah,Designer
Mike,Developer
Lisa,Manager

$ cut -c1-5 employees.csv
John,
Sarah
Mike,
Lisa,
```

---

### tr - Translate Characters

Replace, delete, or squeeze characters.

```
$ echo 'hello world' | tr 'a-z' 'A-Z'
HELLO WORLD
```

#### Common tr Operations

| Operation | What it does | Example |
|-----------|-------------|---------|
| `'a-z' 'A-Z'` | Lowercase to uppercase | `echo 'hello' \| tr 'a-z' 'A-Z'` |
| `'l' 'r'` | Replace character | `echo 'hello' \| tr 'l' 'r'` |
| `-d 'l'` | Delete character | `echo 'hello' \| tr -d 'l'` |
| `-d ' '` | Remove spaces | `echo 'hello world' \| tr -d ' '` |
| `-s 'a-z'` | Squeeze repeated chars | `echo 'heeeellllo' \| tr -s 'a-z'` |
| `':' '\n'` | Replace with newline | `echo 'a:b:c' \| tr ':' '\n'` |

#### Real Output

```
$ echo 'hello world' | tr 'a-z' 'A-Z'
HELLO WORLD

$ echo 'hello' | tr 'l' 'r'
herro

$ echo 'hello' | tr -d 'l'
heo

$ echo 'hello world' | tr -d ' '
helloworld

$ echo 'heeeellllooo' | tr -s 'a-z'
helo

$ echo 'a:b:c:d' | tr ':' '\n'
a
b
c
d
```

---

### wc - Word Count

Count lines, words, and characters.

```
$ wc sample.txt
 9 12 76 sample.txt
```

#### Common wc Options

| Option | What it does | Example |
|--------|-------------|---------|
| `-l` | Count lines | `wc -l file` |
| `-w` | Count words | `wc -w file` |
| `-c` | Count bytes | `wc -c file` |

#### Real Output

```
$ wc -l sample.txt
9 sample.txt

$ wc -w sample.txt
12 sample.txt

$ wc sample.txt
 9 12 76 sample.txt
 (lines) (words) (bytes)
```

---

### Text Utilities Cheat Sheet

| Command | Purpose | Example |
|---------|---------|---------|
| `grep` | Search text | `grep 'error' logfile.txt` |
| `sed` | Find & replace | `sed 's/old/new/g' file` |
| `awk` | Column processing | `awk '{print $1}' file` |
| `sort` | Sort lines | `sort file` |
| `uniq` | Remove duplicates | `sort file \| uniq` |
| `cut` | Extract columns | `cut -d',' -f1 file` |
| `tr` | Translate characters | `echo 'hi' \| tr 'a-z' 'A-Z'` |
| `wc` | Count lines/words | `wc -l file` |

### Common Pipe Combinations

| What you want | Command |
|---------------|---------|
| Count unique words | `cat file \| tr ' ' '\n' \| sort \| uniq -c \| sort -rn` |
| Find top 5 lines | `sort file \| uniq -c \| sort -rn \| head -5` |
| Remove blank lines | `sed '/^$/d' file` |
| Convert to uppercase | `cat file \| tr 'a-z' 'A-Z'` |
| Extract 2nd column | `awk '{print $2}' file` |
| Count lines matching | `grep -c 'pattern' file` |

---

## 15. Redirection and Pipes

Control where command output goes and how commands connect.

### `>` - Output Redirect (Overwrite)

Send output to a file. **Overwrites** existing content.

```
$ echo 'hello' > file.txt
$ cat file.txt
hello

$ echo 'world' > file.txt
$ cat file.txt
world
```

#### Real Output

```
$ echo 'hello' > output_demo.txt
$ cat output_demo.txt
hello

$ echo 'world' > output_demo.txt
$ cat output_demo.txt
world
```

#### Other Uses

| Command | What it does |
|---------|-------------|
| `ls > file.txt` | Save directory listing to file |
| `echo 'text' > file.txt` | Write text to file |
| `command > /dev/null` | Discard output (throw it away) |

```
$ echo 'this goes nowhere' > /dev/null
$ echo "(output sent to /dev/null - it's gone)"
```

**Think of it as:** Overwriting a file with new content.

---

### `>>` - Output Redirect (Append)

Send output to a file. **Adds to the end** without overwriting.

```
$ echo 'line1' > file.txt
$ cat file.txt
line1

$ echo 'line2' >> file.txt
$ cat file.txt
line1
line2

$ echo 'line3' >> file.txt
$ cat file.txt
line1
line2
line3
```

#### Real Output

```
$ echo 'line1' > append_demo.txt
$ echo 'line2' >> append_demo.txt
$ echo 'line3' >> append_demo.txt
$ cat append_demo.txt
line1
line2
line3
```

| Symbol | What it does |
|--------|-------------|
| `>` | Overwrite file |
| `>>` | Append to file |

**Think of it as:** Adding to the end of a document.

---

### `<` - Input Redirect

Feed a file as input to a command.

```
$ wc -l < file.txt
3

$ sort < file.txt
line1
line2
line3

$ tr 'a-z' 'A-Z' < file.txt
LINE1
LINE2
LINE3
```

#### Real Output

```
$ wc -l < append_demo.txt
3

$ sort < append_demo.txt
line1
line2
line3

$ tr 'a-z' 'A-Z' < append_demo.txt
LINE1
LINE2
LINE3
```

**Think of it as:** Feeding a document into a machine for processing.

---

### `|` - Pipe

Send output of one command as input to the next command.

```
$ echo 'hello world' | tr 'a-z' 'A-Z'
HELLO WORLD

$ ls / | head -5
bin
boot
cdrom
Desktop
dev
```

#### Real Output

```
$ echo 'hello world' | tr 'a-z' 'A-Z'
HELLO WORLD

$ ls / | head -5
bin
bin.usr-is-merged
boot
cdrom
Desktop
```

#### Multi-Pipe Chains

```
$ echo -e "apple\nbanana\ncherry\napple\nbanana\ncherry\ncherry" | sort | uniq -c | sort -rn
      3 cherry
      2 banana
      2 apple
```

#### Useful Pipe Combinations

| What you want | Command |
|---------------|---------|
| Count lines | `cat file \| wc -l` |
| Search + count | `grep 'error' file \| wc -l` |
| Sort + unique | `sort file \| uniq` |
| Count duplicates | `sort file \| uniq -c \| sort -rn` |
| Find specific user | `cat /etc/passwd \| grep amit \| cut -d: -f1,6` |

```
$ cat /etc/passwd | grep amit | cut -d: -f1,6
amit:/home/amit
```

**Think of it as:** Connecting machines in an assembly line.

---

### `tee` - Split Output

Show output on screen AND save to file at the same time.

```
$ ls / | tee tee_demo.txt
bin
boot
cdrom
Desktop
...

$ cat tee_demo.txt
bin
boot
cdrom
Desktop
...
```

#### Real Output

```
$ ls / | tee tee_demo.txt
bin
bin.usr-is-merged
boot
cdrom
Desktop
...

$ cat tee_demo.txt
bin
bin.usr-is-merged
boot
cdrom
Desktop
...
```

#### tee -a (Append)

```
$ ls /home | tee -a tee_demo.txt
amit

$ cat tee_demo.txt
bin
boot
...
amit
```

#### Piping with Tee

```
$ echo -e "a\nb\nc\nd" | tee before_sort.txt | sort | tee after_sort.txt
a
b
c
d

$ cat before_sort.txt
a
b
c
d

$ cat after_sort.txt
a
b
c
d
```

| Command | What it does |
|---------|-------------|
| `command \| tee file` | Show AND save (overwrite) |
| `command \| tee -a file` | Show AND save (append) |
| `command \| tee file1 \| tee file2` | Save to multiple files |

**Think of it as:** A splitter that sends output to two places.

---

### Redirection Cheat Sheet

| Symbol | Name | What it does |
|--------|------|-------------|
| `>` | Output redirect | Overwrite file |
| `>>` | Output append | Add to end of file |
| `<` | Input redirect | Feed file as input |
| `\|` | Pipe | Connect commands |
| `2>` | Error redirect | Save error messages |
| `&>` | All redirect | Save output + errors |
| `/dev/null` | Black hole | Discard everything |

#### Real Output - Error Redirection

```
$ ls /nonexistent 2> errors.txt
$ cat errors.txt
ls: cannot access '/nonexistent': No such file or directory
```

---

### How Pipes Work

```
Command 1  |  Command 2  |  Command 3
    |              |              |
    v              v              v
  Output  --->  Input  --->   Output  --->  Final Result
```

```
$ cat /etc/passwd | grep amit | cut -d: -f1,6
    |               |              |
    v               v              v
  Read file    Find "amit"    Extract columns
```

---

## 16. Process Management

A **process** is any program currently running. Each process has a unique **PID** (Process ID).

### ps - Process Status

Shows a snapshot of running processes.

#### Common ps Options

| Command | What it does |
|---------|-------------|
| `ps` | Current terminal processes |
| `ps aux` | ALL processes (all users) |
| `ps -ef` | Full listing (all processes) |
| `ps aux \| grep name` | Find specific process |
| `ps aux --sort=-%cpu` | Sort by CPU usage |
| `ps aux --sort=-%mem` | Sort by memory usage |

#### Understanding ps aux Output

```
$ ps aux | head -5
USER    PID  %CPU %MEM    VSZ   RSS TTY   STAT START  TIME COMMAND
root      1  0.9  0.1  23292 12980 ?     Ss   15:03  0:01 /sbin/init
root      2  0.0  0.0      0     0 ?     S    15:03  0:00 [kthreadd]
```

| Column | Meaning |
|--------|---------|
| `USER` | Who owns the process |
| `PID` | Process ID (unique number) |
| `%CPU` | CPU usage percentage |
| `%MEM` | Memory usage percentage |
| `VSZ` | Virtual memory size |
| `RSS` | Resident memory (actual RAM used) |
| `STAT` | Process state |
| `COMMAND` | Command that started it |

#### Common Process States (STAT)

| State | Meaning |
|-------|---------|
| `R` | Running |
| `S` | Sleeping (waiting) |
| `D` | Uninterruptible sleep (disk I/O) |
| `Z` | Zombie (finished but not cleaned up) |
| `T` | Stopped |

#### Real Output

```
$ ps aux | wc -l
399

$ ps aux | grep nginx
root    1961  0.0  0.0  22232  1408 ?  Ss  15:04  0:00 nginx: master process
www-data 1962  0.0  0.0  23984  3456 ?  S   15:04  0:00 nginx: worker process
www-data 1963  0.0  0.0  23984  3456 ?  S   15:04  0:00 nginx: worker process

$ ps aux --sort=-%cpu | head -5
USER    PID  %CPU %MEM    VSZ   RSS TTY   STAT START  TIME COMMAND
amit    5526 86.6 11.0 75505364 820760 pts/0 Rl+ 15:05 1:43 opencode
amit    5773 57.0 14.7 4850596 1102488 ? Sl  15:05 1:02 firefox-bin

$ ps aux --sort=-%mem | head -5
USER    PID  %CPU %MEM    VSZ   RSS TTY   STAT START  TIME COMMAND
amit    5773 57.0 14.7 4850596 1102488 ? Sl  15:05 1:02 firefox-bin
amit    5526 86.6 11.0 75505620 823832 pts/0 Rl+ 15:05 1:43 opencode
```

---

### top - Interactive Process Viewer

Real-time view of processes. Updates automatically.

```
$ top
top - 15:07:16 up 3 min, 1 user, load average: 5.02, 2.57, 1.01
Tasks: 398 total, 3 running, 395 sleeping, 0 stopped, 0 zombie
%Cpu(s): 41.3 us, 7.7 sy, 0.0 ni, 50.3 id, 0.7 wa
MiB Mem: 7284.4 total, 362.7 free, 5031.6 used, 2199.9 buff/cache

    PID USER   PR NI  VIRT  RES  SHR S %CPU %MEM TIME+ COMMAND
   5526 amit  20  0  72.0g 805468 44928 R 158.3 10.8 1:46.04 opencode
   4535 amit  20  0 1448.5g 259556 103040 R 83.3 3.5 2:20.00 chrome
   3987 amit  20  0  53.2g  94324  80492 S 50.0 1.3 1:15.84 chrome
```

#### top Header Explained

| Line | Meaning |
|------|---------|
| `load average` | System load (1, 5, 15 minutes) |
| `Tasks` | Total/running/sleeping processes |
| `%Cpu(s)` | CPU usage breakdown |
| `MiB Mem` | Memory usage |

#### top Keys

| Key | What it does |
|-----|-------------|
| `q` | Quit |
| `M` | Sort by memory |
| `P` | Sort by CPU |
| `1` | Show all CPU cores |
| `k` | Kill a process |
| `h` | Help |

#### top Batch Mode (for scripts)

```
$ top -bn1 | head -10
top - 15:07:16 up 3 min, 1 user, load average: 5.02, 2.57, 1.01
Tasks: 397 total, 5 running, 392 sleeping, 0 stopped, 0 zombie
...
```

---

### htop - Better Process Viewer

Like `top` but with colors, mouse support, and easier navigation.

```
$ htop
```

#### htop Features

| Feature | Description |
|---------|-------------|
| Color-coded | Easy to read |
| Mouse support | Click to interact |
| Tree view | Press F5 to see parent/child |
| Kill process | Select and press F9 |
| Sort | Click column headers |
| Scroll | Use arrow keys |

#### htop Keys

| Key | What it does |
|-----|-------------|
| `F1` or `?` | Help |
| `F3` | Search |
| `F4` | Filter |
| `F5` | Tree view |
| `F6` | Sort by |
| `F9` | Kill process |
| `F10` | Quit |

#### htop vs top

| Feature | top | htop |
|---------|-----|------|
| Colors | No | Yes |
| Mouse | No | Yes |
| Tree view | No | Yes (F5) |
| Scroll | Limited | Full |
| Ease of use | Basic | Easy |

---

### pgrep - Find Process by Name

Returns the **PID** of processes matching a name.

```
$ pgrep bash
7158
7160

$ pgrep -a bash
7158 zsh
7160 zsh
```

#### Common pgrep Options

| Option | What it does | Example |
|--------|-------------|---------|
| `pgrep name` | Get PID(s) | `pgrep nginx` |
| `pgrep -a name` | With full command | `pgrep -a python` |
| `pgrep -l name` | With process name | `pgrep -l ssh` |
| `pgrep -u user` | By user | `pgrep -u amit` |
| `pgrep -c name` | Count matches | `pgrep -c chrome` |
| `pgrep -f pattern` | Match full command line | `pgrep -f "my script"` |

#### Real Output

```
$ pgrep -u amit | head -5
1336
1345
1380
1492
1493

$ pgrep -c bash
0

$ pgrep -f chrome
3945
3960
3961
3963
```

---

### Process Management Cheat Sheet

| Command | Purpose | Best for |
|---------|---------|----------|
| `ps aux` | Snapshot of all processes | Checking at a moment |
| `top` | Real-time process viewer | Quick monitoring |
| `htop` | Better real-time viewer | Easy monitoring |
| `pgrep name` | Find PID by name | Scripting, killing |

### Common Workflows

| What you want | Command |
|---------------|---------|
| Find nginx PID | `pgrep nginx` or `ps aux \| grep nginx` |
| See what's using CPU | `top` then press `P` |
| See what's using RAM | `top` then press `M` |
| Count all processes | `ps aux \| wc -l` |
| Kill process by name | `pkill nginx` |
| Find PID then kill | `kill $(pgrep nginx)` |

---

## 17. Process Control

### kill - Send Signal to Process

Sends a signal to a process to stop or control it.

```
$ kill PID
$ kill -9 PID
```

#### Real Output

```
$ sleep 300 & TEST_PID=$!
$ ps -p $TEST_PID -o pid,comm,stat
    PID COMMAND         STAT
   8002 sleep           SN

$ kill $TEST_PID
$ ps -p $TEST_PID
Process 8002 is gone
```

#### Common Kill Signals

| Signal | Number | Command | What it does |
|--------|--------|---------|-------------|
| SIGTERM | 15 | `kill PID` | Graceful shutdown (default) |
| SIGKILL | 9 | `kill -9 PID` | Force kill (cannot be blocked) |
| SIGHUP | 1 | `kill -HUP PID` | Reload configuration |
| SIGINT | 2 | `Ctrl+C` | Interrupt |
| SIGSTOP | 19 | `Ctrl+Z` | Pause process |

```
kill PID          # Send SIGTERM (15) - graceful
kill -9 PID       # Send SIGKILL (force) - last resort
kill -HUP PID     # Send SIGHUP - reload config
kill -l           # List all signals
```

**When to use:**
- First try: `kill PID` (graceful)
- If stuck: `kill -9 PID` (force)

---

### pkill - Kill Process by Name

Kills processes matching a name or pattern.

```
$ sleep 300 & sleep 300 & sleep 300 &
$ pgrep sleep
8013
8016
8017

$ pkill sleep
$ pgrep sleep
(no output - all killed)
```

#### Common pkill Options

| Command | What it does |
|---------|-------------|
| `pkill name` | Kill by process name |
| `pkill -f pattern` | Kill by full command line |
| `pkill -u username` | Kill processes of a user |
| `pkill -9 name` | Force kill by name |
| `pkill -f "python.*server"` | Regex pattern match |

```
pkill nginx              # Kill all nginx processes
pkill -f "my script"     # Kill matching full command
pkill -f "python.*server" # Kill python server processes
pkill -9 firefox         # Force kill firefox
```

---

### killall - Kill by Exact Name

Kills all processes with an exact name.

```
$ sleep 300 & sleep 300 & sleep 300 &
$ pgrep sleep
8026
8027
8028

$ killall sleep
$ pgrep sleep
(no output - all killed)
```

#### pkill vs killall

| Feature | pkill | killall |
|---------|-------|---------|
| Match by | Name or pattern | Exact name |
| Pattern support | Yes (`-f`) | Limited |
| Partial match | Yes | No |
| Example | `pkill python` matches `python3`, `python3.12` | `killall python3` matches only `python3` |

---

### Background Jobs

Run commands in the background so you can keep using the terminal.

#### Start Background Job with &

```
$ sleep 60 &
[1] 8035
$ jobs
[1]  + running    sleep 60

$ jobs -l
[1]  + 8035 running    sleep 60
```

#### Job Control Commands

| Command | What it does |
|---------|-------------|
| `command &` | Run in background |
| `jobs` | List background jobs |
| `jobs -l` | List with PIDs |
| `fg %1` | Bring job to foreground |
| `bg %1` | Resume job in background |
| `kill %1` | Kill job 1 |
| `Ctrl+Z` | Pause current process |
| `Ctrl+C` | Kill current process |

#### Workflow Example

```
$ long_running_command
^Z                # Press Ctrl+Z to pause
[1]+ Stopped     long_running_command

$ bg %1           # Resume in background
[1]+ long_running_command &

$ fg %1           # Bring to foreground
```

---

### nohup - Process Survives Logout

Run a process that continues even after you close the terminal.

#### Basic Syntax

```
nohup command > output.log 2>&1 &
```

| Part | What it does |
|------|-------------|
| `nohup` | Ignore hangup signal (survives logout) |
| `command` | What to run |
| `> output.log` | Redirect output to file |
| `2>&1` | Redirect errors to same file |
| `&` | Run in background |

#### Real Output

```
$ nohup sleep 300 > /tmp/nohup_test.log 2>&1 &
PID: 8039

$ ps aux | grep "sleep 300"
amit  8039  0.0  0.0  8288  1920 ?  SN  15:11  0:00 sleep 300
```

#### What nohup Does

1. Ignores SIGHUP signal (process survives terminal close)
2. Redirects output to `nohup.out` (if you don't specify a file)
3. Process runs until killed manually

#### Common Use Cases

```
# Run script that survives logout
nohup python script.py > output.log 2>&1 &

# Run server in background
nohup ./server > server.log 2>&1 &

# Run long task
nohup ./backup.sh > backup.log 2>&1 &
```

#### Kill nohup Process

```
$ pkill -f "sleep 300"
$ kill PID
```

---

### Process Control Cheat Sheet

| Command | Purpose |
|---------|---------|
| `kill PID` | Stop process gracefully |
| `kill -9 PID` | Force stop process |
| `pkill name` | Stop by name/pattern |
| `killall name` | Stop by exact name |
| `command &` | Run in background |
| `jobs` | List background jobs |
| `fg %1` | Bring to foreground |
| `bg %1` | Resume in background |
| `nohup cmd &` | Run surviving logout |
| `Ctrl+Z` | Pause current process |
| `Ctrl+C` | Kill current process |

---

## 18. System Monitoring

### uptime - How Long System Running

Shows system uptime and load average.

```
$ uptime
 15:14:23 up 10 min, 1 user, load average: 2.55, 3.13, 1.92
```

#### Understanding Load Average

| Value | Meaning |
|-------|---------|
| `15:14:23` | Current time |
| `up 10 min` | System running for 10 minutes |
| `1 user` | 1 user logged in |
| `load average: 2.55, 3.13, 1.92` | Load for last 1, 5, 15 minutes |

**Load average interpretation:**
- Load = number of processes waiting for CPU
- If load > CPU cores, processes are waiting
- Example: Load 2.0 on 4-core CPU = 50% capacity used

```
$ uptime -p
up 10 minutes
```

---

### free - Memory Usage

Shows RAM and swap usage.

```
$ free -h
               total        used        free      shared  buff/cache   available
Mem:           7.1Gi       4.9Gi       509Mi        67Mi       2.1Gi       2.2Gi
Swap:           15Gi       3.0Gi        13Gi
```

#### Column Explanations

| Column | Meaning |
|--------|---------|
| `total` | Total RAM |
| `used` | RAM currently used |
| `free` | Completely free RAM |
| `shared` | RAM shared between processes |
| `buff/cache` | RAM used for buffers/cache (reclaimable) |
| `available` | RAM available for new programs |

**Key formula:** `available ≈ free + buffers + cache`

#### free Options

| Command | What it does |
|---------|-------------|
| `free` | Show in KB |
| `free -h` | Human readable (KB, MB, GB) |
| `free -m` | Show in megabytes |
| `free -g` | Show in gigabytes |

```
$ free -m
               total        used        free      shared  buff/cache   available
Mem:            7284        5005         508          67        2108        2279
Swap:          16383        3047       13336
```

---

### vmstat - Virtual Memory Statistics

Shows CPU, memory, swap, and I/O statistics.

```
$ vmstat
procs -----------memory---------- ---swap-- -----io---- -system-- -------cpu-------
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
 2  0 3120384 522380  57616 2102084 1360 5982  9481  8222 18970   20 18  5 77  1  0
```

#### Run with Interval

```
$ vmstat 2 3
procs -----------memory---------- ---swap-- -----io---- -system-- -------cpu-------
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
 2  0 3120384 522128  57616 2102084 1360 5982  9481  8222 18970   20 18  5 77  1  0
 3  0 3119872 315352  61824 2191132 3532    0 50166   366 21408 25647 20  6 72  1  0  0
 4  0 3119616 296376  62648 2198364  114    0  1128   944 23304 25131 15 10 76  0  0  0
```

#### Column Explanations

| Section | Column | Meaning |
|---------|--------|---------|
| **Procs** | `r` | Processes waiting for CPU |
| | `b` | Processes in uninterruptible sleep |
| **Memory** | `swpd` | Virtual memory used |
| | `free` | Free memory |
| | `buff` | Buffers |
| | `cache` | Cache |
| **Swap** | `si` | Swap in (disk → RAM) |
| | `so` | Swap out (RAM → disk) |
| **IO** | `bi` | Blocks received |
| | `bo` | Blocks sent |
| **System** | `in` | Interrupts per second |
| | `cs` | Context switches per second |
| **CPU** | `us` | User time (%) |
| | `sy` | System time (%) |
| | `id` | Idle time (%) |
| | `wa` | I/O wait time (%) |

**What to watch:**
- High `r` → CPU bottleneck
- High `si`/`so` → Swap thrashing (need more RAM)
- High `wa` → Disk bottleneck
- High `us`/`sy` → CPU busy

---

### iostat - I/O Statistics

Shows disk I/O statistics. Requires `sysstat` package.

```
$ iostat
zsh: command not found: iostat
```

#### Install iostat

```
sudo apt install sysstat
```

#### iostat Usage (after install)

| Command | What it does |
|---------|-------------|
| `iostat` | CPU + I/O stats |
| `iostat -x` | Extended stats (await, %util) |
| `iostat -d` | Disk devices only |
| `iostat 2 3` | Update every 2 sec, 3 times |

#### Alternative: Check I/O Without iostat

```
$ cat /proc/diskstats | head -5
   7       0 loop0 11 0 24 1 0 0 0 0 0 2 1 0 0 0 0 0 0
   7       1 loop1 15 0 50 3 0 0 0 0 0 5 3 0 0 0 0 0 0
   7       2 loop2 9 0 22 0 0 0 0 0 0 1 1 0 0 0 0 0 0
```

---

### System Monitoring Cheat Sheet

| Command | What it shows | When to use |
|---------|--------------|-------------|
| `uptime` | Uptime + load average | Quick health check |
| `free -h` | Memory usage | Check RAM |
| `vmstat` | CPU, memory, swap, I/O | Overall system health |
| `iostat` | Disk I/O | Check disk performance |
| `top` | Interactive processes | Real-time monitoring |
| `htop` | Pretty process viewer | Easy monitoring |
| `ps aux` | Process snapshot | Find specific process |
| `df -h` | Disk space | Check free space |

#### Quick Health Check Command

```
$ uptime && free -h && df -h | head -5
 15:14:28 up 10 min, 1 user, load average: 2.51, 3.11, 1.92
               total        used        free      shared  buff/cache   available
Mem:           7.1Gi       5.0Gi       273Mi        67Mi       2.1Gi       2.1Gi
Swap:           15Gi       3.0Gi        13Gi
Filesystem      Size  Used Avail Use% Mounted on
tmpfs           729M  2.2M  727M   1% /run
efivarfs        148K  121K   23K  85% /sys/firmware/efi/efivars
/dev/nvme0n1p2  234G  145G   77G  66% /
tmpfs           3.6G   48M  3.6G   2% /dev/shm
```

---

## 19. Package Management - Debian

Debian-based systems (Ubuntu, Linux Mint, Debian) use **apt** and **dpkg**.

### Check Your Distro

```
$ cat /etc/os-release
NAME="Linux Mint"
VERSION="22.3 (Zena)"
ID=linuxmint
ID_LIKE="ubuntu debian"
```

---

### apt - Advanced Package Tool

**apt** is the high-level tool. It handles dependencies automatically.

#### Daily Use Commands

| Command | What it does |
|---------|-------------|
| `sudo apt update` | Update package list |
| `sudo apt upgrade` | Upgrade all packages |
| `sudo apt install pkg` | Install package |
| `sudo apt remove pkg` | Remove package |
| `sudo apt purge pkg` | Remove package + config files |

```
$ apt --version
apt 2.8.3 (amd64) (Mint wrapper)
```

#### Search and Info Commands

| Command | What it does |
|---------|-------------|
| `apt search keyword` | Search for package |
| `apt show pkg` | Show package info |
| `apt list --installed` | List installed packages |
| `apt list --upgradable` | List upgradable packages |

#### Real Output

```
$ apt search nginx
v   dh-sequence-nginx               -
p   elpa-nginx-mode                 - major mode for editing nginx config files
p   golang-github-nginxinc-nginx-pl - client for NGINX Plus API for Go (library)
p   libnginx-mod-http-auth-pam      - PAM authentication module for Nginx

$ apt show htop
Package: htop
Version: 3.3.0-4build1
Priority: optional
Section: utils
Origin: Ubuntu
Installed-Size: 434 kB
Depends: libc6 (>= 2.38), libncursesw6 (>= 6)
Homepage: https://htop.dev/
Download-Size: 171 kB

$ apt list --installed
Listing...
7zip/noble,now 23.01+dfsg-11 amd64 [installed]
acl/noble-updates,now 2.3.2-1build1.1 amd64 [installed]
adb/noble,now 1:34.0.4-1build3 amd64 [installed]

$ apt list --upgradable
Listing...
accountsservice/noble-updates 23.13.9-2ubuntu6.1 amd64 [upgradable from: 23.13.9-2ubuntu6]
alsa-ucm-conf/noble-updates 1.2.10-1ubuntu5.14 all [upgradable from: 1.2.10-1ubuntu5.8]
```

#### apt Workflow

```
Step 1: sudo apt update          # Get latest package list
Step 2: sudo apt upgrade         # Install available updates
Step 3: sudo apt install pkg     # Install new package
```

---

### dpkg - Debian Package Manager

**dpkg** is the low-level tool. It installs `.deb` files directly.

#### Common dpkg Commands

| Command | What it does |
|---------|-------------|
| `dpkg -l` | List all installed packages |
| `dpkg -s pkg` | Show package status |
| `dpkg -L pkg` | List files in package |
| `dpkg -S /path/file` | Find which package owns file |
| `sudo dpkg -i file.deb` | Install .deb file |
| `sudo dpkg -r pkg` | Remove package |

#### Real Output

```
$ dpkg --version
Debian 'dpkg' package management program version 1.22.6 (amd64).

$ dpkg -l | head -5
||/ Name              Version           Architecture Description
+++-==================-=================-============-============
ii  2to3              3.12.3-0ubuntu2.1 all          2to3 binary using python3
ii  7zip              23.01+dfsg-11     amd64        7-Zip file archiver
ii  accountsservice   23.13.9-2ubuntu6  amd64        query and manipulate user account

$ dpkg -l | grep nginx
ii  nginx              1.24.0-2ubuntu7.5  amd64   small, powerful, scalable web/proxy server
ii  nginx-common       1.24.0-2ubuntu7.5  all     nginx - common files

$ dpkg -s htop
Package: htop
Status: install ok installed
Priority: optional
Section: utils
Installed-Size: 424
Version: 3.3.0-4build1

$ dpkg -L htop
/usr/bin
/usr/bin/htop
/usr/share/applications/htop.desktop
/usr/share/doc/htop/AUTHORS
```

#### dpkg Status Codes (in dpkg -l)

| Code | Meaning |
|------|---------|
| `ii` | Installed |
| `rc` | Removed but config remains |
| `un` | Not installed |
| `iU` | Unpacked but not configured |

---

### apt vs dpkg

| Task | apt | dpkg |
|------|-----|------|
| Update list | `apt update` | N/A |
| Install | `apt install pkg` | `dpkg -i pkg.deb` |
| Remove | `apt remove pkg` | `dpkg -r pkg` |
| List installed | `apt list --installed` | `dpkg -l` |
| Show info | `apt show pkg` | `dpkg -s pkg` |
| Search | `apt search pkg` | N/A |
| Handle deps | Automatic | Manual |

**Key difference:**
- `apt` = high-level (handles dependencies)
- `dpkg` = low-level (installs .deb files)

If `dpkg -i` fails due to missing dependencies:
```
sudo dpkg -i package.deb      # May fail
sudo apt install -f           # Fix dependencies
```

---

## 20. Package Management - Red Hat

Red Hat-based systems (RHEL, CentOS, Fedora) use **dnf/yum** and **rpm**.

### dnf - Dandified YUM (Fedora/CentOS 8+/RHEL 8+)

**dnf** is the modern high-level package manager.

#### Common dnf Commands

| Command | What it does |
|---------|-------------|
| `sudo dnf install pkg` | Install package |
| `sudo dnf remove pkg` | Remove package |
| `sudo dnf update` | Update all packages |
| `sudo dnf search keyword` | Search package |
| `sudo dnf info pkg` | Show package info |
| `dnf list installed` | List installed packages |
| `dnf list available` | List available packages |

```
sudo dnf install htop
sudo dnf remove htop
sudo dnf update
sudo dnf search nginx
sudo dnf info htop
dnf list installed | head
```

---

### yum - Yellowdog Updater Modified (RHEL/CentOS 6-7)

Older version, same syntax as dnf.

| Command | What it does |
|---------|-------------|
| `sudo yum install pkg` | Install package |
| `sudo yum remove pkg` | Remove package |
| `sudo yum update` | Update all packages |
| `sudo yum search keyword` | Search package |
| `sudo yum info pkg` | Show package info |
| `yum list installed` | List installed packages |

**Note:** `yum` is now replaced by `dnf` on modern systems. Same commands work.

---

### rpm - Red Hat Package Manager

**rpm** is the low-level tool. It installs `.rpm` files directly.

#### Common rpm Commands

| Command | What it does |
|---------|-------------|
| `rpm -qa` | List all installed packages |
| `rpm -q pkg` | Check if package installed |
| `rpm -qi pkg` | Show package info |
| `rpm -ql pkg` | List files in package |
| `rpm -qf /path/file` | Find which package owns file |
| `sudo rpm -ivh file.rpm` | Install .rpm file |
| `sudo rpm -e pkg` | Remove package |

```
rpm -qa | head -10
rpm -q htop
rpm -qi htop
rpm -ql htop
rpm -qf /usr/bin/ls
sudo rpm -ivh package.rpm
sudo rpm -e htop
```

---

### dnf/yum vs rpm

| Task | dnf/yum | rpm |
|------|---------|-----|
| Install | `dnf install pkg` | `rpm -i pkg.rpm` |
| Remove | `dnf remove pkg` | `rpm -e pkg` |
| List installed | `dnf list installed` | `rpm -qa` |
| Show info | `dnf info pkg` | `rpm -qi pkg` |
| Search | `dnf search pkg` | N/A |
| Handle deps | Automatic | Manual |

**Key difference:** Same as Debian - high-level handles dependencies, low-level doesn't.

---

### Debian vs Red Hat Comparison

| Task | Debian (apt/dpkg) | Red Hat (dnf/rpm) |
|------|-------------------|-------------------|
| Update list | `sudo apt update` | `sudo dnf update` |
| Install | `sudo apt install pkg` | `sudo dnf install pkg` |
| Remove | `sudo apt remove pkg` | `sudo dnf remove pkg` |
| List installed | `apt list --installed` | `dnf list installed` |
| Show info | `apt show pkg` | `dnf info pkg` |
| Search | `apt search pkg` | `dnf search pkg` |
| Install file | `sudo dpkg -i file.deb` | `sudo rpm -ivh file.rpm` |
| List all (low) | `dpkg -l` | `rpm -qa` |
| Package format | `.deb` | `.rpm` |

---

### Package Management Cheat Sheet

#### Debian/Ubuntu

```
sudo apt update              # Update package list
sudo apt upgrade             # Upgrade all packages
sudo apt install pkg         # Install package
sudo apt remove pkg          # Remove package
sudo apt search keyword      # Search package
apt show pkg                 # Show package info
apt list --installed         # List installed
sudo dpkg -i file.deb        # Install .deb file
dpkg -l                      # List all installed
```

#### Red Hat/Fedora/CentOS

```
sudo dnf install pkg         # Install package
sudo dnf remove pkg          # Remove package
sudo dnf update              # Update all
sudo dnf search keyword      # Search package
dnf info pkg                 # Show package info
dnf list installed           # List installed
sudo rpm -ivh file.rpm       # Install .rpm file
rpm -qa                      # List all installed
```

---

## 21. User Administration

Manage user accounts, passwords, and groups.

### Understanding Users

#### User Files

| File | Purpose |
|------|---------|
| `/etc/passwd` | User account information |
| `/etc/shadow` | Password hashes (root only) |
| `/etc/group` | Group information |

#### /etc/passwd Format

```
username:password:UID:GID:comment:home:shell
```

```
$ cat /etc/passwd | grep -E "amit|root"
root:x:0:0:root:/root:/bin/bash
amit:x:1000:1000:amit,,,:/home/amit:/usr/bin/zsh
```

| Field | Meaning | Example |
|-------|---------|---------|
| `username` | Login name | `amit` |
| `password` | `x` = in /etc/shadow | `x` |
| `UID` | User ID | `1000` |
| `GID` | Primary group ID | `1000` |
| `comment` | Full name/description | `amit,,,` |
| `home` | Home directory | `/home/amit` |
| `shell` | Default shell | `/usr/bin/zsh` |

#### /etc/group Format

```
group:password:GID:members
```

```
$ cat /etc/group | grep -E "amit|sudo|docker"
sudo:x:27:amit
amit:x:1000:
docker:x:986:amit,jenkins
```

| Field | Meaning | Example |
|-------|---------|---------|
| `group` | Group name | `docker` |
| `password` | `x` = in /etc/gshadow | `x` |
| `GID` | Group ID | `986` |
| `members` | Comma-separated users | `amit,jenkins` |

#### Your User Info

```
$ id
uid=1000(amit) gid=1000(amit) groups=1000(amit),4(adm),27(sudo),986(docker)

$ groups
amit adm cdrom sudo dip plugdev users lpadmin sambashare libvirt ollama docker kvm
```

---

### useradd - Create a New User

#### Common useradd Options

| Option | What it does |
|--------|-------------|
| `-m` | Create home directory |
| `-s /bin/bash` | Set default shell |
| `-g group` | Set primary group |
| `-G group1,group2` | Set additional groups |
| `-u UID` | Set custom User ID |
| `-e 2025-12-31` | Set expiry date |
| `-c "comment"` | Add comment (full name) |

#### Examples

```
sudo useradd -m john                    # Create with home dir
sudo useradd -m -s /bin/bash john       # Create + bash shell
sudo useradd -m -s /bin/zsh john        # Create + zsh shell
sudo useradd -m -g developers john      # Set primary group
sudo useradd -m -G sudo,docker john     # Add to multiple groups
sudo useradd -m -u 1500 john            # Custom UID
sudo useradd -m -e 2025-12-31 john      # Account expires
sudo passwd john                        # Set password
```

#### After Creating User

```
sudo useradd -m -s /bin/bash newuser
sudo passwd newuser
id newuser                              # Verify
ls -la /home/newuser                    # Check home dir
```

---

### usermod - Modify Existing User

#### Common usermod Options

| Option | What it does |
|--------|-------------|
| `-l newname` | Change username |
| `-d /new/home` | Change home directory |
| `-s /bin/zsh` | Change default shell |
| `-aG group` | **Add** to group (append) |
| `-G group1,group2` | **Set** groups (replace all) |
| `-L` | Lock account |
| `-U` | Unlock account |
| `-e date` | Change expiry date |

#### Important: -aG vs -G

```
sudo usermod -aG docker john    # ADD to docker (keeps other groups)
sudo usermod -G docker john     # ONLY in docker (removes other groups)
```

**Always use `-aG` when adding to a group!** Using `-G` will remove the user from all other groups.

#### Examples

```
sudo usermod -aG sudo john          # Give sudo access
sudo usermod -aG docker john        # Add to docker group
sudo usermod -l johnny john         # Change username
sudo usermod -s /bin/bash john      # Change shell
sudo usermod -d /home/new john      # Change home dir
sudo usermod -L john                # Lock account
sudo usermod -U john                # Unlock account
```

---

### passwd - Manage Passwords

#### Common passwd Options

| Option | What it does |
|--------|-------------|
| (none) | Change own password |
| `sudo passwd user` | Change user's password |
| `-l user` | Lock password |
| `-u user` | Unlock password |
| `-S user` | Show password status |
| `-e user` | Force password change on next login |
| `-d user` | Delete password (no password needed) |

#### Examples

```
passwd                    # Change your own password
sudo passwd john          # Change John's password
sudo passwd -S john       # Show password status
sudo passwd -l john       # Lock John's account
sudo passwd -u john       # Unlock John's account
sudo passwd -e john       # Force password change on next login
```

#### Your Password Status

```
$ passwd -S $(whoami)
amit P 09/21/2026 0 99999 7 -1
```

| Status | Meaning |
|--------|---------|
| `P` | Password set (valid) |
| `L` | Locked |
| `NP` | No password |

---

### userdel - Delete a User

#### Common userdel Options

| Option | What it does |
|--------|-------------|
| `userdel user` | Delete user (keeps home) |
| `-r user` | Delete user + home directory |
| `-f user` | Force delete (even if logged in) |

#### Examples

```
sudo userdel john           # Delete user (home remains)
sudo userdel -r john        # Delete user + home directory
sudo userdel -f john        # Force delete (logged in)
sudo userdel -r -f john     # Force delete + home
```

**Warning:** `-r` permanently deletes the home directory and all files!

---

### User Management Workflow

#### Create a Complete User

```
sudo useradd -m -s /bin/bash newuser    # Create user
sudo passwd newuser                      # Set password
sudo usermod -aG sudo newuser           # Give sudo (optional)
id newuser                              # Verify
```

#### Delete a User Completely

```
sudo userdel -r username                # Delete user + home
```

---

### User Management Cheat Sheet

| Task | Command |
|------|---------|
| **Create user** | `sudo useradd -m -s /bin/bash user` |
| **Set password** | `sudo passwd user` |
| **Add to group** | `sudo usermod -aG group user` |
| **Change shell** | `sudo usermod -s /bin/bash user` |
| **Lock account** | `sudo usermod -L user` |
| **Unlock account** | `sudo usermod -U user` |
| **Delete user** | `sudo userdel -r user` |
| **View all users** | `cat /etc/passwd` |
| **View all groups** | `cat /etc/group` |
| **User info** | `id user` |
| **Your groups** | `groups` |
| **Password status** | `passwd -S user` |

---

## 22. Group Management

Groups organize users and control shared permissions.

### groupadd - Create New Group

#### Common Options

| Option | What it does |
|--------|-------------|
| `groupadd name` | Create group |
| `-g GID` | Set custom Group ID |
| `-r` | Create system group |

```
sudo groupadd developers           # Create group
sudo groupadd -g 1500 team         # Create with custom GID
sudo groupadd -r sysgroup          # Create system group
```

#### Current Groups on Your System

```
$ cat /etc/group | tail -10
docker:x:986:amit,jenkins
ollama:x:984:amit
libvirt:x:132:amit
```

---

### groupmod - Modify Existing Group

#### Common Options

| Option | What it does |
|--------|-------------|
| `-n newname` | Rename group |
| `-g GID` | Change Group ID |

```
sudo groupmod -n newname oldname     # Rename group
sudo groupmod -g 1500 groupname      # Change GID
```

---

### groupdel - Delete a Group

```
sudo groupdel groupname              # Delete group
sudo groupdel -f groupname           # Force delete
```

**Note:** Cannot delete a group if it's a primary group of any user. Use `-f` to force.

---

### Managing Group Membership

#### Add User to Group

```
sudo usermod -aG groupname username    # Add to group (append)
sudo gpasswd -a username groupname     # Alternative method
```

#### Remove User from Group

```
sudo gpasswd -d username groupname     # Remove from group
sudo usermod -G group1,group2 user     # Set groups (replace all)
```

#### View Group Members

```
groups username               # Show user's groups
id username                   # Show user's groups
getent group groupname        # Show group members
cat /etc/group | grep group   # From group file
```

#### Real Output

```
$ getent group docker
docker:x:986:amit,jenkins

$ id amit
uid=1000(amit) gid=1000(amit) groups=1000(amit),4(adm),27(sudo),986(docker)

$ groups amit
amit adm cdrom sudo dip plugdev users lpadmin sambashare libvirt ollama docker kvm
```

---

### Group Management Cheat Sheet

| Task | Command |
|------|---------|
| Create group | `sudo groupadd groupname` |
| Create with GID | `sudo groupadd -g 1500 groupname` |
| Rename group | `sudo groupmod -n newname oldname` |
| Change GID | `sudo groupmod -g GID groupname` |
| Delete group | `sudo groupdel groupname` |
| Add user to group | `sudo usermod -aG group user` |
| Remove from group | `sudo gpasswd -d user group` |
| View group members | `getent group groupname` |
| View user groups | `groups username` |

---

## 23. Sudo

**sudo** (Super User DO) lets authorized users run commands as root.

### sudo Basics

| Command | What it does |
|---------|-------------|
| `sudo command` | Run command as root |
| `sudo -u user command` | Run as specific user |
| `sudo -i` | Start root shell |
| `sudo -s` | Start shell as root |
| `sudo -l` | List allowed sudo commands |
| `sudo -k` | Forget cached password |

```
$ sudo --version
Sudo version 1.9.15p5

$ groups | grep sudo
sudo
(You are in sudo group)
```

#### Examples

```
sudo apt update                  # Run apt as root
sudo systemctl restart nginx     # Restart service as root
sudo -i                          # Get root shell
sudo -l                          # See what you can run
```

---

### /etc/sudoers - Sudo Configuration

**⚠️ NEVER edit /etc/sudoers directly! Always use `sudo visudo`!**

#### Why Not Edit Directly?

```
$ cat /etc/sudoers
cat: /etc/sudoers: Permission denied
```

If you break the sudoers file with a text editor:
- You get **locked out** of sudo
- Recovery requires booting from live USB

#### Sudoers File Format

```
user  ALL=(ALL:ALL) ALL
```

| Field | Meaning |
|-------|---------|
| `user` | Who can run commands |
| `ALL` | From any host |
| `(ALL)` | As any user |
| `(ALL:ALL)` | As any user:group |
| `ALL` | Any command |

#### Common Sudoers Entries

```
# Full sudo access for a user
amit  ALL=(ALL:ALL) ALL

# Group specification (prefix % means group)
%sudo  ALL=(ALL:ALL) ALL

# Specific command without password
john  ALL=(ALL) NOPASSWD: /usr/bin/apt

# Specific command only
bob   ALL=(ALL) /usr/bin/systemctl restart nginx

# Run as specific user
www   ALL=(www) NOPASSWD: /usr/bin/systemctl reload nginx
```

---

### visudo - Safe Sudoers Editor

#### Why Use visudo?

| Feature | visudo | nano/vi directly |
|---------|--------|------------------|
| Syntax check | Yes | No |
| Prevents lockout | Yes | No |
| Safe | Yes | Dangerous |

#### Usage

```
sudo visudo                # Edit /etc/sudoers safely
sudo visudo -f file        # Edit alternative file
```

#### How It Works

1. Creates a temporary file
2. You edit the temp file
3. Validates syntax before saving
4. If syntax is wrong, **rejects the change**
5. Only saves if valid

#### NEVER Do This

```
sudo nano /etc/sudoers     # ❌ DANGEROUS!
sudo vim /etc/sudoers      # ❌ DANGEROUS!
```

**If you break sudoers:** Boot from live USB → mount disk → fix the file.

---

### Sudo Cheat Sheet

| Task | Command |
|------|---------|
| Run as root | `sudo command` |
| Root shell | `sudo -i` |
| List allowed | `sudo -l` |
| Edit sudoers | `sudo visudo` |
| Check sudo group | `groups \| grep sudo` |
| Add user to sudo | `sudo usermod -aG sudo username` |

### Sudoers Format Quick Reference

```
user  ALL=(ALL:ALL) ALL           # Full access
%group ALL=(ALL:ALL) ALL          # Group access
user  ALL=(ALL) NOPASSWD: cmd     # No password needed
user  ALL=(ALL) /path/to/cmd      # Specific command only
user  ALL=(specific_user) cmd     # Run as specific user
```

---

## 24. Disk Management

View and manage disks, partitions, and filesystems.

### lsblk - List Block Devices

Shows all disks and partitions in a tree view.

```
$ lsblk
NAME        MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
sda           8:0    0 931.5G  0 disk 
├─sda1        8:1    0    16M  0 part 
├─sda2        8:2    0 345.6G  0 part 
├─sda3        8:3    0   293G  0 part 
└─sda4        8:4    0   293G  0 part 
nvme0n1     259:0    0 238.5G  0 disk 
├─nvme0n1p1 259:1    0   512M  0 part /boot/efi
└─nvme0n1p2 259:2    0   238G  0 part /
```

#### Understanding lsblk Output

| Column | Meaning |
|--------|---------|
| `NAME` | Device name |
| `SIZE` | Device size |
| `TYPE` | `disk`, `part`, `rom`, `loop` |
| `MOUNTPOINTS` | Where it's mounted |

#### Common lsblk Options

| Option | What it does |
|--------|-------------|
| `lsblk` | Tree view |
| `lsblk -f` | Show filesystem type |
| `lsblk -d` | Disks only (no partitions) |
| `lsblk -e7` | Exclude loop devices |
| `lsblk -o col1,col2` | Custom columns |

#### Real Output - With Filesystem

```
$ lsblk -f
NAME        FSTYPE FSVER LABEL   UUID                                 MOUNTPOINTS
sda                                                                         
├─sda2      ntfs         Drive_D D68A70A08A707F35
├─sda3      ntfs         Drive_E 8A6A6B276A6B0EEF
└─sda4      ntfs         Drive_F 8040584340584258
nvme0n1                                                                     
├─nvme0n1p1 vfat   FAT32         3ADA-D663                             /boot/efi
└─nvme0n1p2 ext4   1.0           2391876f-a5f5-4a74-b1a1-2c299f87ebb8 /
```

#### Custom Columns

```
$ lsblk -o NAME,SIZE,TYPE,FSTYPE,MOUNTPOINT
NAME          SIZE TYPE FSTYPE MOUNTPOINT
sda         931.5G disk        
├─sda2      345.6G part ntfs   
nvme0n1     238.5G disk        
├─nvme0n1p1   512M part vfat   /boot/efi
└─nvme0n1p2   238G part ext4   /
```

---

### fdisk - Partition Table Editor

Edit disk partitions interactively.

#### View Partitions

```
sudo fdisk -l              # List all partitions
sudo fdisk -l /dev/sda     # List specific disk
```

#### Interactive Mode

```
sudo fdisk /dev/sda        # Edit disk (needs sudo)
```

#### fdisk Commands

| Key | What it does |
|-----|-------------|
| `p` | Print partition table |
| `n` | Create new partition |
| `d` | Delete partition |
| `t` | Change partition type |
| `w` | Write changes to disk |
| `q` | Quit without saving |
| `m` | Show help |

#### Example Workflow

```
$ sudo fdfdisk /dev/sda
Command (m for help): p        # See current partitions
Command (m for help): n        # Create new partition
Command (m for help): w        # Write and exit
```

**Warning:** Always use `q` to quit if you're unsure. Use `w` only when you're sure!

---

### parted - Advanced Partition Manager

More modern than fdisk. Supports GPT and large disks.

#### View Disks

```
sudo parted -l               # List all disks
sudo parted /dev/sda print   # Show specific disk
```

#### Interactive Mode

```
sudo parted /dev/sda         # Edit disk (needs sudo)
```

#### parted Commands

| Command | What it does |
|---------|-------------|
| `print` | Show partition table |
| `mklabel gpt` | Create new GPT partition table |
| `mklabel msdos` | Create new MBR partition table |
| `mkpart` | Create new partition |
| `rm` | Delete partition |
| `resizepart` | Resize partition |
| `quit` | Quit |
| `help` | Show help |

#### parted vs fdisk

| Feature | fdisk | parted |
|---------|-------|--------|
| MBR disks | Yes | Yes |
| GPT disks | Limited | Yes (full) |
| Large disks (>2TB) | Limited | Yes |
| Scripting | Hard | Easy (`-s`) |
| Interactive | Yes | Yes |
| Modern | Older | Newer |

**When to use:**
- `fdisk` = Simple MBR partitioning
- `parted` = GPT, large disks, scripting

---

### Disk Management Workflow

#### View Your Disks

```
lsblk                     # See all disks
lsblk -f                  # With filesystem info
df -h                     # See mounted space
sudo fdisk -l             # Detailed partition info
```

#### Create Partition (fdisk)

```
sudo fdisk /dev/sdb
  p  = Check current state
  n  = New partition
  w  = Write changes
```

#### After Partitioning

```
sudo mkfs.ext4 /dev/sdb1    # Format as ext4
sudo mount /dev/sdb1 /mnt   # Mount
blkid /dev/sdb1             # Get UUID
```

#### Make Permanent (add to /etc/fstab)

```
UUID=xxxx-xxxx  /mnt  ext4  defaults  0  2
```

---

### Disk Management Cheat Sheet

| Task | Command |
|------|---------|
| List disks | `lsblk` |
| List with filesystem | `lsblk -f` |
| List partitions | `sudo fdisk -l` |
| List all disks (parted) | `sudo parted -l` |
| Show mounted space | `df -h` |
| Show disk UUIDs | `blkid` |
| Edit with fdisk | `sudo fdisk /dev/sdX` |
| Edit with parted | `sudo parted /dev/sdX` |
| Format partition | `sudo mkfs.ext4 /dev/sdX1` |
| Mount partition | `sudo mount /dev/sdX1 /mnt` |

---

## 25. Filesystems and Mounting

### Filesystem Types

#### ext4 (Extended 4)

| Feature | Value |
|---------|-------|
| Default on | Ubuntu, Linux Mint, Debian |
| Max file size | 16 TB |
| Max volume | 1 EB |
| Journaling | Yes |
| Snapshots | No |
| Compression | No |

**Best for:** General purpose, root filesystem, servers

#### xfs (X File System)

| Feature | Value |
|---------|-------|
| Default on | RHEL, CentOS, Fedora |
| Max file size | 8 EB |
| Max volume | 8 EB |
| Journaling | Yes |
| Snapshots | No |
| Compression | No |

**Best for:** Large files, media servers, high performance

#### btrfs (B-tree File System)

| Feature | Value |
|---------|-------|
| Default on | Fedora, openSUSE |
| Max file size | 16 EB |
| Journaling | Yes |
| Snapshots | Yes |
| Compression | Yes |
| Checksums | Yes |

**Best for:** NAS, backups, data integrity

#### Comparison Table

| Feature | ext4 | xfs | btrfs |
|---------|------|-----|-------|
| Journaling | Yes | Yes | Yes |
| Snapshots | No | No | Yes |
| Compression | No | No | Yes |
| Max file | 16 TB | 8 EB | 16 EB |
| Performance | Good | Best (large) | Good |
| Default | Ubuntu/Mint | RHEL/CentOS | Fedora |

#### Your Filesystem

```
$ df -T
Filesystem     Type     1K-blocks      Used Available Use% Mounted on
/dev/nvme0n1p2 ext4     244506940 150863684  81150200  66% /
/dev/nvme0n1p1 vfat        523248      6288    516960   2% /boot/efi
```

---

### Filesystem Tools

| Task | Command |
|------|---------|
| Show filesystem type | `lsblk -f` or `df -T` |
| Format as ext4 | `sudo mkfs.ext4 /dev/sdX1` |
| Format as xfs | `sudo mkfs.xfs /dev/sdX1` |
| Format as btrfs | `sudo mkfs.btrfs /dev/sdX1` |
| Check ext4 | `sudo e2fsck /dev/sdX1` |
| Check xfs | `sudo xfs_repair /dev/sdX1` |
| Check btrfs | `sudo btrfs check /dev/sdX1` |

---

### mount - Attach Filesystem

Mount a filesystem to a directory.

#### Basic Syntax

```
sudo mount /dev/sdb1 /mnt           # Mount device to directory
sudo mount /dev/sdb1 /mnt -o ro     # Mount read-only
sudo mount -t ext4 /dev/sdb1 /mnt    # Specify filesystem type
```

#### Common mount Options

| Option | What it does |
|--------|-------------|
| `-o ro` | Read-only |
| `-o rw` | Read-write (default) |
| `-o noexec` | No execute permission |
| `-o nosuid` | No setuid bit |
| `-o loop` | Mount file as loop device |
| `-t type` | Specify filesystem type |

#### View Current Mounts

```
$ mount | head -10
sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime)
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
/dev/nvme0n1p2 on / type ext4 (rw,relatime,discard,errors=remount-ro)
```

---

### umount - Detach Filesystem

Unmount a filesystem.

#### Basic Syntax

```
umount /mnt                          # Unmount by path
umount /dev/sdb1                     # Unmount by device
sudo umount /mnt                     # If permission denied
umount -l /mnt                       # Lazy unmount (if busy)
```

#### If "Device is Busy"

```
fuser -vm /mnt                       # See what's using it
lsof /mnt                            # See open files
umount -l /mnt                       # Lazy detach (detaches when free)
```

---

### /etc/fstab - Automatic Mounting

File that lists filesystems to mount at boot.

#### Format

```
device  mountpoint  type  options  dump  pass
```

| Field | Meaning |
|-------|---------|
| 1. device | `/dev/sdX`, `UUID=xxx`, or `LABEL=xxx` |
| 2. mountpoint | Where to mount |
| 3. type | ext4, xfs, btrfs, vfat, tmpfs |
| 4. options | defaults, ro, noexec, etc. |
| 5. dump | 0=backup off, 1=on |
| 6. pass | 0=no check, 1=first, 2=others |

#### Real fstab Output

```
$ cat /etc/fstab
# <file system> <mount point>   <type>  <options>       <dump>  <pass>
UUID=2391876f-a5f5-4a74-b1a1-2c299f87ebb8 /  ext4  errors=remount-ro,discard 0  1
UUID=3ADA-D663  /boot/efi       vfat    umask=0077      0       1
/swapfile        none            swap    sw              0       0
```

#### Example Entries

```
# device           mountpoint  type  options     dump pass
/dev/sdb1          /mnt/data   ext4  defaults    0    2
UUID=xxxx-xxxx     /home       ext4  defaults    0    2
UUID=yyyy-yyyy     /boot/efi   vfat  umask=0077  0    1
none               /tmp        tmpfs defaults    0    0
```

---

### Mounting Workflow

#### Complete Steps

```
Step 1: Create partition
  sudo fdisk /dev/sdb

Step 2: Format
  sudo mkfs.ext4 /dev/sdb1

Step 3: Create mount point
  sudo mkdir -p /mnt/data

Step 4: Mount
  sudo mount /dev/sdb1 /mnt/data

Step 5: Make permanent (add to fstab)
  sudo blkid /dev/sdb1              # Get UUID
  sudo nano /etc/fstab              # Add entry
  UUID=xxxx  /mnt/data  ext4  defaults  0  2

Step 6: Test
  sudo umount /mnt/data
  sudo mount -a                     # Test fstab
```

---

### Mounting Cheat Sheet

| Task | Command |
|------|---------|
| See filesystems | `lsblk -f` |
| See mounted with type | `df -T` |
| Mount | `sudo mount /dev/sdX /mnt` |
| Unmount | `sudo umount /mnt` |
| Mount all from fstab | `sudo mount -a` |
| View fstab | `cat /etc/fstab` |
| Get UUID | `sudo blkid /dev/sdX1` |
| Format ext4 | `sudo mkfs.ext4 /dev/sdX1` |
| Format xfs | `sudo mkfs.xfs /dev/sdX1` |
| Format btrfs | `sudo mkfs.btrfs /dev/sdX1` |

---

## 26. LVM - Logical Volume Management

LVM lets you manage disk space flexibly - resize, span multiple disks, and create snapshots.

### LVM Architecture

```
+---------------------------+
|   Logical Volumes (LV)    |  <- You format & use these
|   /dev/vg0/lv_data        |
+---------------------------+
|   Volume Groups (VG)      |  <- Pool of storage
|   vg0                     |
+---------------------------+
|   Physical Volumes (PV)   |  <- Actual disks/partitions
|   /dev/sda1, /dev/sdb1    |
+---------------------------+
```

### Benefits of LVM

- Resize volumes **online** (no reboot)
- Span multiple disks as one
- Create snapshots
- Move data between disks

### Check LVM Installation

```
$ lvm version
LVM version: 2.03.16(2) (2022-05-18)
```

Install if missing: `sudo apt install lvm2`

---

### Physical Volumes (PV)

Physical Volumes are actual disks or partitions converted for LVM.

#### Commands

| Command | What it does |
|---------|-------------|
| `sudo pvcreate /dev/sdX1` | Create physical volume |
| `sudo pvdisplay` | Show PV details |
| `sudo pvs` | Short summary |
| `sudo pvscan` | Scan for PVs |

```
sudo pvcreate /dev/sdb1              # Convert partition to PV
sudo pvcreate /dev/sdb1 /dev/sdc1    # Multiple disks
sudo pvs                             # Quick summary
sudo pvdisplay                       # Detailed info
```

---

### Volume Groups (VG)

Volume Groups are pools of storage made from one or more PVs.

#### Commands

| Command | What it does |
|---------|-------------|
| `sudo vgcreate name /dev/sdX1` | Create volume group |
| `sudo vgdisplay` | Show VG details |
| `sudo vgs` | Short summary |
| `sudo vgextend vg /dev/sdX1` | Add PV to VG |
| `sudo vgreduce vg /dev/sdX1` | Remove PV from VG |

```
sudo vgcreate my_vg /dev/sdb1              # Create VG
sudo vgcreate my_vg /dev/sdb1 /dev/sdc1    # Multiple PVs
sudo vgs                                   # Quick summary
sudo vgdisplay                             # Detailed info
sudo vgextend my_vg /dev/sdc1              # Expand VG
```

---

### Logical Volumes (LV)

Logical Volumes are the volumes you actually format and use.

#### Commands

| Command | What it does |
|---------|-------------|
| `sudo lvcreate -L 10G -n name vg` | Create LV (size) |
| `sudo lvcreate -l 100%FREE -n name vg` | Create LV (all space) |
| `sudo lvdisplay` | Show LV details |
| `sudo lvs` | Short summary |
| `sudo lvextend -L +5G /dev/vg/lv` | Grow LV |
| `sudo lvreduce -L 5G /dev/vg/lv` | Shrink LV (careful!) |

```
sudo lvcreate -L 10G -n lv_data my_vg        # Create 10GB LV
sudo lvcreate -l 100%FREE -n lv_data my_vg    # Use all free space
sudo lvs                                      # Quick summary
sudo lvextend -L +5G /dev/my_vg/lv_data       # Add 5GB
sudo lvreduce -L 5G /dev/my_vg/lv_data        # Shrink to 5GB
```

---

### LVM Complete Workflow

#### Create and Use LVM

```
Step 1: Create Physical Volume
  sudo pvcreate /dev/sdb1

Step 2: Create Volume Group
  sudo vgcreate my_vg /dev/sdb1

Step 3: Create Logical Volume
  sudo lvcreate -L 10G -n lv_data my_vg

Step 4: Format
  sudo mkfs.ext4 /dev/my_vg/lv_data

Step 5: Mount
  sudo mkdir -p /mnt/data
  sudo mount /dev/my_vg/lv_data /mnt/data

Step 6: Make permanent
  sudo blkid /dev/my_vg/lv_data
  # Add to /etc/fstab:
  /dev/my_vg/lv_data  /mnt/data  ext4  defaults  0  2
```

---

### LVM Resize Workflow

#### Grow a Logical Volume (Online!)

```
Step 1: Check free space in VG
  sudo vgs

Step 2: Extend LV
  sudo lvextend -L +5G /dev/my_vg/lv_data

Step 3: Resize filesystem
  sudo resize2fs /dev/my_vg/lv_data     # For ext4
  sudo xfs_growfs /mnt/data             # For xfs
```

#### Shrink a Logical Volume (Careful!)

```
Step 1: Unmount
  sudo umount /mnt/data

Step 2: Check filesystem
  sudo e2fsck -f /dev/my_vg/lv_data

Step 3: Shrink filesystem FIRST
  sudo resize2fs /dev/my_vg/lv_data 5G

Step 4: Shrink LV
  sudo lvreduce -L 5G /dev/my_vg/lv_data

Step 5: Remount
  sudo mount /dev/my_vg/lv_data /mnt/data
```

**Important:** Always shrink filesystem BEFORE shrinking LV, or you'll lose data!

---

### LVM Cheat Sheet

#### Physical Volumes

| Command | Purpose |
|---------|---------|
| `sudo pvcreate /dev/sdX1` | Create PV |
| `sudo pvdisplay` | Show details |
| `sudo pvs` | Short summary |
| `sudo pvscan` | Scan for PVs |

#### Volume Groups

| Command | Purpose |
|---------|---------|
| `sudo vgcreate name /dev/sdX1` | Create VG |
| `sudo vgdisplay` | Show details |
| `sudo vgs` | Short summary |
| `sudo vgextend vg /dev/sdX1` | Add disk |
| `sudo vgreduce vg /dev/sdX1` | Remove disk |

#### Logical Volumes

| Command | Purpose |
|---------|---------|
| `sudo lvcreate -L 10G -n name vg` | Create LV |
| `sudo lvdisplay` | Show details |
| `sudo lvs` | Short summary |
| `sudo lvextend -L +5G /dev/vg/lv` | Grow LV |
| `sudo lvreduce -L 5G /dev/vg/lv` | Shrink LV |

#### After LVM

| Command | Purpose |
|---------|---------|
| `sudo mkfs.ext4 /dev/vg/lv` | Format |
| `sudo mount /dev/vg/lv /mnt` | Mount |
| `sudo resize2fs /dev/vg/lv` | Resize ext4 |

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
| `pwd` | Shows where you are |
| `ls` | Shows what's here |
| `cd` | Move to another directory |
| `mkdir` | Create directories |
| `rmdir` | Remove empty directories |
| `cp` | Copy files/directories |
| `mv` | Move or rename files |
| `rm` | Delete files (careful!) |
| `touch` | Create empty file |
| `cat` | Show entire file |
| `head` | Show first lines |
| `tail` | Show last lines |
| `less` | Read file page by page |
| `--help` | Quick help |
| `man` | Full manual |
| `info` | Detailed documentation |
| Permissions | Control who can read/write/execute files |
| `chmod` | Change file permissions |
| `chown` | Change file owner |
| `chgrp` | Change file group |
| `ln` | Create hard links |
| `ln -s` | Create soft (symbolic) links |
| `find` | Search files by criteria |
| `locate` | Fast search from database |
| `which` | Find command location |
| `whereis` | Find binary, source, manual |
| `grep` | Search text in files |
| `sed` | Find & replace text |
| `awk` | Column processing |
| `sort` | Sort lines |
| `uniq` | Remove duplicates |
| `cut` | Extract columns |
| `tr` | Translate characters |
| `wc` | Count lines, words, bytes |
| `>` | Redirect output (overwrite) |
| `>>` | Redirect output (append) |
| `<` | Redirect input |
| `\|` | Pipe output to next command |
| `tee` | Split output to screen + file |
| `ps` | Show process status |
| `top` | Real-time process viewer |
| `htop` | Better process viewer |
| `pgrep` | Find process PID by name |
| `kill` | Send signal to process |
| `pkill` | Kill process by name |
| `killall` | Kill process by exact name |
| `&` | Run command in background |
| `jobs` | List background jobs |
| `nohup` | Run process surviving logout |
| `uptime` | Show uptime and load |
| `free -h` | Show memory usage |
| `vmstat` | Virtual memory statistics |
| `iostat` | Disk I/O statistics |
| `apt` | Debian package manager (high-level) |
| `dpkg` | Debian package manager (low-level) |
| `dnf` | Red Hat package manager (high-level) |
| `yum` | Red Hat package manager (older) |
| `rpm` | Red Hat package manager (low-level) |
| `useradd` | Create new user |
| `usermod` | Modify existing user |
| `passwd` | Manage passwords |
| `userdel` | Delete user |
| `groupadd` | Create new group |
| `groupmod` | Modify existing group |
| `groupdel` | Delete group |
| `gpasswd` | Manage group members |
| `sudo` | Run command as root |
| `visudo` | Edit sudoers safely |
| `lsblk` | List block devices |
| `fdisk` | Partition table editor |
| `parted` | Advanced partition manager |
| `mount` | Attach filesystem |
| `umount` | Detach filesystem |
| `mkfs.*` | Format filesystem (ext4/xfs/btrfs) |
| `/etc/fstab` | Auto-mount at boot |
| `pvcreate` | Create physical volume (LVM) |
| `vgcreate` | Create volume group (LVM) |
| `lvcreate` | Create logical volume (LVM) |
| `lvextend` | Grow logical volume |

---

*Last updated: Sep 21, 2025*
