# Day 34 — Marketing Detective 🕵️

## What I Built
An interactive, gamified web app called **Marketing Detective** — a detective-themed
marketing case study simulator built as a single standalone HTML file (vanilla
JavaScript, no frameworks, no backend).

Players are assigned a randomly selected fictional marketing campaign case,
investigate the evidence (metrics, customer comments, social performance,
channel spend) on a draggable corkboard, examine hidden clues, and then diagnose
the ONE primary marketing mistake that sank the campaign — before receiving a
full "case report" with the correct explanation and suggested improvements.

## Tech Stack
- HTML5, CSS3 (custom corkboard/paper/pin textures, animations, no Tailwind)
- Vanilla JavaScript (no React/build tools — chosen deliberately so the file
  runs reliably standalone, offline, with zero dependencies)
- `localStorage` for persisting player stats (cases closed, accuracy)
- Pointer events for drag-and-drop evidence cards

## Features
- 12 detailed fictional marketing cases across different industries
  (beauty, SaaS, food delivery, fitness tech, travel, gaming, fintech, etc.)
- Randomized case selection on each replay
- Multi-screen game flow: Case Assignment → Investigation Board → Clue
  Examination → Solve → Case Closed animation → Learning Report
- Draggable, pinnable evidence cards on a corkboard UI
- Animated metric bars, typewriter text reveal, stamp-slam "Case Closed" animation
- Multiple-choice mistake diagnosis with distractor options
- Persistent score tracking across sessions

## Key Learnings
1. **Vanilla JS can fully replace a framework for self-contained tools.**
   Since the deliverable had to run as a single offline HTML file, skipping
   React/Babel avoided CDN dependency risk and kept the app 100% reliable.
2. **State-driven rendering without a framework** — building a simple
   `state` object + a single `render()` dispatcher taught me how frameworks
   like React abstract this pattern under the hood.
3. **Pointer events > mouse events** for drag-and-drop — `pointerdown` /
   `pointermove` / `pointerup` with `setPointerCapture` handles both mouse
   and touch input cleanly without extra libraries.
4. **UX pacing matters for engagement** — sequencing reveals (typewriter
   text, clue flip animations, delayed button enabling) created a sense of
   investigation and curiosity instead of dumping all info at once.
5. **Writing realistic case data is its own skill** — each case needed
   metrics and clues that were internally consistent (e.g., high CTR +
   low conversions had to logically point to a funnel-drop-off, not a
   traffic problem) so the "detective" logic actually holds up.

## Screenshots
See `/screenshots` folder for gameplay walkthrough:
1. Intro / Agency screen
2. Case Assignment (folder reveal)
3. Investigation Board (corkboard with evidence)
4. Clue examination
5. Solve screen (multiple choice)
6. Case Closed + Learning Report

## Live File
[`marketing-detective.html`](./marketing-detective.html) — open directly in
any browser, no installation required.




///////////////////////////////////////////////////////////


You are an expert frontend developer, UX designer, instructional designer, and marketing strategist.

Ask the user to choose a color theme from a few presets (including Claude Orange).

Create a beautiful single-file HTML application called 'Marketing Detective'.

Use React via CDN + Babel. However, if React/Babel would prevent the app from running reliably as a standalone local HTML file, automatically switch to an equivalent implementation using pure HTML, CSS and vanilla JavaScript. Do not use Tailwind, npm, backend, APIs, databases, images or external assets.

The application should feel like a polished detective game, not a business dashboard. Every interaction should create curiosity before revealing the next clue.

Generate 10 detailed fictional marketing cases. If output quota allows, expand to 15–20 cases. Store them inside a JavaScript array and randomly load a new case each replay.

Each case must contain:
• Company Name
• Industry
• Campaign Objective
• Target Audience
• Marketing Channels
• Budget Allocation
• Campaign Metrics (Reach, CTR, Engagement, Conversions, Sales)
• Customer Comments
• Social Media Performance
• One Primary Marketing Mistake
• Three Supporting Clues
• Correct Explanation
• Suggested Improvements

User Flow:
1. Case Assignment
2. Investigation Board
3. Interactive Investigation with draggable evidence
4. Solve the Case
5. Case Closed animation
6. Learning Report

Design a premium dark detective aesthetic using corkboards, folders, sticky notes, push pins, paper textures, glowing accents, smooth transitions, hover effects, progress indicators, animated charts, and responsive layout.

Reuse React components wherever possible.

Before returning the final HTML, internally verify there are no syntax or runtime errors and that the application runs correctly as a standalone HTML file.

Return ONLY the complete HTML file.