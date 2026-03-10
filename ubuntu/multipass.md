# Multipass on Ubuntu WSL <span align="right">- Documentation.</span>

![This is an image](/images/multipass.png)
[:back:](/README.md) [home](/README.md) | **Multipass**

<br>

### 📋 Notes
> Multipass allows you to create and manage Ubuntu Virtual Machines within your environment.
> This guide covers advanced setup, including automated aliases, SOCKS proxy tunneling, and port mirroring.
> The goal is to make the VM behave seamlessly, similar to a native WSL distribution.

<br>

### 🚀 Install & Setup
> **Launch Instance:** Create a high-performance Ubuntu 24.04 instance.
> ```ruby
> # Launching the instance with 4 CPUs, 6GB RAM, and 200GB Disk
> $ multipass launch 24.04 --name ubuntu24 --cpus 4 --memory 6G --disk 200G
> ```

> **Automation (Bash Aliases):** Add these to your `~/.bashrc` to manage your VM with short commands.
> ```ruby
> # Create aliases for quick access
> $ echo "alias ubuntu='multipass shell ubuntu24'" >> ~/.bashrc
> $ echo "alias ubuntu-list='multipass list'" >> ~/.bashrc
> $ echo "alias ubuntu-stop='multipass stop ubuntu24'" >> ~/.bashrc
> $ echo "alias ubuntu-start='multipass start ubuntu24'" >> ~/.bashrc
>
> # Refresh terminal to apply changes
> $ source ~/.bashrc
> ```
> **Usage:** Simply type `$ ubuntu` to enter the VM and `$ exit` to leave.

<br>

### 🌐 Accessing Localhost Applications
> When running applications (like Angular or APIs) inside the VM, you have two main ways to access them from your Host.

#### Option A: Direct IP Access (No Mirroring)
> Run your application binding to `0.0.0.0` inside the VM:
> ```ruby
> # Run Angular on 0.0.0.0 to allow external access
> $ ng serve --host 0.0.0.0
> $ ng serve --host 0.0.0.0 --port 4201
> ```
> **Access via Host Browser:** Use the VM's internal IP (e.g., `http://10.19.41.25:4200`).

#### Option B: Host Port Mirroring (SSH Tunneling)
> If you prefer to access the VM services using `http://localhost` on your Host browser, use SSH Port Forwarding:
> ```ruby
> # Mirror a single port (4200)
> $ ssh -L 4200:localhost:4200 ubuntu@10.19.41.25
>
> # Mirror multiple ports (Angular 1, Angular 2, and API)
> $ ssh -L 4200:localhost:4200 -L 4201:localhost:4201 -L 8080:localhost:8080 ubuntu@10.19.41.25
> ```

> **⚠️ Troubleshooting (Invalid Host Header):** If Angular refuses the connection on `localhost`, run it with the host check disabled inside the VM:
> ```ruby
> $ ng serve --host 0.0.0.0 --disable-host-check
> ```

<br>

### 🔄 Dynamic SOCKS Tunneling
> The SOCKS tunnel is dynamic. You can run multiple services in the VM and access them all through the Host browser by keeping a single tunnel open:
>
> * **Angular 1 (Port 4200):** `http://10.19.41.25:4200`
> * **Angular 2 (Port 4201):** `http://10.19.41.25:4201`
> * **API (Port 8080):** `http://10.19.41.25:8080`
>
> **SSH Command:** `$ ssh -D 1080 ubuntu@10.19.41.25`. Configure your browser or **FoxyProxy** extension to use SOCKS v5 on `127.0.0.1:1080`.

<br>

### 💻 VS Code Remote Development
> Connect your Host VS Code directly to the project files inside the Multipass VM via SSH.

> **1. Connect to Host:** Click the green icon (**><**) and enter: `ubuntu@10.19.41.25`. <br>
> **2. Workflow:** Open the VS Code terminal and run `ng serve --host 0.0.0.0`. Access it via Firefox with the FoxyProxy enabled. <br>
> **3. Benefits:** Professional, isolated, and fast environment with real IntelliSense.

<br />

### 📌 Summary Table
| Action | Shortcut Alias |
| :--- | :--- |
| **Enter VM** | `$ ubuntu` |
| **List Instances** | `$ ubuntu-list` |
| **Start VM** | `$ ubuntu-start` |
| **Stop VM** | `$ ubuntu-stop` |

<br />

### 📂 References
> __External Links:__
> 
> - [$ Multipass Documentation](https://multipass.run/docs)
> - [$ Remote development over SSH](https://code.visualstudio.com/docs/remote/ssh)
