# OpenVPN on Ubuntu WSL <span align="right">- Documentation.</span>

![This is an image](/images/openvpn_ubuntu.jpg)<br>
[:back:](/README.md) [home](/README.md) | **OpenVPN**

<br>

### 📋 Notes
> This tutorial guides the installation and configuration of OpenVPN on Ubuntu running on WSL, allowing a secure connection to the company's VPN.
> Based on official Ubuntu documentation, it covers everything from manual installation to automatic startup configuration on WSL boot.
> The setup utilizes **systemd** for auto-start, eliminating the need to manually reconnect during every session.

<br>

### 🛠️ Prerequisites
> * Ubuntu installed on WSL 2.
> * `.ovpn` file provided by the company (e.g., `company.ovpn`).
> * login and password access.
> * Root access via `sudo`.

<br>

### 🚀 Manual Installation
> ```ruby
> # 1. Install openVPN
> $ sudo apt install openvpn easy-rsa
> ```
>

> ```ruby
> # 2. Connect to the VPN (Login and password will be requested)
> $ sudo openvpn --config ~/vpn/MY_FILE.ovpn
> ```
>

> ```ruby
> # 3. Verify connection (Should return the company's IP)
> $ curl [https://ifconfig.me](https://ifconfig.me)
> ```
>

> **Note:** To use a browser through the VPN, install a browser within WSL: `sudo apt install firefox`. The connection requires an active terminal, and restarting Ubuntu will require manual reconnection.

<br>

### 🔐 Credentials File (Auto-login)
> ```ruby
> # 1. Create the credentials file
> $ sudo nano ~/vpn/auth.txt
>
> # Content of auth.txt:
> your_username
> your_password
> ```
>

> ```ruby
> # 2. Configure the .ovpn file
> $ sudo nano ~/vpn/MY_FILE.ovpn
>
> # Change the line: to:
> # from
> $ auth-user-pass
> # to
> $ auth-user-pass /home/YOUR_USERNAME/vpn/auth.txt
> ```
>

> **Note:** This way you can run the command sudo openvpn --config ~/vpn/MY_FILE.ovpn without needing to enter your username and password.


<br>

### 🔄 Auto-start on Linux and WSL Boot
> **Enable systemd:** In WSL 2, systemd is not active by default. Edit the `/etc/wsl.conf` file: (only to WSL)
> ```ruby
> [boot]
> systemd=true
> ```
> *After saving, restart WSL in Windows PowerShell with: `wsl --shutdown`*.

> **Configure the Service:**
> ```ruby
> # Move or copy files to the default directory
> $ sudo cp ~/vpn/auth.txt /etc/openvpn/client/auth.txt
> $ sudo cp ~/vpn/MY_FILE.ovpn /etc/openvpn/client/MY_FILE.conf
> ```
>

> **Note:** The MY_FILE.conf file can have any name, but it is good practice to keep the same name as the .ovpn file. Adjust the line that contains the path to the auth.txt file so it points to the new file inside /etc/openvpn/client/..

> ```ruby
> # Adjust paths and settings in the .conf file
> $ sudo nano /etc/openvpn/client/MY_FILE.conf
>
> # Change the line: to:
> # from
> $ auth-user-pass /home/meu_user/vpn/auth.txt
> # to
> $ auth-user-pass /etc/openvpn/client/auth.txt
> ```
>

> ```ruby
> # Start and verify the service
> $ sudo systemctl restart openvpn-client@MY_FILE
> $ sudo systemctl status openvpn-client@MY_FILE --no-pager -l
> ```
>

<br>

### 📌 Utilities
| Action | Command |
| :--- | :--- |
| **Stop VPN** | `sudo systemctl stop openvpn-client@MY_FILE` |
| **Start VPN** | `sudo systemctl start openvpn-client@MY_FILE` |
| **Disable auto-start** | `sudo systemctl disable openvpn-client@MY_FILE` |
| **Enable auto-start** | `sudo systemctl enable openvpn-client@MY_FILE` |


<br>

### 📂 References
> __Official Link:__
> 
> - [$ Ubuntu OpenVPN Documentation](https://ubuntu.com/server/docs/how-to/security/install-openvpn/)
