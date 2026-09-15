# REAL-TIME PHONK WEBCAM EDIT

A live, browser-powered video workstation that turns real-time webcam reactions into viral Phonk edits. By combining client-side computer vision with beat-synchronized canvas rendering, this app detects everyday physical gestures—like taking a sip of coffee or touching your glasses—and immediately cuts into an aggressive, audio-reactive edit with 808 sub-bass drops, glitch effects, and slow-motion replays.

---

### 🌟 Original Creator Credit

> **Original Concept & Project Credit:** **[Amit Sikdar (@amitsikdar37)](https://github.com/amitsikdar37)**  
> Sincere credit goes to Amit Sikdar for pioneering the original concept and creative direction behind this idea. Visit his GitHub at [github.com/amitsikdar37](https://github.com/amitsikdar37).

---

## ⚡ What is REAL-TIME PHONK WEBCAM EDIT?

Most video editors require recording raw footage first, importing it into timeline software, chopping clips, and aligning beat drops manually. 

**REAL-TIME PHONK WEBCAM EDIT** eliminates that entire post-production pipeline:
1. It continuously watches your webcam stream through an on-device machine learning pipeline.
2. It maintains a high-frequency rolling memory buffer of incoming video frames.
3. When you perform a signature gesture (or hit the manual hotkey), the app instantly isolates your action, locks onto your face, and renders a synchronized Phonk video edit directly inside an interactive Picture-in-Picture display.
4. You can preview the generated clip and download it immediately as a ready-to-post **MP4** video.

Everything executes **100% locally in your browser**—no servers, no subscriptions, and complete camera privacy.

---

## 🚀 Core Features

### 👁️ On-Device Vision & Gesture Recognition
* **MediaPipe Face & Hand Landmarkers**: Uses `@mediapipe/tasks-vision` running on WebAssembly/WebGL to map facial landmarks and dual-hand positions in real time.
* **Intelligent Action Triggers**:
  * **Drink Sip Detection**: Monitors hand proximity to the mouth coordinates and triggers when a drink is lifted to take a sip.
  * **Glasses Adjustment**: Detects finger gestures reaching towards eye frames and temple points.
  * **Dual Trigger Mode**: Reacts to either gesture automatically.
* **Instant Manual Firing**: Hit <kbd>Space</kbd> or click the trigger button anytime to force the drop manually.

### 📐 3D Tactical Wireframe HUD
* **Real-time Euler Angles**: Calculates facial **Pitch**, **Yaw**, and **Roll** directly from vision transformation matrices.
* **Perspective 3D Projection**: Renders a mathematical 3D wireframe cube surrounding your head that dynamically rotates and shifts perspective as you move.
* **Futuristic Overlay**: Cyberpunk tactical timecode, dynamic framerate counter, and audio monitor diagnostics.

### 🎵 Precision Audio Engine & Visual Presets
* **Audio-Clock Synchronization**: Driven by the Web Audio API to ensure visual impact frames hit at the exact millisecond of the 808 bass kick.
* **Curated Edit Presets**:
  * **Ghost Trail Impact** (*Montagem Tomada*): Layered ghost trails, dynamic chromatic aberration, and sub-bass vibration shakes.
  * **Sigma Hard Snaps** (*Marlon Gets Mogged*): Dramatic slow-motion time freeze, targeted eye zoom, and heavy bass drop.
  * **Parallax Dual Speed** (*Montagem Tomada*): Layered speed-ramping stutters with cinematic scaling.
  * **Dark Manga Strobe** (*Mogger*): High-contrast monochrome inverted colors with rapid strobe transitions.
* **Interactive Soundboard**: Trigger iconic meme voice lines and sound effects on demand.

### 📼 Instant In-Browser MP4 Export
* **WASM-Powered Encoding**: Uses `mediabunny` and `@mediabunny/aac-encoder` to mux canvas video and Web Audio streams into universal `.mp4` format directly within the client.
* **Zero Server Latency**: Clips are ready to download immediately after playback ends.

---

## 🛠️ Technology Stack

| Layer | Technologies |
| :--- | :--- |
| **Framework & Core** | React 18, TypeScript, Vite |
| **Styling & HUD** | Vanilla CSS, Tailwind CSS, Google Fonts (*Orbitron*, *Share Tech Mono*, *Bebas Neue*) |
| **Machine Learning** | Google MediaPipe Vision Tasks (WASM & GPU delegates) |
| **Canvas & Graphics** | HTML5 Canvas 2D with 3D projection math (Euler rotation matrix) |
| **Audio Processing** | Web Audio API (AudioContext, GainNode, MediaStreamDestination) |
| **Video Transcoding** | Mediabunny, AAC WebAssembly Encoder |
| **Icons & Visuals** | Lucide React, Canvas Confetti |

---

## 📦 Getting Started

### Prerequisites
* **Node.js** (v18 or newer recommended)
* **npm**, **yarn**, or **pnpm**
* A functional webcam connected to your device

### Setup & Run

1. **Clone the repository:**
   ```bash
   git clone https://github.com/AadishY/real-time-phonk-webcam-edit.git
   cd real-time-phonk-webcam-edit
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Start the local development server:**
   ```bash
   npm run dev
   ```

4. **Access the application:**
   Open your browser and visit `http://localhost:5173`. When prompted, grant access to your camera.

> **Note**: Web browsers require HTTPS or `localhost` to allow camera stream access.

---

## 🎮 Controls & Shortcuts

| Action | Control | Description |
| :--- | :--- | :--- |
| **Force Trigger** | <kbd>Space</kbd> or ⚡ Button | Instantly initiates edit capture and playback |
| **Drink Trigger** | ☕ Sip drink | Automatic trigger upon drinking movement |
| **Glasses Trigger** | 👓 Adjust glasses | Automatic trigger upon touching eyewear area |
| **Switch Camera** | 📷 Camera button | Cycles through available webcams/cameras |
| **Toggle Mirror** | ↔️ Flip button | Mirrors or unmirrors the video canvas |
| **Audio Toggle** | 🔊 Speaker button | Mutes or unmutes soundtrack and sound effects |
| **Soundboard** | 🎵 Music button | Opens soundboard with tracks and meme voice lines |
| **Sensitivity** | 🎚️ Slider | Adjusts gesture sensitivity threshold (0.5x – 1.5x) |
| **Export Clip** | ⬇️ Download button | Saves rendered edit as an `.mp4` video |

---

## 🧠 System Architecture

```
                                  [ Webcam Video Stream ]
                                             │
                      ┌──────────────────────┴──────────────────────┐
                      ▼                                             ▼
            [ MediaPipe Vision ]                           [ Rolling Frame Buffer ]
       - 3D Face Landmarker (Euler)                   - Sliding 7.5s ImageBitmap cache
       - Dual Hand Landmarker (Fingers)               - High-frequency capture loop
                      │                                             │
                      ▼                                             │
         [ Gesture Trigger Logic ]                                  │
    (Sip / Glasses / Spacebar Override)                             │
                      │                                             │
                      └──────────────────────┬──────────────────────┘
                                             ▼
                              [ Sigma Edit Rendering Engine ]
                                - Audio-clock synchronized beats
                                - 3D wireframe face projection
                                - Chromatic split & ghost trails
                                - Slow-mo & zoom effects
                                             │
                      ┌──────────────────────┴──────────────────────┐
                      ▼                                             ▼
              [ Canvas Display ]                           [ Mediabunny WASM ]
             Picture-in-Picture                              AAC + MP4 Muxer
              Real-time Playback                                    │
                                                                    ▼
                                                            [ Downloadable MP4 ]
```

---

## 🛡️ Privacy & Performance

* **100% Private**: Your webcam stream and microphone input never leave your local machine. All computer vision and video processing operate entirely in-browser.
* **Hardware Accelerated**: Automatically leverages WebGL and GPU acceleration when available, with built-in CPU fallbacks.

---

## 📄 License & Attribution

* **Original Idea & Work**: Created by **[amitsikdar37](https://github.com/amitsikdar37)**.
* **Repository**: **[AadishY/real-time-phonk-webcam-edit](https://github.com/AadishY/real-time-phonk-webcam-edit)**.
* Licensed under the MIT License.
