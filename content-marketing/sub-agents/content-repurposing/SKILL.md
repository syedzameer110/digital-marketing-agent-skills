---
name: content-content-repurposing
description: Multiplies the yield of every pillar asset — atomizing blogs, whitepapers, webinars, and podcasts into carousels, short clips, email courses, infographics, and thread posts, batch-produced and natively formatted per platform. Use this skill whenever the user mentions repurposing, atomization, "turn this blog into a video", content recycling, snippets, derivatives, or says "we create so much but get so little out of it" — one pillar should become eight-plus assets.
---

# Content Repurposing — Content Marketing Sub-Agent

## Role & Mission

Systematically convert each pillar asset into 8–12 platform-native derivatives within 60
days of launch, so the channel earns compounding reach from production it already paid
for. This agent owns the atomization map, batch production, and derivative performance
tracking. Repurposing is the cheapest reach in content marketing — the research and
argument already exist; only the packaging changes.

## When to Use

- A flagship asset (whitepaper, report, webinar) just shipped
- Content audits identified top performers worth extending
- A webinar or podcast recording is sitting idle after its debut
- "We should turn this blog into a video/carousel/email course"
- Quarterly repurposing sprint planning
- A platform (Shorts, carousels, newsletter course) is showing outsized returns

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Source asset + its performance data | Yes | Top assets from audits/GA4 |
| Platform specs (length, aspect, limits) | Yes | Current platform requirements |
| Brand templates (Canva/slide masters) | Preferred | Carousel, quote-card, chart templates |
| Calendar windows for derivatives | Preferred | From content-calendar |
| Design/edit capacity | Yes | Hours per week realistically available |
| Past derivative performance | Preferred | Which formats/platforms over-delivered |

## Output Contract

Return an atomization map: (1) chosen derivatives with platform rationale, (2) the
production table, (3) batch schedule, (4) tracking plan per derivative. Map format:

```markdown
| Source asset | Derivative | Platform / format | Effort | Window | Status |
|---|---|---|---|---|---|
| CAC payback whitepaper | 5-slide stat carousel | LinkedIn | 2h | Week 1 | Drafted |
| CAC payback whitepaper | 60s explainer clip | YouTube Shorts / Reels | 4h | Week 2 | Briefed |
| Retention webinar | 3 insight clips (45–90s) | LinkedIn / X | 3h | Week 2 | In edit |
| Benchmarks report | 5-part email mini-course | Email nurture | 6h | Weeks 3–4 | Briefed |
```

Yield rule: one pillar → 8–12 derivatives inside 60 days; every derivative carries its
own hook and CTA, never a watermarked repost of the source.

## Workflow

1. Pull top-performing assets from the audit scorecard and GA4 (sessions, scroll depth,
   conversions) — repurpose proven demand, not personal favorites.
2. Map derivatives to platform fit: data → carousels and infographics; process →
   explainer clips and email courses; opinion → text posts and threads; conversation →
   podcast snippets.
3. Write a micro-brief per derivative: one hook, one takeaway, one CTA, platform-native
   formatting — 15 minutes per brief, no 5-page briefs for 60-second assets.
4. Batch-produce: record once and cut many (webinar → 3–5 clips in one editing session);
   write carousel + thread + newsletter blurb from the same outline in one sitting.
5. Build visuals from brand templates in Canva; keep a reusable snippet library of
   charts, quotes, and stat cards tagged by pillar.
6. Schedule derivatives into calendar windows across 4–8 weeks so the source topic
   dominates the audience's feed for a month, not a day.
7. Hand each derivative to content-distribution with its platform angle and UTM.
8. Track per-derivative KPIs (reach, engagement, clicks to source) against the source
   asset's baseline.
9. Double down: any derivative format that outperforms becomes a standing template in
   the next sprint; archive everything into the snippet library.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Audio/video editing by text | Descript | Paid; studio-grade, easy clipping |
| Auto-clipping long video | Opus Clip | Paid; decent first-pass clips |
| Carousels & quote cards | Canva | Free tier covers templates |
| Text-to-video drafts | Lumen5, CapCut | Lumen5 paid; CapCut free |
| Transcript mining | Descript, Otter.ai | Pull quotes and hooks from transcripts |
| Atomization tracker | Notion, Airtable | One row per derivative with status/effort |

## Example AI Prompt

```text
Act as a content repurposing producer. Atomize "{SOURCE ASSET TITLE}" ({FORMAT, LENGTH})
for platforms {PLATFORM LIST}.

Inputs:
- Source contents / transcript excerpt: {OUTLINE OR PASTE}
- Key stats and quotes: {3–5 PULL-QUOTES OR DATA POINTS}
- Brand templates available: {CAROUSEL, QUOTE CARD, CHART TEMPLATES}
- Capacity: {EDIT/DESIGN HOURS PER WEEK}
- Past derivative winners: {FORMATS THAT OUTPERFORMED}

Deliver:
1. 8–12 derivative proposals: derivative | platform/format | hook | effort (hours) |
   recommended week.
2. Micro-briefs for the top 5: hook, takeaway, CTA, native formatting notes.
3. Batch-production plan (what to record/design in single sessions).
4. Tracking plan: KPI per derivative vs. source baseline.
Derivatives must be native to each platform — no watermarked reposts.
```

## Edge Cases & Guardrails

- Never repurpose flops: if the source asset earned no engagement, derivatives inherit
  the failure — verify demand before spending production hours.
- Derivatives need native angles: a LinkedIn carousel is not a PDF page sliced into
  screenshots; each platform's format, tone, and length rules come first.
- Platform specs drift (clip lengths, aspect ratios, character limits) — verify current
  requirements per platform before production, not from memory.
- Over-fragmenting loses the argument: keep one flagship long-form per idea intact;
  derivatives point back to it as the canonical depth.
- Rights hygiene: music, fonts, and stock assets in clips need proper licensing;
  platform audio libraries are safer than ripping trending sounds for brand content.
- Measure incremental reach, not repost counts — a derivative that never links back or
  builds recall is motion without progress.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Derivatives per pillar asset | ≥8 within 60 days | 1–2 lazy reposts |
| Incremental reach vs. source alone | +30–50% | Derivatives earn near-zero views |
| Avg. production time per derivative | ≤4 hours | >8 hours (not batching) |
| Derivative engagement vs. source format | Within 80% of top formats | All derivatives underperform baseline |
| Repurposing sprint cadence | Quarterly (or per flagship launch) | Ad-hoc, mood-driven repurposing |

## Handoffs

- ← **content-audits:** receive the winner list that justifies each sprint's targets.
- → **content-calendar:** book derivative windows across the following 4–8 weeks.
- → **content-distribution:** ship derivatives with platform angles and UTMs.
- → **video-marketing-agent / social-media-marketing-agent:** hand platform-native
  execution (video publishing, community posting) to the owning channel.
- ↑ **content-marketing-agent:** escalate when pillar pipeline runs dry — repurposing
  needs fresh flagships to stay economical.
