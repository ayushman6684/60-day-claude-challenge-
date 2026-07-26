# Day 56 — Capstone Day 6: Feedback & Scoring Engine (Core MVP Complete)

## What I Built Today
Completed the core MVP loop for CrackIt: Setup -> Interview -> Feedback, fully working end-to-end, live in production.

- Built /api/feedback: real Gemini-powered scoring across 6 categories (Resume Credibility, Technical Knowledge, Communication, Problem Solving, Confidence, Resume-JD Fit), strengths, weaknesses, suggestions, and model answers
- Built the real /results screen with visual score bars, styled consistently with the rest of the app
- Added the required site-wide footer ("Built with Claude as part of the AB Talks 60-Day Claude AI Challenge"), confirmed visible on the live deployed site
- Hardened the Gemini client with automatic retry (3 attempts, increasing backoff) and automatic fallback to a lighter model if the primary model is under heavy free-tier demand
- Found and fixed a real scoring bug: Gemini intermittently returned scores on a 0-10 scale instead of the required 0-100 scale -- fixed with a stricter prompt plus a server-side safety net
- Verified the complete flow on both localhost and the live Vercel deployment, with both a weak-performance test (scored correctly low) and a strong-performance test (scored correctly high, 85-90 range)

## Key Learnings
1. **Free-tier AI APIs need resilience built in, not assumed.** A brief Gemini capacity spike (503 errors) fully blocked the interview flow until I added automatic retry with backoff and a fallback to a secondary model -- something a paid, higher-SLA API might not have forced me to build, but which makes the app meaningfully more robust either way.
2. **Never trust an LLM to silently follow a numeric scale.** Even with the schema clearly defined, Gemini intermittently returned 0-10 instead of 0-100. The fix needed two layers: a stricter, example-driven prompt, AND a server-side safety net that detects and corrects the wrong scale regardless of what the model returns.
3. **Test both ends of the quality spectrum, not just the happy path.** Deliberately giving terse, lazy answers and then detailed, technical answers in separate test runs was the only way to confirm the scoring engine was genuinely differentiating quality, not just returning a fixed number.
4. **"It works on my machine" and "it works in production" require separate verification.** Two real bugs today (Gemini overload, score scale) only became visible when testing the actual deployed app with real interactions -- not from code review or local testing alone.

## Screenshots
See attached: full user flow from resume upload through to the final scored report, on the live deployed application.

## Live Links
- **Live app:** https://crackit-ai-interview.vercel.app
- **Project repo:** https://github.com/ayushman6684/crackit-ai-interview

## Tomorrow's Goal
Day 7: build PDF report generation -- the last piece of the MVP, replacing the "PDF download coming tomorrow" placeholder with a real, downloadable, ATS-style report.
