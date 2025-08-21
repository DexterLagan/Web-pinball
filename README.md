# 🎱 Web Pinball

A browser-based **3D pinball prototype** built with Three.js (WebGL rendering) and Cannon.js (physics).  
Runs entirely in the browser — no plugins, no installs. Just open the demo page on GitHub Pages.

---

## 🚀 Demo

👉 Play on GitHub Pages: https://dexterlagan.github.io/Web-pinball/

(If you see only a magenta screen: give it a few seconds after pushing changes — GitHub Pages can take ~20–30s to propagate.)

---

## 🛠 Features (so far)

- ✅ **3D table** with playfield, walls, pegs (nails), backdrop
- ✅ **Physics** via Cannon.js (ball rolling, bouncing, collisions)
- ✅ **Kinematic flippers** (stable, no jitter) mapped to Shift keys
- ✅ **Plunger**: Space launches from the bottom-right lane, up-table
- ✅ **Nudge**: Space tap (small random impulse) — WIP while plunger is primary
- ✅ **Reset**: R to reset the ball to the launcher lane
- ✅ **Glass cover** collider to keep the ball inside the volume
- ✅ iPad/Safari friendly: robust canvas sizing and local vendored libs

---

## 🎮 Controls

| Key          | Action                                 |
|--------------|----------------------------------------|
| ⇧ Left       | Left flipper up                        |
| ⇧ Right      | Right flipper up                       |
| Space        | Launch ball from plunger lane          |
| R            | Reset ball to launcher lane            |
| (tap Space)  | Small nudge (temporary)                |

---

## 🧩 Project Structure

    Web-pinball/
    │
    ├── index.html                 # main prototype
    ├── vendor/                    # vendored dependencies (local copies)
    │   ├── three.min.js
    │   └── cannon.min.js
    └── README.md

Notes:
- `vendor/` contains local builds of Three.js and Cannon.js because CDNs may be blocked or slow.
- `index.html` hosts the current integrated prototype.

---

## ⚙️ Development

1) **Clone or open in Codespaces**
    
    git clone https://github.com/dexterlagan/Web-pinball.git
    cd Web-pinball

2) **Serve locally**
    
    npx serve .
    
    # Then open:
    # http://localhost:3000

3) **Deploy on GitHub Pages**
- Push to `main`.
- Pages usually refresh within ~20–30 seconds.
- If the browser shows old code, append a cache-buster like `?v=42` to the URL or hard-reload.

---

## 📐 Physics & Scale Notes

- Current abstract playfield: **12 × 20 units** (X × Z), Y is up.
- Ball radius: **0.35** units (diameter ≈ 0.70 units).
- Table is tilted by ~**15–20°** via gravity vector (not by rotating the geometry):
  - Camera at roughly `(0, 16, -14)` looking at `(0, 0, 0)`.
  - “Down-table” (toward the player) corresponds to **−Z** in the current setup.
- Ball mass: **≈ 3.0** (heavier “steel” feel).
- Contact materials:
  - **Ball ↔ Table**: lower restitution (less bounce), low friction (good roll).
  - **Ball ↔ Pegs**: higher restitution (lively deflections).
- A transparent **“glass cover”** is a static plane above the pegs to keep the ball inside.

➡️ Future improvement: convert all dimensions to **meters** (real machine ≈ 129.5 cm × 51.4 cm; ball Ø ≈ 26.99 mm, mass ≈ 80–90 g). Cannon uses SI units, so matching real scale + gravity (9.82 m/s²) will yield more realistic dynamics.

---

## 🧭 Roadmap

- 🎵 Sound effects (flippers, bumpers, glass knock)
- 🧮 Scoring, targets, bumpers, lanes
- 🕹 Proper plunger lane rails (visual + physics guide)
- 📱 Touch controls (tap zones for flippers, swipe to nudge)
- ✨ Visual polish (materials, lighting), optional textures
- 🧰 Level/layout system: JSON-defined peg/bumper placements

---

## 🧯 Troubleshooting

- **Magenta screen** (with or without green border)
  - Usually a JavaScript syntax error or an import path issue.
  - Open DevTools console (on iPad: Safari → Share → “Request Desktop Website” → “Show Web Inspector” or use `alert`/on-page log).
- **Green border only on left/top**
  - Canvas was 0×0 or mis-sized. This repo uses robust iPad-safe sizing (DPR locked to 1, explicit CSS width/height, visualViewport fallback).
- **GitHub Pages shows old code**
  - Add a cache-buster `?v=NN` or force-reload.

---

## 🙌 Credits

- Three.js (r161) — rendering
- Cannon.js — physics
- Built and tested in **Codespaces** on an **iPad Pro (Safari)**

---

## 📄 License

MIT — fork it, learn from it, build your dream table!