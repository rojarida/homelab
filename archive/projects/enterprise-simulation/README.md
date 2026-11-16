# Enterprise Simulation

> [!NOTE]
> **Archived guide.** Retained for reference; no longer maintained. See [current setup](../../../README.md) or the [archive index](../../README.md).

A historical lab for practicing small-enterprise infrastructure with virtual machines. Its documented topology used pfSense, Windows Server 2025, and Windows 11 clients under QEMU/KVM and virt-manager.

## Documented implementation

| Area | Work recorded in the guides |
| --- | --- |
| Networking | [pfSense routing and DHCP](pfSense/README.md), with a NAT-connected WAN and an isolated lab LAN |
| Identity and DNS | [Windows Server domain controller deployment](active-directory/README.md) |
| Client integration | [Windows 11 domain join and sign-in](windows-11-client/tasks/join-domain.md) |
| Administration | [Domain users](active-directory/tasks/create-user.md) and [Organizational Units](active-directory/tasks/create-organizational-units.md) |
| Policy | [GPO scope and client verification](active-directory/tasks/create-group-policy.md), including comparisons across users and computer OUs |
| Troubleshooting | [Addressing and wallpaper-path issues](troubleshooting.md) |

## Design and lessons

- pfSense supplied routing and DHCP; the domain controller supplied domain DNS and authentication. Domain clients needed DNS pointing to the domain controller.
- The lab LAN was separate from the home LAN. A NAT-connected WAN provided upstream access; NAT alone is not proof that access to home networks was blocked.
- User policy and computer policy depended on where the respective directory objects were located and where the GPO was linked.
- A server-local wallpaper path failed on the client; a reachable UNC path resolved the documented issue.
