# CrackIt — Setup Guide
### How to get this project running locally, from a fresh clone

This guide reflects the exact working setup as of Day 3 of the capstone. Follow it top to bottom for a clean install with no detours.

---

## 1. Prerequisites

| Tool | Minimum Version | Used in this project |
|---|---|---|
| Node.js | 18.17+ | v24.15.0 |
| npm | (bundled with Node.js) | 11.12.1 |
| Git | any recent version | already configured |

Check your versions:
```powershell
node --version
npm --version
```

If Node.js is missing or below 18.17, install it from **https://nodejs.org** (choose the LTS version) before continuing.

---

## 2. Clone the Repository

```powershell
git clone https://github.com/ayushman6684/crackit-ai-interview.git
cd crackit-ai-interview
```

---

## 3. Install Dependencies

This project already has a `package.json` listing everything it needs. Install all of it in one command:

```powershell
npm install
```

This installs both the framework dependencies (Next.js, React, Tailwind) and the feature dependencies (Gemini SDK, PDF/DOCX parsing, PDF generation):
- `next`, `react`, `react-dom` — the core framework
- `tailwindcss`, `@tailwindcss/postcss` — styling
- `eslint`, `eslint-config-next` — code quality checks
- `@google/genai` — Gemini API client
- `pdf-parse`, `mammoth` — resume file text extraction (PDF, DOCX)
- `@react-pdf/renderer` — generates the downloadable interview report

---

## 4. Set Up Environment Variables

Create a file named `.env.local` in the project root:

```powershell
@'
GEMINI_API_KEY=your-key-here
'@ | Out-File -Encoding utf8 .env.local
```

Replace `your-key-here` with a real Anthropic API key once you have one (get one at the Google AI Studio). **Never commit this file** — it's already covered by `.gitignore`.

See `ENVIRONMENT.md` for the full list of environment variables and what each one does.

---

## 5. Run the Project Locally

```powershell
npm run dev
```

Open **http://localhost:3000** in your browser. You should see:
- A nav bar with **Home / Setup / Interview / Results** links
- The CrackIt landing page placeholder

---

## 6. Verify a Production Build (optional, but recommended before deploying)

```powershell
npm run build
```

Look for `✓ Compiled successfully` and a route table listing all pages and API routes with no errors.

---

## 7. Known Setup Gotchas (and how they were solved)

These are documented here so nobody re-solves the same problems from scratch:

| Issue | Cause | Fix |
|---|---|---|
| `npx create-next-app@latest .` fails with "directory contains files that could conflict" | An existing file (e.g. `README.md`) is present in the target folder | Temporarily move the conflicting file **out of the folder** (not just rename it — renamed files still get flagged), run the scaffold, then move it back |
| `ReferenceError: __dirname is not defined in ES module scope` in `next.config.mjs` | `.mjs` files are ES Modules, which don't have `__dirname` built in like older CommonJS files do | Manually derive it: `import { fileURLToPath } from "url"; import path from "path"; const __dirname = path.dirname(fileURLToPath(import.meta.url));` |
| Next.js warns about "multiple lockfiles" / wrong workspace root detected | A stray `package-lock.json` existed in a parent folder | Set `turbopack: { root: __dirname }` explicitly in `next.config.mjs` |
| Browser shows `Runtime SyntaxError: Unexpected end of JSON input` | Corrupted `.next` build cache (often from restarting the dev server rapidly) | Delete the cache and rebuild: `Remove-Item -Recurse -Force .next`, then `npm run dev` again |
| Edited a file in the code editor but changes don't appear | The save didn't register (e.g. focus was on the terminal panel instead of the editor tab) | Verify file contents from the terminal with `Get-Content <file>` before assuming a save worked; if wrong, overwrite via a terminal here-string instead |

---

## 8. Deployment (Vercel)

The project auto-deploys from the `main` branch on GitHub via Vercel.

1. Push to `main` → Vercel automatically builds and redeploys.
2. Environment variables (like `GEMINI_API_KEY`) must be set separately in the Vercel dashboard under **Project → Settings → Environment Variables** — they are **not** read from your local `.env.local`.
3. Live URL: `https://crackit-ai-interview.vercel.app`

---

## 9. Project Structure Reference

See `PROJECT-STRUCTURE.md` for the full folder-by-folder breakdown of this codebase.
