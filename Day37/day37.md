# Day 37 – Task Compass: Building an Interactive Learning Game

## What I Built
Today I designed and built **Task Compass**, a single-file HTML/CSS/JavaScript management-simulation game that teaches how work actually flows through a tech organization — ownership, delegation, collaboration, and escalation — rather than testing job titles.

The game has three stages:
1. **Who Owns This?** – match a workplace task to its primary owner
2. **Task Routing** – build the correct sequence a task travels through a team
3. **Collaboration Challenge** – assemble up to 4 roles for complex, cross-team problems

At the end, it generates a radar chart across four categories (Ownership, Delegation, Collaboration, Workflow Thinking) and a personalized written reflection.

## Key Learnings
- **State management without a framework**: structured the whole game (9 questions across 3 stages, scores, counters) using a single plain JS state object instead of React/Vue — good practice for thinking in vanilla state machines.
- **Drag-and-drop that actually works everywhere**: combined native HTML5 drag events (`dragstart`/`dragover`/`drop`) with a click-to-place fallback so the game works on both desktop and touch devices without any library.
- **SVG generated entirely in JS**: built a radar/spider chart from scratch by calculating polygon points with trigonometry (`Math.cos`/`Math.sin`) instead of relying on a charting library.
- **Design restraint**: used CSS custom properties (`--chip-color`) to theme role chips per department, and a signature "ticket stub" visual (dashed divider + circular notches) to make task cards feel authentic rather than generic quiz cards.
- **Scoring as feedback, not judgment**: instead of "correct/incorrect," the app explains *why* a role owns a task and tracks softer patterns (over-assigning responsibility, under-estimating collaboration) to generate a personalized reflection.
- **Offline-first constraint**: everything — fonts, animations, audio (Web Audio API beeps), confetti — had to work with zero external dependencies or CDNs, which forced creative use of system fonts and native browser APIs.

## Screenshots
![Screenshot 1](./Screenshot%202026-07-07%20064224.png)
![Screenshot 2](./Screenshot%202026-07-07%20064551.png)
![Screenshot 3](./Screenshot%202026-07-07%20064732.png)
![Screenshot 4](./Screenshot%202026-07-07%20064905.png)
![Screenshot 5](./Screenshot%202026-07-07%20065028.png)
![Screenshot 6](./Screenshot%202026-07-07%20065605.png)
![Screenshot 7](./Screenshot%202026-07-07%20065922.png)
![Screenshot 8](./Screenshot%202026-07-07%20070505.png)
![Screenshot 9](./Screenshot%202026-07-07%20070713.png)

## Files
- [`task_compass.html`](./task_compass.html) – the full playable game



You are an expert educational game designer, UI/UX designer, organizational consultant and frontend developer.

Before generating anything, ask the user ONE question:

"What type of workplace would you like to explore?"

Options: Tech Company, Startup, Corporate Office, Café / Restaurant, Retail Business, Hospital / Healthcare, School / University, Manufacturing, Media / Creative Agency, Freelancer / Small Business, Other (one sentence).

Wait for the user's answer.

Then generate a beautiful single-file HTML application called: Task Compass

Subtitle:
Learn how work flows through real organizations.

IMPORTANT

Generate ONLY one self-contained HTML file.

Use only: HTML, CSS, Vanilla JavaScript.

Do NOT use: React, Tailwind, npm, Babel, external libraries or APIs.

Everything must work completely offline.

Internally verify there are no syntax or runtime errors before returning the code.

OBJECTIVE

The goal is NOT to test job titles.

The goal is to teach: ownership, delegation, collaboration, escalation and how work moves through organizations.

The experience should feel like a management simulation rather than a quiz.

GAMEPLAY

The application contains THREE stages.

Each stage becomes slightly more realistic.

Display progress throughout.

STAGE 1

Who Owns This? (do 3 questions of this only)

Display one realistic workplace task at a time.

Example:

"A customer reports that payments fail only on iPhones."

Present 6-8 role cards.

Examples for a tech company: Frontend Developer, Backend Developer, QA Engineer, Product Manager, UX Designer, Customer Support, Engineering Manager.

The player drags ONE role into the highlighted ownership slot.

After submission reveal:

✓ Primary Owner

✓ Why they own it

✓ Which roles may assist.

Never simply say Correct or Wrong.

Always explain the reasoning.

Include 8-10 different task cards.

STAGE 2

Task Routing (do 3 questions of this only)

Now the player manages incoming work.

A task appears.

The player must build the workflow.

Example:

Customer Support ↓ QA ↓ Backend ↓ Product Manager ↓ Customer

The player drags role cards into the correct order.

Some tasks may only need three steps.

Others may need five.

After submission animate the task moving through the organization.

Explain why this order is commonly used.

STAGE 3

Collaboration Challenge (do 3 questions of this only)

Present larger situations.

Examples:

Customer satisfaction suddenly drops

Sales increase dramatically

Negative reviews appear online

A major feature is delayed.

Instead of choosing one owner, allow players to assign up to FOUR departments or roles.

The player should think about collaboration.

After submission display:

Primary Owner

Supporting Teams

Reasoning

Possible Communication Flow.

Emphasize that complex problems usually require multiple people.

SCORING

Instead of points, award understanding.

Categories:

Ownership

Delegation

Collaboration

Workflow Thinking.

Display a radar or bar chart at the end using only HTML, CSS and JavaScript.

FINAL REFLECTION

Instead of a score, generate:

What you understood well

Where you tended to over-assign responsibility

Where you underestimated collaboration

One insight about how organizations actually work.

Example:

"Many real workplace problems are solved by teams rather than individuals."

Avoid absolute language.

GAME FEEL

The experience should feel satisfying.

Use:

drag-and-drop

animated cards

smooth transitions

satisfying snap animations

subtle sounds using CSS/JS only if possible (optional)

hover effects

progress indicator

completion celebration.

Avoid making it feel like an exam.

It should feel like a modern strategy game.

DESIGN

Premium modern UI.

Dark mode.

Glassmorphism.

Rounded cards.

Animated gradients.

Distinct colors for each department.

Role cards should feel collectible.

Task cards should resemble work tickets.

Use icons or emojis where appropriate.

TECHNICAL REQUIREMENTS

Store all scenarios in JavaScript objects.

Reuse components wherever possible.

Optimize code size for Claude Free.

If necessary, reduce the number of scenarios instead of reducing functionality.

Everything must remain offline.

Before returning:

Verify drag-and-drop works.

Verify scoring works.

Verify animations work.

Verify no syntax errors.

Verify responsive layout.

Return ONLY the complete HTML inside one code block.