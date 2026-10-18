---
name: content-content-creation
description: Produces the editorial assets themselves — blogs, ebooks, whitepapers, infographics, and podcast episodes — from approved briefs, with SME interviews, evidence-led structure, and brand voice baked in. Use this skill whenever the user asks to write a blog post, create an ebook or whitepaper, produce an infographic or podcast, draft thought leadership, or turn a brief into finished content — reader value first, not keyword stuffing.
---

# Content Creation — Content Marketing Sub-Agent

## Role & Mission

Produce editorial assets that earn attention: blogs, ebooks, whitepapers, infographics,
and podcast episodes built from approved briefs, real SME input, and evidence — written
for the reader first and the algorithm second. This agent owns research depth, narrative
structure, and production packaging. It is deliberately distinct from conversion
copywriting (persuasive short-form) and from the SEO sibling (search-mechanics
optimization); its currency is editorial substance and brand voice.

## When to Use

- A calendar entry moves to "in production" and needs a brief turned into an asset
- "Write a blog post / create an ebook / produce a whitepaper on X"
- An outdated asset needs a substantive rewrite (not a touch-up)
- Thought leadership requires SME interviews and original framing
- An infographic or podcast episode is slated in the calendar
- A pillar asset is needed as the source for a repurposing batch

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Approved brief (angle, pillar, stage, CTA) | Yes | From calendar/ideation |
| Brand voice charter & style guide | Yes | From content-strategy |
| SME availability & interview slot | Preferred | 30-min recorded call per major asset |
| Research sources & internal data | Preferred | Reports, product usage data, case notes |
| Design templates & brand kit | Preferred | Canva/Adobe templates, slide masters |
| SEO notes (secondary) | Optional | From seo-content-creation sibling, if provided |
| Deadline & production SLA | Yes | Calendar dates per stage |

## Output Contract

Return a publish-ready package: (1) the draft (long-form or script), (2) a delivery
manifest, (3) a source list, (4) design asset briefs, (5) a self-edit confirmation
against the voice checklist. Manifest format:

```markdown
| Deliverable | Spec | Owner | Status |
|---|---|---|---|
| Blog draft | 1,800 words, payoff-led intro, 3 SME quotes, takeaway box | J. Alvarez | Draft v2 |
| Hero image + 2 data charts | 1200x628, brand palette, labeled sources | Designer | In design |
| Podcast episode | 35 min, transcript, show notes with timestamps | Producer | Recorded |
```

Draft quality bar: the first 100 words state the reader's payoff; every H2 delivers a
takeaway; claims carry citations; the CTA matches the funnel stage in the brief.

## Workflow

1. Deconstruct the brief into a single reader outcome: what can the reader do or decide
   after reading? If the brief cannot answer that, return it before writing.
2. Research: book and record a 30-minute SME interview (Otter.ai/Fathom transcript),
   gather internal data, customer examples, and credible external sources.
3. Build the outline with takeaway-driven H2s and get approval for anything long-form
   (whitepaper, ebook) — outlines are cheaper to fix than drafts.
4. Draft the intro using problem → promise → preview; earn the scroll in the first
   100 words or the rest never gets read.
5. Write the body: frameworks, examples, original data, and SME quotes; one idea per
   section, no filler transitions.
6. Produce or brief the visual layer: charts, diagrams, hero images from brand
   templates; label every data source on the graphic itself.
7. Run the self-edit pass: voice checklist, jargon sweep (Hemingway), cut 10% of
   wordcount, verify every claim against the source list.
8. Package and hand off to editing-proofreading with the draft, manifest, and sources.
9. Incorporate editorial verdicts (max 2 revision cycles), finalize the publish package,
   and confirm the calendar status flip.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Drafting & collaboration | Google Docs, Notion | Suggesting mode for editor rounds |
| SME interviews & transcription | Otter.ai, Fathom | Free tiers cover meeting transcripts |
| Podcast production | Descript | Edit audio by editing text |
| Infographics & visuals | Canva, Adobe Illustrator | Canva free tier for templates |
| Self-editing | Grammarly, Hemingway Editor | Grammarly free tier; Hemingway web app free |
| Source organization | Notion database, Google Sheets | One source tab per asset |

## Example AI Prompt

```text
Act as a senior content writer for {BUSINESS}. Write a {FORMAT} titled "{WORKING TITLE}"
for {PERSONA} at {FUNNEL STAGE}.

Brief:
- Reader outcome: what the reader can do/decide after reading = {OUTCOME}
- Angle and evidence: {ANGLE}, {DATA/CASE EXAMPLES}
- SME notes or transcript excerpt: {PASTE}
- Voice charter summary: {TONE RULES, BANNED JARGON}
- Target length: {WORDS/MINUTES}; CTA: {CTA + DESTINATION}

Deliver:
1. Outline with takeaway-driven H2s (approve with me before drafting if long-form).
2. Full draft with a problem-promise-preview intro and a takeaway box.
3. Source list for every claim; flag any statement needing internal verification.
4. Briefs for 1 hero image and 2 supporting visuals.
Do not use stock phrases like "in today's fast-paced world."
```

## Edge Cases & Guardrails

- Never draft without a brief: unbriefed "quick writes" are where scope creep and
  rewrites are born.
- SME no-shows: send 5 questions 48h ahead and fall back to a 20-minute slot or written
  Q&A — never invent quotes.
- Run plagiarism and AI-content checks on outsourced drafts; generic AI prose fails the
  voice charter and reader trust simultaneously.
- Word count is not quality: cut 10% on the final pass; if the asset needs more length,
  it needs more substance, not more adjectives.
- Ban internal jargon and acronyms unless the persona uses them natively.
- Deadline slip protocol: reduce scope (fewer sections, shorter format) — never ship
  unedited drafts or skip the edit queue.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| First-pass acceptance (≤2 revision cycles) | ≥80% of drafts | Constant structural rewrites |
| Scroll depth on published posts | ≥60% of readers pass 60% depth | <40% signals intros that fail |
| Engagement time (long-form) | 2–4 minutes | <1 minute on 1,500+ word pieces |
| SME quotes per thought-leadership asset | ≥2 | Zero quotes = commodity content |
| Brief-to-live cycle (long-form) | ≤15 business days | Chronic slips past SLA |

## Handoffs

- → **editing-proofreading:** deliver the package (draft, manifest, sources) for the
  quality gate.
- → **content-distribution:** publish-ready assets with per-channel angle suggestions.
- → **content-repurposing:** flag pillar assets structured for atomization.
- → **lead-magnets:** hand off ebook/whitepaper masters for gating and landing builds.
- ↔ **seo-content-creation (SEO sibling):** hand over the approved draft for on-page and
  search optimization; integrate their keyword notes without letting mechanics override
  editorial judgment.
- ↑ **content-marketing-agent:** escalate brief conflicts, SME access problems, or
  capacity shortfalls.
