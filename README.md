# ARFF Vehicle Explorer

Single-file WebGL / WebXR diagnostic application for inspecting and interacting with modular Aircraft Rescue and Firefighting (ARFF) vehicle assemblies in standard desktop browsers and Meta Quest Passthrough (Mixed Reality).

---

## Overview

The application visualizes an Oshkosh Striker ARFF vehicle split into discrete subsystems. It provides an exploded-view animation engine, technical specifications inspector, bi-directional audio narration via the Web Speech API, and immersive hand-tracking interactions in WebXR AR mode.

### Subsystems Tracked

| Subsystem | Part Number | Flow Spec | Standard | Explosion Vector |
| :--- | :--- | :--- | :--- | :--- |
| **Main Chassis** | `STK-001` | N/A | NFPA 414 | `[0, 0, 0]` |
| **Bumper Monitor** | `BM-002` | 300 GPM | CAP 168 | `[0, 0, 1.5]` |
| **Under-truck Deluge** | `DS-003` | 50 GPM | CAP 168 | `[0, -1.0, 0]` |
| **High Reach Extendable Turret (HRET)** | `HR-004` | 1000 GPM | FAA / ICAO | `[0, 2.0, 0]` |
| **Preconnected Hose Reel** | `HS-005` | 125 GPM | NFPA 1961 | `[-1.5, 0, 0]` |

---

## Core Capabilities

- **Zero-Dependency Runtime:** Delivered entirely within an offline-capable, single-file HTML layout via standard ES importmaps (`three@0.160.0`).
- **Progressive Asset Tracking:** Preloader gate calculates discrete asset streaming percentages and enables execution modes once Draco-compressed assets hydrate.
- **Exploded View Engine:** Linear displacement along component-relative normal vectors, operable through a UI slider, control buttons, or two-handed expansion gestures in XR.
- **Dynamic 2D/3D Projection Overlays:** Screen-space leader lines drawn onto an HTML5 canvas layer track 3D object anchor coordinates to desktop HUD badges in real time.
- **WebXR Passthrough & Ergonomics:**
  - Configured for `immersive-ar` sessions using `local-floor`.
  - Floating 3D canvas control panels spawn at waist level (0.95 m height, 50 cm forward displacement).
  - Component information cards render directly on 3D textures in the user's field of view.
- **Direct Hand Manipulation:** Native Pinch (`index-finger-tip` to `thumb-tip`) and two-finger raise gestures allow users to grab, reposition, and explode assemblies without physical controllers.

---

## File Structure

All 3D assets must sit in the root directory relative to `index.html`:

```text
.
├── index.html
├── intro.mp4              # Ambient splash loop
├── Striker.glb            # Main chassis module
├── BumperMonitor.glb      # Front turret assembly
├── DelugeSystem.glb       # Deluge manifold
├── HRET.glb               # Snozzle boom and piercing nozzle
└── Hose.glb               # Preconnected hose reel unit
```

---

## Technical Stack

- **Graphics Core:** [Three.js r160](https://threejs.org/) via ESM.
- **Mesh Compression:** Google Draco via `DRACOLoader`.
- **XR Extensions:** `three/addons/webxr/XRHandModelFactory.js`.
- **Typography & UI:** Native CSS glassmorphism, responsive viewports, system monospaced stacks.
- **Speech Synthesis:** Web Speech API (`en-GB` voice synthesis).

---

## Development & Local Execution

Browsers restrict WebXR and Web Workers (`DRACOLoader`) when loaded via `file://`. The project must be served over `localhost` or a secure `https://` origin.

### Local Server via Python

```bash
# Python 3
python -m http.server 8080
```

### Local Server via Node.js

```bash
# Using npx serve
npx serve .
```

Navigate to `http://localhost:8080` or `https://<local-ip>:8080` on client hardware.

---

## Deployment & Quest Testing

To run Passthrough mode on a **Meta Quest 3 / Quest 3S / Quest Pro**:

1. Host the project directory on an HTTPS-enabled server (e.g., GitHub Pages, Cloudflare Pages, or local HTTPS via `mkcert`).
2. Open **Meta Quest Browser**.
3. Access the deployed HTTPS URL.
4. Allow camera/spatial permissions when prompted.
5. Once all `.glb` assets indicate `OK`, select **ENTER PASSTHROUGH**.

---

## License

Proprietary — Entoli XR. Created for technical training simulation and emergency response visualization.
