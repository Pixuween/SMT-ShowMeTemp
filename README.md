# SMT-ShowMeTemp
Most monitoring tools are either too heavy (MSI Afterburner, HWiNFO) or too simple. ShowMeTemp sits in the middle — lightweight, always-on, no window cluttering your desktop. Two icons in your tray. One for CPU, one for GPU. That's it.

Features
Live temperature display
Color-coded icons update every 1.5s — white when cool, yellow when warm, red when hot.
Smart alerts
Sound + Windows toast notifications when temps spike, with component-specific advice. Built-in cooldown prevents notification spam.
Hover tooltip
Hover over any icon to see exact temperature + CPU/GPU usage %.
Right-click menu

Current temperature (live)
60-point history graph with threshold lines
Settings — customize warn/critical thresholds, cooldown, refresh rate
Mute alerts — 30 min / 1 hour / until restart
Quit one or quit all

Persistent config
All settings saved to %APPDATA%\ShowMeTemp\config.json.
Auto-language detection
Detects your Windows language automatically.
Supported: 🇫🇷 FR · 🇬🇧 EN · 🇪🇸 ES · 🇩🇪 DE · 🇮🇹 IT · 🇵🇹 PT
Resilient
Auto-resurrects if the tray icon disappears. Single-instance protection. Crash log on Desktop.

Screenshots

Tray icons update in real time. White = normal, yellow = warm (≥65°C), red = critical (≥82°C).


Installation
Option A — Installer (recommended)
1. Run installer.bat as Administrator
2. Accept the UAC prompt for LibreHardwareMonitor
3. Go to Settings > Taskbar > Other system tray icons
4. Enable "Python"

The installer handles Python dependencies, downloads LibreHardwareMonitor to C:\LHM\, sets up autostart, and copies the script to AppData so you can delete the source folder.

Option B — Run directly
bashpip install pillow pystray psutil wmi pywin32
python ShowMeTemp.py

Requires LibreHardwareMonitor running in background for accurate readings.

Option C — Standalone EXE
Build a single .exe with no Python dependency:
bash# On Windows, run:
build.bat
# Output: dist\ShowMeTemp.exe

Requirements
DependencyPurposepillowIcon renderingpystraySystem traypsutilCPU usage %wmi + pywin32LHM sensor accessGPUtilGPU fallbackLibreHardwareMonitorHardware sensor data

How it works
ShowMeTemp reads hardware sensors through LibreHardwareMonitor's WMI interface (root\LibreHardwareMonitor), which provides accurate temps for both AMD and Intel CPUs, and all major GPUs.
Each tray icon runs in its own thread. Sensor reads are decoupled from the pystray message loop to prevent the icon from freezing or disappearing. WMI connections are cached per-thread to avoid COM object leaks.
main()
 ├── CPU_tray thread  ──► pystray message loop
 │    └── CPU_sensors thread  ──► WMI reads every 1.5s
 └── GPU_tray thread  ──► pystray message loop
      └── GPU_sensors thread  ──► WMI reads every 1.5s

Configuration
Settings are stored in %APPDATA%\ShowMeTemp\config.json:
json{
  "warn_temp": 65,
  "crit_temp": 82,
  "alert_cooldown": 60,
  "refresh_s": 1.5,
  "show_usage": true
}
Edit via right-click → Settings, or directly in the JSON.

Uninstall
Run uninstaller.bat
Removes autostart entry, LHM (optional), and all AppData files.

Troubleshooting
Icons not showing
→ Windows Settings > Personalization > Taskbar > Other system tray icons > enable Python
Temperature shows --
→ Make sure LibreHardwareMonitor is running (tray icon visible). Try launching it as Administrator.
Crash on startup
→ Check ShowMeTemp.log on your Desktop for the full traceback.

Stack
Python · pystray · Pillow · LibreHardwareMonitor (WMI) · tkinter · PyInstaller

Changelog
v21032026.1

Mute alerts mode (30min / 1h / session)
Quit all from either tray menu
Live temperature in right-click menu
Auto-resurrect if tray icon disappears
Multi-language support (FR/EN/ES/DE/IT/PT)
Usage % in hover tooltip
Persistent JSON config
WMI connection cache — fixes crash after extended use
Single-instance protection
Fix: source folder unlocked after install
Fix: Settings window crash
Fix: duplicate sensor log entries


<div align="center">
Made with ❤️ by Rebeu_Deep
</div>
