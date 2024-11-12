# Install Docker Engine

This section describes how to install Docker Engine on Linux (Docker CE). Docker Engine is also available for Windows, macOS, and Linux through Docker Desktop. For installation instructions for Docker Desktop, see:

- [Docker Desktop for Linux](https://docs.docker.com/desktop/install/linux-install/)
- [Docker Desktop for Mac (macOS)](https://docs.docker.com/desktop/install/mac-install/)
- [Docker Desktop for Windows](https://docs.docker.com/desktop/install/windows-install/)

---

## Supported Platforms

| Platform          | x86_64 / amd64 | arm64 / aarch64 | arm (32-bit) | ppc64le | s390x |
|-------------------|----------------|------------------|--------------|---------|-------|
| CentOS            | ✅             | ✅               |              | ✅      |       |
| Debian            | ✅             | ✅               | ✅           | ✅      |       |
| Fedora            | ✅             | ✅               |              | ✅      |       |
| Raspberry Pi OS   |                |                  | ✅           |         |       |
| RHEL              | ✅             | ✅               |              |         | ✅     |
| SLES              |                |                  |              |         | ✅     |
| Ubuntu            | ✅             | ✅               | ✅           | ✅      | ✅     |
| Binaries          | ✅             | ✅               | ✅           |         |       |

---

## Installation Notes for Linux Derivatives

Docker Engine may work on derivatives of supported Linux distributions, but Docker does not test or verify these installations. Here are some guidelines:

- **Debian Derivatives**: For Debian-based distributions like *BunsenLabs Linux*, *Kali Linux*, or *LMDE (Debian-based Mint)*, follow the [Debian installation instructions](https://docs.docker.com/engine/install/debian/).
- **Ubuntu Derivatives**: For Ubuntu-based distributions like *Kubuntu*, *Lubuntu*, or *Xubuntu*, follow the [Ubuntu installation instructions](https://docs.docker.com/engine/install/ubuntu/).

**Note**: Some Linux distributions provide their own Docker Engine packages in their repositories, which may have modifications. Bugs in these packages should be reported to the Linux distribution's support channels.

### Manual Installation Using Binaries

Docker provides statically linked binaries for Docker Engine, allowing manual installation on any Linux distribution. See [Docker Engine binaries](https://docs.docker.com/engine/installation/binaries/) for more information.

---

## Release Channels

Docker Engine offers two update channels:

- **Stable**: Latest versions available for general use.
- **Test**: Pre-release versions for testing and feedback. Use with caution, as these versions may contain breaking changes.

---

## Support

Docker Engine is an open-source project supported by Moby project maintainers and the community. Docker provides support for its products, such as Docker Desktop, but does not provide support for Docker Engine itself.

For more on the Moby project, visit the [Moby project website](https://mobyproject.org/).

---

## Upgrade Path

Patch releases are backward compatible within the major and minor version series.

---

## Licensing

Docker Engine is licensed under the [Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0).

---

## Reporting Security Issues

If you discover a security issue, please do not report it publicly. Instead, email security@docker.com to report it privately. Security reports are greatly appreciated, and Docker will acknowledge your contribution.
