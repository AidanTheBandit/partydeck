# Minecraft Handler for Prism Launcher

This handler allows you to run multiple instances of Minecraft Java Edition using Prism Launcher for split-screen multiplayer.

## Prerequisites

1. **Prism Launcher** - Install from your distribution's package manager or from [prismlauncher.org](https://prismlauncher.org/)
2. **Minecraft Java Edition** - Set up through Prism Launcher with your desired version and mods

## Setup Instructions

### 1. Install Prism Launcher

```bash
# Example for Ubuntu/Debian
sudo apt install prismlauncher

# Example for Arch Linux
sudo pacman -S prismlauncher

# Or download from https://prismlauncher.org/
```

### 2. Create a Minecraft Instance

1. Open Prism Launcher
2. Create a new instance with your desired Minecraft version
3. Note the instance name (you'll need this later)
4. Configure any mods or resource packs as needed

### 3. Configure the Handler

1. Copy `handler.json.template` to `handler.json`
2. Import the handler into PartyDeck or edit it directly
3. Set the following fields:
   - **path_gameroot**: Leave empty or set to Prism Launcher's installation directory
   - **exec**: `prismlauncher` (or full path if not in PATH)
   - **args**: `-l <your-instance-name>` (replace with your instance name)
   
   Example: If your instance is named "Vanilla1.20", use `-l Vanilla1.20`

### 4. Optional: Per-Player Configuration

For separate worlds/saves per player, you can:

1. Create multiple Minecraft instances in Prism Launcher (e.g., "Vanilla1.20-P1", "Vanilla1.20-P2", etc.)
2. Use the handler with different args for each player
3. Or use PartyDeck's profile system to separate save data

## Launch Options

Common Prism Launcher arguments you can use:

- `-l <instance>` - Launch specific instance
- `-s <server>` - Connect to server on launch
- `--alive` - Keep launcher window open

Example args for LAN play:
```
-l MyMinecraft --alive
```

## Multiplayer Setup

### For LAN Games

1. Launch PartyDeck with this handler and 2+ instances
2. In one instance, open to LAN (ESC → Open to LAN)
3. Other players can join via the multiplayer menu
4. Make sure port 25565 or the LAN port is accessible

### For Online Servers

Set args to:
```
-l <instance-name> -s <server-address>
```

## Troubleshooting

- **Instances won't launch**: Make sure Prism Launcher is installed and the instance name is correct
- **Can't connect to LAN**: Check firewall settings for port 25565
- **Performance issues**: Lower render distance, disable shaders, or use Optifine/Sodium for better performance
- **Different worlds per player**: Create separate instances in Prism Launcher or use PartyDeck profiles

## Notes

- This is an experimental feature for 8-window multiplayer support
- Performance may vary depending on your system and Minecraft settings
- For best results, use lightweight mod packs or vanilla Minecraft
- Consider using performance mods like Sodium, Lithium, or Optifine
