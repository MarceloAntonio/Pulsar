# Pulsar - WiFi & Bluetooth Manager for Wayland

A native network manager for Wayland using Rust, GTK4, and layer-shell with a high-contrast glassmorphism UI. Manage WiFi, Bluetooth devices, and wired Ethernet connections from a unified, animated panel.

## Interface Preview

<p align="center">
  <img src="screenshots/example.gif" width="300" alt="Pulsar Preview">
</p>

*The configuration shown in this GIF is available at: [MarceloAntonio/Dotfiles](https://github.com/MarceloAntonio/Dotfiles/tree/main/.config/pulsar)*

## Documentation
- [Styling & Theming Guide](docs/STYLING.md) - Learn how to customize CSS, colors, and layout.
- [Contributing Guidelines](CONTRIBUTING.md) - Learn how to help the project and submit code.

## Features

- **WiFi Management**: Smart search, WPA2/WPA3 support, hidden networks, and saved profiles.
- **Ethernet Management**: List wired connections, connect/disconnect easily.
- **Bluetooth Management**: Device details, battery alerts, pairing agent, and signal strength.
- **Modern UI/UX**: High-contrast glassmorphism, smooth animations, and dynamic positioning.
- **Hot-Reloading**: Change styles and configurations on the fly without restarting.

## Installation

### 1. Arch Linux (Pre-compiled Binary via PKGBUILD)
To download the optimized, pre-compiled binary from this repository without compiling Rust locally:
```bash
git clone https://github.com/MarceloAntonio/wifi-bar.git
cd wifi-bar
makepkg -si
```

### 2. Build From Source
First, install the required dependencies:
- **Arch Linux:** `sudo pacman -S base-devel rustup git gtk4 gtk4-layer-shell pkgconf`
- **Ubuntu/Debian:** `sudo apt install build-essential cargo git libgtk-4-dev libgtk4-layer-shell-dev pkg-config`

Then clone and build the project:
```bash
git clone https://github.com/MarceloAntonio/wifi-bar.git
cd wifi-bar
cargo build --release
sudo install -Dm755 target/release/pulsar /usr/bin/pulsar
```

## Running and Activating (Daemon)

Pulsar consists of a background **daemon** (which handles connections, states, and DBus) and a **frontend** (which you trigger to show/hide).

### 1. Starting the Daemon Automatically
To ensure Pulsar is always running in the background and responds instantly, add it to your Wayland compositor's autostart.

**For Hyprland** (in `~/.config/hypr/hyprland.conf`):
```conf
exec-once = pulsar daemon
```

**For Sway** (in `~/.config/sway/config`):
```conf
exec pulsar daemon
```

### 2. Controlling the Interface
Once the daemon is running, you can show, hide, or toggle specific tabs using the CLI (often bound to Waybar or hotkeys):

```bash
# Toggle the main window
pulsar toggle

# Open specifically the WiFi tab
pulsar toggle --tab wifi

# Open specifically the Bluetooth tab
pulsar toggle --tab bluetooth

# Output JSON status for Waybar modules
pulsar waybar-status
```

## Waybar Integration

Pulsar is designed to look native in your bar. Add the following module to your Waybar `config.jsonc`:

```jsonc
"custom/pulsar": {
    "exec": "pulsar waybar-status",
    "return-type": "json",
    "interval": 10,
    "on-click": "pulsar toggle --tab wifi",
    "format": "O"
}
```

## License
MIT License - see [LICENSE](LICENSE) for details.
