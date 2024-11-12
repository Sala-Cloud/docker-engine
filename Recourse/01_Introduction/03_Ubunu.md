# Install Docker Engine on Ubuntu

To get started with Docker Engine on Ubuntu, make sure you meet the prerequisites, and then follow the installation steps.

## Prerequisites

### Firewall Configuration

- **Firewall Limitations**: Docker bypasses firewall rules when exposing container ports. If using `ufw` or `firewalld`, note that Docker container ports bypass these rules.
- **Supported Rulesets**: Ensure firewall rulesets are created with `iptables` or `ip6tables`. Avoid `nft` as it's unsupported by Docker.

### OS Requirements

Make sure you're using a 64-bit version of one of these supported Ubuntu versions:

- Ubuntu 24.10 (Oracular)
- Ubuntu 24.04 LTS (Noble)
- Ubuntu 22.04 LTS (Jammy)
- Ubuntu 20.04 LTS (Focal)

Docker Engine for Ubuntu is compatible with the following architectures:
- `x86_64` (amd64)
- `armhf`
- `arm64`
- `s390x`
- `ppc64le` (ppc64el)

### Remove Conflicting Packages

Before installing Docker, uninstall any conflicting packages. Run this command:

```bash
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
