# Day 55 — Capstone Day 5: Adaptive AI Interview Engine

## What I Built Today
Built the Tone Selection screen and the full adaptive, multi-turn AI interview engine for CrackIt — the core "wow" feature of the whole product.

- Switched the AI engine from the originally-planned Anthropic Claude API to Google Gemini API, since Gemini offers a genuinely free tier with no billing account ever required
- Built lib/gemini.js (AI client) and lib/prompts.js (base interviewer rules, 3 tone personas, adaptive question-count logic, feedback prompt prepared for Day 6)
- Built /api/interview/start and /api/interview/next with real multi-turn Gemini calls
- Built the Tone Selection screen (Friendly / Standard / Tough) and full chat UI
- Verified a complete multi-turn interview end-to-end, both locally and in production: resume-aware questions, tone-correct persona, adaptive follow-ups, correct progress tracking, correct transition to /results

## Key Learnings
1. **A real architecture conflict is worth stopping for.** The original plan used Anthropic's Claude API, but it requires eventual billing setup. Flagging this conflict before writing code — instead of silently building around it — led to a better decision (Gemini's genuinely free tier) instead of a workaround.
2. **Isolate external API config behind one file.** Because the model name lived in exactly one constant (lib/gemini.js), a mid-build model deprecation (gemini-2.5-flash became unavailable to new projects) was a one-line fix instead of a multi-file hunt.
3. **"Works on localhost" and "builds for production" are different tests.** A stray duplicate page.js file in the wrong folder didn't break local dev but did break npm run build — always run a full production build before considering a feature done.
4. **Multi-turn AI conversations need the full transcript resent every call.** With no server-side session, each API call is the AI's only "memory" — the entire conversation history has to be passed every time for follow-up questions to make sense.

## Screenshots
See attached: live multi-turn interview conversation showing resume-aware, adaptive questioning.

## Documentation
Updated docs reflecting the Gemini API swap are attached in this folder: ARCHITECTURE.md, API.md, ENVIRONMENT.md, SETUP.md, PROJECT-STRUCTURE.md, PROJECT-LOG.md

## LinkedIn Graphics
Two versions created showcasing today's one-line refactor fix (bold dark and friendly light variants), attached in this folder.

## Live Links
- **Live app:** https://crackit-ai-interview.vercel.app/interview
- **Project repo:** https://github.com/ayushman6684/crackit-ai-interview

## Tomorrow's Goal
Day 6: build the feedback and scoring engine — /api/feedback and the real /results screen with category scores, strengths/weaknesses, suggestions, and model answers.
