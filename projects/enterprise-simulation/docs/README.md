# Enterprise Simulation Setup

This document covers the initial setup for the `enterprise-simulation` lab. It is focused on preparing a clean, isolated foundation before configuring services such as Active Directory, Group Policy, joining clients to the domain, and other enterprise features.

## Purpose

The goal of this setup is to create a safe test environment that simulates an isolated, enterprise Windows network. This lab is intended for learning, experimentation, troubleshooting practice, and documentation.

## Scope

This setup document covers:

- Preparing the isolated lab environment
- Creating the baseline Windows Server VM
- Creating the baseline Windows 11 Client VM
- Verifying network isolated

This document does **not** cover:

- Active Directory Domain Services configuration
- DNS or DHCP role configuration
- Joining Windows clients to the domain
- Group Policy configuration

These topics will be documented in their own dedicated files under `docs/`.

## Lab Design

This enterprise simulation is intentionally separated from the real home network. The devices that I use to administer the home network are running Ubuntu and Linux Mint. As of right now, there's no benefit in implementing Active Directory in our current network configuration.

The workflow is:

- Build and test the lab in an isolated virtual environment
- Document the full process and troubleshooting steps
- Experiment safely without risking current home network

> [!note]
> This project is for lab use only. It is not intended to be deployed directly onto the home network.

## Prerequisites

Before continuing, complete the following baseline VM setup guides:

- [Windows Server 2025 Setup](../../../virtualization/windows-server-2025/README.md)
- [Windows 11 VM Setup](../../../virtualization/windows-11/README.md)

> ![note]
> For this enterprise simulation, these guides should be followed only up to the base installation and initial OS preparation stage.

## Virtual Machine Inventory

The initial enterprise simulation should be simple.

### 1. Windows Server VM

This VM will act as the core lab server for services such as Active Directory, DNS, and other Windows infrastructure roles.

- `OS`: Windows Server 2025
- `Role`: Server in an isolated lab
- `State`: Clean installation

### 2. Windows 11 Client VM

This VM will be used as the domain-joined workstation for testing and experimentation.

- `OS`: Windows 11 Pro
- `Role`: Client in an isolated lab
- `State`: Clean installation

## Networking Approach

> [!note]
> The lab network should remain isolated from the real home network.

Recommended approach:

- Attach both Windows VMs to the same isolated virtual network
- Do not bridge the lab directly into the home LAN
- Keep the environment self-contained until lab services are configured

This prevents accidental conflicts with the home router and existing DHCP services.

## Initial Setup Checklist

After both VMs are created from their clean setup guides, confirm the following:

- Both VMs boot successfully
- Both VMs are connected to the intended isolated virtual network
- Both VMs have their clean baseline setup completed
- Neither VMs is being used on the home network

## Naming Conventions

> [!tip]
> Using consistent names will make configuration easier to follow.

This is the naming scheme I will be using:

- Server VM: `WIN-SRV-01`
- Client VM: `WIN11-CLIENT-01`

## Documentation Notes

- [Active Directory Setup](./active-directory/README.md): Promoting the server and configuring AD DS
- [Join a Windows 11 client](./active-directory/tasks/w11-join-domain.md): Joining the Windows 11 VM to the domain
- `docs/group-policy.md`: Testing and documenting policy changes
- [Troubleshooting](./troubleshooting.md): Issues, fixes, and lessons learned
