# 🎮 3D Mini-Games — Flask + Three.js + Bootstrap

A collection of browser-based mini-games combining a **Flask** backend, **Bootstrap 5** UI, and **Three.js** for interactive 3D rendering — all served from a single route with zero external JS/CSS files (everything is inline in `templates/index.html`).

This README covers two games built with the same stack:

1. 🧠 **3D Memory Game** (card-matching)
2. ⭕❌ **3D Tic-Tac-Toe** (2-player & vs Computer)

---

## 📁 Project Structure

```
session2/
├── app.py
└── templates/
    └── index.html
```

> Each game lives in its own `session2/` folder using this identical structure — swap in the relevant `index.html` for the game you want to run.

---

## 🛠️ Tech Stack

| Layer      | Technology              |
|------------|--------------------------|
| Backend    | Flask (Python)           |
| UI / Layout| Bootstrap 5.3.3 (CDN)    |
| 3D Engine  | Three.js r128 (CDN)      |
| Scripting  | Vanilla JS (inline, no external `.js` files) |
| Styling    | Bootstrap utility classes only — **no custom/internal CSS** |

---

## ⚙️ Requirements

- Python 3.8+
- Flask

Install Flask if you don't already have it:

```bash
pip install flask
```

---

## 🚀 Running the Games

1. Navigate into the game's folder:
   ```bash
   cd session2
   ```
2. Run the Flask app:
   ```bash
   python app.py
   ```
3. Open your browser and go to:
   ```
   http://127.0.0.1:5000/
   ```

Debug mode is enabled by default in `app.py`, so the server auto-reloads on file changes.

---

## 🧠 Game 1: 3D Memory Game

A classic card-matching game rendered as a 4×4 grid of flippable 3D cards.

### How to Play
- Click a card to flip it and reveal its symbol.
- Click a second card to try to find a match.
- Matching pairs stay face-up and turn **green**.
- Non-matching pairs flip back after a short delay.
- Match all **8 pairs** in as few moves as possible.

### Key Features
- Cards are `THREE.BoxGeometry` meshes with canvas-drawn textures for front/back faces.
- Smooth eased flip animation (manual tween, no external library).
- Raycasting handles click detection on 3D cards.
- Bootstrap stat cards track **Moves** and **Pairs Found**.
- Win state shown via a Bootstrap success alert.
- "Restart Game" button reshuffles and rebuilds the board.

---

## ⭕❌ Game 2: 3D Tic-Tac-Toe

A 3×3 Tic-Tac-Toe board rendered in 3D, supporting both local 2-player matches and a computer opponent.

### How to Play
- **2 Players:** Take turns — X goes first, then O.
- **Vs Computer:** You play X; the computer (O) moves automatically.
  - **Easy** difficulty — random legal moves.
  - **Unbeatable** difficulty — powered by the **minimax algorithm** (never loses).
- Click an empty cell on the 3D board to place your mark.
- First to align 3 marks (row, column, or diagonal) wins.
- All 9 cells filled with no winner = draw.

### Key Features
- Board cells are flat `BoxGeometry` tiles with raycasting for click detection.
- X marks are two crossed 3D bars; O marks are `TorusGeometry` rings.
- Winning line is highlighted in green.
- Score tracker (X / O / Draw) persists across rounds.
- Mode and difficulty switches use Bootstrap `btn-check` radio groups.
- "Computer is thinking..." indicator during CPU turns for a natural pacing feel.

---

## 🎨 Design Notes

- **No inline or internal `<style>` blocks** — all visual styling comes from Bootstrap utility/component classes (`card`, `btn`, `alert`, `modal`, `navbar`, etc.).
- **No external JS files** — all game logic lives inside a single `<script>` tag in `index.html`.
- **CDN-only dependencies** — Bootstrap and Three.js are loaded via `<link>`/`<script>` tags pointing to public CDNs, so no `static/` folder or build step is required.
- Both games use `THREE.Raycaster` + mouse coordinates to translate 2D clicks into 3D object selection.

---

## 📌 Possible Extensions

- Persist high scores / win tallies using a Flask backend route + database.
- Add sound effects on flip/match or move/win events.
- Add difficulty levels to the Memory Game (6×6 grid, timed mode).
- Add an "impossible-proof" AI trainer mode for Tic-Tac-Toe showing move scores.

---

## 📄 License

Free to use and modify for learning, demos, or personal projects.
