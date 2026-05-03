# 🍵 KitchenAI Kiosk

> **A premium AI-powered recipe assistant kiosk built on Raspberry Pi 5**  
> Touch + Voice controlled • Apple Glass UI • Step-by-step cooking guidance

---

![KitchenAI Kiosk Banner](https://images.unsplash.com/photo-1556742049-0cfed4f6a45d?w=1200&h=400&fit=crop&q=80)

---

## 📺 Demo Video

> 🎥 *Video coming soon — will be added after hardware demo recording*

---

## ✨ Features

| Feature | Description |
|---|---|
| 🎤 **Voice Control** | Say "chai", "coffee", or "maggi" to select a recipe |
| 👆 **Touch Control** | Tap any recipe card on the 7" touchscreen |
| 🗣️ **Text to Speech** | App speaks each step aloud as you cook |
| ✨ **Step Highlight** | Current step glows — never lose your place |
| 🔄 **Recipe Switching** | Switch recipes mid-way anytime |
| ⏮️ **Step Navigation** | Tap any step to restart from there |
| 🎉 **Completion Screen** | Celebrates when your recipe is done |
| 🌑 **Apple Glass UI** | Dark theme with blur, transparency & premium feel |
| 🚀 **Auto Boot** | Launches automatically when Raspberry Pi starts |

---

## 🍽️ Available Recipes

### 🍵 Masala Chai
> Spiced Indian Tea — 8 step guide with voice narration

### ☕ Filter Coffee  
> Rich & Bold Brew — 8 step guide with voice narration

### 🍜 Maggi Noodles
> 2 Minute Magic — 8 step guide with voice narration

---

## 🛠️ Hardware Used

| Component | Details |
|---|---|
| 🖥️ **Board** | Raspberry Pi 5 |
| 📺 **Display** | 7 inch HDMI Touchscreen |
| 🔊 **Audio** | Speaker via 3.5mm jack |
| 🎤 **Microphone** | USB Microphone |
| 📦 **Purchased from** | Robokits.co.in |

---

## 🧩 Project Structure

```
kiosk/
├── src/
│   ├── App.jsx          → Root app, screen routing, voice recognition
│   ├── App.css          → Full premium glass UI styling
│   └── recipes.js       → All recipe data (steps, colors, images)
├── public/
│   └── index.html       → Entry HTML
├── package.json
└── vite.config.js
```

---

## 🧠 Component Breakdown

### `App.jsx`
Main entry point. Controls:
- Screen routing (`HomeScreen` ↔ `RecipeScreen` ↔ `EndScreen`)
- Voice recognition using **Web Speech API**
- Global speech synthesis control

---

### `HomeScreen`
The welcome screen users see first.
- Shows 3 animated glass recipe cards
- Each card has image, name, tagline, color accent
- **Mic button** at bottom with pulse animation when listening
- Live clock in top right corner
- Ambient floating color orbs in background

---

### `RecipeCard`
Individual recipe card on home screen.
- Glassmorphism design with recipe-specific color theme
- Hover effects — image zoom, glowing border, arrow slide
- Tap or voice triggers navigation to recipe screen

---

### `RecipeScreen`
Main cooking guidance screen. Split layout:

**Left Panel — Steps List:**
- All steps shown in scrollable list
- Active step highlighted with recipe color glow
- Completed steps shown with ✓ and reduced opacity
- Tap any step → restarts voice from that step
- Prev / Next navigation buttons

**Right Sidebar:**
- Recipe image with gradient overlay
- Recipe name and tagline
- Live progress bar showing % completion
- Switch recipe buttons — change recipe anytime mid-cook

---

### `EndScreen`
Shown when all steps are complete.
- Floating animated recipe emoji
- Speaks: *"I hope you enjoy this! Bon appétit!"*
- Options to Make Again or go back Home

---

### `recipes.js`
Data file containing all recipe information:
```js
{
  id, name, emoji, tagline,
  color, accent, gradient,
  image,
  steps: [{ id, instruction }]
}
```

---

## 🎤 Voice Commands

| Say this | Action |
|---|---|
| `"chai"` or `"tea"` | Opens Masala Chai recipe |
| `"coffee"` | Opens Filter Coffee recipe |
| `"maggi"` or `"noodles"` | Opens Maggi Noodles recipe |

> Voice uses **Web Speech API** with `en-IN` language model — works best in Chromium browser on Raspberry Pi

---

## 🚀 Installation & Setup

### Prerequisites
- Raspberry Pi 5 with Raspberry Pi OS
- Node.js v20+
- Chromium browser
- Internet connection (first time only)

### Step 1 — Install Node.js
```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install nodejs -y
node --version  # Should show v20.x.x
```

### Step 2 — Clone this repo
```bash
git clone https://github.com/YOURUSERNAME/kitchen-ai-kiosk.git
cd kitchen-ai-kiosk
```

### Step 3 — Install dependencies
```bash
npm install
```

### Step 4 — Run the app
```bash
npm run dev -- --host --port 5173
```

Open Chromium and go to `http://localhost:5173`

---

## ⚙️ Auto Start on Boot

### Step 1 — Create autostart folder
```bash
mkdir -p ~/.config/autostart
```

### Step 2 — Create server autostart
```bash
nano ~/.config/autostart/kiosk-server.desktop
```
Paste:
```ini
[Desktop Entry]
Type=Application
Name=Kiosk Server
Exec=bash -c "cd ~/kitchen-ai-kiosk && npm run dev -- --host --port 5173"
```

### Step 3 — Create browser autostart
```bash
nano ~/.config/autostart/kiosk-browser.desktop
```
Paste:
```ini
[Desktop Entry]
Type=Application
Name=Kiosk Browser
Exec=bash -c "sleep 8 && chromium --kiosk --disable-infobars http://localhost:5173"
```

### Step 4 — Reboot and test
```bash
sudo reboot
```

App will launch automatically on boot! ✅

---

## 📱 Tablet Access

Your kiosk can also run on a tablet connected to the same network:

```bash
# Find your Pi's IP
hostname -I
```

Then on tablet browser:
```
http://YOUR_PI_IP:5173
```

---

## 🎨 Design System

| Property | Value |
|---|---|
| **Theme** | Dark glassmorphism |
| **Font** | DM Sans + Playfair Display |
| **Background** | `#0a0a0f` deep dark |
| **Glass** | `rgba(255,255,255,0.06)` with `backdrop-filter: blur(24px)` |
| **Chai Color** | `#f59e0b` Amber |
| **Coffee Color** | `#8b5cf6` Purple |
| **Maggi Color** | `#10b981` Emerald |

---

## 🔮 Future Plans

- [ ] Add more recipes
- [ ] Hindi voice support
- [ ] Token/order number system
- [ ] Payment integration
- [ ] Admin panel to manage recipes
- [ ] Nutritional information per recipe
- [ ] Timer for each step

---

## 👨‍💻 Built By

> Built with ❤️ on Raspberry Pi 5  
> Inspired by McDonald's self-order kiosks  
> Powered by React + Vite + Web Speech API

---

## 📄 License

MIT License — free to use and modify
