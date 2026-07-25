# CrackIt — Environment Reference
### All environment variables, tools, and configuration in one place

> **Updated Day 5:** The AI engine was switched from the originally-planned Anthropic Claude API to Google's Gemini API, since Gemini offers a genuinely free tier with no billing account ever required — better fit for this project's zero-cost constraint. `GEMINI_API_KEY` replaces the originally-planned `ANTHROPIC_API_KEY` throughout. The Gemini API is now actively used by `/api/interview/start` and `/api/interview/next` as of Day 5.

---

## 1. Environment Variables

| Variable | Where it's set | Purpose | Required for |
|---|---|---|---|
| `GEMINI_API_KEY` | `.env.local` (local) / Vercel Project Settings (production) | Authenticates requests to the Gemini API — powers the interview engine and feedback scoring | Day 5 onward (not yet used by any code as of Day 3) |

**Important distinctions:**
- `.env.local` is **never committed to Git** (covered by `.gitignore`) — it only affects your local machine.
- Vercel's environment variables (set in the dashboard) are **separate** from your local `.env.local` — you must set both independently. Changing one does not affect the other.
- As of Day 3, both are set to the placeholder value `your-key-here`. This must be replaced with a real key before Day 5, when the Gemini API is first actually called.

### How to get a real `GEMINI_API_KEY`
1. Go to the Google AI Studio (console.anthropic.com).
2. Create an account or sign in.
3. Navigate to API Keys and generate a new key.
4. Replace the placeholder in both `.env.local` (local) and the Vercel dashboard (production) — see `SETUP.md` Section 4 and 8.

---

## 2. Development Tools & Versions

| Tool | Version confirmed working | Notes |
|---|---|---|
| Node.js | v24.15.0 | Well above the 18.17 minimum Next.js requires |
| npm | 11.12.1 | Bundled with Node.js |
| Next.js | 16.2.11 | Scaffolded with App Router, Turbopack (default dev bundler) |
| React | (bundled with Next.js 16) | — |
| Tailwind CSS | latest (via `@tailwindcss/postcss`) | Styling |
| ESLint | latest (`eslint-config-next`) | Code quality checks |
| Git | already configured | Used for GitHub integration |
| VS Code | user's existing install | Primary code editor |

---

## 3. Key Configuration Files

| File | Purpose |
|---|---|
| `next.config.mjs` | Next.js configuration. Explicitly sets `turbopack.root` to this project's own folder (via `__dirname`, manually derived since `.mjs` files are ES Modules) — this prevents Next.js from getting confused by an unrelated `package-lock.json` elsewhere on the machine. |
| `jsconfig.json` | JavaScript project configuration — enables clean import paths. |
| `eslint.config.mjs` | Linting rules (using the "ESLint" option, not Biome). |
| `postcss.config.mjs` | Required for Tailwind CSS to process styles. |
| `.gitignore` | Excludes `node_modules/`, `.next/`, `.env*.local`, and other files that should never be committed. |
| `.env.local` | Local-only environment variables (see Section 1). |
| `package.json` / `package-lock.json` | Dependency manifest and exact locked versions. |

---

## 4. Hosting & Deployment Environment

| Setting | Value |
|---|---|
| Hosting provider | Vercel |
| Plan | **Hobby (free tier)** — confirmed selected during setup, not Pro |
| Vercel account/team namespace | `ayushman-crackit` |
| Connected repository | `ayushman6684/crackit-ai-interview` (GitHub) |
| Deployment branch | `main` (auto-deploys on every push) |
| Live URL | `https://crackit-ai-interview.vercel.app` |
| Root directory | `./` (project root, default) |
| Framework preset | Next.js (auto-detected) |

---

## 5. Next.js Scaffold Choices (locked in, do not change without discussion)

These were selected during `npx create-next-app@latest .` and match the approved Architecture/Project Structure docs:

| Option | Choice | Reason |
|---|---|---|
| TypeScript | No | Keeps the codebase simpler for a 9-day solo build; matches original Blueprint decision |
| Linter | ESLint | Standard, well-supported |
| React Compiler | No | Newer, still-maturing optimization tool not needed for this project's scale |
| Tailwind CSS | Yes | Fast styling without a custom design system |
| `src/` directory | Yes | Matches `PROJECT-STRUCTURE.md` |
| App Router | Yes | Required for the routing structure in `PROJECT-STRUCTURE.md` and `API.md` |
| Turbopack (dev) | Auto-enabled by this Next.js version | Faster local dev builds; no impact on production behavior |
| Import alias customization | No | Default `@/*` alias is fine, unused so far |
| AGENTS.md | No | Redundant with our existing `docs/` folder, which already serves this purpose |
