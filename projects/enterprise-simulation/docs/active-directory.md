# Active Directory

This document covers the server-side configurations steps for the enterprise simulation lab.

> [!note]
> Ensure the Windows Server VM is using a clean base installation and is connected only to the isolated lab network.

- I will be using the isolated virtual network: `192.168.40.0/24`.
    - DHCP is disabled.

## Prerequisites

Before continuing, confirm the following:

- Windows Server was installed successfully using the clean server setup guide (see: [Windows Server Setup](../../../virtualization/windows-server-2025/README.md))
- The server boots normally with no issues
- Initial updates and basic setup are complete
- The VM is attached only to the isolated virtual network
- The VM is not using NAT or a bridged adapter

## Server Network Configuration


