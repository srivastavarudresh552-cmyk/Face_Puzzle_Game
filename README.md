# 🧩 Face Puzzle Game

Take a selfie with your webcam, slice it into a sliding puzzle, and race the clock to put your face back together. Built as a single self-contained HTML file — no build step, no backend, no dependencies.

## ✨ Features

- **Live webcam capture** — requests camera permission, shows a mirrored live preview, and snaps a square photo on demand
- **Adjustable difficulty** — 3×3, 4×4, or 5×5 puzzle grids
- **Drag & touch controls** — built on the Pointer Events API, so mouse drag and touch drag work identically on desktop, tablet, and mobile
- **Visual feedback** — a colored border while dragging a piece, a green border when a piece lands correctly
- **Live timer & move counter** — `mm:ss.t` precision timer plus a running tally of swaps and correctly placed pieces
- **Automatic win detection** — the puzzle checks itself; no "I'm done" button needed
- **Persistent leaderboard** — top 5 best times saved to `localStorage` with date, time, moves, and difficulty
- **Fully responsive** — works on phones, tablets, and desktop browsers
- **Zero dependencies** — pure HTML, CSS, and JavaScript in one file

## 🚀 Getting Started

Camera access requires a **secure context** — either `https://` or `localhost`. Opening the file directly via `file://` will not work in most browsers.

### Option 1 — Local server (recommended)

```bash
git clone https://github.com/your-username/face-puzzle-game.git
cd face-puzzle-game

# any static server works, for example:
python3 -m http.server 8000
# or
npx serve .
```

Then open `http://localhost:8000` in your browser.

### Option 2 — Deploy it

Drop `index.html` into any static host (GitHub Pages, Netlify, Vercel, Cloudflare Pages) — it just needs to be served over HTTPS.

## 🎮 How to Play

1. **Allow camera access** when prompted and frame your face in the preview
2. Click **📸 Take Photo** to capture a snapshot
3. Pick a difficulty — **3×3**, **4×4**, or **5×5**
4. Click **▶ Start Puzzle** — the timer starts immediately
5. **Drag pieces** (mouse or touch) to swap them into the correct cell
6. Solve the puzzle to trigger the **win screen**, see your stats, and check the leaderboard
7. Use **🔁 Play Again** to reshuffle the same photo, or **📷 New Photo** to start over

## 🛠 How It Works

- **Capture**: the live `<video>` stream is drawn onto a `<canvas>`, cropped to a centered square, and mirrored to match the selfie preview
- **Slicing**: rather than cutting separate image files, each puzzle piece is a `<div>` with `background-size: N*100%` and a `background-position` percentage offset — a responsive CSS trick that re-slices automatically at any screen size, with no JavaScript recalculation needed
- **Scrambling**: pieces are assigned a random permutation of grid positions (Fisher–Yates shuffle), re-rolled if it's too close to solved. Because any two pieces can be swapped directly via drag-and-drop, every permutation is solvable — there's no 15-puzzle parity constraint to worry about
- **Dragging**: a single set of Pointer Event handlers (`pointerdown` / `pointermove` / `pointerup`) drives both mouse and touch input, with `touch-action: none` to prevent scroll interference on mobile
- **Win detection**: after every swap, each piece's current position is compared to its correct position; when all match, the timer stops and the results overlay appears

## 🌐 Browser Support

| Browser | Support |
|---|---|
| Chrome / Edge (desktop & mobile) | ✅ |
| Firefox (desktop & mobile) | ✅ |
| Safari (macOS & iOS 13+) | ✅ |

Camera permission errors (denied, no device found, device in use, unsupported browser) are caught and shown with a clear message and a **🔄 Retry Camera** button.

## 🔒 Privacy

Everything happens **entirely in your browser**:

- The webcam feed and captured photo never leave your device — there is no server, no upload, no analytics
- The only persisted data is your leaderboard (best times, moves, difficulty, date), stored locally via `localStorage`
- Closing the tab or clearing site data removes everything

## 📁 Project Structure

```
face-puzzle-game/
└──index.html   # everything — HTML, CSS, and JS in one file
```

## 📄 License

MIT — do whatever you'd like with it.

## 🙌 Contributing

Issues and pull requests are welcome. Since it's a single file, most changes are easy to review — feel free to open a PR for new features (timed challenges, multiplayer race, custom piece shapes, etc.).
