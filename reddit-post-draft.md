# Reddit Post Draft for r/homeassistant

## Post Title
I created Squeeze Plex Hub - A Home Assistant add-on that bridges Plexamp to Squeezebox/LMS players

## Post Content

Hey r/homeassistant! 👋

I've been working on a Home Assistant add-on that I think many of you will find useful, especially if you're like me and have both Plex and Squeezebox/LMS players in your setup.

### What is Squeeze Plex Hub?

Squeeze Plex Hub is an add-on that bridges **Plexamp** with **Squeezebox** and **Lyrion Music Server (LMS)** players. It allows you to:

- **Stream Plex music to Squeezebox/LMS players** - Play your Plex music library through Squeezebox devices
- **Control from Plexamp** - Use the Plexamp app as your primary controller for Squeezebox players
- **Automatic discovery** - Uses Plexamp's GDM discovery to find Plex Media Server automatically
- **Web interface** - Simple web UI for monitoring and configuration

### Why I Built This

I've been using Squeezebox players for years and recently started using Plex for my music library. I wanted a way to control my Squeezebox players from Plexamp, so I built this bridge. It's been working great for me, and I thought others might find it useful too!

### Key Features

- 🎵 Seamless integration between Plexamp and Squeezebox/LMS ecosystems
- 🏠 Runs as a Home Assistant add-on with full integration
- 🔊 Multi-room audio support - Control multiple Squeezebox players from one interface
- 📱 Mobile control - Use Plexamp on your phone to control home audio
- 🔄 Auto-discovery - Automatically finds Plex Media Server via GDM
- 🌐 Web interface for configuration and monitoring

### Installation

**Quick Install (Recommended):**

[![Add Repository](https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg)](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2Fpserra77%2Flms-plexhub-ha-addon)

Click the button above to add this repository to your Home Assistant Add-on Store automatically.

**Manual Installation:**

1. Open Home Assistant web interface
2. Navigate to **Settings → Add-ons → Add-on Store**
3. Click the three-dot menu (⋮) in the top right
4. Select **Repositories**
5. Add: `https://github.com/pserra77/lms-plexhub-ha-addon`
6. Click **Add**
7. Find **Squeeze Plex Hub** in the add-on store
8. Click **Install**

### Requirements

- **Home Assistant OS** running on ARM64/aarch64 architecture (Raspberry Pi 4/5, Home Assistant Yellow, etc.)
- **Plex Media Server** running and accessible on your network
- **Squeezebox/LMS players** connected to your network
- **Plexamp app** installed on your control device (phone/tablet)

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

### Configuration

The add-on has minimal configuration options:

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `log_level` | list | `info` | Logging verbosity: `debug`, `info`, `warn`, `error` |

### Networking

This add-on uses **host networking** mode because Plexamp discovery requires UDP broadcast on port 32412.

**Port Requirements:**
- TCP 3000: Web interface
- UDP 32412: Plexamp GDM discovery

**Important:** If Plex Media Server is running on the same machine as Home Assistant, it may also try to bind UDP 32412. In this case, disable GDM discovery in Plex Media Server settings or run Plex Media Server on a different machine.

### Troubleshooting

**"No players found" in Plexamp:**
- Verify all devices are on the same network
- Check firewall settings for UDP 32412
- Restart Squeezebox players
- Restart the add-on

**Add-on fails to start:**
- Check add-on logs for specific error messages
- Verify ports are available (3000 and 32412)
- Stop conflicting services

**Enable debug logging:**
Set `log_level` to `debug` in the add-on configuration for detailed logging.

### Links

- **GitHub Repository:** https://github.com/pserra77/lms-plexhub-ha-addon
- **Documentation:** https://github.com/pserra77/lms-plexhub-ha-addon#readme
- **Issues:** https://github.com/pserra77/lms-plexhub-ha-addon/issues

### Support

If you encounter any issues or have questions:
1. Check the [README](https://github.com/pserra77/lms-plexhub-ha-addon#readme) for detailed documentation
2. Search existing [issues](https://github.com/pserra77/lms-plexhub-ha-addon/issues) on GitHub
3. Open a new issue with:
   - Home Assistant version
   - Add-on version
   - Architecture (ARM64)
   - Relevant log excerpts
   - Steps to reproduce

### Contributing

Contributions are welcome! If you'd like to contribute:
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

### License

This project is licensed under the MIT License.

---

**Enjoy your unified music experience!** 🎵

*Bridge the gap between Plexamp and Squeezebox with this Home Assistant add-on.*

---

## Posting Tips

### Best Time to Post
- **Weekdays** between **9 AM - 12 PM EST** (when most people are active)
- **Tuesday - Thursday** tend to have higher engagement

### Tags/Flair
- Use **"Project"** or **"Add-on"** flair if available
- Consider adding tags like `plex`, `squeezebox`, `lyrion`, `music`

### Engagement Tips
1. **Respond quickly** to comments and questions
2. **Be helpful** and provide troubleshooting tips
3. **Update the post** with any new features or fixes
4. **Thank people** for their feedback and suggestions

### Cross-posting
Consider sharing on these related subreddits:
- r/Plex - For Plex users
- r/squeezebox - For Squeezebox enthusiasts
- r/selfhosted - For self-hosting community
- r/opensource - For open source projects

### Reddit Rules to Follow
1. **No spam** - Don't post the same content repeatedly
2. **Be transparent** - Mention you're the author
3. **Engage with community** - Respond to comments
4. **Follow subreddit rules** - Check r/homeassistant rules before posting

### Example First Comment
When you post, consider adding a first comment like:

> "Hey everyone! I'm the author of this add-on. I've been using Squeezebox players for years and recently started using Plex for my music library. I wanted a way to control my Squeezebox players from Plexamp, so I built this bridge. It's been working great for me, and I thought others might find it useful too! Feel free to ask any questions or suggest improvements."
