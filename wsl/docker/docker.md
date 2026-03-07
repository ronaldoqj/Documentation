# Docker Engine on Ubuntu WSL <span align="right">- Documentation.</span>

![This is an image](/images/docker-on-windows.jpg)
[:back:](/README.md) [home](/README.md) | **Docker**

<br>

### 📋 Notes
> This documentation covers the installation of Docker Engine on Ubuntu via the official Docker repository.
> This method is recommended for users who want a native Linux experience within WSL 2 without relying on Docker Desktop.

<br>

### 🚀 Install Docker Engine
> ```ruby
> # 1. Update the apt package index and install certificates
> $ sudo apt update
> $ sudo apt install ca-certificates curl
> ```
>

> ```ruby
> # 2. Add Docker's official GPG key
> $ sudo install -m 0755 -d /etc/apt/keyrings
> $ sudo curl -fsSL [https://download.docker.com/linux/ubuntu/gpg](https://download.docker.com/linux/ubuntu/gpg) -o /etc/apt/keyrings/docker.asc
> $ sudo chmod a+r /etc/apt/keyrings/docker.asc
> ```
>

> ```ruby
> # 3. Add the repository to Apt sources
> $ sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
> Types: deb
> URIs: [https://download.docker.com/linux/ubuntu](https://download.docker.com/linux/ubuntu)
> Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
> Components: stable
> Signed-By: /etc/apt/keyrings/docker.asc
> EOF
> ```
>

> ```ruby
> # 4. Install the Docker packages
> $ sudo apt update
> $ sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
> ```
>

<br>

### ✅ Verification
> **Check Service Status -** Verify if the Docker daemon is active and running:
> ```ruby
> $ sudo systemctl status docker
> ```
>

> **Hello World -** Run a test container to ensure the installation was successful:
> ```ruby
> $ sudo docker run hello-world
> ```
>

<br />

### 📌 Extras
> __Reference link:__
> 
> - [$ Docker Official Documentation](https://docs.docker.com/engine/install/ubuntu/#installation-methods)

<br />

## 📋 Notes

#### Systemd Requirement
> Ensure that **systemd** is enabled in your `/etc/wsl.conf` for the `systemctl` commands to work correctly. If it is not enabled, you can start the service manually using `sudo service docker start`.
