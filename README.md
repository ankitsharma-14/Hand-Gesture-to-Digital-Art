[README.md](https://github.com/user-attachments/files/31658250/README.md)
# 🎨 Hand Gesture to Digital Art

An interactive, touchless canvas application that translates real-time hand gestures into dynamic digital art using computer vision, browser-native Web APIs, and high-performance visual rendering engine.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![MediaPipe](https://img.shields.io/badge/MediaPipe-Hands-orange.svg)
![HTML5 Canvas](https://img.shields.io/badge/WebGL%2FCanvas-HTML5-green.svg)
![Status](https://img.shields.io/badge/status-active-brightgreen.svg)

---

## 📖 Table of Contents

- [Overview](#-overview)
- [Key Features](#-key-features)
- [Gesture Controls](#-gesture-controls)
- [Artistic Brush Modes](#-artistic-brush-modes)
- [Architecture & Tech Stack](#-architecture--tech-stack)
- [Quick Start](#-quick-start)
- [Configuration & Sensitivity](#-configuration--sensitivity)
- [Project Structure](#-project-structure)
- [Performance Optimization](#-performance-optimization)
- [License](#-license)

---

## 🌟 Overview

**Hand Gesture to Digital Art** turns any standard webcam into an expressive, controller-free digital paint environment. By capturing 21 visual hand landmarks in 3D space, the application maps spatial coordinates and dynamic gestures to canvas drawing commands in real time. 

Whether used as an interactive art exhibit, an accessibility tool, or a computer vision demo, this project provides a seamless bridge between human physical movement and digital canvas aesthetics.

---

## ✨ Key Features

- 🖐 **Real-Time Hand Tracking:** High-precision tracking of 21 3D hand landmarks via MediaPipe.
- 🎨 **Multiple Visual Modes:** Neon Glow, Flowing Particles, Dynamic Rainbow, and Classic Line.
- 📐 **Depth & Speed Responsiveness:** Dynamic brush sizing and opacity linked to hand distance from camera and gesture velocity.
- 🧼 **Touchless Navigation:** Perform full canvas clears, tool switches, and color selections entirely through spatial gestures.
- 📷 **High-Res Export:** Save your artwork directly to PNG format with custom background overlays.
- ⚡ **Zero External Hardware:** Operates purely through standard browser webcams without specialized gloves or sensors.

---

## 🖐 Gesture Controls

| Gesture | Action | Trigger Details |
| :--- | :--- | :--- |
| **Pinch (Thumb + Index)** | **Draw / Paint** | Brings Index Tip (Landmark 8) and Thumb Tip (Landmark 4) together. |
| **Open Palm (5 Fingers)** | **Clear Canvas** | Fully extends all 5 fingers for 1.5 seconds to wipe the screen. |
| **Peace Sign (Index + Middle)**| **Next Color** | Extends Index and Middle fingers while folding ring and pinky. |
| **Fist (All Closed)** | **Pause Tracking** | Halts drawing input while preserving existing artwork on canvas. |
| **Z-Axis Push / Pull** | **Brush Size Scale** | Moving hand closer/further changes bounding box scale dynamically. |

---

## 🖌 Artistic Brush Modes

1. **Neon Glow (`globalCompositeOperation = 'lighter'`):**
   Uses multi-layered Gaussian blur and additive color blending to create vibrant light trails reminiscent of light painting photography.
2. **Particle Spray:**
   Spawns dynamic velocity-driven particles along the fingertip trajectory that decay and scatter gracefully over time.
3. **Dynamic Spectrum:**
   Cycles smoothly through the HSL color spectrum based on drawing speed and stroke acceleration.
4. **Calligraphy / Classic Line:**
   Sleek vector path drawing with pressure-simulated line width smoothing.

---

## 🛠 Architecture & Tech Stack

```
[ Web Camera Feed ] 
         │
         ▼
[ MediaPipe Hands (CDN) ] ── (Extract 21 3D Landmarks)
         │
         ▼
[ Gesture Recognition Engine ] ── (Pinch Distance, Open Palm Filter)
         │
         ▼
[ HTML5 Canvas / WebGL Engine ] ── (Render Strokes, Particles & FX)
         │
         ▼
[ Interactive UI Overlay ] ── (Presets, Controls & PNG Export)
```

- **Frontend:** HTML5, CSS3 (Modern Flex/Grid UI Overlay), Vanilla JavaScript (ES6+).
- **Vision Pipeline:** `@mediapipe/hands`, `@mediapipe/camera_utils`.
- **Render Engine:** 2D Canvas API / WebGL with `requestAnimationFrame` render loops.

---

## 🚀 Quick Start

### Prerequisites
- A modern web browser supporting WebGL and WebRTC (Chrome, Edge, Firefox, Safari).
- An integrated or external USB webcam.

### Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/your-username/hand-gesture-art.git
   cd hand-gesture-art
   ```

2. **Serve the project locally:**
   Webcam permissions require a secure context (`https://`) or a local server (`http://localhost`).

   Using Python:
   ```bash
   python3 -m http.server 8000
   ```
   Using Node.js (`npx`):
   ```bash
   npx serve .
   ```

3. **Launch in Browser:**
   Open `http://localhost:8000` in your web browser and allow webcam access when prompted.

---

## ⚙️ Configuration & Sensitivity

You can adjust tracking sensitivity directly inside `js/config.js` or through the developer console:

```javascript
const CONFIG = {
  // Distance threshold between index and thumb tip to trigger drawing (in normalized coordinate space)
  PINCH_THRESHOLD: 0.05,
  
  // Smoothing factor for landmark coordinates (0 = raw, 1 = maximum smooth)
  SMOOTHING_FACTOR: 0.65,
  
  // Time threshold (ms) required to trigger clear gesture
  CLEAR_GESTURE_HOLD_MS: 1500,
  
  // Maximum particle lifetime in frame counts
  PARTICLE_LIFESPAN: 60
};
```

---

## 📁 Project Structure

```
hand-gesture-art/
├── index.html          # Main HTML entry point & UI overlay layout
├── css/
│   └── style.css       # Fullscreen canvas layout, glassmorphism UI overlay
├── js/
│   ├── app.js          # Main application initializer & render loop
│   ├── tracking.js     # MediaPipe pipeline initialization & data processing
│   ├── gestures.js     # Gesture evaluation logic (Pinch, Open Palm, Fist)
│   ├── brushes.js      # Rendering routines (Neon, Particle, Rainbow, Ink)
│   └── config.js       # Global configuration & sensitivity settings
└── assets/
    └── icons/          # UI control iconography
```

---

## ⚡ Performance Optimization

- **Render Loop:** Employs off-screen canvas buffering to prevent redraw stuttering at high frame rates.
- **Data Smoothing:** Uses exponential moving averages on landmark coordinates to reduce camera jitter.
- **Resource Management:** Automatic particle pooling to prevent garbage collection spikes during dense rendering sessions.

---

## 📜 License

Distributed under the MIT License. See `LICENSE` for more information.
