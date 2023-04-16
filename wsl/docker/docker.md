# Docker in WLS 2 (without Docker-Desktop) <span align="right">- Documentation.</span>

![This is an image](/images/docker-on-windows.jpg)
[:back:](/README.md) [home](/README.md) | **Docker**

<br>

### 📋 Notes
> For this installation you don't need have docker installation on your windows.<br>
> If you have docker installed you can uninstall it.

<br>

### 🚀 Install Docker / Docker Compose v2 in WSL 2
> ```ruby
> # Install Docker, you can ignore the warning from Docker about using WSL
> $ curl -fsSL https://get.docker.com -o get-docker.sh
> $ sudo sh get-docker.sh
> ```

> ```ruby
> # Add your user to the Docker group
> $ sudo usermod -aG docker $USER
> ```

> ```ruby
> # Install Docker Compose v2
> $ sudo apt-get update && sudo apt-get install docker-compose-plugin
> ```

> ```ruby
> # Sanity check that both tools were installed successfully
> $ docker --version
> $ docker compose version
> ```

> ```ruby
> # Using Ubuntu 22.04 or Debian 10 / 11? You need to do 1 extra step for iptables
> # compatibility, you'll want to choose option (1) from the prompt to use iptables-legacy.
> $ sudo update-alternatives --config iptables
> ```

> **Obs:** Ensure the Docker Service Runs in WSL 2 At the time of this post systemd isn’t started inside of WSL 2 by default. <br>
> All you have to do is drop this into your ~/.profile, .zprofile or equivalent file:
> ```ruby
>
> # Settings to Docker
> if grep -q "microsoft" /proc/version > /dev/null 2>&1; then
>   if service docker status 2>&1 | grep -q "is not running"; then
>     wsl.exe --distribution "${WSL_DISTRO_NAME}" --user root \
>       --exec /usr/sbin/service docker start > /dev/null 2>&1
>   fi
> fi
> ```

> **Checking installation -** The idea here is the Docker service will get started if it’s not already running.
> The first time this runs it’ll hang your terminal for a few seconds. However, even if you close your terminal the next time you open it,
> it will open instantly since Docker will already be running. Closing your terminal will not stop Docker, only rebooting Windows or fully shutting down WSL will.
> ```ruby
> 
> # You can run the command below to see the Docker daemon running:
> $ ps aux | grep docker
> ```

> **Hello world -** After opening a new terminal you should now be able to run below without **"sudo"**.
> ```ruby
>
> $ docker run hello-world

<br />


### 📌 Extras
> __Reference link:__
> 
> - [$ nickjanetakis.com](https://nickjanetakis.com/blog/install-docker-in-wsl-2-without-docker-desktop)
> 

<br />

## 📋 Notes

#### Source of images and volumes on disk
> Also if you’re coming from Docker Desktop and want to investigate your images and volumes on disk you can access them in cd /var/lib/docker.
> You’ll need to be the root user. This is the default spot where Docker saves files on Linux.
