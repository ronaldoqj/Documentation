# VPN Network <span align="right">- Documentation.</span>

![This is an image](/images/vpn_network.jpg)
[:back:](/README.md) [home](/README.md) | **OpenVPN**

<br>

### 📋 Notes
> While using the terminal is excellent for debugging, having a toggle switch directly in the Ubuntu taskbar makes daily use much easier.
> This guide explains how to import your `.ovpn` file into the Ubuntu (GNOME) Network Manager for a seamless graphical experience.

<br>

### 🚀 Step 1: Install Dependencies
> Although Ubuntu has basic support, you often need the specific plugin for Network Manager to parse OpenVPN files correctly.
> ```ruby
> # Update repositories and install the GNOME OpenVPN plugin
> $ sudo apt update && sudo apt install network-manager-openvpn-gnome -y
> ```

<br>

### 📥 Step 2: Import the .ovpn File
> 1. Click the **Network icon** in the top-right corner of your screen and select **Settings**.
> 2. In the left sidebar, click on **Network**.
> 3. Look for the **VPN** section and click the **+ (plus)** button.
> 4. **The key step:** Instead of selecting "OpenVPN", choose the last option: **Import from file...**.
> 5. Navigate to your folder and select your `.ovpn` file (e.g., `company_vpn.ovpn`).

<br>

### ⚙️ Step 3: Authentication & Tweaks
> A window will appear with most settings pre-filled from your file.
> * **Credentials:** Enter your **Username** and **Password**. 
> * **Password Storage:** Click the icon in the password field to select "Store the password for all users" if you don't want to type it every time.
> * **Finalize:** Click **Add** in the top-right corner.

<br>

### 🔄 How to Connect/Disconnect
> You no longer need the terminal for daily use:
> 1. Click the **Status Menu** (where Wi-Fi/Battery icons are).
> 2. Select **VPN Off**.
> 3. Click **Connect**.

<br />

### 📌 Troubleshooting
> **The "Certificate Error":**
> If the connection fails immediately, check if your `.ovpn` file refers to external certificate files (`.ca`, `.crt`) that might be missing from the folder. 
> * **Tip:** "All-in-one" files (where keys are embedded inside the text) usually work on the first try without issues.

<br />

### 📂 References
> __External Links:__
> 
> - [$ GNOME Help - VPN Setup](https://help.gnome.org/users/gnome-help/stable/net-vpn-connect.html.en)
> - [$ NetworkManager Official Site](https://networkmanager.dev/)
