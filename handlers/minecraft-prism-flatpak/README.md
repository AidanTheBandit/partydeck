# Minecraft Handler for Prism Launcher (Flatpak)

This handler allows you to run multiple instances of Minecraft Java Edition using Prism Launcher installed via Flatpak for split-screen multiplayer.

## Why Use Flatpak?

Flatpak provides:
- Universal compatibility across Linux distributions
- Sandboxed application environment
- Easy installation and updates
- Consistent runtime environment

## Prerequisites

1. **Flatpak** - Package manager for installing applications
2. **Prism Launcher (Flatpak)** - Minecraft launcher
3. **Minecraft Java Edition** - Set up through Prism Launcher

## Setup Instructions

### 1. Install Flatpak

If you don't have Flatpak installed:

```bash
# Ubuntu/Debian
sudo apt install flatpak

# Fedora
sudo dnf install flatpak

# Arch Linux
sudo pacman -S flatpak

# Add the Flathub repository
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```

### 2. Install Prism Launcher via Flatpak

```bash
flatpak install flathub org.prismlauncher.PrismLauncher
```

### 3. Set Up Minecraft

1. Launch Prism Launcher:
   ```bash
   flatpak run org.prismlauncher.PrismLauncher
   ```
2. Create a new instance with your desired Minecraft version
3. Note the instance name (you'll need this for the handler)
4. Configure any mods, resource packs, or shaders as needed
5. Test that the instance launches successfully

### 4. Configure the PartyDeck Handler

1. Copy `handler.json.template` to `handler.json`
2. Import the handler into PartyDeck
3. The key settings are:
   - **exec**: `org.prismlauncher.PrismLauncher` (the Flatpak app ID)
   - **is_flatpak**: `true` (IMPORTANT!)
   - **args**: `-l <your-instance-name>` (replace with your instance name)

   Example configuration:
   ```json
   {
     "exec": "org.prismlauncher.PrismLauncher",
     "args": "-l Vanilla1.20",
     "is_flatpak": true
   }
   ```

## Per-Player Configuration

For separate worlds/saves per player, you have two options:

### Option 1: Multiple Minecraft Instances (Recommended)

1. Create separate instances in Prism Launcher for each player:
   - Player 1: "Vanilla1.20-P1"
   - Player 2: "Vanilla1.20-P2"
   - Player 3: "Vanilla1.20-P3"
   - etc.

2. Configure each instance with different settings if desired

3. Create multiple handlers or use PartyDeck's profile system

### Option 2: PartyDeck Profile System

Use PartyDeck's built-in profile system to separate save data while using the same Minecraft instance.

## Launch Options

Common Prism Launcher arguments:

- `-l <instance>` - Launch specific instance
- `-s <server>` - Connect to server on launch
- `--alive` - Keep launcher window open (not recommended for split-screen)

Example args for different use cases:

**Basic local play:**
```
-l MyMinecraft
```

**Connect to server on launch:**
```
-l MyMinecraft -s play.example.com
```

## Multiplayer Setup

### LAN Games

1. Launch PartyDeck with this handler and 2+ instances
2. In one instance, open to LAN (ESC → Open to LAN)
3. Other players can join via the multiplayer menu
4. Ensure port 25565 or the LAN port is accessible in your firewall

### Online Servers

Configure the handler args to connect directly:
```
-l <instance-name> -s <server-address>
```

## Troubleshooting

### Instances won't launch
- Verify Prism Launcher is installed: `flatpak list | grep PrismLauncher`
- Check that the instance name matches exactly (case-sensitive)
- Ensure `is_flatpak` is set to `true` in the handler

### Can't connect to LAN
- Check firewall settings for port 25565
- Try manually specifying the LAN game's IP address

### Performance issues
- Lower render distance in Minecraft settings
- Disable shaders or use lightweight shader packs
- Use performance mods like Sodium, Lithium, or Optifine
- Consider using Minecraft 1.12.2 or earlier for better multi-instance performance

### Flatpak permissions
If you encounter file access issues:
```bash
# Grant Prism Launcher access to your home directory
flatpak override org.prismlauncher.PrismLauncher --filesystem=home
```

## Technical Details

When `is_flatpak` is set to `true`, PartyDeck will:
- Use `flatpak run <app-id>` instead of executing the binary directly
- Skip game directory mounting (Flatpak handles sandboxing)
- Use the home directory as the working directory
- Pass the arguments directly to the Flatpak application

## Notes

- This is an experimental feature for split-screen Minecraft multiplayer
- Performance may vary depending on your system and Minecraft settings
- For best results, use vanilla Minecraft or lightweight mod packs
- Each instance will consume system resources - plan accordingly
- The Flatpak sandbox provides additional isolation between instances

## Finding Other Flatpak App IDs

To use this approach with other Flatpak applications:

1. List installed Flatpak apps:
   ```bash
   flatpak list --app
   ```

2. Find the Application ID (usually in reverse-DNS format like `org.example.AppName`)

3. Use that ID in the `exec` field and set `is_flatpak` to `true`

## Examples of Other Flatpak Launchers

This same approach can work with other Flatpak-based launchers:

- **MultiMC**: `org.multimc.MultiMC`
- **ATLauncher**: `com.atlauncher.ATLauncher`
- **Heroic Games Launcher**: `com.heroicgameslauncher.hgl`
- **Lutris**: `net.lutris.Lutris`

Just replace the `exec` field with the appropriate Flatpak app ID.
