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

### Set a Static IP Address

1. In the Server Manager, click on `Local Server`.

    - Once there, take note of the `Computer name`. If you haven't changed it, now would be a good time.
        1. Click on the name of the computer.
        2. Then select `Change` to rename this computer.
        3. Change the computer name. You must restart the server for settings to take effect.
 
2. Beside Ethernet: select `IPv4 address assigned by DHCP, IPv6 enabled`

    - Troubleshooting
        1. Shut down the server
        2. Change the NIC device model to `e1000e`
        3. Apply the settings
        4. Start the Windows Server

3. Right click on the adapter and select `Properties`.

4. Select `Internet Protocol Version 4 (TCP/IPv4)` and click on `Properties`.

5. Because this is a Server, we want it to have a static IP address. The isolated virtual network I'm using is `192.168.40.0/24`.

- I will be using these IP settings:
    - IP Address: `192.168.40.10`
    - Subnet mask: `255.255.255.0` (/24)
    - Default gateway: leave blank for now
    - Preferred DNS server: `192.168.40.10` (the IP address of the server)


