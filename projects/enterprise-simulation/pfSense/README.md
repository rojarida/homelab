# pfSense for Enterprise Simulation

This documents how pfSense is configured for the `enterprise-simulation` lab.

> [!note]
> This is **not** a pfSense installation guide. (See: [pfSense Setup](../../../pfSense/setup/README.md))

## Overview

pfSense is used as the:

- Default Gateway
- Firewall
- DHCP Server
- Path to upstream internet access

The domain controller will handle:

- Active Directory
- DNS for the domain
- Authentication
- Group Policy

## Goal
