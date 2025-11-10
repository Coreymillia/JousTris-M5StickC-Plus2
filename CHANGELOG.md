# Changelog

All notable changes to JousTris will be documented in this file.

## [1.0] - 2024-11-10 - FINAL RELEASE

### 🎉 Major Features
- **Limited Hunter System**: Only 1-3 enemies actively hunt player per wave
- **Wanderer Enemies**: Remaining enemies patrol randomly for better board coverage
- **Dynamic Hunter Assignment**: Dead hunters automatically replaced
- **Procedural Platform Generation**: Fresh layout every wave
- **Enhanced Wave Progression**: Smarter difficulty scaling
- **Ceiling Bounce**: Both player and enemies bounce from top boundary
- **True God Mode**: Invincible with instant kills from any angle
- **Auto-Flap Persistence**: Auto-flap mode stays enabled across waves

### 🎮 Gameplay Balance
- Wave 1-2: 1 hunter + 2-3 wanderers
- Wave 3-8: 2 hunters + 3-5 wanderers
- Wave 9+: 3 hunters (max) + 5 wanderers
- Hunters: 80-95% chase behavior
- Wanderers: 17-30% chase behavior (mostly random)

### 🐛 Bug Fixes
- Fixed auto-flap causing ceiling stuck in Wave 2+
- Fixed auto-flap resetting between waves
- Fixed static variable timing issues
- Fixed hunter swarm overwhelming early game

### ⚡ Performance
- Optimized AI decision making
- Improved collision detection
- Better spawn checking for respawn system

---

## [1.6] - 2024-11-10 - God Mode

### Added
- True invincible god mode
- God mode kills enemies from any angle (no height requirement)
- God mode works on pterodactyls (no precision needed)

### Fixed
- God mode was skipping all collision detection
- God mode not allowing enemy kills

---

## [1.5] - 2024-11-10 - Enhanced Waves (COMPLETE2)

### Added
- Procedural platform generation (3-5 platforms per wave)
- Platform layout randomizes every wave
- Smarter AI behavior based on wave level
- Aggressive chase behavior increases with wave
- Pterodactyl spawn timers shorten each wave

### Changed
- AI state change frequency increases with wave (3s → 0.8s)
- Chase behavior chance increases (65% → 80%)
- Enemy speed scales better (1.0x → 2.5x max)
- Pterodactyl wave timer: 30s → 15s minimum
- Pterodactyl idle timer: 15s → 8s minimum

---

## [1.4] - 2024-11-10 - Safe Respawn (COMPLETE)

### Added
- Safe spawn point checking (avoids enemies, eggs, pterodactyls)
- 0.8 second respawn delay
- 2 second invulnerability after respawn with flashing sprite
- Multiple spawn location attempts
- Smart spawn positioning

### Changed
- Death no longer causes instant game over (unless 0 lives)
- Respawn system keeps game flowing
- World continues running during respawn delay

---

## [1.3] - 2024-11-10 - Pterodactyl & Eggs

### Added
- Pterodactyl anti-camping hazard
- Pterodactyl homing behavior
- Pterodactyl precision head hitbox requirement
- Aggressive egg hatch timing (6s → 2s by wave 10)
- Egg visual warning (flashes red in last 1.5s)
- Egg warning bar in last 3 seconds

### Changed
- Eggs drop from defeated enemies
- Eggs hatch into stronger enemies if not collected
- Pterodactyl spawns when stalling (30s+ wave time or 15s+ idle)
- Multiple pterodactyls in later waves

---

## [1.2] - 2024-11-10 - Working Waves

### Added
- Wave completion detection
- Wave progression system
- Enemy count increases per wave (3 → 8 max)
- Smarter enemy AI to avoid lava suicide
- Enemy flapping logic for survival

### Fixed
- Wave 1 getting stuck (enemies never cleared)
- Enemies flying into lava immediately
- Enemies flying off top of screen
- Wave not advancing after clearing enemies

---

## [1.1] - 2024-11-10 - Directional Birds

### Added
- S-piece shape when flying right
- Z-piece shape when flying left
- Dynamic sprite flipping based on velocity
- Consistent colors (green player, red enemies)

### Changed
- Birds now visually face direction of travel
- Same color whether S or Z shape

---

## [1.0] - 2024-11-10 - Starting Point

### Initial Release
- Classic Joust physics (gravity + flapping)
- Height-based combat system
- S and Z tetromino bird sprites
- Platform system (5 static platforms)
- Screen wrapping (left/right edges)
- Lava hazard at bottom
- Basic enemy AI (3 states: wander, chase, flee)
- Egg drop system
- Particle effects
- Lives system (3 lives, game over at 0)
- Score tracking
- JoyC controller support
- Auto-flap mode
- God mode
- Title screen with animation

### Core Features
- M5StickC Plus2 support
- Mini JoyC Hat control
- RGB565 color graphics
- 135x240 portrait display
- 60 FPS gameplay

---

## Development Timeline

**Total Development Time**: ~6 hours  
**Date**: November 10, 2024  
**Platform**: M5StickC Plus2 with Mini JoyC Hat  
**Framework**: Arduino/ESP32 + PlatformIO  

---

## Credits

**Game Design**: Corey Millia  
**Development**: Corey Millia  
**Inspired by**: Joust (Williams Electronics, 1982)  
**Hardware**: M5Stack  

---

*For detailed commit history, see Git log*
