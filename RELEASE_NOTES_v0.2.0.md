# TuffNode Lite v0.2.0

TuffNode Lite v0.2.0 is a major refactor of the Lite experience.

The beta-era dashboard has been replaced by a compact single-server control surface built around four focused areas: **Server, Console, Plugins and Settings**.

## Highlights

### Compact single-server UI

- New 520 × 620 compact window.
- Four primary tabs: Server, Console, Plugins and Settings.
- Compact first-run setup.
- Setup can be reopened later without deleting the current world.
- Dark and Snow themes with the Lite Electric Cyan accent.
- Custom themed controls and slim scrollbars.

### Server control

- One-click server start and graceful stop.
- Live status and uptime.
- Real Java-process RAM and CPU telemetry.
- TPS display for compatible server types.
- Automatic free-port selection when the preferred port is occupied.
- Local IP and public IP shown separately.
- Copy actions for Java and Bedrock endpoints.
- Quick commands directly on the Server page.

### Console

- Dedicated live Console tab.
- Direct command input with Enter-to-send.
- Clear and auto-scroll controls.
- Bounded console history.

### Server settings

The Settings tab now edits the real server.properties values used by the Lite server, including MOTD, difficulty, game mode, render distance, simulation distance, max players, Java port, spawn protection, online mode, PvP, whitelist, allow flight and command blocks.

### Providers

v0.2.0 supports Paper, Purpur, Vanilla, Spigot, CraftBukkit, Fabric, Forge, NeoForge and Custom .jar.

Managed Java provisioning remains part of the normal Lite setup flow.

### Plugins and mods

Plugins now have two dedicated sub-tabs:

- Browse for discovery and installation.
- Installed for add-ons already present on disk.

Managed sources are Modrinth, Hangar and SpigotMC. Fabric, Forge and NeoForge use Modrinth for managed mod discovery.

Installed add-ons can be enabled, disabled or deleted. Local .jar drag-and-drop remains supported.

### Geyser / Bedrock

Geyser is now a first-class managed add-on on compatible Java plugin servers.

- Install
- Enable
- Disable
- Bedrock local/public connection information on the Server page

### Windows integration

- Start Lite automatically with Windows.
- Minimize to tray or exit on close.
- Safe exit confirmation while the server is running.
- Running/idle tray icons.
- Active server port in the tray status.

### Localization

The Lite UI supports 18 languages and switches language live without restarting the app.

## Requirements

- Windows 10 or Windows 11 x64
- Internet access for downloading Minecraft server software, Java runtimes and managed add-ons

## Network note

Showing a public IP does not automatically make the server reachable from the Internet. Router NAT/port forwarding and firewall configuration may still be required.

## Distribution

This public release is binary-only. The TuffNode Lite application source code is maintained privately and is not distributed through the public release repository.

See the full history in CHANGELOG.md.
