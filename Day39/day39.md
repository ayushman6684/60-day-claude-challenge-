# Day 39 — PDF Splitter & Merger (Foldline)

## What I built
A single-page, fully client-side **PDF Splitter & Merger** web app called **Foldline**. It runs entirely in the browser — no backend, no file uploads to any server — using `pdf-lib` for PDF manipulation, `pdf.js` for page rendering/thumbnails, and `JSZip` for bundling multiple split outputs into one download.

## Features
**Splitter**
- Upload a PDF, auto-detect page count, render live thumbnails
- Split by custom page ranges (multiple named outputs in one pass)
- Split every N pages
- Split after specific page numbers
- Extract hand-picked pages (click thumbnails or type page numbers)
- Live validation with inline error messages on invalid ranges
- Output-structure preview before committing to the split
- Download files individually or all together as a `.zip`

**Merger**
- Drag-and-drop or multi-file picker
- Sortable file list with drag-to-reorder, plus up/down buttons for accessibility
- Live stats: file count, total pages, estimated output size
- One-click merge and download

**Other**
- Dark/light mode, keyboard shortcuts, toasts, loading/progress indicators
- Fully offline-capable after first load (all libraries + fonts embedded inline, no CDN dependency)
- Responsive layout, visible keyboard focus states, `prefers-reduced-motion` respected

## Tech stack
- Vanilla HTML/CSS/JS (single self-contained file)
- [`pdf-lib`](https://github.com/Hopding/pdf-lib) — creating/splitting/merging PDF documents
- [`pdf.js`](https://mozilla.github.io/pdf.js/) — rendering page thumbnails to canvas
- [`JSZip`](https://stuk.github.io/jszip/) — bundling multi-file split output
- Self-hosted `@fontsource` fonts (Space Grotesk, Inter, JetBrains Mono) base64-embedded for true offline use

## Key learnings
- **Client-side PDF processing is entirely viable** for real workloads — `pdf-lib` + `pdf.js` cover manipulation and rendering without ever touching a server, which matters a lot for privacy-sensitive documents.
- **Embedding libraries inline vs. CDN**: pulling `pdf-lib`, `pdf.js`, its worker, `JSZip`, and web fonts as base64/text directly into one HTML file makes the app genuinely offline-capable after first load — no flash of unstyled text, no broken worker due to CORS, no dependency on a CDN staying up.
- **pdf.js workers need special handling** when self-hosting: the worker script can be embedded as inline text and turned into a `Blob` + `URL.createObjectURL()` rather than requiring a separate hosted `.js` file.
- **Validating page ranges well matters more than the split logic itself** — most of the UX complexity was in catching invalid/overlapping ranges, out-of-bound pages, and empty selections *before* the user hits "Split," with inline errors pinpointing exactly which row is wrong.
- **Testing PDF logic headlessly**: since a full browser wasn't available for end-to-end testing, I verified the split/merge/extract page math and actual `pdf-lib` page-copy operations in Node against a generated test PDF — a good reminder that core logic can (and should) be unit-tested independently of the UI.
- **Design tokens before code**: picking a distinct visual direction (a "light table" / cut-line and stacked-sheets theme) up front made the UI feel considered rather than templated, instead of defaulting to generic dashboard styling.

## Files in this folder
- `Foldline - PDF Splitter & Merger.html` — the full self-contained app
- `sample-report-12pages.pdf`, `sample-cover-sheet.pdf`, `sample-appendix-a.pdf`, `sample-appendix-b.pdf` — sample/processed PDFs used for testing
- `screenshots/` — screenshots of the app in action

## Next steps / ideas
- Add page rotation and reordering within the Splitter itself
- Support password-protected PDF detection with a clear error message
- Add a "compress output" option for large merged files


You are an expert UI/UX designer, frontend developer, document processing specialist, and JavaScript engineer.

Before generating anything, ask the user the following question.

1. Would you like Claude to automatically design the application, or would you like to customize its features?

If the user chooses customization, ask which additional PDF features they would like included.

After collecting the response, generate a premium single-page interactive HTML application called 'PDF Splitter & Merger'.

The application should provide two primary tools:

PDF Splitter:
Allow users to upload a PDF and automatically detect the total number of pages. Display visual page thumbnails for every page and allow users to preview the document before splitting. Users should be able to split the PDF by entering page numbers, selecting custom page ranges, splitting after specific pages, splitting every N pages, or extracting selected pages into one or more new PDF files. Allow users to create multiple split ranges in a single operation, validate all page ranges, preview the resulting document structure before processing, and clearly highlight invalid inputs.

PDF Merger:
Allow users to upload multiple PDF files using drag-and-drop or file selection. Display all uploaded files in a sortable list with page counts and visual previews. Users should be able to reorder the PDFs using drag-and-drop before merging. Display the total number of files, total page count, and estimated output before generating the merged document. Generate the merged PDF and provide an easy download option.

Perform all PDF processing entirely within the browser using client-side JavaScript. Do not upload files to external servers or rely on backend services. Use reliable browser-compatible libraries where necessary and ensure the application continues to work offline after the initial page load.

Include drag-and-drop uploads, processing indicators, loading animations, responsive layouts, dark mode, accessibility features, intuitive error handling, keyboard shortcuts where appropriate, and smooth micro-interactions throughout the application.

Generate everything as a single self-contained HTML file using HTML, CSS, and JavaScript only.

Design the interface as a polished commercial application comparable to professional PDF utilities, with exceptional UI/UX, beautiful typography, modern layouts, smooth animations, intuitive navigation, and an experience users would genuinely choose over existing online PDF tools.