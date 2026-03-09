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
- `Memory`: 4096
- `CPU`: 2
- `Disk`: 40 GB
- `Network`: NAT

