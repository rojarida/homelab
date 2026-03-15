# Windows 11 Join Domain

This document covers how to join a Windows 11 VM to an Active Directory domain.

At this point, the environment should have the following:

- Windows Server VM installed
- Active Directory Domain Services configured
- Server promoted to a Domain Controller (DC)
- Clean Windows 11 VM installation

## Prerequisites

Before continuing, complete the following:

- [Windows Server 2025 Setup](../../../../virtualization/windows-server-2025/README.md)
- [Active Directory Setup](../../active-directory/README.md)
- [Windows 11 VM Setup](../../../../virtualization/windows-11/README.md)

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

- Client has an IP on the same lab network (`192.168.40.0/24`).

![verify network settings](./screenshots/w11-join-domain/01-verify-network-settings.png)

- DNS Server is set to the domain controller's IP.
- Client can ping the server by IP.
- Client should be able to ping the server by hostname.

![test server connectivity](./screenshots/w11-join-domain/02-verify-connectivity.png)

## 2. Open the domain join settings

### Right click the start menu and select `Settings`.

![open settings](./screenshots/w11-join-domain/03-settings.png)

### Go to `System`.

![open system](./screenshots/w11-join-domain/04-system.png)

### Scroll down and select `About`.

### Then under `Device specifications`, scroll down and select `Domain or workgroup`.

![select domain or workgroup](./screenshots/w11-join-domain/05-domain-or-workgroup.png)

### To change the domain, select `Change`.

![change domain](./screenshots/w11-join-domain/06-system-properties.png)

### Then at the bottom, change `Member of.. Domain:` to the domain name when creating the Windows Server.

![member of domain](./screenshots/w11-join-domain/07-member-of-domain.png)

It will then ask you for an account with permission to join the domain. Log in with your Windows Server administrator account.

In my case:
- Username: `CORP\Administrator`
- Password: `...`

![account with permissions](./screenshots/w11-join-domain/08-account-with-permission.png)

After authenticating, you should be welcomed to the domain.

![domain welcome message](./screenshots/w11-join-domain/09-successful-domain-join.png)

## 3. Reboot the Windows 11 VM

> TODO: Document creating domain account and link here.

You should now be able to join a domain account. Since we haven't configured any users, you can log in with the Administrator account.

In the bottom left, select `Other user`. Notice how it shows your NetBIOS name. Ensure you prepend this when typing in your username.

[domain login](./screenshots/w11-join-domain/10-other-user.png)

## 4. Verify login

Right click the start menu and select `Settings`.

You should see the username and domain as the logged in user!

### Congratulations. You've successfully joined a Windows VM to a domain.

![verify joined domain](./screenshots/w11-join-domain/11-verify-login.png)
