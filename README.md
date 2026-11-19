# XRP-Ghostlink

**Portable Raspberry Pi Tailscale Travel Node**

XRP-Ghostlink is a headless Raspberry Pi travel node designed to connect to configured Wi-Fi networks and route internet traffic through an existing Tailscale exit node.

The project is intended for portable use, allowing a Raspberry Pi to connect to a trusted remote network through Tailscale while traveling.

Optional Ethernet sharing is planned for compatible hardware, allowing a connected device to use the same routed connection without installing Tailscale individually.

> [!WARNING]
> **Project Status: Under Development**
>
> The existing installation and uninstallation scripts are prototypes and have not been validated against current Raspberry Pi OS networking defaults.
>
> The scripts and manual procedures require further development and testing before use on a deployed system.

## Purpose

XRP-Ghostlink provides a portable Tailscale client for use on external networks.

Unlike XRP-Portkey and XRP-Waystone, which are intended to operate as remote Tailscale exit nodes, XRP-Ghostlink is designed to connect through an existing exit node.

The intended use cases include:

- Automatically connecting to configured Wi-Fi networks.
- Routing internet traffic through a selected Tailscale exit node.
- Accessing approved remote network resources through Tailscale.
- Providing optional Ethernet connectivity for downstream devices.
- Recovering network and Tailscale connectivity after a reboot.

## Architecture

The intended network path is:

```text
Travel Wi-Fi / Hotspot
        |
        v
  XRP-Ghostlink
  Raspberry Pi
        |
        v
  Tailscale Client
        |
        v
Encrypted Tailscale Tunnel
        |
        v
Remote Tailscale Exit Node
        |
        v
     Internet
```

Optional Ethernet sharing, when supported and configured, would allow a downstream client to route through XRP-Ghostlink.

XRP-Ghostlink does not need to advertise itself as an exit node to perform its intended role.

## Features

The following capabilities are part of the intended design. They have not yet been fully validated.

- Headless Raspberry Pi operation.
- Automatic connection to configured Wi-Fi networks.
- Tailscale authentication and persistent device identity.
- Selection of an existing Tailscale exit node.
- Optional Ethernet sharing using DHCP and NAT.
- Automatic recovery after reboot.
- Installation and uninstallation scripts.
- Manual setup and troubleshooting documentation.

The existing scripts provide an initial implementation of several features. Their behavior requires review and correction before deployment.

## Prerequisites

The intended deployment requires:

- A compatible Raspberry Pi running Raspberry Pi OS Lite.
- Network access through Wi-Fi or another supported interface.
- A Tailscale account and access to the tailnet.
- An existing, authorized Tailscale exit node.
- Administrative access to configure the Raspberry Pi.
- Appropriate network hardware for optional Ethernet sharing.

Hardware requirements and supported Raspberry Pi OS versions will be finalized during development.

Networks requiring captive-portal authentication may need additional setup before Tailscale connectivity is available.

## Repository Structure

```text
xrp-ghostlink/
├── README.md
├── LICENSE
├── .gitignore
├── scripts/
│   ├── install-ghostlink.sh
│   └── uninstall-ghostlink.sh
└── docs/
    ├── manual-setup.md
    ├── manual-setup-beginner.md
    ├── verification.md
    ├── troubleshooting.md
    └── uninstall-instructions.md
```

## Installation

### Clone the Repository

```bash
git clone https://github.com/CenterfireXid/xrp-ghostlink.git
cd xrp-ghostlink
```

### Automated Installation

The installer is located at:

```text
scripts/install-ghostlink.sh
```

The current installer is interactive and includes configuration for Wi-Fi, Tailscale, optional Ethernet sharing, and boot persistence.

**Do not execute the installer yet.** The networking configuration and persistence mechanisms require revision and validation.

A tested installation procedure will be documented after the script overhaul.

### Manual Installation

The repository includes two manual installation references:

- [Manual Setup](docs/manual-setup.md)
- [Beginner-Friendly Manual Setup](docs/manual-setup-beginner.md)

Both documents describe the original installation architecture and are pending revision.

## Verification

The intended verification process includes:

1. Confirming Wi-Fi connectivity and internet access.
2. Confirming the Tailscale service is operational.
3. Verifying Tailscale authentication and device identity.
4. Confirming the selected exit node is being used.
5. Testing DNS resolution and internet connectivity.
6. Testing optional Ethernet sharing, when configured.
7. Confirming the configuration survives a reboot.

The existing checklist is available in [Verification](docs/verification.md).

A successful installation has not yet been established by these procedures on the redesigned Ghostlink configuration.

## Troubleshooting

The existing [Troubleshooting Guide](docs/troubleshooting.md) covers:

- Wi-Fi connection failures.
- DHCP and DNS issues.
- Tailscale authentication.
- Exit-node selection and routing.
- Optional Ethernet sharing.
- Boot persistence.

The procedures require review before use with the redesigned installer.

## Backup and Recovery

Tailscale device identity is stored locally, including sensitive state under:

```text
/var/lib/tailscale/
```

The Tailscale state must be treated as sensitive information and must never be committed to GitHub.

Wi-Fi credentials, authentication keys, and other local secrets must also remain outside the public repository.

A complete backup and clean-install recovery procedure will be finalized after the configuration system is redesigned.

## Uninstallation

The uninstaller is located at:

```text
scripts/uninstall-ghostlink.sh
```

See [Uninstall Instructions](docs/uninstall-instructions.md) for the original procedure and current limitations.

**Do not execute the uninstaller until its networking changes, removal behavior, and recovery safeguards have been reviewed.**

## Roadmap

- [ ] Redesign Wi-Fi configuration for current Raspberry Pi OS networking defaults.
- [ ] Implement safe handling of multiple configured Wi-Fi networks.
- [ ] Review Tailscale authentication and exit-node selection.
- [ ] Correct boot persistence and connectivity recovery.
- [ ] Review optional Ethernet sharing and hardware requirements.
- [ ] Implement secure configuration and secret handling.
- [ ] Address captive-portal limitations.
- [ ] Add installation pre-checks and error handling.
- [ ] Correct and validate the uninstallation process.
- [ ] Test installation, reboot persistence, and recovery.
- [ ] Update manual setup, verification, and troubleshooting documentation.

## License

XRP-Ghostlink is licensed under the MIT License.

See [LICENSE](LICENSE) for the full license text.
