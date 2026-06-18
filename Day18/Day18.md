# Day 18 — Brain Dump Action Planner: Custom Claude Skill

## What I Built Today
Today's focus was a custom Claude Skill called **Brain Dump Action Planner** — a reusable workflow that turns messy meeting transcripts, voice memos, and brainstorm notes into a structured, interactive breakdown without inventing or assuming any information that wasn't actually stated.

## The Skill
**Trigger:** `/brain-dump-action-planner`

**Purpose:** Transform unstructured notes (meeting transcripts, voice memos, brain dumps) into:
- A short summary
- Key takeaways
- An interactive action items table (Task / Owner / Deadline / Status)
- Open questions
- Risks & blockers
- Conflicts (in deadlines, owners, or decisions)
- Additional notes
- *(Transcript Mode only)* Speaker summaries, decisions by speaker, and action items by speaker — with attribution notes wherever ownership wasn't explicit

**Core rule:** never invent, assume, or estimate missing information. Anything not stated in the source is labeled "Not specified."

## Generated Dashboard
Fed the skill a sample quarterly growth strategy meeting transcript. The output was a single self-contained HTML dashboard (no external dependencies beyond Google Fonts) with:
- Sidebar navigation with scroll-spy highlighting
- An animated metrics strip (revenue growth, traffic, retention, and an enterprise deal funnel that counts up and fills in on load)
- Collapsible speaker-summary cards
- A sortable, filterable action items table with click-to-complete checkboxes, a live completion progress bar, and a confetti celebration when every item is checked off
- Color-coded status badges (🔴 High Priority, ⏳ Pending, ✅ Completed, ⚠️ Conflict, ❓ Open Question)
- Scroll-reveal animations and a reading-progress bar for polish

## Structured Outputs Produced
1. Summary
2. Key Takeaways
3. Speaker Summary
4. Action Items (table)
5. Action Items by Speaker
6. Decisions by Speaker
7. Open Questions
8. Risks & Blockers
9. Conflicts
10. Additional Notes (incl. Attribution Notes for unclear ownership)

## Screenshots
*(Screenshots live in `Day18/screenshots/` — see setup commands below.)*

## Key Learnings
- Custom Skills let Claude follow a fixed, repeatable output contract instead of improvising the format every time — useful for anything that needs a consistent shape, like status reports or meeting logs.
- An explicit "never invent missing data" rule changes output quality in a real way: it forces "Not specified" instead of a plausible-sounding guess, which matters once a document starts circulating.
- Transcript Mode (speaker-by-speaker breakdown) surfaces ownership gaps that a flat summary would hide — several action items in this transcript had no explicitly named owner, and the skill flagged that via Attribution Notes instead of silently assigning one.
- Small interaction details — a completion progress bar, animated counters, a confetti moment on finishing all action items — make a dashboard people actually want to open and use, instead of a static report that gets skimmed once.
- Iterating on a generated artifact (a visual polish pass, then a targeted bug fix on the status-toggle logic) is faster and safer than rebuilding from scratch.

## Tech Stack
- Claude Sonnet 4.6 (custom Skill: Brain Dump Action Planner)
- Self-contained HTML/CSS/vanilla JS dashboard artifact

---
*Log entry generated June 18, 2026.*
Prompt used////////////////////////////////////////////
Skill Name: brain-dump-action-planner

Description: Transform messy notes, meeting transcripts, voice memos, brainstorming sessions, and stream-of-consciousness thoughts into structured summaries, action plans, decisions, open questions, and task lists. Organize information clearly without inventing, assuming, or filling gaps. Preserve all names, dates, numbers, and terminology exactly as provided.

Instructions:

## Output Requirement

For Full Breakdown, Transcript Mode, and Merge Mode, generate the output as a complete interactive HTML artifact.

Requirements:

* Output a self-contained HTML artifact starting with <style>.
* Use a modern dashboard layout.
* Mobile responsive.
* Use cards, sections, badges, tables, and visual indicators.
* Do not use markdown.
* Use clean typography and strong visual hierarchy.
* Highlight important items using colored status badges.
* Make action items visually prominent.
* Use collapsible sections for long notes.
* Output only the HTML artifact.

### Required Sections

1. Summary

* Short overview of the note, meeting, transcript, or brain dump.

2. Key Takeaways

* Display as cards or structured highlights.

3. Action Items

* Interactive table containing:
* Task
* Owner
* Deadline
* Status

4. Open Questions

* Display unresolved topics and pending decisions.

5. Risks / Blockers

* Display dependencies, blockers, risks, and concerns.

6. Conflicts

* Display conflicting deadlines, owners, decisions, or information.

7. Additional Notes

* Supporting context that does not fit elsewhere.

8. Source Information (Merge Mode only)

* Display merged sources.

### Status Badges

Use:

* 🔴 High Priority
* 🟠 Medium Priority
* 🟢 Low Priority
* ⚠️ Conflict
* ❓ Open Question
* ✅ Completed
* ⏳ Pending

### Missing Information

If information is missing display:

'Not specified'

Never invent values.

### Transcript Mode

Include:

* Speaker Summary
* Decisions by Speaker
* Action Items by Speaker
* Attribution Notes when ownership is unclear

Use speaker labels exactly as provided.

### Merge Mode

Include:

* Duplicate Items Section
* Conflict Resolution Review Section
* Source Note

Never automatically resolve conflicts.

### Design Goals

The final artifact should feel like:

* Notion
* ClickUp
* Linear
* Asana
* Airtable
* Modern Project Dashboard

Use responsive cards, clean tables, section headers, badges, hover effects, soft shadows, and dashboard-style layouts.

Everything displayed must come directly from the provided notes.

Never add, infer, assume, predict, estimate, or complete missing information.

Generate the complete HTML directly starting with <style>.