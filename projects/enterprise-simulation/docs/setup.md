# Enterprise Simulation Setup

This document covers the initial setup for the `enterprise-simulation` lab. It is focused on preparing a clean, isolated foundation before configuring services such as Active Directory, Group Policy, joining clients to the domain, and other enterprise features.

## Purpose

The goal of this setup is to create a safe test environment that simulates an isolated, enterprise Windows network. This lab is intended for learning, experimentation, troubleshooting practice, and documentation.

## Scope

This setup document covers:

- Preparing the isolated lab environment
- Creating the baseline Windows Server VM
- Creating the baseline Windows 11 Client VM
- Verifying network isolated

This document does **not** cover:

- Active Directory Domain Services configuration
- DNS or DHCP role configuration
- Joining Windows clients to the domain
- Group Policy configuration

These topics will be documented in their own dedicated files under `docs/`.

## Lab Design

This enterprise simulation is intentionally separated from the real home network. The devices that I use to administer the home network are running Ubuntu and Linux Mint. As of right now, there's no benefit in implementing Active Directory in our current network configuration.

The workflow is:

- Build and test the lab in an isolated virtual environment
- Document the full process and troubleshooting steps
- Experiment safely without risking current home network

> [!note]
> This project is for lab use only. It is not intended to be deployed directly onto the home network.

## Prerequisites

Before continuing, complete the following baseline VM setup guides:

- [Windows Server 2025 Setup](../../../virtualization/windows-server-2025/README.md)
- [Windows 11 VM Setup](../../../virtualization/
