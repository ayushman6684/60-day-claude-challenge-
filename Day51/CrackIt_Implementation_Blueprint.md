# CrackIt — Implementation Blueprint (Days 2–10)
### AI Resume Defense Simulator — AB Talks 60-Day Claude AI Challenge, 10-Day Capstone

> **This document is the single source of truth for the rest of the build.** Each day below is written so that a *fresh* AI conversation (with no memory of prior sessions) can pick it up and execute it directly — the architecture, stack, and major decisions are already made. No day should require re-planning or re-architecting; if something is genuinely ambiguous, make the smallest reasonable choice and note it in the handoff.

---

## 0. Locked Architecture & Tech Stack (do not re-litigate this)

This stack was chosen for: zero/near-zero cost, single-repo simplicity, and a solo intermediate developer shipping in ~3–4 hrs/day.

| Layer | Choice | Why |
|---|---|---|
| Framework | **Next.js 14 (App Router, JavaScript)** | One framework for frontend + backend (API routes) → one deploy, no CORS, no separate backend hosting |
| Styling | **Tailwind CSS** | Fast to build polished UI without a design system from scratch |
| AI Model | **Anthropic Claude API** (`claude-sonnet` family) | Aligned with the challenge; strong at multi-turn reasoning and structured output; low cost per session |
| Resume parsing (PDF) | **pdf-parse** (npm) | Simple, free, good enough for text-based resumes |
| Resume parsing (DOCX) | **mammoth** (npm) | Free, reliable DOCX → plain text |
| PDF report generation | **@react-pdf/renderer** | Generate the ATS-style report as React components, rendered server-side to PDF |
| Hosting | **Vercel (Free/Hobby tier)** | Native Next.js support, generous free tier, simple `git push` deploys |
| Version control | **GitHub** | Standard, free, integrates directly with Vercel |
| State / storage | **None (stateless)** — full conversation transcript passed with each request from client state | No accounts, no DB needed for v1.0; simplest possible reliable architecture |
| Secrets | **Environment variables** (`.env.local` locally, Vercel dashboard in production) | Never commit API keys |

**Data flow in one sentence:** the browser holds the session state (resume text, JD, tone, transcript) in React state; each interview turn and the final feedback/report generation are separate API calls to Next.js API routes, which call the Claude API and return structured JSON.

**Repo name suggestion:** `crackit-ai-interview`

---

## Day 2 — 🎨 Design & Architecture

### 🎯 Objective
Turn the PRD into a concrete technical design: confirm the architecture above, design the AI prompt strategy for the three interview tones, define API contracts between frontend and backend, and sketch the screen flow — all on paper/docs, no code yet.

### 📖 What I'll learn
- How to design a stateless, session-based architecture without a database
- How to structure prompts for a multi-turn, persona-driven AI conversation
- How to define clean API contracts before writing implementation code

### 🛠 Features to build
None yet — this is a planning/design day. Output is documentation, not code.

### 📝 Step-by-step implementation plan
1. **Confirm the architecture** in Section 0 above — read it fully before doing anything else.
2. **Design the screen flow** (5 screens): Landing → Resume & JD Input → Tone Selection → Interview Chat → Feedback & Report. Sketch each screen's key elements (can be a simple wireframe in any tool, or described in words/boxes — doesn't need to be fancy).
3. **Define the API routes** (Next.js API routes under `app/api/`):
   - `POST /api/parse-resume` — accepts an uploaded file, returns extracted plain text (or an error indicating fallback-to-paste is needed).
   - `POST /api/interview/start` — accepts `{ resumeText, jobTitle, jobDescription, tone }`, returns the first interview question + a `sessionContext` object (question count target, etc.) to be held client-side.
   - `POST /api/interview/next` — accepts `{ transcript, sessionContext }`, returns the next AI question, or a flag `interviewComplete: true` when the adaptive cap is reached.
   - `POST /api/feedback` — accepts the full `transcript` + `sessionContext`, returns structured JSON: scores per category, strengths, weaknesses, suggestions, and model answers.
   - `POST /api/generate-report` — accepts the feedback JSON + transcript, returns a PDF file (binary) via `@react-pdf/renderer`.
4. **Design the three interviewer personas as system prompts.** Draft (in a `PROMPTS.md` scratch file) the tone-specific instructions:
   - **Friendly:** supportive coach, gentle follow-ups, encouraging language, still asks real questions but softens pressure.
   - **Standard:** professional interviewer, realistic follow-ups, respectful pushback on weak points.
   - **Tough:** skeptical panel-style interviewer, directly challenges vague claims, presses on inconsistencies and technical depth.
   Each persona prompt should instruct the model to: reference specific resume/JD details by name, ask one question at a time, adapt follow-ups to the candidate's last answer, and internally track progress toward the 6–12 question cap.
5. **Design the adaptive question-count logic.** Simplest reliable approach: the `start` API estimates a target question count (6–8 for a resume with <2 projects/experience entries and no JD; 9–12 for richer resumes and/or a JD provided) and stores it in `sessionContext`. The `next` API checks `transcript.length` against that target to decide whether to continue or return `interviewComplete: true`.
6. **Design the feedback JSON schema** — lock this now so the report generator (Day 7) has a stable contract:
   ```json
   {
     "scores": {
       "resumeCredibility": 0,
       "technicalKnowledge": 0,
       "communication": 0,
       "problemSolving": 0,
       "confidence": 0,
       "resumeJdFit": 0
     },
     "strengths": ["..."],
     "weaknesses": ["..."],
     "suggestions": ["..."],
     "modelAnswers": [
       { "question": "...", "candidateAnswer": "...", "betterAnswer": "..." }
     ]
   }
   ```
