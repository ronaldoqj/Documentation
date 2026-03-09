# Multipass on Ubuntu WSL <span align="right">- Documentation.</span>

![This is an image](/images/multipass.png)
[:back:](/README.md) [home](/README.md) | **Multipass**

<br>

### 📋 Notes
> Multipass allows you to create and manage Ubuntu Virtual Machines within your environment.
> This guide covers advanced setup, including automated aliases, SOCKS proxy tunneling for internal network access, and VS Code remote development.
> The configuration aims to make the VM behave seamlessly, similar to a native WSL distribution.

<br>

### 🚀 Install & Setup
> **Launch Instance:** Create a high-performance Ubuntu 24.04 instance with specific resources.
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

### 🌐 Internal Network Access (SOCKS Tunnel)
> Access the VM's internal VPN or network services directly from your Host browser using a secure tunnel.

> **1. Get the VM Internal IP:**
> ```ruby
> $ multipass info ubuntu24 | grep IPv4
> # Example output: “IPv4: 10.19.41.25”
> ```

> **2. Open the SSH Tunnel:** Keep this terminal window open to maintain the "data pipe".
> ```ruby
> $ ssh -D 1080 ubuntu@10.19.41.25
> ```

> **3. Configure Browser (Firefox):**
> * Go to **Settings** > Search for **"Proxy"** > Click **Settings...**
> * Select **Manual proxy configuration**.
> * **SOCKS Host:** `127.0.0.1` | **Port:** `1080` | Select **SOCKS v5**.
> * **CRUCIAL:** Check the box **"Proxy DNS when using SOCKS v5"**.
> * **Tip:** Use the **FoxyProxy** extension to toggle this on/off with one click.

<br>

### 💻 VS Code Remote Development
> Connect your Host VS Code directly to the project files inside the Multipass VM via SSH.

> **1. Install Extension:**
> * Install **Remote - SSH** (by Microsoft) in your local VS Code.

> **2. Connect to Host:**
> * Click the green/blue icon (**><**) in the bottom-left corner.
> * Select **Connect to Host...** and enter: `ubuntu@10.19.41.25`.
> * VS Code will automatically install the server components inside the VM.

> **3. Open Project:**
> * Go to **File > Open Folder** and browse the VM's internal directories.
> * **Benefits:** Full IntelliSense support (reads `node_modules` inside the VM) and integrated terminal within the VM environment.

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