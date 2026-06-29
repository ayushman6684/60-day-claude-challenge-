# Day 29 — Operation Lifeline: Supply Chain Crisis Lab

**Date:** 29 June 2026  
**Project:** AI-Powered Supply Chain Simulation Game  
**Type:** Single-file HTML App (React via CDN + Babel JSX)  
**File Size:** 76.6 KB

---

## 🎯 What I Built

A complete, offline-ready supply chain crisis simulation game called **Operation Lifeline**.  
Built as a single HTML file with React (CDN), Babel JSX, and vanilla CSS — no npm, no backend, no external assets.

Players take the role of a supply chain executive navigating a real-world crisis across 8 interactive screens.

---

## 🖥️ Screenshots

### Welcome Screen
![Welcome Screen](Screenshot%202026-06-29%20172311.png)

### Company Profile
![Company Profile](Screenshot%202026-06-29%20172346.png)

### Crisis Briefing
![Crisis Briefing](Screenshot%202026-06-29%20172403.png)

### War Room — Response Actions
![War Room](Screenshot%202026-06-29%20172427.png)

### Supplier Negotiation
![Negotiation](Screenshot%202026-06-29%20172633.png)

### Final Dashboard
![Final Dashboard](Screenshot%202026-06-29%20172703.png)

---

## 🗺️ Game Flow (8 Screens)

| # | Screen | What Happens |
|---|--------|-------------|
| 1 | Welcome | Title screen with feature overview |
| 2 | Company Profile | Random fictional company generated (industry, revenue, suppliers, countries) |
| 3 | Crisis Briefing | 1 of 8 random crises assigned with urgency + financial impact |
| 4 | War Room | Player picks 3 of 6 response actions; animated metrics update live |
| 5 | Supplier Negotiation | 4-round branching negotiation affecting Trust, Price, Lead Time |
| 6 | CEO Boardroom | 5 executive decision-making questions, scored out of 100 |
| 7 | AI Strategy | Player selects 2 of 5 AI technologies with business impact data |
| 8 | Final Dashboard | Animated score ring, 6-dimension breakdown, expert feedback |

---

## ⚙️ Tech Stack

- **React 18** via CDN (no npm)
- **Babel Standalone** for JSX in-browser transpilation
- **Vanilla CSS** with CSS custom properties (dark theme)
- **Google Fonts** — Inter + JetBrains Mono
- Pure `useState` hooks — no Redux, no Context API
- Runs 100% offline from a single `.html` file

---

## 🎮 Features

- **8 crisis types:** Factory Fire, Supplier Bankruptcy, Port Strike, Cyberattack, Flood, Raw Material Shortage, Political Conflict, Shipping Delay
- **Randomized every playthrough:** company name, industry, countries, crisis type, affected region
- **Animated progress bars** with spring easing
- **Score ring SVG** animation on final screen
- **Branching decisions** with expert feedback after each choice
- **Personalized final report:** strongest area, biggest gap, recommendation, lessons learned
- Fully **responsive** — works on mobile and desktop
- **Premium dark theme** — enterprise dashboard aesthetic

---

## 📊 Scoring System

| Dimension | Weight | Source |
|-----------|--------|--------|
| Leadership | 22% | CEO Boardroom answers |
| Negotiation | 18% | 4-round supplier negotiation |
| Resilience | 18% | War Room inventory + delivery metrics |
| Cost Control | 15% | War Room cost metric + AI choices |
| Risk Management | 15% | Combined negotiation + leadership |
| Customer Satisfaction | 12% | War Room satisfaction metric |

---

## 💡 Key Learnings

1. **Single-file React apps are powerful** — Babel CDN lets you write JSX without any build tooling. Great for prototypes and offline tools.

2. **CSS custom properties make dark themes maintainable** — defining `--accent`, `--card`, `--border` etc. at `:root` level means the entire visual system can be changed in one place.

3. **Game design is UX design** — every screen needed a "why does this matter" explanation so beginners felt informed, not lost. Context before decision = better engagement.

4. **Randomization creates replayability** — by separating data (company templates, crisis types, action effects) from logic, every playthrough feels fresh with minimal extra code.

5. **Animated progress bars signal consequence** — using CSS transitions on bar width makes abstract score changes feel real and impactful to the player.

6. **Supply chain tradeoffs are genuinely hard** — researching real crisis response strategies (air freight vs safety stock, exclusivity vs flexibility) made the simulation credible and educational.

---

## 🚀 How to Run

1. Download `operation-lifeline.html`
2. Open it in any modern browser (Chrome, Edge, Firefox)
3. No internet required after initial font load
4. Click **Start Simulation** and play!

---

## 📁 Files in This Folder

/////////////////////////////////////////////////////////////You are an expert frontend developer, UX designer, game designer, and supply chain consultant.

Build it so a complete beginner can play it — plain language, context before every decision, 'why does this matter' explanations, and guidance that makes you feel smart rather than lost.

Build a complete single-file HTML app named 'Operation Lifeline: Supply Chain Crisis Lab'.

Requirements:
• Output ONLY one HTML file.
• React via CDN + Babel JSX.
• Plain HTML, CSS, and JavaScript only.
• No Tailwind, npm, backend, APIs, images, or external assets.
• Must run offline by opening the HTML file.
• No placeholders or incomplete features.

Flow:
1. Welcome screen with title, subtitle, and 'Start Simulation'.
2. Generate a random fictional company (industry, revenue, factories, warehouses, suppliers, inventory days, lead time, countries) displayed as modern cards.
3. Generate one random crisis (factory fire, supplier bankruptcy, port strike, cyberattack, flood, raw material shortage, political conflict, shipping delay) with urgency and business impact.
4. War Room: Present six response actions. The player chooses three. Simulate consequences by updating Cost, Inventory, Profit, Delivery Speed, and Customer Satisfaction using animated progress bars.
5. Negotiation: Branching supplier negotiation with four rounds. Each choice affects Trust, Price, and Lead Time. Display a negotiation score.
6. CEO Boardroom: Five multiple-choice leadership questions. Score executive decision-making.
7. AI Strategy: Let the player choose two AI investments from Demand Forecasting, Inventory Optimization, Supplier Risk Monitoring, Warehouse Vision, and Procurement Copilot. Show expected business impact.
8. Final Dashboard: Display Overall Crisis Score (0-100), Leadership, Negotiation, Resilience, Cost Control, Risk Management, and Customer Satisfaction. Include personalized feedback, biggest mistake, best decision, expert recommendation, and lessons learned.

Design:
• Premium dark theme inspired by enterprise dashboards.
• Responsive.
• Rounded cards.
• Smooth transitions.
• Hover effects.
• Progress bars.
• Modern typography.
• Replay button.
• Every playthrough should randomize companies, crises, values, and outcomes.

Structure the React code into reusable components using useState. Ensure every button works, there are no console errors, and the final response contains only the complete HTML code inside a single code block.