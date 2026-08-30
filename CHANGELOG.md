# TuffNode Lite Changelog

## v0.1.0-beta.1

First public beta of TuffNode Lite.

TuffNode Lite introduces a simpler single-server management experience for Windows while keeping the controls normally needed for a self-hosted Minecraft server.

### Setup and server providers

- Guided first-launch server setup.
- Minecraft version selection.
- Paper, Purpur, Vanilla, Spigot, CraftBukkit, Fabric, Forge and NeoForge provider support.
- Managed Java runtime download and setup.
- Minecraft EULA handling during provisioning.

### Performance

- Configurable server RAM.
- Allocated, available and total system memory visibility.
- Garbage collector selection with G1GC as the recommended default.
- ZGC, Parallel GC and JVM-default options.

### Add-ons

- Plugin browser with Modrinth, Hangar and SpigotMC-compatible sources.
- Source selection between All Sources, Modrinth, Hangar and SpigotMC.
- Compatible plugin installation directly from Lite.
- Local `.jar` plugin import.
- Installed plugins are read from the real server `plugins` folder.
- Enable, disable and uninstall installed plugins.
- Disabled plugins remain visible and can be enabled again later.
- Installed plugins are managed in a separate popup so they do not reduce the marketplace browser area.

### Players

- Known-player and online-player views.
- Ban and unban controls.
- Kick controls.
- OP and de-op controls.
- Whitelist controls.
- Ban-list visibility.

### Console and settings

- Live server console output.
- Server command input.
- MOTD configuration.
- Max-player configuration.
- Gamemode and difficulty controls.
- PvP and whitelist settings.
- View-distance and simulation-distance controls.
- Configurable Java server port.

### Java and Bedrock cross-play

- Optional Geyser support for compatible server types.
- Java and Bedrock connection information shown separately.
- Bedrock UDP port handling for Geyser-enabled servers.

### Network, Sync and Shield

- Local IPv4 discovery.
- Public IP discovery with fallback providers.
- Java and Bedrock connection endpoints.
- Optional TuffNode Sync local publication registry.
- Published server snapshots include server state, addresses, ports, provider and version information.
- TuffNode Shield posture checks for Windows Firewall state and secure defaults.

### Interface

- Custom TuffNode Lite window chrome.
- Fixed standard viewport across Overview, Players, Add-ons, Console and Settings.
- Custom dark scrollbars and tab content styling.
- Add-ons marketplace redesigned around a larger browsing area.

### Beta notes

- This is a testing release and behavior may still change before the first stable Lite version.
- TuffNode Sync currently publishes to the local TuffNode Sync registry; a remote/cloud Sync backend is not included in this beta.
- Internet joins still require appropriate network configuration such as router port forwarding unless another networking layer is used.
- Forge, NeoForge and BuildTools-based providers need broader validation across more Minecraft versions and environments.
- The first beta installer is not code-signed unless explicitly built with a signing certificate.
