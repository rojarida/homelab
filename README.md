# Homelab

This repository documents my personal homelab: hardware, network, services, and infrastructure projects I build for learning, experimentation, and reference.

The lab is centered around hands-on IT and systems work including:
- Virtualization
- Network Infrastructure
- Routing and Firewalling
- NAS/Storage Services
- VPN Access
- Documentation

### Goal
- Personal reference for rebuilding and troubleshooting
- Portfolio of practical infrastructure and networking projects

---

## Overview

My homelab is built around an Ubuntu-based server, a virtualized pfSense router/firewall, local storage services, and a small home network that I can expand over time.

Current areas of focus:
- pfSense virtual router/firewall
- Home network topology and documentation
- Static addressing and DHCP reservations
- VPN and Remote Access
- Future VLAN Segmentation
- Future Managed Switching

---

## Current Network Configuration

- pfSense runs as a VM on the Ubuntu Host
- pfSense is the primary LAN gateway
- AXE95 runs in AP mode

- LAN Subnet: `192.168.0.0/24`
- Ubuntu Host: `192.168.0.200`
- AP Mgmt IP: `192.168.0.2`
- pfSense Mgmt IP: `192.168.0.1`

---

## Repository Structure

```text
.
├── pfsense
│   ├── docs
│   └── README.md
└── README.md
```

> Sample structure for repository. It will grow over time.

---

## Lab Hardware

### Main Workstation

Dual-boot workstation with Linux Mint as the primary OS and Windows 11 for compatibility. Used for development, coursework, gaming, and general use.

- Pre-built PC
    - `Case`: Corsair 5000D AIRFLOW Mid-Tower ATX
    - `Motherboard`: Gigabyte B550 GAMING X V2
    - `CPU`: AMD Ryzen 7 5700X
    - `RAM`: 32GB (2x16GB) DDR4 @ 3200 MHz
    - `GPU`: AMD Radeon RX 6800XT 16GB VRAM
    - `OS`:
        - `Windows 11`: Western Digital Blue SN550 500GB
        - `Linux Mint`: Samsung SSD 970 EVO Plus 1TB

- Peripherals
    - `Monitor` 
        - `Main`: Sceptre 27-inch 2560x1440 @ 144Hz
        - `Secondary`: Asus VG248QE 1920x1080 @ 144Hz
    - `Keyboard`: Logitech MX Keys S Wireless
    - `Mouse`: Logitech MX Master 4 Wireless
    - `Mousepad`: Glorious XXL Extended Black

### Ubuntu Host

Primary homelab server used for virtualization, NAS services, and hosting the pfSense router/firewall VM.

- Dell OptiPlex 7050 SFF
    - `Motherboard`: Dell 0NW6H5
    - `CPU`: Intel i7-7700 @ 3.60GHz
    - `RAM`: 24GB DDR4 (1x8GB + 2x8GB) @ 2133MHz
    - `Boot Drive`: Micron 256GB SATA III M.2 2280
    - `Storage Pool`: 2x PNY CS900 1TB (ZFS mirror)
    - `Hypervisor`: QEMU/KVM with virt-manager
        - `ISO`: pfSense CE (FreeBSD)

### Networking Gear

Core networking hardware used for routing, switching, and wireless access.

- `Access Point`: TP-Link Archer AXE95
- `Switch`: TP-Link TL-SG105 (**unmanaged**)
- `NIC`: Intel I350-AM2 (dual-port)
    - Dedicated WAN/LAN connectivity for pfSense VM

---

## Projects

### pfSense
Virtualized router/firewall running on the Ubuntu Host.

Includes:
- VM Setup
- WAN/LAN Design
- LAN DHCP Configuration
- AP Mode Migration
- Troubleshooting Notes

See: [pfSEnse/README.md](pfsense/README.d)

---

## Current Priorities

- [x] Configure pfSense VM
- [x] Migrate AXE95
- [x] Document homelab hardware
- [ ] Add pfSense setup documentation
- [ ] Add VPN documentation
- [ ] Move to managed switching
- [ ] Plan VLAN segmentation

---
