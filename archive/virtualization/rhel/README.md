# Red Hat Enterprise Linux VM Setup

This documents walks through creating and installing a fresh RHEL VM from scratch using `QEMU/KVM` and `virt-manager`.

## Goal

The purpose of this VM is to create a clean RHEL installation that will be used as my lab environment for preparing for RHCSA

## Prerequisites

Before starting, ensure the following:

- QEMU/KVM is installed on the host (see: [steps 1 - 4](../ubuntu/README.md#1-update-the-host))
- virt-manager is installed
- RHEL DVD-ISO is downloaded
- Available host resources for VM

## RHEL VM Settings

- `Host System`: Linux Mint
- `Hypervisor`: QEMU/KVM and virt-manager
- `Guest OS`: RHEL 10.1
- `VM Name`: rhel
- `Memory`: 8192
- `CPU`: 4
- `Disk`: 50 GB
- `Network`: NAT

## 1. Create the Virtual Machine

- Open `virt-manager` and create a new virtual machine.

![virt-manager](./screenshots/01-virt-manager.png)

### Create a new virtual machine

- Select `Local install media (ISO image or CDROM)`.

![create virtual machine](./screenshots/02-create-a-new-vm.png)

### Browse for the ISO

- Browse to the ISO and select it.

- `virt-manager` should automatically detect RHEL.

![select rhel dvd iso](./screenshots/03-select-rhel-dvd-iso.png)

### Choose the Memory and CPU settings

- Set the VM resources.
- 2GB RAM is sufficient.


![choose memory and cpu](./screenshots/04-select-memory-and-cpu.png)

### Create the disk image

- Create the storage for the virtual machine.
- 20GB is sufficient

![create virtual disk](./screenshots/05-create-disk.png)

### Name the VM and Review

- You can optionally customize configuration before installing.

> ![note]
> RHCSA is conducted without internet access.

## 2. RHEL Setup

- You will be greeted with GRUB.
- Proceed with `Install Red Hat Enterprise Linux 10.1`

![grub](./screenshots/07-bootloader.png)

### Select language

![select language](./screenshots/08-select-language.png)

### Installation Summary

- You need to configure a user and installation destination before proceeding.

> ![warning]
> Root Account should remain disabled.

#### Create User

- Make sure `Add administrative privileges to this user account` is selected.

![create user](./screenshots/10-create-user.png)

#### Installation Destination

- Ensure the virtual disk is selected.
- Storage configuration can remain automatic.

![installation destination](./screenshots/11-installation-destination.png)

#### Network and Host Name

- Optionally change host name.
  - Default would be `localhost.local`

### Begin Installation

- Once you've configured a user account and selected an installation destination, select `Begin Installation`

![begin installation](./screenshots/13-begin-installation.png)

### Installation Complete

- Once installation is complete, you may reboot the system.

![installation complete](./screenshots/14-installation-complete.png)

### Login Screen

- Your user account should show up on the login screen.

![login screen](./screenshots/15-login-screen.png)

### Welcome Screen

- You should be welcomed to RHEL.
- Skip the welcome screen.

![welcome screen](./screenshots/16-welcome-screen.png)

### System Not Registered

> ![important]
> Do not register system.

- Internet access is required to register system. During RHCSA, you have no internet access.

## Installing with custom partitioning

- The steps are exactly the same until you reach the summary installation.

### Installation Destination (Custom Partitioning)

- This time, select `Custom` for Storage Configuration.

![custom storage configuration](./screenshots/18-custom-configuration.png)

### Manual Partitioning

- Change the partitioning scheme to `Standard Partition`.

- You must now create mount points for critical Linux data.

- Click the `+` sign to add a mount point.

![add a new mount point](./screenshots/20-add-new-mount-point.png)

#### /boot

![boot mount](./screenshots/21-boot-mount.png)

#### /boot/efi

![boot/efi mount](./screenshots/22-boot-efi.png)

> ![note]
> Notice how the File System is EFI System Partition

![efi system partition](./screenshots/23-efi-system-partition.png)

#### root

![root mount](./screenshots/24-root-mount.png)

#### swap

![swap mount](./screenshots/25-swap-mount.png)

#### log

![log mount](./screenshots/26-log-mount.png)

#### biosboot

![bios boot mount](./screenshots/27-bios-boot-mount.png)

### Review Partitions

![review partitions](./screenshots/28-review-partitions.png)

### Summary of Changes

![summary of changes](./screenshots/29-summary-of-partitions.png)

### Installation Complete

- Installation should be completed, select `Reboot System`.

![installation complete](./screenshots/14-installation-complete.png)

## Congratulations

- You've successfully installed RHEL VM using automatic partitioning and custom partitioning!

- Now go and have fun labbing with RHEL 10.

![rhel desktop](./screenshots/30-main-screen.png)
