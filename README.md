# GESTURAL — 3D Model Controller

> Control 3D models with your bare hands using real-time gesture recognition.

**[Try Out →](https://sparkscratch-p.github.io/gestural/)**

---

## What is Gestural?

**Gestural** is a browser-based 3D model viewer that lets you rotate, pan, zoom, and roll any GLB/GLTF model using only hand gestures captured through your webcam — no mouse, no touch, no controller.

It uses **MediaPipe Hands** for real-time landmark tracking and **Three.js** for 3D rendering, packaged entirely as a single HTML file with zero build steps.

---

## Features

- **5 distinct hand gestures** mapped to 3D transform actions
- **Drag-and-drop GLB/GLTF loading** — drop any model directly onto the canvas
- **Multi-model support** — load and switch between multiple models in a session
- **Adjustable sensitivity** — per-axis sliders for rotate, pan, and zoom
- **Smoothing toggle** — interpolated gesture application for fluid motion
- **Wireframe mode** — toggle wireframe rendering on the active model
- **Axes gizmo** — live orientation indicator in the viewport corner
- **Live camera preview** — mirrored feed with hand skeleton overlay in the sidebar
- **Gesture highlighting** — active gesture cards illuminate in real time
- **Keyboard shortcuts** — quick access to reset, camera, wireframe, fullscreen
- **Toast notifications** — feedback for every major action
- **Dark, focused UI** — custom cursor, ambient glow, grid overlay, Syne + DM Mono typography

---

## Gesture Reference

| Gesture | Hand Shape | Action |
|---|---|---|
| ✋ **Roll** | Open palm (4+ fingers extended) | Rotate model — slide left/right → Y axis, slide up/down → X axis |
| ✌️ **Pan** | Two fingers extended | Pan the camera — strong lateral movement |
| ☝️ **Zoom** | One finger extended (index) | Zoom in/out — move finger up/down |
| 🤙 **Z-Roll** | Pinch (thumb + index touching) | Roll model along Z axis by rotating the pinch angle |
| 👊 **Depth Zoom** | Closed fist | Zoom based on wrist depth (Z-axis proximity) |

---

## Self-Hosting

Since the entire app is a single file, self-hosting is trivial:

```bash
git clone https://github.com/SparkScratch-P/gestural.git
cd gestural
# Serve with any static server, e.g.:
npx serve .
# or
python3 -m http.server 8080
```

Then open `http://localhost:8080` in your browser.

> **Note:** Camera access requires a secure context (`https://` or `localhost`). Serving over plain `http://` on a non-localhost address will block webcam access.

---

## UI Layout

The interface is split into three zones: a **left toolbar**, a **central 3D viewport**, and a **right panel**.

---

## Left Toolbar

The vertical toolbar on the left edge gives quick access to the primary viewport controls:

| Icon | Button | Shortcut | Description |
|---|---|---|---|
| 🔄 | **Rotate Mode** | — | Sets the active mouse/orbit mode to rotate (default active state) |
| ✥ | **Pan Mode** | — | Sets the active mouse/orbit mode to pan |
| 🔍 | **Zoom Mode** | — | Sets the active mouse/orbit mode to zoom |
| ↩ | **Reset View** | `R` | Resets the model's position, rotation, and camera to defaults |
| △ | **Wireframe Toggle** | `W` | Switches the active model between solid and wireframe rendering |
| ⛶ | **Fullscreen** | `F` | Enters or exits fullscreen mode |

The three mode buttons (Rotate / Pan / Zoom) are mutually exclusive — the active one is highlighted with a cyan glow. These control how mouse/trackpad interaction behaves in the viewport alongside hand gestures.

---

## Right Panel

The collapsible right panel contains all session controls and live feedback, organized into five sections:

### Camera Feed
A mirrored live preview of your webcam feed. When hand tracking is active, a color-coded hand skeleton is drawn directly on the preview. The skeleton color changes per gesture type (cyan = rotate, green = pan, amber = zoom, purple = Z-roll, red = depth). An **Enable / Disable Camera** button toggles webcam access.

### Loaded Models
Lists all GLB/GLTF files loaded in the current session. Click any entry to switch the active model. A remove (×) button appears on each item to unload it. A **Load GLB / GLTF** button opens the file picker for additional models.

### Gestures
A live gesture reference card strip. Each card shows the hand emoji, shape description, and mapped action. The card for the gesture currently being detected highlights in real time with a cyan border and glow — useful for learning or debugging tracking.

### Sensitivity
Four independent range sliders (0.1 – 3.0, default 1.0) to tune gesture responsiveness per action:

| Slider | Controls |
|---|---|
| **Rotate** | Speed of open-palm slide → model rotation |
| **Pan** | Speed of two-finger slide → camera translation |
| **Zoom** | Speed of index-finger movement → zoom |
| **Depth Zoom** | Speed of fist depth movement → zoom |

### Settings
Four toggle switches for behavior preferences:

| Toggle | Default | Description |
|---|---|---|
| **Auto-rotate when idle** | Off | Slowly spins the model when no gesture is detected |
| **Show hand skeleton** | On | Draws the 21-landmark hand overlay on the camera preview |
| **Smooth gestures** | On | Interpolates gesture deltas for fluid, lag-free motion |
| **Right hand only** | On | Ignores the left hand to prevent accidental input |

---

## Status Bar

The header displays three live status pills — **Camera**, **Hand**, and **Model** — each with a pulsing dot that turns green when active. The footer shows real-time readouts of the current rotation (X/Y/Z), camera distance, and an active-gesture value bar.

---

## Keyboard Shortcuts

| Key | Action |
|---|---|
| `C` | Toggle camera on / off |
| `R` | Reset model position and rotation |
| `W` | Toggle wireframe mode |
| `F` | Toggle fullscreen |

---

## Tech Stack

| Library | Version | Purpose |
|---|---|---|
| [Three.js](https://threejs.org/) | r128 | 3D rendering, GLTFLoader, OrbitControls |
| [MediaPipe Hands](https://google.github.io/mediapipe/solutions/hands) | latest | Real-time hand landmark detection |
| [Syne](https://fonts.google.com/specimen/Syne) + [DM Mono](https://fonts.google.com/specimen/DM+Mono) | — | Typography |

No bundler, no framework, no npm install — everything loads from CDN.

---

## Browser Compatibility

| Browser | Support |
|---|---|
| Chrome 90+ | ✅ Recommended |
| Edge 90+ | ✅ Supported |
| Firefox | ⚠️ MediaPipe may have reduced performance |
| Safari | ❌ WebRTC limitations |

Requires a webcam and WebGL support.

---

## License

Licensed under the **GNU General Public License v3.0**. See [LICENSE](./LICENSE) for details.

---

## Author

Made by [SparkScratch-P](https://github.com/SparkScratch-P)
