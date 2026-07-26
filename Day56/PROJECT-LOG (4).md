# CrackIt — Project Log

A running log of progress across the 10-day capstone. One entry per day.

---

## Day 1 — Requirements
**Date:** July 21, 2026
**Phase:** Requirements
**Summary:** Discovered and scoped the project through a guided interview. Selected "CrackIt — AI Resume Defense Simulator": an AI interviewer that cross-examines a candidate's resume against a target job description, with adjustable tone (Friendly/Standard/Tough), adaptive question count, and a downloadable ATS-style PDF feedback report. Explicitly scoped out accounts, voice, and shareable links for v1.0.
**Deliverables produced:** `PRD.docx`, `Implementation Blueprint (Days 2-10).md`, `Pitch Deck.pptx`
**Status:** ✅ Complete

---

## Day 2 — Design
**Date:** July 22, 2026
**Phase:** Design
**Summary:** Created the GitHub repository (`crackit-ai-interview`) and established the initial project skeleton (`README.md`, `.gitignore`, `docs/` folder). Finalized and justified the full tech stack (Next.js, Tailwind, Claude API, no database/no auth, Vercel free tier). Designed the complete system architecture (component diagram, data flow, request lifecycle, AI prompt composition), the session-based data schema (in place of a database, per the stateless architecture decision), the full API contract for all 5 endpoints, the complete UI/user flow with low-fidelity wireframes for all 5 screens, and the final project folder structure. Updated the Implementation Blueprint's Day 3 section to reflect that repo creation happened today instead of Day 3.
**Deliverables produced:** `ARCHITECTURE.md`, `SCHEMA.md`, `API.md`, `UI-WIREFRAMES.md`, `PROJECT-STRUCTURE.md`, updated `Implementation Blueprint.md`
**Status:** ✅ Complete — Day 3 can begin implementation immediately, no further planning required.

---

## Day 3 — Setup
*(To be filled in at the end of Day 3)*

## Day 3 — Setup
**Date:** July 23, 2026
**Phase:** Setup
**Summary:** Verified environment (Node v24.15.0, npm 11.12.1 — no install needed). Scaffolded Next.js in place inside the existing repo (JavaScript, ESLint, Tailwind, `src/` directory, App Router, no TypeScript/React Compiler/AGENTS.md). Installed feature dependencies (`@anthropic-ai/sdk`, `pdf-parse`, `mammoth`, `@react-pdf/renderer`). Built the full folder structure with 4 placeholder pages and 5 placeholder API routes matching `API.md` exactly. Pulled forward a few cheap foundation pieces: working `NavBar.js`, a fully-shaped `SessionContext.js`, and a `lib/claude.js` client stub. Resolved several tooling issues (README file conflict during scaffolding, ES-module `__dirname` fix in `next.config.mjs`, corrupted `.next` cache, a layout.js save issue) without any architecture changes. Verified both local dev server and production build (`npm run build`) run cleanly with zero errors. Committed and pushed 27 files to GitHub. Deployed live to Vercel on the free Hobby tier at `https://crackit-ai-interview.vercel.app`, verified matching local behavior exactly.
**Deliverables produced:** `SETUP.md`, `ENVIRONMENT.md`, `PROJECT-STRUCTURE.md` (updated), `DAY3-SUMMARY.md`, updated `Implementation Blueprint.md`
**Status:** ✅ Complete — Day 4 can begin building the first real feature (Resume & JD Input) immediately, no further setup required.

---

## Day 4 — Implementation: Resume & JD Input
*(To be filled in at the end of Day 4)*

## Day 4 — Implementation: Resume & JD Input
**Date:** July 24, 2026
**Phase:** Implementation
**Summary:** Built the real Resume & Job Description Input screen. Implemented `/api/parse-resume` with actual PDF (`pdf-parse`) and DOCX (`mammoth`) text extraction, graceful fallback on unreadable files, and file type/size validation. Built the full `/setup` page UI: paste/upload toggle, editable extracted text, optional job title/description fields, and a Continue button gated on resume text being present. Created `src/styles/theme.js` for shared brand colors. Resolved several `pdf-parse` packaging issues along the way (a broken ESM default export, then a version that required unavailable browser rendering APIs, then a debug-mode file path bug) by pinning to `pdf-parse@1.1.1` and importing its internal module directly via `createRequire`. Verified all 6 test scenarios (paste, real PDF, real DOCX, corrupted file fallback, optional job fields, Continue navigation) both locally and on the live Vercel deployment. Clean production build, committed and pushed, auto-deployed and confirmed working in production.
**Deliverables produced:** Working `/setup` screen, working `/api/parse-resume` endpoint, `src/styles/theme.js`
**Status:** ✅ Complete — Day 5 can begin building the Tone Selection screen and adaptive AI interview engine immediately; `SessionContext` already holds resume/JD data correctly.

