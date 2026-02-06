# detraque ❌🍪

> Break the tracking. Take back control of your links.

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
![Version](https://img.shields.io/badge/version-0.1.0--beta-orange)
![Shell](https://img.shields.io/badge/shell-bash-green)

[🇫🇷 Version française](README.md)

---

## 🎯 What is it?

**detraque** is a command-line tool that automatically removes tracking parameters from URLs. Lightweight, fast, with automatic logging and YouTube timestamp support.

Designed for activists, data professionals, public servants, and anyone concerned about their digital privacy.

### ✨ Features

- 🧹 **Automatic cleaning** of tracking parameters on YouTube, X/Twitter, Facebook, Instagram
- ⏱️ **YouTube timestamps**: easily add a timestamp to your video links
- 📝 **Automatic logging**: keeps a history of all your cleaned links
- ✅ **URL verification**: test if a link works before sharing it
- 🎨 **Colorful interface**: for a pleasant daily use
- 📋 **Automatic clipboard copy** (macOS)

### 🔍 Supported platforms

| Platform | Removed parameters |
|----------|-------------------|
| YouTube | `?si=`, `&feature=`, `&utm_*` |
| X/Twitter | `?s=`, `?t=`, `&utm_*` |
| Facebook | `?fbclid=`, `&utm_*` |
| Instagram | `?igshid=`, `&utm_*` |

---

## 🚨 Why tracking is problematic

### 📊 Your personal data is being sold

Tracking parameters in URLs allow platforms to know:
- **Who** shares a link with **whom**
- **When** and **where** a link is shared
- **How** content spreads through your network

This data feeds detailed advertising profiles that are then monetized. **If it's free, you're the product.**

### 🏢 Big Tech's dominant position

Systematic tracking reinforces the power of tech giants by giving them considerable informational advantage over:
- Social behaviors
- Influence networks
- Information dissemination patterns

In an era where digital sovereignty and the commons are becoming priorities worldwide, every action counts.

### 🔒 Cybersecurity concerns

Tracking parameters can also:
- **Reveal sensitive information** about your organization
- **Expose your habits** in browsing and communication
- **Facilitate phishing** by allowing attackers to better target their victims

For data professionals, DPOs, CISOs, and public servants: cleaning your links is a **good digital hygiene practice**.

---

## 💡 Why "detraque"?

**detraque** is a play on words:
- In French: "détraqué" = to break, to disrupt → **we break tracking**
- In English: with a French pronunciation, it has a "French touch"
- It's unique: no other CLI tool has this name

*Fun fact*: The name also references the song **"Mon inconnu"** by Zaho de Sagazan 🎵

---

## 📦 Installation

### Prerequisites

- **bash** (pre-installed on macOS and Linux)
- **curl** (usually pre-installed)
- **sed** and **grep** (standard tools)

### Quick install

```bash
# 1. Download the script
curl -O https://raw.githubusercontent.com/caffe-doppio/detraque/main/detraque

# 2. Make it executable
chmod +x detraque

# 3. Move to a PATH directory
sudo mv detraque /usr/local/bin/

# 4. Verify installation
detraque help
```

### Manual installation

```bash
# 1. Clone the repo
git clone https://github.com/caffe-doppio/detraque.git
cd detraque

# 2. Copy the script
cp detraque ~/bin/detraque
chmod +x ~/bin/detraque

# 3. Add ~/bin to PATH if needed
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.zshrc  # or ~/.bashrc
source ~/.zshrc
```

---

## 🚀 Usage

### Available commands

```bash
detraque clean <url>                  # Clean a URL
detraque clean-time <url> <hh:mm:ss>  # Clean + add timestamp
detraque timestamp <hh:mm:ss> [url]   # Convert timestamp
detraque verify <url>                 # Verify a URL
detraque logs                         # Show today's logs
detraque help                         # Help
```

### Practical examples

#### 1️⃣ Clean a YouTube link

```bash
detraque clean "https://www.youtube.com/watch?v=abc123&si=tracker123"
```

**Result:**
```
Platform detected: YouTube

Original:
https://www.youtube.com/watch?v=abc123&si=tracker123

Cleaned:
https://www.youtube.com/watch?v=abc123

✓ Logged in: ~/Documents/detraque-logs/2025-02-05-cleaned-urls.md
✓ Copied to clipboard
```

#### 2️⃣ Share a specific moment of a video (without tracking)

```bash
detraque clean-time "https://youtube.com/watch?v=abc&si=tracker" 1:08:33
```

**Result:**
```
Platform detected: YouTube
Timestamp: 1:08:33 (4113s)

Original:
https://youtube.com/watch?v=abc&si=tracker

Cleaned + Timestamp:
https://youtube.com/watch?v=abc?t=4113s

✓ Logged in: ~/Documents/detraque-logs/2025-02-05-cleaned-urls.md
✓ Copied to clipboard
```

#### 3️⃣ Note multiple moments from a long video

While watching a 2-hour conference:

```bash
# Interesting moment at 15:30
detraque clean-time "https://youtube.com/watch?v=conf2024" 15:30

# Another moment at 45:20
detraque clean-time "https://youtube.com/watch?v=conf2024" 45:20

# Retrieve all links
detraque logs
```

All your moments are logged with their timestamps, ready to share!

#### 4️⃣ Verify a link works

```bash
detraque verify "https://youtube.com/watch?v=abc123"
```

**Result:**
```
Verifying: https://youtube.com/watch?v=abc123

✓ Functional URL (HTTP 200)
Title: My awesome video - YouTube
```

---

## 📊 Automatic logs

All cleaned links are automatically saved in:

```
~/Documents/detraque-logs/YYYY-MM-DD-cleaned-urls.md
```

**Log format:**

```markdown
# Cleaned URLs - 2025-02-05

---

## [2025-02-05 14:30:15] - Timestamp: 1:08:33

**Original:**
```
https://www.youtube.com/watch?v=abc&si=tracker
```

**Cleaned:**
```
https://www.youtube.com/watch?v=abc?t=4113s
```

---
```

To display today's logs:

```bash
detraque logs
```

---

## 🛠️ Compatibility

### Supported systems

- 🍎 **macOS** (tested on macOS 14+)
- 🐧 **Linux** (Ubuntu, Debian, Fedora, Asahi, Arch...)
- 🖥️ **WSL** (Windows Subsystem for Linux)

### Clipboard

Automatic copy works with:
- **macOS**: `pbcopy` (pre-installed)
- **Linux**: `xclip` (install if needed)

```bash
# Install xclip on Linux
sudo apt install xclip      # Debian/Ubuntu
sudo dnf install xclip      # Fedora
sudo pacman -S xclip        # Arch
```

---

## 🐧 Want to make the switch to Linux?

**detraque** runs natively on Linux. If you want to take the leap and discover a free system, here are three recommended distributions:

### 🟠 Ubuntu
**For a smooth start**
- Intuitive and modern interface
- Huge community worldwide
- Excellent hardware support
- [Download Ubuntu](https://ubuntu.com/download/desktop)

### 🍎 Asahi Linux
**For Apple Silicon Macs**
- Fedora-based distribution optimized for M1/M2/M3 processors
- Ambitious project that frees modern Macs
- Perfect if you want to keep your Mac but migrate to Linux
- [Discover Asahi](https://asahilinux.org/)

### 🦜 Parrot OS
**For security and privacy**
- Cybersecurity-focused distribution with **all tools pre-installed**
- Super stable out-of-the-box
- Ideal for DPOs, CISOs, and data professionals
- Little known but incredibly complete
- [Download Parrot OS](https://parrotsec.org/)

💡 **Why Parrot?** Contrary to popular belief, the CLI (command line) is not reserved for experts. It's like learning a language: you don't avoid grammar just because it's complex. Parrot gives you all the tools from the start, and the community is there to support you.

---

## 🤝 Contributing

Contributions are welcome!

### Report a bug

Open an [issue](https://github.com/caffe-doppio/detraque/issues) describing:
- Expected behavior
- Observed behavior
- Steps to reproduce
- Your system (macOS, Linux, version)

### Suggest a feature

Have an idea? Open an [issue](https://github.com/caffe-doppio/detraque/issues) with the `enhancement` tag.

### Add a platform

To add support for a new platform:
1. Fork the project
2. Add cleaning patterns in `clean_url()` and `clean_time()` functions
3. Test on multiple URLs
4. Open a Pull Request

---

## 📜 License

This project is licensed under **GNU General Public License v3.0**.

This means you can:
- 🌱 Use this tool freely
- 🧑🏻‍💻 Study and modify the source code
- ♻️ Redistribute copies
- ↩️ Distribute your modified versions

**Important condition**: Any modified version must also be distributed under GPL-3.0 (copyleft).

See the [LICENSE](LICENSE) file for details.

---

## 👤 Author

Created by **[@caffe-doppio](https://github.com/caffe-doppio)**

*Developed as part of a commitment to digital sovereignty and privacy protection.*

---

## 🙏 Acknowledgments

- To everyone advocating for more ethical digital practices
- To public servants working on digital sovereignty
- To the open source community

---

## 📚 Resources

### Privacy and tracking

- [CNIL - Cookies and trackers](https://www.cnil.fr/en/cookies-and-other-tracking-devices-cnil-publishes-new-guidelines) (France's data protection authority)
- [ANSSI - IT hygiene guide](https://www.ssi.gouv.fr/en/guide/it-hygiene/) (French cybersecurity agency)

### Digital sovereignty

- [Public interest digital commons](https://lesbases.anct.gouv.fr/) (France)
- [Digital suite and more](https://www.proconnect.gouv.fr/services) (France)

---

**Break the tracking. Take back control.** ❌🍪
