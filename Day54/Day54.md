@'
# Day 54 — Capstone Day 4: Resume & Job Description Input

## What I Built Today
Implemented the first real, functional feature of **CrackIt**: resume input with actual PDF and DOCX text extraction.

- Real PDF text extraction using pdf-parse
- Real DOCX text extraction using mammoth
- Paste-or-upload toggle UI, styled with the CrackIt brand palette
- Graceful fallback for unreadable/corrupted files (no crashes)
- Optional job title + job description fields
- Continue button gated on resume text being present
- Verified all scenarios locally AND on the live production deployment

## Key Learnings
1. **A "simple" feature can hide real debugging work.** Getting pdf-parse working required solving three separate library issues: a broken ESM default export, a newer version requiring unavailable browser rendering APIs, and a debug-mode file path bug — none of which were bugs in my own code.
2. **Pin dependency versions when a library misbehaves.** Downgrading to pdf-parse@1.1.1 (a long-stable version) and importing its internal module directly via createRequire solved what looked like a deep compatibility problem.
3. **Always verify in production, not just localhost.** Serverless environments can behave differently from a local dev server — testing the live Vercel deployment caught this early instead of on Day 9.
4. **Good fallback UX matters as much as the happy path.** A corrupted file upload never crashes the app — it shows a clear message and lets the user paste instead, which was as important to get right as the successful extraction path.

## Screenshots
See attached: successful PDF upload with extracted text, successful DOCX upload, and the graceful fallback error for a corrupted file.

## Documentation
Updated `PROJECT-LOG.md` reflects today's Day 4 entry (attached in this folder).

## Live Links
- **Live app:** https://crackit-ai-interview.vercel.app/setup
- **Project repo:** https://github.com/ayushman6684/crackit-ai-interview

## Tomorrow's Goal
Build the Tone Selection screen and the adaptive AI interview engine — the core "wow" feature of CrackIt, powered by the Claude API.
'@ | Out-File -Encoding utf8 Day54\day54.md