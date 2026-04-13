# 🍅 Cross-Distro Pomodoro Timer for Waybar

A portable, cross-distro Pomodoro timer that integrates with [Waybar](https://github.com/Alexays/Waybar) and [Hyprland](https://hyprland.org/).

Works on **any Linux distro** with just `bash`, `coreutils`, and `notify-send`.

## Features

- ⏱️ 25-minute work sessions
- ☕ 5-minute breaks
- 🌴 15-minute long breaks (after 4 sessions)
- 🔔 Desktop notifications for phase transitions
- 🎨 Color-coded states in Waybar
- ⏯️ Start/Pause/Resume/Reset functionality
- ⌨️ Keyboard shortcuts (Hyprland)

## Installation

### 1. Copy the Script

```bash
mkdir -p ~/.config/hypr/scripts
cp pomodoro.sh ~/.config/hypr/scripts/pomodoro.sh
chmod +x ~/.config/hypr/scripts/pomodoro.sh
```

### 2. Add Waybar Module

Add the module definition to your Waybar config or included file:

```json
"custom/pomodoro": {
    "format": "{}",
    "return-type": "json",
    "interval": 1,
    "exec": "$HOME/.config/hypr/scripts/pomodoro.sh status",
    "on-click": "$HOME/.config/hypr/scripts/pomodoro.sh toggle",
    "on-click-right": "$HOME/.config/hypr/scripts/pomodoro.sh reset",
    "on-click-middle": "$HOME/.config/hypr/scripts/pomodoro.sh start",
    "tooltip": true
}
```

Then add `"custom/pomodoro"` to your `modules-left`, `modules-center`, or `modules-right`.

### 3. Add CSS Styling

Add the styles from `waybar/style.css` to your Waybar theme file.

### 4. Add Keybindings (Hyprland)

Source the keybindings file in your `hyprland.conf`:

```ini
source = ~/.config/hypr/UserConfigs/pomodoro-keybinds.conf
```

Or copy the bindings from `hyprland/keybindings.conf` directly.

### 5. Restart Waybar

```bash
pkill waybar && waybar &
```

## Usage

### Waybar Interaction

| Action | Result |
|--------|--------|
| Left-click | Toggle (Start/Pause) |
| Right-click | Reset |
| Middle-click | Force Start |

### Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `SUPER + ALT + P` | Toggle (Start/Pause) |
| `SUPER + ALT + R` | Reset |

### CLI Commands

```bash
pomodoro.sh start     # Start/resume timer
pomodoro.sh pause     # Pause timer
pomodoro.sh toggle    # Toggle start/pause
pomodoro.sh reset     # Reset timer
pomodoro.sh status    # Output Waybar JSON format
```

## Configuration

Override default durations via environment variables:

```bash
export POMO_WORK=1800      # 30 min work
export POMO_BREAK=600      # 10 min break
export POMO_LONG_BREAK=1200 # 20 min long break
export POMO_SESSIONS=3     # Long break after 3 sessions
```

## Color Coding

| State | Color | Meaning |
|-------|-------|---------|
| 🍅 Idle | Default | Ready to start |
| 🔴 Work | Red | Focus session active |
| 🟢 Break | Green | Short break |
| 🔵 Long Break | Blue | Extended break |
| 🟡 Paused | Yellow | Timer paused |

## License

MIT
