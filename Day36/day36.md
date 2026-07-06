# Day 36 – Cognitive Pattern Explorer

## 🎯 Objective
Build a single-file, offline-capable web app — **Cognitive Pattern Explorer** — using only HTML, CSS, and vanilla JavaScript. The app is a psychology-inspired, self-reflection experience that explores personal thinking tendencies through calm, game-like interactive scenarios (not a clinical test).

## 🧩 What the App Does
- **Start Screen** – choose Calm or Quick (stress) mode, setting the pace of the experience.
- **Chapter 1 – Discover Your Thinking Style** – answer short scenario-based questions.
- **Chapter 2 – Choose Your Priorities** – rank cards using drag-and-drop.
- **Chapter 3 – Map Your Thinking** – arrange a timeline of thought patterns using drag-and-drop.
- **Final Reflection Journal** – a personalized, percentage-based breakdown across five thinking tendencies (Analytical Thinker, Emotional Intuitive, Overthinking Loop Style, Action-First Decision Maker, Balanced Reflective Thinker), shown with an animated bar chart and a constellation-style diagram, plus a save-to-device journal note.

## 🛠️ Tech Stack
- Pure **HTML5**, **CSS3**, and **vanilla JavaScript** (no frameworks/libraries).
- Native **Pointer Events** used to build one reusable drag-and-drop component that works across mouse, touch, and keyboard (Arrow Up/Down) input.
- All scenario/question/card data stored as plain JavaScript objects — easy to extend or edit.
- Fully offline — no external requests, no CDN dependencies, works by just opening the `.html` file in a browser.

## 📸 Screenshots

![Screenshot 1](./Screenshot%202026-07-06%20130911.png)
*Start screen with Calm / Quick mode selection.*

![Screenshot 2](./Screenshot%202026-07-06%20130942.png)
*Chapter 1 – scenario question in progress.*

![Screenshot 3](./Screenshot%202026-07-06%20131028.png)
*Chapter 2 – draggable priority ranking cards.*

![Screenshot 4](./Screenshot%202026-07-06%20131915.png)
*Chapter 3 – draggable thinking timeline.*

![Screenshot 5](./Screenshot%202026-07-06%20131938.png)
*Final reflection – percentage breakdown and constellation diagram.*

![Screenshot 6](./Screenshot%202026-07-06%20134227.png)
*Additional view of the completed app / file properties.*

## 📂 Files in This Folder
- `cognitive-pattern-explorer.html` – the complete, single-file working app.
- `day36.md` – this write-up.
- Screenshots (`.png`) documenting each stage of the app.

## 💡 Key Learnings
- **Single-file architecture**: Learned how to structure a full interactive app — markup, styling, and logic — inside one `.html` file while keeping the code organized and readable using clear section comments.
- **Reusable components**: Built one generic `createReorderList()` drag-and-drop function and reused it for both the priority-ranking chapter and the timeline-mapping chapter, instead of duplicating logic.
- **Pointer Events over separate touch/mouse handlers**: Using the Pointer Events API (`pointerdown`, `pointermove`, `pointerup`) unified mouse, touch, and pen input in a single code path, removing the need for separate touch-specific fallback code.
- **Accessibility matters from the start**: Added keyboard reordering (Arrow Up/Down), `aria-live` regions for screen-reader announcements, visible focus states, and `prefers-reduced-motion` support — accessibility is far easier to bake in early than retrofit later.
- **State management without a framework**: Managed multi-step flow (chapters, question index, drag order, scores) using plain JavaScript objects and small pure functions, which reinforced how much structure vanilla JS can hold without needing React or similar.
- **Responsible design language**: Practiced writing reflective, non-diagnostic copy ("you often...", "this suggests...") to keep a psychology-themed tool educational and non-clinical.
- **Git/GitHub workflow**: Practiced organizing daily project work into dated folders (`Day36`) and pushing them from VS Code using `git add`, `git commit`, and `git push`.

## ✅ Status
Completed and verified — app works offline, drag-and-drop and scoring function correctly, layout is responsive, and no console/syntax errors were found.





Create a single-file offline web app called 'Cognitive Pattern Explorer' using only HTML, CSS, and vanilla JavaScript (no frameworks). Combine HTML, CSS, and JS into one responsive file.

Purpose:
Build a psychology-inspired self-reflection experience that explores thinking patterns through interactive scenarios. It must feel calm, game-like, and exploratory rather than like a test.

This is educational only. Never diagnose or clinically assess mental health. Use reflective language ('you often...', 'this suggests...') instead of absolute labels.

Thinking Tendencies:
- Analytical Thinker
- Emotional Intuitive
- Overthinking Loop Style
- Action-First Decision Maker
- Balanced Reflective Thinker

Flow:
1. Start Screen with Calm/Stress Mode.
2. Chapter 1 – Discover Your Thinking Style.
3. Chapter 2 – Choose Your Priorities using draggable cards.
4. Chapter 3 – Map Your Thinking using draggable timelines.
5. Final Reflection Journal with personalized insights and percentage breakdown.

Design:
- Calm modern aesthetic.
- Smooth transitions.
- Progress indicators.
- Responsive layout.
- Ambient animations.
- Keyboard accessibility.
- Reduced motion support.

Technical Requirements:
- Single HTML file.
- Vanilla JavaScript only.
- Native drag-and-drop with touch fallback.
- Works completely offline.
- Store all scenarios as JavaScript objects.
- Reuse drag-and-drop components.
- Verify there are no syntax errors, scoring works, progress tracking works, and the layout is responsive.

Return only one complete HTML file.

