# Shinsekai Tools (新世界) — Companion Dynamic Suite for Omarchy

<p align="center">
  <a href="https://github.com/Madhukumar511/omarchy-shinsekai-theme"><img src="https://img.shields.io/badge/Theme-Shinsekai%20(omarchy--shinsekai--theme)-blue?style=for-the-badge&logo=github" alt="Main Theme"></a>
  <img src="https://img.shields.io/badge/Platform-Omarchy%20%7C%20Hyprland-blue?style=for-the-badge&logo=archlinux" alt="Platform">
  <img src="https://img.shields.io/badge/CLI%20Tool-shin--bg%20Manager-magenta?style=for-the-badge" alt="CLI Tool">
  <img src="https://img.shields.io/badge/Theming-Real--Time%20Dynamic%20Sync-green?style=for-the-badge" alt="Dynamic Theming">
  <img src="https://img.shields.io/badge/License-MIT-orange?style=for-the-badge" alt="License">
</p>

> [!IMPORTANT]
> 🎨 **Theme Companion Suite**: These tools are the companion automation engine for the **[Shinsekai Omarchy Theme](https://github.com/Madhukumar511/omarchy-shinsekai-theme)**.
> If you have not installed the main theme yet, install it first via Omarchy:
> ```bash
> omarchy theme install https://github.com/Madhukumar511/omarchy-shinsekai-theme.git
> # or activate it:
> omarchy theme set shinsekai
> ```

---

## Overview

**Shinsekai Tools** provides the real-time dynamic automation layer for the Shinsekai anime theme on Omarchy Linux:

- **`shinsekai-wallpaper` (`shin` / `shin-bg`)**: Interactive terminal CLI tool to download 4K/8K anime wallpapers, auto-assign indices, detect links from clipboard, switch wallpapers, auto-cycle day/night wallpapers, and restore deleted wallpapers via trash undo.
- **`dynamic-theme.py`**: Hue-clustering color extraction engine that analyzes the active wallpaper and recalculates dominant accents, window borders, SwayOSD popups, Walker launcher styling, browser tints, and terminal colors in real time.
- **`shinsekai-watcher.py`**: Zero-CPU Linux kernel `inotify` background daemon that triggers color recalculation on wallpaper changes.
- **`shinsekai-pulse.py`**: Low-overhead PipeWire audio stream visualizer that pulses and rotates Hyprland border gradients in sync with music/video playback.
- **`shinsekai-daemon.sh`**: Standalone bash automation loop for standalone environments.

---

## Quick Setup (1-Minute Installation)

### 1. Clone the Tools Repository

```bash
git clone https://github.com/Madhukumar511/omarchy-shinsekai-tools.git ~/.local/share/omarchy-shinsekai-tools
```

### 2. Create CLI Symlinks

```bash
mkdir -p ~/.local/bin
ln -nsf ~/.local/share/omarchy-shinsekai-tools/shinsekai-wallpaper ~/.local/bin/shin
ln -nsf ~/.local/share/omarchy-shinsekai-tools/shinsekai-wallpaper ~/.local/bin/shin-bg
ln -nsf ~/.local/share/omarchy-shinsekai-tools/shinsekai-wallpaper ~/.local/bin/shinsekai
```

### 3. Enable Background Color Sync Daemon (Systemd)

```bash
mkdir -p ~/.config/systemd/user
cat << 'EOF' > ~/.config/systemd/user/shinsekai-dynamic.service
[Unit]
Description=Shinsekai Theme Dynamic Wallpaper Color Sync
After=graphical-session.target

[Service]
Type=simple
ExecStart=/usr/bin/python3 %h/.local/share/omarchy-shinsekai-tools/shinsekai-watcher.py
Restart=always
RestartSec=1

[Install]
WantedBy=default.target
EOF

systemctl --user daemon-reload
systemctl --user enable --now shinsekai-dynamic.service
```

---

## Wallpaper Manager CLI (`shin` / `shin-bg`)

Shinsekai includes a fast terminal CLI tool `shin` (or `shin-bg`) to manage, download, toggle effects, and inspect wallpapers from any directory.

### Commands Reference

| Command | Action | Example |
| :--- | :--- | :--- |
| `shin` (or `shin-bg`) | Open interactive manager with clipboard link detector | `shin` |
| `shin list` | View all installed wallpapers with assigned numbers `[01-N]` | `shin list` |
| `shin set <number>` | Switch active wallpaper by number (auto-pauses cycling) | `shin set 4` |
| `shin next` | Cycle to next wallpaper | `shin next` |
| `shin current` | Show currently active wallpaper filename & resolution | `shin current` |
| `shin add <url-or-path> [name]` | Download 4K/8K wallpaper & auto-assign next number | `shin add <link> solo-leveling` |
| `shin rename <num> <name>` | Rename wallpaper while preserving index order | `shin rename 13 lord-of-mysteries` |
| `shin auto [on\|off\|status]` | Toggle Day/Night time-of-day auto wallpaper transitions | `shin auto on` |
| `shin pulse [on\|off\|status]` | Toggle music-reactive audio glowing window borders | `shin pulse on` |
| `shin lock [on\|off\|status]` | Toggle dynamic lockscreen blur & accent border sync | `shin lock off` |
| `shin remove <number>` | Safely move wallpaper to recovery trash | `shin remove 13` |
| `shin restore [number]` | Undo / Restore deleted wallpaper | `shin undo` or `shin restore 13` |
| `shin trash` | View deleted wallpapers in recovery trash | `shin trash` |

---

## Key Features

### 1. Trash Recovery & Undo System
Accidentally deleted a wallpaper?
- Removed wallpapers are moved to `.trash/` instead of being permanently erased.
- Run **`shin undo`** to immediately restore the last deleted wallpaper.
- Or run **`shin restore <number>`** to recover a specific wallpaper number.

### 2. Music-Reactive Audio Border Pulse
- **PipeWire Native Stream Tracking**: Detects audio from YouTube, Spotify, VLC, browser tabs, or media players with zero lag.
- **Dynamic Gradient Rotation**: Window borders gently pulse and rotate their dual-tone anime gradient in sync with playing audio.
- **Zero-CPU Idle Sleep**: Immediately halts when music/video stops, using **0.00% CPU** during silence.
- Toggle with `shin pulse on` or `shin pulse off`.

### 3. Day & Night Time-of-Day Auto-Cycling
Automatically transitions between anime atmospheres according to your local time:
- **Day (07:00 – 17:00)**: Sunlit meadows, blue flower fields, open skies.
- **Sunset (17:00 – 20:00)**: Golden hour horizons, lake sunsets, twilight vistas.
- **Night (20:00 – 07:00)**: Celestial skies, neon cityscapes, starry doors, moonlit skylines.
- Toggle with `shin auto on` or `shin auto off`.
> **Smart Pause:** Selecting any wallpaper manually via `shin set <number>` automatically pauses auto-cycling so your custom choice is never overwritten.

### 4. Dynamic Lock Screen Engine
- **Frosted Acrylic Background**: Live multi-pass Gaussian blur rendered over your current wallpaper.
- **Dynamic Glow Border**: Password entry box pulses in the dominant accent color extracted from your current wallpaper.
- Toggle with `shin lock on` or `shin lock off`.

---

## Connected Repositories

- **Theme Repository**: [Madhukumar511/omarchy-shinsekai-theme](https://github.com/Madhukumar511/omarchy-shinsekai-theme)
- **Tools Repository**: [Madhukumar511/omarchy-shinsekai-tools](https://github.com/Madhukumar511/omarchy-shinsekai-tools)

## License

Released under the **MIT License**.
