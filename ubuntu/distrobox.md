# Distrobox on Ubuntu WSL <span align="right">- Documentation.</span>

![This is an image](/images/distrobox.jpg)<br>
[:back:](/README.md) [home](/README.md) | **Distrobox**

<br>

### 📋 Notes
> Distrobox uses podman or docker to create containers highly integrated with the host. 
> This guide covers a clean reinstallation, container creation with shared volumes, and running GUI applications like Firefox.

<br>

### 🧹 Step 1: Clean Uninstall
> Before reinstalling, ensure all previous traces of Distrobox and Podman are removed.
> ```ruby
> # Stop and remove all containers
> $ distrobox stop --root --all
> $ distrobox rm --root --all --force
>
> # Uninstall Distrobox and Podman
> $ sudo apt purge distrobox podman -y
> $ sudo apt autoremove -y
> ```
> **Verification:** Run `distrobox list` (should be empty) and `which podman` (should return nothing).

<br>

### 🚀 Step 2: Reinstallation & Container Setup
> **2.1 Install Podman + Distrobox:**
> ```ruby
> $ sudo apt update
> $ sudo apt install podman distrobox -y
> ```

> **2.2 Create a Clean Ubuntu Container:**
> First, create the shared directory on your host:
> ```ruby
> $ mkdir -p ~/.local/share/distrobox/vm-shared
> ```
> Now, create the container with network admin capabilities and volume mapping:
> ```ruby
> $ distrobox create --root \
>   --name dev-ubuntu \
>   --image ubuntu:24.04 \
>   --volume ~/.local/share/distrobox/vm-shared:/home/ronaldoqj/shared:rw \
>   --additional-flags "--cap-add=NET_ADMIN --device /dev/net/tun"
> ```

> **Enter the container:**
> ```ruby
> $ distrobox enter --root dev-ubuntu
> ```

<br>

### 🌐 Step 3: GUI Application (Firefox)
> Perform these steps **inside** the Distrobox container (prompt should show `ronaldoqj@dev-ubuntu`).

> **3.1 Install Dependencies:**
> ```ruby
> $ sudo apt update && sudo apt install -y \
> libasound2t64 libdbus-1-3 libnss3 libxrandr2 libx11-xcb1 \
> libxkbcommon0 libxcomposite1 libxdamage1 libxfixes3 \
> libatk1.0-0t64 libatk-bridge2.0-0t64 libgtk-3-0t64 libglib2.0-0t64 \
> libxext6 libxrender1 wget nano
> ```

> **3.2 Install Official Firefox:**
> ```ruby
> # Download and extract Firefox
> $ mkdir -p ~/apps && cd ~/apps
> $ wget -O firefox.tar.bz2 "[https://download-installer.cdn.mozilla.net/pub/firefox/releases/134.0/linux-x86_64/en-US/firefox-134.0.tar.bz2](https://download-installer.cdn.mozilla.net/pub/firefox/releases/134.0/linux-x86_64/en-US/firefox-134.0.tar.bz2)"
> $ tar xjf firefox.tar.bz2
>
> # Setup binary links
> $ sudo mkdir -p /opt
> $ sudo mv firefox /opt/firefox
> $ sudo ln -sf /opt/firefox/firefox /usr/local/bin/firefox
> ```

> **3.3 Exporting to Host Menu:**
> To run Firefox from your main Ubuntu menu:
> ```ruby
> $ distrobox-export --app firefox
> ```

<br />

### 📌 Troubleshooting
> **Display Errors:** If Firefox fails to open from the host, run this on your **host terminal**:
> ```ruby
> $ xhost +local:
> ```

<br />

### 📂 References
> __External Links:__
> 
> - [$ Distrobox Official GitHub](https://github.com/89luca89/distrobox)
> - [$ Podman Documentation](https://podman.io/)

<br />

## 📋 Notes

#### Volume Permissions
> Files placed in `~/.local/share/distrobox/vm-shared` on your host will be available inside the container at `/home/ronaldoqj/shared`. Use this for persistent development files.
