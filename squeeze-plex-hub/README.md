# Squeeze Plex Hub Home Assistant add-on

This add-on runs the ARM64 image `onmomo/squeeze-plex-hub` on Home Assistant OS.

## Installation

1. Push this repository to GitHub.
2. In Home Assistant, open **Settings → Apps → Install app**.
3. Open the three-dot menu and choose **Repositories**.
4. Add the repository URL.
5. Install **Squeeze Plex Hub**.
6. Start it and open its web UI.

## Networking

The add-on uses host networking because Plexamp discovery requires UDP `32412`.
Ensure Plex Media Server does not bind UDP `32412` on the same host. Keep Plex's
other GDM ports if desired: UDP `32410`, `32413`, and `32414`.

The web interface is exposed on TCP `3000`.

## ARM64 image requirement

The image must provide an ARM64/aarch64 manifest. If installation reports that no
ARM64 image exists, build and publish an ARM64 image or run Squeeze Plex Hub on a
separate Linux host.

## Troubleshooting

Use add-on logs with `log_level: debug`. If the add-on fails to start, check for
another process already using UDP `32412`.
