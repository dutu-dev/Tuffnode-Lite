# TuffNode Lite

Official binary distribution repository for **TuffNode Lite**.

Current version: **v0.2.1**

## Download

Download the latest Windows release from GitHub Releases:

https://github.com/dutu-dev/Tuffnode-Lite/releases/latest

The official Windows installer is built with **Inno Setup 6**.

Installer filename:

`TuffNode-Lite-v0.2.1.exe`

## What's new in v0.2.1

v0.2.1 is a focused reliability patch for plugin and mod installation.

### Plugin installation

- Fixed Browse showing add-ons while Install could fail on a newly configured server that had not been provisioned yet.
- Lite can now prepare/provision the server automatically when installing an add-on.
- Fixed successfully installed add-ons continuing to show **Install** in Browse.
- Browse now detects the real installed JAR and changes the action to **Installed** automatically.
- Installed actions are disabled and refresh without requiring an application restart.
- Local `.jar` import and managed Geyser installation use the same preparation path.

### Provider reliability

- Improved Modrinth loader/version resolution.
- Fixed `Latest stable` compatibility filtering before first server start.
- Improved Hangar compatible-release selection.
- Added a SpigotMC/Spiget fallback when direct download fails.
- JSON API requests and binary JAR downloads now use separate appropriate HTTP headers.
- Downloaded add-ons are validated before being placed in the live plugins/mods folder.
- Provider errors now surface useful details instead of only a generic `Error` message.

See [RELEASE_NOTES_v0.2.1.md](RELEASE_NOTES_v0.2.1.md) for the complete patch notes and [CHANGELOG.md](CHANGELOG.md) for the cumulative product history.

## TuffNode Lite

TuffNode Lite is a free Windows application for running and managing one self-hosted Minecraft server through a compact interface.

The application is organized around four areas:

- **Server** — start/stop, telemetry, local/public addresses and quick commands
- **Console** — live output and direct Minecraft commands
- **Plugins** — Browse and Installed add-on management
- **Settings** — real Minecraft server settings plus Lite application settings

## Server providers

TuffNode Lite supports:

- Paper
- Purpur
- Vanilla
- Spigot
- CraftBukkit
- Fabric
- Forge
- NeoForge
- Custom `.jar`

Compatible Java runtimes can be provisioned automatically for managed server types.

## Plugins and mods

Plugin-capable servers can browse managed add-ons from:

- Modrinth
- Hangar
- SpigotMC

Fabric, Forge and NeoForge use Modrinth for managed mod discovery.

Installed add-ons are read from the real server add-on directory. They can be enabled, disabled or removed, and Browse reflects installed state directly. Local `.jar` drag-and-drop is supported.

## Geyser / Bedrock

Geyser is available as a managed add-on on compatible plugin-based Java servers.

When enabled, Lite displays separate local/public Bedrock connection information alongside the normal Java server addresses.

## Server settings

The Settings tab exposes common real `server.properties` values including:

- MOTD
- difficulty
- game mode
- render distance
- simulation distance
- max players
- port
- spawn protection
- online mode
- PvP
- whitelist
- allow flight
- command blocks

## Windows integration

- Dark and Snow themes
- 18 UI languages
- Start with Windows
- Minimize to tray
- Safe graceful shutdown when exiting with a running server

## Installer experience

The v0.2.1 installer includes:

1. TuffNode Lite branded Welcome page.
2. License Agreement with mandatory acceptance.
3. What's New in v0.2.1 page.
4. Installation directory selection.
5. Shortcut options.
6. Ready to Install summary.
7. Installation.
8. Finish page with optional Launch.

The installer preserves the existing TuffNode Lite product identity, so v0.2.1 upgrades v0.2.0 rather than creating a second installation.

## What is published here

This repository is intentionally distribution-only.

- Windows installer binaries through GitHub Releases
- Release notes
- Changelog
- Public release information

**The TuffNode Lite application source code is not published in this repository.**

## Network note

Public IP discovery is informational. It does not automatically configure router port forwarding, NAT or firewall access.

## Requirements

- Windows 10 / 11 x64
- Internet access for downloading Minecraft server software, Java runtimes and managed add-ons

## Release history

- `v0.2.1` — plugin/mod installation and installed-state reliability patch
- `v0.2.0` — compact Lite redesign
- `v0.1.0-beta.1` — first public beta

## Publisher

Developed and published by **dutu-dev - TuffNode**.

## Contact

contact@tuffnode.com  
https://tuffnode.com

## Trademark / affiliation

TuffNode is an independent project and is not affiliated with, endorsed by, or associated with Mojang Studios or Microsoft.
