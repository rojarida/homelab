# Ubuntu VM Setup

This document describes how I created a fresh `Ubuntu Virtal Machine` for homelab documentation, testing, and nested lab work.

This VM is intended to serve as a clean baseline environment for projects such as:

- Virtualization Practice
- Lab Rebuild Documentation
- General Linux Server Administration

---

## Environment

This Ubuntu VM was created inside my homelab environment as a clean test/documentation machine.

### Intended Purpose
- Reproducible Screenshots
- Cleaner Documentation
- Fresh Configurations
- Easier Testing

---

## Prerequisites

Before creating the VM, ensure you have:

- Working virtualization host
- Ubuntu ISO
- Available CPU, RAM, and disk space
- Access to VM manager or hypervisor

Examples of virtualization platforms:

- QEMU/KVM with virt-manager (what we will be doing)
- VirtualBox
- VMware Workstation
- Hyper-V

---

## 1. Update the Host

Before installing virtualization packages, update/upgrade your packages:

```bash
sudo apt update && sudo apt upgrade
```

## 2. Install QEMU/KVM, libvirt, and virt-manager

```bash
sudo apt install qemu-kvm libvirt-daemon-system libvirt-clients virt-manager bridge-utils
```

## 3. Add user to virtualization groups

```bash
sudo usermod -aG libvirt,kvm $USER
```

Then log out and back in for affects to take place.

## 4. Verify libvirt is responding

```bash
virsh list --all
```

## 5. Download or Locate the Ubuntu ISO

Make sure the ISO is located somewhere easy to browse.

Example:
```txt
~/vm_isos/ubuntu-22.04.5-desktop-amd64.iso
```
## 6. Setting up Ubuntu VM

Open virt-manager:

[!virt-manager main window](../screenshots/01-virt-manager.png)

### Create a new virtual machine

Select `Local install media (ISO image or CDROM)`.

[!create a new virtual machine](../screenshots/02-create-new-virtual-machine.png)

### Browse for the ISO

Browse to the ISO and select it.

virt-manager should automatically detect the operating system you are installing.
    - In this case, we're installing Ubuntu 22.04 LTS

[!browse for iso](../screenshots/03-browse-for-iso.png)

### Choose the Memory and CPU settings

Set the VM resources.

For this build, I used:
    - `Memory`: 4GB
    - `CPUs`: 2

[!choose memory and cpu](../screenshots/04-choose-memory-and-cpu.png)

### Create the virtual disk

Create the guest storage disk.

For this VM, I used:
    - `Storage`: 25GB

[!create the disk image](../screenshots/05-create-disk-image.png

### Name the VM and Review

Before selecting `Finish`:
    - Give the VM a name
    - Review configurations

[!name the virtual machine](../screenshots/06-name-the-virtual-machine.png)

## 7. Once Ubuntu loads

Start the new VM.

### Install Ubuntu

Once it boots from the ISO, the Ubuntu installer should appear.

From here, proceed by selecting `Install Ubuntu`.

[!install ubuntu](../screenshots/07-install-ubuntu.png)

### Select your keyboard layout

[!select keyboard layout](../screenshots/08-select-keyboard-layout.png)

### Proceed with normal installation

Proceed with Normal installation.

`Optionally`: Install third-party software for graphics and Wi-Fi hardware and additional media formats

[!normal installation](../screenshots/09-normal-installation.png)

### Erase disk and install Ubuntu

Since this is a VM, we can proceed with erasing the disk and installing Ubuntu.

[!erase disk and install](../screenshots/10-erase-disk-and-install.png)

### Select your timezone

Select your timezone.

[!select timezone](../screenshots/11-select-timezone.png)

### Configure your user

Enter your user account details.

[!configure user](../screenshots/12-configure-your-user.png)

## 8. Reboot

[!reboot](../screenshots/13-reboot.png)

Congrats! You've successfully virtualized Ubuntu!

[!congrats](../screenshots/14-congrats.png)
