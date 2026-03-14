# ShowMeTemp

**Real-time CPU & GPU temperature monitor — system tray, always on, zero bloat.**

![Version](https://img.shields.io/badge/version-21032026.1-black?style=flat-square)
![Platform](https://img.shields.io/badge/platform-Windows%2010%2F11-blue?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)
![Status](https://img.shields.io/badge/status-release-brightgreen?style=flat-square)

</div>

---


Screenshots
https://ibb.co/hJ69S64Y
https://ibb.co/RkgJRP6r
https://ibb.co/B5TBccJK

---

## Installation

Download `ShowMeTemp_Setup_21032026.1.exe` and run it.

The installer handles everything:
- Installs ShowMeTemp
- Bundles and configures LibreHardwareMonitor
- Creates a Start Menu shortcut
- Sets up autostart at Windows boot

**No Python. No manual setup. No dependencies.**

> Windows 10 / 11 only.

---

## First launch

After installation, two icons appear in your system tray — one for CPU, one for GPU.

If you don't see them, go to:
```
Settings > Personalization > Taskbar > Other system tray icons > enable Python
```

---

## Usage

| Action | Result |
|---|---|
| Glance at tray | Live temperature, color-coded |
| Hover over icon | Exact temp + usage % |
| Right-click | Full menu |

**Color codes**

| Color | Meaning |
|---|---|
| White | Normal |
| Yellow | Warm (≥ 65°C) |
| Red | Critical (≥ 82°C) |

**Right-click menu**

- Current temperature (live)
- History — 60-point graph for that component
- Settings — adjust thresholds, cooldown, refresh rate
- Mute alerts — 30 min / 1 hour / until restart
- Quit / Quit all

---

## Settings

Access via right-click → Settings.

| Option | Default | Description |
|---|---|---|
| Warning threshold | 65°C | Icon turns yellow above this |
| Critical threshold | 82°C | Icon turns red, alert fires |
| Alert cooldown | 60s | Minimum time between alerts |
| Refresh rate | 1.5s | How often temps are read |
| Show usage % | On | CPU/GPU load in tooltip |

Settings are saved automatically to `%APPDATA%\ShowMeTemp\config.json`.

---

## Troubleshooting

**Icons not visible in tray**
Go to Settings → Personalization → Taskbar → Other system tray icons → enable **Python**

**Temperature shows `--`**
LibreHardwareMonitor needs to be running. It should start automatically — if not, launch it manually from `C:\LHM\LibreHardwareMonitor.exe` and accept the UAC prompt.

**App crashed**
Check `ShowMeTemp.log` on your Desktop for the full error log.

**Already running message on launch**
Another instance is already active. Check your system tray — the icons may be hidden.

---

## Uninstall

Go to **Settings → Apps → ShowMeTemp → Uninstall**.

Removes the app, autostart entry, and AppData config. LibreHardwareMonitor in `C:\LHM\` is left in place in case other apps use it — delete it manually if needed.

---

## Languages

Detected automatically from your Windows language setting.

🇫🇷 French &nbsp;·&nbsp; 🇬🇧 English &nbsp;·&nbsp; 🇪🇸 Spanish &nbsp;·&nbsp; 🇩🇪 German &nbsp;·&nbsp; 🇮🇹 Italian &nbsp;·&nbsp; 🇵🇹 Portuguese

---

## For developers — build from source

```
Requirements : Python 3.8+, Inno Setup 6
```

```bash
# Clone the repo, then:
build.bat
```

The build script will:
1. Install Python dependencies
2. Download LibreHardwareMonitor
3. Compile `ShowMeTemp.exe` with PyInstaller
4. Package everything into `installer\ShowMeTemp_Setup_21032026.1.exe`

---

## Stack

`Python` &nbsp;·&nbsp; `pystray` &nbsp;·&nbsp; `Pillow` &nbsp;·&nbsp; `LibreHardwareMonitor` &nbsp;·&nbsp; `tkinter` &nbsp;·&nbsp; `PyInstaller` &nbsp;·&nbsp; `Inno Setup`

---

## Changelog

### v21032026.1 — first public release
- Plug & play installer (LHM bundled)
- Multi-language support — FR / EN / ES / DE / IT / PT
- Mute alerts mode — 30min / 1h / session
- Quit all from either tray icon
- Live temperature in right-click menu
- 60-point history graph with threshold lines
- Auto-resurrect if tray icon disappears
- Single-instance protection
- WMI connection cache — fixes crash on extended use
- Persistent JSON config in AppData
- AppUserModelID — proper taskbar icon

---

<div align="center">

Made with ❤️ by **Rebeu_Deep**

</div>
