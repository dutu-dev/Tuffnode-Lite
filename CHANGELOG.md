# TuffNode Lite Changelog

This changelog documents the product history of TuffNode Lite. The public distribution repository contains release information and binaries only; the application source code is maintained privately.

---

## v0.2.1 — 2026-09-10

TuffNode Lite v0.2.1 is a focused reliability patch for the plugin/mod installation workflow introduced in v0.2.0.

The primary issue in v0.2.0 was that add-ons could already be discovered in **Plugins → Browse** before a new server had ever been started, but the Install command required the server profile to already be provisioned. This created a broken state where a user could browse compatible plugins and press Install, but installation would not proceed.

### Plugin installation lifecycle

- Removed the early `IsProvisioned` gate that blocked marketplace installation on newly configured servers.
- Plugin/mod installation now prepares and provisions the selected Minecraft server automatically when required.
- The automatic preparation step resolves the server build, Java runtime, server directory and concrete Minecraft version before trying to install an add-on.
- Normal server startup and add-on installation now share the same provisioning path instead of duplicating the lifecycle logic.
- Local `.jar` drag-and-drop also uses the automatic preparation path if the server has not yet been provisioned.
- Managed Geyser installation can now prepare the server automatically instead of requiring the user to start the server first.
- File-system watching and Installed-list refresh are reinitialized after automatic provisioning so newly installed files appear immediately.

### Minecraft version resolution

- Fixed add-on search behavior when the selected version is `Latest stable` and the server has not yet been provisioned.
- Lite now resolves a concrete Minecraft release through the server provider catalog before applying compatibility filters.
- Explicitly selected Minecraft versions continue to be used directly.
- Changing the configured Minecraft version now triggers a fresh plugin/mod search so the results match the new compatibility target.
- Custom JAR servers avoid pretending that Lite knows a concrete Minecraft version when one has not been resolved.

### Modrinth reliability

- Reworked Modrinth version resolution to try compatible loaders individually in priority order.
- Paper servers can fall back across Paper, Spigot and Bukkit-compatible project releases.
- Purpur servers can fall back across Purpur, Paper, Spigot and Bukkit-compatible project releases.
- Spigot uses Spigot and Bukkit candidates.
- CraftBukkit uses Bukkit and Spigot candidates.
- Fabric, Forge and NeoForge keep their native loader filters.
- The literal `Latest stable` label is no longer sent to Modrinth as a Minecraft version facet.
- Version downloads use the concrete Minecraft version actually selected/resolved by Lite.
- File selection now prefers the provider-designated primary `.jar` and otherwise uses the first valid JAR.
- Auxiliary files such as sources/Javadocs are ignored for installation.

### HTTP / JAR download pipeline

- Removed the shared global `Accept: application/json` header from the add-on HTTP client.
- JSON API calls now request `application/json` only on JSON requests.
- JAR downloads request Java archive / binary content instead of inheriting a JSON-only header.
- Increased the content-service timeout to better tolerate slower provider/CDN downloads.
- Downloaded files are validated as ZIP/JAR archives before being moved into the live plugin/mod directory.
- HTML error pages, proxy responses and other invalid payloads are rejected instead of being left behind with a `.jar` extension.
- Failed temporary `.download` files are cleaned up automatically.
- Content-service User-Agent now identifies TuffNode Lite v0.2.1.

### Hangar reliability

- Improved Hangar release selection instead of blindly taking the first returned build.
- Lite checks Paper platform compatibility metadata where available.
- Exact Minecraft versions are supported.
- `.x` compatibility expressions are supported.
- Simple minimum-to-maximum version ranges are supported.
- If compatibility metadata is absent or incomplete, Lite falls back to the newest returned release rather than immediately refusing installation.

### SpigotMC / Spiget reliability

- The direct Spiget free-resource download endpoint remains the preferred installation path.
- Added a metadata-based download fallback when the direct endpoint returns an HTTP error or invalid JAR payload.
- Search no longer removes otherwise valid free resources solely because Spiget omitted the `file.type` field.
- Explicit non-JAR resources are still excluded.
- Premium and external/manual resources remain excluded from automatic installation.

