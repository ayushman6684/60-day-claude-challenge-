# 30-Day Growth Plan — CrackIt: AI Resume Defense Simulator

Turning the v1.0.0 MVP into a significantly more complete product. Each day is one shippable milestone — commit and (where relevant) redeploy at the end of every day. Stack assumed throughout: Next.js 16 App Router, React 19, Tailwind 4, Gemini (`@google/genai`), Vercel.

## Week 1 — Harden the Core (Days 1–7)
1. **Day 1:** Add basic request rate-limiting (e.g. Vercel Edge Config or an in-memory token bucket) so one heavy session can't exhaust the Gemini free-tier quota.
2. **Day 2:** Add error boundaries + friendly fallback UI for: Gemini API failure, malformed PDF/DOCX upload, and network timeout.
3. **Day 3:** Add a "Resume-JD Fit" gap list to the report — explicit keywords the JD asks for that the resume doesn't mention.
4. **Day 4:** Add one clarifying follow-up question when an answer is too vague, before the interview moves to the next topic.
5. **Day 5:** Write integration tests for the resume-parsing pipeline (PDF + DOCX) covering at least 3 real-world resume formats.
6. **Day 6:** Add a loading/progress indicator during resume parsing and AI response generation (perceived performance).
7. **Day 7:** Ship a "Try a sample resume" button so a first-time visitor can experience the full flow with zero friction.

## Week 2 — Depth of the Interview Experience (Days 8–14)
8. **Day 8:** Add a 4th interviewer tone: "Panel" — simulates 2–3 interviewer personas in one session.
9. **Day 9:** Add role-specific question weighting for SDE vs Data/ML vs PM (same engine, different emphasis).
10. **Day 10:** Improve the scoring rubric with explicit weight transparency — show *why* a category scored the way it did, not just the number.
11. **Day 11:** Add a "model answer" comparison view — show the candidate's answer next to a strong model answer side-by-side.
12. **Day 12:** Add session timing (how long each answer took) as a soft signal for the Confidence category.
13. **Day 13:** Mobile responsiveness pass — dedicated layout testing on the interview and report screens at 375px width.
14. **Day 14:** Accessibility pass — keyboard navigation, ARIA labels, color contrast check on the report screen.

## Week 3 — Product Surface & Trust (Days 15–21)
15. **Day 15:** Add an optional "email me this report" flow (no account required, short-lived link).
16. **Day 16:** Add a privacy page explaining exactly what is and isn't stored — reinforce the stateless-by-default trust story.
17. **Day 17:** Add analytics (privacy-respecting, e.g. Vercel Analytics) to see where users drop off in the flow.
18. **Day 18:** Add a feedback widget ("Was this question relevant?") to start collecting signal for future tuning.
19. **Day 19:** Write and record a 90-second demo video for the README and LinkedIn.
20. **Day 20:** Add Open Graph / social preview image so shared links look polished.
21. **Day 21:** SEO pass — meta description, sitemap, proper page titles for discoverability.

## Week 4 — Scale & Polish Toward v2.0 (Days 22–30)
22. **Day 22:** Add CI via GitHub Actions — lint + build check on every push.
23. **Day 23:** Add a CONTRIBUTING.md and issue templates to make the repo genuinely open-source-friendly.
24. **Day 24:** Abstract the AI provider layer so a second model (e.g. Claude or GPT) could be swapped in without a rewrite.
25. **Day 25:** Add a second, JD-only "screening mode" for recruiters to test multiple candidates against one JD.
26. **Day 26:** Add dark mode.
27. **Day 27:** Performance pass — audit Lighthouse scores, optimize bundle size and PDF generation latency.
28. **Day 28:** Security review — confirm no API keys are ever exposed client-side, confirm uploaded resumes are never persisted anywhere.
29. **Day 29:** Write full documentation of the architecture (docs/ARCHITECTURE.md) for future contributors.
30. **Day 30:** Tag and ship **v2.0.0** — write release notes summarizing the month's improvements, and post the milestone publicly.

---

**How to use this plan:** don't try to do all 30 days back-to-back at capstone intensity. One milestone a day, committed and pushed, is the whole system. If a day's milestone turns out to be bigger than expected, split it — the goal is a steady visible commit trail, not heroics.
