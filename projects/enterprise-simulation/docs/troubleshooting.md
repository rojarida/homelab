# Troubleshooting

This document will show any issues with setting up the enterprise environment.

## Bypass `Connecting to Network`

> [!note]
> When creating a Windows 11 VM in an isolated virtual network, it may ask you to connect to a network.
>
> `OOBE\BYPASSNRO` bypasses mandatory internet connection and Microsoft Account requirements.

To bypass this:
- Press Shift + F10
- Then type: `OOBE\BYPASSNRO`
- Windows should then restart on its own

Now when you go through the installation process and get back to the `Let's connect you to a network`, you should see an option to select `I don't have internet`.
