# Enterprise Simulation

A homelab project for simulating a small enterprise environment using virtual machines.

## Overview

This lab is designed to practice core enterprise infrastructure concepts in an isolated environment with controlled internet access.

The environment will use:

- pfSense as the virtual router/firewall
- Windows Server for domain services
- Windows client VMs for joining domain and policy testing

## Goals

- Build a small routed lab network
- Deploy Active Directory, DNS, and related services
- Join Windows clients to the domain
- Practice user, group, and policy management
- Troubleshooting enterprise networking and authentication issues
- Document the full setup step by step

## Planned Topology

- `pfSense WAN`: Virtual NAT
- `pfSense LAN`: Isolated lab network
- `Windows Server`: Domain Services
- `Windows Clients`: Domain-joined test machines

## Scope

This project is focused on:

- Active Directory
- DNS
- DHCP
- Group Policy
- Joining Windows Clients to domain
- Basic internal enterprise simulation

This lab is meant for testing and learning. It is not intended for production use on home network.

## Documentation