### Error reporting and UX

- Installing from Browse now shows a preparation state while Lite provisions a new server.
- The status changes to the selected add-on name while the provider download is running.
- Provider/download exceptions are surfaced in the Plugins view instead of collapsing every failure to a generic `Error` message.
- Error messages are capped to keep the compact UI usable.
- Enable/disable, delete, Geyser and several setup/settings operations now retain more actionable error details.

### Release / installer

- Application version updated to `0.2.1`.
- Assembly and file versions updated to `0.2.1.0`.
- Inno Setup installer metadata updated to v0.2.1 while retaining the existing `AppId={{TuffNode-Lite}}` for upgrade compatibility.
- Installer output renamed to `TuffNode-Lite-v0.2.1.exe`.
- Installer release-notes payload now points to `docs/releases/v0.2.1.md`.
- `INSTALL-NOTES.txt` now describes the v0.2.1 plugin-installation fixes.
- Publisher remains `dutu-dev - TuffNode`.

### Compatibility note

- Automatic installation still depends on a third-party provider exposing a downloadable JAR compatible with the selected Minecraft version and loader.
- Premium, external/manual-download or incompatible resources may still require manual `.jar` installation.
- Add-on changes generally require a Minecraft server restart before the plugin/mod becomes active.

---

## v0.2.0 — 2026-09-10

TuffNode Lite v0.2.0 is the first major product-shape refactor after the initial beta. The application moves away from the larger beta dashboard and becomes a compact, single-server Windows control surface focused on fast startup, direct server control, add-on management and the settings most people actually need.

### Product direction and interface

