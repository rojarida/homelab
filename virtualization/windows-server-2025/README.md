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

- Open `virt-manager` and create a new virtual machine.

### Create a new virtual machine

- Select `Local install media (ISO image or CDROM)`.

### Browse for the ISO

- Browse to the ISO and select it.

- `virt-manager` should automatically detect the operating system you are installing.
    - In this case, we're installing Windows Server 2025. It wasn't automatically detected, so I had to manually search for it.

### Choose the Memory and CPU settings

- Set the VM resources.

- For this build, I used:
    - `Memory`: 8GB
    - `CPUs`: 4

### Create the virtual disk

- Create the storage for the virtual machine.

- For this build, I used:
    - `Storage`: 40GB

### Name the VM and Review

- I will be using the `default` network selection.

- You can optionally customize configuration before installing; however, we will just proceed.

## 2. Once Windows loads

- Start the new VM.

### Select language settings

- Proceed with your settings.

### Select keyboard settings


### Select setup option

- Since this is a fresh VM, we don't need to repair.

- Select `Install Windows Server` and make sure `I agree everything will be deleted including files, apps, and settings` is checked.

### Select Image

- For the easiest GUI-based walkthrough, select `Windows Server 2025 Standard Evaluation (Desktop Experience)`.

    - If you're comfortable with the CLI, proceed with `Windows Server 2025 Standard Evaluation`.

### Applicable notices and license terms

### Select location to install Windows Server

- Since this is a fresh VM, we will use the virtual disk. Select `Disk 0 Unallocated Space` and press Next.

### Ready to install

- Review the configuration and ensure you're installing the Windows image you want.

### Windows will now install

### Customize settings

- You will now create the Administrator account.

## 3. Login to your Administrator account

- Once logged in, proceed with Windows installation.

### Server Manager should automatically open

- I'm changing the display resolution to: `1920x1080`. The following screenshots might be enlarged.

## 4. Verify settings

### Confirm the edition and hostname

- Go to:
    - Settings -> System -> About

- Verify that the correct Windows Server installed

- Take a note of the current computer name
    - I recommend renaming it immediately

### If NAT was used, check if network is working

- Confirm the VM got an IP address
- Confirm whether it got it from DHCP
- Test internet access by pinging `google.com` and `8.8.8.8`

### Check date, time, and time zone

- Make sure the time is correct.
- This is **important** for logs, authentication, and domain services.

### Check for updates

- Go to:
    - Settings -> Windows Update

- Check if there's any available updates.

### Recommended configurations

- Rename the server
- Enable Remote Deskop
    - Located: `Settings -> System -> Remote Desktop`
    - This will make management easier in the future.

### Reboot and check if settings changed

- Check that the system is up to date
- Check if Remote Desktop is enabled
- Check that the hostname changed

## 5. Complete

- Congratulations! You've successfully installed Windows Server.
- For the purpose of this document, we will not proceed any further.
