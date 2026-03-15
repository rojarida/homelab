# pfSense for Enterprise Simulation

This documents how pfSense is configured for the `enterprise-simulation` lab.

> [!note]
> This is **not** a pfSense installation guide. (See: [pfSense Setup](../../../pfSense/setup/README.md))

## Overview

pfSense is used as the:

- Default Gateway
- Firewall
- DHCP Server
- Path to upstream internet access

The domain controller will handle:

- Active Directory
- DNS for the domain
- Authentication
- Group Policy

## DNS Note

> [!note]
> Even though pfSense provides DHCP, **domain clients should use the domain controller as their DNS server**.

To clarify:

- pfSense hands out IP addresses
- pfSense hands out the **domain controller IP as DNS**
- Clients query the domain controller for DNS
- Domain controller forwards unknown queries upstream

## Lab Layout

### WAN

The WAN interface should connect to an upstream network (NAT).

### LAN

The LAN interface should still remain as an isolated, internal lab network.

This network will contain:

- pfSense LAN
- Windows Server 2025 domain controller
- Windows 11 domain-joined VM

## Networking Addressing

- Network: `192.168.40.0/24`
- pfSense LAN: `192.168.40.1`
- Domain Controller: `192.168.40.10`
- DHCP Range: `192.168.40.100 - 192.168.40.199`

## Prerequisites

Before continuing, ensure that:

- pfSense is already installed
- WAN and LAN interfaces are assigned
    - WAN is connected to an upstream network
    - LAN is connected to an isolated lab network
- Windows Server 2025 VM exists
- Both VMs can be placed on the pfSense LAN
