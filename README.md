***

# 🎛️ C4DashboardTool (Licensed Edition)

A standalone Windows application for monitoring and controlling your **Control4** smart home system via the Director API. Just download, configure, and run.

> **🔐 LICENSE NOTICE:** This application uses a secure, offline **Hardware-Locked RSA Licensing** system. It is tied to your specific machine's hardware fingerprint. Please contact the developer to obtain your unique activation key.

---

## 📦 What's Included

| File | Purpose |
|------|---------|
| `C4DashboardTool.exe` | The main application (compiled Python executable) |
| `public_key.pem` | **Required** for license verification (Do not delete) |
| `.env` | Your credentials, settings, and license key (must be configured) |
| `dashboard_config.json` | Your dashboard layout and widgets (auto-managed) |

---

## 🚀 Quick Start

### Step 1: Download All Files
Ensure all four files (`C4DashboardTool.exe`, `public_key.pem`, `.env`, `dashboard_config.json`) are in the **same folder** on your computer.

### Step 2: Configure `.env`
Open the `.env` file with any text editor (Notepad, VS Code, etc.) and update the following:

```env
C4_USERNAME="your_control4_email@example.com"
C4_PASSWORD="your_control4_password"
C4_HOST="192.168.1.XX"
C4_GUI_PORT=65003
C4_AUTO_OPEN_BROWSER=true
C4_POLLING_INTERVAL_MS=1000
NTP_ADDRESS="89.109.251.21"
LICENSE_KEY=""
```

| Variable | Description |
|----------|-------------|
| `C4_USERNAME` | Your Control4 account email |
| `C4_PASSWORD` | Your Control4 account password |
| `C4_HOST` | IP address of your Control4 controller |
| `C4_GUI_PORT` | Port for the web dashboard (default: 65003) |
| `C4_AUTO_OPEN_BROWSER` | `true` = opens browser automatically on startup |
| `C4_POLLING_INTERVAL_MS` | How often to refresh widget data (in milliseconds) |
| `NTP_ADDRESS` | NTP server used for secure time verification (optional) |
| `LICENSE_KEY` | **Paste your unique activation key here** (provided by developer) |

### Step 3: Run the Application
Double-click `C4DashboardTool.exe`. 

A console window will appear showing connection logs, and your default browser will open the dashboard at `http://127.0.0.1:65003` (or your configured port).

---

## 🛡️ Activation & Licensing

### First-Time Activation
If you run the application without a `LICENSE_KEY` in your `.env` file, you will see an **"Access Denied"** screen in your browser. This screen displays your unique **Machine Fingerprint**:

> **Your Machine Fingerprint:**
> * **OS GUID:** `a1b2c3d4...`
> * **CPU ID:** `Intel Core i7...`
> * **MAC Address:** `00:1A:2B...`

**To activate the software:**
1. Copy the text from the "Access Denied" screen.
2. Send it to the developer.
3. The developer will generate a unique, cryptographically signed License Key tied to your hardware.
4. Paste the key into the `LICENSE_KEY=""` line in your `.env` file.
5. Restart `C4DashboardTool.exe`. The dashboard will now load, and the bottom-right corner will display `License valid till [Date]`.

### Hardware Upgrades (2-out-of-3 Rule)
The licensing system is designed to be forgiving. It checks three hardware IDs (OS GUID, CPU ID, and MAC Address). **As long as 2 out of the 3 IDs match**, your license will remain valid. 
* *Example:* If you upgrade your network card (changing the MAC address), your license will still work because the OS and CPU match.
* *Note:* If you replace your entire motherboard and reinstall Windows, all 3 IDs will change, and you will need to request a new key from the developer.

---

## 🛠️ Using the Dashboard

### First Time Setup
1. Click **"Enter Setup Mode"** in the top-right corner.
2. Click **"🛠️ Add Widget"** to create your first widget.
3. Follow the wizard:
   - **Step 1:** Choose widget type: **Button**, **Textbox**, **Combo-Button**, or **MACRO**.
   - **Step 2:** Select your device(s) using the **Quick Search bar**. 
   - **Step 3/4:** Configure commands, variables, parameters, and **Dynamic Color Rules**. For MACROs, build your timeline and use the **Test** button.
   - **Step 5:** Set a label and assign to a room.
4. Click **"✅ Save & Close"**.

### ✨ Features & UI Improvements

**MACRO Widget (Scene Director)**
A powerful new widget type for executing complex batch commands. 
- **Parallel & Serial Execution:** Commands in the same row run concurrently; rows run sequentially.
- **Configurable Delays:** Add a delay (up to 60 seconds) before *any* row executes.
- **Visual Feedback:** The widget pulses with a smooth color animation while running.

**Unsaved Macro Testing**
Test your MACRO timelines directly from the setup wizard using the **Test** button before saving.

