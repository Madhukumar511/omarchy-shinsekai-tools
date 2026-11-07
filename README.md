# Shinsekai Tools (新世界)

Companion dynamic theming daemon, wallpaper manager CLI, and color sync tools for the **[Shinsekai Omarchy Theme](https://github.com/Madhukumar511/omarchy-shinsekai-theme)**.

## Included Tools

- **`shinsekai-wallpaper` (`shin-bg` / `shin`)**: Interactive CLI tool for downloading 4K wallpapers, quality analysis, clipboard detection, wallpaper switching, and undo/trash recovery.
- **`dynamic-theme.py`**: Hue-clustered dynamic color extractor that adapts Omarchy system palettes to match wallpaper colors in real-time.
- **`shinsekai-watcher.py`**: Zero-CPU Linux kernel `inotify` background daemon that triggers color recalculation on wallpaper changes.
- **`shinsekai-pulse.py`**: PipeWire audio stream visualizer for reactive Hyprland border animations.
- **`shinsekai-daemon.sh`**: Standalone bash automation loop.

## Installation

```bash
git clone https://github.com/Madhukumar511/omarchy-shinsekai-tools.git ~/.local/share/omarchy-shinsekai-tools
ln -nsf ~/.local/share/omarchy-shinsekai-tools/shinsekai-wallpaper ~/.local/bin/shin-bg
ln -nsf ~/.local/share/omarchy-shinsekai-tools/shinsekai-wallpaper ~/.local/bin/shin
```

## License

MIT
