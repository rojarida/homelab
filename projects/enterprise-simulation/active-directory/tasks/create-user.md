# Create User

This document shows how to create a new domain user in Active Directory on Windows Server. Then verify that the account can be used to sign in from a Windows client that joined the domain.

## Goal

Create a new user in Active Directory Users and Computers (ADUC) and confirm the account exists in the domain.

## Prerequisites

Before starting, make sure:

- Active Directory Domain Services is installed
- Server has been promoted to a Domain Controller
- The client has already joined the domain

See:
- [Active Directory Setup](../README.md)
- [Join W11 VM to Domain](../../windows-11-client/tasks/join-domain.md)

## 1. Open Active Directory Users and Computers

On `Server Manager`:

1. On the top right, click `Tools`.
2. Select `Active Directory Users and Computers` from the dropdown.

This opens the ADUC console where domain users, groups, and computers can be managed.

![open active directory users and computers](./screenshots/01-open-aduc.png)

> [!note]
> You should be able to see the Windows 11 VM that you joined to the domain under Computers.

![verify joined client](./screenshots/02-verify-w11-joined-domain.png)

## 2. Navigate to the location for a new user

In the left pane, expand your domain name.

Choose where you want to create the user. For a simple lab setup, placing the account in the default `Users` container is fine.

![location for new user](./screenshots/03-aduc-users.png)

## 3. Create a new user

1. Right click the `Users` container.
2. Select `New`.
3. Click `User`.

This is where you create a new user.

![create a new user](./screenshots/04-create-new-user.png)

## 4. Enter the user's information

Fill in the user details:

- `First name`
- `Last name`
- `Full name`
- `User logon name`

![new object user](./screenshots/05-new-user-object.png)

I will be creating this user:

- First name: `Thor`
- Last name: `Odinson`
- User logon name: `odithor`

Once filled out, click `Next`.

![filling out user information](./screenshots/06-filling-user-details.png)

## 5. Set the password

Enter an initial password for the user.

You also have several account options:

- `User must change password at next logon`
- `User cannot change password`
- `Password never expires`
- `Account is disabled`

For a regular user, it's common to leave `User must change password at next logon` checked.

![set initial password](./screenshots/15-set-user-password.png)

## 6. Finish creating the user

Review the summary page, then click `Finish`.

![finish and review user](./screenshots/07-review-user.png)

The created user should now appear in the selected container. Right click the user and select `Properties`. Take the time to look at the different properties.

![user should appear in container](./screenshots/08-created-user-should-appear.png)

## 7. Test sign-in from a domain-joined client

On a Windows client joined to the domain:

1. Select `Other user` in the bottom left

    - ![select other user](./screenshots/09-login-screen.png)

2. Sign in using either:
    - `DOMAIN\username`
    - `username@domain.name`

    - ![sign in to domain](./screenshots/10-log-into-created-user.png)

If you left the `User must change password at next logon` checked, you will see the prompt to change the user's password.

![change password before signing in](./screenshots/11-if-password-change-checked.png)
![creating a new password](./screenshots/12-change-password-logon.png)
![password has been changed](./screenshots/13-password-changed.png)

## 8. Verify user

When logged on, verify the user by clicking the start menu. Then click on the user. You should see the `First name`, `Last name`, and the `logon name with domain`.

![verify user](./screenshots/14-verify-domain-user.png)

## 9. Congratulations

You've successfully added a new user in Active Directory using ADUC and verified that the account can sign in from a domain-joined client.
