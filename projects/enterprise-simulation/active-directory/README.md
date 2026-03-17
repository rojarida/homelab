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

    ![server manager](./screenshots/01-server-manager.png)

- Once there, take note of the `Computer name`. If you haven't changed it, now would be a good time.
    1. Click on the name of the computer.
    2. Then select `Change` to rename this computer.

    ![system properties](./screenshots/02-system-properties.png)

    3. Change the computer name. You must restart the server for settings to take effect.

    ![change computer name](./screenshots/03-computer-name-domain-change.png)

2. Beside Ethernet: select `IPv4 address assigned by DHCP, IPv6 enabled`

    ![select ethernet](./screenshots/04-select-ethernet.png)

    - Troubleshooting
        1. Shut down the server
        2. Change the NIC device model to `e1000e`
        3. Apply the settings
        4. Start the Windows Server

3. Right click on the adapter and select `Properties`.

    ![right click adapter](./screenshots/05-right-click-adapter.png)

4. Select `Internet Protocol Version 4 (TCP/IPv4)` and click on `Properties`.

    ![click on ipv4](./screenshots/06-select-ipv4.png)

5. Because this is a Server, we want it to have a static IP address. The isolated virtual network I'm using is `192.168.40.0/24`.

- I will be using these IP settings:
    - IP Address: `192.168.40.10`
    - Subnet mask: `255.255.255.0` (/24)
    - Default gateway: leave blank for now
    - Preferred DNS server: `192.168.40.10` (the IP address of the server)

    ![set static ip](./screenshots/07-set-static-ip.png)

## Install the Active Directory Domain Services

### 1. Open Server Manager.

### 2. In the top right, select `Manage` and then `Add Roles and Features`.

![add roles and features](./screenshots/08-add-roles-and-features.png)

### 3. Click `Next` on the opening page.

![before you begin](./screenshots/09-before-you-begin.png)

### 4. For the installation type, select `Role-based or featured-based installation` and then click `Next`.

![select installation type](./screenshots/10-installation-type.png)

### 5. Select the local server and then click `Next`.

![select destination server](./screenshots/11-server-selection.png)

### 6. On Server Roles, check `Active Directory Domain Services`.

![check active directory domain services](./screenshots/12-select-ad-ds.png)

### 7. Then select `Add features` on the window that pops up.

![add adds features](./screenshots/13-ad-features.png)

### 8. Once `Active Directory Domain Services` is checked, click `Next`.

### 9. For features, default is fine. Click `Next`.

![select features](./screenshots/14-select-features.png)

### 10. On `Active Directory Domain Services`, click `Next`.

![active directory domain services](./screenshots/15-active-directory-domain-services.png)

### 11. On `Confirm installation selections`, click `Install`.

![confirm installation selections](./screenshots/16-confirm-installation-selections.png)

### 12. Once `Active Directory Domain Services` installed successsfuly, click `Close`.

![adds installed](./screenshots/17-ad-ds-installation-succeeded.png)

### 13. Click the flag with the yellow triangle in the top right of `Server Manager`.

### 14. Select `Promote this server to a domain controller`.

![select flag with yellow triangle](./screenshots/18-click-flag-yellow-triangle.png)

### 15. Select `Add a new forest`.

### 16. Enter a `Root domain name`. I will be using `corp.example.com`. Click `Next`.
> [!warning]
> Avoid using `.local` as it may conflict with multicast DNS.

![deployment configuration](./screenshots/19-root-domain-name.png)

### 17. On `Domain Controller Options`, default is fine. Create your password, then click `Next`.

![domain controller options](./screenshots/20-domain-controller-options.png)

### 18. Leave `DNS delegation` unchecked, then click `Next`.

![dns options](./screenshots/21-dns-delegation.png)

### 19. Verify the NetBIOS domain name. I will be using `CORP`. Click `Next`.

![netbios domain name](./screenshots/22-netbios-domain-name.png)

### 20. On `Paths`, default is fine. Click `Next`.

![adds paths](./screenshots/23-ad-ds-paths.png)

### 21. Review the options, then click `Next`.

![review options](./screenshots/24-review-options.png)

### 22. On `Prerequisites Check`, click `Install`.

![prerequisites check](./screenshots/25-prerequisites-check.png)

## Log into domain Administrator account

After you installed Active Directory Domain Services, you should see the domain you selected followed by the built-in Administrator account. This is the same account that you used previously, it's now joined to the domain.

![domain administrator account](./screenshots/26-after-ad-ds-installs.png)

## Verify

1. You should have been able to login using the built-in Administrator account on the domain.

2. Confirm the hostname is still the same. You should see that `WORKGROUP` changed into `Domain` and has the Root domain name that you created.

    ![verify hostname and domain](./screenshots/27-verify-server-and-domain.png)

3. On command prompt, run `ipconfig /all`. You should notice a couple of things:
    - Host name: The hostname configured
    - Primary DNS Suffix: The domain configured
    - IPv4 Address: The static IP address configured
    - Subnet Mask: `255.255.255.0` (/24)
    - NetBIOS over TCPIP: `Enabled`

    ![verify network settings](./screenshots/28-verify-network-settings.png)

## Congratulations!

You've successfully configured Active Directory Domain Services and promoted the Windows Server VM to a domain controller for the `corp.example.com` enterprise simulation lab. The server can now provide centralized identity and directory services for the isolated environment.

## Related

- [Join a Windows 11 client](../windows-11-client/tasks/join-domain.md)
- [Create a domain user](./tasks/create-user.md)
- [Create Organizational Units](./tasks/create-organizational-units.md)
- [Create Group Policy](./tasks/create-group-policy.md)
