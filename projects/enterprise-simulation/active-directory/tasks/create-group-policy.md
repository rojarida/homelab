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

This is console used to create, link, edit, and manage GPOs.

> 01


