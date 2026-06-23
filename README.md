# 🎛️ C4DashboardTool (Beta Trial)

A standalone Windows application for monitoring and controlling your **Control4** smart home system via the Director API. Just download, configure, and run.

> **️ BETA TRIAL NOTICE:** This is a trial version of the application. It includes a built-in **Date Guard** that will automatically expire and stop running on **August 1, 2026**. Please contact the developer for the full, unrestricted version after this date.

---

##  What's Included

| File | Purpose |
|------|---------|
| `C4DashboardTool.exe` | The main application (compiled Python executable) |
| `.env` | Your credentials and settings (must be configured) |
| `dashboard_config.json` | Your dashboard layout and widgets (auto-managed) |

---

## 🚀 Quick Start

### Step 1: Download All Files
Ensure all three files (`C4DashboardTool.exe`, `.env`, `dashboard_config.json`) are in the **same folder** on your computer.

### Step 2: Configure `.env`
Open the `.env` file with any text editor (Notepad, VS Code, etc.) and update the following:

```env
C4_USERNAME="your_control4_email@example.com"
C4_PASSWORD="your_control4_password"
C4_HOST="192.168.1.XX"
C4_GUI_PORT=65001
C4_AUTO_OPEN_BROWSER=true
C4_POLLING_INTERVAL_MS=1000
```

| Variable | Description |
|----------|-------------|
| `C4_USERNAME` | Your Control4 account email |
| `C4_PASSWORD` | Your Control4 account password |
| `C4_HOST` | IP address of your Control4 controller (found in your router or Control4 app) |
| `C4_GUI_PORT` | Port for the web dashboard (default: 65001) |
| `C4_AUTO_OPEN_BROWSER` | `true` = opens browser automatically on startup |
| `C4_POLLING_INTERVAL_MS` | How often to refresh widget data (in milliseconds, default: 1000) |

### Step 3: Run the Application
Double-click `C4DashboardTool.exe`. 

A console window will appear showing connection logs, and your default browser will open the dashboard at `http://127.0.0.1:65001` (or your configured port).

---

## 🖥️ Using the Dashboard

### First Time Setup
1. Click **"Enter Setup Mode"** in the top-right corner.
2. Click **"🛠️ Add Widget"** to create your first widget.
3. Follow the 5-step wizard:
   - **Step 1:** Choose widget type (Button or Textbox)
   - **Step 2:** Select your device
   - **Step 3:** Choose a command or variable
   - **Step 4:** Configure parameters (if needed) and test
   - **Step 5:** Set a label, color, and assign to a room
4. Click **"✅ Save & Close"**

### Room Management
- Click **" Manage Rooms"** (in Setup Mode) to create rooms like "Living Room", "Kitchen", etc.
- Use the **Room Tabs** at the top to filter your view.
- In Setup Mode, click the **📂 folder badge** at the bottom-left of any widget to move it to a different room.

### Reordering Widgets
- In Setup Mode, drag widgets using the **⋮ handle** on the top-left.
- Widgets auto-save their order.

### Copying Text
- For Textbox widgets, simply click and drag to highlight the text, then press `Ctrl+C`.

---

## ⚠️ Important Notes

### ⏳ Trial Expiration Guard
This build contains a time-lock for beta testing purposes. 
* The application will function perfectly until **August 1, 2026**. 
* After this date, the application will display an "Access Expired" message and close automatically. 
* *Note for developers:* The date guard is implemented as a standalone function in `c4d_gui.py` and can be easily removed for the final production build.

### 📱 Mobile & Local Network Access
The server is configured to listen on `0.0.0.0`, allowing you to access the dashboard from your smartphone, tablet, or other PCs on your local Wi-Fi network.
1. Find your PC's local IP address (e.g., `192.168.1.50`).
2. Open Chrome on your phone and navigate to `http://192.168.1.50:65001`.
3. **Pro Tip:** Tap the Chrome menu (three dots) and select **"Add to Home screen"** to install it as a full-screen web app on your phone!

###  Security
- **Never share your `.env` file** — it contains your Control4 credentials in plain text.
- This repository is **private** for a reason. Do not make it public.
- If you accidentally commit your `.env` to a public repo, change your Control4 password immediately.

### 📁 File Locations
- The `.exe` looks for `.env` and `dashboard_config.json` in the **same folder** as itself.
- If you move the `.exe` to a different folder, you must move the config files with it.

### 🔄 Updates
- When a new version of `C4DashboardTool.exe` is released, simply replace the old `.exe` with the new one.
- Keep your existing `.env` and `dashboard_config.json` files — they are compatible across versions.

---

## 🛠️ Troubleshooting

| Issue | Solution |
|-------|----------|
| **"Access Expired"** | The trial period (ending Aug 1, 2026) has ended. Contact the developer for the full version. |
| **"Authentication failed"** | Check your `C4_USERNAME`, `C4_PASSWORD`, and `C4_HOST` in `.env`. Ensure your controller is online and Director API is enabled. |
| **"dashboard.html is missing"** | The `.exe` cannot find its internal files. Ensure you downloaded the complete package. |
| **"Port already in use"** | Change `C4_GUI_PORT` in `.env` to a different port (e.g., `65002`). |
| **Dashboard won't open** | Check the console window for errors. Ensure `C4_AUTO_OPEN_BROWSER=true` in `.env`. |
| **Cannot connect from phone** | Ensure your phone and PC are on the same Wi-Fi. Check Windows Firewall and allow `C4DashboardTool.exe` (or Python) through for Private networks. |
| **Widgets show "ERR"** | The controller may be unreachable. Check your network connection and `C4_HOST` IP address. |
| **High controller CPU usage** | Increase `C4_POLLING_INTERVAL_MS` to `3000` or `5000` to reduce request frequency. |

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
- **Firewall:** If other devices can't connect, allow `C4DashboardTool.exe` through Windows Firewall.
- **Performance:** For the best mobile experience, keep the number of active Textbox widgets reasonable to minimize polling load on your Control4 controller.

---

## 💡 Thanks to ->>

Inspired by the brilliant work of #lawtancool and his predecessors. Uses some code from https://github.com/lawtancool/pyControl4. Made by Qwen AI under human supervision


## 📄 License

Free for personal use untill the beta period is expired.