---

## Day 5 — Implementation: Adaptive Interview Engine
*(To be filled in at the end of Day 5)*

## Day 5 — Implementation: Adaptive Interview Engine
**Date:** July 25, 2026
**Phase:** Implementation
**Summary:** Built the Tone Selection screen and the full adaptive AI interview engine — the core "wow" feature of CrackIt. **Architecture change:** swapped the AI engine from the originally-planned Anthropic Claude API to Google's Gemini API, since Gemini offers a genuinely free tier with no billing requirement ever, versus Anthropic's API which requires eventual billing setup even for low-cost usage. This changes `lib/claude.js` → `lib/gemini.js`, the env variable from `ANTHROPIC_API_KEY` → `GEMINI_API_KEY`, and the SDK from `@anthropic-ai/sdk` → `@google/genai`. All other architecture (stateless sessions, adaptive question-count logic, tone personas, API contracts) is unchanged. Built `lib/prompts.js` with base interviewer rules, 3 tone personas (Friendly/Standard/Tough), adaptive question-count heuristic (6-12 based on resume/JD complexity), and the feedback-scoring prompt (prepared now, used starting Day 6). Built `/api/interview/start` and `/api/interview/next` with real multi-turn Gemini calls. Built the full Tone Selection + Chat UI in `/interview`. Resolved a model-availability issue (`gemini-2.5-flash` was restricted for new API projects) by switching to Google's auto-updating `gemini-flash-latest` alias, and a stray duplicate `src/app/api/interview/page.js` file that broke the production build. Verified full multi-turn conversations (both locally and in production) correctly reference resume/JD specifics, adapt tone appropriately, track progress, and transition to `/results` when the adaptive question cap is reached.
**Deliverables produced:** Working Tone Selection screen, working multi-turn AI interview chat, `src/lib/gemini.js`, `src/lib/prompts.js`
**Status:** ✅ Complete — Day 6 can begin building the feedback/scoring engine immediately; `buildFeedbackPrompt()` is already written and ready to use, and completed transcripts are already available in `SessionContext`.

---

## Day 6 — Implementation: Feedback & Scoring Engine
*(To be filled in at the end of Day 6)*

## Day 6 — Implementation: Feedback & Scoring Engine
**Date:** July 26, 2026
**Phase:** Implementation
**Summary:** Built the real `/api/feedback` endpoint and the full `/results` screen, completing the core MVP loop end-to-end (Setup → Tone → Interview → Feedback). Implemented category-wise scoring (Resume Credibility, Technical Knowledge, Communication, Problem Solving, Confidence, Resume-JD Fit), strengths/weaknesses, actionable suggestions, and model answers referencing real transcript exchanges, with retry-and-validate logic for malformed JSON responses. Added the required site-wide footer ("Built with Claude as part of the AB Talks 60-Day Claude AI Challenge") via a new `Footer.js` component in the root layout. Hardened the Gemini client with automatic retry (3 attempts, increasing backoff) and automatic fallback to `gemini-flash-lite-latest` if the primary model is under heavy free-tier demand — resolved a real production incident where `gemini-flash-latest` returned repeated 503 errors. Found and fixed a genuine scoring bug: Gemini intermittently returned scores on a 0-10 scale instead of the required 0-100 scale; fixed with an explicit, example-driven prompt constraint plus a server-side rescale safety net that detects and corrects an all-≤10 score set before it reaches the user. Verified extensively on both localhost and the live Vercel deployment: a terse, low-effort answer set correctly scored in the single digits/low range, and a detailed, technical answer set correctly scored in the 85-90 range — confirming genuine, meaningful score differentiation in both directions, in production.
**Deliverables produced:** Working `/api/feedback` endpoint, working `/results` screen with scorecard/strengths/weaknesses/suggestions/model answers, `src/components/ScoreBar.js`, `src/components/Footer.js`, hardened `src/lib/gemini.js` with retry + fallback
**Status:** ✅ Complete — core MVP loop (Setup → Interview → Feedback) fully functional end-to-end, locally and in production. Day 7 can begin PDF report generation immediately; feedback data shape is already stable and available in `SessionContext`.

---

## Day 7 — Implementation: PDF Report Generation
*(To be filled in at the end of Day 7)*

## Day 8 — Testing & Polish
*(To be filled in)*

## Day 9 — Deployment
*(To be filled in)*

## Day 10 — Maintenance & Launch
*(To be filled in)*
