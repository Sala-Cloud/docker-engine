# Installing Docker

Docker can be installed on various operating systems. This chapter will guide you through installing Docker on Linux, macOS, and Windows.

## Installing Docker on Linux

To install Docker on a Linux system, follow these steps:

```bash
# Update the package database
sudo apt-get update

# Install Docker dependencies
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

# Add Docker's official GPG key
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# Add the Docker repository
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Install Docker
sudo apt-get install docker-ce docker-ce-cli containerd.io
