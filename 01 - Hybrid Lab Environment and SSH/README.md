# Module 1: Hybrid Lab Environment and SSH Fundamentals

## Overview

Modern infrastructure is built around Linux-based systems running in cloud environments, virtual machines, and containers. Understanding how these components interact is essential for anyone working with Cloud, DevOps, Platform Engineering, or Kubernetes.

This module introduces the foundational concepts behind Linux servers, virtualization, cloud computing, and the mindset required to operate modern infrastructure.

## Table of Contents

- [Module 1 - Lesson 1: Cloud-Native Mindset](#module-1---lesson-1-cloud-native-mindset)
  - [1. Why Linux Matters](#1-why-linux-matters)
  - [2. Linux Desktop vs Linux Server](#2-linux-desktop-vs-linux-server)
  - [3. Understanding Virtualization](#3-understanding-virtualization)
  - [4. Hypervisor Types](#4-hypervisor-types)
  - [5. What Happens When a Virtual Machine Starts?](#5-what-happens-when-a-virtual-machine-starts)
  - [6. Virtual Machines vs Containers](#6-virtual-machines-vs-containers)
  - [7. Cloud Computing Fundamentals](#7-cloud-computing-fundamentals)
  - [8. What Happens When You Launch a Cloud Instance?](#8-what-happens-when-you-launch-a-cloud-instance)
  - [9. Local Virtualization vs Cloud Infrastructure](#9-local-virtualization-vs-cloud-infrastructure)
  - [10. Pets vs Cattle](#10-pets-vs-cattle)
  - [11. Pets](#11-pets)
  - [12. Cattle](#12-cattle)
  - [Key Takeaways](#key-takeaways)
- [Module 1 - Lesson 2: Local Lab Environment: VirtualBox and Ubuntu Server](#module-1---lesson-2-local-lab-environment-virtualbox-and-ubuntu-server)
  - [1. Installing VirtualBox](#1-installing-virtualbox)
  - [2. Downloading Ubuntu Server](#2-downloading-ubuntu-server)
  - [3. Why Build a Local Lab?](#3-why-build-a-local-lab)
  - [Key Takeaways](#key-takeaways-1)
- [Module 1 - Lesson 3: Creating the Virtual Machine and Installing Ubuntu Server](#module-1---lesson-3-creating-the-virtual-machine-and-installing-ubuntu-server)
  - [1. Creating the Virtual Machine](#1-creating-the-virtual-machine)
  - [2. Network Configuration](#2-network-configuration)
  - [3. Installing Ubuntu Server](#3-installing-ubuntu-server)
  - [4. Storage Configuration and LVM](#4-storage-configuration-and-lvm)
  - [5. User Configuration](#5-user-configuration)
  - [6. SSH Configuration](#6-ssh-configuration)
  - [7. Optional Software Packages](#7-optional-software-packages)
  - [8. Understanding the First Boot Process](#8-understanding-the-first-boot-process)
  - [Key Takeaways](#key-takeaways-2)
- [Module 1 - Lesson 4: SSH: The Essential Remote Access Tool](#module-1---lesson-4-ssh-the-essential-remote-access-tool)
  - [1. What is SSH?](#1-what-is-ssh)
  - [2. Connecting to a Virtual Machine](#2-connecting-to-a-virtual-machine)
  - [3. Initial System Verification](#3-initial-system-verification)
  - [4. Check the Current User](#4-check-the-current-user)
  - [5. Check the Hostname](#5-check-the-hostname)
  - [6. Check Kernel Information](#6-check-kernel-information)
  - [7. Check Network Interfaces and IP Addresses](#7-check-network-interfaces-and-ip-addresses)
  - [8. Update the System](#8-update-the-system)
  - [9. Check Disk Usage](#9-check-disk-usage)
  - [10. Expanding an LVM Volume](#10-expanding-an-lvm-volume)
  - [Important Commands from This Lesson](#important-commands-from-this-lesson)
  - [Key Takeaways](#key-takeaways-3)
- [Module 1 - Lesson 5: AWS EC2 Lab (Free Tier)](#module-1---lesson-5-aws-ec2-lab-free-tier)
  - [1. Creating an AWS Account](#1-creating-an-aws-account)
  - [2. Securing the AWS Root Account](#2-securing-the-aws-root-account)
  - [3. Understanding Security Groups](#3-understanding-security-groups)
  - [4. Recommended Security Group Configuration](#4-recommended-security-group-configuration)
  - [5. Understanding EC2 Key Pairs](#5-understanding-ec2-key-pairs)
  - [6. Launching an EC2 Instance](#6-launching-an-ec2-instance)
  - [7. Obtaining the Public IP Address](#7-obtaining-the-public-ip-address)
  - [8. Public IP vs Elastic IP](#8-public-ip-vs-elastic-ip)
  - [9. Connecting to EC2 via SSH](#9-connecting-to-ec2-via-ssh)
  - [10. Common SSH Error: Unprotected Private Key File](#10-common-ssh-error-unprotected-private-key-file)
  - [11. Successful Connection](#11-successful-connection)
  - [Important Commands from This Lesson](#important-commands-from-this-lesson-1)
  - [Key Takeaways](#key-takeaways-4)
- [Module 1 - Lesson 6: SSH Productivity, Key Management, and File Transfers](#module-1---lesson-6-ssh-productivity-key-management-and-file-transfers)
  - [1. SSH Configuration File (`~/.ssh/config`)](#1-ssh-configuration-file-sshconfig)
  - [2. Generating SSH Key Pairs with `ssh-keygen`](#2-generating-ssh-key-pairs-with-ssh-keygen)
  - [3. Installing a Public Key on a Remote Server](#3-installing-a-public-key-on-a-remote-server)
  - [4. Secure File Transfers with SCP](#4-secure-file-transfers-with-scp)
  - [5. Uploading a File](#5-uploading-a-file)
  - [6. Downloading a File](#6-downloading-a-file)
  - [7. Copying Directories Recursively](#7-copying-directories-recursively)
  - [8. Efficient Synchronization with rsync](#8-efficient-synchronization-with-rsync)
  - [9. Installation](#9-installation)
  - [10. Synchronizing a Local Directory to a Remote Server](#10-synchronizing-a-local-directory-to-a-remote-server)
  - [11. Synchronizing from Remote to Local](#11-synchronizing-from-remote-to-local)
  - [12. Excluding Files and Directories](#12-excluding-files-and-directories)
  - [13. Creating a Mirror Copy](#13-creating-a-mirror-copy)
  - [14. Performing a Dry Run](#14-performing-a-dry-run)
  - [15. Common rsync Use Cases](#15-common-rsync-use-cases)
  - [Important Commands from This Lesson](#important-commands-from-this-lesson-2)
  - [Key Takeaways](#key-takeaways-5)

---

# Module 1 - Lesson 1: Cloud-Native Mindset

## 1. Why Linux Matters

Linux is the dominant operating system powering modern infrastructure.

Some key facts:

* The vast majority of internet servers run Linux.
* Public cloud providers build their services on Linux-based platforms.
* Kubernetes nodes run Linux.
* Containers rely on Linux kernel features such as namespaces and cgroups.
* Android is built on the Linux kernel.

Because cloud-native platforms are fundamentally Linux-based, proficiency with Linux is a core skill for infrastructure and platform engineers.

Understanding Linux is not simply learning an operating system—it is learning the foundation of modern computing infrastructure.

---

## 2. Linux Desktop vs Linux Server

A critical distinction in infrastructure operations is understanding the difference between desktop and server environments.

### Linux Desktop

Desktop distributions are optimized for user interaction and productivity.

Examples include:

* Ubuntu Desktop
* Fedora Workstation
* KDE Plasma environments
* GNOME-based distributions

These systems provide:

* Graphical user interfaces (GUI)
* Desktop applications
* Multimedia support
* User-focused tooling

### Linux Server

Production servers typically operate without a graphical interface.

Benefits of a headless server include:

#### Reduced Resource Consumption

Graphical environments consume additional CPU and memory resources that are unnecessary for server workloads.

#### Smaller Attack Surface

Fewer installed components reduce potential security vulnerabilities.

#### Better Automation

Infrastructure automation is performed through:

* Shell scripts
* APIs
* Infrastructure as Code (IaC)
* Configuration management tools

#### Remote Administration

Servers are usually accessed remotely through SSH rather than local monitors and keyboards.

A typical production server environment consists of:

* Terminal access
* Command-line tools
* Automated deployment workflows
* Minimal installed software

---

## 3. Understanding Virtualization

Virtualization allows multiple virtual machines (VMs) to run on a single physical server.

Each VM operates as if it owns dedicated hardware resources:

* CPU
* Memory
* Storage
* Network interfaces

In reality, these resources are managed by a software layer called a **hypervisor**.

---

## 4. Hypervisor Types

### Type 1 Hypervisor (Bare-Metal)

A Type 1 hypervisor runs directly on physical hardware.

Common examples include:

* KVM
* VMware ESXi
* Microsoft Hyper-V Server

Architecture:

```text
┌─────────┐   ┌─────────┐   ┌─────────┐
│   VM 1  │   │   VM 2  │   │   VM 3  │
├─────────┤───├─────────┤───├─────────┤
│          TYPE 1 HYPERVISOR          │
├─────────────────────────────────────┤
│           PHYSICAL HARDWARE         │
└─────────────────────────────────────┘
```

Type 1 hypervisors are commonly used by cloud providers because they provide better performance and isolation.

---

### Type 2 Hypervisor (Hosted)

A Type 2 hypervisor runs on top of an existing operating system.

Common examples include:

* VirtualBox
* VMware Workstation
* Parallels Desktop

Architecture:

```text
┌─────────┐   ┌─────────┐   ┌─────────┐
│   VM 1  │   │   VM 2  │   │   VM 3  │
├─────────┤───├─────────┤───├─────────┤
│          TYPE 2 HYPERVISOR          │
├─────────────────────────────────────┤
│        HOST OPERATING SYSTEM        │
│        (Windows/macOS/Linux)        │
├─────────────────────────────────────┤
│         PHYSICAL HARDWARE           │
└─────────────────────────────────────┘
```

Type 2 hypervisors are commonly used for:

* Development environments
* Testing labs
* Personal learning environments

---

## 5. What Happens When a Virtual Machine Starts?

When a virtual machine is created:

1. The hypervisor allocates CPU resources.
2. Memory is reserved for the VM.
3. Virtual storage is attached.
4. Virtual network interfaces are created.
5. The guest operating system boots as if it were running on dedicated hardware.

For example, a VM configured with a 20 GB disk may actually be backed by a file stored on the host machine.

The virtualization layer abstracts the physical hardware and presents virtualized resources to the guest operating system.

---

## 6. Virtual Machines vs Containers

Virtual machines virtualize hardware.

Containers do not.

Containers share the host operating system kernel and isolate applications using Linux kernel features such as:

* Namespaces
* cgroups

As a result, containers are typically:

* Faster to start
* More resource efficient
* Easier to scale

This distinction becomes fundamental when working with Kubernetes.

---

## 7. Cloud Computing Fundamentals

## 8. What Happens When You Launch a Cloud Instance?

When a virtual machine is launched in a cloud platform, the following process occurs:

1. A request is made through a web console, CLI, or API.
2. Compute resources are allocated.
3. Storage is attached.
4. Networking is configured.
5. An operating system image is deployed.
6. The virtual machine is started.

From a technical perspective, a cloud instance is still a virtual machine running on physical hardware in a data center.

The primary innovation of cloud computing is not virtualization itself, but the ability to provision infrastructure through APIs at scale.

---

## 9. Local Virtualization vs Cloud Infrastructure

| Aspect       | Local Virtual Machine         | Cloud Virtual Machine            |
| ------------ | ----------------------------- | -------------------------------- |
| Cost         | Uses local hardware resources | Consumption-based pricing        |
| Performance  | Limited by local hardware     | Scalable through instance sizing |
| Network      | Local network                 | Global connectivity              |
| Storage      | Local disk files              | Managed block storage services   |
| Availability | Dependent on host uptime      | Designed for high availability   |
| Provisioning | Manual                        | API-driven and automated         |

---

## 10. Pets vs Cattle

One of the most important cloud-native concepts is the distinction between **Pets** and **Cattle**.

## 11. Pets

Traditional servers are treated as unique systems:

* Individually configured
* Manually maintained
* Given meaningful names
* Difficult to replace

If a server fails, significant effort is invested in recovering it.

---

## 12. Cattle

Cloud-native infrastructure treats servers as disposable resources:

* Automatically provisioned
* Consistently configured
* Easily replaced
* Managed through code

If an instance fails, a new one is created automatically.

This approach relies on practices such as:

* Infrastructure as Code (IaC)
* Immutable Infrastructure
* Automated provisioning
* Self-healing systems

The goal is to make infrastructure reproducible, scalable, and resilient rather than dependent on manual administration.

---

## Key Takeaways

* Linux is the foundation of modern cloud infrastructure.
* Production servers are typically managed through command-line interfaces and SSH.
* Virtualization enables multiple virtual machines to share physical hardware.
* Type 1 hypervisors power most cloud environments.
* Cloud instances are virtual machines provisioned through APIs.
* Containers differ fundamentally from virtual machines by sharing the host kernel.
* Modern infrastructure favors the **Cattle** model, where servers are disposable and managed through automation.

---

# Module 1 - Lesson 2: Local Lab Environment: VirtualBox and Ubuntu Server

## 1. Installing VirtualBox

VirtualBox is a Type 2 hypervisor that allows virtual machines to run on top of an existing operating system.

Supported host operating systems include:

* Windows
* macOS
* Linux

After downloading the appropriate installer for your platform, follow the standard installation process and accept the default settings unless specific customization is required.

### Apple Silicon Considerations

For macOS systems based on Apple Silicon processors (M-series), VirtualBox support may be limited depending on the version.

Alternative virtualization platforms include:

* UTM
* Parallels Desktop

The virtualization concepts covered throughout this training remain the same regardless of the platform used.

---

## 2. Downloading Ubuntu Server

For this training, use the latest available **Ubuntu Server LTS (Long-Term Support)** release.

### Why Choose an LTS Release?

LTS releases are designed for production environments and provide:

* Long-term security updates
* Stability and reliability
* Extended support lifecycle
* Broad ecosystem compatibility

These characteristics make LTS releases the preferred choice for servers, cloud instances, and enterprise environments.

### Ubuntu Server vs Ubuntu Desktop

It is important to download **Ubuntu Server**, not Ubuntu Desktop.

Ubuntu Server is optimized for infrastructure workloads and includes:

* Minimal package installation
* Command-line administration
* Lower resource consumption
* Reduced attack surface

Unlike desktop editions, Ubuntu Server does not include a graphical user interface by default, which more closely reflects real-world production environments.

---

## 3. Why Build a Local Lab?

A local laboratory provides several advantages during the learning process:

### Safe Experimentation

Configuration changes, troubleshooting exercises, and software installations can be performed without impacting production systems.

### Repeatable Learning Environment

Virtual machines can be recreated, reset, and reconfigured as needed.

### Infrastructure Practice

The environment can be used to practice:

* SSH access
* Linux administration
* Network configuration
* Service management
* Storage management
* Automation scripts

### Cloud Preparation

Many of the concepts learned locally will later be applied to cloud virtual machines such as AWS EC2 instances.

The primary difference is the hosting location; the underlying operating system and administration techniques remain largely the same.

---

## Key Takeaways

* VirtualBox provides a simple way to create a Linux learning environment.
* Ubuntu Server closely reflects the operating systems commonly used in production environments.
* LTS releases are recommended for stability and long-term support.
* Server environments are typically managed through the command line rather than graphical interfaces.
* A local lab offers a safe environment for experimentation before working with cloud infrastructure.

---

# Module 1 - Lesson 3: Creating the Virtual Machine and Installing Ubuntu Server

## 1. Creating the Virtual Machine

Open VirtualBox and create a new virtual machine using the following recommended settings:

| Parameter | Recommended Value          | Rationale                                       |
| --------- | -------------------------- | ----------------------------------------------- |
| Name      | `linux-lab`                | Simple and descriptive                          |
| Type      | Linux                      | Matches the guest operating system              |
| Version   | Ubuntu (64-bit)            | Matches the downloaded ISO                      |
| Memory    | 2048 MB (2 GB)             | Sufficient for a Linux server lab               |
| CPUs      | 2 vCPUs                    | Provides adequate performance for lab workloads |
| Disk      | 20 GB (Dynamic Allocation) | Efficient storage utilization                   |

### Dynamic vs Fixed Disk Allocation

VirtualBox supports two disk allocation methods:

#### Dynamic Allocation

The virtual disk file grows as data is written inside the VM.

Advantages:

* Consumes less host storage initially
* Ideal for learning environments
* More efficient use of local disk space

#### Fixed Allocation

The entire disk size is allocated immediately.

Advantages:

* Slightly better disk performance
* Predictable storage consumption

For laboratory environments, dynamic allocation is generally the preferred option.

---

## 2. Network Configuration

Before starting the virtual machine, review the network adapter settings.

Understanding virtualization networking modes is fundamental for Linux and cloud networking concepts.

### NAT (Network Address Translation)

NAT is the default VirtualBox networking mode.

Characteristics:

* The VM can access the internet.
* External devices cannot directly access the VM.
* The VM receives a private virtualized address.

Architecture:

```text
Internet <--> Host Machine <--> NAT <--> Virtual Machine (10.0.2.15)
```

### Bridged Adapter

The virtual machine becomes a full participant in the physical network.

Characteristics:

* Receives an IP address from the local DHCP server.
* Appears as an independent device on the network.
* Can be accessed directly from other devices.

Architecture:

```text
Internet <--> Router <--> Host Machine (192.168.1.10) <--> Virtual Machine (192.168.1.20)
```

### Host-Only Adapter

Creates an isolated network between the host and the virtual machine.

Characteristics:

* Host can access the VM.
* VM cannot access the internet.
* Useful for isolated testing environments.

Architecture:

```text
Host Machine <--> Isolated Network <--> Virtual Machine (192.168.56.10) (No Internet Access)
```

### Recommended Configuration

For this training environment, a **Bridged Adapter** is recommended because it provides:

* Internet connectivity
* Direct SSH access
* A networking model closer to real-world server environments

If Bridged mode is restricted by corporate or wireless network policies, use NAT with port forwarding.

Example SSH forwarding rule:

| Setting    | Value     |
| ---------- | --------- |
| Protocol   | TCP       |
| Host IP    | 127.0.0.1 |
| Host Port  | 2222      |
| Guest Port | 22        |

SSH access can then be established using:

```bash
ssh -p 2222 username@127.0.0.1
```

---

## 3. Installing Ubuntu Server

Attach the downloaded Ubuntu Server ISO to the virtual machine and start the installation process.

The Ubuntu Server installer will guide you through the operating system deployment.

### Keyboard Layout

Select the keyboard layout that matches your physical keyboard.

Using the correct layout is particularly important when working with symbols commonly used in Linux administration and scripting:

```text
|
\
{
}
~
```

---

### Installation Type

Select the standard **Ubuntu Server** installation.

Avoid the minimized installation option, as several utilities used throughout the training may not be included.

---

### Network Configuration

If DHCP is available, Ubuntu should automatically obtain an IP address.

Examples:

```text
Bridged: 192.168.x.x
NAT:     10.0.2.x
```

Record the assigned IP address, as it will be required for SSH access.

---

### Proxy and Package Mirror

Unless operating behind a corporate proxy, leave the proxy settings empty and use the default Ubuntu package mirror.

---

## 4. Storage Configuration and LVM

For storage configuration, select:

* Use an entire disk
* Enable LVM (Logical Volume Manager)

### What Is LVM?

LVM introduces a logical abstraction layer between physical storage devices and filesystems.

Benefits include:

* Online volume expansion
* Flexible storage management
* Easier disk growth operations
* Better support for enterprise environments

LVM consists of three primary components:

### Physical Volume (PV)

The physical storage device or partition managed by LVM.

### Volume Group (VG)

A storage pool created from one or more physical volumes.

### Logical Volume (LV)

Virtual partitions created from a volume group.

Architecture:

```text
┌──────────────────────────────────────┐
│         Logical Volumes (LV)         │
│  ┌────────────┐  ┌────────────────┐  │
│  │  LV: root  │  │  LV: home      │  │
│  │  /  (15GB) │  │  /home  (5GB)  │  │
│  └────────────┘  └────────────────┘  │
├──────────────────────────────────────┤
│          Volume Group (VG)           │
│          ubuntu-vg (20GB)            │
├──────────────────────────────────────┤
│         Physical Volume (PV)         │
│         /dev/sda3 (20GB)             │
├──────────────────────────────────────┤
│          Physical Disk               │
│          /dev/sda (20GB)             │
└──────────────────────────────────────┘
```

LVM is widely used in enterprise Linux environments because it enables storage growth without major system reconfiguration.

> **Note:** Ubuntu may intentionally leave unallocated space inside the Volume Group. This allows logical volumes to be expanded later without repartitioning.

---

## 5. User Configuration

Create a standard administrative user account.

Examples:

```text
devops
admin
luisgustavo
```

Avoid using `root` as the primary login account.

Administrative privileges can be granted through `sudo`, which provides improved security and accountability.

---

## 6. SSH Configuration

During installation, enable:

```text
Install OpenSSH Server
```

This component is required for remote administration and will be used extensively throughout the training.

Without OpenSSH Server, remote terminal access will not be available.

---

## 7. Optional Software Packages

Skip the optional featured Snap packages during installation.

A minimal server installation provides:

* Lower resource consumption
* Reduced attack surface
* Easier maintenance
* Faster updates

---

## 8. Understanding the First Boot Process

After installation and reboot, Linux follows a defined startup sequence.

### 1. GRUB

The bootloader loads the Linux kernel into memory.

### 2. Linux Kernel

The kernel initializes core hardware components such as:

* CPU
* Memory
* Storage devices
* Network interfaces

### 3. systemd

The first userspace process starts.

`systemd` runs as PID 1 and is responsible for launching system services such as:

* Networking
* SSH
* Logging
* Scheduled tasks

### 4. Login Prompt

The system presents a login screen, allowing user authentication and access to the server environment.

After logging in, the Linux server is ready for administration and remote access.

---

## Key Takeaways

* A virtual machine is created in VirtualBox with the recommended specs (2 GB RAM, 2 vCPUs, 20 GB dynamically allocated disk) before installing the OS.
* The network adapter mode must be chosen before boot: **Bridged** is recommended for this lab because it gives the VM its own LAN IP and direct SSH access, closer to a real server; **NAT** requires port forwarding to reach the VM from outside.
* During Ubuntu Server installation: pick the matching keyboard layout, choose the standard (non-minimized) install so training utilities are available, let DHCP assign the network address, and leave proxy/mirror settings at their defaults unless behind a corporate proxy.
* Enabling **LVM** during storage setup adds a logical layer (Physical Volume → Volume Group → Logical Volume) on top of the physical disk, allowing the filesystem to grow later without repartitioning — Ubuntu may deliberately leave space unallocated in the Volume Group for this purpose.
* Create a standard administrative user instead of logging in as `root`; use `sudo` for privileged actions.
* Enable **OpenSSH Server** during installation — without it, no remote terminal access is possible.
* Skip optional Snap packages to keep the installation minimal, reducing resource usage and attack surface.
* On first boot, Linux follows a fixed sequence: **GRUB** loads the kernel → the **kernel** initializes hardware (CPU, memory, storage, network) → **systemd** starts as PID 1 and launches services (networking, SSH, logging, scheduled tasks) → the **login prompt** appears.

---

# Module 1 - Lesson 4: SSH: The Essential Remote Access Tool

With both your local VM and cloud instance running, the next step is connecting to them remotely using SSH.

---

## 1. What is SSH?

**SSH (Secure Shell)** is an encrypted network protocol used for secure communication between computers. It follows a **client-server architecture**:

* **SSH Server (`sshd`)** runs on the target machine and listens for incoming connections (port **22** by default).
* **SSH Client (`ssh`)** is the command-line tool used to initiate a connection from your local machine.

All traffic is encrypted, protecting credentials and data from interception when accessing systems over local networks or the public internet.

---

## 2. Connecting to a Virtual Machine

### Using a Bridged Network

If your VM is configured with a **Bridged Adapter**, it receives an IP address from your local network.

```bash
ssh devops@192.168.1.20
```

### First Connection Warning

The first time you connect to a server, SSH displays a host verification message:

```text
The authenticity of host '192.168.1.20' can't be established.
ED25519 key fingerprint is SHA256:xxxxxxxxxxxxxxxxxxx.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

This message indicates that your SSH client has never connected to this host before.

In a lab environment, it is generally acceptable to type:

```text
yes
```

> **Warning:** In production environments, always verify the server fingerprint through a trusted channel before accepting it. This helps prevent **Man-in-the-Middle (MITM)** attacks.

After accepting the fingerprint, SSH prompts for the user's password.

### Using NAT with Port Forwarding

If the VM uses **NAT networking** and port forwarding is configured (host port `2222` → guest port `22`), connect using:

```bash
ssh -p 2222 devops@127.0.0.1
```

---

## 3. Initial System Verification

After establishing the connection, verify that the system is functioning correctly and become familiar with basic administrative commands.

## 4. Check the Current User

Display the account currently logged into the system:

```bash
whoami
```

Example output:

```text
devops
```

## 5. Check the Hostname

Display the machine's hostname:

```bash
hostname
```

Example output:

```text
linux-lab
```

## 6. Check Kernel Information

Display detailed operating system and kernel information:

```bash
uname -a
```

Example output:

```text
Linux linux-lab 6.8.0-45-generic #45-Ubuntu SMP x86_64 GNU/Linux
```

### Understanding the Output

| Field              | Description                   |
| ------------------ | ----------------------------- |
| `Linux`            | Kernel name                   |
| `linux-lab`        | Hostname                      |
| `6.8.0-45-generic` | Kernel version                |
| `x86_64`           | CPU architecture (64-bit x86) |
| `GNU/Linux`        | Operating system environment  |

The Linux kernel is responsible for managing hardware resources, memory, processes, storage, and networking.

## 7. Check Network Interfaces and IP Addresses

Display all network interfaces:

```bash
ip addr
```

Example output:

```text
1: lo: <LOOPBACK,UP>
    inet 127.0.0.1/8 scope host lo

2: enp0s3: <BROADCAST,MULTICAST,UP>
    inet 192.168.1.20/24 brd 192.168.1.255 scope global dynamic enp0s3
```

### Understanding the Interfaces

#### Loopback Interface (`lo`)

```text
127.0.0.1
```

The loopback interface allows the system to communicate with itself and is commonly used for local services and testing.

#### Physical Network Interface

```text
enp0s3
```

This is the machine's network adapter. Interface names may vary depending on the operating system and virtualization platform:

* `enp0s3`
* `eth0`
* `ens33`

The IP address assigned to this interface is typically the address used for SSH connections.

## 8. Update the System

Refresh package metadata and install available updates:

```bash
sudo apt update && sudo apt upgrade -y
```

### Command Breakdown

| Command          | Purpose                                                    |
| ---------------- | ---------------------------------------------------------- |
| `sudo`           | Execute with administrative privileges                     |
| `apt update`     | Refresh package repository metadata                        |
| `&&`             | Execute the next command only if the previous one succeeds |
| `apt upgrade -y` | Install available package updates automatically            |

Keeping systems updated is a fundamental security and maintenance practice.

## 9. Check Disk Usage

Display filesystem usage in a human-readable format:

```bash
df -h
```

Example output:

```text
Filesystem                         Size  Used Avail Use% Mounted on
/dev/mapper/ubuntu--vg-ubuntu--lv  9.8G  4.2G  5.1G  46% /
```

### Understanding the Output

| Column       | Description           |
| ------------ | --------------------- |
| `Size`       | Total filesystem size |
| `Used`       | Consumed space        |
| `Avail`      | Available space       |
| `Use%`       | Percentage used       |
| `Mounted on` | Mount point           |

## 10. Expanding an LVM Volume

In some Ubuntu installations, **Logical Volume Manager (LVM)** allocates only part of the available disk space during installation.

For example, a VM with a 20 GB virtual disk may initially expose only 10 GB to the root filesystem.

To allocate all remaining free space:

```bash
sudo lvextend -l +100%FREE /dev/mapper/ubuntu--vg-ubuntu--lv
sudo resize2fs /dev/mapper/ubuntu--vg-ubuntu--lv
```

### Verify the Expansion

```bash
df -h
```

The filesystem should now reflect the full available capacity.

One of the key advantages of LVM is the ability to expand storage volumes dynamically without reinstalling the operating system or recreating filesystems.

## Important Commands from This Lesson

| Command | Purpose |
|---|---|
| `ssh user@IP` | Connect to a host directly reachable on the local network (bridged VM). |
| `ssh -p PORT user@127.0.0.1` | Connect to a NAT VM through a forwarded host port. |
| `whoami` | Show the currently logged-in user. |
| `hostname` | Show the machine's hostname. |
| `uname -a` | Show kernel name, version, and CPU architecture. |
| `ip addr` | List network interfaces and their assigned IP addresses. |
| `sudo apt update && sudo apt upgrade -y` | Refresh package metadata and install available updates. |
| `df -h` | Show filesystem usage in human-readable form. |
| `sudo lvextend -l +100%FREE /dev/mapper/VG-LV` | Allocate all remaining free space to an LVM logical volume. |
| `sudo resize2fs /dev/mapper/VG-LV` | Grow the filesystem to fill the expanded logical volume. |

---

## Key Takeaways

* SSH is an encrypted client-server protocol: `sshd` listens on the target machine (port 22 by default) and the `ssh` client initiates the connection, protecting credentials and data from interception.
* A **Bridged** VM is reached directly by its LAN IP (`ssh user@192.168.1.20`); a **NAT** VM requires connecting through the forwarded host port (`ssh -p 2222 user@127.0.0.1`).
* The first connection to any host always shows a fingerprint verification prompt — in production, always verify the fingerprint through a trusted channel before accepting it, to guard against Man-in-the-Middle attacks.
* After connecting, basic system verification uses `whoami` (current user), `hostname`, `uname -a` (kernel/OS info), `ip addr` (network interfaces), and `df -h` (disk usage).
* `sudo apt update && sudo apt upgrade -y` refreshes package metadata and installs updates — a fundamental security and maintenance habit.
* If LVM only allocated part of the disk during installation, `sudo lvextend -l +100%FREE <volume>` followed by `sudo resize2fs <volume>` expands the filesystem live, without reinstalling the OS.

---

# Module 1 - Lesson 5: AWS EC2 Lab (Free Tier)

A local environment is essential for learning Linux and DevOps fundamentals, but real-world experience requires working with cloud infrastructure. AWS EC2 provides an ideal platform for practicing server administration, networking, and remote access in a production-like environment.

---

## 1. Creating an AWS Account

Create an AWS account at:

https://aws.amazon.com/

A valid payment method is required during registration. However, resources that remain within the AWS Free Tier limits will not incur charges.

> **Warning:** Always monitor your AWS usage to avoid unexpected costs.

---

## 2. Securing the AWS Root Account

Before creating any resources, enable **Multi-Factor Authentication (MFA)** for the root account.

Navigate to:

```text
IAM → Security Credentials → Assign MFA Device
```

Use an authentication application such as:

* Google Authenticator
* Authy
* Microsoft Authenticator

> **Note:** MFA significantly reduces the risk of unauthorized access and should always be enabled on privileged accounts.

---

## 3. Understanding Security Groups

A **Security Group** is a stateful virtual firewall that controls inbound and outbound traffic for an EC2 instance.

### Inbound Rules

Define:

* Who can access the instance
* Which protocol is allowed
* Which port can be reached

### Outbound Rules

Define:

* Where the instance can send traffic
* Which protocols and destinations are allowed

### Stateful Behavior

Security Groups are stateful by design.

If an inbound connection is allowed, the corresponding response traffic is automatically permitted without requiring an explicit outbound rule.

---

## 4. Recommended Security Group Configuration

| Direction | Type        | Protocol | Port | Source         | Purpose                                              |
| --------- | ----------- | -------- | ---- | -------------- | ---------------------------------------------------- |
| Inbound   | SSH         | TCP      | 22   | Your Public IP | Remote administration                                |
| Outbound  | All Traffic | All      | All  | 0.0.0.0/0      | Internet access for updates and package installation |

> **Warning:** Never expose SSH (port 22) to `0.0.0.0/0`.
>
> Restrict access to your public IP whenever possible. AWS provides a **My IP** option that automatically detects and populates your current IP address.

---

## 5. Understanding EC2 Key Pairs

AWS EC2 uses **public key authentication** instead of traditional passwords.

A key pair consists of:

| Key Type    | Purpose                     |
| ----------- | --------------------------- |
| Public Key  | Stored on the EC2 instance  |
| Private Key | Stored securely by the user |

The public key is placed on the server in:

```bash
~/.ssh/authorized_keys
```

The private key is the `.pem` file downloaded during instance creation.

### Authentication Flow

1. The SSH client initiates a connection.
2. The server verifies the user's public key.
3. The server generates a cryptographic challenge.
4. The client signs the challenge using the private key.
5. Access is granted if the response is valid.

The private key is never transmitted across the network.

---

## 6. Launching an EC2 Instance

Navigate to:

```text
EC2 → Instances → Launch Instance
```

Configure the instance as follows:

| Setting        | Value                     |
| -------------- | ------------------------- |
| Name           | linux-lab-aws             |
| AMI            | Ubuntu Server LTS         |
| Instance Type  | t2.micro or t3.micro      |
| Key Pair       | Existing or newly created |
| Storage        | 20 GB gp3                 |
| Security Group | SSH restricted to your IP |

After reviewing the configuration, click:

```text
Launch Instance
```

Wait until the instance state changes to:

```text
Running
```

---

## 7. Obtaining the Public IP Address

From the EC2 instance details page, locate:

```text
Public IPv4 Address
```

This address will be used for SSH connections.

## 8. Public IP vs Elastic IP

### Public Dynamic IP

* Assigned automatically
* Changes when the instance is stopped and started

### Elastic IP

* Static public IP address
* Remains associated with your account
* May incur charges if allocated but unused

For lab environments, a dynamic public IP is usually sufficient.

---

## 9. Connecting to EC2 via SSH

Move the downloaded private key to a dedicated location:

```bash
mkdir -p ~/.ssh/keys
mv ~/Downloads/linux-lab.pem ~/.ssh/keys/
```

Connect using:

```bash
ssh -i ~/.ssh/keys/linux-lab.pem ubuntu@<EC2-PUBLIC-IP>
```

Example:

```bash
ssh -i ~/.ssh/keys/linux-lab.pem ubuntu@54.123.45.67
```

---

## 10. Common SSH Error: Unprotected Private Key File

A common error when connecting to EC2 is:

```text
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@

Permissions 0644 for '/home/user/.ssh/keys/linux-lab.pem'
are too open.

This private key will be ignored.
Load key "...": bad permissions
Permission denied (publickey).
```

This occurs because SSH requires private keys to be accessible only by their owner.

### Fixing the Permission Issue

Set restrictive permissions on the key file:

```bash
chmod 400 ~/.ssh/keys/linux-lab.pem
```

Permission breakdown:

| Permission | Description |
| ---------- | ----------- |
| 4          | Read        |
| 0          | No access   |
| 0          | No access   |

Only the file owner can read the key.

Retry the connection:

```bash
ssh -i ~/.ssh/keys/linux-lab.pem ubuntu@<EC2-PUBLIC-IP>
```

---

## 11. Successful Connection

If authentication succeeds, the terminal prompt will resemble:

```bash
ubuntu@ip-172-31-xx-xx:~$
```

At this point, you are connected directly to the EC2 instance, and all commands are executed on the remote server rather than your local machine.

## Important Commands from This Lesson

| Command | Purpose |
|---|---|
| `mkdir -p ~/.ssh/keys` | Create a dedicated directory for storing private key files. |
| `mv ~/Downloads/KEY.pem ~/.ssh/keys/` | Move a downloaded private key into that directory. |
| `ssh -i ~/.ssh/keys/KEY.pem ubuntu@IP` | Connect to an EC2 instance, authenticating with a private key instead of a password. |
| `chmod 400 ~/.ssh/keys/KEY.pem` | Restrict a private key file to read-only access by its owner, as required by SSH. |

---

## Key Takeaways

* AWS Free Tier usage
* Root account security with MFA
* Security Groups
* Stateful firewall behavior
* Public and private key authentication
* EC2 instance deployment
* Public IP addressing
* SSH connectivity
* Linux file permissions
* Secure management of private keys

---

# Module 1 - Lesson 6: SSH Productivity, Key Management, and File Transfers

## 1. SSH Configuration File (`~/.ssh/config`)

Typing the full SSH command every time can become repetitive and error-prone:

```bash
ssh -i ~/.ssh/keys/linux-lab.pem ubuntu@54.123.45.67
```

A common practice is to use the SSH configuration file to create reusable connection profiles.

Create or edit the configuration file:

```bash
vim ~/.ssh/config
```

Example configuration:

```text
Host aws-lab
    HostName 54.123.45.67
    User ubuntu
    IdentityFile ~/.ssh/keys/linux-lab.pem

Host local-lab
    HostName 192.168.1.20
    User devops
```

After saving the file, connections can be established using simple aliases:

```bash
ssh aws-lab
```

or

```bash
ssh local-lab
```

### Benefits

* Simplifies connection management
* Reduces typing errors
* Centralizes SSH settings
* Scales efficiently across multiple servers

This approach becomes particularly valuable when managing multiple environments or infrastructure components.

---

## 2. Generating SSH Key Pairs with `ssh-keygen`

While cloud providers often generate SSH keys during instance creation, administrators typically maintain their own personal key pairs for consistent access across environments.

Generate a modern Ed25519 key pair:

```bash
ssh-keygen -t ed25519 -C "your-email@example.com"
```

### Parameters

| Option       | Description                              |
| ------------ | ---------------------------------------- |
| `-t ed25519` | Uses the Ed25519 cryptographic algorithm |
| `-C`         | Adds a descriptive comment to the key    |

Accept the default location:

```text
~/.ssh/id_ed25519
```

You will also be prompted to configure a passphrase, which adds an additional layer of protection to the private key.

### Generated Files

```text
~/.ssh/id_ed25519       # Private key
~/.ssh/id_ed25519.pub   # Public key
```

> **Warning:** Never share the private key. The public key can be safely distributed to systems that should trust your identity.

---

## 3. Installing a Public Key on a Remote Server

SSH public key authentication requires the public key to be stored in the remote user's `authorized_keys` file.

The easiest method is:

```bash
ssh-copy-id -i ~/.ssh/id_ed25519.pub devops@192.168.1.20
```

This command:

1. Connects to the remote host.
2. Prompts for the user's password.
3. Copies the public key.
4. Configures the appropriate permissions automatically.

Afterward, access can be established using:

```bash
ssh devops@192.168.1.20
```

### Adding a Personal Key to an AWS EC2 Instance

Display your public key:

```bash
cat ~/.ssh/id_ed25519.pub
```

Copy the output and connect to the EC2 instance using the original `.pem` key.

Append the public key to the authorized keys file:

```bash
echo "paste-your-public-key-here" >> ~/.ssh/authorized_keys
```

Future connections can then use your personal SSH key instead of the AWS-generated key pair.

---

## 4. Secure File Transfers with SCP

`scp` (Secure Copy) uses SSH to transfer files securely between systems.

## 5. Uploading a File

```bash
scp -i ~/.ssh/keys/linux-lab.pem file.txt ubuntu@54.123.45.67:/home/ubuntu/
```

If SSH aliases are configured:

```bash
scp file.txt aws-lab:/home/ubuntu/
```

---

## 6. Downloading a File

```bash
scp aws-lab:/var/log/syslog ./syslog-backup.log
```

---

## 7. Copying Directories Recursively

```bash
scp -r my-directory/ aws-lab:/home/ubuntu/
```

The `-r` option enables recursive directory transfers.

---

## 8. Efficient Synchronization with rsync

While `scp` copies all files during every transfer, `rsync` synchronizes only the differences between source and destination.

This significantly reduces transfer time and bandwidth consumption for large datasets.

---

## 9. Installation

```bash
sudo apt install rsync -y
```

---

## 10. Synchronizing a Local Directory to a Remote Server

```bash
rsync -avz --progress /opt/project/ aws-lab:/opt/project/
```

### Common Options

| Option       | Description                                       |
| ------------ | ------------------------------------------------- |
| `-a`         | Archive mode (preserves metadata and permissions) |
| `-v`         | Verbose output                                    |
| `-z`         | Compresses data during transfer                   |
| `--progress` | Displays transfer progress                        |

---

## 11. Synchronizing from Remote to Local

```bash
rsync -avz aws-lab:/var/log/nginx/ /tmp/nginx-logs/
```

---

## 12. Excluding Files and Directories

```bash
rsync -avz \
  --exclude='.git' \
  --exclude='node_modules' \
  /opt/project/ aws-lab:/opt/project/
```

This is commonly used to avoid transferring source control metadata, build artifacts, or dependency directories.

---

## 13. Creating a Mirror Copy

```bash
rsync -avz --delete /opt/project/ aws-lab:/opt/project/
```

The `--delete` option removes files from the destination that no longer exist in the source.

> **Warning:** Use this option carefully, as deletions are propagated to the target system.

---

## 14. Performing a Dry Run

Before executing a synchronization operation, especially when using `--delete`, simulate the changes:

```bash
rsync -avzn /opt/project/ aws-lab:/opt/project/
```

The `-n` option performs a dry run and displays the actions that would be executed without modifying any files.

---

## 15. Common rsync Use Cases

`rsync` is widely used for:

* Application deployments
* Incremental backups
* Log synchronization
* Environment migrations
* Data replication
* Large-scale file transfers

Because it transfers only changed data and preserves filesystem metadata, it remains one of the most important tools in Linux administration, DevOps, and Site Reliability Engineering (SRE).

---

## Important Commands from This Lesson

| Command | Purpose |
|---|---|
| `vim ~/.ssh/config` | Edit the SSH client config file to create reusable connection aliases. |
| `ssh HOST_ALIAS` | Connect using a `Host` alias defined in `~/.ssh/config`. |
| `ssh-keygen -t ed25519 -C "comment"` | Generate a new Ed25519 SSH key pair. |
| `ssh-copy-id -i ~/.ssh/id_ed25519.pub user@host` | Copy a public key to a remote host's `authorized_keys` file and set permissions automatically. |
| `cat ~/.ssh/id_ed25519.pub` | Print a public key so it can be copied manually (e.g. onto an EC2 instance). |
| `echo "KEY" >> ~/.ssh/authorized_keys` | Append a public key to the authorized keys file by hand. |
| `scp file.txt user@host:/path` | Upload a file to a remote host over SSH. |
| `scp user@host:/path/file ./` | Download a file from a remote host over SSH. |
| `scp -r dir/ user@host:/path` | Copy a directory recursively over SSH. |
| `sudo apt install rsync -y` | Install `rsync`. |
| `rsync -avz --progress SRC DEST` | Synchronize only the differences between source and destination, with progress output. |
| `rsync -avz --exclude='PATTERN' SRC DEST` | Synchronize while excluding matching files or directories. |
| `rsync -avz --delete SRC DEST` | Mirror the source, removing destination files that no longer exist in the source. |
| `rsync -avzn SRC DEST` | Dry run: show what `rsync` would do without changing any files. |

---

## Key Takeaways

* An SSH config file (`~/.ssh/config`) lets you define per-host aliases (`Host`, `HostName`, `User`, `IdentityFile`) so you can connect with a short name instead of retyping the full `ssh -i ... user@ip` command every time.
* `ssh-keygen` generates a personal key pair (Ed25519 is the modern default); the private key must never be shared, while the public key can be freely distributed to systems that should trust your identity.
* `ssh-copy-id` is the standard way to install your public key on a remote server's `authorized_keys` file; on providers like AWS EC2 that don't support it directly, the key can instead be appended manually after connecting with the original `.pem` key.
* `scp` copies files and directories (with `-r`) over SSH, transferring the full content every time.
* `rsync` synchronizes only the differences between source and destination, making it far more efficient than `scp` for large or repeated transfers: `-a` preserves metadata, `-z` compresses, `--exclude` skips unwanted paths, `--delete` mirrors the source exactly, and `-n` previews changes without applying them.
* Because of its efficiency and the `--delete`/dry-run safety net, `rsync` is generally the preferred tool for deployments, backups, and large-scale file synchronization in Linux administration and SRE work.

---
