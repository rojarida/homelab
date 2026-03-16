# Create Group Policy in Active Directory

## Overview

This document demonstrates the standard process of creating and applying Group Policy in an Active Directory environment.

## Goal

The goal is to show how Group Policy Objects (GPOs) are created, linked to Organizational Units (OUs), applied to users or computers, and then verified on a domain-joined client.

In this lab, we will use the `Sales` department that I created in [Create Organizational Units](./create-organizational-units.md). The same process can be used for any department or OU.

## Why Group Policy?

Group Policy is used to centrally manage user and computer settings in an Active Directory domain. It allows administrators to apply configurations such as:

- Restricting access to system tools
- Controlling settings visibility
- Enforcing security and administrative standards
- Customizing desktop experience
- Many, MANY more..

A Group Policy Object becomes effective when it is linked to a site, domain, or OU containing the users or computers that should receive the policy.

Group Policy has two main sections:

- `User Configuration`: Applies to user accounts.
- `Computer Configuration`: Applies to computer accounts.

For example:

- If a policy should affect users in a department OU, link it to that department OU.
- If a policy should affect a workstation, link it to the OU containing that computer object.

## Environment

- Domain Controller: `WIN-SRV-01`
- Domain: `corp.example.com`
- Tools: `Group Policy Management Console (GPMC)`
- Test OU: `Sales`
- Test Client `WIN11-CLI-02`

## Prerequisites

- Active Directory domain is functioning properly (See: [Windows Server Setup](../README.md))
- Target OU exists (See: [Create Organizational Units](./create-organizational-units.md))
- At least one domain user exists in the OU (See: [Create Domain User](./create-user.md))
- At least one client computer is joined to the domain (See: [Join W11 Client to Domain](../../windows-11-client/tasks/join-domain.md))
- Client can communicate with the domain controller
- DNS is working correctly

## Create Group Policy

### 1. Open Group Policy Management

On the domain controller:

1. Open `Server Manager`.
2. In the top right, click on `Tools`, and select `Group Policy Management`.

> 01

This is console used to create, link, edit, and manage GPOs.

> 02

### 2. Identify the target OU

Before creating a GPO, determine where it should be applied.

In this lab, the target OU for user policy testing is the `Sales` department.

### 3. Create a new GPO

1. In Group Policy Management, expand:

    - `Forest: corp.example.com`
    - `Domains`
    - `corp.example.com`
    - `Departments`

2. Right click the target OU (`Sales`)
3. Select `Create a GPO in this domain, and Link it here...`

> 3

4. Enter a descriptive name for the GPO

    - I will be using: `Department User Baseline`

    > 4

### 4. Edit the GPO

1. Right click the newly created GPO
2. Select `Edit`

> 5

This opens the `Group Policy Management Editor`. This is where you configure the settings you want to apply.

> 6

### 5. Configure policy settings

There's an extensive list of policy settings that can be configured. Take the time to look at the different settings that can be applied to both `User Configuration` and `Computer Configuration`.

In this lab, I will be using the following policy settings:

- `User Configuration`:
    - `Prohibit access to Control Panel and PC settings`: Located `User Configuration > Policies > Administrative Templates > Control Panel`.

        > 07
        > 08

    - `Prevent access to the command prompt`: Located `User Configuration > Policies > Administrative Templates > System`.

        > 09

    - `Desktop Wallpaper`: Located `User Configuration > Policies > Administrative Templates > Desktop > Desktop`.

        > 10

- `Computer Configuration`:
    - `Do not display last signed-in user`: Located `Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options`.

        > 11

    - `Message text/title for users attempting to log on`: Located `Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options`.

        > 12

> [!note]
> The reason for these policies is because it's easy to verify on a client VM. It demonstrates how Group Policy affects both user accounts and workstations.

### 6. Confirm the GPO link

After configuration, return to `Group Policy Management` and confirm that the GPO is linked to the intended OU.

> [!tip]
> A correctly configured GPO will only apply if correctly linked.
> An example will be shown later.

### 7. Confirm target object is in the correct OU

The user or computer must exist in the OU where the GPO is linked. In this example, we only linked the GPO for the OU `Departments/Sales`. We created a `Workstations/Sales`, but we haven't linked the GPO.

### 8. Update the policy on the client

> [!warning]
> Make sure the client is joined to the domain.
> (See: [Join W11 VM to Domain](../../windows-11-client/tasks/join-domain.md))


Sign in to the domain-joined client and run:

```cmd
gpupdate /force
```

Depending on the policy, Windows may require:

- Logging back in
- Reboot

