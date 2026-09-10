# TuffNode Lite v0.2.1

TuffNode Lite v0.2.1 is a focused reliability patch for plugin and mod installation.

## Fixed

### Add-on installation on new servers

- Fixed Plugins → Browse showing installable add-ons while the Install action could refuse to proceed before the server had been started for the first time.
- Installing a plugin or mod can now automatically prepare/provision the selected server when required.
- Local `.jar` drag-and-drop uses the same automatic preparation path.
- Managed Geyser installation can also prepare the server automatically.

### Installed-state feedback

- Fixed successfully installed add-ons continuing to show **Install** in Plugins → Browse.
- Browse now reconciles catalog results against the real JAR files present in the active `plugins` / `mods` directory.
- Installed add-ons switch automatically to **Installed** and the action becomes disabled.
- Installed-state changes refresh without requiring an application restart.
- Versioned JAR names such as `PluginName-1.2.3.jar` are recognized when matching installed files to Browse results.

### Modrinth

- Improved compatible-version resolution by trying server loaders individually in priority order.
- Paper-family servers can fall back to compatible Paper / Spigot / Bukkit releases where appropriate.
- Purpur checks Purpur, Paper, Spigot and Bukkit-compatible versions.
- Fabric, Forge and NeoForge retain their native loader filters.
- Fixed searches that could use the literal `Latest stable` label as if it were a Minecraft version.
- Lite now resolves a concrete Minecraft version before compatibility filtering when necessary.
- Download selection prefers the primary JAR and ignores non-JAR auxiliary files.

### Download reliability

- JSON API requests and binary JAR downloads now use appropriate HTTP request headers independently.
- Downloaded add-ons are validated as real JAR/ZIP archives before installation.
- Invalid provider responses are rejected instead of being saved as fake `.jar` files.
- Failed temporary downloads are cleaned up.

### Hangar

- Improved release selection using Paper/Minecraft compatibility metadata when available.
- Added handling for exact versions, `.x` expressions and simple version ranges.

### SpigotMC / Spiget

- Added a metadata-based fallback when the direct free-resource download endpoint fails or returns an invalid JAR.
- Search no longer rejects otherwise valid free resources solely because `file.type` is absent.
- Premium and external/manual resources remain excluded from automatic installation.

### Error reporting

- Plugin installation now shows preparation and installation status.
- Provider/download errors are surfaced with useful details instead of only a generic `Error` message.

## Version

- App: `0.2.1`
- Installer: `TuffNode-Lite-v0.2.1.exe`
- Publisher: `dutu-dev - TuffNode`
- Platform: Windows 10 / 11 x64

## Upgrade

v0.2.1 keeps the existing TuffNode Lite installer identity, so it can be installed over v0.2.0 as an upgrade.

## Distribution

The official Windows installer is published as a GitHub Release asset in this public distribution repository. The application source code is maintained separately in a private repository and is not distributed here.

## Note

Automatic installation still depends on the selected Minecraft version, server loader and a downloadable compatible JAR being available from the third-party provider. Premium, external/manual-download or incompatible resources may still require manual `.jar` installation.
