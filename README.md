# TuffNode Lite

Official binary distribution repository for **TuffNode Lite**.

## Download

Download the latest Windows release from **GitHub Releases**:

https://github.com/dutu-dev/Tuffnode-Lite/releases/latest

Current release: **v0.2.0**

## What is published here

This repository is intentionally distribution-only.

- Windows release binaries
- Release notes
- Changelog
- Public release information

**The TuffNode Lite application source code is not published in this repository.**

## About TuffNode Lite

TuffNode Lite is a free Windows application for running and managing one self-hosted Minecraft server through a compact interface.

v0.2.0 is organized around four areas:

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
- Custom .jar

Compatible Java runtimes can be provisioned automatically for managed server types.

## Plugins and mods

Plugin-capable servers can browse managed add-ons from:

- Modrinth
- Hangar
- SpigotMC

Fabric, Forge and NeoForge use Modrinth for managed mod discovery.

Installed add-ons can be enabled, disabled or removed, and local .jar drag-and-drop is supported.

## Geyser / Bedrock

Geyser is available as a managed add-on on compatible plugin-based Java servers.

When enabled, Lite displays separate local/public Bedrock connection information alongside the normal Java server addresses.

## Server settings

The Settings tab exposes common real server.properties values including:

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

## Network note

Public IP discovery is informational. It does not automatically configure router port forwarding, NAT or firewall access.

## Requirements

- Windows 10 / 11 x64
- Internet access for downloading Minecraft server software, Java runtimes and managed add-ons

## Release notes

See [RELEASE_NOTES_v0.2.0.md](RELEASE_NOTES_v0.2.0.md).

## Changelog

See [CHANGELOG.md](CHANGELOG.md).

## Publisher

Developed and published by Dutu.

## Contact

contact@tuffnode.com  
https://tuffnode.com

## Trademark / affiliation

TuffNode is an independent project and is not affiliated with, endorsed by, or associated with Mojang Studios or Microsoft.
