Set-Content -Path "C:\Users\Ayushman\Downloads\pa-simulator\Day26\day26.md" -Value @"
# Day 26 - Prior Authorization Workflow Simulator
## #60DayClaudeChallenge

### What I Built
An interactive Prior Authorization (PA) Workflow Simulator —
a drag-and-drop dashboard that walks through the real-world
process of getting medical treatments approved by insurance.

### Built With
- Claude AI (Anthropic)
- HTML, CSS, JavaScript
- Drag and Drop API

### Key Learning
83% of physicians report PA delays lead to patients
abandoning treatment. Building this simulator made me
understand how fragile and complex this system really is.

### Features
- 4 Real-world case types (Surgery, MRI, Medication, Inpatient)
- Efficiency scoring and day tracking
- Peer-to-peer review and appeal workflows
- Educational notes grounded in AMA, KFF and CMS data
- Dark professional dashboard UI

### Screenshots
![Screenshot 1](Screenshot%202026-06-26%20143751.png)
![Screenshot 2](Screenshot%202026-06-26%20143821.png)
![Screenshot 3](Screenshot%202026-06-26%20143850.png)
![Screenshot 4](Screenshot%202026-06-26%20143908.png)
![Screenshot 5](Screenshot%202026-06-26%20143925.png)
![Screenshot 6](Screenshot%202026-06-26%20143956.png)
![Screenshot 7](Screenshot%202026-06-26%20144044.png)
![Screenshot 8](Screenshot%202026-06-26%20144131.png)
![Screenshot 9](Screenshot%202026-06-26%20144159.png)
///////////////////////////////////////////////////////
Prior Authorization Workflow Simulator (gamified, drag-and-drop)

Build a single-file, self-contained HTML application (HTML + CSS + vanilla JavaScript, no external dependencies, no build step) that visually simulates the US healthcare Prior Authorization (PA) workflow as an interactive, gamified, drag-and-drop experience.

The simulator should include:

• Three workflow lanes: Patient, Provider, and Payer.
• Interactive drag-and-drop movement of cases between stages.
• Multiple patient scenarios (elective surgery, MRI, specialty medication, inpatient admission).
• Medical necessity evaluation.
• Prior Authorization document collection.
• Submission to payer.
• Review outcomes including Approval, Pend, Denial, Appeal, and Peer-to-Peer Review.
• Educational explanations after every step.
• Progress tracker across the top.
• Days elapsed counter.
• Efficiency score.
• Celebration animation on approval.
• Workflow summary on completion.
• Responsive modern UI using shades of blue with black text.
• Working Restart / New Patient button.
• Fully functional buttons and interactions.

Technical Requirements:
- Single HTML file.
- HTML, CSS and Vanilla JavaScript only.
- No frameworks.
- No CDNs.
- No localStorage.
- All workflow state managed in JavaScript memory.
- Well-commented code.
- Scenario data stored in an editable array near the top.
- Output only the complete HTML file without truncation.