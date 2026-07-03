# Day 33 — Media Integrity Analyzer

## 🎯 Project Overview
An interactive, single-file HTML web app that teaches media literacy through guided discovery. Users read fictional headlines and social posts, form their own gut reaction, then reveal an analysis showing manipulation techniques, accuracy scores, and fair rewrites.

## 🛠️ Tech Stack
- Pure vanilla **HTML, CSS, and JavaScript**
- No frameworks, no backend, no external assets — works fully offline in a single file
- Custom SVG-based animated gauges, sticky metrics sidebar, and modal system

## ✨ Features
- **Challenge 1 — Headline Detective:** Tap misleading phrases in a fictional headline, compare your gut reaction to the actual Headline Accuracy Score, and see a fair rewritten headline.
- **Challenge 2 — Emotion Detector:** Identify which words in a social post trigger which emotions, then reveal the target audience and manipulation technique used.
- **Live Media Integrity Metrics:** Headline Accuracy, Source Reliability, Emotional Manipulation, and Audience Targeting update in real time as you progress.
- **Media Integrity Dashboard:** A final score based on your own detection accuracy, plus key takeaways and practical media literacy habits.
- **Replay Mode:** Randomized scenarios so each playthrough feels fresh.

## 📚 Key Learnings
- Designing a scoring system that reflects *user skill* rather than fixed content properties — an early version blended in a fixed "content trust" score that unfairly capped everyone's results low.
- Building interactive, clickable text spans in vanilla JS without any UI framework.
- Using CSS custom properties (`:root` variables) to keep a consistent dark editorial theme across every component.
- The importance of testing interactive flows programmatically (simulated clicks) rather than just visually — caught a real bug where the "Reveal" button could be triggered with zero phrase selections, silently producing a 0 score.
- UX lesson: interactive elements need strong visual/discoverability cues — added a "jump to headline" scroll-and-highlight link after users struggled to find the clickable text.

## 📸 Screenshots
![Intro screen](./Screenshot%202026-07-03%20163530.png)
![Challenge 1 — Headline Detective](./Screenshot%202026-07-03%20163550.png)
![Reveal analysis](./Screenshot%202026-07-03%20163707.png)
![Challenge 2 — Emotion Detector](./Screenshot%202026-07-03%20163756.png)
![Media Integrity Dashboard](./Screenshot%202026-07-03%20163856.png)

## 🔗 Files
- [media-integrity-analyzer.html](./media-integrity-analyzer.html)   





/////////////////////////////////////////////////////////////
You are an expert frontend developer, UX designer, instructional designer, and media literacy analyst.

Ask the user to choose a color theme from a few options (including Claude Orange).

Create a beautiful single-file HTML application called 'Media Integrity Analyzer'.

Use pure vanilla CSS and JS. No Tailwind, npm, backend, APIs, images, or external assets. Everything must work offline in one HTML file.

The goal is to teach media literacy through interactive discovery, not test prior knowledge. The experience should feel like a guided lesson where users learn by observing, thinking, and then revealing the answer.

Make it interactive.

Before each challenge, briefly explain the concept in simple language, why it matters, and how it applies to everyday life.

Challenge 1: Headline Detective
- Generate a fictional news headline and matching article.
- Ask: Would you click this? (Yes / Maybe / No)
- Ask the user to identify exaggerated or misleading parts.
- Reveal the Headline Accuracy Score, highlighted mismatches, explanation, fair rewritten headline, and key takeaway.

Challenge 2: Emotion Detector
- Generate a fictional social media post, reel caption, or article excerpt.
- Ask how it made the user feel and which words influenced that feeling.
- Reveal the target audience, intended emotional response, manipulation technique, highlighted emotional phrases, neutral rewrite, and key takeaway.

Display live Media Integrity metrics:
- Headline Accuracy
- Source Reliability
- Emotional Manipulation
- Audience Targeting

Finish with a Media Integrity Dashboard containing:
- Overall Media Integrity Score
- What the user learned
- Biggest red flag
- Three practical media literacy habits
- Replay with completely new scenarios

Design a premium editorial-style dark interface with smooth animations, progress indicators, hover effects, modern cards, and responsive layout.

Ensure there are zero syntax errors.

Return ONLY the complete HTML inside one code block.