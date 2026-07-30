# Future Scope — CrackIt: AI Resume Defense Simulator

CrackIt v1.0.0 already does the hard part: it reads a real resume, asks questions a real interviewer would ask, and hands back a scored report. Everything below builds *on top of* that working core — none of it requires rearchitecting what exists today.

---

## Next 3 Months — Depth & Trust

The goal here is to make each individual interview session smarter and more trustworthy, without adding new surface area.

- **Follow-up probing on weak answers** — if the candidate's answer to a resume claim is vague ("I improved performance"), the interviewer should ask one clarifying follow-up ("By how much? What did you measure?") before moving on, the way a real technical interviewer does.
- **Confidence calibration** — cross-reference the six scored categories against answer length, specificity, and hedging language, so "Confidence" score reflects more than just tone.
- **Session history (optional, opt-in)** — right now CrackIt is fully stateless by design, which is a genuine privacy strength. Add an *optional* "email me my report" or short-lived session link, without breaking the no-signup default.
- **Better JD parsing** — extract required skills/keywords from the pasted job description and explicitly show "Resume-JD Fit" gaps in the report (e.g., "JD asks for AWS, resume doesn't mention it").
- **Rate limiting & abuse protection** — since Gemini's free tier is finite, add basic request throttling so one heavy user session doesn't exhaust the shared quota.

## Next 6 Months — Breadth

Once the single-session experience is airtight, expand what CrackIt can be used *for*.

- **Role-specific interview modes** — SDE, Data/ML, PM, and Frontend-specific question banks layered on top of the resume-aware core, since a fresher applying for a frontend role should get different probing than one applying for backend.
- **Multi-round simulation** — chain a screening round → technical round → HR round in one flow, mirroring how real hiring pipelines are structured.
- **Peer benchmark (anonymized)** — show a user how their scored categories compare to an anonymized aggregate of other sessions for similar roles, giving context to an otherwise isolated score.
- **Mobile-responsive polish pass** — dedicated pass on small-screen layouts for the interview and report screens, since a meaningful share of students will try this on a phone first.
- **Public API / embed widget** — let college placement cells or bootcamps embed a CrackIt widget on their own site.

## Next 12 Months — Platform

- **Recruiter-facing mode** — a second, opt-in mode where a recruiter uploads a JD and CrackIt screens multiple candidate resumes with the same rubric, standing up CrackIt as a two-sided tool rather than only a practice tool.
- **Multi-model support** — abstract the AI layer so CrackIt isn't locked to Gemini alone, allowing cost/quality trade-offs (e.g., a paid tier on a stronger model) without a rewrite.
- **Interview analytics dashboard** — for users who opt into saved history, trend their scores across multiple practice sessions over time.
- **Voice mode** — accept spoken answers (speech-to-text in, the existing text pipeline unchanged) to simulate the verbal pressure of a real interview, which is the single biggest gap between practicing on CrackIt today and a real interview.

---

**Guiding principle for all of the above:** every addition should preserve what makes CrackIt distinct today — it reads *your* actual resume and probes *your* actual claims, instead of asking the same 20 generic questions every other mock-interview tool asks. Anything that dilutes that specificity isn't worth adding, no matter how popular the feature sounds in isolation.
