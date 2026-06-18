# Module 1: Hybrid Lab Environment and SSH Fundamentals

## Overview

Modern infrastructure is built around Linux-based systems running in cloud environments, virtual machines, and containers. Understanding how these components interact is essential for anyone working with Cloud, DevOps, Platform Engineering, or Kubernetes.

This module introduces the foundational concepts behind Linux servers, virtualization, cloud computing, and the mindset required to operate modern infrastructure.

---

# 1.1 Cloud-Native Mindset

## Why Linux Matters

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

## Linux Desktop vs Linux Server

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

## Understanding Virtualization

Virtualization allows multiple virtual machines (VMs) to run on a single physical server.

Each VM operates as if it owns dedicated hardware resources:

* CPU
* Memory
* Storage
* Network interfaces

In reality, these resources are managed by a software layer called a **hypervisor**.

---

## Hypervisor Types

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

## What Happens When a Virtual Machine Starts?

When a virtual machine is created:

1. The hypervisor allocates CPU resources.
2. Memory is reserved for the VM.
3. Virtual storage is attached.
4. Virtual network interfaces are created.
5. The guest operating system boots as if it were running on dedicated hardware.

For example, a VM configured with a 20 GB disk may actually be backed by a file stored on the host machine.

The virtualization layer abstracts the physical hardware and presents virtualized resources to the guest operating system.

---

## Virtual Machines vs Containers

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

# Cloud Computing Fundamentals

## What Happens When You Launch a Cloud Instance?

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

## Local Virtualization vs Cloud Infrastructure

| Aspect       | Local Virtual Machine         | Cloud Virtual Machine            |
| ------------ | ----------------------------- | -------------------------------- |
| Cost         | Uses local hardware resources | Consumption-based pricing        |
| Performance  | Limited by local hardware     | Scalable through instance sizing |
| Network      | Local network                 | Global connectivity              |
| Storage      | Local disk files              | Managed block storage services   |
| Availability | Dependent on host uptime      | Designed for high availability   |
| Provisioning | Manual                        | API-driven and automated         |

---

# Pets vs Cattle

One of the most important cloud-native concepts is the distinction between **Pets** and **Cattle**.

## Pets

Traditional servers are treated as unique systems:

* Individually configured
* Manually maintained
* Given meaningful names
* Difficult to replace

If a server fails, significant effort is invested in recovering it.

---

## Cattle

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

# 1.2 Local Lab Environment: VirtualBox and Ubuntu Server

## Installing VirtualBox

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

## Downloading Ubuntu Server

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

## Why Build a Local Lab?

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

# 1.3 Local Lab Environment: VirtualBox and Ubuntu Server

## Creating the Virtual Machine

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

## Network Configuration

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

## Installing Ubuntu Server

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

## Storage Configuration and LVM

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

## User Configuration

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

## SSH Configuration

During installation, enable:

```text
Install OpenSSH Server
```

This component is required for remote administration and will be used extensively throughout the training.

Without OpenSSH Server, remote terminal access will not be available.

---

## Optional Software Packages

Skip the optional featured Snap packages during installation.

A minimal server installation provides:

* Lower resource consumption
* Reduced attack surface
* Easier maintenance
* Faster updates

---

## Understanding the First Boot Process

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

# 1.4 SSH: The Essential Remote Access Tool

With both your local VM and cloud instance running, the next step is connecting to them remotely using SSH.

---

## What is SSH?

**SSH (Secure Shell)** is an encrypted network protocol used for secure communication between computers. It follows a **client-server architecture**:

* **SSH Server (`sshd`)** runs on the target machine and listens for incoming connections (port **22** by default).
* **SSH Client (`ssh`)** is the command-line tool used to initiate a connection from your local machine.

All traffic is encrypted, protecting credentials and data from interception when accessing systems over local networks or the public internet.

---

## Connecting to a Virtual Machine

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

In production environments, always verify the server fingerprint through a trusted channel before accepting it. This helps prevent **Man-in-the-Middle (MITM)** attacks.

After accepting the fingerprint, SSH prompts for the user's password.

### Using NAT with Port Forwarding

If the VM uses **NAT networking** and port forwarding is configured (host port `2222` → guest port `22`), connect using:

```bash
ssh -p 2222 devops@127.0.0.1
```

---

# Initial System Verification

After establishing the connection, verify that the system is functioning correctly and become familiar with basic administrative commands.

## Check the Current User

Display the account currently logged into the system:

```bash
whoami
```

Example output:

```text
devops
```

## Check the Hostname

Display the machine's hostname:

```bash
hostname
```

Example output:

```text
linux-lab
```

## Check Kernel Information

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

## Check Network Interfaces and IP Addresses

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

## Update the System

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

## Check Disk Usage

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

## Expanding an LVM Volume

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
