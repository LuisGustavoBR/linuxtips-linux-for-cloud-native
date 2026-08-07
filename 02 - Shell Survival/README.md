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

# Module 2 - Lesson 2: Command-Line Navigation

## The Linux Shell

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

# Navigating Directories

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

# Absolute Paths

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

# Relative Paths

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

# Current and Parent Directory References

Two special path references are especially important when working with relative paths.

## Current Directory: `.`

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

## Parent Directory: `..`

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

# Combining Relative Paths

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

# Switching to the Previous Directory

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

# Returning to the Home Directory

Running `cd` without specifying a path returns to the current user's home directory:

```bash
cd
```

This provides a convenient way to return to a known location without typing the full path.

---

# Listing Directory Contents

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

## Long Format

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

# Human-Readable Sizes

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

# Hidden Files

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

# Combining `ls` Options

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

# Command History

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

# Clearing the Terminal

The `clear` command clears the visible contents of the terminal:

```bash
clear
```

The `Ctrl+L` shortcut commonly provides the same functionality in an interactive shell.

Clearing the terminal does not delete command history or terminate running processes. It only clears the current visible screen.

---

# Tab Completion

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

# Practical Navigation Example

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

# Practical Command Reference

| Command     | Description                                                |
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

# Key Concepts

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

# Module 2 - Lesson 3: File and Directory Management

## Creating Directories

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

## Creating Nested Directories

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

## Creating Empty Files

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

## Copying Files and Directories

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

## Moving Files and Directories

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

## Removing Files and Directories

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

## Removing Directories Recursively

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

## The Danger of `rm -rf /`

The root directory `/` represents the top of the Linux filesystem hierarchy.

Therefore, commands that recursively target `/` can potentially remove the entire filesystem.

For example:

```bash
rm -rf /
```

This should **never** be executed on a real system.

Modern versions of GNU `rm` normally include safeguards such as `--preserve-root`, which prevents accidental recursive deletion of `/`. However, these protections should not be treated as a substitute for verifying commands before execution.

When working as `root`, destructive commands require particular care because the root user has unrestricted access to the system.

---

## Command Summary

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

## Practice

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

---

# Module 2 - Lesson 4: Terminal Shortcuts, Aliases, and Bash Configuration

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

# 8. Aliases

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

# 11. Bash and Its Configuration Files

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

# 15. `echo`

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

# 16. Redirection with `>`

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

# 17. Redirection with `>>`

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

Be especially careful with this when working with configuration files.

---

# 18. Adding an Alias to `.bashrc`

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

# 19. `cat`

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

# 20. `source`

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

# 21. `sudo`

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

# 23. Aliases with `sudo`

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

# 24. Alpine vs Debian

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

# 25. Practice

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

# Lesson 4 Summary

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

The goal is to become faster and more comfortable in the Linux terminal while learning how to customize your shell environment.

---
