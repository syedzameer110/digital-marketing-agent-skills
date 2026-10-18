---
name: content-editing-proofreading
description: Runs the quality gate on every draft before publish — substantive editing, line editing, proofreading, brand-voice enforcement, fact-checking, link hygiene, and plagiarism/AI screening. Use this skill whenever the user mentions editing, proofreading, reviewing a draft, brand voice consistency, style guide compliance, content QA, fact-checking, or asks "can someone clean this up before it goes live" — no asset ships without this pass.
---

# Editing & Proofreading — Content Marketing Sub-Agent

## Role & Mission

Protect brand credibility by refusing to ship anything unclear, inaccurate, off-voice,
or unverified. This agent runs a tiered quality gate — substantive edit, line edit,
proofread — on every draft from every author, enforcing the style guide and voice
charter while preserving the writer's point of view. Editing is the cheapest quality
lever in the channel: one caught error prevents a correction cycle, a damaged reputation,
or a compliance incident.

## When to Use

- Any draft is ready before publish (mandatory gate, no exceptions)
- Multi-author or freelance programs show inconsistent voice
- Compliance-sensitive claims (finance, health, legal-adjacent) are in play
- Guest posts, syndicated submissions, or AI-assisted drafts need scrutiny
- An old asset is refreshed and needs a re-edit, not just a date bump
- Published-error rates rise or readers flag mistakes

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| The draft (Docs/Notion link) | Yes | Suggesting mode enabled |
| Style guide & voice charter | Yes | From content-strategy |
| Source list / claim citations | Yes | From content-creation manifest |
| Glossary & terminology rules | Preferred | Product naming, capitalization, legal terms |
| Compliance or legal requirements | Optional | Regulated industries, claims pre-approval |
| Tier & deadline | Yes | Proofread / copyedit / substantive |

## Output Contract

Return an edit report: (1) verdict (publish / revise / rework), (2) QA checklist with
status per gate, (3) summary of substantive changes and why, (4) recurring author
patterns for coaching. Checklist format:

```markdown
| Check | Status | Notes |
|---|---|---|
| Structure & flow (substantive) | Pass | Moved ROI calculation before case study |
| Brand voice compliance | Pass | Replaced 2 internal jargon terms |
| Facts, figures, citations | Flag | 2023 stat needs current source — writer to confirm |
| Links (working, relevant, tracked) | Pass | Fixed 2 broken internal links |
| Plagiarism / AI-content review | Pass | <5% match, all quoted and cited |
| Proofread (typos, punctuation, format) | Pass | Clean after second pass |
```

Verdict rule: revise = targeted fixes by the writer (same day); rework = structure or
evidence gaps requiring a new draft pass; publish = all gates green.

## Workflow

1. Triage the tier from the brief and draft state: proofread (clean draft, final pass),
   copyedit (clarity/voice/consistency), or substantive (structure, argument, evidence).
2. Structural pass first: does the intro deliver the promise, do sections follow a
   logical spine, does each H2 carry a takeaway, is the CTA staged correctly? Move
   blocks before touching sentences.
3. Line edit for clarity and rhythm: cut 5–10%, kill throat-clearing openers, convert
   passive constructions, break 40+ word sentences, remove filler transitions.
4. Enforce voice and style: run the charter checklist (tone, banned jargon, person,
   capitalization, number style); use PerfectIt or a style sheet for consistency across
   authors.
5. Fact-check every statistic, quote, and claim against the source list; verify primary
   sources exist and are current (within 24 months for data claims unless historical).
6. QA links and media: all links resolve and are relevant, internal links use tracked
   UTM schemes per distribution rules, images have alt text and captions.
7. Screen for plagiarism and undisclosed AI content (Copyscape/Originality.ai);
   investigate matches manually before flagging.
8. Proofread on staging, not just in the doc — formatting, mobile wrapping, and CTA
   placement break between environments.
9. Issue the verdict with the checklist, log recurring author patterns, and update the
   style guide when a new ruling repeats twice.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Grammar & spelling baseline | Grammarly Business | Paid; free tier covers basics |
| Readability & complexity | Hemingway Editor | Free web app; target grade 7–10 B2B |
| Deep style analysis | ProWritingAid | Paid; strongest for long-form consistency |
| Consistency enforcement | PerfectIt | Paid; style-sheet automation |
| Plagiarism / AI screening | Copyscape, Originality.ai | Paid per-credit; manual review of matches |
| Collaborative markup | Google Docs suggesting mode | Never edit over the writer's voice silently |

## Example AI Prompt

```text
Act as a managing editor applying our quality gate to the draft below.

Context:
- Asset type & audience: {FORMAT} for {PERSONA}
- Voice charter summary: {TONE RULES, BANNED JARGON}
- Style guide excerpts: {KEY RULES}
- Source list: {SOURCES FOR CLAIMS}
- Tier requested: {PROOFREAD / COPYEDIT / SUBSTANTIVE}

Deliver:
1. Verdict: publish / revise / rework, with one-paragraph rationale.
2. QA checklist: structure, voice, facts & citations, links & media, plagiarism/AI
   review, proofread — each Pass or Flag with notes.
3. Substantive changes list (what moved/cut and why) — not a silent rewrite.
4. Coaching notes: 3 recurring patterns for this author.
5. If Flag: exact items the writer must fix, with suggested wording where possible.
Draft: {PASTE OR ATTACH}
```

## Edge Cases & Guardrails

- Preserve the author's voice: flag patterns and suggest, never ghost-rewrite a piece
  into the editor's own style — consistency comes from the charter, not one editor's
  taste.
- Fact-check by primary source, not by vibe: a statistic repeated in five blogs is not
  five sources.
- Plagiarism tools throw false positives on common phrases and quoted industry language;
  review every match before accusing anyone.
- Deadline pressure is never a reason to skip compliance checks on claims, legal names,
  or regulated language — cut scope instead.
- Keep a dated changelog for pieces with legal or financial claims; corrections need an
  audit trail.
- The staging proofread is mandatory: publish-ready docs routinely break in the CMS
  (heading levels, image wrapping, CTA blocks).

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Published error rate | <1 per 1,000 words | Reader-flagged corrections monthly |
| Edit turnaround (copyedit tier) | ≤2 business days | >5 days or queue ballooning |
| Revision cycles per draft | ≤2 | 3+ cycles signal brief problems upstream |
| First-time gate pass rate | ≥85% of drafts | Chronic revise verdicts |
| Readability (B2B editorial) | Grade 7–10 | Graduate-school prose or dumbed-down drift |

## Handoffs

- → **content-creation:** return revise/rework verdicts with the exact fix list.
- → **content-distribution:** green-light approved assets with final URLs and alt text.
- → **content-calendar:** flip statuses (Editing → Approved) so the pipeline reflects truth.
- → **content-strategy:** push recurring rulings into the style guide and voice charter.
- ↑ **content-marketing-agent:** escalate systemic voice drift, chronic author quality
  issues, or compliance incidents immediately.
