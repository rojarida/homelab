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

![create virtual machine](./screenshots/01-create-virtual-machine.png)

### Browse for the ISO

- Browse to the location where the Windows 11 ISO is located and select it.
- `virt-manager` should automatically detect the operating system you are installing.
    - In this case, we're installing Microsoft Windows 11.

![select the iso](./screenshots/02-select-the-iso.png)

### Choose the Memory and CPU settings

- Set the VM resources.

![choose memory and cpu](./screenshots/03-choose-memory-and-cpu.png)

### Create the virtual disk

- Create a disk image for the virtual machine.

![create virtual disk](./screenshots/04-create-virtual-disk.png)

### Name the VM and Review

- The network selection will be dependent on the use for the client.

![review vm](./screenshots/05-review-vm.png)

### If you run into this screen, press any key.

![press any key](./screenshots/06-press-any-key.png)

## 2. Once Windows loads

- Start the new VM.
- Proceed with your settings.

### Select language settings

![select language settings](./screenshots/07-select-language-settings.png)

### Select keyboard settings

![select keyboard settings](./screenshots/08-select-keyboard-settings.png)

### Select setup option

- Since this is a fresh VM, we don't need to repair.

- Select `Install Windows 11` and make sure `I agree everything will be deleted including files, apps, and settings` is checked.

![select setup option](./screenshots/09-select-setup-option.png)

### Product key

- Since this is a client VM, we won't be needing a product key.

- At the bottom, select `I don't have a product key`

![product key](./screenshots/10-product-key.png)

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

![select image](./screenshots/11-select-image.png)

### Applicable notices and license terms

- Accept the software license terms.

![license terms](./screenshots/12-license-terms.png)

### Select location to install Windows 11

- Since this is a fresh VM, we will use the virtual disk. Select `Disk 0 Unallocated Space` and press Next.

![select location for windows 11](./screenshots/13-select-location-for-w11.png)

### Ready to install

- Review the configuration and ensure you're installing the Windows image you want.

![ready to install](./screenshots/14-ready-to-install.png)

### Windows will not install

- This might take some time.

> [!warning]
> Do not shutdown.

![installing windows](./screenshots/15-installing-windows.png)

## 3. Continue with Windows installation

### Select country or region

![select country](./screenshots/16-select-country.png)

### Select keyboard layout or input method

![select keyboard layout](./screenshots/17-select-keyboard-layout.png)

### Option to add second keyboard layout

![second keyboard layout](./screenshots/18-second-keyboard-layout.png)

### Name your device

- I will be naming the device `lab-client-01`.

> [!note]
> This is different from the virtual machine name.

![name your device](./screenshots/19-name-your-device.png)

### Set up for personal or organization

> [!note] 
> Depending on the project, select the appropriate type.

- We will continue `Set up for personal use`.

![set up device](./screenshots/20-set-up-device.png)

### Windows will now download

- This will take some time.

> [!warning]
> Do not shutdown.

![downloading steps](./screenshots/21-downloading-steps.png)

### Unlock your Microsoft experience

![microsoft experience](./screenshots/22-microsoft-experience.png)

### Add your Microsoft account

- I will be logging in to a Microsoft account to show the complete set up process.

![add microsoft account](./screenshots/23-add-microsoft-account.png)

### Create a PIN

![create a pin](./screenshots/24-create-a-pin.png)

### Choose privacy settings

- Select the settings and Accept

![privacy settings](./screenshots/25-privacy-settings.png)

### Getting things ready for you.

- Almost there!

![getting things ready](./screenshots/26-getting-things-ready.png)

### Customize your experience

- I will be selecting `Skip` here.

![customize experience](./screenshots/27-customize-experience.png)

### Use your phone from your PC

I will not be showing a screenshot for this screen.

### Always have access to your recent browsing data

![recent browsing data](./screenshots/28-access-to-browsing-data.png)

### Microsoft 365 promotions

![microsoft 365 trial](./screenshots/29-microsoft-365-trial.png)
![more cloud storage](./screenshots/30-more-cloud-storage.png)
![game pass premium](./screenshots/32-game-pass.png)

### Use Microsoft 365 for free

![use microsoft 365 for free](./screenshots/31-use-microsoft-365-for-free.png)

## Congratulations!

- You've successfully set up a clean virtual machine installation of Windows 11.

![windows 11 desktop](./screenshots/33-desktop.png)
