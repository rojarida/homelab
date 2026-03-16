# Create Organizational Units

## Overview

This document demonstrates how to create a simple Organizational Unit (OU) structure in Active Directory Users and Computers (ADUC). In this lab, OUs are used to separate administrative areas by department and function.

The following OUs will be created:

- Departments
    - IT
    - HR
    - Sales
    - Engineering
- Workstations
- Groups

## Why Organizational Units?

Organizational Units help organize objects such as users and computers inside Active Directory.

They're commonly used to:

- Keep domain structured and easier to navigate
- Separate users and computers by department or function
- Apply Group Policy to specific parts of the domain
- Delegate Administrative control when needed

> [!note]
> It's important to distinguish OUs from groups:
>
> **OUs**: Mainly for organization, delegation, and Group Policy
> **Groups**: Mainly for permission and access control

## Environment

- Domain Controller: `WIN-SRV-01`
- Domain: `corp.example.com`
- Tools: `Active Directory Users and Computers (ADUC)`

## Prerequisites

- Windows Server 2025 setup (See: [Windows Server Setup](../README.md))

## Initial State

The domain contains default built-in containers and folders such as:

- Builtin
- Computers
- Domain Controllers
- ForeignSecurityPrincipals
- Managed Service Accounts
- Users

## Creating Organizational Units
