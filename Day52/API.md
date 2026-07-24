# CrackIt — API Design
### Day 2 Deliverable — Full Endpoint Contracts (No implementation yet)

> All endpoints are Next.js API Routes under `src/app/api/`. There is no authentication layer (per the PRD's no-accounts decision), so "Authentication" below is `None` for every endpoint — this is intentional, not an oversight. All endpoints are stateless: every request must include all data needed to process it.

---

## 1. `POST /api/parse-resume`

**Purpose:** Extract plain text from an uploaded resume file (PDF or DOCX), so it can populate the resume input field.

**Request:** `multipart/form-data`
| Field | Type | Required |
|---|---|---|
| `file` | File (`.pdf` or `.docx`, max 5MB) | Yes |

**Response — success (200):**
```json
{ "success": true, "text": "Extracted resume text..." }
```

**Response — failure (200, not 4xx — this is an expected outcome, not a server error):**
```json
{ "success": false, "reason": "Could not extract readable text from this file." }
```

**Validation:**
- File extension must be `.pdf` or `.docx` — reject others with `success: false` before attempting extraction.
- File size must be ≤ 5MB — reject oversized files early with a specific reason string.
- Extracted text must be ≥ 100 characters — otherwise treated as a failed extraction (likely a scanned/image-only PDF).

**Authentication:** None.

**Error cases:**
| Case | Response |
|---|---|
| No file provided | `400` — `{ "success": false, "reason": "No file provided." }` |
| Unsupported file type | `200` — `{ "success": false, "reason": "Unsupported file type. Please upload a PDF or DOCX." }` |
| File too large | `200` — `{ "success": false, "reason": "File exceeds 5MB limit." }` |
| Parsing library throws (corrupted file) | `200` — `{ "success": false, "reason": "Could not read this file. Please paste your resume text instead." }` |

---

## 2. `POST /api/interview/start`

**Purpose:** Initialize an interview session — compute the adaptive question target and generate the first interviewer question.

**Request:**
```json
{
  "resumeText": "string, required, min 50 chars",
  "jobTitle": "string, optional",
  "jobDescription": "string, optional",
  "tone": "friendly | standard | tough, required"
}
```

**Response — success (200):**
```json
{
  "question": "Walk me through the 'Inventory System' project on your resume...",
  "sessionContext": { "tone": "standard", "targetQuestionCount": 8, "questionIndex": 1 }
}
```

**Validation:**
- `resumeText` required, minimum 50 characters (reject obviously empty/placeholder input).
- `tone` must be exactly one of the 3 allowed enum values.
- `jobTitle`/`jobDescription` are optional strings; no minimum length enforced, but a reasonable max length cap (e.g., 8,000 characters) to protect prompt size and cost.

**Authentication:** None.

**Error cases:**
| Case | Response |
|---|---|
| Missing/too-short `resumeText` | `400` — `{ "error": "Resume text is required and must be substantive." }` |
| Invalid `tone` value | `400` — `{ "error": "Tone must be one of: friendly, standard, tough." }` |
| Claude API failure/timeout | `502` — `{ "error": "The interviewer is temporarily unavailable. Please try again." }` |

---

## 3. `POST /api/interview/next`

**Purpose:** Given the transcript so far, return the next interviewer question — or signal that the interview is complete.

**Request:**
```json
{
  "transcript": [
    { "role": "interviewer", "text": "..." },
    { "role": "candidate", "text": "..." }
  ],
  "sessionContext": { "tone": "standard", "targetQuestionCount": 8, "questionIndex": 1 },
  "resumeText": "string, required (resent for prompt context)",
  "jobDescription": "string, optional (resent for prompt context)"
}
```

**Response — success, more questions (200):**
```json
{
  "question": "...",
  "sessionContext": { "tone": "standard", "targetQuestionCount": 8, "questionIndex": 2 },
  "interviewComplete": false
}
```

**Response — success, interview complete (200):**
```json
{ "interviewComplete": true }
```

**Validation:**
- `transcript` must be a non-empty array, alternating roles, ending in a `candidate` entry (i.e., the candidate must have just answered before requesting the next question).
- `sessionContext.questionIndex` and `targetQuestionCount` must both be present integers.
- If `questionIndex >= targetQuestionCount`, skip the Claude call entirely and return `interviewComplete: true` (cost + latency optimization, per `ARCHITECTURE.md`).

**Authentication:** None.

**Error cases:**
| Case | Response |
|---|---|
| Malformed/empty transcript | `400` — `{ "error": "A valid transcript ending in a candidate answer is required." }` |
| Missing `sessionContext` fields | `400` — `{ "error": "sessionContext with tone, targetQuestionCount, and questionIndex is required." }` |
| Claude API failure/timeout | `502` — `{ "error": "The interviewer is temporarily unavailable. Please try again." }` |

---

## 4. `POST /api/feedback`

**Purpose:** Analyze the full completed transcript and generate the structured scorecard, strengths/weaknesses, suggestions, and model answers.

**Request:**
```json
{
  "transcript": [ /* full transcript array */ ],
  "resumeText": "string, required",
  "jobDescription": "string, optional",
  "tone": "friendly | standard | tough"
}
```

**Response — success (200):** exact `FeedbackResult` shape defined in `SCHEMA.md`:
```json
{
  "scores": { "resumeCredibility": 72, "technicalKnowledge": 65, "communication": 80, "problemSolving": 58, "confidence": 70, "resumeJdFit": 63 },
  "strengths": ["..."],
  "weaknesses": ["..."],
  "suggestions": ["..."],
  "modelAnswers": [ { "question": "...", "candidateAnswer": "...", "betterAnswer": "..." } ]
}
```

**Validation:**
- `transcript` must contain at least 6 candidate answers (i.e., a genuinely completed interview) — reject premature feedback requests.
- Server must validate Claude's JSON response against the expected schema before returning it to the client; if parsing fails after stripping markdown fences, retry once, then fail gracefully.

**Authentication:** None.

**Error cases:**
| Case | Response |
|---|---|
| Transcript too short / incomplete | `400` — `{ "error": "Interview must be completed before requesting feedback." }` |
| Claude returns unparseable JSON (after retry) | `502` — `{ "error": "Could not generate your feedback report. Please try again." }` |
| Claude API failure/timeout | `502` — `{ "error": "Feedback generation is temporarily unavailable. Please try again." }` |

---

## 5. `POST /api/generate-report`

**Purpose:** Render the feedback + transcript into a downloadable, ATS-style PDF.

**Request:**
```json
{
  "feedback": { /* FeedbackResult shape */ },
  "transcript": [ /* full transcript array */ ],
  "jobTitle": "string, optional — included in the report header if present"
}
```

**Response — success (200):** Binary PDF stream.
Headers:
```
Content-Type: application/pdf
Content-Disposition: attachment; filename="CrackIt_Report.pdf"
```

**Validation:**
- `feedback` object must match the `FeedbackResult` schema exactly (all 6 score keys present, arrays non-empty) — reject with a clear error rather than rendering a broken PDF.
- `transcript` must be non-empty.

**Authentication:** None.

**Error cases:**
| Case | Response |
|---|---|
| Missing/malformed `feedback` object | `400` — `{ "error": "Valid feedback data is required to generate a report." }` |
| Empty transcript | `400` — `{ "error": "A completed interview transcript is required." }` |
| PDF rendering exception | `500` — `{ "error": "Could not generate the PDF report. Please try again." }` |

---

## 6. Cross-Cutting Rules (apply to all endpoints)

- **No authentication anywhere** — this is a deliberate architectural decision (PRD Section 5.2), not a gap.
- **Input length caps** on all free-text fields (`resumeText`, `jobDescription`, individual `transcript` entries) to protect against abuse and unexpectedly large Claude API bills — exact limits to be finalized during Day 9 (Deployment Hardening) per the Blueprint, but designed for now with generous defaults (e.g., 20,000 characters for resume/JD).
- **All error responses share a consistent shape:** `{ "error": "human-readable message" }` for 4xx/5xx, so the frontend can render errors uniformly.
- **All success responses are JSON** except `/api/generate-report`, which returns a binary PDF stream.
