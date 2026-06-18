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
┌─────────┐  ┌─────────┐  ┌─────────┐
│   VM 1  │  │   VM 2  │  │   VM 3  │
├─────────┤  ├─────────┤  ├─────────┤
│         TYPE 1 HYPERVISOR          │
├────────────────────────────────────┤
│          PHYSICAL HARDWARE         │
└────────────────────────────────────┘
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
┌─────────┐  ┌─────────┐
│   VM 1  │  │   VM 2  │
├─────────┤  ├─────────┤
│      TYPE 2 HYPERVISOR      │
├─────────────────────────────┤
│       HOST OPERATING SYSTEM │
│    (Windows/macOS/Linux)    │
├─────────────────────────────┤
│       PHYSICAL HARDWARE     │
└─────────────────────────────┘
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
