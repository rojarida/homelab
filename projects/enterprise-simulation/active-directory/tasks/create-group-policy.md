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

![open group policy management](./screenshots/create-group-policy/01-open-group-policy-management.png)

This is console used to create, link, edit, and manage GPOs.

[group policy management window](./screenshots/create-group-policy/02-group-policy-management-window.png)

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

![expand target ou](./screenshots/create-group-policy/03-expand-target-ou.png)

4. Enter a descriptive name for the GPO

    - I will be using: `Department User Baseline`

    ![create new gpo](./screenshots/create-group-policy/04-create-new-gpo.png)

### 4. Edit the GPO

1. Right click the newly created GPO
2. Select `Edit`

![edit the gpo](./screenshots/create-group-policy/05-edit-the-gpo.png)

This opens the `Group Policy Management Editor`. This is where you configure the settings you want to apply.

![group policy management editor](./screenshots/create-group-policy/06-group-policy-management-editor.png)

### 5. Configure policy settings

There's an extensive list of policy settings that can be configured. Take the time to look at the different settings that can be applied to both `User Configuration` and `Computer Configuration`.

In this lab, I will be using the following policy settings:

- `User Configuration`:
    - `Prohibit access to Control Panel and PC settings`: Located `User Configuration > Policies > Administrative Templates > Control Panel`.

    ![prohibit control panel](./screenshots/create-group-policy/07-prohibit-control-panel.png)
    ![enable prohibit control panel](./screenshots/create-group-policy/08-enable-prohibit-control-panel.png)

    - `Prevent access to the command prompt`: Located `User Configuration > Policies > Administrative Templates > System`.

    ![prevent access to command prompt](./screenshots/create-group-policy/09-prevent-access-to-command-prompt.png)

    - `Desktop Wallpaper`: Located `User Configuration > Policies > Administrative Templates > Desktop > Desktop`.

    ![desktop wallpaper group policy](./screenshots/create-group-policy/10-desktop-wallpaper-gp.png)

- `Computer Configuration`:
    - `Do not display last signed-in user`: Located `Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options`.

    ![dont display last signed in](./screenshots/create-group-policy/11-dont-display-last-signed-in.png)

    - `Message text/title for users attempting to log on`: Located `Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options`.

    ![message text/title log on](./screenshots/create-group-policy/12-message-text-title.png)

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

![run gpupdate](./screenshots/create-group-policy/13-run-gpupdate.png)

Depending on the policy, Windows may require:

- Logging back in
- Reboot

> [!important]
> Based on how we applied the GPO, what do you think will happen when restarting the client?

### 9. Verify the GPO

So, we linked the child OU `Sales` and the GPO `Department User Baseline`.

This means that as of right now, only users in `Sales` OU will receive the GPO. We can verify that here:

- Notice how Jill Estrada received the background wallpaper.

![verify gpo 01](./screenshots/create-group-policy/14-verify-gpo.png)
![verify gpo](./screenshots/create-group-policy/15-verify-gpo-01.png)

- Jill Estrada is unable to open the command prompt.

![verify gpo 02](./screenshots/create-group-policy/16-verify-gpo.png)

- Unable to open `Settings` or `Control Panel`.

![verify gpo 03](./screenshots/create-group-policy/17-verify-gpo.png)

- Testing with another user in `Sales`, we noticed the same settings have applied.

![verify gpo 04](./screenshots/create-group-policy/18-verify-gpo.png)

#### Now lets try logging in to the device with a user that's not in Sales

We have Guillermo Mccall.

![verify gpo 05](./screenshots/create-group-policy/19-verify-gpo.png)

- Does not have the background wallpaper.
- Able to open command prompt.

![verify gpo 06](./screenshots/create-group-policy/20-verify-gpo.png)

- Able to open `Settings`.

![verify gpo 07](./screenshots/create-group-policy/21-verify-gpo.png)

- Able to open `Control Panel`.

