# Day 21 — Privacy & Digital Footprint Audit Dashboard

## #60DayClaudeChallenge

### What I built
An interactive HTML dashboard that audits a digital footprint from a simple list of apps (Instagram, Snapchat, TikTok, YouTube, Discord, WhatsApp, iMessage, Spotify, Roblox, PUBG Mobile, Amazon, Meesho, Google Search, Google Pay, Google Photos).

The dashboard generates:
- Digital Footprint Score (0–100) and Privacy Score (0–100)
- Exposure Heatmap across all 15 services
- Company Exposure Ranking (parent-company concentration)
- Data Collection Matrix (app vs. data-type grid)
- Risk Radar across 6 exposure dimensions
- Digital Twin Profile (estimated traits, confidence-labeled)
- Most Valuable Data Assets ranking
- Live Privacy Improvement Simulator
- Final Verdict summary

### Key constraint I enforced
Every claim on the dashboard is explicitly tagged **FACT** or **ESTIMATE** — directly in the UI, not just as a disclaimer. No certainty language on inferred traits. No claim of accessing real private data; everything is calculated transparently from the 15-service list using a stated formula.

### Privacy findings (illustrative, from the sample dataset)
- 15 services traced back to **11 distinct parent companies**
- Google alone owns **4 of 15 services** (Search, YouTube, Pay, Photos) — a 26.7% ecosystem concentration
- Footprint Score: **78/100 (Significant)**
- Privacy Score: **47/100 (Fair)**
- Highest-value inferred data assets: real-time location history and purchase/spending patterns

### The redesign moment
Asked Claude to "make it more attractive." Instead of a palette swap, it treated it as a full design brief — moved from a generic dark dashboard look to a case-file/dossier aesthetic (paper background, serif headers, stamped section markers) that fits the subject matter of a privacy audit. It also ran its own WCAG contrast checks and validated the underlying data logic in a sandboxed script before handing the file back.

### Learnings
- Separating "fact" from "inference" works best when it's a structural part of the UI, not a footnote.
- Asking for "more attractive" without specifics can still produce a deliberate result if the model treats it as a design brief rather than a styling tweak.
- Transparent, formula-based scoring (vs. a black-box "score") makes a privacy tool more trustworthy and easier to sanity-check.

### Files in this folder
- `day21-privacy-dashboard.html` — the full interactive dashboard
- Screenshots of the dashboard sections
//////////////////////////////////////////////////////
### Sample User Dataset

Use the following dataset as the user's reported digital footprint.

Facts:

Applications : Instagram, Snapchat, TikTok, YouTube, Discord, WhatsApp, iMessage, Spotify, Roblox, PUBG Mobile, Amazon, Meesho, Google Search, Google Pay, Google Photos

Dataset Rules:
* Treat all listed services as Facts.
* Use these services to calculate all scores, exposure rankings, heatmaps, risk levels, ecosystem concentration, digital twin insights, data collection likelihood, and privacy recommendations.
* Infer parent companies from the services.
* Any behavioural, demographic, lifestyle, shopping, spending, entertainment, mobility, travel, communication, or technology-related conclusions must be labeled as Estimates.
* Never claim certainty.
* Never claim access to private databases.
* If information cannot reasonably be inferred, display: 'Not enough information provided.'

# Output Requirement

Generate a complete interactive HTML artifact starting with <style>.

Do not output markdown.

The artifact should feel like a premium cybersecurity dashboard.

Design Inspiration:

Notion, Stripe Dashboard, Linear, Google Privacy Checkup, Apple Privacy Reports, Modern SaaS Analytics Platforms.

### Dashboard Overview

Create a visually rich dashboard containing:

1. Digital Footprint Score (0-100)
2. Privacy Score (0-100)
3. Exposure Heatmap
4. Company Exposure Ranking
5. Data Collection Matrix
6. Risk Radar
7. Digital Twin Profile
8. Most Valuable Data Assets
9. Privacy Improvement Plan

Display:

Digital Footprint Score
🟢 0-30 = Minimal
🟡 31-60 = Moderate
🟠 61-80 = Significant
🔴 81-100 = Extensive

Privacy Score
🔴 0-30 = Weak
🟠 31-60 = Fair
🟡 61-80 = Good
🟢 81-100 = Strong

Include:
* Total Services Used
* Number of Parent Companies
* Ecosystem Concentration Score
* Estimated Tracking Surface

Create all sections exactly as specified including Digital Twin Profile, Exposure Heatmap, Company Exposure Ranking, Data Collection Matrix, Risk Radar, WOW Insights, Most Valuable Data Assets, Privacy Improvement Simulator, and Final Verdict.

Critical Rules:
* Never claim access to private databases.
* Never claim certainty about inferred traits.
* Separate Facts from Estimates.