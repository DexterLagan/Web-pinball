# 🤖 AGENTS.md

This file documents the **development history**, **lessons learned**, **precise specifications**, and **visual layout** of the Web Pinball prototype.
It is intended as a **guide for autonomous agents or future developers** (Codex, Copilot, ChatGPT, etc.) who may continue the project.

Current code is consolidated into a single `index.html` entry point; legacy stage HTML files have been removed.

---

## 📜 Development History & Lessons Learned

The project evolved incrementally through several "stages":

1. **Stage 1 – Spinning Cube Test**
   - Verified Three.js rendering worked.
   - Lesson: vendor local copies of libraries.

2. **Stage 2 – Ball + Table + Pegs**
   - Introduced Cannon.js physics, ball, pins.
   - Lesson: CDN imports unreliable → use `vendor/`.

3. **Stage 3 – Integration with Diagnostics**
   - Added boot banners and frame counters.
   - Lesson: GitHub Pages caching requires `?v=XX`.

4. **Stage 4 – Flippers & Controls**
   - First hinge-joint attempt failed (vibration, wrong pivot).
   - Solution: kinematic flippers (direct rotation).
   - Lesson: Flippers must be **kinematic**.

5. **Controls**
   - ⇧ Left → left flipper
   - ⇧ Right → right flipper
   - Space → plunger
   - R → reset

6. **Scaling & Canvas**
   - iPad Safari required manual sizing.
   - Lesson: Use `visualViewport`, lock DPR=1.

7. **Ball Physics**
   - Needed heavier mass and tilted table.
   - Lesson: model steel ball with realistic mass.

8. **Consolidation**
   - Merged stage prototypes into a single `index.html`.
   - Simplified the project to one entry point.

---

## 📐 Current Specifications

### Table Geometry
- Playfield: **12 units (X) × 20 units (Z)**
- Incline: gravity tilted ~15–20°
- Walls: 4 rectangular frames
- Backdrop: covers base so ball doesn’t fall through
- Glass cover: transparent plane ~1.5 units above playfield

### Ball
- Radius: **0.35 units**
- Mass: **3.0**
- Restitution: 0.3
- Friction: 0.05

### Flippers
- Kinematic bodies
- Rest angle: −35° (downward, toward player)
- Active angle: 0° (flat)
- Gap between flippers: ~0.7 units (2× ball diameter)

### Pegs
- Radius 0.2, height 0.5
- Restitution 0.6–0.8

### Plunger
- Bottom-right of table
- Launches ball up the right-side lane
- Impulse applied along +Z (up-table)

### Camera
- Position `(0,16,-14)`
- Target `(0,0,0)`
- Perspective ~45°

---

## 🎨 ASCII Layout

### Top-Down Schematic (playfield view)

```
 -------------------------------------------------
|                                                 |
|    o     o      o      o      o      o      o   |
|                                                 |
|       o       o       o       o       o         |
|                                                 |
|    o     o      o      o      o      o      o   |
|                                                 |
|                 (ball path)                     |
|                                                 |
|                    ||                           |
|                    ||                           |
| Left flipper   ___/  \___   Right flipper       |
|               /          \                      |
|              /            \                     |
|                                                 |
| Plunger lane (ball start)   [O]                 |
| (bottom-right vertical lane) ↑                  |
|                             Space = launch      |
 -------------------------------------------------
```

Legend:  
- `o` = peg  
- `[O]` = ball in plunger  
- Flippers angled downward at rest  
- Ball travels upward from right-side plunger lane  

---

## 🔧 Known Issues

- Plunger lane not yet visually modeled.
- Glass cover is a single plane, needs bounding box.
- Flipper visuals are abstract, pivoting without base hardware.

---

## 🧭 Improvements & Next Steps

1. Add proper plunger lane (guides/rails).
2. Glass cover as a full bounding box.
3. Real-world scaling (m → units).
4. Ramps, bumpers, scoring.
5. Sound effects.
6. Touchscreen controls (tap = flipper).

---

## 🧯 Debugging Conventions

- Always print `BUILD: bXX | PHASE: Y` on boot.
- Use `?v=NN` query to force GitHub Pages refresh.
- Entry point is `index.html`; legacy stage demos have been removed.

---

## 🙌 Credits

- Rendering: Three.js (r161)  
- Physics: Cannon.js  
- Environment: GitHub Codespaces on iPad Pro (Safari)  
- Debugging: floating HTML console overlay

---
