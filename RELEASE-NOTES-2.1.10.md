# REVO 2.1.10 — release notes (Windows)

Released 2026-11-25. Version `2.1.10`. Application ID (`com.revo.xray`) and the
installer identity are unchanged, so this upgrades 2.1.9 in place and keeps all
data.

## Added

- **DNS Changer** with feature parity to the Android edition:
  - its own sidebar entry and screen;
  - saved profiles with an optional name and primary/secondary resolvers;
  - favourites, selection, activation and stopping;
  - real Windows adapter changes through `netsh`, applied to the physical adapter
    that carries the default route (VPN, loopback and virtual adapters are
    excluded by the query);
  - the complete original IPv4 and IPv6 DNS state is saved before the first
    change, including whether each family used DHCP or a static list;
  - stopping, switching profiles, deleting the active profile and quitting REVO
    restore that snapshot; an interrupted change is recovered on the next start;
  - a refused change (no administrator rights) is reported exactly, the original
    settings are kept, and the UI never shows a false active state.

  DNS Changer is DNS-only: it does not start the Xray core, the system proxy or the
  Full Tunnel.

## Changed

- **DNS controls moved to Settings → Advanced settings** in this order:
  1. Enable Local DNS
  2. Enable Fake DNS
  3. VPN DNS
  There is no second copy of these controls anywhere in the app. Stored keys are
  unchanged, so upgrading preserves the current values.

- **VPN DNS drives the real VPN DNS path.** It is written to the REVO tunnel
  adapter and used by the core resolver, so DNS does not follow a stale
  adapter-only override. In Windows proxy and Manual proxy modes each application
  resolves names itself and the UI says the switches are not applied.

- Fake DNS keeps its dependency on Local DNS: it is stored but not applied without
  it, with an explicit warning, and enabling it never enables Local DNS.

## Fixed

- **Collapsed sidebar logo.** The 36 px logo sat next to a zero-width label whose
  11 px flex gap still took space inside a 36 px column, so the logo shrank and
  drifted off-centre. The gap now collapses with the label and the logo keeps its
  size and centre. The expanded sidebar is unchanged.

## Unchanged

- Routing rules and their location in Advanced options.
- Servers, subscriptions, Best Server, favourites, Local Proxy, Split Tunneling
  behaviour (no Windows per-app split-tunneling UI is added by this release), light
  and dark themes, and the Liquid Glass styling.

## Verified

- Windows regression and feature suite: 26 tests, 0 failures, including real Xray
  config validation and a real HTTPS measurement through the bundled core.
- DNS Changer HTTP integration: 9 tests, 0 failures, including profile CRUD,
  validation, a real apply attempt on the live adapter, and confirmation that a
  refused apply leaves the adapter DNS byte-for-byte unchanged.
- The installer builds successfully and reports file version 2.1.10.
- A real elevated run on the active Wi-Fi adapter applied a profile, confirmed
  the addresses Windows reported, restored a static list exactly, and restored
  the original DHCP state for IPv4 and IPv6.

## Known limitations

- The application is unsigned, so SmartScreen may warn. Compare the SHA-256.
- Changing adapter DNS needs administrator rights. Without them REVO refuses,
  restores the snapshot and offers an explicit **Restart as administrator**
  action (UAC). It never elevates silently.
- DNS Changer does not cover applications with their own DoH/DoT resolver or a
  system-wide Private DNS setting.
- Real changes were verified on the active Wi-Fi adapter only; no Ethernet
  adapter was connected during the release test.
