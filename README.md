# REVO 2.1.10 — Windows

REVO is a local Xray client for Windows. It runs the bundled Xray core and
connects only to the servers you add. Your server list, subscriptions and settings
stay on this computer.

## Files

| File | Purpose |
| --- | --- |
| `REVO-Setup-2.1.10.exe` | Installer (x64). This is the supported package. |
| `SHA256SUMS.txt` | SHA-256 checksum of the installer. |

No portable package is built for this release: the project's build configuration
produces the NSIS installer only.

## Requirements

- Windows 10 or Windows 11, 64-bit.
- Administrator rights only for **Full Tunnel** and for **DNS Changer**. Windows
  proxy and Manual proxy modes run without elevation.

## Install (first time)

1. Run `REVO-Setup-2.1.10.exe`.
2. Choose the install folder if you want; otherwise accept the default.
3. Open REVO, add a server (share link, manual entry, or subscription URL), select
   it and press Connect.

The installer is not code-signed, so Windows SmartScreen may warn about an
unknown publisher. Verify the SHA-256 checksum below before running it

## Upgrade from an earlier version

Run the new installer over the existing installation. Your servers,
subscriptions, settings and DNS Changer profiles are kept. Uninstalling keeps the
app's data as well, so a later reinstall can pick it up.

## Verify the download

```powershell
Get-FileHash .\REVO-Setup-2.1.10.exe -Algorithm SHA256
```

Compare the result with `SHA256SUMS.txt`, or run `sha256sum -c SHA256SUMS.txt`
from Git Bash.

## What is new in 2.1.10

- **DNS Changer**: its own screen, saved profiles, favourites, primary/secondary
  resolvers, live adapter detection, native Windows adapter DNS changes, exact
  DHCP/static IPv4+IPv6 restoration, crash recovery and an explicit administrator
  error instead of a false active state. It never starts the proxy or the tunnel.
- DNS controls moved to **Settings → Advanced settings** in one order:
  **Enable Local DNS**, **Enable Fake DNS**, **VPN DNS**.
- **VPN DNS** now drives both the core resolver and the REVO tunnel adapter, so
  DNS is not pulled to an adapter-only value.
- The sidebar logo is centred and no longer shrinks when the sidebar is collapsed.
- Version 2.1.10.

Routing rules and their location are unchanged in this release.

See `RELEASE-NOTES-2.1.10.md` for the full list and known limitations.

## Notes

- Full Tunnel is Windows-only and creates a Wintun adapter; `wintun.dll` ships in
  the installation.
- The Xray core is bundled; its licence is included with the application files.
- This folder contains no signing keys, certificates, API tokens, subscription
  URLs, personal data or local machine paths.

## Licence

REVO is proprietary software. All rights reserved.
The source code is not publicly distributed.

Third-party components remain subject to their respective
licences. Their notices are included with the application files.