7. **Decide the visual identity**: pick a color palette and font pairing now so every later day builds toward one consistent look (e.g., navy + ice-blue + a warm gold accent, per the pitch deck; Tailwind's default font stack is fine).

### 📂 Files and folders to create or modify
- `DESIGN.md` — screen flow, wireframe notes, palette decision
- `PROMPTS.md` — draft system prompts for all 3 tones
- `API_CONTRACTS.md` — the 5 API route contracts above, request/response shapes

### 🔗 APIs, libraries, services, or tools to integrate
None installed yet — this is design-only. Just confirm you have (or can get) a free Anthropic API key for Day 4+.

### 🧪 Testing tasks
- Sanity-check each persona prompt by mentally role-playing 2–3 exchanges — does "Tough" actually sound tougher than "Standard"?
- Walk through the full screen flow end-to-end on paper — does every screen have a clear "next" action?

### 🐞 Common issues and debugging tips
- If the adaptive question-count logic feels too complex, simplify: start with a flat range (e.g., always target 8, ±2 based on one simple signal like "JD provided or not") and refine later — don't over-engineer Day 2.

### ✅ End-of-day checklist
- [ ] `DESIGN.md`, `PROMPTS.md`, `API_CONTRACTS.md` created and committed to a local folder (repo comes Day 3)
- [ ] All 5 screens sketched/described
- [ ] All 3 tone prompts drafted
- [ ] Feedback JSON schema locked
- [ ] Color palette and font decision made

### 📸 Expected project state and screenshots to capture
- No running app yet. Capture: the wireframe sketch/notes and the three drafted prompts as your "before code" artifact.

### ➡️ Handoff notes for the next day
Day 3 starts a **brand-new AI conversation**. Give it: this blueprint file, `DESIGN.md`, `PROMPTS.md`, and `API_CONTRACTS.md`. Day 3's job is pure scaffolding — creating the repo, installing dependencies, and deploying a "hello world" version to Vercel to validate the deployment pipeline before any real feature work begins.

---

## Day 3 — ⚙️ Setup & Project Scaffolding

### 🎯 Objective
Stand up the Next.js project, install all core dependencies, set up GitHub + Vercel, and get a bare-bones "hello world" version successfully deployed live — so the deployment pipeline is proven working before any real feature is built.

### 📖 What I'll learn
- Scaffolding a Next.js + Tailwind project from scratch
- Managing environment variables/secrets safely
- Connecting a GitHub repo to Vercel for continuous deployment

### 🛠 Features to build
- Empty but running app shell with routing for all 5 screens (placeholder content only)
- Live deployment on Vercel

### 📝 Step-by-step implementation plan
1. Create the Next.js app: `npx create-next-app@latest crackit-ai-interview` — choose: JavaScript (not TypeScript), Tailwind CSS = Yes, App Router = Yes, `src/` directory = Yes (your choice, stay consistent).
2. `cd crackit-ai-interview` and verify it runs locally: `npm run dev` → check `http://localhost:3000`.
3. Install feature dependencies now (even though unused today), so Day 4+ has zero setup friction:
   ```bash
   npm install @anthropic-ai/sdk pdf-parse mammoth @react-pdf/renderer
   ```
4. Create the app route structure with placeholder pages (just a heading on each for now):
   - `src/app/page.js` → Landing screen
   - `src/app/setup/page.js` → Resume + JD input screen
   - `src/app/interview/page.js` → Chat/interview screen
   - `src/app/results/page.js` → Feedback + report screen
5. Create empty API route files (return a placeholder `{ status: "ok" }` for now):
   - `src/app/api/parse-resume/route.js`
   - `src/app/api/interview/start/route.js`
   - `src/app/api/interview/next/route.js`
   - `src/app/api/feedback/route.js`
   - `src/app/api/generate-report/route.js`
6. Create `.env.local` with `ANTHROPIC_API_KEY=your-key-here` and add `.env.local` to `.gitignore` (verify it's already there — Next.js adds it by default).
7. Initialize git, create a **private** GitHub repo, push the initial commit.
8. Connect the GitHub repo to Vercel (import project → framework auto-detected as Next.js) and deploy.
9. Add `ANTHROPIC_API_KEY` as an environment variable inside the Vercel project settings (Production + Preview).
10. Confirm the live Vercel URL loads all placeholder pages correctly.

### 📂 Files and folders to create or modify
```
crackit-ai-interview/
├── src/app/
│   ├── page.js
│   ├── setup/page.js
│   ├── interview/page.js
│   ├── results/page.js
│   └── api/
│       ├── parse-resume/route.js
│       ├── interview/start/route.js
│       ├── interview/next/route.js
│       ├── feedback/route.js
│       └── generate-report/route.js
├── .env.local
├── .gitignore
├── package.json
```

### 🔗 APIs, libraries, services, or tools to integrate
- Anthropic API key (free/low-cost tier — get one from the Anthropic Console)
- GitHub (new repo)
- Vercel (new project, linked to the repo)

### 🧪 Testing tasks
- Local dev server runs without errors (`npm run dev`)
- All 5 placeholder pages render at their routes locally
- All 5 placeholder API routes return a 200 response (test with browser or `curl`)
- Live Vercel URL matches local behavior

### 🐞 Common issues and debugging tips
- **Vercel deploy fails on build:** check the build logs for a missing dependency or a typo in an import path — Next.js build errors are usually very specific.
- **API key not found in production:** confirm the env var was added in Vercel *and* redeploy — env var changes don't apply retroactively to old deployments.
- **`.env.local` accidentally committed:** if it happens, rotate the API key immediately and add the file to `.gitignore` properly.

### ✅ End-of-day checklist
- [ ] Next.js + Tailwind project created and runs locally
- [ ] All dependencies installed (`@anthropic-ai/sdk`, `pdf-parse`, `mammoth`, `@react-pdf/renderer`)
- [ ] All 5 page routes and 5 API routes exist (placeholder content is fine)
- [ ] GitHub repo created and pushed
- [ ] Vercel project created, deployed, and live at a public URL
- [ ] `ANTHROPIC_API_KEY` set in both `.env.local` and Vercel env vars

### 📸 Expected project state and screenshots to capture
- Screenshot of the live Vercel URL showing the placeholder Landing page
- Screenshot of the Vercel dashboard showing a successful deployment

### ➡️ Handoff notes for the next day
Day 4 starts a **new AI conversation**. Give it: this blueprint, `DESIGN.md`, `API_CONTRACTS.md`, and the repo (or a description of its current file structure). The project is scaffolded and deployed but has no real functionality yet. Day 4 builds the first real feature: resume + JD input with file parsing.

---

## Day 4 — 📄 Resume & Job Description Input

### 🎯 Objective
Build the fully working "Setup" screen: paste-or-upload resume input with real PDF/DOCX parsing, optional job title + job description fields, and validation — the first real end-to-end feature.

### 📖 What I'll learn
- Handling file uploads in a Next.js API route
- Extracting text from PDF and DOCX server-side
- Designing graceful fallback UX when automated parsing fails

### 🛠 Features to build
- Resume paste textbox
- Resume file upload (PDF/DOCX) with drag-and-drop or file picker
- Automatic text extraction from uploaded files
- Fallback prompt to paste text if extraction fails or yields too little content
- Optional job title + job description textboxes
- "Continue" button that validates a resume is present before proceeding to tone selection

### 📝 Step-by-step implementation plan
1. Build the `/setup` page UI: a tab or toggle between "Paste resume" and "Upload resume", a textarea for pasted text, a file input for upload, and two optional fields for job title and job description below.
2. Implement `POST /api/parse-resume`:
   - Accept `multipart/form-data` with the uploaded file.
   - If `.pdf`: use `pdf-parse` to extract text.
   - If `.docx`: use `mammoth` to extract text.
   - If extracted text is under ~100 characters or extraction throws an error, return `{ success: false, reason: "..." }` so the frontend can show the paste fallback prompt.
   - On success, return `{ success: true, text: "..." }`.
3. Wire the `/setup` page: on file upload, call `/api/parse-resume`, show a loading state, then either populate the textarea with extracted text (editable) or show an inline message: *"We couldn't read that file automatically — please paste your resume text below."*
4. Add basic client-side validation: file type restricted to `.pdf`/`.docx`, file size capped (e.g., 5MB), and the "Continue" button disabled until resume text (pasted or extracted) is non-empty.
5. Persist the collected input (resume text, job title, job description) in React state (e.g., lifted to a parent layout or a simple context) so it survives navigation to the Tone Selection and Interview screens without a database.
6. Style the screen with Tailwind to match the Day 2 palette decision — this is the user's first real impression, worth 20–30 extra minutes of polish.

### 📂 Files and folders to create or modify
- `src/app/setup/page.js` (full implementation)
- `src/app/api/parse-resume/route.js` (full implementation)
- `src/context/SessionContext.js` (new — simple React context to hold resume text, JD, tone, transcript across pages)
- `src/app/layout.js` (wrap the app in `SessionContext.Provider`)

### 🔗 APIs, libraries, services, or tools to integrate
- `pdf-parse` for PDF text extraction
- `mammoth` for DOCX text extraction
- Native `FormData` / `fetch` for file upload from the client

### 🧪 Testing tasks
- Upload a real PDF resume → confirm extracted text looks correct
- Upload a real DOCX resume → confirm extracted text looks correct
- Upload a corrupted or image-only (scanned) PDF → confirm graceful fallback message appears, not a crash
- Paste resume text directly → confirm it flows through correctly
- Leave resume empty → confirm "Continue" stays disabled
- Enter a job title/description → confirm both are optional and don't block continuation

### 🐞 Common issues and debugging tips
- **`pdf-parse` throws on certain PDFs:** wrap extraction in try/catch and always fall back to the paste prompt rather than letting the API route 500.
- **Next.js API routes and file uploads:** make sure you're reading the incoming file as a buffer correctly (`request.formData()` in the App Router, then `file.arrayBuffer()` → `Buffer.from(...)`) — this trips people up on the first attempt.
- **Extracted text has weird spacing/line breaks:** don't over-engineer cleanup on Day 4; basic whitespace normalization is enough, since the AI in Day 5 is tolerant of messy input.

### ✅ End-of-day checklist
- [ ] Paste and upload both work for resume input
- [ ] PDF and DOCX extraction both verified with real files
- [ ] Fallback-to-paste flow verified with a deliberately broken/scanned file
- [ ] Job title + job description fields present and optional
- [ ] Session state (resume, JD, title) persists across page navigation
- [ ] Screen is styled and matches the chosen palette

### 📸 Expected project state and screenshots to capture
- Screenshot of the Setup screen with a resume pasted
- Screenshot of a successful PDF upload with extracted text shown
- Screenshot of the fallback message triggered by a bad file

### ➡️ Handoff notes for the next day
Day 5 starts a **new AI conversation**. Give it: this blueprint, `PROMPTS.md`, `API_CONTRACTS.md`, and note that resume/JD input is fully working and stored in `SessionContext`. Day 5 builds the Tone Selection screen and the core adaptive AI interview engine (the heart of the product).

---

## Day 5 — 🤖 Adaptive AI Interview Engine

### 🎯 Objective
Build the Tone Selection screen and the full interview chat experience: a multi-turn, adaptive, persona-driven conversation with the Claude API that questions the resume against the (optional) job description.

### 📖 What I'll learn
- Designing multi-turn conversational prompts with a persistent persona
- Managing conversation state client-side across multiple API calls
- Calling the Claude API from a Next.js API route with structured system prompts

### 🛠 Features to build
- Tone Selection screen (Friendly / Standard / Tough)
- Chat-style Interview screen with AI questions and user text responses
- Adaptive question count logic (6–12, capped)
- Progress indicator (e.g., "Question 4 of ~8")
- "Interview complete" transition to the Results screen

### 📝 Step-by-step implementation plan
1. Build the `/interview/tone` selection UI (or fold it into the top of `/interview` — your call): three cards (Friendly, Standard, Tough) with a one-line description each; selecting one stores `tone` in `SessionContext` and starts the interview.
2. Implement `POST /api/interview/start`:
   - Input: `{ resumeText, jobTitle, jobDescription, tone }`.
   - Build the system prompt by combining the base interviewer instructions with the tone-specific prompt from `PROMPTS.md`, and inject the resume text + JD (if present).
   - Estimate a target question count (per Day 2's design) and return it as part of `sessionContext`.
   - Call the Claude API once to generate the **first question only**.
   - Return `{ question: "...", sessionContext: { tone, targetQuestionCount, questionIndex: 1 } }`.
3. Implement `POST /api/interview/next`:
   - Input: the full `transcript` (array of `{ role: "interviewer"|"candidate", text }`) plus `sessionContext`.
   - If `questionIndex >= targetQuestionCount`, return `{ interviewComplete: true }` instead of calling the API again.
   - Otherwise, send the full transcript + system prompt back to Claude, instructing it to ask exactly one natural follow-up question based on the candidate's last answer.
   - Return `{ question: "...", sessionContext: { ...updated questionIndex } }`.
4. Build the `/interview` chat UI: a scrolling message list (interviewer questions left-aligned, candidate answers right-aligned), a text input + send button, and a progress bar/counter.
5. Wire the chat flow: on mount, call `/api/interview/start`; on each candidate submission, append to `transcript` in `SessionContext`, call `/api/interview/next`, append the AI's next question (or redirect to `/results` if `interviewComplete`).
6. Add a lightweight loading indicator ("Interviewer is thinking...") during each API call, and basic error handling (e.g., a retry button if a call fails).

### 📂 Files and folders to create or modify
- `src/app/interview/page.js` (full chat implementation, includes or precedes tone selection)
- `src/app/api/interview/start/route.js` (full implementation)
- `src/app/api/interview/next/route.js` (full implementation)
- `src/lib/prompts.js` (new — exports the 3 tone system prompts + the shared base interviewer instructions, based on `PROMPTS.md`)
- `src/lib/claude.js` (new — small wrapper around the `@anthropic-ai/sdk` client so it's not duplicated across routes)

### 🔗 APIs, libraries, services, or tools to integrate
- `@anthropic-ai/sdk` — calling the Claude API from server-side API routes only (never expose the API key client-side)

### 🧪 Testing tasks
- Run a full interview in each of the 3 tones with the same resume — confirm the tone/pressure genuinely differs
- Run one interview with a JD provided and one without — confirm JD-provided questions reference the job description specifics
- Confirm the question counter increments correctly and the interview stops at the adaptive cap
- Test with a very short, sparse resume vs. a long, detailed one — confirm the adaptive count reacts differently
- Force an API error (e.g., temporarily use an invalid key) — confirm the UI shows a friendly retry message, not a crash

### 🐞 Common issues and debugging tips
- **AI asks multiple questions in one turn:** tighten the system prompt with an explicit instruction like "Ask exactly ONE question. Do not ask multiple questions in the same turn."
- **AI loses track of the resume/JD context in later turns:** always resend the full system prompt (not just the transcript) on every `/next` call — don't rely on model memory across separate API calls.
- **Conversation feels scripted/repetitive:** make sure the system prompt explicitly instructs the model to reference the candidate's *previous answer* when forming the next question, not just the resume.

### ✅ End-of-day checklist
- [ ] Tone selection screen implemented and functional
- [ ] Interview chat UI implemented with working message flow
- [ ] `/api/interview/start` and `/api/interview/next` fully working
- [ ] Adaptive question cap verified with at least 2 different resume lengths
- [ ] All 3 tones tested and behave distinctly
- [ ] Loading and error states implemented

### 📸 Expected project state and screenshots to capture
- Screenshot of the Tone Selection screen
- Screenshot of an in-progress interview conversation
- Screenshot of the interview reaching "complete" state

### ➡️ Handoff notes for the next day
Day 6 starts a **new AI conversation**. Give it: this blueprint, the feedback JSON schema from `DESIGN.md`, and note that a full transcript is available in `SessionContext` by the time the interview completes. Day 6 builds the feedback/scoring engine that consumes that transcript.

---

## Day 6 — 📊 Feedback & Scoring Engine

### 🎯 Objective
Build the `/api/feedback` endpoint that analyzes the full interview transcript and generates structured, category-wise scores plus written feedback and model answers, and build the Results screen that displays it.

### 📖 What I'll learn
- Prompting an LLM to return reliable, structured JSON output
- Designing a results UI that presents scores and feedback clearly
- Handling and validating AI-generated structured data safely

### 🛠 Features to build
- `/api/feedback` endpoint
- Results screen: score visualization, strengths/weaknesses, suggestions, model answers
- "Download Report" button (wired to a placeholder for now — real PDF comes Day 7)

### 📝 Step-by-step implementation plan
1. Implement `POST /api/feedback`:
   - Input: full `transcript`, `resumeText`, `jobDescription` (if any), `tone`.
   - Construct a system prompt instructing Claude to act as an interview evaluator and return **only** valid JSON matching the exact schema from `DESIGN.md` (scores 0–100 per category, strengths array, weaknesses array, suggestions array, modelAnswers array referencing the 2–3 weakest exchanges).
   - Call Claude, then parse the response as JSON. Wrap parsing in try/catch — if it fails, strip any accidental markdown code fences (```json ... ```) before re-attempting, per standard practice.
   - Return the parsed feedback object to the client.
2. Build the `/results` page UI:
   - **Score section:** 6 category scores as simple progress bars or radial indicators with numeric values (0–100).
   - **Strengths / Weaknesses:** two clearly separated lists.
   - **Suggestions:** a short, scannable list of specific, actionable tips.
   - **Model Answers:** for each of the 2–3 weakest exchanges, show the original question, the candidate's answer, and the AI's suggested better answer, in a clear before/after layout.
3. On the Results screen mount, call `/api/feedback` with the completed transcript from `SessionContext`, show a loading state while scoring happens, then render the results.
4. Add a "Download Report (PDF)" button — for today, it can call a stub function or show a "coming tomorrow" placeholder if you're short on time; full PDF wiring happens Day 7.
5. Style the Results screen with the same palette — this is the "payoff" screen, so give it clear visual hierarchy (scores should be the most prominent element).

### 📂 Files and folders to create or modify
- `src/app/api/feedback/route.js` (full implementation)
- `src/app/results/page.js` (full implementation)
- `src/lib/prompts.js` (add the evaluator/scoring system prompt)

### 🔗 APIs, libraries, services, or tools to integrate
- `@anthropic-ai/sdk` (same client wrapper from Day 5)

### 🧪 Testing tasks
- Run feedback generation against 2–3 different completed transcripts (varying quality of candidate answers) — confirm scores meaningfully differ (a strong performance should score higher than a weak one)
- Confirm the JSON always parses correctly across at least 5 test runs; if it fails even once, tighten the prompt's "return ONLY JSON" instruction
- Confirm all 6 categories always appear with values in a sensible 0–100 range
- Confirm model answers reference real questions from the transcript, not invented ones

### 🐞 Common issues and debugging tips
- **AI wraps JSON in markdown fences or adds commentary:** explicitly instruct "Respond with raw JSON only. No markdown, no code fences, no explanation before or after." Also defensively strip ` ```json` / ` ``` ` if present before parsing.
- **Scores cluster around the same number every time (e.g., always 70):** add explicit instruction to differentiate based on transcript evidence, and consider a few-shot example in the prompt showing a high-scoring vs. low-scoring exchange.
- **JSON parsing crashes the page:** always wrap the fetch + parse in try/catch on the frontend too, and show a friendly "couldn't generate your report, please retry" state rather than a blank screen.

### ✅ End-of-day checklist
- [ ] `/api/feedback` returns valid, well-differentiated structured JSON reliably
- [ ] Results page displays all 6 scores clearly
- [ ] Strengths, weaknesses, suggestions all rendering correctly
- [ ] Model answers section shows question / candidate answer / better answer
- [ ] Page handles loading and error states gracefully

### 📸 Expected project state and screenshots to capture
- Screenshot of the full Results screen with real scores and feedback
- Screenshot of the Model Answers section

### ➡️ Handoff notes for the next day
Day 7 starts a **new AI conversation**. Give it: this blueprint and note that `/results` fully displays feedback in-browser, and the feedback JSON shape is confirmed working end-to-end. Day 7's job is to turn that same data into a downloadable, polished PDF report.

---

## Day 7 — 🧾 PDF Report Generation

### 🎯 Objective
Build the `/api/generate-report` endpoint that turns the feedback JSON + transcript into a professional, ATS-style downloadable PDF, and wire the "Download Report" button to it.

### 📖 What I'll learn
- Generating PDFs server-side from React components using `@react-pdf/renderer`
- Designing a clean, print-friendly document layout
- Streaming binary file responses from a Next.js API route

### 🛠 Features to build
- PDF report template (header, candidate summary, scores, strengths/weaknesses, suggestions, model answers, footer)
- Working "Download Report" button that triggers a real PDF download

### 📝 Step-by-step implementation plan
1. Design the PDF layout on paper first: title/header with "CrackIt Interview Report", session metadata (target role if provided, date), a scores table/section, strengths/weaknesses side-by-side, suggestions list, and a model-answers section — in that order.
2. Build React-PDF components using `@react-pdf/renderer` primitives (`Document`, `Page`, `View`, `Text`, `StyleSheet`) — this is a distinct component tree from your normal UI, not reused directly, since react-pdf has its own primitives.
3. Implement `POST /api/generate-report`:
   - Input: the feedback JSON, transcript, resume metadata (job title if provided).
   - Render the PDF document via `@react-pdf/renderer`'s server-side render-to-buffer/stream function.
   - Return the PDF with headers `Content-Type: application/pdf` and `Content-Disposition: attachment; filename="CrackIt_Report.pdf"`.
4. Wire the "Download Report" button on `/results`: on click, call `/api/generate-report` with the current session's feedback + transcript, receive the binary response, and trigger a browser download (e.g., via a Blob + temporary `<a>` element).
5. Polish the PDF's visual design to feel "ATS-style" — clean serif/sans header, clear section dividers, no clutter — matching the palette chosen on Day 2 as much as `@react-pdf/renderer`'s styling allows.
6. Test with a genuinely long transcript (12 questions, verbose answers) to confirm the PDF paginates correctly instead of overflowing or cutting off content.

### 📂 Files and folders to create or modify
- `src/app/api/generate-report/route.js` (full implementation)
- `src/lib/pdf/ReportDocument.js` (new — the `@react-pdf/renderer` document component)
- `src/app/results/page.js` (wire the real download action)

### 🔗 APIs, libraries, services, or tools to integrate
- `@react-pdf/renderer`

### 🧪 Testing tasks
- Generate a report from a short interview (6 questions) — confirm correct pagination
- Generate a report from a long interview (12 questions, long answers) — confirm no content is cut off or overlapping across pages
- Confirm the downloaded file opens correctly in a standard PDF viewer
- Confirm the filename and content-type are correct in the browser download

### 🐞 Common issues and debugging tips
- **Content overflows a page awkwardly:** `@react-pdf/renderer` auto-paginates `View`/`Text` elements reasonably well, but test with realistic long content early rather than only with short placeholder text.
- **Fonts look default/plain:** register a custom font via `Font.register` if you want something beyond the built-in Helvetica — optional polish, don't let it block progress.
- **Download doesn't trigger in the browser:** double-check you're creating an object URL from the Blob response and revoking it after triggering the click, a common gotcha with binary downloads via `fetch`.

### ✅ End-of-day checklist
- [ ] PDF report template built and styled
- [ ] `/api/generate-report` returns a valid downloadable PDF
- [ ] Download button works end-to-end from the Results screen
- [ ] Tested with both short and long interview transcripts
- [ ] PDF opens correctly and looks professional

### 📸 Expected project state and screenshots to capture
- Screenshot of the downloaded PDF report (multiple pages if applicable)
- Screenshot of the Results screen with the working Download button

### ➡️ Handoff notes for the next day
Day 8 starts a **new AI conversation**. Give it: this blueprint and note that the full end-to-end flow (Setup → Tone → Interview → Results → PDF Download) works. Day 8 is dedicated entirely to testing, edge cases, and polish — no new features.

---

## Day 8 — 🧪 Testing, Edge Cases & Polish

### 🎯 Objective
Harden the full end-to-end flow against real-world edge cases, fix bugs, and polish the UI/UX — no new features today, only quality.

### 📖 What I'll learn
- Systematic end-to-end testing of a multi-step web app
- Identifying and handling edge cases before they become demo-day failures
- UI polish techniques (loading states, empty states, responsive layout)

### 🛠 Features to build
None new — this day is entirely about hardening what exists.

### 📝 Step-by-step implementation plan
1. Run through the full flow at least 5 times end-to-end with different inputs:
   - A strong, detailed resume + a matching JD
   - A sparse, thin resume + no JD
   - A resume with a career gap or inconsistency
   - A resume pasted with messy formatting/line breaks
   - A resume uploaded as PDF, then again as DOCX
2. Test every edge case explicitly and fix what breaks:
   - Empty resume submission attempt (should be blocked client-side)
   - Corrupted/unsupported file upload (should trigger the paste fallback, not a crash)
   - Extremely short candidate answers during the interview (e.g., "yes"/"no") — confirm the AI still asks a sensible follow-up rather than breaking
   - Network/API failure mid-interview (simulate by briefly using an invalid key) — confirm a retry option appears
   - Very long job description pasted (a full multi-paragraph JD) — confirm no input or prompt-length issues
3. Add or improve loading states anywhere they're missing (file parsing, each interview turn, feedback generation, PDF generation) so the user always has visual feedback that something is happening.
4. Add a simple, friendly empty/landing state if not already polished (clear headline, one-line explanation of what CrackIt does, a clear "Start" call to action).
5. Check responsive layout on a mobile-width browser window for all 5 screens — fix any obvious breakage (this is a nice-to-have, not a blocker, if time is tight).
6. Do a full visual pass: consistent spacing, consistent button styles, consistent color usage across all screens per the Day 2 palette decision.
7. Write a short `README.md` for the repo: what the project is, tech stack, how to run locally, and a link to the live deployment.

### 📂 Files and folders to create or modify
- Any files touched while fixing bugs (likely across `setup/`, `interview/`, `results/`, and the API routes)
- `README.md` (new)

### 🔗 APIs, libraries, services, or tools to integrate
None new.

### 🧪 Testing tasks
- All 5 scenarios in step 1 run successfully end-to-end
- All edge cases in step 2 handled gracefully (no blank crashes, no unhandled console errors)
- Loading states present at every async step
- Mobile-width layout doesn't visibly break (best-effort)

### 🐞 Common issues and debugging tips
- **Bugs found late feel overwhelming:** triage by severity — fix anything that fully breaks the flow first (crashes, dead ends); cosmetic issues can wait until time allows.
- **AI behavior inconsistent across edge cases:** if very short answers cause odd AI behavior, add an explicit prompt instruction: "If the candidate's answer is very brief or evasive, ask a clarifying follow-up rather than moving on."
- **Too many small polish items to track:** keep a running bug list in a scratch file and check items off as you fix them, rather than fixing ad hoc and losing track.

### ✅ End-of-day checklist
- [ ] 5 full end-to-end test runs completed successfully
- [ ] All edge cases from step 2 tested and handled gracefully
- [ ] Loading states present everywhere needed
- [ ] Visual consistency pass completed
- [ ] `README.md` written
- [ ] No known crashing bugs remain

### 📸 Expected project state and screenshots to capture
- Screenshot of at least one handled edge case (e.g., the fallback message, or a retry state)
- Screenshot of the polished landing page

### ➡️ Handoff notes for the next day
Day 9 starts a **new AI conversation**. Give it: this blueprint and note that the app is feature-complete, tested, and already deployed on Vercel from Day 3 (redeploys have been happening automatically on every push since). Day 9 focuses on a proper production deployment review, environment hardening, and final smoke testing — not a from-scratch deployment.

---

## Day 9 — 🚀 Deployment Hardening & Production Verification

### 🎯 Objective
Treat today as the "go live for real" day: verify the production deployment is fully correct, secure, and reliable, and do a final smoke test of the live URL exactly as a judge or recruiter would experience it.

### 📖 What I'll learn
- Production environment configuration best practices
- How to smoke-test a deployed app methodically
- Basic web app security hygiene (secrets, input limits)

### 🛠 Features to build
None new — this day verifies and hardens the existing deployed app.

### 📝 Step-by-step implementation plan
1. Confirm the latest code (with all Day 4–8 work) is pushed to GitHub's main branch and that Vercel has auto-deployed the latest commit — check the Vercel dashboard's deployment log.
2. Re-verify environment variables in the Vercel project settings: `ANTHROPIC_API_KEY` present and correct, no accidental exposure of secrets in client-side code (search the codebase for any place the key might be referenced outside API routes).
3. Set sensible input limits in the API routes if not already present: max resume text length, max job description length, max file upload size — to protect against accidental abuse or unexpectedly expensive API calls.
4. Do a **cold, from-scratch smoke test**: open the live URL in a private/incognito window (no cached state) and run through the entire flow once, exactly as a first-time visitor would, timing how long each step takes.
5. Check the Vercel free-tier limits (function execution time, bandwidth) against your expected usage — confirm you're comfortably within them for a demo/portfolio-traffic level of usage.
6. If a custom-feeling URL is desired and available for free on your Vercel plan, set it up (e.g., a cleaner Vercel subdomain); otherwise the default `*.vercel.app` URL is perfectly fine.
7. Optional (only if time allows and Day 4–8 are fully solid): begin the voice input/output stretch goal groundwork here, but do **not** let it risk the core deployment's stability — this is explicitly a "bonus if time permits" item, not a Day 9 requirement.

### 📂 Files and folders to create or modify
- Minor edits only, likely within existing API routes (adding input length validation) if not already present from Day 8.

### 🔗 APIs, libraries, services, or tools to integrate
None new.

### 🧪 Testing tasks
- Full cold smoke test in an incognito window, timing each step
- Confirm no console errors appear in the browser dev tools during a full run
- Confirm the API key and any other secrets are not visible anywhere in client-side network requests (check the Network tab in dev tools)
- Confirm input length limits reject absurdly long pastes gracefully rather than erroring

### 🐞 Common issues and debugging tips
- **Works locally but not in production:** almost always an environment variable mismatch — double check Vercel's env vars match `.env.local` exactly.
- **Cold start feels slow on first request:** this is normal for serverless free tiers; if it's noticeably disruptive for a demo, do a "warm-up" request a minute or two before presenting live.
- **Function timeout on longer AI calls:** check Vercel's free-tier function timeout limit and make sure your Claude API calls comfortably finish within it; if not, consider trimming max tokens on the feedback/report generation calls.

### ✅ End-of-day checklist
- [ ] Latest code confirmed live on Vercel
- [ ] Environment variables verified correct and secure
- [ ] Input length limits in place on all relevant API routes
- [ ] Full cold smoke test completed successfully with no console errors
- [ ] Confirmed comfortably within Vercel free-tier limits

### 📸 Expected project state and screenshots to capture
- Screenshot of the Vercel deployment dashboard showing a successful production deployment
- Screenshot of a full cold smoke-test run of the live URL

### ➡️ Handoff notes for the next day
Day 10 starts a **new AI conversation**. Give it: this blueprint, and note that the app is fully deployed, hardened, and smoke-tested. Day 10 is the final polish, bug-bash, and demo-preparation day — the last day before presenting to judges.

---

## Day 10 — 🏁 Final Polish, Demo Prep & Submission

### 🎯 Objective
Close out the capstone: final bug bash, last-mile UI polish, prepare and rehearse a demo script, finalize all supporting materials (PRD, blueprint, pitch deck already exist — just confirm they're current), and confidently submit/present a polished, deployed v1.0.

### 📖 What I'll learn
- How to prepare and rehearse a compelling product demo
- Final-mile quality bar-raising on a nearly-finished product
- Making a disciplined stretch-goal call under time pressure

### 🛠 Features to build
- No mandatory new features.
- **Optional stretch goal (only if the core product is fully solid and time genuinely remains):** basic voice input using the browser's Web Speech API for candidate answers, and/or text-to-speech for AI questions. This must be additive and never risk breaking the reliable text-based core — implement behind a simple toggle, and be ready to disable/hide it instantly if it's flaky.

### 📝 Step-by-step implementation plan
1. Do one final full end-to-end run-through and fix any last bugs found (should be minor, given Day 8's hardening).
2. Prepare a **demo script**: a specific example resume + JD you'll use live (rehearsed, not improvised), the tone you'll demo (Standard or Tough shows the concept best), and a clear narrative: problem → live demo → report → future vision.
3. Rehearse the demo at least twice, timing it, ideally showing: (a) the resume/JD input, (b) 2–3 real interview exchanges, (c) jumping to a pre-completed session's Results screen and PDF (to avoid waiting live through a full 8-question interview during the demo).
4. Prepare a fallback: take screenshots or a short screen-recording of a full successful run, in case of live demo issues (network hiccup, cold start) during actual presentation.
5. Review the PRD, Implementation Blueprint, and Pitch Deck (from Day 1) for accuracy against what was actually built — note any deviations honestly rather than silently, since judges may ask about them.
6. **Only if steps 1–5 are done and time remains:** attempt the voice stretch goal behind a toggle, test it thoroughly, and be willing to cut it from the demo if it's not rock-solid.
7. Do a final live smoke test of the production URL right before presenting/submitting.
8. Submit according to the AB Talks Challenge's submission requirements (repo link, live URL, and the three Day 1 deliverables).

### 📂 Files and folders to create or modify
- Minor bug fixes only, plus optionally `src/components/VoiceToggle.js` and related Web Speech API wiring if the stretch goal is attempted.
- `DEMO_SCRIPT.md` (new — your rehearsed talking points and example resume/JD to use live)

### 🔗 APIs, libraries, services, or tools to integrate
- (Optional stretch only) Browser-native **Web Speech API** (`SpeechRecognition` for input, `SpeechSynthesis` for output) — free, no external service needed, but has inconsistent browser support (best in Chrome).

### 🧪 Testing tasks
- Full rehearsed demo run-through, timed, at least twice
- Final live smoke test of the production URL immediately before presenting
- (If attempted) voice stretch goal tested in isolation before being added to the live demo plan

### 🐞 Common issues and debugging tips
- **Live demo anxiety about API latency:** pre-warm the deployed app a few minutes before presenting, and have the fallback screen-recording ready regardless.
- **Web Speech API inconsistent across browsers:** if attempting the stretch goal, test specifically in the browser you'll demo with, and don't rely on it working universally — keep it optional/toggleable.
- **Last-minute scope temptation:** if a "just one more feature" urge appears today, resist it — Day 10's job is polish and confidence, not new scope.

### ✅ End-of-day checklist
- [ ] Final end-to-end bug bash complete
- [ ] Demo script written and rehearsed at least twice
- [ ] Fallback screenshots/recording prepared
- [ ] PRD, Blueprint, and Pitch Deck reviewed for accuracy
- [ ] (Optional) voice stretch goal implemented and tested, or consciously deferred
- [ ] Final live smoke test passed
- [ ] Project submitted per AB Talks Challenge requirements

### 📸 Expected project state and screenshots to capture
- Screenshots/recording of the full rehearsed demo flow
- Final screenshot of the live, deployed v1.0 product

### ➡️ Handoff notes for the next day
There is no Day 11 in this capstone — this is the finish line. If you continue past submission, the natural next step is the v2 Future Scope list in the PRD (accounts, shareable links, voice as a first-class feature, broader role support).

---

## Appendix: Standing Reminders for Every Day

- **No day should require re-choosing the tech stack or re-architecting.** If a fresh AI conversation starts questioning the stack in Section 0, redirect it back to this blueprint.
- **Always keep the paste-resume fallback working** — it's the reliability backbone of the whole product.
- **Never let a single day's scope expand into "while I'm here, let me also add..."** — if a good idea comes up mid-build, write it into the Future Scope list and stay on task.
- **Commit and push at the end of every day**, even if a feature is only partially done — Vercel's auto-deploy from Day 3 onward means the live URL should reflect real progress daily.
