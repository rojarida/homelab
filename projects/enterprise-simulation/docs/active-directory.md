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

## Install the Active Directory Domain Services

1. Open Server Manager.
2. In the top right, select `Manage` and then `Add Roles and Features`.
3. Click `Next` on the opening page.
4. For the installation type, select `Role-based or featured-based installation` and then click `Next`.
5. Select the local server and then click `Next`.
6. On Server Roles, check `Active Directory Domain Services`.
7. Then select `Add features` on the window that pops up.
8. Once `Active Directory Domain Services` is checked, click `Next`.
9. For features, default is fine. Click `Next`.
10. On `Active Directory Domain Services`, click `Next`.
11. On `Confirm installation selections`, click `Install`.
12. Once `Active Directory Domain Services` installed successsfuly, click `Close`.
13. Click the flag with the yellow triangle in the top right of `Server Manager`.
14. Select `Promote this server to a domain controller`.
15. Select `Add a new forest`.
16. Enter a `Root domain name`. I will be using `corp.example.com`. Click `Next`.
    - Avoid using `.local` as it may conflict with multicast DNS.
17. On `Domain Controller Options`, default is fine. Create your password, then click `Next`.
18. Leave `DNS delegation` unchecked, then click `Next`.
19. Verify the NetBIOS domain name. I will be using `CORP`. Click `Next`.
20. On `Paths`, default is fine. Click `Next`.
21. Review the options, then click `Next`.
22. On `Prerequisites Check`, click `Install`.

## Log into domain Administrator account

After you installed Active Directory Domain Services, you should see the domain you selected followed by the built-in Administrator account. This is the same account that you used previously, it's now joined to the domain.
