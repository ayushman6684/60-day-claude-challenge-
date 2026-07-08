# Day 38 — Typing Speed Studio (Programming Edition)

## What I Built
A premium, single-page **Typing Speed Studio** — a Monkeytype-inspired typing trainer focused on programming practice, built entirely with vanilla HTML, CSS, and JavaScript (no frameworks or libraries).

**Live file:** [`typing-speed-studio.html`](./typing-speed-studio.html)

## Key Features
- **8 typing modes:** Time (15/30/60/120s), Word Count (25/50/100/250), Quote, Programming (9 languages), Custom Text, Adaptive difficulty, Focus mode, and Zen mode
- **Real code snippets** across JavaScript, TypeScript, Python, Java, C++, Go, SQL, HTML, and CSS — at multiple difficulty tiers, not one recycled paragraph
- **IDE-styled editor UI:** line numbers, file tab, live progress bar, animated caret, correct/incorrect character highlighting
- **Live stats:** WPM, Raw WPM, CPM, Accuracy, Elapsed Time, Mistake Count, Streak, Completion %
- **Post-session analytics dashboard:** WPM/accuracy graphs, consistency score, character breakdown (correct/incorrect/extra/missed), keyboard error heatmap, percentile estimate, achievement badges, and a written performance summary
- **Local persistence:** session history, personal bests, and daily streaks — all stored in `localStorage`, no account required
- **Extras:** pause/resume, restart, 4 selectable themes (including a light mode), font size control, WebAudio-generated sound effects, reduced-motion accessibility setting, and keyboard shortcuts (`Tab` restart, `Esc` pause)

## Screenshots
![Screenshot 1](./screenshots/Screenshot%202026-07-08%20111908.png)
![Screenshot 2](./screenshots/Screenshot%202026-07-08%20111930.png)
![Screenshot 3](./screenshots/Screenshot%202026-07-08%20112006.png)

## Key Learnings
- **Accurate WPM math matters more than it looks.** Net WPM (correct chars ÷ 5 ÷ minutes) and Raw WPM (total keystrokes ÷ 5 ÷ minutes) need a time floor to avoid divide-by-near-zero spikes at the very start of a session — otherwise you get nonsense values like thousands of WPM in the first fraction of a second.
- **Hidden-input typing capture** (a visually hidden `<textarea>` that stays focused) is more robust than raw `keydown` listeners — it naturally supports backspace, mobile virtual keyboards, and IME input without extra plumbing.
- **CSS custom properties make multi-theme support painless.** Swapping an entire visual identity (Indigo, Forest, Paper, Terminal) came down to redefining a handful of `--variables` per `[data-theme]` selector instead of duplicating styles.
- **Consistency scoring** (based on the coefficient of variation of WPM samples over time) gives a much more meaningful signal than a raw average — two typists with the same average WPM can have very different rhythm stability.
- **Designing for "no unrealistic values"** required deliberately clamping stats (e.g., capping WPM/CPM display ceilings) rather than trusting the math to always behave, especially around session start/end edge cases.
- **Local-first data storage** (`localStorage`) is enough to deliver a full "track your progress over time" experience without needing a backend or login — good for scoping a project realistically in a single day.

## Next Steps
- Add more languages/snippet variety to the Adaptive mode pool
- Explore exporting session history as CSV/JSON
- Consider a lightweight backend to sync progress across devices



# Typing Speed Studio

You are an expert UI/UX designer, frontend developer, educational game designer, performance engineer, and JavaScript developer.

Before generating anything, ask the user the following questions ONE AT A TIME. Wait for each response before continuing.

1. What kind of typing experience would you like to build?

Examples include General English, Programming, Academic, Business, Medical, Legal, Creative Writing, or an Adaptive version that supports all categories.

If the user chooses the Adaptive version, the generated application should allow users to switch between categories.

2. Would you like Claude to automatically decide the features, or would you like to customize them?

If the user chooses customization, ask which features they would like included.

After collecting the responses, generate a premium single-page interactive HTML application called 'Typing Speed Studio'.

The application should feel like a polished commercial typing platform rather than a basic typing test.

Include multiple typing modes such as Time Mode (15, 30, 60 and 120 seconds), Word Count Mode (25, 50, 100 and 250 words), Quote Mode, Programming Mode (HTML, CSS, JavaScript, Python, Java, C++, SQL and other languages where appropriate), Custom Text Mode, Adaptive Mode that adjusts difficulty based on performance, Focus Mode where only the current line is visible, and Zen Mode for distraction-free untimed practice.

Generate practice passages dynamically according to the selected category. Programming mode should use realistic code snippets, business mode should use professional communication, medical mode should use medical terminology, legal mode should use legal text, creative writing mode should use literature-style passages, and so on. Do not hardcode the same practice paragraph for every mode.

Display live typing statistics including WPM, Raw WPM, CPM, Accuracy, Elapsed Time, Mistake Count, Current Streak, Completion Percentage, Remaining Time or Words, and a real-time progress indicator. Highlight correct characters, incorrect characters, the active cursor position, and completed text with smooth visual feedback.

After every completed session, generate a beautiful analytics dashboard inspired by modern typing platforms such as Monkeytype. Include WPM, Raw WPM, Accuracy, Consistency, Completion Percentage, Characters Typed (Correct, Incorrect, Extra and Missed), Mistake Count, Typing Rhythm, Error Heatmap, WPM Progress Graph, Accuracy Graph, Session Duration, Personal Bests, Percentile Estimate, Achievement Badges, and a detailed performance summary highlighting strengths, weaknesses, commonly mistyped keys, and personalized suggestions for improvement.

Ensure the calculations are accurate and never generate unrealistic values such as 20,000 WPM.

Store session history locally so users can review previous attempts, compare scores, monitor improvement over time, maintain streaks, and track personal records without requiring an account.

Include optional sound effects, keyboard shortcuts, pause and resume functionality, restart options, theme customization, font size controls, dark mode, responsive design, smooth animations, and accessibility features.

Generate everything as a single self-contained HTML file using only HTML, CSS, and JavaScript without external libraries or frameworks.

Design the interface as a premium commercial application with exceptional UI/UX, beautiful typography, modern layouts, polished micro-interactions, smooth transitions, and an experience that feels comparable to the best typing platforms available today.