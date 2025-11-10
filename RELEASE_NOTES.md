# JousTris v1.0 - Release Notes

**Release Date**: November 10, 2024  
**Version**: 1.0 FINAL  
**Platform**: M5StickC Plus2 with Mini JoyC Hat

---

## 🎉 What's New in v1.0

### Major Features
- ✅ **Smart Hunter System** - Only 1-3 enemies hunt you, others wander naturally
- ✅ **Procedural Platforms** - Unique layout every wave
- ✅ **Enhanced AI** - Wave-based difficulty scaling
- ✅ **Perfect Controls** - Fixed auto-flap, ceiling bounce
- ✅ **God Mode** - True invincibility with instant kills

### Gameplay Highlights
- Endless wave progression
- Height-based aerial combat
- Egg collection urgency
- Pterodactyl anti-camping
- Safe respawn system
- 3 lives, unlimited continues

---

## 📦 What's Included

### Binary Files
- **JousTrisM5_FINAL.bin** (443 KB)
  - For PlatformIO upload or esptool
  - Firmware only
  
- **JousTrisM5_FINAL_MERGED.bin** (507 KB) ⭐
  - For M5Burner (Recommended)
  - Includes bootloader + partition table + firmware
  - Single file flashing at 0x0000

### Source Code
- **JousTris-Source.zip** (13 KB)
  - Complete PlatformIO project
  - Ready to build and modify
  - Includes all dependencies configuration

### Documentation
- **README.md** - Complete game documentation
- **BUILD.md** - Detailed build instructions
- **CHANGELOG.md** - Full version history
- **LICENSE** - MIT License

---

## 🚀 Quick Start

### Option 1: M5Burner (Easiest) ⭐
1. Download `JousTrisM5_FINAL_MERGED.bin`
2. Open [M5Burner](https://docs.m5stack.com/en/download)
3. Select Custom → Load the `.bin` file
4. Connect M5StickC Plus2 via USB
5. Click "Burn"
6. Play!

### Option 2: PlatformIO
```bash
# Download JousTrisM5_FINAL.bin
pio run --target upload
```

### Option 3: Build from Source
```bash
# Extract JousTris-Source.zip
cd JousTris
pio run -t upload
```

---

## 🎮 Controls

### Hardware Setup
- M5StickC Plus2 (ESP32 handheld)
- Mini JoyC Hat (I2C analog joystick - **required**)

### Controls
- **Joystick Left/Right** - Fly horizontally
- **JoyC Button** - Flap wings
- **Button A (Side)** - Toggle auto-flap mode
- **Button B (Front)** - Toggle god mode

---

## 📊 Game Statistics

### Code
- **Lines of Code**: ~1,200 (main.cpp)
- **RAM Usage**: 27 KB (8.4%)
- **Flash Usage**: 443 KB (34.3%)
- **Frame Rate**: ~60 FPS

### Gameplay
- **Starting Lives**: 3
- **Max Enemies**: 8 per wave
- **Hunter Progression**: 1 → 2 → 3 (Wave 1 → 3 → 9)
- **Egg Hatch Time**: 6s → 2s (Wave 1 → 10+)
- **Pterodactyl Timer**: 30s → 15s (Wave 1 → 15+)

---

## 🐛 Known Issues

**None currently!**

Report bugs on [GitHub Issues](../../issues)

---

## 🔄 Upgrading from Previous Version

If you have an earlier build:
1. Flash `JousTrisM5_FINAL_MERGED.bin` 
2. All settings/saves will reset (no persistent storage)
3. Enjoy improved gameplay!

---

## ⚠️ Requirements

### Hardware (Required)
- M5StickC Plus2
- Mini JoyC Hat (I2C joystick addon)
- USB-C cable

### Software (for building)
- PlatformIO (VSCode or CLI)
- ESP32 toolchain (auto-installed by PlatformIO)

---

## 📝 Changelog Highlights

### v1.0 (Current)
- Limited hunter system (1-3 active hunters)
- Procedural platform generation
- Enhanced wave progression
- Fixed auto-flap persistence
- Ceiling bounce mechanic
- True god mode

### v1.6
- God mode implementation
- Instant kills from any angle

### v1.5
- Procedural platforms
- Smart AI scaling
- Pterodactyl timer adjustments

### v1.4
- Safe respawn system
- Smart spawn checking
- Invulnerability period

See **CHANGELOG.md** for complete history.

---

## 🎯 Game Tips

### Beginner
- Use **auto-flap mode** for easier flight control
- Focus on the **single hunter** enemy first
- Collect eggs quickly (they flash red when urgent)
- Land on platforms to rest and reposition

### Advanced
- Master **ceiling bounce** for aerial superiority
- Bait hunters into pterodactyls
- Use wanderers for easy scoring
- Practice precision pterodactyl head hits (100 pts!)

### God Mode
- Press Button B for invincibility
- Great for learning wave patterns
- Practice egg collection timing
- Test late-game difficulty

---

## 🤝 Contributing

Want to improve JousTris?

1. Fork the repository
2. Extract `JousTris-Source.zip`
3. Make your changes
4. Test on hardware
5. Submit a Pull Request

See **BUILD.md** for development setup.

---

## 📚 Additional Resources

- [M5StickC Plus2 Docs](https://docs.m5stack.com/en/core/M5StickC%20PLUS2)
- [PlatformIO Documentation](https://docs.platformio.org/)
- [Original Joust Wiki](https://en.wikipedia.org/wiki/Joust_(video_game))

---

## 🙏 Acknowledgments

- **Inspired by**: Joust (Williams Electronics, 1982)
- **Hardware**: M5Stack ecosystem
- **Framework**: Arduino/ESP32 + PlatformIO
- **Development**: Corey Millia

---

## 📞 Support

- **Issues**: [GitHub Issues](../../issues)
- **Discussions**: [GitHub Discussions](../../discussions)
- **Email**: [Your contact if desired]

---

## 📜 License

MIT License - See LICENSE file for details.

---

## 🌟 Star This Project!

If you enjoy JousTris, please ⭐ the repository!

---

**Made with ❤️ for retro arcade fans**

*Now go fly some tetromino birds!* 🐦🎮
