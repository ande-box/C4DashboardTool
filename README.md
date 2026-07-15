***

# ️ C4DashboardTool (Beta Trial)

A standalone Windows application for monitoring and controlling your **Control4** smart home system via the Director API. Just download, configure, and run.

> **⚠️ BETA TRIAL NOTICE:** This is a trial version of the application. It includes a built-in **Date Guard** that will automatically expire and stop running at the end of licensed period. Please contact the developer for the full, unrestricted version after this date.

---

## 📦 What's Included

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
C4_GUI_PORT=65003
C4_AUTO_OPEN_BROWSER=true
C4_POLLING_INTERVAL_MS=1000
```

| Variable | Description |
|----------|-------------|
| `C4_USERNAME` | Your Control4 account email |
| `C4_PASSWORD` | Your Control4 account password |
| `C4_HOST` | IP address of your Control4 controller (found in your router or Control4 app) |
| `C4_GUI_PORT` | Port for the web dashboard (default: 65003) |
| `C4_AUTO_OPEN_BROWSER` | `true` = opens browser automatically on startup |
| `C4_POLLING_INTERVAL_MS` | How often to refresh widget data (in milliseconds, default: 1000) |

### Step 3: Run the Application
Double-click `C4DashboardTool.exe`. 

A console window will appear showing connection logs, and your default browser will open the dashboard at `http://127.0.0.1:65003` (or your configured port).

---

## ️ Using the Dashboard

### First Time Setup
1. Click **"Enter Setup Mode"** in the top-right corner.
2. Click **"🛠️ Add Widget"** to create your first widget.
3. Follow the wizard:
   - **Step 1:** Choose widget type: **Button** (Command only), **Textbox** (Status only), **Combo-Button** (Command + Status), or **MACRO** (Batch Commands).
   - **Step 2:** Select your device(s) using the **Quick Search bar** to instantly filter by name or ID. 
   - **Step 3/4:** Configure commands, variables, parameters, and **Dynamic Color Rules**. For MACROs, build your timeline and use the **Test** button to verify it before saving.
   - **Step 5:** Set a label and assign to a room.
4. Click **"✅ Save & Close"**.

### ✨ Features & UI Improvements

**MACRO Widget (Scene Director)**
A powerful new widget type for executing complex batch commands. 
- **Parallel & Serial Execution:** Commands in the same row run concurrently; rows run sequentially (top to bottom).
- **Configurable Delays:** Add a delay (up to 60 seconds) before *any* row executes, perfect for waiting on devices to boot or respond.
- **Visual Feedback:** The widget pulses with a smooth color animation while running, and the text area displays the active commands.

**Unsaved Macro Testing**
You can now test your MACRO timelines directly from the setup wizard. Click the **Test** button to run your sequence and verify it works perfectly before saving it to your dashboard.

**Quick Device Search**
The widget setup wizard now includes a quick-search text field above device dropdowns. Instantly filter your Control4 devices by name or ID instead of scrolling through long lists.

**Refined UI Defaults**
Widgets now default to a sleek light gray accent (`#aaaaaa`) with fixed title colors. This ensures high readability and a professional look, regardless of what dynamic color rules are triggered.

**Dynamic Color Rules (Colorized Conditions)**
Automatically change a widget's **Left Border Accent and Background Tint** based on specific variable values. 
- **How it works:** In the wizard, define conditions (e.g., if value is `True` turn Green, if `Error` turn Red). 
- **Simplified Logic:** If the variable's value does not match any of your custom rules, the widget automatically defaults to the standard light gray theme color. The title text remains fixed for a clean, consistent look.

**Combo-Button (2-in-1 Widget)**
The **Combo-Button** is a hybrid widget that acts as a clickable button to send a command (like a light toggle) while simultaneously polling and displaying a live status variable (like the light's current state).

**Cleaner Pure Buttons**
Standard **Button** widgets no longer display an empty status text area. They are rendered as clean, compact cards showing only their label, making the dashboard look much tidier.

**Optimized Frontend Code**
The dashboard HTML, CSS, and JavaScript have been heavily optimized and minified. This results in a significantly smaller file size and much faster load times, especially when accessing the dashboard from mobile devices over local Wi-Fi.

**Room Management**
- Click **"🏠 Manage Rooms"** (in Setup Mode) to create rooms like "Living Room", "Kitchen", etc.
- Use the **Room Tabs** at the top to filter your view.
- In Setup Mode, click the **📂 folder badge** at the bottom-left of any widget to move it to a different room.

**Reordering Widgets**
- In Setup Mode, drag widgets using the **⋮ handle** on the top-left.
- Widgets auto-save their order. The dashboard uses a **Masonry Layout**, meaning widgets will dynamically resize to fit their content without stretching the entire row.

**Copying Text**
- For Textbox, Combo-Button, and MACRO widgets, simply click and drag to highlight the text, then press `Ctrl+C` (native text selection).

---

## ⚠️ Important Notes

### ⏳ Trial Expiration Guard & NTP Verification
This build contains a time-lock for beta testing purposes. 
* The application will function perfectly until **January 1, 2027**. 
* **NTP Verification:** The application first attempts to verify the current time against an NTP server to prevent local clock tampering. If the NTP server is unreachable, it falls back to the local system time.
* After the expiration date, the application will display an "Access Expired" message and close automatically. 


### 🔄 Automatic Token Renewal
Control4 authentication tokens expire every 24 hours. This application now features **background auto-renewal**. If a token expires, the system silently catches the error, re-authenticates with the controller, and retries the request. You will never need to manually restart the app to fix "Authentication failed" errors.

###  Mobile & Local Network Access
The server is configured to listen on `0.0.0.0`, allowing you to access the dashboard from your smartphone, tablet, or other PCs on your local Wi-Fi network.
1. Find your PC's local IP address (e.g., `192.168.1.50`).
2. Open Chrome on your phone and navigate to `http://192.168.1.50:65003`.
3. **Pro Tip:** Tap the Chrome menu (three dots) and select **"Add to Home screen"** to install it as a full-screen web app on your phone!

### 🛡️ Smart UI Features
- **Smart Shutdown Button:** To prevent accidental server shutdowns, the ** Shutdown** button is automatically hidden when accessing the dashboard from a mobile device or tablet. It is only visible on the host PC.
- **Mobile Setup Restriction:** The "Enter Setup Mode", "Add Widget", and "Manage Rooms" buttons are completely hidden on mobile devices. This prevents accidental edits and keeps the mobile interface strictly for viewing and controlling.
- **Version Tag:** A small, unobtrusive version tag (e.g., `v260713 | License valid till Jan 01, 2027`) is displayed in the bottom-right corner for easy version tracking.

### 🔒 Security
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
| **"Access Expired"** | The trial period (ending Jan 1, 2027) has ended. Contact the developer for the full version. |
| **"Authentication failed" / Token Expired** | Handled automatically! The app will silently re-authenticate in the background. If it persists, check your `C4_USERNAME`, `C4_PASSWORD`, and `C4_HOST` in `.env`. |
| **"dashboard.html is missing"** | The `.exe` cannot find its internal files. Ensure you downloaded the complete package. |
| **"Port already in use"** | Change `C4_GUI_PORT` in `.env` to a different port (e.g., `65004`). |
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
- **Performance:** For the best mobile experience, keep the number of active Textbox/Combo widgets reasonable to minimize polling load on your Control4 controller.

---

## 💡 Thanks to ->>

Inspired by the brilliant work of #lawtancool and his predecessors. Uses some code from https://github.com/lawtancool/pyControl4. Made by Qwen AI under human supervision.

---

## 📄 License

Free for personal use until the beta period is expired.
