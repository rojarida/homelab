# pfSense Setup

This document describes how I setup `pfSense CE as a virtual router/firewall` on my Ubuntu home server using `QEMU/KVM and virt-manager`.

This is meant to be a personal reference guide.

---

## Goal

The goal of this project was to move routing and firewall responsibilities away from a consumer, all-in-one router setup and into a more flexible homelab design.

The intended final design is:

- pfSense acts as the primary router/firewall
- AXE95 runs in AP Mode
- LAN uses the subnet: `192.168.0.0/24`
- pfSense provides DHCP for clients
- The Ubuntu Host remains reachable on a static LAN IP: `192.168.0.200`

---

## Starting Environment

Before this setup:

- Home network was already running on the `192.168.0.0/24` subnet.
- The Ubuntu Host was hosting virtualization with `QEMU/KVM`
- pfSense was planned to run as a VM on the Ubuntu Host
- The Wireless Router would later be converted into an `Access Point`

--

