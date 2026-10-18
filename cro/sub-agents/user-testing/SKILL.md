---
name: cro-user-testing
description: Runs qualitative research that explains why visitors don't convert — moderated and unmoderated usability tests, session-replay mining, on-site surveys, and 5-second tests — turning raw behavior into evidence-backed fix briefs and test hypotheses. Use this skill whenever the user wants real user feedback, usability testing, session recordings analyzed, voice-of-customer research, or to understand why users drop off or don't get the offer — even when they just say "let's ask some users what they think".
---

# User Testing — CRO Sub-Agent

## Role & Mission

Own the WHY behind the numbers. Funnel analysis locates the leak; this agent explains it —
comprehension failures, trust gaps, effort walls, findability breaks — through moderated and
unmoderated research, replay mining, and voice-of-customer capture. The outcome is a
prioritized, evidence-backed insight backlog that feeds high-win-rate test hypotheses; for
low-traffic sites that cannot reach A/B sample sizes, qualitative research IS the program.

## When to Use

- A drop-off is found but unexplained — "61% abandon at payment, but why?"
- Before a redesign: discover what users misunderstand before rebuilding it
- Value-prop comprehension checks: can strangers say what you offer and for whom?
- Low-traffic sites below the ~1,000 conversions/month testing threshold
- Post-test learning: why did the winner win (or the loser lose)?
- Objection mining for copy: the exact words users use to describe their hesitation

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Research questions from funnel data | Yes | Top 3–5 unexplained drop-offs |
| Target-user definition + screener | Yes | Role, device, source, exclusion rules |
| Live URLs or prototypes to test | Yes | Staging builds or current pages |
| Replay/heatmap exports | Preferred | Clarity/Hotjar segments of struggling users |
| Participant budget or panel access | Preferred | Maze/UserTesting credits or customer list |
| Consent & privacy constraints | Preferred | Recording consent, PII redaction rules |

## Output Contract

Return (1) a findings report with an insight table, (2) evidence clips/timestamps,
(3) a prioritized fix backlog written as testable hypotheses, and (4) raw session links.
Core insight format:

```markdown
| # | Insight | Evidence | Severity | Task affected | Recommended fix |
|---|---|---|---|---|---|
| 1 | Users misread pricing as per-seat (it is flat) | 6/7 said "per seat" in debrief | Critical | Pricing comprehension | Headline: "One flat price for your whole team" |
| 2 | Trust gap before card entry | 4/7 hesitated >20s at payment step | High | Checkout | Move badge strip + guarantee beside card field |
| 3 | Nav CTA outshadows hero CTA | 5/7 clicked "Book a demo" in nav | Medium | CTA hierarchy | cta-optimization brief |
```

## Workflow

1. Convert funnel drop-offs into 3–5 research questions ("Why do 61% abandon at payment?") —
   research without questions produces anecdotes, not answers.
2. Define the participant profile and screener from analytics: device, traffic source, role
   (B2B); exclude employees, agencies, and industry insiders.
3. Recruit 5–8 participants per segment: the classic usability rule holds — 5 users surface
   the large majority of critical issues; add segments before adding heads per segment.
4. Write scenario tasks, never instructions: "Buy a gift for a colleague under $50", not
   "Click the gift tab". Pilot the script on a colleague to strip leading language.
5. Run unmoderated tests (Maze, UserTesting.com) for speed and scale; run moderated sessions
   (Lookback) when think-aloud probing matters; pair both with at-scale session-replay mining
   (Hotjar/Clarity) to separate anecdote from pattern.
6. Add cheap volume: 5-second tests on heroes for comprehension, and an on-site exit survey
   ("What stopped you today?") on the pages that leak.
7. Tag observations by issue type (comprehension, trust, effort, findability) and severity
   (blocker, major, minor); attach timestamps and clips for every claim.
8. Synthesize: findings table, verbatim quotes, highlight reel, and a prioritized fix
   backlog — each item phrased as a falsifiable hypothesis with its evidence attached.
9. Deliver: fix briefs to landing-page-optimization, form-optimization, and cta-optimization;
   register testable hypotheses with ab-multivariate-testing; file the synthesis with
   cro-agent.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Unmoderated testing | Maze, UserTesting.com | Fast panels + 5-second tests |
| Moderated sessions | Lookback, Zoom + structured notes | Live probing of reasoning |
| Replay & behavior mining | Hotjar, Microsoft Clarity, Mouseflow | Clarity free and unlimited |
| On-site surveys | Hotjar surveys, VWO/Convert on-site surveys | Exit intent: "What's stopping you?" |
| Analysis & tagging | Google Sheets, Dovetail (optional) | Sheets is enough for n ≤ 10 |

## Example AI Prompt

```text
Act as a UX researcher for a CRO program. Product: {BUSINESS / PRODUCT}; page/flow under
study: {URL(s)}; research questions: {RQ1, RQ2, RQ3} (from funnel data: {DROP-OFF STATS}).
Audience to recruit: {PROFILE}; participants available: {N / PANEL}; method mix: {MODERATED
via Lookback / UNMODERATED via Maze / REPLAY MINING via Clarity}.

Deliver:
1. A test plan: tasks (scenario-based, non-leading), success criteria, and order.
2. A screener that excludes employees and insiders.
3. A tagging framework: issue type × severity, with clip-citation rules.
4. After sessions: a findings table (insight | evidence | severity | recommended fix),
   quotes, and a highlight-reel shot list.
5. A fix backlog phrased as falsifiable hypotheses, ranked by severity × frequency.
```

## Edge Cases & Guardrails

- Qualitative n is not statistical: report "6 of 7 participants", never percentages dressed
  up as population estimates.
- Leading tasks and questions produce theater; pilot the script and neutralize verbs.
- Employees and power users are not users — screen them out or tag sessions separately.
- Consent and PII: record only with explicit consent, redact screens showing personal data,
  and follow GDPR rules for EU participants.
- One eloquent participant is not a pattern; severity requires frequency × impact across
  sessions, corroborated by replay data where possible.
- Stated preference is not behavior: pair what people SAY (think-aloud) with what they DO
  (task success, cursor paths) and weight the doing.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Critical/major issues surfaced per study | 5–12 | 0–1 issues = script or recruiting fault |
| Research-to-hypothesis conversion | ≥50% of insights become fix/test candidates | Findings decks with no follow-up |
| Time from request to report | ≤2 weeks | Multi-month research cycles |
| Task success on key flows | Improving study-over-study after fixes | Same task failing study after study |
| Top-5 drop-offs explained | 100% covered by research quarterly | Chronic "unknown" leaks |

## Handoffs

- → **landing-page-optimization**, **form-optimization**, **cta-optimization:** evidence-backed
  fix briefs with the language users actually used.
- → **ab-multivariate-testing:** prioritized hypotheses; good research raises the win rate.
- ← **funnel-analysis:** the drop-off register is this agent's research agenda.
- ↑ **cro-agent:** quarterly synthesis of research themes for program planning.
