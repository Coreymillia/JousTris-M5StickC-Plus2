# GitHub Upload Instructions

Quick guide to uploading JousTris to GitHub.

---

## 📋 Prerequisites

1. GitHub account
2. All files from `github-release/` folder

---

## 🚀 Step-by-Step Upload

### Step 1: Create New Repository

1. Go to https://github.com/new
2. **Repository name**: `JousTris`
3. **Description**: "Joust meets Tetris - Arcade aerial combat for M5StickC Plus2"
4. **Visibility**: Public (or Private if preferred)
5. **Initialize with**:
   - ✅ Add README file (we'll replace it)
   - ✅ Add .gitignore (choose "Arduino")
   - ✅ Choose a license: MIT License
6. Click **Create repository**

### Step 2: Upload Files

#### Method A: Web Interface (Easiest)

1. **Upload Source Code**:
   - Click "Add file" → "Upload files"
   - Drag `JousTris-Source.zip`
   - Commit message: "Add source code"
   - Click "Commit changes"

2. **Replace README**:
   - Click on `README.md`
   - Click pencil icon (Edit)
   - Replace content with `github-release/README.md` content
   - Commit message: "Update README with game documentation"
   - Click "Commit changes"

3. **Add Other Documentation**:
   - Upload `BUILD.md`
   - Upload `CHANGELOG.md`
   - Commit message: "Add documentation"

#### Method B: Git Command Line

```bash
# Clone your new repository
git clone https://github.com/YOUR_USERNAME/JousTris.git
cd JousTris

# Copy files from github-release folder
cp /home/coreymillia/Documents/JousTris/github-release/* .

# Add all files
git add .

# Commit
git commit -m "Initial release v1.0"

# Push
git push origin main
```

### Step 3: Create Release

1. Go to your repository page
2. Click "Releases" (right sidebar)
3. Click "Create a new release"

4. **Tag version**: `v1.0`
   - Click "Create new tag: v1.0 on publish"

5. **Release title**: `JousTris v1.0 - FINAL RELEASE`

6. **Description**: Copy content from `RELEASE_NOTES.md`

7. **Attach binaries**:
   - Click "Attach binaries by dropping them here"
   - Upload `JousTrisM5_FINAL.bin`
   - Upload `JousTrisM5_FINAL_MERGED.bin`
   - Upload `JousTris-Source.zip`

8. **Mark as latest release**: ✅ Check this box

9. Click **Publish release**

---

## 📁 Final Repository Structure

Your GitHub repo should look like:

```
JousTris/
├── README.md                          # Main documentation
├── BUILD.md                           # Build instructions
├── CHANGELOG.md                       # Version history
├── LICENSE                            # MIT License
├── .gitignore                        # Git ignore patterns
└── Releases (v1.0)
    ├── JousTrisM5_FINAL.bin          # Firmware binary
    ├── JousTrisM5_FINAL_MERGED.bin   # M5Burner binary ⭐
    └── JousTris-Source.zip           # Source code
```

---

## 🎨 Optional: Add Topics

Add topics to your repository for discoverability:

1. Go to your repository
2. Click ⚙️ next to "About"
3. Add topics:
   - `m5stack`
   - `m5stickc-plus2`
   - `arduino`
   - `esp32`
   - `joust`
   - `tetris`
   - `retro-games`
   - `arcade-game`
   - `platformio`

---

## 🖼️ Optional: Add Screenshots

If you have screenshots or photos:

1. Create `screenshots/` folder in repo
2. Upload images
3. Add to README.md:
   ```markdown
   ## Screenshots
   
   ![Gameplay](screenshots/gameplay.jpg)
   ![Title Screen](screenshots/title.jpg)
   ```

---

## 📝 Recommended README Badges

Add these to top of README.md:

```markdown
![Version](https://img.shields.io/badge/version-1.0-blue)
![Platform](https://img.shields.io/badge/platform-M5StickC%20Plus2-orange)
![License](https://img.shields.io/badge/license-MIT-green)
![Stars](https://img.shields.io/github/stars/YOUR_USERNAME/JousTris)
```

---

## 🔗 Share Your Repository

After uploading, share on:

- [M5Stack Community](https://community.m5stack.com/)
- Reddit: r/M5Stack, r/esp32, r/embedded
- Twitter/X with hashtags: #M5Stack #ESP32 #RetroGaming
- Hackaday.io

---

## ✅ Verification Checklist

Before making repository public, verify:

- [ ] README.md displays correctly
- [ ] BUILD.md has correct instructions
- [ ] CHANGELOG.md is complete
- [ ] Release v1.0 created
- [ ] Binaries attached to release
- [ ] Source zip downloadable
- [ ] License file present
- [ ] Repository description set
- [ ] Topics added

---

## 🎯 Example URLs

After upload, your URLs will be:

- **Repository**: `https://github.com/YOUR_USERNAME/JousTris`
- **Releases**: `https://github.com/YOUR_USERNAME/JousTris/releases`
- **Latest Release**: `https://github.com/YOUR_USERNAME/JousTris/releases/tag/v1.0`
- **Clone URL**: `https://github.com/YOUR_USERNAME/JousTris.git`

---

## 🆘 Troubleshooting

**Files too large**:
- Use Git LFS for binaries >100MB
- Your files are under limit (507 KB max)

**Can't push**:
```bash
git pull origin main --rebase
git push origin main
```

**Wrong branch**:
```bash
git branch -M main  # Rename branch to 'main'
git push -u origin main
```

---

## 📧 Need Help?

- [GitHub Docs](https://docs.github.com/)
- [Git Basics](https://git-scm.com/book/en/v2/Getting-Started-Git-Basics)

---

**You're Ready to Share JousTris with the World!** 🎉

*Good luck with your release!* 🚀
