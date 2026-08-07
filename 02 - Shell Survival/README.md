# Module 2 - Lesson 1: Exploring the Linux Filesystem

## Overview

Understanding the Linux filesystem hierarchy is one of the most important skills for anyone working with Linux, Cloud, DevOps, or Kubernetes.

In this lesson, you'll explore the purpose of the most important system directories, learn how Linux organizes files, understand symbolic links, executable binaries, device files, and discover how the operating system exposes hardware and kernel information through the filesystem.

---

# Linux Is a Kernel, Not a Complete Operating System

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

# What Is a Linux Distribution?

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

# Why Alpine Linux?

Throughout this course, many examples use **Alpine Linux**.

Alpine is widely adopted in cloud-native environments because it is:

* Extremely lightweight
* Security-focused
* Fast to boot
* Minimal by design
* Commonly used as a base image for containers

Unlike traditional server distributions, Alpine installs only the components necessary to run applications efficiently, making it ideal for Docker containers and Kubernetes workloads.

---

# Navigating the Filesystem

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

# Special Directory Entries

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

# Understanding `ls -l`

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

# Symbolic Links

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

# Linux File Permissions

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

# The `/bin` Directory

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

# BusyBox

BusyBox is a single executable that provides hundreds of standard Linux utilities.

Instead of installing separate binaries for each command, Alpine uses BusyBox to provide lightweight implementations of common tools.

Benefits include:

* Smaller filesystem footprint
* Lower memory usage
* Faster container images

BusyBox is one of the reasons Alpine images are significantly smaller than most Linux distributions.

---

# The `/dev` Directory

Everything in Linux is represented as a file—including hardware devices.

The `/dev` directory contains device files that allow applications to communicate with hardware.

There are two main device types.

## Character Devices

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

## Block Devices

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

## Terminal Devices (`tty`)

Linux terminals are also represented as device files.

Examples:

```text
/dev/tty0
/dev/tty1
```

These are **character devices**, since they exchange streams of characters rather than storing data.

---

# The `/etc` Directory

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

# The `/home` Directory

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

# The `/root` Directory

The root user's home directory is:

```text
/root
```

This directory is reserved exclusively for the system administrator.

---

# The `/lib` Directory

The `/lib` directory stores shared libraries required by executables.

These libraries serve a similar purpose to DLL files on Windows.

Examples include:

* Shared runtime libraries
* Dynamic loader components
* Kernel modules

Removing essential libraries from this directory can prevent the system from functioning correctly.

---

## Kernel Modules

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

# The `/media` Directory

The `/media` directory is commonly used for automatically mounted removable media, such as:

* USB drives
* DVDs
* External storage

Desktop environments typically manage this directory automatically.

---

# The `/mnt` Directory

The `/mnt` directory is intended for temporary mount points created by administrators.

Examples include mounting:

* Remote filesystems
* Additional disks
* Network shares

---

# The `/opt` Directory

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

# The `/proc` Directory

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

## Process Information

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

## Process IDs (PID)

Every running process receives a unique **Process ID (PID)**.

You can list active processes with:

```bash
ps -ef
```

The PID uniquely identifies each running process.

On most Linux systems, process `1` is the system's init process (such as `systemd` or another init implementation), responsible for starting userspace services during boot.

---

# The `/run` Directory

The `/run` directory stores runtime data created while the system is operating.

Typical contents include:

* PID files
* Runtime sockets
* Lock files
* Temporary service information

Its contents are recreated after every reboot.

---

# The `/sbin` Directory

The `/sbin` directory contains system administration binaries.

Examples include commands used for:

* Network configuration
* System shutdown
* Filesystem management
* Service management

These tools are primarily intended for administrative users.

---

# The `/sys` Directory

Like `/proc`, the `/sys` directory is a virtual filesystem.

It exposes information about:

* Devices
* Kernel subsystems
* Drivers
* Hardware
* Kernel parameters

Many system management tools interact directly with this filesystem.

---

# The `/tmp` Directory

The `/tmp` directory stores temporary files.

Applications frequently use this location for:

* Temporary data
* Installation files
* Intermediate processing

Most systems automatically remove its contents after a reboot or periodically through cleanup services.

---

# The `/usr` Directory

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

# The `/var` Directory

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

---

# Key Takeaways

* Linux distributions combine the Linux kernel with user-space utilities and libraries.
* Alpine Linux is a lightweight distribution widely used for containers and cloud-native workloads.
* The Linux filesystem follows standardized conventions that organize executables, configuration files, libraries, devices, and runtime data.
* `/proc` and `/sys` are virtual filesystems that expose real-time kernel and system information.
* Device files in `/dev` represent hardware and system interfaces.
* Understanding the purpose of each top-level directory is essential for Linux administration, troubleshooting, automation, and platform engineering.

---
