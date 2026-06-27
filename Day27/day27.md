# Day 27 — Prior Authorization Simulator 🏥

## #60DayClaudeChallenge

---

## 🎯 What I Built
An interactive **Prior Authorization (PA) Journey Simulator** that walks users through the complete healthcare insurance approval process — from doctor visit to denial to appeal to final approval.

---

## 🖥️ Tech Stack
- Single HTML file
- Pure CSS Variables
- Vanilla JavaScript
- Zero dependencies
- Zero backend
- Works fully offline

---

## ✨ Features
- 🎭 8 fully interactive scenes
- 🌙 Dark / Light mode toggle
- ⚡ Speed control — Slow / Normal / Fast / Instant
- ▶️ Auto-play mode
- 🔢 Scene jump buttons
- 📊 Live progress bar
- 💬 Typing indicators
- 🔤 Inline tooltips
- 📖 Collapsible glossary — 10 PA terms
- 🎯 Score-based choices
- 🏆 Finish screen with metrics

---

## 🎭 8 Scenes Covered
1. 👨‍⚕️ Doctor visit & RA diagnosis
2. 📤 PA submission workflow
3. 📚 PA education — step therapy explained
4. 🔍 Insurance clinical review
5. ❌ Denial with exact reason
6. 📝 Appeal + Letter of Medical Necessity
7. ✅ Approval & reference number issued
8. 💡 Key takeaways

---

## 💡 Key Learnings

### What is Prior Authorization?
A requirement by an insurer that a provider must obtain approval before prescribing a medication for it to be covered.

### What I didn't know before building this:
- ✅ A denial is NOT final — it's a legal roadmap to appeal
- ✅ Every denial letter must legally state the exact reason
- ✅ Insurers must follow published clinical guidelines in appeals
- ✅ Step Therapy forces cheaper drugs first — even when wrong
- ✅ One wrong ICD-10 code = instant denial
- ✅ One PA Reference Number covers ALL fills for 12 months
- ✅ ePA mandates will cut approval from 14+ days → under 24 hours
- ✅ Humira costs $6,000–$8,000/month without insurance approval

---

## 📸 Screenshots
![Screenshot 1](Screenshot%202026-06-27%20122559.png)
![Screenshot 2](Screenshot%202026-06-27%20122627.png)
![Screenshot 3](Screenshot%202026-06-27%20122741.png)
![Screenshot 4](Screenshot%202026-06-27%20122819.png)
![Screenshot 5](Screenshot%202026-06-27%20122928.png)
![Screenshot 6](Screenshot%202026-06-27%20123111.png)
![Screenshot 7](Screenshot%202026-06-27%20123147.png)

---

## 🔗 Files
- `prior-auth-simulator-v2.html` — Full simulator

---

## 🙏 Tools Used
- Claude by Anthropic
- VS Code
- GitHub
///////////////////////////////////////////////////
Prior Authorization Story Simulator

Single-file HTML app. HTML, Tailwind CSS CDN, Vanilla JavaScript.
Use createElement + appendChild for every new chat bubble. Never call innerHTML = on the chat container.
Design: same as previously established.

Characters
👦 Rahul — patient. Appears left.
👧 Priya — healthcare operations specialist. Appears right.
Narrators and doctors appear as centered italic text only, never chat bubbles.

Story — 8 scenes with append-only chat feed and progress bar:

1. Doctor Visit — Rahul visits City Medical Center. Dr. Patel diagnoses Rheumatoid Arthritis, prescribes Humira.

2. Insurance Roadblock — Dr. Patel's office submits PA directly to StarCare Health (payer). No pharmacy involved. Flow: Provider → PA Request → Payer. Approved PA is saved on file permanently.

3. What is PA? — Priya explains in plain language. Include: step therapy isn't just bureaucracy — for aggressive diagnoses, delays can affect disease progression. Cite: 'AMA 2023 PA Survey: PA causes treatment delays in the majority of cases.'

4. Insurance Review — Priya walks through what StarCare Health checks: eligibility, clinical documentation, ICD-10 diagnosis match, step therapy history. Explain why each matters.

5. Denial — Denied: missing step therapy documentation. Denial ≠ permanent. Priya notes the system side: 'PA denials cost physician offices 2+ staff hours to resolve.'

6. Appeal — Gather documents, Letter of Medical Necessity, formal appeal filing.

7. Approval — PA approved, saved on file. Reference number issued. No repeat PA needed for Humira.

8. Takeaways — Two perspectives: Patient (what Rahul learned) + System (how health systems track denial rate, appeal rate, resolution time).

After each scene show 2 choices that influence dialogue and progression.
Label StarCare Health as an illustrative example throughout.
Beginner-friendly language.
Healthcare education design system.