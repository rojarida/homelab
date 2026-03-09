# Windows Server 2025 VM Setup

This document walks through creating and installing a fresh Windows Server 2025 virtual machine from scratch using `QEMU/KVM` and `virt-manager`.

## Goal

The purpose of this VM is to create a clean Windows Server 2025 installation that can later serve as a reference for future homelab projects.

For this setup, I will keep configuration simple and focus on:

- Successful VM creation
- Successful OS installation
- Initial boot and login
- Post-install verification
- Screenshots and documentation

This setup focuses only on getting a basic standalone Windows Server 2025 VM installed and working.

## Prerequisites

Before starting, ensure the following:

- QEMU/KVM is installed on the host (see: [steps 1 - 4](../ubuntu-vm/README.md#1-update-the-host))
- virt-manager is installed
- Virtualization is enabled
- Windows Server 2025 is downloaded
- Available host resources for VM

## Windows Server 2025 VM Settings

- `Host System`: Linux Mint
- `Hypervisor`: QEMU/KVM and virt-manager
- `Guest OS`: Windows Server 2025 Standard
- `Install Type`: Desktop Experience
- `VM Name`: windows-server-2025
- `Memory`: 8192
- `CPU`: 4
- `Disk`: 40 GB
- `Network`: NAT

## 1. Create the Virtual Machine

Open `virt-manager` and create a new virtual machine.

### Create a new virtual machine

Select `Local install media (ISO image or CDROM)`.

### Browse for the ISO

Browse to the ISO and select it.

`virt-manager` should automatically detect the operating system you are installing.
    - In this case, we're installing Windows Server 2025 but `virt-manager` shows Windows Server 2022, which is the closest match.

### Choose the Memory and CPU settings

Set the VM resources.

For this build, I used:
    - `Memory`: 8GB
    - `CPUs`: 4

### Create the virtual disk

Create the storage for the virtual machine.

For this build, I used:
    - `Storage`: 40GB

### Name the VM and Review

I will be using the `default` network selection.

You can optionally customize configuration before installing; however, we will just proceed.


