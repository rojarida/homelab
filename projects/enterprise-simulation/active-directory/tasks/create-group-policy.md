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
- Test Client `WIN11-CLIENT-02`

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

Sign in to the domain-joined client with an administrative account and run:

```cmd
gpupdate /force
```

> 13

Depending on the policy, Windows may require:

- Logging back in
- Reboot

> [!important]
> Based on how we applied the GPO, what do you think will happen when restarting the client?

### 9. Verify the GPO

So, we linked the child OU `Sales` and the GPO `Department User Baseline`.

This means that as of right now, only users in `Sales` OU will receive the GPO. We can verify that here:

- Notice how Jill Estrada received the background wallpaper.
- Jill Estrada is unable to open the command prompt.
- Unable to open `Settings` or `Control Panel`.
- Testing with another user in `Sales`, we noticed the same settings have applied.

#### Now lets try logging in to the device with a user that's not in Sales

We have Guillermo Mccall.

- Does not have the background wallpaper.
- Able to open command prompt.
- Able to open `Settings`.
- Able to open `Control Panel`.

#### Notice how no Computer Configurations have been applied

Because we didn't link the GPO to the workstation, `Computer Configuration` did not get applied.

Lets link the workstation.

1. Create the child OU for `Sales`.

2. Move `WIN11-CLIENT-02` from the default `Computers` to `Workstations/Sales`.

3. Go back to `Group Policy Management`.

    1. Expand `corp.example.com`.
    2. Expand `Workstations`.
    3. Right click on `Sales`.
    4. Select `Link an Existing GPO...`

    > [!important]
    > Splitting User Configuration and Computer Configuration is easier to manage.
    >
    > In this lab, we combined the two into a single GPO.

    5. Select the GPO that we created.

### Creating a Security Group

Since we added a GPO for users in `Sales`, lets restrict the workstation so only users in `Sales` are authorized to access the workstation.

In `Active Directory Users and Computers`:

1. Right click `Groups` OU.
2. Select `New`, then select `Group`.
3. Give the security group a name. I used `Sales_Workstation_Users`.
4. Group scope: `Global`.
5. Group type: `Security`.
6. Click `OK`.

#### Add the users in Sales to the group

While still in `ADUC`:

1. Double click on `Sales_Workstation_Users`.
2. Go to `Members`.
3. Click `Add`.
4. Add the users in `Sales`.

#### Edit the GPO to allow only users from the Sales department

In `Group Policy Management`:

1. Expand:
    
    - `Forest: corp.example.com`
    - `Domains`
    - `corp.example.com`
    - `Workstations`

2. Click on `Sales`. You should see the GPO that we created.
3. Right click the GPO and `Edit`.
4. Locate `Allow log on locally` by following `Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > User Rights Assignment`.
5. Add:
    - `Administrators`
    - `Sales_Workstation_Users`

> [!caution]
> Administrators must be included or else they will be locked out.

#### Update policy on client

On the `Sales` workstation, log in as an administrator then run:

```cmd
gpupdate /force
```

After restarting, you should notice the `Computer Configuration` that we created in the GPO.

- The logon title/message should now appear
- You no longer see last signed-in user in the bottom left.

#### Only users in the Sales department can log into this workstation

You can test this by logging in with a user in another department.

## Congratulations!

You've successfully implemented Group Policy in Active Directory!

## Conclusion

This document showed the full workflow of creating, linking, applying, and verifying Group Policy in Active Directory. By testing the policy on the `Sales` OU and a domain-joined client, it became easier to understand how `User Configuration` and `Computer Configuration` are applied based on where objects are located.

This is also a good reminder that OUs and groups serve different purposes:

- OUs: Organize objects and scope policy
- Groups: Used to manage permissions and access.