- Rebuilt the Lite shell around a compact single-server workflow instead of a reduced version of the Community interface.
- Replaced the previous large desktop shell with a compact 520 × 620 window.
- Added a four-tab top navigation model: Server, Console, Plugins and Settings.
- Added a compact custom title bar with TuffNode Lite branding, minimize, close and direct Settings access.
- Added native window dragging and a custom border/chrome treatment.
- Reworked spacing, cards, controls and navigation around the Lite-specific Electric Cyan accent (#38BDF8).
- Replaced native-looking white Windows controls with fully themed WPF controls for Dark and Snow themes.
- Added slim custom scrollbars so scrolling no longer visually dominates compact pages.
- Added a dedicated compact first-run setup surface instead of the previous full-size setup wizard.
- Added Run setup again in Settings so the setup flow can be reopened later without deleting the existing server world.
- Preserved setup state across restarts when a new setup is started but not completed.

### Server setup and providers

- Restored a guided first-run setup designed specifically for one local server.
- Added real provider selection from the server catalog:
  - Paper
  - Purpur
  - Vanilla
  - Spigot
  - CraftBukkit
  - Fabric
  - Forge
  - NeoForge
  - Custom .jar
- Added Minecraft version selection per supported provider.
- Added automatic server-version lookup for managed providers.
- Added configurable RAM during setup.
- Added Custom JAR selection and provisioning.
- Provider changes now invalidate the old provisioning state so Lite does not silently reuse the wrong runtime/server binary.
- Minecraft version changes also force reprovisioning when required.
- Setup choices are persisted locally and reused after restart.

### Managed Java and server runtime

- Consolidated Lite onto a single runtime path based on LiteServerEngineV2.
- Removed the superseded V1 runtime engine to avoid two competing start/stop implementations.
- Added automatic Java runtime discovery/provisioning for managed server types.
- Added safe process execution with redirected asynchronous stdout/stderr.
- Added reliable one-click start and stop behavior.
- Graceful stop continues to use the Minecraft stop command before process exit.
- Added safe exit behavior when closing the application while the server is running.
- Added Custom JAR runtime support.
- Added first-free-port allocation when the preferred Java port is already occupied.
- When Lite selects a replacement port, it updates server.properties before launch.
- Persisted runtime-selected ports after successful startup.
- Kept the dashboard/tray on the actually active port until a restart applies a newly configured port.

### Server dashboard

- Added a compact status pill for stopped, starting and online states.
- Added live uptime while the server is running.
- Added a single large Start Server / Stop Server hero action.
- Added real Java-process telemetry:
  - working-set RAM
  - CPU usage
  - TPS where the selected server supports TPS reporting
- Added direct connection information to the first page.
- Added separate Local IP and Public IP rows with copy actions.
- Added Windows Firewall status.
- Added Bedrock/Geyser connection rows when Geyser is enabled.
- Added separate Java and Bedrock endpoints so users do not confuse the two connection types.
- Added contextual copy feedback for connection addresses.
- Added preset quick commands directly on the Server dashboard:
  - list players
  - save world
  - TPS
  - send server message
  - whitelist on
  - whitelist off
- Quick-command actions are disabled when the server is not running.

### Console

- Added a dedicated Console tab instead of mixing console output into the main server view.
- Added live stdout/stderr streaming from the Minecraft process.
- Added direct command input.
- Pressing Enter sends the current command.
- Commands may be entered with or without a leading slash.
- Added Send and Clear controls.
- Added optional auto-scroll.
- Added a bounded console buffer to avoid unlimited UI memory growth.
- Quick commands and manually entered commands use the same server command pipeline.

### Minecraft settings

- Added a dedicated Settings tab with real server.properties integration.
- The Settings view re-reads the current server.properties when opened so external edits can be reflected in Lite.
- Added editable MOTD.
- Added Difficulty selection.
- Added Game Mode selection.
- Added Render Distance / view-distance.
- Added Simulation Distance.
- Added Max Players.
- Added Java server port.
- Added Spawn Protection.
- Added Online Mode.
- Added PvP.
- Added Whitelist.
- Added Allow Flight.
- Added Command Blocks.
- Saving writes the values back to the actual server configuration.
- Lite indicates when a server restart is required for changes to take effect.
- Server settings are also reflected in the persisted Lite profile.

### Plugins and mods

- Rebuilt the add-on surface around two dedicated sub-tabs: Browse and Installed.
- Browse is now focused only on discovery and installation.
- Installed is focused only on add-ons already present on disk.
- Added real source filtering for plugin-capable servers:
  - All sources
  - Modrinth
  - Hangar
  - SpigotMC
- Fabric, Forge and NeoForge use Modrinth as the managed mod source.
- Vanilla exposes no fake plugin marketplace sources.
- Search results include provider/source information, descriptions and download counts.
- Added direct Install actions from Browse.
- Added a live FileSystemWatcher for the active add-on directory.
- Installed add-ons update automatically when files are added, removed or renamed.
- Added local .jar drag-and-drop installation.
- Added Enable / Disable by renaming .jar and .jar.disabled.
- Disabled add-ons remain visible and can be re-enabled later.
- Added Delete with confirmation.
- Added installed add-on count.
- Added direct Open plugins folder / add-on folder access.
- Added restart-required guidance when modifying add-ons while the server is running.

### Geyser / Bedrock support

- Added Geyser as a first-class managed add-on instead of relying on a random marketplace result.
- Geyser is surfaced on compatible Java plugin servers: Paper, Purpur, Spigot and CraftBukkit.
- Added Install, Enable and Disable actions.
- Geyser state is synchronized with the real Geyser-Spigot.jar / disabled file on disk.
- Removing or disabling Geyser updates the persisted Lite profile state.
- When enabled, the Server dashboard shows Bedrock local/public connection endpoints and the configured Bedrock port.

### Network behavior

- Added local IPv4 discovery.
- Added public IP discovery.
- Added Java local/public socket display.
- Added Bedrock local/public socket display when Geyser is active.
- Added copy actions for every displayed endpoint.
- Public-IP display is informational only and does not imply that NAT, router port forwarding or firewall rules are configured.
- Improved active-port reporting when Lite automatically changes the server port at launch.

### Themes and visual system

- Added semantic theme resources instead of hardcoded control colors.
- Added Dark theme.
- Added Snow theme.
- Added Lite-specific Electric Cyan accent.
- Theme switching is applied live without restarting the application.
- Added themed buttons, inputs, combo boxes, checkboxes, sliders and scrollbars.
- Fixed dark-theme controls that previously fell back to native white Windows rendering.
- Updated selected-tab and hover states for the compact navigation model.

### Localization

- Added the native loc:Tr binding flow for Lite.
- Added live language switching without application restart.
- Added an embedded catalog for 18 languages:
  - English
  - Română
  - Deutsch
  - Français
  - Español
  - Português (Brasil)
  - Polski
  - Italiano
  - Nederlands
  - Čeština
  - Magyar
  - Svenska
  - Türkçe
  - Українська
  - Русский
  - 日本語
  - 한국어
  - 简体中文
- Reused established TuffNode terminology from the wider product where possible.
- Fixed language selectors so the UI shows the native language name instead of the raw LocaleInfo object representation.

### Windows integration and tray behavior

- Added app-lite.ico branding to the application.
- Added separate idle and running tray icons.
- Tray status changes with the Minecraft server state.
- Tray tooltip reports TuffNode Lite server state and active Java port.
- Added optional Start TuffNode Lite on Windows startup.
- Startup registration uses the current-user Windows Run key and launches Lite with --minimized.
- Added configurable close-button behavior: Minimize to System Tray or Exit Application.
- Minimize-to-tray is the default behavior.
- If Exit Application is selected while the server is running, Lite asks for confirmation and performs a graceful server shutdown before exiting.

### Build, release and engineering cleanup

- Application version metadata is now 0.2.0.
- The solution builds on .NET 10.
- CI builds use -warnaserror.
- v0.2.0 was validated with zero build warnings and zero build errors.
- Added semantic localization/settings contracts.
- Added one application settings service for theme, language, startup and close behavior.
- Removed the old large MainWindow shell.
- Removed the old ServerPanel view and view model.
- Removed the old SetupWizard view and view model.
- Removed the old Installed Add-ons popup.
- Removed the old title-bar and Sync panel UI from the compact Lite shell.
- Removed superseded theme dictionaries and control styles.
- Removed the V1 server engine.
- Reduced the number of competing UI/runtime paths so Lite has one primary single-server workflow.

### Changed from v0.1.0-beta.1

- The large beta dashboard has been replaced by the compact four-tab shell.
- The old full-size setup wizard has been replaced by an embedded compact setup flow.
- Installed add-ons are no longer managed in a separate popup; they now have their own Plugins → Installed sub-tab.
- The dedicated Players administration surface from the beta is not part of the v0.2.0 compact shell.
- Common player/server actions are available through quick commands and the Console.
- TuffNode Sync is no longer exposed as a primary panel in the compact v0.2.0 shell.
- The v0.2.0 UI prioritizes one local server, direct control and low navigation overhead.

### Notes and known limitations

- Public IP discovery does not configure router NAT or port forwarding.
- Some server.properties changes require a Minecraft server restart.
- Add-on changes generally require a restart before the server loads the new plugin/mod state.
- Geyser is managed only on compatible plugin-based Java server providers.
- BuildTools-based and modded providers can take significantly longer to provision than Paper/Purpur/Vanilla.
- Official public distribution remains binary-only; application source code is not published in the public release repository.

---

## v0.1.0-beta.1 — 2026-08-30

First public beta of TuffNode Lite.

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
- Local .jar plugin import.
- Installed plugins read from the real server plugins folder.
- Enable, disable and uninstall installed plugins.
- Disabled plugins remain visible and can be enabled again later.
- Installed plugins were managed in a separate popup.

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
- Published server snapshots included server state, addresses, ports, provider and version information.
- TuffNode Shield posture checks for Windows Firewall state and secure defaults.

### Interface

- Custom TuffNode Lite window chrome.
- Fixed standard viewport across Overview, Players, Add-ons, Console and Settings.
- Custom dark scrollbars and tab content styling.
- Add-ons marketplace redesigned around a larger browsing area.

### Beta notes

- This was an early testing release and behavior was expected to change before the first stable Lite direction.
- TuffNode Sync published to the local TuffNode Sync registry; a remote/cloud Sync backend was not included.
- Internet joins required appropriate network configuration such as router port forwarding unless another networking layer was used.
- Forge, NeoForge and BuildTools-based providers required broader validation across Minecraft versions and environments.
- The application source code was not publicly distributed.