![verify gpo 08](./screenshots/create-group-policy/22-verify-gpo.png)

#### Notice how no Computer Configurations have been applied

Because we didn't link the GPO to the workstation, `Computer Configuration` did not get applied.

Lets link the workstation.

1. Create the child OU for `Sales`.

![create workstation sales](./screenshots/create-group-policy/23-create-workstation-sales.png)

2. Move `WIN11-CLIENT-02` from the default `Computers` to `Workstations/Sales`.

![move client to workstation](./screenshots/create-group-policy/24-move-client-to-workstations.png)

3. Go back to `Group Policy Management`.

    1. Expand `corp.example.com`.
    2. Expand `Workstations`.
    3. Right click on `Sales`.
    4. Select `Link an Existing GPO...`

    ![link existing gpo](./screenshots/create-group-policy/25-link-existing-gpo.png)

    > [!important]
    > Splitting User Configuration and Computer Configuration is easier to manage.
    >
    > In this lab, we combined the two into a single GPO.

    5. Select the GPO that we created.

    ![select the existing gpo](./screenshots/create-group-policy/26-select-gpo.png)

### Creating a Security Group

Since we added a GPO for users in `Sales`, lets restrict the workstation so only users in `Sales` are authorized to access the workstation.

In `Active Directory Users and Computers`:

1. Right click `Groups` OU.
2. Select `New`, then select `Group`.

![create policy group](./screenshots/create-group-policy/27-create-policy-group.png)

3. Give the security group a name. I used `Sales_Workstation_Users`.

![name security group](./screenshots/create-group-policy/28-name-security-group.png)

4. Group scope: `Global`.
5. Group type: `Security`.
6. Click `OK`.

![security group properties](./screenshots/create-group-policy/29-security-group-properties.png)

#### Add the users in Sales to the group

While still in `ADUC`:

1. Double click on `Sales_Workstation_Users`.
2. Go to `Members`.
3. Click `Add`.
4. Add the users in `Sales`.

![add sales users to security group](./screenshots/create-group-policy/30-add-users-to-security-group.png)

#### Edit the GPO to allow only users from the Sales department

In `Group Policy Management`:

1. Expand:
    
    - `Forest: corp.example.com`
    - `Domains`
    - `corp.example.com`
    - `Workstations`

2. Click on `Sales`. You should see the GPO that we created.
3. Right click the GPO and `Edit`.

![edit gpo](./screenshots/create-group-policy/35-edit-gpo.png)

4. Locate `Allow log on locally` by following `Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > User Rights Assignment`.

![allow log on locally](./screenshots/create-group-policy/31-allow-logon-locally.png)

5. Add:
    - `Administrators`
    - `Sales_Workstation_Users`

![allow administrators and sales](./screenshots/create-group-policy/32-allow-admin-sales.png)

> [!caution]
> Administrators must be included or else they will be locked out.

#### Update policy on client

On the `Sales` workstation, log in as an administrator then run:

```cmd
gpupdate /force
```

After restarting, you should notice the `Computer Configuration` that we created in the GPO.

- The logon title/message should now appear

![login title and message](./screenshots/create-group-policy/33-computer-configuration.png)

- You no longer see last signed-in user in the bottom left.

![cant view last signedin user](./screenshots/create-group-policy/36-cant-see-last-signedin-user.png)

#### Only users in the Sales department can log into this workstation

You can test this by logging in with a user in another department.

![only sales users can log in](./screenshots/create-group-policy/34-only-sales-user.png)

## Congratulations!

You've successfully implemented Group Policy in Active Directory!

## Conclusion

This document showed the full workflow of creating, linking, applying, and verifying Group Policy in Active Directory. By testing the policy on the `Sales` OU and a domain-joined client, it became easier to understand how `User Configuration` and `Computer Configuration` are applied based on where objects are located.

This is also a good reminder that OUs and groups serve different purposes:

- OUs: Organize objects and scope policy
- Groups: Used to manage permissions and access.
