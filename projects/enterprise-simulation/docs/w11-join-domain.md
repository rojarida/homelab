# Windows 11 Join Domain

This document covers how to join a Windows 11 VM to an Active Directory domain.

At this point, the environment should have the following:

- Windows Server VM installed
- Active Directory Domain Services configured
- Server promoted to a Domain Controller (DC)
- Clean Windows 11 VM installation

## Prerequisites

Before continuing, complete the following:

- [Windows Server 2025 Setup](../../../virtualization/windows-server-2025/README.md)
- [Active Directory Setup](./active-directory.md)
- [Windows 11 VM Setup](../../../virtualization/windows-11/README.md)

## Verify your environment state

- Windows Server running as the domain controller
- Both VMs are connected to the same isolated virtual network
- Windows 11 VM booted normally
- Windows 11 Edition supports domain join

In this example:

- Domain Name: `corp.example.com`
- Network: `192.168.0.40.0/24`
- Server Hostname: `WIN-SRV-01`
- Server IP: `192.168.40.10`

## 1. Confirm Basic Network Connectivity

On the Windows 11 VM, ensure it can reach the domain controller.

Verify:

- Client has an IP on the same lab network (`192.168.40.0/24`)
- DNS Server is set to the domain controller's IP
- Client can ping the server by IP
- Client should be able to ping the server by hostname


