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
