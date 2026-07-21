***

# 🎛️ C4DashboardTool (Beta Edition)

A standalone Windows application for monitoring and controlling your **Control4** smart home system via the Director API. Just download, configure, and run.

> **🔐 BETA NOTICE:** This application is currently in an open Beta phase. It is hardcoded to run freely until **January 1, 2027**. After this date, a valid license key will be required to use the software.

---

## 📦 What's Included

| File | Purpose |
|------|---------|
| `C4DashboardTool.exe` | The main application (compiled Python executable) |
| `public_key.pem` | **Required** for license verification. Do not delete or move this file. |
| `.env` | Your credentials and settings (must be configured) |
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
| `LICENSE_KEY` | Currently bypassed by Beta Dateguard. Paste your license key here after Jan 1, 2027. |

### Step 3: Run the Application
Double-click `C4DashboardTool.exe`. 

A console window will appear showing connection logs, and your default browser will open the dashboard at `http://127.0.0.1:65003` (or your configured port).

---

## 🛡️ Licensing & Beta Status

### Current Beta Status
The application is currently in an open Beta phase. A hardcoded Dateguard allows the app to run freely without a key until **January 1, 2027**. 

The bottom-right corner of the dashboard will display the current status: 
`v260720 | Valid till Jan 01, 2027. Ask for license after.`

### Post-Beta Activation
After January 1, 2027, the application will enforce its secure licensing system and will require a valid license key to run. 
* **Keep `public_key.pem` safe:** This file is strictly required by the application to verify your license. **Never delete it or move it away from the `.exe` file.** If this file is missing, the application will not start.
* If you need a license key after the Beta period, please contact the developer.

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

### 🔌 Check That Your Port Is Free Before Launching
The application binds to the port specified in `C4_GUI_PORT` (default: **65003**). If another application — or **another running instance of C4DashboardTool itself** — is already using that port, the dashboard will fail to start.

**Before launching**, open **PowerShell** (run as Administrator for full details) and verify the port is not occupied:

```powershell
Get-NetTCPConnection -LocalPort 65003 -ErrorAction SilentlyContinue | ForEach-Object {
    $proc = Get-Process -Id $_.OwningProcess -ErrorAction SilentlyContinue
    [PSCustomObject]@{
        Port        = $_.LocalPort
        State       = $_.State
        PID         = $_.OwningProcess
        ProcessName = $proc.ProcessName
        Path        = $proc.Path
    }
} | Format-Table -AutoSize
```

- **No output** = the port is free ✅ — you're good to launch.
- **Output appears** = something is already using the port ⛔. You can either:
  1. **Kill the process:** `Stop-Process -Id <PID> -Force` (replace `<PID>` with the number shown).
  2. **Change the port:** Edit `C4_GUI_PORT` in your `.env` file to a different value (e.g., `65004`).

> **Tip:** Replace `65003` in the command above with whatever port you have configured in `.env`.

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
- **Version Tag:** A small tag in the bottom-right corner (e.g., `v260716 | Valid till Jan 01, 2027. Ask for license after.`) tracks the version and beta status.

### 🔒 Security & File Locations
- **Never share your `.env` file** — it contains your Control4 credentials.
- **Keep `public_key.pem` safe** — the application will not run without it.
- The `.exe` looks for all config files in the **same folder** as itself. If you move the `.exe`, you must move the `.env`, `dashboard_config.json`, and `public_key.pem` with it.

### 🔄 Updates
- When a new version of `C4DashboardTool.exe` is released, simply replace the old `.exe` and `public_key.pem` with the new ones. Keep your existing `.env` and `dashboard_config.json` files.

---

## 🛠️ Troubleshooting

| Issue | Solution |
|-------|----------|
| **"Access Denied" / Shows Fingerprint** | The beta period (ending Jan 1, 2027) has ended, or the license check failed. Ensure `public_key.pem` is in the same folder as the `.exe`. If the date has passed, contact the developer for a license. |
| **"Authentication failed"** | Handled automatically via background renewal. If it persists, check your credentials in `.env`. |
| **"dashboard.html is missing"** | The `.exe` cannot find its internal files. Ensure you downloaded the complete package. |
| **"Port already in use"** | Another application or a second instance of C4DashboardTool is occupying the port. Run the **PowerShell port check** from the [Important Notes](#-check-that-your-port-is-free-before-launching) section above to identify and stop the conflicting process, or change `C4_GUI_PORT` in `.env` to a different port (e.g., `65004`). |
| **Cannot connect from phone** | Ensure your phone and PC are on the same Wi-Fi. Allow `C4DashboardTool.exe` through Windows Firewall. |
| **Widgets show "ERR"** | The controller may be unreachable. Check your network connection and `C4_HOST` IP address. |

---

## 💻 System Requirements

- **OS:** Windows 10 or Windows 11 (64-bit)
- **Network:** Access to your Control4 controller on the local network
- **Browser:** Any modern browser (Chrome, Firefox, Edge, Safari)

---

## ⚖️ Disclaimer

This project is **unofficial** and not affiliated with, endorsed by, or supported by Control4 Corporation. Use at your own risk. The Director API is intended for integration partners; ensure compliance with your local smart home policies and network security standards.

---

## 💡 Tips

- **Run only one instance** of `C4DashboardTool.exe` at a time. A second instance will fail to start because the port is already occupied by the first. Use the [PowerShell port check](#-check-that-your-port-is-free-before-launching) if you're unsure whether an instance is already running.
- **Firewall:** If other devices can't connect, allow `C4DashboardTool.exe` through Windows Firewall for Private networks.
- **Performance:** Keep the number of active Textbox/Combo widgets reasonable to minimize polling load on your Control4 controller.

---

## 💡 Thanks to ->>

Inspired by the brilliant work of #lawtancool and his predecessors. Uses some code from https://github.com/lawtancool/pyControl4. Made by Qwen AI under human supervision.

---

## 📄 License

Free for personal use during the Beta period (valid until Jan 1, 2027). The application includes a secure licensing framework designed for authorized usage post-Beta.

---


