# 🤟 SignSpeak — Real-Time Sign Language Gesture Recognition

> A browser-based sign language gesture recognition app powered by **MediaPipe Hands**. Detects **12 gestures** in real-time using your webcam with **voice feedback** — no backend, no installation, fully private.

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![MediaPipe](https://img.shields.io/badge/MediaPipe-4285F4?style=for-the-badge&logo=google&logoColor=white)

---

## ✨ Features

- 🖐 **12 Sign Language Gestures** — Hello, Goodbye, Please, Thank You, Yes, No, I Love You, Peace, OK, Call Me, Rock On, Point
- 🤲 **Dual-Hand Tracking** — Tracks both hands simultaneously with distinct colored skeletons (purple & teal)
- 🔊 **Text-to-Speech** — Speaks each detected gesture aloud using the Web Speech API (toggleable)
- 🦴 **Hand Skeleton Overlay** — Beautiful real-time hand landmark visualization on the camera feed
- ⚡ **Low Latency** — Runs at 30+ FPS with <200ms detection latency
- 🔒 **100% Private** — All processing happens on-device. No video data leaves your browser
- 📦 **Single File** — Just one `index.html` — no build tools, no server, no dependencies to install
- 📊 **Session Stats** — Live tracking of total detections, hand confidence, session time & hand count
- 🎨 **Premium UI** — Dark theme with glassmorphism, gradient accents, and micro-animations
- 🍞 **Toast Notifications** — Visual feedback for every detected gesture with action descriptions
- ⏱ **Smart Debounce** — 1.5s cooldown prevents duplicate gesture triggers

---

## 🤟 Supported Gestures

| # | Gesture | Hand Sign | Action Triggered |
|---|---------|-----------|-----------------|
| 1 | **Hello** | Open palm, fingers spread wide | Welcome |
| 2 | **Goodbye** | Closed fist, all fingers curled | Close / Exit |
| 3 | **Please** | Flat hand, fingers together | Submit / Confirm |
| 4 | **Thank You** | Open hand raised near face | Like / Upvote |
| 5 | **Yes** | 👍 Thumbs up | Approve / Agree |
| 6 | **No** | 👎 Thumbs down | Reject / Decline |
| 7 | **I Love You** | 🤟 Thumb + index + pinky up (ASL ILY) | Express love |
| 8 | **Peace** | ✌️ Index + middle up, rest curled | Peace sign |
| 9 | **OK** | 👌 Thumb-index circle, 3 fingers up | All good |
| 10 | **Call Me** | 🤙 Thumb + pinky out, rest curled | Call me |
| 11 | **Rock On** | 🤘 Index + pinky up, rest curled | Rock on |
| 12 | **Point** | ☝️ Only index finger extended | Attention |

---

## 🚀 Getting Started

### Option 1: Open Locally
Simply open the `index.html` file in your browser:

```bash
# Clone the repo
git clone https://github.com/your-username/sign-language-recognition.git

# Open in browser
start index.html        # Windows
open index.html         # macOS
xdg-open index.html     # Linux
```

### Option 2: GitHub Pages
Deploy to GitHub Pages for a shareable link:

1. Push to a GitHub repository
2. Go to **Settings → Pages**
3. Set source to `main` branch, root folder
4. Your app will be live at `https://your-username.github.io/sign-language-recognition/`

### Option 3: Live Server (VS Code)
1. Install the **Live Server** extension in VS Code
2. Right-click `index.html` → **Open with Live Server**

> **Requirements:** A modern browser (Chrome or Edge recommended) with webcam access.

---

## 🛠 Tech Stack

| Layer | Technology | Purpose |
|-------|-----------|---------|
| Hand Tracking | [MediaPipe Hands](https://google.github.io/mediapipe/solutions/hands.html) (CDN) | Real-time 21-point hand landmark detection |
| Gesture Logic | Custom JavaScript (Rule-Based) | Classify gestures from landmark positions |
| Voice Output | Web Speech API (`speechSynthesis`) | Speak detected gesture names aloud |
| Camera | WebRTC `getUserMedia()` | Native browser camera access |
| UI | HTML5 + Canvas + CSS3 | Single-file, responsive, no framework |
| Hosting | GitHub Pages | Free, instant deployment |

---

## 🏗 Project Structure

```
sign-language-recognition/
├── index.html              # Complete application (single file)
└── README.md               # This file
```

---

## 🎮 How It Works

```
┌──────────────┐     ┌─────────────────┐     ┌──────────────────┐
│   Webcam     │────▶│  MediaPipe Hands │────▶│  21 Landmarks    │
│   (WebRTC)   │     │  (WASM + WebGL)  │     │  per hand (x,y,z)│
└──────────────┘     └─────────────────┘     └────────┬─────────┘
                                                       │
                                                       ▼
┌──────────────┐     ┌─────────────────┐     ┌──────────────────┐
│  Voice (TTS) │◀────│  Action Trigger  │◀────│  Rule-Based      │
│  Toast UI    │     │  + Debounce      │     │  Classifier      │
└──────────────┘     └─────────────────┘     └──────────────────┘
```

1. **Camera Feed** — WebRTC captures live video from the webcam
2. **Hand Detection** — MediaPipe Hands detects up to 2 hands and extracts 21 landmarks each
3. **Skeleton Overlay** — Landmarks are drawn on canvas with colored connections
4. **Gesture Classification** — Rule-based logic checks finger extension/curl states to classify gestures
5. **Action & Feedback** — Recognized gesture triggers toast notification + text-to-speech output

---

## 🧠 Gesture Classification Logic

The classifier uses **finger state detection** based on MediaPipe's 21 hand landmarks:

- **Finger Extended** — Fingertip is above (further from wrist than) the PIP joint
- **Finger Curled** — Fingertip is below the PIP joint
- **Thumb Extended** — Thumb tip distance from index MCP exceeds threshold
- **Thumb Up/Down** — Thumb tip position relative to thumb IP and wrist

Classification follows a **specificity-first order** — more specific gestures (like OK, I Love You) are checked before general ones (like Hello, Goodbye) to minimize misclassification.

---

## ⚙️ Controls

| Button | Function |
|--------|----------|
| 📷 **Toggle Camera** | Start/stop the webcam feed |
| 🦴 **Skeleton** | Show/hide hand landmark overlay |
| 🔊 **Voice** | Enable/disable text-to-speech output |
| 🔄 **Reset** | Reset all gesture counts and session timer |

---

## 🔒 Privacy

- ✅ All processing runs **100% on-device** using WebAssembly and WebGL
- ✅ **No video data** is sent to any server
- ✅ **No cookies**, no analytics, no tracking
- ✅ Voice output uses the browser's **built-in speech synthesis** (offline-capable)

---

## 🌟 Performance

| Metric | Target | Achieved |
|--------|--------|----------|
| Detection FPS | ≥30 FPS | ✅ 30+ FPS on mid-range laptops |
| Gesture Latency | <200ms | ✅ Near-instant classification |
| Hands Tracked | 2 | ✅ Dual-hand support |
| Gestures | 12 | ✅ 12 distinct gestures |

---

## 📋 Roadmap

### ✅ Phase 1 (Current) — Rule-Based
- [x] MediaPipe Hands integration
- [x] 12 gesture rule-based classification
- [x] Dual-hand tracking
- [x] Text-to-speech feedback
- [x] Premium dark UI with animations
- [x] Toast notifications with debounce
- [x] Session statistics

### 🔮 Phase 2 (Future) — ML-Based
- [ ] Collect landmark data and train a TensorFlow.js LSTM model
- [ ] Expand to 20+ gestures (ISL/ASL vocabulary)
- [ ] Add text-to-speech output in multiple languages
- [ ] Mobile / touch device support
- [ ] Two-hand simultaneous gesture combinations
- [ ] Embed as a React component for integration

---

## 📝 License

This project is open source and available under the [MIT License](LICENSE).

---

## 👨‍💻 Author

**Karthik** — Built as an AI portfolio project to make the web more accessible through gesture-based interaction.

---

<p align="center">
  Made with ❤️ using MediaPipe & Web Speech API
</p>