**Quick Device Search**
Instantly filter your Control4 devices by name or ID in the setup wizard instead of scrolling through long lists.

**Refined UI Defaults**
Widgets default to a sleek light gray accent (`#aaaaaa`) with fixed title colors, ensuring high readability regardless of dynamic color rules.

**Dynamic Color Rules**
Automatically change a widget's **Left Border Accent and Background Tint** based on specific variable values (e.g., Green for "True", Red for "Error").

**Combo-Button (2-in-1 Widget)**
A hybrid widget that acts as a clickable button to send a command while simultaneously polling and displaying a live status variable.

**Cleaner Pure Buttons & Optimized Code**
Standard Buttons are rendered as clean, compact cards. The frontend code is heavily optimized for faster load times on mobile devices.

**Room Management & Reordering**
- Create rooms and filter views via tabs.
- Drag and drop widgets using the **⋮ handle** in Setup Mode.
- The dashboard uses a **Masonry Layout** to dynamically resize widgets without stretching rows.

---

## ⚠️ Important Notes

### 🔄 Automatic Token Renewal
Control4 authentication tokens expire every 24 hours. This application features **background auto-renewal**. If a token expires, the system silently catches the error, re-authenticates, and retries. You will never need to manually restart the app.

### 📱 Mobile & Local Network Access
The server listens on `0.0.0.0`, allowing access from smartphones, tablets, or other PCs on your local Wi-Fi.
1. Find your PC's local IP address (e.g., `192.168.1.50`).
2. Navigate to `http://192.168.1.50:65003` on your mobile device.
3. **Pro Tip:** Tap the Chrome menu and select **"Add to Home screen"** to install it as a full-screen web app!

### 🛡️ Smart UI Features
- **Smart Shutdown Button:** Hidden on mobile devices to prevent accidental server shutdowns.
- **Mobile Setup Restriction:** Setup controls are hidden on mobile to keep the interface clean.
- **Version Tag:** A small tag in the bottom-right corner (e.g., `v260715 | License valid till 2027-01-01`) tracks the version and license status.

### 🔒 Security
- **Never share your `.env` file** — it contains your Control4 credentials and license key.
- **Keep `public_key.pem` safe** — the application will not run without it.

###  File Locations & Updates
- The `.exe` looks for all config files in the **same folder** as itself.
- When a new version of `C4DashboardTool.exe` is released, simply replace the old `.exe` and `public_key.pem` with the new ones. Keep your existing `.env` and `dashboard_config.json`.

---

## 🛠️ Troubleshooting

| Issue | Solution |
|-------|----------|
| **"Access Denied" / Shows Fingerprint** | No `LICENSE_KEY` is present in `.env`. Copy the fingerprint and send it to the developer to receive your key. |
| **"Hardware mismatch"** | You changed too much hardware. The system requires 2 out of 3 IDs (OS, CPU, MAC) to match. Contact the developer for a new key. |
| **"Invalid License Key"** | Ensure `public_key.pem` is in the same folder as the `.exe`, and the key in `.env` is copied exactly without extra spaces. |
| **"Authentication failed"** | Handled automatically via background renewal. If it persists, check your credentials in `.env`. |
| **"dashboard.html is missing"** | The `.exe` cannot find its internal files. Ensure you downloaded the complete package. |
| **"Port already in use"** | Change `C4_GUI_PORT` in `.env` to a different port (e.g., `65004`). |
| **Cannot connect from phone** | Ensure your phone and PC are on the same Wi-Fi. Allow `C4DashboardTool.exe` through Windows Firewall. |
| **Widgets show "ERR"** | The controller may be unreachable. Check your network connection and `C4_HOST` IP address. |

---

## 📊 System Requirements

- **OS:** Windows 10 or Windows 11 (64-bit)
- **Network:** Access to your Control4 controller on the local network
- **Browser:** Any modern browser (Chrome, Firefox, Edge, Safari)

---

## 📜 Disclaimer

This project is **unofficial** and not affiliated with, endorsed by, or supported by Control4 Corporation. Use at your own risk. The Director API is intended for integration partners; ensure compliance with your local smart home policies and network security standards.

---

## 💡 Tips

- **Run only one instance** of `C4DashboardTool.exe` at a time to avoid overloading your controller.
- **Firewall:** If other devices can't connect, allow `C4DashboardTool.exe` through Windows Firewall for Private networks.
- **Performance:** Keep the number of active Textbox/Combo widgets reasonable to minimize polling load on your Control4 controller.

---

## 💡 Thanks to ->>

Inspired by the brilliant work of #lawtancool and his predecessors. Uses some code from https://github.com/lawtancool/pyControl4. Made by Qwen AI under human supervision.

---

## 📄 License

Licensed for personal use. The application utilizes a secure, offline Hardware-Locked RSA licensing framework to ensure authorized usage.
