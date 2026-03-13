# Windows 11 VM Setup

This document walks through creating and installing a fresh Windows 11 virtual machine from scratch using `QEMU/KVM` and `virt-manager`.

## Goal

The purpose of this VM is to create a clean Windows 11 installation that can later serve as a reference for future homelab projects.

For this setup, I will keep configuration simple and focus on:

- Successful VM creation
- Successful OS installation
- Initial boot and login
- Post-install verification
- Screenshots and documentation

> [!note]
> This setup focuses only on getting a basic installation of Windows 11 VM installed and working.

## Prerequisites

Before starting, ensure the following:

- QEMU/KVM is installed on the host (see: [steps 1 - 4](https://github.com/rojarida/homelab/blob/main/virtualization/ubuntu/README.md#1-update-the-host))
- virt-manager is installed
- Virtualization is enabled
- Windows 11 ISO is downloaded
- Available host resources for VM creation

## Windows 11 VM Settings

- `Host System`: Linux Mint
- `Hypervisor`: QEMU/KVM and virt-manager
- `Guest OS`: Windows 11 Pro
- `VM Name`: windows-client-01
- `Memory`: 4096
- `CPU`: 2
- `Disk`: 40 GB
- `Network`: Dependent on project

## 1. Create the Virtual Machine

- Open `virt-manager` and create a new virtual machine.

### Create a new virtual machine

- Select `Local install media (ISO image or CDROM)`

### Browse for the ISO

- Browse to the location where the Windows 11 ISO is located and select it.
- `virt-manager` should automatically detect the operating system you are installing.
    - In this case, we're installing Microsoft Windows 11.

### Choose the Memory and CPU settings

- Set the VM resources.

### Create the virtual disk

- Create a disk image for the virtual machine.

### Name the VM and Review

- The network selection will be dependent on the use for the client.

## 2. Once Windows loads

- Start the new VM.
- Proceed with your settings.

### Select language settings

### Select keyboard settings

### Select setup option

- Since this is a fresh VM, we don't need to repair.

- Select `Install Windows 11` and make sure `I agree everything will be deleted including files, apps, and settings` is checked.

### Product key

- Since this is a client VM, we won't be needing a product key.

- At the bottom, select `I don't have a product key`

### Select Image

They're different versions of Windows 11. I will briefly describe each version.

> [!note]
> Images that have `N` are equivalent to the edition (e.g. Home and Home N), but doesn't come with pre-installed media-related technologies.

- `Windows 11 Home`: Standard consumer edition for everyday personal use.
- `Windows 11 Home Single Language`: Similar to Home, but intended for systems locked to one display language.
- `Windows 11 Education`: Designed for schools and academic environments.
- `Windows 11 Pro`: Professional edition intended for business and advanced users. This is the version that we will be installing for this VM setup.
- `Windows 11 Pro Education`: A professional-based edition for schools and academic environments.
- `Windows 11 Pro for Workstations`: Built for high-performance hardware and demanding workloads like CAD, 3D animation, data science, and more.

### Applicable notices and license terms

- Accept the software license terms.

### Select location to install Windows 11

- Since this is a fresh VM, we will use the virtual disk. Select `Disk 0 Unallocated Space` and press Next.

### Ready to install

- Review the configuration and ensure you're installing the Windows image you want.

### Windows will not install

- This might take some time.

> [!warning]
> Do not shutdown.

## 3. Continue with Windows installation

### Select country or region

### Select keyboard layout or input method

### Option to add second keyboard layout

### Name your device

### Set up for personal or organization

> [!note] 
> Depending on the project, select the appropriate type.

- We will continue `Set up for personal use`.

### Windows will now download

- This will take some time.

> [!warning]
> Do not shutdown.

### Unlock your Microsoft experience

- In this setup, I will be logging into a Microsoft account to show the complete process.

### Create a PIN

### Choose privacy settings

- Select the settings and Accept

### Getting things ready for you.

### Customize your experience

- I will be selecting `Skip` here.

### Use your phone from your PC

I will not be showing a screenshot for this screen.

### Always have access to your recent browsing data

### Microsoft 365 promotions

### Use Microsoft 365 for free

## Congratulations!

- You've successfully set up a clean virtual machine installation of Windows 11.
