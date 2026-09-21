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

---

*Last updated: Sep 21, 2025*
