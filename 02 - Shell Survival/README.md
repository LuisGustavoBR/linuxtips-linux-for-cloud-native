# Module 2: Shell Survival

## Overview

Working effectively in a Linux environment means being comfortable at the shell: knowing how the filesystem is organized, moving around it quickly, managing files and directories, customizing the terminal, finding what you need, and packing/unpacking data for storage or transfer.

This module builds those skills from the ground up, across seven lessons: the Linux filesystem hierarchy, command-line navigation, file and directory management, terminal shortcuts and Bash configuration, finding files and directories, archiving and compression, and symbolic links, hard links, inodes, and shell productivity.

## Table of Contents

- [Lesson 1: Exploring the Linux Filesystem](#lesson-1-exploring-the-linux-filesystem)
  - [1. Linux Is a Kernel, Not a Complete Operating System](#1-linux-is-a-kernel-not-a-complete-operating-system)
  - [2. What Is a Linux Distribution?](#2-what-is-a-linux-distribution)
  - [3. Why Alpine Linux?](#3-why-alpine-linux)
  - [4. Navigating the Filesystem](#4-navigating-the-filesystem)
  - [5. Special Directory Entries](#5-special-directory-entries)
  - [6. Understanding `ls -l`](#6-understanding-ls--l)
  - [7. Symbolic Links](#7-symbolic-links)
  - [8. Linux File Permissions](#8-linux-file-permissions)
  - [9. The `/bin` Directory](#9-the-bin-directory)
  - [10. BusyBox](#10-busybox)
  - [11. The `/dev` Directory](#11-the-dev-directory)
  - [12. The `/etc` Directory](#12-the-etc-directory)
  - [13. The `/home` Directory](#13-the-home-directory)
  - [14. The `/root` Directory](#14-the-root-directory)
  - [15. The `/lib` Directory](#15-the-lib-directory)
  - [16. The `/media` Directory](#16-the-media-directory)
  - [17. The `/mnt` Directory](#17-the-mnt-directory)
  - [18. The `/opt` Directory](#18-the-opt-directory)
  - [19. The `/proc` Directory](#19-the-proc-directory)
  - [20. The `/run` Directory](#20-the-run-directory)
  - [21. The `/sbin` Directory](#21-the-sbin-directory)
  - [22. The `/sys` Directory](#22-the-sys-directory)
  - [23. The `/tmp` Directory](#23-the-tmp-directory)
  - [24. The `/usr` Directory](#24-the-usr-directory)
  - [25. The `/var` Directory](#25-the-var-directory)
  - [Important Commands from This Lesson](#important-commands-from-this-lesson)
  - [Key Takeaways](#key-takeaways)
- [Lesson 2: Command-Line Navigation](#lesson-2-command-line-navigation)
  - [1. The Linux Shell](#1-the-linux-shell)
  - [2. Navigating Directories](#2-navigating-directories)
  - [3. Absolute Paths](#3-absolute-paths)
  - [4. Relative Paths](#4-relative-paths)
  - [5. Current and Parent Directory References](#5-current-and-parent-directory-references)
  - [6. Combining Relative Paths](#6-combining-relative-paths)
  - [7. Switching to the Previous Directory](#7-switching-to-the-previous-directory)
  - [8. Returning to the Home Directory](#8-returning-to-the-home-directory)
  - [9. Listing Directory Contents](#9-listing-directory-contents)
  - [10. Human-Readable Sizes](#10-human-readable-sizes)
  - [11. Hidden Files](#11-hidden-files)
  - [12. Combining `ls` Options](#12-combining-ls-options)
  - [13. Command History](#13-command-history)
  - [14. Clearing the Terminal](#14-clearing-the-terminal)
  - [15. Tab Completion](#15-tab-completion)
  - [16. Practical Navigation Example](#16-practical-navigation-example)
  - [Important Commands from This Lesson](#important-commands-from-this-lesson-1)
  - [Key Takeaways](#key-takeaways-1)
- [Lesson 3: File and Directory Management](#lesson-3-file-and-directory-management)
  - [1. Creating Directories](#1-creating-directories)
  - [2. Creating Nested Directories](#2-creating-nested-directories)
  - [3. Creating Empty Files](#3-creating-empty-files)
  - [4. Copying Files and Directories](#4-copying-files-and-directories)
  - [5. Moving Files and Directories](#5-moving-files-and-directories)
  - [6. Removing Files and Directories](#6-removing-files-and-directories)
  - [7. Removing Directories Recursively](#7-removing-directories-recursively)
  - [8. The Danger of `rm -rf /`](#8-the-danger-of-rm--rf-)
  - [9. Practice](#9-practice)
  - [Important Commands from This Lesson](#important-commands-from-this-lesson-2)
  - [Key Takeaways](#key-takeaways-2)
- [Lesson 4: Terminal Shortcuts, Aliases, and Bash Configuration](#lesson-4-terminal-shortcuts-aliases-and-bash-configuration)
  - [1. Terminal Shortcuts](#1-terminal-shortcuts)
  - [2. Ctrl + R - Search the Command History](#2-ctrl--r---search-the-command-history)
  - [3. Ctrl + W - Delete a Word](#3-ctrl--w---delete-a-word)
  - [4. Ctrl + U - Delete the Line](#4-ctrl--u---delete-the-line)
  - [5. Ctrl + A and Ctrl + E](#5-ctrl--a-and-ctrl--e)
  - [6. Ctrl + C - Interrupt a Command](#6-ctrl--c---interrupt-a-command)
  - [7. Ctrl + D - Exit the Shell](#7-ctrl--d---exit-the-shell)
  - [8. Aliases](#8-aliases)
  - [9. Viewing Aliases](#9-viewing-aliases)
  - [10. Aliases Are Temporary](#10-aliases-are-temporary)
  - [11. Bash and Its Configuration Files](#11-bash-and-its-configuration-files)
  - [12. `.bash_history`](#12-bash_history)
  - [13. `.bashrc`](#13-bashrc)
  - [14. `.bash_logout`](#14-bash_logout)
  - [15. `echo`](#15-echo)
  - [16. Redirection with `>`](#16-redirection-with-)
  - [17. Redirection with `>>`](#17-redirection-with-)
  - [18. Adding an Alias to `.bashrc`](#18-adding-an-alias-to-bashrc)
  - [19. `cat`](#19-cat)
  - [20. `source`](#20-source)
  - [21. `sudo`](#21-sudo)
  - [22. Why Use `sudo`?](#22-why-use-sudo)
  - [23. Aliases with `sudo`](#23-aliases-with-sudo)
  - [24. Alpine vs Debian](#24-alpine-vs-debian)
  - [25. Practice](#25-practice)
  - [Important Commands from This Lesson](#important-commands-from-this-lesson-3)
  - [Key Takeaways](#key-takeaways-3)
- [Lesson 5: Finding Files and Directories in Linux](#lesson-5-finding-files-and-directories-in-linux)
  - [1. Revisiting Previous Lessons](#1-revisiting-previous-lessons)
  - [2. Metacharacters and Wildcards](#2-metacharacters-and-wildcards)
  - [3. Brace Expansion](#3-brace-expansion)
  - [4. The Asterisk Wildcard](#4-the-asterisk-wildcard)
  - [5. Using `*` with Other Commands](#5-using--with-other-commands)
  - [6. The Question Mark Wildcard](#6-the-question-mark-wildcard)
  - [7. Character Sets with `[ ]`](#7-character-sets-with--)
  - [8. Filename Substitution with Braces](#8-filename-substitution-with-braces)
  - [9. The `find` Command](#9-the-find-command)
  - [10. Searching the Entire Filesystem](#10-searching-the-entire-filesystem)
  - [11. Using Wildcards with `find`](#11-using-wildcards-with-find)
  - [12. Searching by File Type](#12-searching-by-file-type)
  - [13. Understanding File Types](#13-understanding-file-types)
  - [14. Searching by File Size](#14-searching-by-file-size)
  - [15. Searching by Modification Time](#15-searching-by-modification-time)
  - [16. Deleting Files with `find`](#16-deleting-files-with-find)
  - [17. Executing Commands with `find`](#17-executing-commands-with-find)
  - [18. Using `echo` with `find`](#18-using-echo-with-find)
  - [19. `find` vs `-delete`](#19-find-vs--delete)
  - [20. Case Sensitivity](#20-case-sensitivity)
  - [21. Case-Insensitive Search](#21-case-insensitive-search)
  - [22. The `file` Command](#22-the-file-command)
  - [23. Listing a Directory vs the Directory Itself](#23-listing-a-directory-vs-the-directory-itself)
  - [24. The `which` Command](#24-the-which-command)
  - [25. Practical Exercise](#25-practical-exercise)
  - [Important Commands from This Lesson](#important-commands-from-this-lesson-4)
  - [26. Important Wildcards and Metacharacters](#26-important-wildcards-and-metacharacters)
  - [27. `find` Options to Remember](#27-find-options-to-remember)
  - [Lesson Review](#lesson-review)
  - [28. Final Practice Challenge](#28-final-practice-challenge)
  - [Key Takeaways](#key-takeaways-4)
- [Lesson 6: Archiving and Compression](#lesson-6-archiving-and-compression)
  - [1. Archiving vs. Compression](#1-archiving-vs-compression)
  - [2. TAR](#2-tar)
  - [3. Creating a TAR Archive](#3-creating-a-tar-archive)
  - [4. Creating a TAR.GZ Archive](#4-creating-a-targz-archive)
  - [5. TAR File Size](#5-tar-file-size)
  - [6. Listing the Contents of an Archive](#6-listing-the-contents-of-an-archive)
  - [7. Extracting a TAR.GZ Archive](#7-extracting-a-targz-archive)
  - [8. Extracting to a Specific Directory](#8-extracting-to-a-specific-directory)
  - [9. BZIP2 Compression](#9-bzip2-compression)
  - [10. GZIP](#10-gzip)
  - [11. GZIP Compression Levels](#11-gzip-compression-levels)
  - [12. BZIP2](#12-bzip2)
  - [13. Comparing GZIP and BZIP2](#13-comparing-gzip-and-bzip2)
  - [14. Creating Test Files with DD](#14-creating-test-files-with-dd)
  - [15. Testing Compression Performance with TIME](#15-testing-compression-performance-with-time)
  - [16. Backups and Compression](#16-backups-and-compression)
  - [17. Commands to Practice](#17-commands-to-practice)
  - [Important Commands from This Lesson](#important-commands-from-this-lesson-5)
  - [Key Takeaways](#key-takeaways-5)
- [Lesson 7: Symbolic Links, Hard Links, Inodes, and Shell Productivity](#lesson-7-symbolic-links-hard-links-inodes-and-shell-productivity)
  - [1. Quick Review from Lessons 1-3](#1-quick-review-from-lessons-1-3)
  - [2. What Is a Link?](#2-what-is-a-link)
  - [3. Symbolic Links](#3-symbolic-links)
  - [4. Understanding Inodes](#4-understanding-inodes)
  - [5. Why Inodes Matter](#5-why-inodes-matter)
  - [6. Checking Inodes](#6-checking-inodes)
  - [7. Creating a Test File](#7-creating-a-test-file)
  - [8. Creating Large Test Files with `dd`](#8-creating-large-test-files-with-dd)
  - [9. Creating a Test Directory Structure](#9-creating-a-test-directory-structure)
  - [10. Hard Links](#10-hard-links)
  - [11. Creating a Hard Link](#11-creating-a-hard-link)
  - [12. Symbolic Link vs Hard Link](#12-symbolic-link-vs-hard-link)
  - [13. The Main Difference](#13-the-main-difference)
  - [14. Why Hard Links Cannot Cross Filesystems](#14-why-hard-links-cannot-cross-filesystems)
  - [15. What Happens When We Delete a Hard Link?](#15-what-happens-when-we-delete-a-hard-link)
  - [16. Understanding Link Counts](#16-understanding-link-counts)
  - [17. Using `man`](#17-using-man)
  - [18. Symbolic Links in `ls`](#18-symbolic-links-in-ls)
  - [19. Hard Links in `ls`](#19-hard-links-in-ls)
  - [20. Shell Productivity: Tab Completion](#20-shell-productivity-tab-completion)
  - [21. Command History](#21-command-history)
  - [22. Aliases](#22-aliases)
  - [23. Making an Alias Persistent](#23-making-an-alias-persistent)
  - [24. Reloading `.bashrc`](#24-reloading-bashrc)
  - [25. ZSH and Other Shells](#25-zsh-and-other-shells)
  - [Important Commands from This Lesson](#important-commands-from-this-lesson-6)
  - [26. Practice Challenge](#26-practice-challenge)
  - [Key Takeaways](#key-takeaways-6)

---

# Lesson 1: Exploring the Linux Filesystem

Understanding the Linux filesystem hierarchy is one of the most important skills for anyone working with Linux, Cloud, DevOps, or Kubernetes.

In this lesson, you'll explore the purpose of the most important system directories, learn how Linux organizes files, understand symbolic links, executable binaries, device files, and discover how the operating system exposes hardware and kernel information through the filesystem.

---

## 1. Linux Is a Kernel, Not a Complete Operating System

A common misconception is that Linux itself is a complete operating system.

In reality, **Linux is the kernel**—the component responsible for managing hardware resources, processes, memory, networking, and devices.

To become a complete operating system, the Linux kernel is combined with additional software, including:

* GNU utilities (such as `ls`, `cp`, `mv`, and `cat`)
* Shells
* Compilers
* Package managers
* System libraries
* Installation tools

This combination forms what is known as a **Linux distribution**.

---

## 2. What Is a Linux Distribution?

A Linux distribution packages the Linux kernel together with the software required to create a fully functional operating system.

Popular distributions include:

* Debian
* Ubuntu
* Red Hat Enterprise Linux (RHEL)
* Fedora
* Rocky Linux
* AlmaLinux
* Arch Linux
* Alpine Linux

Each distribution targets different use cases, from desktop systems to enterprise servers and cloud-native environments.

---

## 3. Why Alpine Linux?

Throughout this course, many examples use **Alpine Linux**.

Alpine is widely adopted in cloud-native environments because it is:

* Extremely lightweight
* Security-focused
* Fast to boot
* Minimal by design
* Commonly used as a base image for containers

Unlike traditional server distributions, Alpine installs only the components necessary to run applications efficiently, making it ideal for Docker containers and Kubernetes workloads.

---

## 4. Navigating the Filesystem

The following commands are used frequently while exploring the filesystem:

```bash
pwd
ls
ls -l
cd
clear
```

Useful keyboard shortcuts include:

```text
Ctrl + L    Clear the terminal
Tab         Auto-complete commands and paths
```

---

## 5. Special Directory Entries

Every directory contains two special entries:

| Entry | Meaning           |
| ----- | ----------------- |
| `.`   | Current directory |
| `..`  | Parent directory  |

For example:

```bash
cd ..
```

Moves to the parent directory.

```bash
cd .
```

Keeps you in the current directory.

These entries are fundamental to filesystem navigation.

---

## 6. Understanding `ls -l`

The long listing format provides detailed information about files.

Example:

```bash
ls -l
```

Typical output:

```text
lrwxrwxrwx 1 root root ... ls -> /bin/busybox
```

This output includes:

* File type
* Permissions
* Owner
* Group
* File size
* Modification date
* File name

If the file is a symbolic link, the destination is also displayed.

---

## 7. Symbolic Links

A symbolic link is similar to a shortcut in other operating systems.

Example:

```text
ls -> /bin/busybox
```

In this example:

* `ls` is not the actual executable.
* It points to the `busybox` binary.

The first character in the permission field identifies the file type:

| Prefix | File Type        |
| ------ | ---------------- |
| `-`    | Regular file     |
| `d`    | Directory        |
| `l`    | Symbolic link    |
| `c`    | Character device |
| `b`    | Block device     |

---

## 8. Linux File Permissions

A permission string contains ten characters.

Example:

```text
-rwxr-xr-x
```

Structure:

```text
- rwx rwx rwx
│ │   │   │
│ │   │   └── Others
│ │   └────── Group
│ └────────── Owner
└──────────── File type
```

Permission symbols:

| Symbol | Meaning |
| ------ | ------- |
| `r`    | Read    |
| `w`    | Write   |
| `x`    | Execute |

Permission management is covered in detail later in the course.

---

## 9. The `/bin` Directory

The `/bin` directory contains essential executable programs required by all users.

Examples include:

* `ls`
* `cp`
* `mv`
* `cat`
* `echo`

Characteristics:

* System-wide commands
* Available to every user
* Required during system startup

On Alpine Linux, many of these commands are symbolic links pointing to the **BusyBox** executable.

---

## 10. BusyBox

BusyBox is a single executable that provides hundreds of standard Linux utilities.

Instead of installing separate binaries for each command, Alpine uses BusyBox to provide lightweight implementations of common tools.

Benefits include:

* Smaller filesystem footprint
* Lower memory usage
* Faster container images

BusyBox is one of the reasons Alpine images are significantly smaller than most Linux distributions.

---

## 11. The `/dev` Directory

Everything in Linux is represented as a file—including hardware devices.

The `/dev` directory contains device files that allow applications to communicate with hardware.

There are two main device types.

### Character Devices

Character devices transfer data as a continuous stream.

Examples include:

* Terminal devices
* Serial ports
* Network interfaces

Their permission string begins with:

```text
c
```

---

### Block Devices

Block devices store data in fixed-size blocks.

Examples include:

* Hard drives
* SSDs
* USB storage devices

Their permission string begins with:

```text
b
```

---

### Terminal Devices (`tty`)

Linux terminals are also represented as device files.

Examples:

```text
/dev/tty0
/dev/tty1
```

These are **character devices**, since they exchange streams of characters rather than storing data.

---

## 12. The `/etc` Directory

The `/etc` directory stores system-wide configuration files.

Typical examples include:

* Network configuration
* SSH configuration
* Hostname
* User authentication
* System services

For example:

```bash
cat /etc/hostname
```

Displays the system hostname.

The `/etc` directory is one of the most important locations for Linux administration.

---

## 13. The `/home` Directory

Each regular user has a personal home directory under `/home`.

Example:

```text
/home/alice
/home/bob
```

These directories store:

* Personal files
* User-specific configuration
* Shell settings
* SSH keys

The root user's home directory is **not** located here.

---

## 14. The `/root` Directory

The root user's home directory is:

```text
/root
```

This directory is reserved exclusively for the system administrator.

---

## 15. The `/lib` Directory

The `/lib` directory stores shared libraries required by executables.

These libraries serve a similar purpose to DLL files on Windows.

Examples include:

* Shared runtime libraries
* Dynamic loader components
* Kernel modules

Removing essential libraries from this directory can prevent the system from functioning correctly.

---

### Kernel Modules

Kernel modules are typically stored under:

```text
/lib/modules
```

These modules provide support for:

* Network drivers
* Storage devices
* Filesystems
* Hardware controllers

Modules can be loaded dynamically without rebuilding the kernel.

---

## 16. The `/media` Directory

The `/media` directory is commonly used for automatically mounted removable media, such as:

* USB drives
* DVDs
* External storage

Desktop environments typically manage this directory automatically.

---

## 17. The `/mnt` Directory

The `/mnt` directory is intended for temporary mount points created by administrators.

Examples include mounting:

* Remote filesystems
* Additional disks
* Network shares

---

## 18. The `/opt` Directory

Optional third-party software is commonly installed under:

```text
/opt
```

This directory is intended for software that is not managed by the operating system's package manager.

Examples include:

* Commercial software
* Custom applications
* Vendor-provided tools

---

## 19. The `/proc` Directory

The `/proc` directory is a virtual filesystem that exposes real-time kernel and process information.

Its contents are generated dynamically while the system is running.

Examples:

```bash
cat /proc/cpuinfo
```

Displays CPU information.

```bash
cat /proc/meminfo
```

Displays memory statistics.

Unlike regular files, these entries do not permanently exist on disk.

---

### Process Information

Every running process has a corresponding directory inside `/proc`.

Example:

```text
/proc/1
```

Each process directory contains runtime information, including:

* Command line
* Environment variables
* Status
* Memory usage

Example:

```bash
cat /proc/1/cmdline
```

Displays the command used to start process `1`.

---

### Process IDs (PID)

Every running process receives a unique **Process ID (PID)**.

You can list active processes with:

```bash
ps -ef
```

The PID uniquely identifies each running process.

On most Linux systems, process `1` is the system's init process (such as `systemd` or another init implementation), responsible for starting userspace services during boot.

---

## 20. The `/run` Directory

The `/run` directory stores runtime data created while the system is operating.

Typical contents include:

* PID files
* Runtime sockets
* Lock files
* Temporary service information

Its contents are recreated after every reboot.

---

## 21. The `/sbin` Directory

The `/sbin` directory contains system administration binaries.

Examples include commands used for:

* Network configuration
* System shutdown
* Filesystem management
* Service management

These tools are primarily intended for administrative users.

---

## 22. The `/sys` Directory

Like `/proc`, the `/sys` directory is a virtual filesystem.

It exposes information about:

* Devices
* Kernel subsystems
* Drivers
* Hardware
* Kernel parameters

Many system management tools interact directly with this filesystem.

---

## 23. The `/tmp` Directory

The `/tmp` directory stores temporary files.

Applications frequently use this location for:

* Temporary data
* Installation files
* Intermediate processing

Most systems automatically remove its contents after a reboot or periodically through cleanup services.

---

## 24. The `/usr` Directory

The `/usr` hierarchy contains user-space applications, libraries, documentation, and shared resources.

Common subdirectories include:

| Directory    | Purpose                       |
| ------------ | ----------------------------- |
| `/usr/bin`   | User applications             |
| `/usr/sbin`  | Administrative applications   |
| `/usr/lib`   | Shared libraries              |
| `/usr/share` | Architecture-independent data |
| `/usr/local` | Locally installed software    |

Software installed manually is commonly placed under `/usr/local`, keeping it separate from operating system packages.

---

## 25. The `/var` Directory

The `/var` directory stores data that changes frequently during normal system operation.

Examples include:

* Log files
* Package manager data
* Application caches
* Mail queues
* Databases
* Runtime state

One of the most frequently accessed locations is:

```text
/var/log
```

System logs can be viewed using:

```bash
cat /var/log/messages
```

Or monitored in real time:

```bash
tail -f /var/log/messages
```

Log analysis is a fundamental skill for Linux troubleshooting and operations.

## Important Commands from This Lesson

| Command | Purpose |
|---|---|
| `pwd` | Print the current working directory. |
| `ls` / `ls -l` | List directory contents, or in long format with type, permissions, owner, group, size, and date. |
| `cd` / `cd ..` / `cd .` | Change directory; move to the parent directory; stay in the current directory. |
| `clear` | Clear the terminal screen. |
| `cat /etc/hostname` | Display the system's configured hostname. |
| `cat /proc/cpuinfo` | Display CPU information exposed by the kernel. |
| `cat /proc/meminfo` | Display memory statistics exposed by the kernel. |
| `cat /proc/PID/cmdline` | Display the command line used to start a given process. |
| `ps -ef` | List running processes and their PIDs. |
| `cat /var/log/messages` | View the contents of a system log file. |
| `tail -f /var/log/messages` | Follow a system log file in real time. |

---

## Key Takeaways

* Linux distributions combine the Linux kernel with user-space utilities and libraries.
* Alpine Linux is a lightweight distribution widely used for containers and cloud-native workloads.
* The Linux filesystem follows standardized conventions that organize executables, configuration files, libraries, devices, and runtime data.
* `/proc` and `/sys` are virtual filesystems that expose real-time kernel and system information.
* Device files in `/dev` represent hardware and system interfaces.
* Understanding the purpose of each top-level directory is essential for Linux administration, troubleshooting, automation, and platform engineering.

---

# Lesson 2: Command-Line Navigation

## 1. The Linux Shell

The **shell** is a command interpreter that provides an interface between the user and the operating system.

When you type a command such as:

```bash
ls
```

the shell interprets the command and executes it.

The shell is therefore one of the primary interfaces used to interact with a Linux system.

Common Linux shells include:

* `sh`
* `bash`
* `zsh`
* `fish`
* `ksh`

### Bash

**Bash** stands for **Bourne Again Shell**.

It is one of the most widely used shells in Linux environments and provides features such as:

* Command execution
* Command history
* Shell scripting
* Variables
* Pipes
* Redirection
* Command substitution
* Tab completion

### Zsh

**Zsh** is another popular Unix shell with extensive customization and plugin support.

The shell available on a system depends on the distribution and user configuration.

---

## 2. Navigating Directories

The `cd` command is used to change the current working directory.

For example:

```bash
cd /var/log
```

After changing directories, `pwd` can be used to verify the current location:

```bash
pwd
```

Example output:

```text
/var/log
```

The current working directory is important because relative paths are interpreted from this location.

---

## 3. Absolute Paths

An **absolute path** specifies the complete location of a file or directory starting from `/`.

For example:

```bash
cd /var/log
```

This path is valid regardless of the directory you are currently in.

Another example:

```bash
cd /usr/local/bin
```

Absolute paths always start with `/`.

---

## 4. Relative Paths

A **relative path** is interpreted from the current working directory.

Suppose you are currently in:

```text
/var
```

You can enter the `log` directory using:

```bash
cd log
```

There is no need to specify `/var/log` because `log` is being resolved relative to the current directory.

Relative paths are particularly useful when navigating nearby directories.

---

## 5. Current and Parent Directory References

Two special path references are especially important when working with relative paths.

### Current Directory: `.`

The single dot represents the current directory:

```text
.
```

For example:

```bash
cd .
```

does not change the current location.

The `.` reference is also useful when specifying the current directory as part of another command.

---

### Parent Directory: `..`

The double dot represents the parent directory:

```text
..
```

For example:

```bash
cd ..
```

moves one directory level up.

If you are currently in:

```text
/var/log
```

running:

```bash
cd ..
```

takes you to:

```text
/var
```

You can continue moving upward:

```bash
cd ..
```

which takes you to:

```text
/
```

---

## 6. Combining Relative Paths

Relative paths can combine `.` and `..` references.

For example:

```bash
cd ../../etc
```

means:

1. Move to the parent directory.
2. Move to its parent directory.
3. Enter the `etc` directory.

This allows you to navigate through the filesystem without specifying the complete absolute path.

---

## 7. Switching to the Previous Directory

The following command returns to the previously visited directory:

```bash
cd -
```

For example:

```bash
cd /var/log
cd /tmp
cd -
```

The final command switches back to:

```text
/var/log
```

This is useful when working alternately between two locations.

---

## 8. Returning to the Home Directory

Running `cd` without specifying a path returns to the current user's home directory:

```bash
cd
```

This provides a convenient way to return to a known location without typing the full path.

---

## 9. Listing Directory Contents

The `ls` command lists files and directories.

```bash
ls
```

A path can also be provided:

```bash
ls /var/log
```

The `ls` command supports several useful options.

---

### Long Format

Use `-l` to display detailed information:

```bash
ls -l
```

The output includes information such as:

* File type
* Permissions
* Number of links
* Owner
* Group
* Size
* Modification time
* Name

For example:

```text
drwxr-xr-x 2 root root 4096 Aug 7 10:00 logs
```

The first character identifies the file type, while the remaining characters contain permission information.

File permissions will be covered in more detail later.

---

## 10. Human-Readable Sizes

The `-h` option displays file sizes in a human-readable format.

For example:

```bash
ls -lh
```

Instead of displaying only raw byte counts, sizes can be shown using units such as:

```text
KB
MB
GB
TB
```

This option is particularly useful when inspecting files with large sizes.

---

## 11. Hidden Files

Linux uses a simple convention for hidden files: their names begin with a dot.

Examples include:

```text
.bashrc
.bash_history
.profile
```

A standard `ls` command does not display these files:

```bash
ls
```

Use the `-a` option to include hidden files:

```bash
ls -a
```

The `-a` option means **all**, including hidden entries.

---

## 12. Combining `ls` Options

Multiple options can be combined.

For example:

```bash
ls -la
```

displays:

* Detailed information
* Hidden files

You can also combine all three options discussed above:

```bash
ls -lah
```

This provides a detailed listing that includes hidden files and displays sizes in a human-readable format.

This is one of the most useful forms of `ls` when inspecting a directory:

```bash
ls -lah
```

---

## 13. Command History

The shell keeps a history of previously executed commands.

To display the command history:

```bash
history
```

The history can also be accessed interactively using the arrow keys:

* `↑` — previous command
* `↓` — next command

For example, pressing `↑` repeatedly allows you to navigate through commands that were previously executed.

This is useful when repeating or modifying commands without typing them again.

---

## 14. Clearing the Terminal

The `clear` command clears the visible contents of the terminal:

```bash
clear
```

The `Ctrl+L` shortcut commonly provides the same functionality in an interactive shell.

Clearing the terminal does not delete command history or terminate running processes. It only clears the current visible screen.

---

## 15. Tab Completion

The `Tab` key provides command and path completion.

For example, instead of typing:

```bash
cd /var/log
```

you can begin typing:

```bash
cd /var/lo
```

and press `Tab`.

If the path is unambiguous, the shell can automatically complete it:

```bash
cd /var/log
```

Tab completion is useful because it:

* Saves time
* Reduces typing
* Prevents spelling mistakes
* Makes long paths easier to work with

It can also be used to complete commands and filenames.

---

## 16. Practical Navigation Example

Consider the following sequence:

```bash
cd /
ls
cd var
pwd
```

The current directory is now:

```text
/var
```

You can then enter a child directory using a relative path:

```bash
cd log
```

The current directory becomes:

```text
/var/log
```

To return to `/var`:

```bash
cd ..
```

To return to `/`:

```bash
cd ..
```

Alternatively, you could use an absolute path at any point:

```bash
cd /var/log
```

Or return directly to the previous location:

```bash
cd -
```

This demonstrates the difference between absolute and relative navigation.

---

## Important Commands from This Lesson

| Command     | Purpose                                                     |
| ----------- | ---------------------------------------------------------- |
| `cd <path>` | Change the current directory                               |
| `cd`        | Return to the user's home directory                        |
| `cd ..`     | Move to the parent directory                               |
| `cd .`      | Reference the current directory                            |
| `cd -`      | Return to the previous directory                           |
| `pwd`       | Display the current working directory                      |
| `ls`        | List directory contents                                    |
| `ls -l`     | Display detailed file information                          |
| `ls -a`     | Include hidden files                                       |
| `ls -h`     | Display human-readable sizes                               |
| `ls -lh`    | Detailed listing with human-readable sizes                 |
| `ls -lah`   | Detailed listing including hidden files and readable sizes |
| `clear`     | Clear the terminal screen                                  |
| `history`   | Display previously executed commands                       |

---

## Key Takeaways

By the end of this lesson, you should be comfortable with:

* Understanding the role of the Linux shell
* Using `cd` to navigate directories
* Checking your current location with `pwd`
* Using absolute paths
* Using relative paths
* Understanding `.` and `..`
* Moving to the previous directory with `cd -`
* Returning to the home directory with `cd`
* Using `ls` to inspect directories
* Reading detailed `ls -l` output
* Displaying hidden files with `ls -a`
* Using human-readable sizes with `ls -h`
* Combining command-line options
* Using `history`
* Clearing the terminal
* Using Tab completion

The goal of this lesson is not simply to memorize commands. Practice navigating the filesystem from the terminal and use both absolute and relative paths until the behavior becomes intuitive.

---

# Lesson 3: File and Directory Management

## 1. Creating Directories

In Linux, the correct terminology is **directory**, rather than folder.

To create a directory, use the `mkdir` command:

```bash
mkdir <directory>
```

For example:

```bash
mkdir giropops
```

Verify that the directory was created:

```bash
ls
```

Every directory automatically contains two special entries:

* `.` — refers to the current directory.
* `..` — refers to the parent directory.

These references can be used when navigating the filesystem.

---

## 2. Creating Nested Directories

By default, `mkdir` creates only the directory specified in the command. If the parent directory does not exist, the command fails.

For example:

```bash
mkdir products/checkout
```

If `products` does not exist, the command will fail.

Use the `-p` option to create the required parent directories automatically:

```bash
mkdir -p products/checkout
```

This creates the entire directory hierarchy:

```text
products/
└── checkout/
```

The `-p` option is particularly useful when creating multiple levels of a directory structure at once.

---

## 3. Creating Empty Files

The `touch` command can be used to create an empty file:

```bash
touch <filename>
```

For example:

```bash
touch strigos
```

You can also specify a complete path:

```bash
touch giropops/products/checkout/strigos
```

If the file does not exist, `touch` creates an empty file.

A simplified structure would then look like:

```text
giropops/
└── products/
    └── checkout/
        └── strigos
```

---

## 4. Copying Files and Directories

The `cp` command is used to copy files and directories.

### Copying a File

The basic syntax is:

```bash
cp <source> <destination>
```

For example:

```bash
cp giropops/products/checkout/strigos giropops/
```

The original file remains in its original location.

### Copying Directories

To copy a directory and its contents, use the `-R` option:

```bash
cp -R <source> <destination>
```

For example:

```bash
cp -R giropops/products/checkout .
```

The `-R` option means **recursive**. It allows `cp` to traverse the source directory and copy its contents.

The key difference is:

* `cp` — copies files.
* `cp -R` — recursively copies directories and their contents.

---

## 5. Moving Files and Directories

The `mv` command moves files or directories:

```bash
mv <source> <destination>
```

For example:

```bash
mv giropops/products/checkout/strigos .
```

Unlike `cp`, `mv` removes the item from its original location after moving it.

### Renaming Files

`mv` is also used to rename files and directories.

For example:

```bash
mv strigos giros
```

The file previously named `strigos` is now named `giros`.

This works because, in Linux, renaming an item is essentially changing its directory entry rather than using a separate rename command.

---

## 6. Removing Files and Directories

The `rm` command removes files:

```bash
rm <filename>
```

For example:

```bash
rm giros
```

To remove a directory, use `rmdir`:

```bash
rmdir <directory>
```

However, `rmdir` can only remove **empty directories**.

For example:

```bash
rmdir checkout
```

If the directory contains files or subdirectories, the command fails.

---

## 7. Removing Directories Recursively

To remove a directory and everything inside it, use:

```bash
rm -R <directory>
```

The `-R` option means **recursive**.

For example:

```bash
rm -R checkout
```

This recursively removes the directory and its contents.

### Force Removal

The `-f` option means **force**:

```bash
rm -Rf <directory>
```

or:

```bash
rm -rf <directory>
```

This combination is commonly used to recursively remove files and directories without prompting for confirmation.

> **Warning:** `rm -rf` is a potentially destructive command. Always verify the target path before executing it, especially when operating as `root`.

---

## 8. The Danger of `rm -rf /`

The root directory `/` represents the top of the Linux filesystem hierarchy.

Therefore, commands that recursively target `/` can potentially remove the entire filesystem.

For example:

```bash
rm -rf /
```

> **Warning:** This should **never** be executed on a real system.

Modern versions of GNU `rm` normally include safeguards such as `--preserve-root`, which prevents accidental recursive deletion of `/`. However, these protections should not be treated as a substitute for verifying commands before execution.

When working as `root`, destructive commands require particular care because the root user has unrestricted access to the system.

---

## 9. Practice

Practice these commands by creating and manipulating your own directory structure.

For example:

```bash
mkdir -p ~/lab/products/checkout
touch ~/lab/products/checkout/example.txt
cp ~/lab/products/checkout/example.txt ~/lab/
mv ~/lab/example.txt ~/lab/renamed.txt
rm ~/lab/renamed.txt
```

Then create additional directories and files and experiment with copying, moving, renaming, and removing them.

The goal is to become comfortable manipulating the Linux filesystem from the command line.

## Important Commands from This Lesson

| Command    | Purpose                                                 |
| ---------- | ------------------------------------------------------- |
| `mkdir`    | Create a directory                                      |
| `mkdir -p` | Create a directory hierarchy, including missing parents |
| `touch`    | Create an empty file                                    |
| `cp`       | Copy files                                              |
| `cp -R`    | Recursively copy directories                            |
| `mv`       | Move files or directories                               |
| `mv`       | Rename files or directories                             |
| `rm`       | Remove files                                            |
| `rmdir`    | Remove empty directories                                |
| `rm -R`    | Recursively remove directories and their contents       |
| `rm -f`    | Force removal without confirmation                      |
| `rm -rf`   | Recursively and forcibly remove files and directories   |

---

## Key Takeaways

* `mkdir` creates a directory; `mkdir -p` also creates any missing parent directories in one command.
* `touch` creates an empty file (or updates its timestamp if the file already exists).
* `cp` copies a file, leaving the source untouched; `cp -R` recursively copies a directory and everything inside it.
* `mv` moves files or directories, and is also how Linux renames them — renaming is just changing a directory entry, not a separate operation.
* `rm` removes files and `rmdir` removes only empty directories; `rm -R` recursively removes a directory and its contents, and adding `-f` (as in `rm -rf`) forces removal without a confirmation prompt.
* `rm -rf /` would recursively delete the entire filesystem. Modern `rm` ships safeguards like `--preserve-root`, but those should never replace double-checking the target path before running a destructive command, especially as `root`.

---

# Lesson 4: Terminal Shortcuts, Aliases, and Bash Configuration

## 1. Terminal Shortcuts

Now that you already know how to navigate the Linux filesystem and manipulate files and directories, it is time to learn some shortcuts that make working in the terminal much faster.

These shortcuts are used constantly in the daily work of Linux administrators, DevOps engineers, and developers.

---

## 2. Ctrl + R - Search the Command History

`Ctrl + R` allows you to search for commands that were previously executed.

Press:

```text
Ctrl + R
```

The Bash shell enters reverse search mode.

For example, if you previously executed:

```bash
pwd
cd /var/log
ls -lha
```

and then press `Ctrl + R` and start typing:

```text
pwd
```

the terminal will find the corresponding command in the history.

You can press `Ctrl + R` repeatedly to search through previous matches.

This is extremely useful when you have previously executed a long command and do not want to type it again.

---

## 3. Ctrl + W - Delete a Word

`Ctrl + W` removes the word immediately before the current cursor position.

For example:

```bash
cp file.txt /var/tmp/file.txt
```

If the cursor is at the end of the line and you press:

```text
Ctrl + W
```

the last word will be removed.

This is useful for quickly correcting commands without having to delete characters one by one.

---

## 4. Ctrl + U - Delete the Line

`Ctrl + U` removes the content of the command line from the cursor position toward the beginning of the line.

For example:

```bash
cp file.txt /var/tmp/file.txt
```

If you want to remove the command you are currently typing and start over, you can use:

```text
Ctrl + U
```

---

## 5. Ctrl + A and Ctrl + E

Two simple but extremely useful shortcuts are:

### Ctrl + A

Moves the cursor to the beginning of the command line.

```text
Ctrl + A
```

### Ctrl + E

Moves the cursor to the end of the command line.

```text
Ctrl + E
```

These shortcuts are particularly useful when working with long commands.

---

## 6. Ctrl + C - Interrupt a Command

`Ctrl + C` is used to interrupt a command or process currently running in the terminal.

For example, if a command keeps running continuously or takes longer than expected, you can press:

```text
Ctrl + C
```

The process receives an interrupt signal and the terminal normally returns to the shell prompt.

This is one of the shortcuts you will use frequently in your daily work.

---

## 7. Ctrl + D - Exit the Shell

`Ctrl + D` has another important function.

When used at an interactive shell prompt, it sends an EOF (End Of File) indication and normally terminates the current shell session.

For example:

```text
Ctrl + D
```

is a common way to exit a shell session.

It can also be useful when leaving a session started under another user.

---

## 8. Aliases

Now we can introduce a very useful shell feature: aliases.

An alias is essentially a shortcut or alternative name for a command.

Imagine that you frequently use:

```bash
ls -lha
```

You can create an alias called `ll`:

```bash
alias ll='ls -lha'
```

Now you can simply run:

```bash
ll
```

and the shell will execute:

```bash
ls -lha
```

Aliases are commonly used to create shortcuts for long or frequently used commands.

---

## 9. Viewing Aliases

To display the aliases currently configured in your shell session, run:

```bash
alias
```

The shell will display the available aliases.

Some Linux distributions already provide aliases by default.

For example:

```bash
alias ll='ls -lha'
```

or:

```bash
alias ls='ls --color=auto'
```

This explains why the same command may behave slightly differently depending on the Linux distribution or the user's configuration.

---

## 10. Aliases Are Temporary

There is an important characteristic of aliases:

```bash
alias ll='ls -lha'
```

creates the alias only for the current shell session.

If you log out and start a new session, the alias may disappear.

To make the configuration persistent, we need to place it in a shell configuration file.

This is where `.bashrc` becomes important.

---

## 11. Bash and Its Configuration Files

Bash is one of the most commonly used shells on Linux systems.

It uses several files to configure the user's environment.

Some important files include:

```text
.bash_history
.bashrc
.bash_logout
```

Each file has a different purpose.

---

## 12. `.bash_history`

The file:

```text
~/.bash_history
```

is used by Bash to store the command history.

This allows previously executed commands to be retrieved later.

For example, features such as `Ctrl + R` use the command history to find previously executed commands.

---

## 13. `.bashrc`

The file:

```text
~/.bashrc
```

is commonly used to configure an interactive Bash environment.

It can contain:

* aliases
* environment variables
* shell functions
* prompt configuration
* other Bash customizations

For example:

```bash
alias ll='ls -lha'
```

can be placed inside `.bashrc`.

This allows the alias to be loaded again when a new Bash session starts.

---

## 14. `.bash_logout`

The file:

```text
~/.bash_logout
```

can contain commands that should be executed when a Bash login session is terminated.

It can be used to perform specific actions during logout.

---

## 15. `echo`

The `echo` command prints text to the terminal.

For example:

```bash
echo "Hello, Linux!"
```

Output:

```text
Hello, Linux!
```

However, `echo` becomes even more useful when combined with output redirection.

---

## 16. Redirection with `>`

The:

```text
>
```

operator redirects command output to a file.

For example:

```bash
echo "Hello" > file.txt
```

This creates `file.txt` containing:

```text
Hello
```

There is an important detail:

> `>` overwrites the existing content of the file.

For example:

```bash
echo "First line" > file.txt
echo "Second line" > file.txt
```

After these commands, the file will contain only:

```text
Second line
```

The first line was overwritten.

---

## 17. Redirection with `>>`

When you want to append content to the end of a file, use:

```text
>>
```

For example:

```bash
echo "First line" > file.txt
echo "Second line" >> file.txt
```

The file will now contain:

```text
First line
Second line
```

The difference is important:

```text
>   overwrite
>>  append
```

> **Warning:** Be especially careful with this when working with configuration files.

---

## 18. Adding an Alias to `.bashrc`

We can combine everything we have learned so far.

Imagine that we want to permanently add:

```bash
alias ll='ls -lha'
```

to `.bashrc`.

We can use:

```bash
echo "alias ll='ls -lha'" >> ~/.bashrc
```

The `echo` command generates the text and `>>` appends that text to the end of the file.

The alias is now stored in `.bashrc`.

---

## 19. `cat`

The `cat` command can be used to display the contents of a file.

For example:

```bash
cat ~/.bashrc
```

This displays the contents of `.bashrc` in the terminal.

It is useful for checking whether a configuration was actually added to the file.

For example:

```bash
cat ~/.bashrc
```

may show:

```bash
alias ll='ls -lha'
```

---

## 20. `source`

After modifying a configuration file, there is an important detail:

The change has been saved to the file, but the current shell may not have loaded the new configuration yet.

To reload the file without logging out and back in, use:

```bash
source ~/.bashrc
```

An equivalent syntax is:

```bash
. ~/.bashrc
```

`source` reads and executes the contents of the file in the current shell session.

For example:

```bash
echo "alias ll='ls -lha'" >> ~/.bashrc
source ~/.bashrc
```

The alias will now be available in the current session:

```bash
ll
```

---

## 21. `sudo`

Another important Linux concept is `sudo`.

Certain operations require administrative privileges.

The `root` user has elevated privileges and can perform operations that regular users cannot.

`sudo` allows an authorized user to execute a command with administrative privileges.

For example:

```bash
sudo apt update
```

In this case, `apt update` is executed with administrative privileges.

This is different from simply running:

```bash
apt update
```

as a regular user without the required permissions.

---

## 22. Why Use `sudo`?

The main idea is to avoid working as `root` all the time.

Working as `root` increases the risk of accidentally performing destructive operations.

With `sudo`, you request elevated privileges only when they are actually required.

A common workflow is:

```text
regular user
    |
    v
sudo command
    |
    v
command executed with administrative privileges
```

We will explore permissions and `sudo` configuration in more detail later in the training.

---

## 23. Aliases with `sudo`

We can also create aliases that execute commands using `sudo`.

For example:

```bash
alias update='sudo apt update'
```

Now:

```bash
update
```

will be equivalent to:

```bash
sudo apt update
```

This can be convenient for commands that you use frequently.

However, if you want the alias to remain available after logging out, it needs to be configured in `.bashrc`.

---

## 24. Alpine vs Debian

During the training, we may work with different Linux distributions.

For example:

* Alpine Linux
* Debian

The fundamental Linux concepts remain the same, but some implementation details can differ.

One example is the default shell.

Alpine commonly uses the BusyBox `ash` shell, while Debian commonly uses Bash.

This means that certain shell features, aliases, and configuration files may vary depending on the environment.

It is therefore important to understand:

```text
Which Linux distribution am I using?
Which shell am I using?
Which user am I using?
```

These details can affect how certain commands behave.

---

## 25. Practice

Now it is time to put everything into practice.

Test the following shortcuts:

```text
Ctrl + R
Ctrl + W
Ctrl + U
Ctrl + A
Ctrl + E
Ctrl + C
Ctrl + D
```

Then practice aliases:

```bash
alias ll='ls -lha'
alias
ll
```

Create a test file:

```bash
echo "First line" > test.txt
```

Append another line:

```bash
echo "Second line" >> test.txt
```

Check the result:

```bash
cat test.txt
```

Then practice Bash configuration:

```bash
echo "alias test='echo It works!'" >> ~/.bashrc
source ~/.bashrc
```

Run:

```bash
test
```

The goal of this lesson is not simply to memorize commands.

You should start using these features naturally while working in the terminal.

---

## Important Commands from This Lesson

| Resource        | Purpose                                         |
| --------------- | ----------------------------------------------- |
| `Ctrl + R`      | Search the command history                      |
| `Ctrl + W`      | Delete a word                                   |
| `Ctrl + U`      | Delete the command line                         |
| `Ctrl + A`      | Move to the beginning of the line               |
| `Ctrl + E`      | Move to the end of the line                     |
| `Ctrl + C`      | Interrupt a running command                     |
| `Ctrl + D`      | Exit the shell/session                          |
| `alias`         | Create command shortcuts                        |
| `.bash_history` | Store Bash command history                      |
| `.bashrc`       | Configure the Bash environment                  |
| `.bash_logout`  | Configure actions performed during logout       |
| `echo`          | Print text                                      |
| `>`             | Redirect output and overwrite                   |
| `>>`            | Redirect output and append                      |
| `cat`           | Display file contents                           |
| `source`        | Reload a configuration file                     |
| `sudo`          | Execute commands with administrative privileges |

---

## Key Takeaways

* Bash's line-editing shortcuts speed up terminal work: `Ctrl + R` searches command history, `Ctrl + W`/`Ctrl + U` delete a word/the whole line, `Ctrl + A`/`Ctrl + E` jump to the start/end of the line, `Ctrl + C` interrupts a running command, and `Ctrl + D` sends EOF to exit the shell.
* An `alias` is a shortcut for a longer command, but it only lasts for the current shell session unless it is added to a startup file such as `.bashrc`.
* `~/.bashrc` configures an interactive Bash session (aliases, environment variables, functions, prompt); `~/.bash_history` stores previously executed commands; `~/.bash_logout` runs commands when a login session ends.
* After editing `.bashrc`, run `source ~/.bashrc` (or the equivalent `. ~/.bashrc`) to reload it into the current session without logging out and back in.
* `sudo` lets an authorized user run a single command with administrative privileges, avoiding the risks of working as `root` all the time; aliases can also wrap `sudo` commands, e.g. `alias update='sudo apt update'`.
* Distribution, default shell, and current user can all affect available features and configuration file behavior — for example, Alpine's default `ash` shell differs from Debian's Bash.

---

# Lesson 5: Finding Files and Directories in Linux

In this lesson, we will learn how to locate files and directories in Linux.

We will also start working with an important Shell concept:

* Metacharacters
* Wildcards
* The `find` command
* File types
* File sizes
* File modification times
* Executing commands with `find`
* Case-sensitive and case-insensitive searches
* The `which` command
* The `file` command

These concepts are extremely useful in day-to-day Linux administration.

Before starting, open your terminal and practice the commands yourself. Do not just read the examples. Type them and observe the results.

---

## 1. Revisiting Previous Lessons

Before moving forward, let's review some concepts from the previous lessons.

### Lesson 1 - Basic Linux Navigation

We learned commands such as:

```bash
pwd
ls
cd
```

* `pwd` shows the current directory.
* `ls` lists files and directories.
* `cd` changes the current directory.

We also learned that Linux has a hierarchical filesystem.

For example:

```text
/
├── etc
├── home
├── var
├── tmp
└── usr
```

The `/` directory is the root of the filesystem.

---

### Lesson 2 - Working with Files and Directories

We learned how to create, copy, move, and remove files and directories.

Common commands:

```bash
touch file.txt
mkdir project
cp file.txt backup.txt
mv file.txt /tmp/
rm file.txt
rm -r project
```

We also learned that Linux treats files and directories differently and that commands can operate on multiple files at once.

---

### Lesson 3 - File and Directory Information

We learned how to inspect files and directories using commands such as:

```bash
ls -l
ls -la
cat
```

The `ls -l` output also introduced us to file types.

For example:

```text
drwxr-xr-x
-rw-r--r--
```

The first character identifies the type:

```text
d = directory
- = regular file
c = character device
b = block device
```

This will become important later in this lesson.

---

### Lesson 4 - Shell Shortcuts and Aliases

We learned several useful terminal shortcuts:

```text
Ctrl + L    Clear the terminal
Ctrl + R    Search command history
Ctrl + W    Delete a word
Ctrl + U    Delete from cursor to beginning
Ctrl + A    Go to beginning of line
Ctrl + E    Go to end of line
Ctrl + C    Cancel a running command
Ctrl + D    Exit/logout
```

We also learned about aliases:

```bash
alias ll='ls -la'
```

And persistent Bash configuration using:

```bash
~/.bashrc
```

After modifying `.bashrc`, we can reload it with:

```bash
source ~/.bashrc
```

These concepts will help us work more efficiently while practicing the commands in this lesson.

---

## 2. Metacharacters and Wildcards

One of the most useful Shell features is the ability to use special characters to represent patterns.

These are commonly called wildcards.

Some important ones are:

```text
*       One or more characters
?       Exactly one character
[ ]     A set or range of characters
{ }     Brace expansion
```

These characters allow us to work with many files without specifying every filename manually.

---

## 3. Brace Expansion

Let's create a directory for our experiments:

```bash
mkdir projects
cd projects
```

Suppose we want to create three files:

```text
arc-1.txt
arc-2.txt
arc-3.txt
```

We could create them individually:

```bash
touch arc-1.txt
touch arc-2.txt
touch arc-3.txt
```

But this is unnecessary.

We can use brace expansion:

```bash
touch arc-{1,2,3}.txt
```

Check the result:

```bash
ls
```

You should see:

```text
arc-1.txt
arc-2.txt
arc-3.txt
```

Brace expansion can also generate ranges.

For example:

```bash
touch arc-{10..20}.txt
```

This creates:

```text
arc-10.txt
arc-11.txt
arc-12.txt
...
arc-20.txt
```

This is very useful when creating multiple files or directories with similar names.

---

## 4. The Asterisk Wildcard

The `*` wildcard represents zero or more characters.

For example:

```bash
ls /etc/*.conf
```

This means:

> List every file in `/etc` whose name ends with `.conf`.

You can also use it with `cp`.

For example:

```bash
mkdir conf
cp /etc/*.conf conf/
```

Now:

```bash
ls conf
```

will show the configuration files that matched the pattern.

The important idea is:

```text
*.conf
```

means:

```text
anything.conf
```

The `*` can represent multiple characters.

For example:

```text
a.conf
test.conf
network.conf
my-long-configuration.conf
```

All of them can match:

```bash
*.conf
```

---

## 5. Using `*` with Other Commands

Wildcards are not exclusive to `ls`.

They can be used with many commands.

For example:

```bash
rm *
```

This removes all files in the current directory.

Be extremely careful with commands such as:

```bash
rm -rf *
```

> **Warning:** This can remove a large amount of data very quickly. Always verify what a wildcard matches before performing destructive operations.

A good habit is:

```bash
ls *.txt
```

before:

```bash
rm *.txt
```

---

## 6. The Question Mark Wildcard

The `?` wildcard represents exactly one character.

Let's create some files:

```bash
mkdir giropops
cd giropops
touch arc-{1..20}.txt
```

Now:

```bash
ls arc-?.txt
```

The `?` represents exactly one character.

Therefore, it matches:

```text
arc-1.txt
arc-2.txt
...
arc-9.txt
```

But it does not match:

```text
arc-10.txt
arc-11.txt
```

because those filenames contain two characters after `arc-`.

To match files from `10` to `20`, we can use:

```bash
ls arc-??.txt
```

Now `??` represents exactly two characters.

Therefore:

```text
arc-10.txt
arc-11.txt
...
arc-20.txt
```

will match.

---

## 7. Character Sets with `[ ]`

Square brackets allow us to specify a set or range of characters.

For example:

```bash
ls arc-[1-5].txt
```

This matches:

```text
arc-1.txt
arc-2.txt
arc-3.txt
arc-4.txt
arc-5.txt
```

We can also explicitly list characters:

```bash
ls arc-[123].txt
```

This matches:

```text
arc-1.txt
arc-2.txt
arc-3.txt
```

The important difference is:

```text
?       Exactly one arbitrary character
[123]   Exactly one character from the specified set
[1-5]   Exactly one character from the specified range
```

---

## 8. Filename Substitution with Braces

Shell expansion can also be useful when creating alternative filenames.

For example:

```bash
touch file.txt
```

We can create a backup using:

```bash
cp file.txt{,.bak}
```

This expands to:

```bash
cp file.txt file.txt.bak
```

The comma-separated empty value means that the original filename is reused.

This is a useful Shell trick for quickly creating backups.

---

## 9. The `find` Command

Now we get to one of the most important commands in this lesson:

```bash
find
```

The `find` command searches for files and directories.

Its basic structure is:

```bash
find <directory> <criteria>
```

For example:

```bash
find /etc -name "motd"
```

This tells Linux:

> Search inside `/etc` for something named `motd`.

The result might be:

```text
/etc/motd
```

---

## 10. Searching the Entire Filesystem

The `/` directory represents the entire filesystem.

Therefore:

```bash
find / -name "arc-10.txt"
```

means:

> Search the entire filesystem for a file named `arc-10.txt`.

Depending on the system, this may take some time.

If a command is taking too long or producing too much output, remember the shortcut from Lesson 4:

```text
Ctrl + C
```

This cancels the running command.

---

## 11. Using Wildcards with `find`

We can also use wildcards with `find`.

For example:

```bash
find / -name "arc-*.txt"
```

This searches for filenames that:

* Start with `arc-`
* Have any number of characters after that
* End with `.txt`

Another example:

```bash
find / -name "arc-?.txt"
```

Here `?` represents exactly one character.

When using wildcards with `find`, it is generally best to quote the pattern:

```bash
find / -name "arc-*.txt"
```

instead of:

```bash
find / -name arc-*.txt
```

The quotes prevent the current Shell from expanding the wildcard before `find` receives it.

This is an important distinction.

---

## 12. Searching by File Type

`find` can search for specific types of filesystem objects.

The main option is:

```bash
-type
```

For example:

```bash
find / -name "giropops"
```

could return both:

```text
/giropops
/estrigos/giropops
```

One could be a directory and the other could be a regular file.

To search only for directories:

```bash
find / -type d -name "giropops"
```

To search only for regular files:

```bash
find / -type f -name "giropops"
```

Common file types include:

```text
f = regular file
d = directory
c = character device
b = block device
```

---

## 13. Understanding File Types

We can verify file types with:

```bash
ls -l
```

For example:

```text
drwxr-xr-x  giropops
-rw-r--r--  giropops.txt
```

The first character tells us the type.

```text
d
```

means directory.

```text
-
```

means regular file.

This connects directly with what we learned in previous lessons.

---

## 14. Searching by File Size

`find` can also search based on file size.

For example:

```bash
find / -type f -size 10k
```

This searches for files with a size matching the specified value.

You can also use:

```bash
find / -type f -size +10k
```

The `+` means:

> Greater than 10 KB.

And:

```bash
find / -type f -size -10k
```

means:

> Smaller than 10 KB.

This is extremely useful when troubleshooting disk usage.

---

## 15. Searching by Modification Time

Another useful `find` option is:

```bash
-mtime
```

It searches based on the number of days since a file was modified.

For example:

```bash
find / -type f -mtime +20
```

means:

> Find regular files modified more than 20 days ago.

You can also search for files modified recently:

```bash
find / -type f -mtime -1
```

This means:

> Find regular files modified within the last day.

There are related options as well:

```text
-mtime    Modification time in days
-mmin     Modification time in minutes
-ctime    Change time
-atime    Access time
```

These options become very useful when investigating logs, backups, temporary files, and old data.

---

## 16. Deleting Files with `find`

`find` can also execute actions on the files it finds.

For example:

```bash
find / -type f -name "giropops" -delete
```

This searches for matching files and deletes them.

> **Warning:** Be extremely careful with `-delete`. The command does not ask for confirmation. If the search pattern is wrong, you can delete the wrong files.

For this reason, it is usually safer to test the search first:

```bash
find / -type f -name "giropops"
```

> **Warning:** Only after confirming the results should you consider a destructive action.

---

## 17. Executing Commands with `find`

A safer and more flexible option is `-exec`.

For example:

```bash
find / -type f -name "giropops" -exec ls -la {} \;
```

This means:

1. Search for the specified files.
2. Find a matching file.
3. Execute `ls -la` on that file.

The special placeholder:

```text
{}
```

represents the file found by `find`.

The command ends with:

```text
\;
```

The syntax is important.

For example:

```bash
-exec ls -la {} \;
```

The backslash prevents the Shell from interpreting the semicolon before `find` can use it.

---

## 18. Using `echo` with `find`

We can also use `echo` to produce custom output.

For example:

```bash
find / -name "giropops" -exec echo "Found: {}" \;
```

The result can look like:

```text
Found: /estrigos/giropops
```

This is useful when building scripts or creating more readable output.

---

## 19. `find` vs `-delete`

The difference is important.

Using:

```bash
find / -name "giropops" -delete
```

directly deletes the matching files.

Using:

```bash
find / -name "giropops" -exec ls -la {} \;
```

allows us to inspect what was found.

A good operational habit is:

```text
Search first
Inspect the results
Then perform the action
```

> **Warning:** Do not start with destructive commands.

---

## 20. Case Sensitivity

Linux is case-sensitive.

These are different names:

```text
giropops
Giropops
GIROPOPS
```

For example:

```bash
find / -name "giropops"
```

will not normally match:

```text
Giropops
```

because the capitalization is different.

---

## 21. Case-Insensitive Search

For a case-insensitive search, we can use:

```bash
-iname
```

For example:

```bash
find / -iname "giropops"
```

This can match:

```text
giropops
Giropops
GIROPOPS
```

The important difference is:

```text
-name     Case-sensitive
-iname    Case-insensitive
```

---

## 22. The `file` Command

Another useful command is:

```bash
file
```

It identifies the type of a file.

For example:

```bash
file somefile
```

It can tell you whether something is:

* A text file
* A binary executable
* A directory
* An image
* An archive
* Another recognized file format

This is useful when the filename or extension does not tell you what the file actually contains.

---

## 23. Listing a Directory vs the Directory Itself

There is an important difference between:

```bash
ls giropops
```

and:

```bash
ls -ld giropops
```

The first command lists the contents of the directory.

The second displays information about the directory itself.

For example:

```bash
ls giropops
```

might show:

```text
file1.txt
file2.txt
file3.txt
```

While:

```bash
ls -ld giropops
```

might show:

```text
drwxr-xr-x  giropops
```

The `-d` option tells `ls` to operate on the directory itself instead of listing its contents.

---

## 24. The `which` Command

Another useful command for locating programs is:

```bash
which
```

For example:

```bash
which vi
```

This can return something like:

```text
/usr/bin/vi
```

This tells you where the executable being used by your Shell is located.

For example:

```bash
which ls
```

might return:

```text
/usr/bin/ls
```

This is useful when troubleshooting PATH issues or determining which executable is actually being used.

---

## 25. Practical Exercise

Create a practice environment:

```bash
mkdir -p ~/giropops
cd ~/giropops
```

Create several files:

```bash
touch arc-{1..20}.txt
touch giropops
touch Giropops
touch GIROPOPS
```

Now practice the following.

### List all files

```bash
ls
```

### List files from 1 to 9

```bash
ls arc-?.txt
```

### List files from 10 to 20

```bash
ls arc-??.txt
```

### List files from 1 to 5

```bash
ls arc-[1-5].txt
```

### Find a specific file

```bash
find . -name "arc-10.txt"
```

### Find all `.txt` files

```bash
find . -name "*.txt"
```

### Find only regular files

```bash
find . -type f
```

### Find only directories

```bash
find . -type d
```

### Case-sensitive search

```bash
find . -name "giropops"
```

### Case-insensitive search

```bash
find . -iname "giropops"
```

### Find files larger than 1 KB

```bash
find . -type f -size +1k
```

### Find recently modified files

```bash
find . -type f -mtime -1
```

### Execute `ls -la` on matching files

```bash
find . -type f -name "*.txt" -exec ls -la {} \;
```

---

## Important Commands from This Lesson

| Command  | Purpose                                   |
| -------- | ----------------------------------------- |
| `ls`     | List files and directories                |
| `mkdir`  | Create directories                        |
| `touch`  | Create files                              |
| `cp`     | Copy files                                |
| `rm`     | Remove files                              |
| `find`   | Search for files and directories          |
| `file`   | Identify file type                        |
| `which`  | Locate an executable                      |
| `ls -ld` | Show information about a directory itself |

---

## 26. Important Wildcards and Metacharacters

| Pattern   | Meaning                              |
| --------- | ------------------------------------ |
| `*`       | Zero or more characters              |
| `?`       | Exactly one character                |
| `[abc]`   | One character from the specified set |
| `[1-5]`   | One character from a range           |
| `{1,2,3}` | Brace expansion                      |
| `{1..10}` | Range expansion                      |

Examples:

```bash
*.txt
arc-?.txt
arc-[1-5].txt
file-{1,2,3}.txt
file-{1..10}.txt
```

---

## 27. `find` Options to Remember

These are the options you should become comfortable with:

```text
-name       Search by name
-iname      Search by name ignoring case
-type       Search by file type
-size       Search by file size
-mtime      Search by modification time in days
-mmin       Search by modification time in minutes
-exec       Execute a command on the result
-delete     Delete matching results
```

Common file types:

```text
f = regular file
d = directory
c = character device
b = block device
```

---

## Lesson Review

At this point, you should understand how Linux can work with groups of files using Shell expansion and how `find` can locate files based on different criteria.

The most important concepts are:

### Wildcards

```bash
*
?
[ ]
```

They allow us to work with groups of files using patterns.

### Brace expansion

```bash
touch file-{1..10}.txt
```

It allows us to generate multiple filenames quickly.

### `find`

```bash
find / -name "file.txt"
```

It searches the filesystem.

### File types

```bash
find / -type f
find / -type d
```

It allows us to distinguish regular files from directories.

### File size

```bash
find / -type f -size +10k
```

It allows us to search based on size.

### Modification time

```bash
find / -type f -mtime -1
```

It allows us to find recently modified files.

### Command execution

```bash
find / -name "*.log" -exec ls -la {} \;
```

It allows us to execute commands against search results.

### Case sensitivity

```bash
find / -name "giropops"
find / -iname "giropops"
```

Linux distinguishes uppercase and lowercase characters.

### Binary location

```bash
which ls
which vi
```

It helps identify where an executable is located.

---

## 28. Final Practice Challenge

Do not just read this section. Open the terminal and complete it.

1. Create a directory called `practice`.
2. Enter the directory.
3. Create 20 files named `file-1.txt` through `file-20.txt`.
4. List only files from `file-1.txt` through `file-9.txt`.
5. List only files from `file-10.txt` through `file-20.txt`.
6. Create three files with different capitalization of the same name.
7. Use `find -name` to search for them.
8. Use `find -iname` to search for them again.
9. Search for only regular files.
10. Search for files larger than 1 KB.
11. Search for files modified within the last 24 hours.
12. Use `-exec` to run `ls -la` against the files you find.
13. Use `which` to locate `ls`.
14. Use `file` to identify one of your files.

The goal is not to memorize every option immediately.

The goal is to understand how the Shell interprets patterns and how `find` can combine a search location, criteria, and an action.

Practice these commands until they become natural.

---

## Key Takeaways

Remember these concepts:

```text
*       Multiple characters
?       One character
[ ]     Character set or range
{ }     Brace expansion

find    Search for files and directories
-name   Search by name
-iname  Search ignoring case
-type   Search by object type
-size   Search by size
-mtime  Search by modification time
-exec   Execute a command on results
-delete Delete results - use with caution

which   Locate executables
file    Identify file types
```

The most important lesson is this:

> Learn to search first, inspect the results, and only then perform potentially destructive actions.

This mindset will become increasingly important as you work with Linux servers, automation, DevOps, and production environments.

---

# Lesson 6: Archiving and Compression

## 1. Archiving vs. Compression

In Linux, it is important to understand the difference between **archiving** and **compression**.

### Archiving

Archiving means putting multiple files and directories into a single package without necessarily reducing their size.

For example:

```bash
tar
```

A tar archive can contain an entire directory structure while preserving the files inside it.

### Compression

Compression reduces the amount of disk space required to store data.

Common compression formats in Linux include:

* GZIP - `.gz`
* BZIP2 - `.bz2`

These concepts are often combined:

```text
Archive + Compression = .tar.gz
Archive + Compression = .tar.bz2
```

---

## 2. TAR

`tar` is one of the most important commands for working with archives in Linux.

It can be used to:

* Create archives
* Extract archives
* List archive contents
* Combine archiving with compression

A common TAR syntax is:

```bash
tar [options] archive_name files
```

Some options are especially important and should be memorized.

| Option | Meaning                  |
| ------ | ------------------------ |
| `c`    | Create an archive        |
| `x`    | Extract an archive       |
| `t`    | List archive contents    |
| `v`    | Verbose output           |
| `f`    | Specify the archive file |
| `z`    | Use GZIP compression     |
| `j`    | Use BZIP2 compression    |

---

## 3. Creating a TAR Archive

Suppose we have a project with the following structure:

```text
project/
├── backend/
├── frontend/
└── infra/
    └── iac/
```

To create a regular TAR archive:

```bash
tar -cvf backup.tar project/
```

The options mean:

* `c` - create
* `v` - verbose
* `f` - specify the output file

The result is:

```text
backup.tar
```

This archive is **not compressed**.

It simply packages the files into a single archive.

---

## 4. Creating a TAR.GZ Archive

To create an archive compressed with GZIP:

```bash
tar -czvf backup.tar.gz project/
```

The important difference is the `z` option:

```text
c = create
z = GZIP compression
v = verbose
f = file
```

The result is:

```text
backup.tar.gz
```

This means:

```text
project/
    ↓
TAR archive
    ↓
GZIP compression
    ↓
backup.tar.gz
```

The `.tar` part represents the archive, while `.gz` represents the compression.

---

## 5. TAR File Size

A TAR archive without compression can be significantly larger than a compressed TAR archive.

For example:

```text
backup.tar      -> archive only
backup.tar.gz   -> archive + GZIP compression
```

The exact difference depends on the data being compressed.

Some files compress very well, while others are already compressed and may not become significantly smaller.

---

## 6. Listing the Contents of an Archive

The `t` option lists the contents of a TAR archive without extracting it.

For a regular TAR archive:

```bash
tar -tvf backup.tar
```

For a GZIP-compressed TAR archive:

```bash
tar -tzvf backup.tar.gz
```

The important option here is:

```text
t = list contents
```

This is useful when you want to inspect an archive before extracting it.

---

## 7. Extracting a TAR.GZ Archive

To extract a GZIP-compressed TAR archive:

```bash
tar -xzvf backup.tar.gz
```

The options mean:

```text
x = extract
z = GZIP
v = verbose
f = file
```

The archive contents will be extracted into the current directory.

---

## 8. Extracting to a Specific Directory

You can specify where the archive should be extracted.

For example:

```bash
tar -xzvf backup.tar.gz -C backup/
```

The `-C` option changes the destination directory for the extraction.

This is useful when you don't want to extract everything into the current directory.

---

## 9. BZIP2 Compression

Another common compression algorithm is **BZIP2**.

With TAR, BZIP2 compression is enabled using:

```bash
j
```

For example:

```bash
tar -cjvf backup.tar.bz2 project/
```

Here:

```text
c = create
j = BZIP2 compression
v = verbose
f = file
```

To list its contents:

```bash
tar -tjvf backup.tar.bz2
```

To extract it:

```bash
tar -xjvf backup.tar.bz2
```

---

## 10. GZIP

GZIP can also be used independently of TAR.

To compress a file:

```bash
gzip file
```

For example:

```bash
gzip giropops
```

The result will be:

```text
giropops.gz
```

The original uncompressed file is replaced by the compressed version.

To decompress it:

```bash
gzip -d giropops.gz
```

The `-d` option means:

```text
d = decompress
```

The original file is restored.

---

## 11. GZIP Compression Levels

GZIP supports different compression levels.

The levels range from:

```text
1 - fastest compression
9 - maximum compression
```

For example:

```bash
gzip -1 file
```

or:

```bash
gzip -9 file
```

Higher compression levels generally require more CPU time.

This creates an important trade-off:

```text
Higher compression
        ↓
Smaller file
        ↓
More processing time
```

The best option depends on the use case.

---

## 12. BZIP2

BZIP2 can also be used independently.

To compress a file:

```bash
bzip2 file
```

For example:

```bash
bzip2 giropops
```

The result is:

```text
giropops.bz2
```

To decompress it:

```bash
bzip2 -d giropops.bz2
```

BZIP2 can provide good compression ratios, but it may require more processing time than GZIP.

---

## 13. Comparing GZIP and BZIP2

The choice between compression algorithms depends on the situation.

| Tool        | Extension  | General characteristic               |
| ----------- | ---------- | ------------------------------------ |
| GZIP        | `.gz`      | Fast and widely used                 |
| BZIP2       | `.bz2`     | Good compression, potentially slower |
| TAR         | `.tar`     | Archiving, not compression           |
| TAR + GZIP  | `.tar.gz`  | Very common Linux archive            |
| TAR + BZIP2 | `.tar.bz2` | Good compression, potentially slower |

A very common Linux format is:

```text
.tar.gz
```

You will encounter it frequently when downloading source code, distributing software, creating backups, and working with Linux systems.

---

## 14. Creating Test Files with DD

The `dd` command can be used for many advanced operations in Linux.

For now, we can use it to create a file with a specific size.

Example:

```bash
dd if=/dev/zero of=giropops bs=1M count=5
```

The parameters mean:

| Parameter | Meaning          |
| --------- | ---------------- |
| `if`      | Input file       |
| `of`      | Output file      |
| `bs`      | Block size       |
| `count`   | Number of blocks |

In this example:

```text
Input:       /dev/zero
Output:      giropops
Block size:  1 MB
Count:       5
```

Therefore, the resulting file will be approximately:

```text
5 MB
```

`/dev/zero` provides a continuous stream of zero bytes, which makes it useful for generating test data.

This is particularly useful when you need a file with a known size to test compression, storage, or performance.

---

## 15. Testing Compression Performance with TIME

Linux provides the `time` command to measure how long a command takes to execute.

For example:

```bash
time gzip giropops
```

The command executes `gzip` and reports timing information.

You can use the same approach with BZIP2:

```bash
time bzip2 giropops
```

This allows you to compare the performance of different compression algorithms.

For example:

```text
GZIP
    ↓
Fast compression

BZIP2
    ↓
Potentially better compression
    ↓
Potentially more processing time
```

The actual results depend heavily on the type and size of the data.

---

## 16. Backups and Compression

Compression is not always the best choice for every backup scenario.

When designing a backup strategy, you need to consider:

* Storage space
* CPU usage
* Backup duration
* Restore duration
* Network transfer time
* Data type

For example, if restoring a backup quickly is more important than saving disk space, aggressive compression may not be desirable.

The important principle is:

```text
Compression is a trade-off between
storage efficiency and processing time.
```

---

## 17. Commands to Practice

Create a test directory:

```bash
mkdir project
```

Create some files:

```bash
touch project/file1
touch project/file2
touch project/file3
```

Create a TAR archive:

```bash
tar -cvf project.tar project/
```

Create a TAR.GZ archive:

```bash
tar -czvf project.tar.gz project/
```

List the contents:

```bash
tar -tvf project.tar
```

List the contents of the compressed archive:

```bash
tar -tzvf project.tar.gz
```

Extract the TAR archive:

```bash
tar -xvf project.tar
```

Extract the TAR.GZ archive:

```bash
tar -xzvf project.tar.gz
```

Create a test file:

```bash
dd if=/dev/zero of=testfile bs=1M count=10
```

Compress it with GZIP:

```bash
gzip testfile
```

Decompress it:

```bash
gzip -d testfile.gz
```

Compress it with BZIP2:

```bash
bzip2 testfile
```

Decompress it:

```bash
bzip2 -d testfile.bz2
```

Measure compression time:

```bash
time gzip testfile
```

---

## Important Commands from This Lesson

| Command | Purpose |
| --- | --- |
| `tar -cvf archive.tar dir/` | Create an uncompressed TAR archive |
| `tar -czvf archive.tar.gz dir/` | Create a GZIP-compressed TAR archive |
| `tar -cjvf archive.tar.bz2 dir/` | Create a BZIP2-compressed TAR archive |
| `tar -tvf archive.tar` / `tar -tzvf archive.tar.gz` | List archive contents without extracting |
| `tar -xzvf archive.tar.gz` | Extract a GZIP-compressed TAR archive |
| `tar -xzvf archive.tar.gz -C dir/` | Extract an archive into a specific directory |
| `gzip file` / `gzip -d file.gz` | Compress / decompress a file with GZIP |
| `gzip -1` ... `gzip -9` | Set the GZIP compression level (fastest to smallest) |
| `bzip2 file` / `bzip2 -d file.bz2` | Compress / decompress a file with BZIP2 |
| `dd if=/dev/zero of=file bs=1M count=N` | Create a test file of a specific size |
| `time command` | Measure how long a command takes to run |

---

## Key Takeaways

By the end of this lesson, you should understand:

* The difference between **archiving** and **compression**
* What `tar` does
* How to create a `.tar` archive
* How to create a `.tar.gz` archive
* How to create a `.tar.bz2` archive
* How to list archive contents
* How to extract archives
* What GZIP and BZIP2 are
* How to compress and decompress files directly
* How compression levels affect performance
* How `dd` can create test files
* How `time` can measure command execution time

The most important TAR options to memorize are:

```text
c = create
x = extract
t = list
v = verbose
f = file
z = GZIP
j = BZIP2
```

A useful way to remember the most common commands is:

```bash
tar -czvf backup.tar.gz project/
tar -tzvf backup.tar.gz
tar -xzvf backup.tar.gz
```

These three commands cover the basic workflow:

```text
Create
  ↓
Inspect
  ↓
Extract
```

---

# Lesson 7: Symbolic Links, Hard Links, Inodes, and Shell Productivity

In this lesson, we will continue building our Linux shell skills and learn an important filesystem concept:

* Symbolic links
* Hard links
* Inodes
* How Linux identifies files internally
* How to inspect inode numbers
* How to create symbolic and hard links
* Important limitations of hard links
* The `man` command
* More shell productivity techniques
* Persistent aliases
* Tab completion and command history

These concepts are very common in Linux administration, DevOps, Cloud, and troubleshooting.

---

## 1. Quick Review from Lessons 1-3

Before continuing, let's review some commands and concepts we have already learned.

### `ls`

Lists files and directories.

```bash
ls
```

Detailed listing:

```bash
ls -l
```

Show hidden files:

```bash
ls -la
```

Show inode numbers:

```bash
ls -li
```

The `-i` option displays the inode number of each file.

---

### `mkdir`

Creates directories.

```bash
mkdir project
```

Create parent directories when necessary:

```bash
mkdir -p etc/conf
```

---

### `touch`

Creates an empty file.

```bash
touch file.txt
```

---

### `mv`

Moves or renames files and directories.

```bash
mv file.txt /tmp/
```

---

### `rm`

Removes files.

```bash
rm file.txt
```

Be careful with commands such as:

```bash
rm -rf
```

> **Warning:** They can recursively remove files and directories without asking for confirmation.

---

### `man`

Displays the manual page for a command.

```bash
man ls
```

You can navigate using:

* Arrow keys
* Page Up
* Page Down
* Space

Press `q` to exit the manual.

---

## 2. What Is a Link?

A link is a reference to a file or directory.

Linux has two important types of links:

1. Symbolic links
2. Hard links

They look similar from a user's perspective, but they work very differently internally.

---

## 3. Symbolic Links

A symbolic link, also called a symlink, is similar to a shortcut in Windows.

Imagine that we have:

```text
original.txt
```

We can create:

```text
link.txt
```

where `link.txt` points to `original.txt`.

The link does not contain the original file's data. It contains a reference to the original file.

The command to create a symbolic link is:

```bash
ln -s original.txt link.txt
```

The `-s` means symbolic.

---

### 4.1 Symbolic Link Behavior

Suppose we have:

```text
original.txt
     ↑
     |
link.txt
```

If we delete the symbolic link:

```bash
rm link.txt
```

The original file remains untouched.

```text
original.txt
```

However, if we delete the original:

```bash
rm original.txt
```

The symbolic link remains, but it becomes a broken link.

This is called a dangling or broken symbolic link.

---

### 4.2 Modifying Through a Symbolic Link

If the symbolic link points to a normal file, accessing the link accesses the original file.

For example:

```bash
echo "Hello Linux" > link.txt
```

The contents of `original.txt` will also change because both operations ultimately access the original file.

This is why symbolic links are extremely useful for configuration files, application versions, directories, and system administration.

---

## 4. Understanding Inodes

To understand hard links, we first need to understand inodes.

An inode is an internal filesystem structure that stores information about a file.

You can think of an inode as an internal identification number associated with a file.

The inode contains metadata such as:

* File type
* Permissions
* Owner
* Group
* File size
* Timestamps
* References to the file's data blocks

The filename itself is not the file's inode.

Instead, the filesystem maintains a relationship between:

```text
filename -> inode -> file data
```

For example:

```text
giropops -> inode 5320194 -> file data
```

---

## 5. Why Inodes Matter

Inodes are finite.

A filesystem can run out of inodes even when there is still free disk space.

For example, imagine a filesystem with:

```text
Disk space:
200 GB free

Inodes:
0 available
```

You may still have 200 GB of free storage, but you cannot create new files because there are no free inodes.

This can happen when a system creates a huge number of very small files.

For example:

```text
file001
file002
file003
file004
...
file10000000
```

Even if every file is only 0 bytes or a few bytes, each file still requires filesystem metadata and an inode.

This is a common troubleshooting scenario on Linux servers.

---

## 6. Checking Inodes

We can use:

```bash
ls -li
```

The `-i` option displays the inode number.

Example:

```text
5320194 -rw-r--r-- 1 user user 104857600 giropops
```

Here:

```text
5320194
```

is the inode number.

You can also use `df -i` to inspect inode usage across filesystems:

```bash
df -i
```

This is an important command when troubleshooting a filesystem that appears to have free disk space but refuses to create new files.

---

## 7. Creating a Test File

Let's create a file:

```bash
touch Corinthians
```

Now:

```bash
ls -li
```

You will see that the file has:

```text
0 bytes
```

but it still has an inode.

A zero-byte file still consumes filesystem metadata.

---

## 8. Creating Large Test Files with `dd`

We can use `dd` to create files with a specific size.

For example:

```bash
dd if=/dev/zero of=giropops bs=10M count=10
```

This creates a file of approximately:

```text
10M x 10 = 100M
```

Let's break it down:

### `if`

Input file:

```bash
if=/dev/zero
```

`/dev/zero` provides a continuous stream of zero bytes.

### `of`

Output file:

```bash
of=giropops
```

### `bs`

Block size:

```bash
bs=10M
```

Each block is 10 MB.

### `count`

Number of blocks:

```bash
count=10
```

Therefore:

```text
10 MB x 10 = 100 MB
```

`dd` is a powerful command and can be used for much more than creating test files. It can also perform low-level data copying between devices and filesystems.

> **Warning:** Be careful with `dd`, especially when writing directly to disks.

---

## 9. Creating a Test Directory Structure

Let's create a simple structure:

```bash
mkdir -p etc/conf
```

Now we can move our test file:

```bash
mv giropops etc/conf/
```

Check it:

```bash
ls -li etc/conf/
```

You should see the inode number associated with `giropops`.

---

## 10. Hard Links

Now we can introduce the hard link.

A hard link is different from a symbolic link.

A hard link does not point to another filename.

Instead, it creates another directory entry pointing to the same inode.

Imagine:

```text
original filename
       |
       v
   inode 202
       ^
       |
 hard link
```

Both names reference the same inode.

Therefore, they are effectively two names for the same underlying file.

---

## 11. Creating a Hard Link

The basic syntax is:

```bash
ln original hardlink
```

For example:

```bash
ln etc/conf/giropops giropops-hard-link
```

Now:

```bash
ls -li
```

You should see something similar to:

```text
5320194 ... giropops-hard-link
5320194 ... giropops
```

Notice that the inode number is exactly the same.

This is the key difference.

---

## 12. Symbolic Link vs Hard Link

Let's compare them.

### Symbolic link

```bash
ln -s original symlink
```

Creates a new file with a different inode.

The symbolic link stores a path to the original.

Conceptually:

```text
symlink
   |
   v
original
   |
   v
inode
```

### Hard link

```bash
ln original hardlink
```

Creates another directory entry for the same inode.

Conceptually:

```text
original ----\
              > inode
hardlink ----/
```

---

## 13. The Main Difference

| Feature                        | Symbolic Link | Hard Link |
| ------------------------------ | ------------- | --------- |
| Creates another inode          | Yes           | No        |
| Points to another path         | Yes           | No        |
| Points directly to same inode  | No            | Yes       |
| Can cross filesystems          | Yes           | No        |
| Can become broken              | Yes           | No        |
| Removing link removes original | No            | No        |
| Removing original breaks link  | Yes           | No        |
| Shows `l` in `ls -l`           | Yes           | No        |
| Created with                   | `ln -s`       | `ln`      |

---

## 14. Why Hard Links Cannot Cross Filesystems

Each filesystem has its own inode table.

Suppose we have:

```text
Filesystem A
    inode 202

Filesystem B
    inode 202
```

These inode numbers are unrelated.

A hard link must reference an inode belonging to the same filesystem.

Therefore:

```text
Filesystem A -> Filesystem B
```

cannot be used to create a hard link.

Symbolic links do not have this limitation because they store a path.

Therefore, a symbolic link can point to a file located on another filesystem.

---

## 15. What Happens When We Delete a Hard Link?

Suppose:

```text
giropops --------\
                  > inode 5320194
hard-link -------/
```

If we remove:

```bash
rm giropops
```

the inode still exists because `hard-link` references it.

The file data remains accessible through:

```bash
cat hard-link
```

Only when the last hard link is removed does the filesystem release the file's data.

This is why a hard link is more than just a shortcut.

It is another name for the same underlying file.

---

## 16. Understanding Link Counts

Run:

```bash
ls -li
```

You may notice a number after the permissions:

```text
-rw-r--r-- 2 user user ...
```

That `2` is the number of hard links associated with the inode.

For example:

```text
giropops
hard-link
```

Both point to the same inode, so the link count becomes `2`.

If you remove one:

```bash
rm hard-link
```

the link count becomes `1`.

The underlying file still exists.

---

## 17. Using `man`

Linux commands usually have detailed manual pages.

For example:

```bash
man ls
```

You can search through the manual using:

```text
/
```

Then type a search term.

For example:

```text
/inode
```

Press `Enter` to search.

Use:

* `Space` to move down
* Arrow keys to navigate
* `q` to quit

You should become comfortable with `man`.

You do not need to memorize every Linux command or every option.

You need to know how to find the information when you need it.

---

## 18. Symbolic Links in `ls`

When you run:

```bash
ls -l
```

a symbolic link is easy to identify.

You will see something similar to:

```text
lrwxrwxrwx 1 user user 20 symlink -> /path/to/original
```

The first character is:

```text
l
```

which means symbolic link.

The arrow:

```text
->
```

shows where the symbolic link points.

A normal file does not show this arrow.

---

## 19. Hard Links in `ls`

A hard link looks like a normal file:

```text
-rw-r--r-- 2 user user ...
```

There is no arrow.

The important clue is the inode number.

Run:

```bash
ls -li
```

If two filenames have the same inode number, they are hard links to the same underlying file.

---

## 20. Shell Productivity: Tab Completion

Another important shell skill is tab completion.

Instead of typing:

```bash
cd /var/log/my-very-long-directory-name
```

you can type part of the name and press:

```text
Tab
```

The shell will try to complete it.

Tab completion works with:

* Commands
* Files
* Directories
* Paths
* Many command arguments

Using `Tab` makes you faster and also reduces typing mistakes.

Get used to using it constantly.

---

## 21. Command History

We previously learned:

```bash
history
```

It displays commands that you have executed.

You can also use:

```text
Ctrl + R
```

to search through command history interactively.

For example, press:

```text
Ctrl + R
```

and type:

```text
tar
```

The shell will search for previous commands containing `tar`.

This is one of the most useful shell shortcuts you can learn.

---

## 22. Aliases

An alias creates a shortcut for a command.

For example:

```bash
alias listar='ls -lai'
```

Now:

```bash
listar
```

executes:

```bash
ls -lai
```

You can see the aliases currently configured with:

```bash
alias
```

Aliases are useful when a command is long or when you frequently use a particular combination of options.

---

## 23. Making an Alias Persistent

There is an important limitation.

If you run:

```bash
alias listar='ls -lai'
```

the alias normally exists only for the current shell session.

If you close the terminal, the alias is gone.

To make it persistent in Bash, add it to:

```bash
~/.bashrc
```

For example:

```bash
echo "alias listar='ls -lai'" >> ~/.bashrc
```

Notice the two `>` characters:

```bash
>>
```

This means append.

It adds the new content to the end of the file.

Be careful with:

```bash
>
```

> **Warning:** A single `>` redirects output and overwrites the destination file.

Therefore:

```bash
>>
```

is generally what you want when adding a new configuration line.

---

## 24. Reloading `.bashrc`

After modifying `.bashrc`, you can reload it without closing the terminal:

```bash
source ~/.bashrc
```

This tells Bash to read and execute the contents of the file again.

You can also use:

```bash
. ~/.bashrc
```

The dot is another way of invoking `source`.

After that, the alias should be available:

```bash
listar
```

---

## 25. ZSH and Other Shells

Not every Linux environment uses Bash.

For example, ZSH uses:

```bash
~/.zshrc
```

So always check which shell you are using.

You can run:

```bash
echo $SHELL
```

For example:

```text
/bin/bash
```

or:

```text
/bin/zsh
```

The configuration file depends on the shell.

---

## Important Commands from This Lesson

| Resource | Purpose |
| --- | --- |
| `ln -s original symlink` | Create a symbolic link |
| `ln original hardlink` | Create a hard link |
| `ls -li` | Show inode numbers |
| `df -i` | Check inode usage across filesystems |
| `man command` | Open the manual page for a command (press `q` to exit) |
| `touch file` | Create an empty test file |
| `dd if=/dev/zero of=file bs=10M count=10` | Create a large test file of a specific size |
| `alias listar='ls -lai'` | Create a temporary alias |
| `echo "alias listar='ls -lai'" >> ~/.bashrc` | Make an alias persistent |
| `source ~/.bashrc` | Reload the Bash configuration file |
| `history` | Display command history |
| `Ctrl + R` | Search command history interactively |
| `Tab` | Auto-complete commands, files, and paths |

---

## 26. Practice Challenge

Now it is time to practice.

Create a test environment:

```bash
mkdir -p ~/linux-links/etc/conf
cd ~/linux-links
```

Create a test file:

```bash
dd if=/dev/zero of=etc/conf/giropops bs=1M count=10
```

Check the inode:

```bash
ls -li etc/conf/giropops
```

Create a symbolic link:

```bash
ln -s etc/conf/giropops giropops-symlink
```

Create a hard link:

```bash
ln etc/conf/giropops giropops-hardlink
```

Now compare them:

```bash
ls -li
```

Answer these questions:

1. Which files have the same inode?
2. Which file has a different inode?
3. Which one displays an arrow with `->`?
4. What happens if you delete the symbolic link?
5. What happens if you delete the original file?
6. What happens if you delete the hard link?
7. What happens to the inode link count?
8. Why can't a hard link cross filesystems?

Then create an alias:

```bash
alias listar='ls -lai'
```

Test it:

```bash
listar
```

Make it persistent:

```bash
echo "alias listar='ls -lai'" >> ~/.bashrc
```

Reload the configuration:

```bash
source ~/.bashrc
```

Finally, open the manual:

```bash
man ln
```

and investigate the available options.

---

## Key Takeaways

The most important concepts from this lesson are:

```text
Symbolic link = another file that points to a path
Hard link     = another name for the same inode
```

Remember:

```text
Symbolic link
      |
      v
   original
      |
      v
    inode
```

versus:

```text
original -----\
               > inode
hard link ----/
```

Also remember:

* `ls -li` shows inode numbers.
* `df -i` shows inode usage.
* `ln -s` creates symbolic links.
* `ln` creates hard links.
* Hard links cannot cross filesystems.
* Symbolic links can become broken.
* Hard links continue working as long as at least one link remains.
* `man` is your built-in Linux documentation.
* `Tab` improves shell productivity.
* `Ctrl + R` searches command history.
* `alias` creates command shortcuts.
* `~/.bashrc` stores persistent Bash configuration.
* `>>` appends to a file.
* `>` overwrites a file.
* `source ~/.bashrc` reloads the configuration.

Do not just read this lesson.

Open the terminal and reproduce everything.

Create symbolic links, create hard links, delete them, inspect inode numbers, break a symbolic link, and observe what happens.

The goal is not simply to memorize the commands.

The goal is to understand how the Linux filesystem works and become comfortable using the shell.

---
