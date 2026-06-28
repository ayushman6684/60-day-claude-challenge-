# Day 28 — Hospital Admission Readiness Simulator

## 📅 Date: 28 June 2026

## 🏥 Project: MedAdmit Pro — Simulator V2.0

### 🔗 Live File
[hospital-admission-simulator-pro.html](./hospital-admission-simulator-pro.html)

---

## 📌 What I Built

A **Hospital Admission Readiness Simulator** — a fully interactive
clinical workflow training tool for:
- Case Managers
- Utilization Review Specialists  
- Admission Coordinators

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| 🔬 4-Phase Workflow | Setup → Analysis → Actions → Decision |
| 📊 Score Ring | Animated readiness % ring (live updates) |
| 🧩 6 Components | PA, Documentation, Orders, Insurance, Consent, Bed |
| ⚡ Action Chips | Click to resolve items, score updates instantly |
| 🛡️ Risk Assessment | High/Medium/Low risk tracking |
| 👥 Care Team Cards | Role-based coordination display |
| 📌 Governance Panel | Industry benchmarks (CMS, CAQH data) |
| ✅ Final Decision | Admit or Hold with full reasoning |
| 🕐 Live Clock | Real-time header clock |
| 📱 Responsive | Mobile + Desktop compatible |

---

## 🧠 Score Engine Logic
**Rules:**
- Initial score capped at 30–60% (before actions)
- ICU + Denied PA → hard cap at 67% until appeal succeeds
- 90%+ required for Admit decision

---

## 📸 Screenshots

### Phase 1 — Patient Setup
![Setup](./screenshots/setup.png)

### Phase 2 — Initial Analysis (30% — High Gaps)
![Analysis](./screenshots/analysis.png)

---

## 🎬 Demo Video
https://drive.google.com/file/d/13Q3S1p3smxNl6KmNe-y9089LcE6JiIne/view?usp=sharing
---

## 🔑 Key Learnings

1. **Weighted scoring systems** — Different components have
   different importance levels (PA = 25% most critical)

2. **Prior Authorization (PA)** — Most critical bottleneck
   in hospital admissions. Denied PA = cannot admit ICU patient

3. **InterQual/Milliman criteria** — Medical necessity
   standards that documentation must meet for UR review

4. **CMS 2-Midnight Rule** — Observation status patients
   have different billing, SNF eligibility vs inpatient

5. **MOON Notification** — Medicare patients in observation
   must receive written notice before services begin

6. **Care Coordination** — Multiple roles involved:
   Attending MD, Case Manager, UR, Nursing, Discharge Planner

7. **Claude AI** — Used to build advanced HTML simulator
   with animations, logic engine, and professional UI/UX

---

## 🛠️ Tech Stack

- **HTML5** — Single file application
- **CSS3** — Custom design system, animations, dark theme
- **Vanilla JavaScript** — Score engine, state management
- **Google Fonts** — Inter + JetBrains Mono
- **Claude AI** — Generated and enhanced the entire project

---

## 📊 Simulation Results

| Scenario | Initial Score | Final Score | Decision |
|----------|--------------|-------------|----------|
| AMI + ICU + PA Pending | 30% | 90%+ | ✅ Admit |
| CHF + Inpatient + PA Denied | 30% | 67% max | ⚠️ Hold |
| Pneumonia + OBS + PA Approved | 50% | 95% | ✅ Admit |

---

## 💡 What is Hospital Admission Readiness?

Before a patient is admitted to a hospital, several checks
must be completed:

1. **Prior Authorization** — Insurance company must approve
2. **Insurance Verification** — Benefits confirmed
3. **Clinical Documentation** — H&P, physician notes ready
4. **Physician Orders** — Attending MD completes order set
5. **Patient Consent** — Signed forms obtained
6. **Bed Assignment** — Physical bed confirmed in unit

If any critical item is missing → patient admission is delayed
or denied → potential revenue loss + patient safety risk.

---

*Built with ❤️ using Claude AI — Day 28 of my learning journey*
////////////////////////////////////////
Hospital Admission Readiness Simulator

Single-file HTML app. HTML, Tailwind CSS CDN, Vanilla JavaScript.
style: same as previously established
Healthcare simulation design system. Task-first — no dashboard on load.
User plays Hospital Admission Coordinator.

Setup — collect:
- Provider, Attending Physician
- Diagnosis: Acute MI / CHF / Pneumonia / Elective Surgery / Hip Fracture
- Admission Type: Inpatient / Observation / Emergency / ICU / Same-Day Surgery
- PA Status, Admission Date

Observation Status must always show: 'CMS 2-Midnight Rule applies — different cost-sharing, SNF eligibility, and billing than inpatient. Medicare patients require written MOON notification.'
Label all provider/payer names as illustrative training data.

Button: 🏥 Analyze Admission Readiness

Initial Analysis
Generate status for: PA, Insurance, Bed, Documentation, Physician Orders, Consent.
Readiness Score 30–60%. Do not reveal final decision yet.

Score Weighting:
PA Status 25% · Clinical Documentation 20% · Physician Orders 20% · Insurance 15% · Consent 10% · Bed 10%
Denied PA + ICU admission cannot reach 70% from admin tasks alone.

PA Branches:
Approved → continue.
Pending → Follow Up, Upload Docs, Contact Physician.
Denied → Review Reason, Contact Insurance, Submit Appeal.
Successful appeal converts to Approved.

Workflow Actions:
Assign Bed / Verify Insurance / Upload Documentation / Complete Consent / Contact Physician / Notify Nursing / Prepare Patient Arrival

Acute MI and CHF trigger a criteria note:
'InterQual/Milliman thresholds apply — ensure documentation meets medical necessity standards before UR review.'

Timeline milestones:
PA Review → Insurance Verification → Bed Assignment → Documentation → Consent → Patient Arrival → Registration → Clinical Assessment → Admission Complete

Care Coordination Cards:
Attending / Case Manager / Nursing / Utilization Review / Discharge Planner
UR card must name: concurrent review, denial risk identification, InterQual, Milliman.

Risk Tracking:
Documentation Risk / Insurance Risk / Bed Risk / Clinical Risk
Clinical Risk weighted higher for Acute MI, CHF, ICU.

At Readiness ≥ 75% show Governance Snapshot:
'Industry benchmarks (estimates only): PA turnaround 3–5 days · Inpatient denial rate ~8–10% (CMS) · PA rework cost ~$11/transaction (CAQH)'

Final Decision:
≥ 90% → ✅ Admit — full summary.
< 90% → ⚠ Not Ready — missing items, required actions, remaining risks.