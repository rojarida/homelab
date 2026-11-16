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

- QEMU/KVM is installed on the host (see: [steps 1 - 4](../ubuntu/README.md#1-update-the-host))
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

![create virtual machine](./screenshots/01-create-a-new-virtual-machine.png)


### Browse for the ISO

- Browse to the ISO and select it.

- `virt-manager` should automatically detect the operating system you are installing.
    - In this case, we're installing Windows Server 2025. It wasn't automatically detected, so I had to manually search for it.

![browse for iso](./screenshots/02-browse-for-iso.png)

### Choose the Memory and CPU settings

- Set the VM resources.

- For this build, I used:
    - `Memory`: 8GB
    - `CPUs`: 4

![choose memory and cpu](./screenshots/03-choose-memory-and-cpu.png)

### Create the virtual disk

- Create the storage for the virtual machine.

- For this build, I used:
    - `Storage`: 40GB

![create virtual disk](./screenshots/04-create-virtual-disk.png)

### Name the VM and Review

- I will be using the `default` network selection.

- You can optionally customize configuration before installing; however, we will just proceed.

![name and review](./screenshots/05-name-and-review.png)

## 2. Once Windows loads

- Start the new VM.
- Proceed with your settings.

### Select language settings

![select language](./screenshots/06-select-language.png)

### Select keyboard settings

![select keyboard](./screenshots/07-select-keyboard.png)

### Select setup option

- Since this is a fresh VM, we don't need to repair.

- Select `Install Windows Server` and make sure `I agree everything will be deleted including files, apps, and settings` is checked.

![select setup option](./screenshots/08-select-setup-option.png)

### Select Image

- For the easiest GUI-based walkthrough, select `Windows Server 2025 Standard Evaluation (Desktop Experience)`.

    - If you're comfortable with the CLI, proceed with `Windows Server 2025 Standard Evaluation`.

![select image](./screenshots/09-select-image.png)

### Applicable notices and license terms

- Accept the software license terms.

![accept license terms](./screenshots/10-accept-license-terms.png)

### Select location to install Windows Server

- Since this is a fresh VM, we will use the virtual disk. Select `Disk 0 Unallocated Space` and press Next.

![select install location](./screenshots/11-select-install-location.png)

### Ready to install

- Review the configuration and ensure you're installing the Windows image you want.

![ready to install](./screenshots/12-ready-to-install.png)

### Windows will now install

This might take some time. Wait until it's fully complete and **DO NOT** shutdown.

![installing windows server](./screenshots/13-installing-windows-server.png)

### Customize settings

- You will now create the Administrator account.

![create administrator user](./screenshots/14-create-administrator.png)

## 3. Login to your Administrator account

- Log in with the credentials you used.
- Once logged in, proceed with Windows installation.

![windows login screen](./screenshots/15-windows-login-screen.png)
![send diagnostic](./screenshots/16-send-diagnostic.png)

### Server Manager should automatically open

- I will be changing the display resolution to: `1920x1080`. The following screenshots might be enlarged.

![server manager dashboard](./screenshots/17-server-manager-dashboard.png)

## 4. Verify settings

### Confirm the edition and hostname

- Go to:
    - Settings -> System -> About

- Verify that the correct Windows Server installed

- Take a note of the current computer name
    - I recommend renaming it immediately

![verify os and hostname](./screenshots/18-verify-os-and-hostname.png)

### If NAT was used, check if network is working

- Confirm the VM got an IP address
- Confirm whether it got it from DHCP
- Test internet access by pinging `google.com` and `8.8.8.8`

![check ipconfig](./screenshots/19-check-ipconfig.png)
![ping google](./screenshots/20-ping-google.png)

### Check date, time, and time zone

- Make sure the time is correct.
- This is **important** for logs, authentication, and domain services.

![check time and date](./screenshots/21-check-time-and-date.png)

### Check for updates

- Go to:
    - Settings -> Windows Update

- Check if there's any available updates. There will likely be security updates as it's a fresh VM installation.

![check for updates](./screenshots/22-check-for-updates.png)

### Recommended configurations

- Rename the server
- Enable Remote Deskop
    - Located: `Settings -> System -> Remote Desktop`
    - This will make management easier in the future.

![enable remote desktop](./screenshots/23-enable-remote-desktop.png)

### Reboot and check if settings changed

- Check that the system is up to date
- Check if Remote Desktop is enabled
- Check that the hostname changed

![up to date](./screenshots/24-up-to-date.png)
![rdp and hostname](./screenshots/25-rdp-and-hostname.png)

## 5. Complete

- Congratulations! You've successfully installed Windows Server.
- For the purpose of this document, we will not proceed any further.
