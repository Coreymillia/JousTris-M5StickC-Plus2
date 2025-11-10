# Building JousTris from Source

Complete guide to building and modifying JousTris for M5StickC Plus2.

---

## 📋 Prerequisites

### Required Software
1. **PlatformIO** (one of the following):
   - [VSCode + PlatformIO Extension](https://platformio.org/install/ide?install=vscode) (Recommended)
   - [PlatformIO CLI](https://platformio.org/install/cli)

2. **USB Drivers** (if needed):
   - Windows: [CP210x USB Driver](https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers)
   - macOS/Linux: Usually works out of the box

### Required Hardware
- M5StickC Plus2
- Mini JoyC Hat (I2C analog joystick)
- USB-C cable

---

## 🚀 Quick Build

### Using VSCode + PlatformIO

1. **Install VSCode & PlatformIO**
   ```bash
   # Download VSCode from https://code.visualstudio.com/
   # Install PlatformIO extension from Extensions marketplace
   ```

2. **Clone/Extract Project**
   ```bash
   git clone https://github.com/YOUR_USERNAME/JousTris.git
   cd JousTris
   ```
   Or extract `JousTris-Source.zip`

3. **Open in VSCode**
   - File → Open Folder → Select `JousTris` folder
   - PlatformIO will auto-detect project

4. **Build & Upload**
   - Connect M5StickC Plus2 via USB
   - Click **PlatformIO: Upload** (→) button in bottom status bar
   - Or press `Ctrl+Alt+U` (Windows/Linux) or `Cmd+Shift+U` (macOS)

5. **Monitor (Optional)**
   - Click **PlatformIO: Serial Monitor** (🔌) button
   - View debug output at 115200 baud

### Using PlatformIO CLI

```bash
# Navigate to project directory
cd JousTris

# Build project
pio run

# Upload to device
pio run --target upload

# Build and upload in one command
pio run -t upload

# Monitor serial output
pio device monitor -b 115200
```

---

## 📁 Project Structure

```
JousTris/
├── src/
│   ├── main.cpp              # Main game code (~1200 lines)
│   ├── UNIT_MiniJoyC.cpp     # JoyC I2C controller driver
│   └── UNIT_MiniJoyC.h       # JoyC header
├── include/                   # Additional headers (if needed)
├── platformio.ini            # PlatformIO config
├── .pio/                     # Build output (auto-generated)
│   └── build/
│       └── m5stick-c-plus2/
│           ├── firmware.bin  # Compiled game
│           ├── bootloader.bin
│           └── partitions.bin
└── README.md
```

---

## ⚙️ Configuration

### platformio.ini Explained

```ini
[env:m5stick-c-plus2]
platform = espressif32
board = m5stick-c
framework = arduino

# Dependencies (auto-installed)
lib_deps = 
    m5stack/M5StickCPlus2@^1.0.2

# Build flags
build_flags = 
    -DCORE_DEBUG_LEVEL=0
    
# Serial monitor
monitor_speed = 115200
monitor_filters = default

# Upload settings
upload_speed = 1500000
```

### Key Settings
- **Platform**: ESP32 (espressif32)
- **Board**: M5Stick-C (compatible with Plus2)
- **Framework**: Arduino
- **Upload Speed**: 1.5 Mbps (fast)
- **Monitor Speed**: 115200 baud

---

## 🔧 Customizing the Game

### Editing Game Constants

Open `src/main.cpp` and modify these values:

#### Physics
```cpp
#define GRAVITY 0.3              // Falling speed
#define FLAP_POWER 4.5          // Jump strength
#define MAX_VY 8.0              // Max vertical velocity
#define HORIZONTAL_SPEED 2.0    // Move speed
```

#### Game Balance
```cpp
#define MAX_ENEMIES 8           // Max enemies per wave
#define MAX_EGGS 6              // Max eggs on screen
#define MAX_PTERODACTYLS 2      // Max pterodactyls

// Starting lives
player.lives = 3;               // Line ~321

// Enemy spawn count per wave
int enemiesToSpawn = min(3 + wave, 8);  // Line ~888
```

#### Colors (RGB565 format)
```cpp
#define COLOR_BG 0x0000         // Black background
#define COLOR_S 0x07E0          // Green player
#define COLOR_Z 0xF800          // Red enemies
#define COLOR_PLATFORM 0x7BEF   // Gray platforms
#define COLOR_EGG 0xFFE0        // Yellow eggs
#define COLOR_LAVA 0xF800       // Red lava
```

#### AI Behavior
```cpp
// Hunter assignment (line ~269)
int maxHunters = 1;              // Wave 1-2
if (wave >= 3 && wave < 9) {
    maxHunters = 2;              // Wave 3-8
} else if (wave >= 9) {
    maxHunters = 3;              // Wave 9+
}

// Chase probability (line ~533)
int chaseChance = min(75 + wave * 5, 95);  // Hunters
int chaseChance = min(15 + wave * 2, 30);  // Wanderers
```

---

## 🐛 Troubleshooting

### Build Errors

**Error**: `Platform 'espressif32' not installed`
```bash
pio platform install espressif32
```

**Error**: `Library 'M5StickCPlus2' not found`
```bash
pio lib install "m5stack/M5StickCPlus2@^1.0.2"
```

**Error**: `Cannot open serial port`
- Check USB cable (data cable, not charging-only)
- Install CP210x drivers
- Check device permissions (Linux: `sudo usermod -a -G dialout $USER`)

### Upload Issues

**Device not detected**:
```bash
# List connected devices
pio device list

# Manual port specification
pio run -t upload --upload-port /dev/ttyUSB0    # Linux
pio run -t upload --upload-port COM3            # Windows
pio run -t upload --upload-port /dev/cu.SLAB*   # macOS
```

**Upload fails during flashing**:
- Hold Button A while clicking Upload
- Press Reset button after upload starts
- Try slower upload speed in `platformio.ini`:
  ```ini
  upload_speed = 921600
  ```

### Runtime Issues

**Black screen**:
- Check M5StickC Plus2 is powered on
- Try resetting device
- Verify firmware uploaded successfully

**JoyC not responding**:
- Check JoyC Hat is properly connected to I2C port
- Verify I2C address (0x54) matches in code
- Try reseating the hat

**Crashes/Resets**:
- Enable debug output:
  ```cpp
  #define CORE_DEBUG_LEVEL 3
  ```
- Monitor serial output for error messages

---

## 🔍 Advanced: Creating Merged Binary

For M5Burner distribution, create a merged binary with bootloader:

```bash
cd JousTris

# Create merged binary (Python)
python3 << 'EOF'
# Read binaries
with open('.pio/build/m5stick-c-plus2/bootloader.bin', 'rb') as f:
    bootloader = f.read()
with open('.pio/build/m5stick-c-plus2/partitions.bin', 'rb') as f:
    partitions = f.read()
with open('.pio/build/m5stick-c-plus2/firmware.bin', 'rb') as f:
    firmware = f.read()

# Create merged binary
merged = bytearray(0x10000 + len(firmware))
merged[0x1000:0x1000+len(bootloader)] = bootloader
merged[0x8000:0x8000+len(partitions)] = partitions
merged[0x10000:0x10000+len(firmware)] = firmware

# Save
with open('JousTris_MERGED.bin', 'wb') as f:
    f.write(merged)
print(f'Created: JousTris_MERGED.bin ({len(merged)} bytes)')
EOF
```

**Memory Layout**:
- `0x0000 - 0x0FFF`: Padding
- `0x1000 - 0x5FFF`: Bootloader (~17 KB)
- `0x8000 - 0x8FFF`: Partition table (~3 KB)
- `0x10000+`: Firmware (~443 KB)

---

## 📊 Build Statistics

**Typical build output**:
```
RAM:   [=         ]   8.4% (used 27396 bytes from 327680 bytes)
Flash: [===       ]  34.3% (used 453008 bytes from 1310720 bytes)
```

**Build time**: ~15-20 seconds (first build with dependencies)  
**Upload time**: ~5 seconds @ 1.5 Mbps  
**Total time**: ~25 seconds cold build → upload  

---

## 🧪 Testing Changes

### Quick Test Cycle
1. Modify code
2. `pio run -t upload` (or click Upload in VSCode)
3. Device auto-resets and runs new code
4. Test gameplay
5. Repeat

### Using Serial Monitor
Add debug output to your code:
```cpp
Serial.println("Player position: " + String(player.x) + "," + String(player.y));
```

View in monitor:
```bash
pio device monitor -b 115200
```

---

## 📚 Additional Resources

### Documentation
- [PlatformIO Docs](https://docs.platformio.org/)
- [M5StickC Plus2 Docs](https://docs.m5stack.com/en/core/M5StickC%20PLUS2)
- [Arduino ESP32 Core](https://docs.espressif.com/projects/arduino-esp32/)

### Libraries Used
- [M5StickCPlus2](https://github.com/m5stack/M5StickCPlus2) - Hardware abstraction
- [M5Unified](https://github.com/m5stack/M5Unified) - Unified M5 API
- [M5GFX](https://github.com/m5stack/M5GFX) - Graphics library

### Community
- [M5Stack Community](https://community.m5stack.com/)
- [PlatformIO Community](https://community.platformio.org/)

---

## 🤝 Contributing

When submitting changes:

1. **Test thoroughly** on real hardware
2. **Follow existing code style**
3. **Comment complex logic**
4. **Update README if adding features**
5. **Test all game modes** (normal, auto-flap, god mode)
6. **Verify builds cleanly**:
   ```bash
   pio run --target clean
   pio run
   ```

---

**Happy Coding!** 🎮

*Questions? Open an issue on GitHub.*
