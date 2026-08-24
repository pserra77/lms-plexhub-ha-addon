# Squeeze Plex Hub Home Assistant Add-on

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-Add--on-blue.svg)](https://www.home-assistant.io/)
[![Architecture](https://img.shields.io/badge/Architecture-ARM64-purple.svg)](https://github.com/onmomo/squeeze-plex-hub)
[![Add Repository](https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg)](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2Fpserra77%2Flms-plexhub-ha-addon)

> Bridge Plexamp to Squeezebox and Lyrion Music Server players

## Overview

Squeeze Plex Hub is a Home Assistant add-on that seamlessly integrates Plexamp with Squeezebox and Lyrion Music Server (LMS) players. This bridge allows you to control your Squeezebox/LMS devices directly from Plexamp, creating a unified music experience across your home audio system.

### What It Does

- **Stream Plex music to Squeezebox players** - Play your Plex music library through Squeezebox/LMS devices
- **Control from Plexamp** - Use the Plexamp app as your primary controller for Squeezebox devices
- **Automatic discovery** - Uses Plexamp's GDM discovery to find Plex Media Server automatically
- **Web interface** - Simple web UI for monitoring and configuration

### Key Features

- 🎵 **Seamless Integration** - Bridges Plexamp and Squeezebox/LMS ecosystems
- 🏠 **Home Assistant Native** - Runs as a Home Assistant add-on with full integration
- 🔊 **Multi-room Audio** - Control multiple Squeezebox players from one interface
- 📱 **Mobile Control** - Use Plexamp on your phone to control home audio
- 🔄 **Auto-discovery** - Automatically finds Plex Media Server via GDM
- 🌐 **Web Interface** - Easy-to-use web UI for configuration and monitoring

## Prerequisites

Before installing this add-on, ensure you have:

### Hardware Requirements

- **Home Assistant OS** running on ARM64/aarch64 architecture
  - Raspberry Pi 4/5 (64-bit OS)
  - Home Assistant Yellow
  - Other ARM64-based Home Assistant installations

### Software Requirements

- **Home Assistant** version 2023.1 or newer
- **Plex Media Server** running and accessible on your network
- **Squeezebox/LMS players** connected to your network
- **Plexamp app** installed on your control device (phone/tablet)

### Network Requirements

- All devices (Home Assistant, Plex Media Server, Squeezebox players) must be on the same local network
- UDP port 32412 must be available for Plexamp discovery
- TCP port 3000 must be available for the web interface

## Installation

### Quick Install (Recommended)

[![Add Repository](https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg)](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2Fpserra77%2Flms-plexhub-ha-addon)

Click the button above to add this repository to your Home Assistant Add-on Store automatically.

### Manual Installation

If you prefer manual installation:

1. **Add the repository to Home Assistant:**
   - Open Home Assistant web interface
   - Navigate to **Settings → Add-ons → Add-on Store**
   - Click the three-dot menu (⋮) in the top right
   - Select **Repositories**
   - Add: `https://github.com/pserra77/lms-plexhub-ha-addon`
   - Click **Add**

2. **Install the add-on:**
   - Find **Squeeze Plex Hub** in the add-on store
   - Click **Install**
   - Wait for installation to complete

3. **Configure and start:**
   - Open the add-on configuration
   - Set your preferred log level (default: `info`)
   - Click **Start**

4. **Access the web interface:**
   - Open the add-on panel
   - Click **Open Web UI**
   - Or navigate to `http://your-home-assistant-ip:3000`

### Developer Installation

If you want to install from source:

```bash
# Clone the repository
git clone https://github.com/pserra77/lms-plexhub-ha-addon.git

# Copy to Home Assistant add-ons directory
cp -r lms-plexhub-ha-addon/squeeze-plex-hub /addons/

# Restart Home Assistant
# Then install via the add-on store
```

## Configuration

### Add-on Options

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `log_level` | list | `info` | Logging verbosity: `debug`, `info`, `warn`, `error` |

### Configuration Example

```yaml
log_level: debug  # Use 'debug' for troubleshooting
```

### Environment Variables

The add-on automatically configures these environment variables:

- `NITRO_PORT`: Web interface port (default: 3000)
- `NITRO_LOG_LEVEL`: Log level for the Nitro framework

## Networking

### Port Requirements

| Port | Protocol | Purpose |
|------|----------|---------|
| 3000 | TCP | Web interface |
| 32412 | UDP | Plexamp GDM discovery |

### Host Networking

This add-on uses **host networking** mode because Plexamp discovery requires UDP broadcast on port 32412. This means:

- The add-on shares the network stack with Home Assistant
- No port mapping is needed
- UDP broadcasts work correctly for device discovery

### Important Network Notes

1. **Plex Media Server Conflict**: If Plex Media Server is running on the same machine as Home Assistant, it may also try to bind UDP 32412. In this case:
   - Disable GDM discovery in Plex Media Server settings, OR
   - Run Plex Media Server on a different machine

2. **Firewall Rules**: Ensure UDP 32412 is not blocked by your firewall

3. **VLAN Segmentation**: If your devices are on different VLANs, UDP broadcasts may not work. Ensure proper network configuration.

## Usage

### Getting Started

1. **Start the add-on** and verify it's running
2. **Open Plexamp** on your phone or tablet
3. **Discover devices**: Plexamp should automatically discover your Squeezebox players
4. **Select a player**: Choose a Squeezebox player from the Plexamp interface
5. **Play music**: Start playing music from your Plex library

### Web Interface

The web interface provides:

- **Player status**: See which Squeezebox players are connected
- **Now playing**: View current playback information
- **Logs**: Access real-time logs for troubleshooting
- **Configuration**: Adjust settings if needed

### Advanced Usage

#### Multiple Plex Libraries

If you have multiple Plex libraries, configure them in Plexamp:

1. Open Plexamp settings
2. Go to **Libraries**
3. Add or configure your music libraries
4. The bridge will automatically sync available libraries

#### Multi-room Audio

Squeezebox/LMS supports multi-room audio:

1. Group players in LMS web interface
2. Use Plexamp to control the group
3. Enjoy synchronized playback across rooms

## Troubleshooting

### Common Issues

#### "No players found" in Plexamp

**Possible causes:**
- Squeezebox players not powered on or connected to network
- UDP port 32412 blocked by firewall
- Devices on different network segments

**Solutions:**
1. Verify all devices are on the same network
2. Check firewall settings for UDP 32412
3. Restart Squeezebox players
4. Restart the add-on

#### Add-on fails to start

**Possible causes:**
- Port 3000 already in use
- Port 32412 already in use
- Insufficient permissions

**Solutions:**
1. Check add-on logs for specific error messages
2. Verify ports are available:
   ```bash
   # Check if ports are in use
   netstat -tuln | grep -E '3000|32412'
   ```
3. Stop conflicting services
4. Restart the add-on

#### Audio stuttering or gaps

**Possible causes:**
- Network congestion
- Wi-Fi interference
- Squeezebox player limitations

**Solutions:**
1. Use wired connections where possible
2. Reduce network load during playback
3. Check Squeezebox player firmware is up to date
4. Use 5GHz Wi-Fi for wireless players

### Debug Logging

To enable detailed logging:

1. Open add-on configuration
2. Set `log_level` to `debug`
3. Restart the add-on
4. View logs in the web interface or Home Assistant add-on panel

### Log Analysis

Common log messages and their meanings:

| Log Message | Meaning | Action |
|-------------|---------|--------|
| `Starting Squeeze Plex Hub` | Add-on initializing | Normal startup |
| `Listening on port 3000` | Web interface ready | Ready to use |
| `GDM discovery started` | Looking for Plex servers | Normal operation |
| `Player connected: [name]` | Squeezebox player found | Ready to stream |
| `Connection refused` | Cannot reach Plex server | Check Plex settings |

### Getting Help

If you encounter issues not covered here:

1. **Check the logs** with `log_level: debug`
2. **Search existing issues** on [GitHub](https://github.com/pserra77/lms-plexhub-ha-addon/issues)
3. **Open a new issue** with:
   - Home Assistant version
   - Add-on version
   - Architecture (ARM64)
   - Relevant log excerpts
   - Steps to reproduce

## Architecture

### How It Works

```
┌─────────────┐     ┌─────────────────┐     ┌──────────────────┐
│   Plexamp   │────▶│ Squeeze Plex Hub│────▶│ Squeezebox/LMS   │
│  (Mobile)   │     │  (Add-on)       │     │    Players        │
└─────────────┘     └─────────────────┘     └──────────────────┘
                           │
                           ▼
                    ┌─────────────────┐
                    │  Plex Media     │
                    │  Server         │
                    └─────────────────┘
```

1. **Plexamp** discovers Squeeze Plex Hub via GDM (UDP 32412)
2. **Squeeze Plex Hub** receives playback commands from Plexamp
3. **Squeeze Plex Hub** translates commands for Squeezebox/LMS players
4. **Squeezebox/LMS** streams music from Plex Media Server

### Technology Stack

- **Base Image**: `onmomo/squeeze-plex-hub` (ARM64)
- **Framework**: Nitro (Node.js)
- **Discovery**: Plexamp GDM protocol
- **Control**: Squeezebox/LMS CLI protocol

## Contributing

Contributions are welcome! Here's how you can help:

### Reporting Issues

1. Check existing issues first
2. Include detailed reproduction steps
3. Provide log excerpts (use `log_level: debug`)
4. Specify your Home Assistant version and architecture

### Submitting Changes

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

### Development Setup

```bash
# Clone the repository
git clone https://github.com/pserra77/lms-plexhub-ha-addon.git
cd lms-plexhub-ha-addon

# Make changes to squeeze-plex-hub/
# Test in your Home Assistant environment
# Submit PR
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- [Squeeze Plex Hub](https://github.com/onmomo/squeeze-plex-hub) - The original bridge project
- [Lyrion Music Server](https://lyrion.org/) - Successor to Squeezebox Server
- [Plexamp](https://www.plex.tv/products/plexamp/) - Beautiful music player
- [Home Assistant](https://www.home-assistant.io/) - Open source home automation
- [Squeezebox Community](https://forums.slimdevices.com/) - For their continued support

## Support

- **Documentation**: [GitHub README](https://github.com/pserra77/lms-plexhub-ha-addon)
- **Issues**: [GitHub Issues](https://github.com/pserra77/lms-plexhub-ha-addon/issues)
- **Community**: [Home Assistant Community](https://community.home-assistant.io/)

## Important Note: HACS vs Add-on Store

This is a **Home Assistant Add-on**, not a HACS integration. Here's the difference:

- **Home Assistant Add-on Store** - Manages add-ons like this one. Add-ons run as containers alongside Home Assistant.
- **HACS (Home Assistant Community Store)** - Manages custom integrations, themes, and plugins. These extend Home Assistant's functionality differently.

**To install this add-on:** Use the Add-on Store (instructions above), NOT HACS.

If you're looking for a Squeezebox integration for Home Assistant (not an add-on), check the [Squeezebox integration](https://www.home-assistant.io/integrations/squeezebox/) in Home Assistant Core.

---

**Enjoy your unified music experience!** 🎵

*Bridge the gap between Plexamp and Squeezebox with this Home Assistant add-on.*
