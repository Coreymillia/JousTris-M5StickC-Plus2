# 🎮 JousTris

**Classic Joust Meets Tetris on M5StickC Plus2!**

Fly on S and Z tetromino pieces as birds in this arcade-style aerial combat game. Battle enemies, collect eggs before they hatch, and survive endless waves of increasing difficulty!

![Version](https://img.shields.io/badge/version-1.0-blue)
![Platform](https://img.shields.io/badge/platform-M5StickC%20Plus2-orange)
![License](https://img.shields.io/badge/license-MIT-green)

---

## 📋 Table of Contents
- [Features](#-features)
- [Hardware Requirements](#-hardware-requirements)
- [Quick Start](#-quick-start)
- [Controls](#-controls)
- [Gameplay](#-gameplay)
- [Building from Source](#-building-from-source)
- [Game Mechanics](#-game-mechanics)
- [Version History](#-version-history)
- [Credits](#-credits)

---

## ✨ Features

### Core Gameplay
- 🐦 **Classic Joust Physics** - Gravity-based flight with flap mechanics
- 🎨 **Tetromino Birds** - S and Z pieces that flip based on direction
- ⚔️ **Height-Based Combat** - Higher position wins collisions
- 🥚 **Egg System** - Defeated enemies drop eggs that hatch if not collected
- 🦖 **Pterodactyl Hazard** - Anti-camping punishment for stalling
- 🔥 **Lava Bottom** - Deadly hazard at screen bottom
- 🌀 **Screen Wrapping** - Seamless left/right edge wrapping

### Advanced Systems
- 🧠 **Smart AI** - Limited hunters (1-3) actively chase you, others wander
- 🏔️ **Procedural Platforms** - Fresh layout every wave
- 📈 **Endless Progression** - Difficulty scales infinitely
- 💾 **Safe Respawn** - Smart spawn checking with invulnerability
- 🎯 **God Mode** - Invincible testing/practice mode
- 🚀 **Auto-Flap** - Continuous flapping accessibility option

---

## 🛠️ Hardware Requirements

### Required
- **M5StickC Plus2** (ESP32-based handheld)
- **Mini JoyC Hat** (Analog joystick addon)
- USB-C cable for programming

### Optional
- M5Burner (for easy flashing without IDE)

---

## 🚀 Quick Start

### Option 1: M5Burner (Easiest)
1. Download [M5Burner](https://docs.m5stack.com/en/download)
2. Download `JousTrisM5_FINAL_MERGED.bin` from [Releases](../../releases)
3. Connect M5StickC Plus2 via USB
4. Open M5Burner, select Custom, load the `.bin` file
5. Click "Burn"
6. Play!

### Option 2: PlatformIO Upload
1. Download `JousTrisM5_FINAL.bin` from [Releases](../../releases)
2. Use esptool or PlatformIO to flash:
```bash
pio run --target upload
```

### Option 3: Build from Source
See [Building from Source](#-building-from-source) below

---

## 🕹️ Controls

### JoyC Mini Hat
- **Joystick Left/Right** - Fly horizontally
- **JoyC Button** - Flap wings (tap or hold)

### M5StickC Plus2 Buttons
- **Button A (Side)** - Toggle Auto-Flap mode
- **Button B (Front)** - Toggle God Mode

### Control Modes
- **Normal Mode** - Tap button to flap (classic arcade)
- **Auto-Flap Mode** - Hold button for continuous flapping (4 flaps/sec)
- **God Mode** - Invincible, instant kills from any angle

---

## 🎮 Gameplay

### Objective
Survive endless waves by defeating enemy birds and collecting eggs before they hatch into stronger enemies.

### Combat Rules
- **Higher Y position wins** - Attack from above!
- **Same height** - Bounce apart
- **Lower position** - You lose a life
- **God Mode** - Win from any angle

### Enemies
- **Hunters** (1-3 per wave) - Actively chase you
- **Wanderers** - Patrol randomly across the board
- **Pterodactyls** - Spawn if you stall, must hit head to kill

### Scoring
- Defeat enemy: **50 points**
- Collect egg: **+points**
- Defeat pterodactyl: **100 points**

### Wave Progression

| Wave | Enemies | Hunters | AI Speed | Egg Hatch | Pterodactyl Timer |
|------|---------|---------|----------|-----------|-------------------|
| 1-2  | 4       | 1       | 1.0x     | 6 sec     | 30 sec            |
| 3-8  | 5-7     | 2       | 1.4-2.0x | 4-3 sec   | 27-22 sec         |
| 9+   | 8       | 3       | 2.2x+    | 2 sec     | 20-15 sec         |

---

## 🔨 Building from Source

### Prerequisites
- [PlatformIO](https://platformio.org/) (CLI or VSCode extension)
- Git

### Clone & Build
```bash
# Clone repository
git clone https://github.com/YOUR_USERNAME/JousTris.git
cd JousTris

# Build
pio run

# Upload to device
pio run --target upload

# Monitor serial output (optional)
pio device monitor
```

### Project Structure
```
JousTris/
├── src/
│   ├── main.cpp              # Main game code
│   ├── UNIT_MiniJoyC.cpp     # JoyC controller driver
│   └── UNIT_MiniJoyC.h
├── include/                   # Header files (if any)
├── platformio.ini            # PlatformIO configuration
└── README.md                 # This file
```

### Dependencies (Auto-installed)
- `M5StickCPlus2` (v1.0.2+)
- `M5Unified` (v0.2.10+)
- `M5GFX`

---

## 🎯 Game Mechanics

### Physics
```cpp
Gravity: 0.3 pixels/frame
Flap Power: -4.5 pixels
Max Vertical Velocity: ±8.0 pixels
Horizontal Speed: 2.0 pixels
```

### Enemy AI States
1. **Wander** - Random horizontal movement
2. **Chase** - Pursue player horizontally, try to get above
3. **Flee** - Move away from player

### Hunter Assignment
- Wave 1-2: **1 hunter**, rest wander
- Wave 3-8: **2 hunters**, rest wander  
- Wave 9+: **3 hunters** (max), rest wander
- Dead hunters are replaced automatically

### Egg Mechanics
- Drop when enemy defeated
- Fall with gravity, land on platforms
- **Hatch timer**: 6s (Wave 1) → 2s (Wave 10+)
- Flash red in last 1.5 seconds
- Hatch into stronger enemies if not collected

### Pterodactyl
- **Spawn Trigger**: 
  - Wave takes >30s (decreases to 15s by Wave 15)
  - Player idle with eggs >15s (decreases to 8s)
- **Behavior**: Homes in on player position
- **Speed**: 3.0 → 5.0 (increases with wave)
- **Kill Method**: Must hit tiny red head hitbox (precision)
- **God Mode**: Instant kill from any angle

### Respawn System
- **Death**: 0.8 second delay
- **Spawn Check**: Finds safe location away from enemies/eggs
- **Invulnerability**: 2 seconds (flashing sprite)
- **Lives**: Start with 3, game over at 0

### Boundaries
- **Top (y=10)**: Bounce down (velocity +2.0-2.5)
- **Bottom (y=230)**: Lava death (except god mode)
- **Left/Right**: Wrap to opposite side

---

## 📜 Version History

### v1.0 - FINAL (Current)
- ✅ Limited hunter system (1-3 hunters max per wave)
- ✅ Wanderer enemies for board coverage
- ✅ Dynamic hunter reassignment
- ✅ Procedural platform generation
- ✅ Enhanced wave progression
- ✅ Ceiling bounce mechanic
- ✅ True god mode (instant kills)
- ✅ Fixed auto-flap persistence

### Development Versions
- v1.6 - God Mode
- v1.5 - Enhanced Waves (COMPLETE2)
- v1.4 - Safe Respawn (COMPLETE)
- v1.3 - Pterodactyl & Eggs
- v1.2 - Working Waves
- v1.1 - Directional Birds
- v1.0 - Starting Point

---

## 🎨 Customization

Want to tweak the game? Edit these constants in `src/main.cpp`:

```cpp
// Physics
#define GRAVITY 0.3
#define FLAP_POWER 4.5
#define HORIZONTAL_SPEED 2.0

// Game balance
#define MAX_ENEMIES 8
#define MAX_EGGS 6

// Colors (RGB565)
#define COLOR_S 0x07E0      // Player color (green)
#define COLOR_Z 0xF800      // Enemy color (red)
#define COLOR_EGG 0xFFE0    // Egg color (yellow)
```

---

## 🐛 Known Issues

None currently! Report issues on [GitHub Issues](../../issues)

---

## 📝 License

MIT License - Feel free to modify and share!

---

## 👏 Credits

**Game Design & Development**: Corey Millia  
**Inspired by**: Joust (Williams Electronics, 1982)  
**Platform**: M5Stack M5StickC Plus2  
**Framework**: Arduino/ESP32 + PlatformIO

---

## 🤝 Contributing

Pull requests welcome! Please:
1. Fork the repository
2. Create a feature branch
3. Test thoroughly on hardware
4. Submit PR with description

---

## 📞 Support

- **Issues**: [GitHub Issues](../../issues)
- **Discussions**: [GitHub Discussions](../../discussions)
- **Hardware**: [M5Stack Store](https://shop.m5stack.com/)

---

## 🌟 Acknowledgments

- M5Stack community for excellent hardware
- PlatformIO for seamless embedded development
- Williams Electronics for the original Joust

---

**Made with ❤️ for retro arcade fans**

*Play responsibly. Watch for pterodactyls.* 🦖
