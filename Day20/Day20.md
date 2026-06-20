# Day 20 — Face Puzzle Game 🧩

## #60DayClaudeChallenge

## What I Built
A fully self-contained, single-file HTML face puzzle game. The app accesses
your webcam, lets you snap a selfie, slices it into a draggable jigsaw puzzle
(3×3, 4×4, or 5×5), and challenges you to reassemble your own face against
the clock.

## Features
- **Live camera capture** with graceful permission-denied / no-camera handling
- **Selectable difficulty**: 3×3, 4×4, or 5×5 grids
- **Guaranteed-solvable shuffle** — any scramble can always be solved
- **Drag-and-drop + touch support** — works on desktop and mobile
- **Visual feedback** — dragging highlight, correct-position green border
- **Live timer (mm:ss.t) and move counter**
- **Win detection** with a results overlay
- **Persistent local leaderboard** (top 5 best times via localStorage)
- **Fully responsive UI**, zero external frameworks

## Tech Stack
- Plain HTML, CSS, and vanilla JavaScript — no frameworks, no build step
- `getUserMedia()` API for webcam access
- `<canvas>` for capturing and cropping the photo
- CSS `background-position` math for slicing the image into tiles
- `localStorage` for the persistent leaderboard

## How It Works
1. Request camera access on load and show a live preview
2. Capture and crop the photo to a square on a hidden canvas
3. Slice the image into N×N tiles using background-position offsets
4. Shuffle tile positions with a Fisher–Yates shuffle (re-rolled if it lands
   on the solved state, since any two tiles can always be swapped)
5. Handle drag/touch events to swap tiles and snap them to the grid
6. Check after every move whether all tiles are correctly placed
7. On win, stop the timer and save the result to the top-5 leaderboard

## Screenshots
![Camera capture](./screenshots/Screenshot%202026-06-20%20173924.png)
![Puzzle in progress](./screenshots/Screenshot%202026-06-20%20193941.png)
![Dragging a tile](./screenshots/Screenshot%202026-06-20%20194011.png)
![Correct placement highlight](./screenshots/Screenshot%202026-06-20%20194032.png)
![Win screen and leaderboard](./screenshots/Screenshot%202026-06-20%20195606.png)

## Key Learnings
- Specifying exact requirements (camera error states, solvability guarantee,
  touch + mouse parity) up front produces complete, production-ready code
  in a single pass — vague prompts lead to vague output.
- A swap-based sliding puzzle (any two tiles can swap, not just adjacent to
  a blank) has no parity constraint, so a simple shuffle is always solvable —
  no need for a complex solvability check.
- Slicing an image purely with CSS `background-size` / `background-position`
  avoids per-tile canvas cropping and keeps the puzzle fast even at 5×5.
- Deploying a static single-file app requires the entry file to be named
  `index.html` for most static hosts (e.g. Netlify Drop) to resolve the
  root URL correctly.

## Live Demo
[Add your deployed link here once hosted]

## Try It
Open `face-puzzle.html` directly in Chrome, Firefox, or Safari. Camera
access requires HTTPS or `localhost`.
You are an expert front-end developer. Build me a complete, fully working face puzzle game as a single self-contained HTML file (no external dependencies except what can load from cdnjs.cloudflare.com, cdn.jsdelivr.net, or unpkg.com).

FEATURES REQUIRED — deliver ALL of these in one complete response:

1. CAMERA ACCESS
   - On load, request webcam permission using getUserMedia()
   - Show a live video preview (front-facing camera preferred)
   - Display a 'Take Photo' button to snapshot the user's face onto a canvas

2. PUZZLE GENERATION
   - After snapshot, let the user choose difficulty: 3×3, 4×4, or 5×5 grid
   - Slice the captured face image into equal puzzle pieces
   - Randomly scramble the pieces (guarantee it is solvable)
   - Render each piece as a draggable tile at its scrambled position

3. DRAG & TOUCH GESTURE CONTROLS
   - Support both mouse drag (desktop) and touch drag (mobile/tablet)
   - When a piece is dropped onto another piece's cell, swap their positions
   - Snap pieces to the nearest grid cell on release
   - Highlight a piece with a coloured border while it is being dragged
   - Show a green border on pieces that land in their correct position

4. TIMER & MOVE COUNTER
   - Start the timer the moment the puzzle begins
   - Display elapsed time live (format: mm:ss.t)
   - Count and display total moves made
   - Show how many pieces are correctly placed out of the total

5. WIN DETECTION & RESULTS SCREEN
   - Detect automatically when all pieces are in the correct position
   - Stop the timer immediately on win
   - Show a results overlay with: final time, total moves, and difficulty
   - Save the top 5 best times to localStorage with date, time, moves, and difficulty
   - Display a leaderboard of saved best times

6. UI & POLISH
   - Clean, modern design
   - Works on desktop and mobile
   - 'Retake Photo' button
   - 'Play Again' button
   - 'New Photo' button
   - Responsive layout

TECHNICAL REQUIREMENTS:
- Single HTML file
- All CSS and JS inline
- No frameworks
- Must work in Chrome, Firefox, and Safari
- Camera must work over HTTPS or localhost
- Handle camera permission denied gracefully
- Do NOT leave placeholder comments

Output the complete HTML file in one code block. Do not truncate or summarise any section.