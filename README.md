# 🎨 Hand Gesture to Digital Art

An interactive, touchless canvas application that translates real-time hand gestures into dynamic digital art using computer vision, browser-native Web APIs, and high-performance visual rendering engine.

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
- [Performance Notes](#-performance-notes)
- [Camera Privacy](#-camera-privacy)
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
- A modern browser with camera support.
- An integrated or external webcam.
- Internet access to load MediaPipe and icon assets from the CDNs referenced in `index.html`.

The browser must be able to request camera permission. Run the page from `http://localhost` or HTTPS, not an arbitrary insecure HTTP host.

### Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/ankitsharma-14/Hand-Gesture-to-Digital-Art.git
   cd Hand-Gesture-to-Digital-Art
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

The application is currently a single-page implementation. Its styles, gesture handling, brush rendering, and configuration live inside `index.html`, not in a separate `js/config.js` file.

To tune tracking, inspect the script in `index.html`, including the MediaPipe `hands.setOptions({ ... })` call. Its current settings include `maxNumHands: 1`, `modelComplexity: 1`, and minimum detection/tracking confidence values of `0.70`. The interface also offers on-screen controls for drawing behavior.

You can experiment with these values in a local copy and reload the browser. There is no separate build step for this project.

---

## 📁 Project Structure

```text
Hand-Gesture-to-Digital-Art/
├── README.md      # Documentation and local setup
└── index.html     # Styles, application logic, and browser interface
```

---

## ⚡ Performance Notes

MediaPipe processes webcam frames in the browser, while the canvas renders strokes and effects. Tracking performance depends on browser, device, lighting, and camera frame rate. For smoother drawing, try the available in-app stabilization controls and good lighting.

---

## 🔒 Camera Privacy

The application requests webcam access only after the browser prompts for permission. Processing is browser-side using MediaPipe scripts loaded from CDNs. Review third-party CDN dependencies and browser permissions before using it with sensitive camera feeds.

---

## 📜 License

No license file is currently included in this repository. Check with the repository owner before reusing or redistributing code; a badge alone does not grant a software license.
