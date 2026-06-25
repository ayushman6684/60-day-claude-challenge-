# Day 25 — AI Shark Tank Simulator 🦈

## What I Built
A complete, production-quality **AI Shark Tank Simulator** as a single self-contained HTML file — no backend, no framework, just one file that runs in any browser.

---

## Features
- 🎤 **Startup Pitch Form** — 6-field intake (name, problem, solution, revenue model, audience, funding ask)
- 🦈 **4 AI Judge Personas** — VC, Serial Founder, Customer Advocate, Angel Investor
- ❓ **Dynamic Q&A Round** — Each judge asks 2 live AI-generated questions and reacts to your answers
- 📊 **Scoring System** — 5 metrics scored out of 100 with animated bars and ring chart
- 🏆 **Investment Decision** — INVEST / REJECT / ACQUIRE / COME BACK LATER with valuation
- 🎊 **Confetti** on funding success
- 📄 **PDF Report Download** — Dark-themed pitch report via jsPDF
- 🏅 **Leaderboard** — Persistent across sessions via localStorage
- 🔗 **Share Result** button

---

## My Startup Pitched: InternTrust

| Field | Details |
|-------|---------|
| **Startup** | InternTrust |
| **Ask** | $400,000 for 8% equity |
| **Problem** | 50% of internships in developing markets are unpaid; Tier-2/3 students face geographic discrimination |
| **Solution** | AI-powered skill-based internship marketplace with paid-only listings and global reach |
| **Revenue** | Freemium ($5–8/mo students) + SaaS ($99–249/mo companies) + 8–12% success fee |
| **Audience** | College students Yr 2–4 in India, SEA, Nigeria, Brazil + startups/SMBs 10–500 employees |

---

## Shark Tank Results

| Metric | Score |
|--------|-------|
| Market Potential | /100 |
| Innovation | /100 |
| Business Model | /100 |
| Execution | /100 |
| Investment Worthiness | /100 |
| **Overall** | **/100** |

**Verdict:** <!-- INVEST / REJECT / ACQUIRE / COME BACK LATER -->

**Valuation:** <!-- Fill in -->

---

## Screenshots

### Pitch Form
![Pitch Form](Screenshot%202026-06-25%20063325.png)

### Tank Room & Judges
![Tank Room](Screenshot%202026-06-25%20063822.png)

### Q&A Round
![Q&A Round](Screenshot%202026-06-25%20064153.png)

### Final Decision
![Decision](Screenshot%202026-06-25%20064322.png)

---

## Tech Stack
- Vanilla HTML + CSS + JavaScript (zero frameworks)
- Claude Sonnet 4.6 API (AI questions, reactions, scoring, decisions)
- jsPDF (browser-side PDF generation)
- canvas-confetti (celebration effect)
- localStorage (leaderboard persistence)
- Google Fonts (Rajdhani + Inter)

---

## Key Learnings

1. **Fallback-first design** — Always build graceful fallbacks before relying on an external API. The simulator works 100% offline with smart pre-written questions.
2. **Single-file architecture** — Keeping HTML + CSS + JS in one file makes sharing and deployment trivially easy (drag to Netlify = live in 30 seconds).
3. **AI persona engineering** — Each judge needed a distinct system prompt with clear focus areas to produce meaningfully different questions.
4. **UX over features** — The animated score bars, confetti, and dark theme made the experience feel real and engaging — polish matters.
5. **Founder-market fit** — Pitching InternTrust revealed gaps in my own pitch I hadn't noticed. The simulator is genuinely useful as a prep tool.

---

## Files in This Folder
| File | Description |
|------|-------------|
| `shark-tank-simulator.html` | Complete single-file app |
| `day25.md` | This file |
| `Screenshot 2026-06-25 063325.png` | Pitch form screen |
| `Screenshot 2026-06-25 063822.png` | Tank room & judges |
| `Screenshot 2026-06-25 064153.png` | Q&A round |
| `Screenshot 2026-06-25 064322.png` | Final decision |

---

## Live Demo
> Open `shark-tank-simulator.html` directly in any browser — no server needed.

---

/////////////////////////////////////////////
You are an expert full-stack developer and product designer.

Build a complete, production-quality AI Shark Tank Simulator as a single self-contained HTML file.

Requirements:

1. USER IDEA INPUT
- Startup Name
- Problem Statement
- Solution
- Revenue Model
- Target Audience
- Funding Ask

2. AI JUDGES
Create 4 distinct AI judges:

🦈 Venture Capitalist
- Focus on market size and scalability

🦈 Founder
- Focus on execution

🦈 Customer
- Focus on usefulness

🦈 Angel Investor
- Focus on profitability

3. PITCH ROUND
- Display startup pitch
- Each judge asks 2 questions
- User can answer
- Judges react dynamically

4. SCORING SYSTEM
Score out of 100:

- Market Potential
- Innovation
- Business Model
- Execution
- Investment Worthiness

5. INVESTMENT DECISION
Generate:
- Invest
- Reject
- Acquire
- Come Back Later

Show:
- Suggested Valuation
- Funding Amount
- Reasoning

6. UI
- Modern dark theme
- Shark Tank style
- Animated cards
- Responsive design

7. BONUS
- Confetti on funding success
- Download Pitch Report PDF
- Leaderboard
- Share Result button

Deliver as a single HTML file with no backend required.