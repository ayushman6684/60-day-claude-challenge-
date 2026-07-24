# CrackIt — Project Structure
### Updated Day 3 — Reflects Actual Scaffolded Codebase

> Originally defined on Day 2 as a plan; this version reflects what actually exists in the repository after Day 3 scaffolding. Differences from the Day 2 plan are called out explicitly in Section 3.

---

## 1. Full Folder Tree (as of end of Day 3)

```
crackit-ai-interview/
├── docs/                              # All planning & design documentation
│   ├── CrackIt_PRD.docx
│   ├── CrackIt_Implementation_Blueprint.md
│   ├── CrackIt_Pitch_Deck.pptx
│   ├── ARCHITECTURE.md
│   ├── SCHEMA.md
│   ├── API.md
│   ├── UI-WIREFRAMES.md
│   ├── PROJECT-STRUCTURE.md           # this file
│   ├── PROJECT-LOG.md
│   ├── SETUP.md                       # new — Day 3
│   ├── ENVIRONMENT.md                 # new — Day 3
│   └── DAY3-SUMMARY.md                # new — Day 3
│
├── public/                            # Static assets (default Next.js icons — to be replaced with CrackIt branding later)
│   ├── file.svg, globe.svg, next.svg, vercel.svg, window.svg
│
├── src/
│   ├── app/                           # Next.js App Router — pages & API routes
│   │   ├── page.js                    # Landing screen (/) — placeholder content
│   │   ├── layout.js                  # Root layout — wraps app in SessionProvider + renders NavBar
│   │   ├── globals.css                # Tailwind base styles (default, not yet re-themed)
│   │   ├── favicon.ico                # Default Next.js favicon (placeholder)
│   │   │
│   │   ├── setup/
│   │   │   └── page.js                # Resume + JD input screen (/setup) — placeholder content
│   │   │
│   │   ├── interview/
│   │   │   └── page.js                # Tone selection + chat screen (/interview) — placeholder content
│   │   │
│   │   ├── results/
│   │   │   └── page.js                # Feedback + report screen (/results) — placeholder content
│   │   │
│   │   └── api/
│   │       ├── parse-resume/
│   │       │   └── route.js           # POST /api/parse-resume — returns placeholder { status: "ok" }
│   │       ├── interview/
│   │       │   ├── start/
│   │       │   │   └── route.js       # POST /api/interview/start — placeholder
│   │       │   └── next/
│   │       │       └── route.js       # POST /api/interview/next — placeholder
│   │       ├── feedback/
│   │       │   └── route.js           # POST /api/feedback — placeholder
│   │       └── generate-report/
│   │           └── route.js           # POST /api/generate-report — placeholder
│   │
│   ├── components/
│   │   └── NavBar.js                  # ✅ Built Day 3 (moved up from later plan) — Home/Setup/Interview/Results links
│   │       # ToneCard.js, ChatBubble.js, ScoreBar.js, LoadingIndicator.js, ErrorBanner.js — still pending, Day 5-8
│   │
│   ├── context/
│   │   └── SessionContext.js          # ✅ Built Day 3 — full shape from SCHEMA.md already implemented (resumeText, jobTitle,
│   │                                   #    jobDescription, tone, interviewSessionContext, transcript, feedback), all as empty/null state for now
│   │
│   ├── lib/
│   │   ├── claude.js                  # ✅ Built Day 3 — Anthropic client wrapper, reads ANTHROPIC_API_KEY, not yet called anywhere
│   │   └── pdf/                       # empty — ReportDocument.js still pending, Day 7
│   │
│   └── styles/                        # empty — theme.js still pending (brand colors/fonts), Day 4+
│
├── .env.local                         # ANTHROPIC_API_KEY=your-key-here (placeholder, never committed)
├── .gitignore
├── eslint.config.mjs
├── jsconfig.json
├── next.config.mjs                    # customized: explicit turbopack.root fix (see SETUP.md gotchas)
├── package.json
├── package-lock.json
├── postcss.config.mjs
└── README.md
```

---

## 2. What Changed Since Day 2's Plan

| Item | Day 2 Plan | What Actually Happened Day 3 | Why |
|---|---|---|---|
| `NavBar.js` | Planned as part of later UI work | Built today | Cheap to add now, needed to click between placeholder pages during verification, and matches the Architecture doc's screen flow |
| `SessionContext.js` | Planned to be filled in Day 4 | Full shape built today (empty/null state) | Since `layout.js` needed to wrap the app in a provider today anyway, it made sense to implement the real schema shape now rather than a throwaway stub |
| `lib/claude.js` | Planned for Day 5 | Stub created today | Zero-cost to scaffold now; contains no logic yet, just the client setup — Day 5 still does all the real prompt/API work |
| `next.config.mjs` | Not specifically planned | Required a custom fix | A stray `package-lock.json` elsewhere on the developer's machine caused Turbopack root-detection issues; fixed by explicitly setting `turbopack.root` (see `SETUP.md` Section 7 for full detail) |

**None of these are scope changes** — they're small pull-forwards of trivial scaffolding work that make Day 4 onward faster, not new features. No functional/business logic was implemented today, consistent with the Blueprint's Day 3 objective.

---

## 3. Folders/Files Still Empty (planned for later days, per the Blueprint)

| Folder/File | Built on |
|---|---|
| `src/components/ToneCard.js`, `ChatBubble.js` | Day 5 |
| `src/components/ScoreBar.js` | Day 6 |
| `src/components/LoadingIndicator.js`, `ErrorBanner.js` | Day 8 |
| `src/lib/prompts.js` | Day 5 |
| `src/lib/pdf/ReportDocument.js` | Day 7 |
| `src/styles/theme.js` | Day 4 (when the Setup screen gets real styling) |

This confirms the project structure still matches the original Architecture and API design — nothing has been restructured, only scaffolded ahead of schedule where it was free to do so.
