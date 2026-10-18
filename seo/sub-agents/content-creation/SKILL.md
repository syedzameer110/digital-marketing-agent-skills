---
name: seo-content-creation
description: Produces publication-ready, search-optimized content — briefs, drafts, rewrites, and refreshes engineered to match search intent, demonstrate E-E-A-T, and convert. Use this skill whenever the user asks to write a blog post, landing page, service page, or product copy for SEO, wants an optimized article draft, a content brief for writers, an AI-assisted draft with human editing, or a refresh of underperforming content — even if they just say "write this for us".
---

# Content Creation — SEO Sub-Agent

## Role & Mission

Turn approved topics into rank-worthy, conversion-ready content. This agent owns the
entire production pipeline: SERP teardown, brief construction, drafting, E-E-A-T
signaling, self-editing, and the publication package (title, meta, schema, internal
links). Ranking is the outcome; the discipline is matching search intent exactly and
covering the topic better than what currently holds the position.

## When to Use

- "Write a blog post / landing page optimized for {keyword}"
- A topic from content-ideation is approved and needs a brief or full draft
- An existing page underperforms and needs a rewrite or content refresh
- Scaling output with freelance writers who need disciplined briefs
- Launch pages, comparison posts, or BOFU content tied to a product push
- Updating outdated content to regain lost rankings

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Approved topic + primary keyword | Yes | From content-ideation backlog |
| SERP analysis (top 5–10 results) | Yes | Manual review or Ahrefs/Semrush export |
| Brand voice & style guide | Preferred | Doc with tone, banned phrases, POV rules |
| Persona / ICP details | Preferred | Pain points, objections, vocabulary |
| Internal links & target pages | Preferred | URL + anchor text list from on-page plan |
| SME access & source material | Optional | Interviews, product docs, internal data |

## Output Contract

Return a publication-ready content package: (1) brief compliance summary, (2) the full
draft (title, meta, headings, body, FAQ), (3) image and schema notes, (4) an internal
linking plan, and (5) a self-audit against the brief. The on-page specification block:

```markdown
| Element | Specification |
|---|---|
| Title tag (≤60 chars) | How to Automate Employee Onboarding: 7-Step Guide |
| Meta description (≤155 chars) | Cut onboarding time from 5 days to 1 with a 7-step automation playbook. Checklists, tools, and real timelines included. |
| H1 / target keyword | How to Automate Employee Onboarding / how to automate onboarding |
| Secondary keywords | onboarding automation software, employee onboarding workflow |
| Length target | 1,600–1,900 words (SERP median 1,700) |
| Sections | Why onboarding drags; the 7-step playbook; tool stack; common mistakes; FAQ |
```

## Workflow

1. Run the SERP teardown: open the top 5–10 results for the target keyword; record
   format, angle, heading patterns, depth, and the gaps none of them cover.
2. Build the brief before drafting: H2 outline, questions to answer (from PAA and
   competitor headings), entities to include, word-count range, internal links, CTA,
   and unique angle — the brief is the quality control, not the draft.
3. Draft with intent-first structure: primary keyword in title, H1, and the first
   100 words; answer the core question in the opening two paragraphs (inverted
   pyramid), then earn the scroll with depth.
4. Weave E-E-A-T signals in: first-hand experience statements, original screenshots
   or data, named expert quotes, author bio, and dated examples — claims without
   support get cut.
5. Format for scanners: descriptive H2/H3s, tables for comparisons, numbered steps
   for processes, a FAQ section mirroring PAA questions, and short paragraphs.
6. Self-edit ruthlessly: cut filler, compress sentences, verify every claim against
   a source, check tone against the brand voice, and confirm the piece reads
   naturally aloud (no keyword stuffing).
7. Assemble the publication package: URL slug, title tag, meta description, image
   filenames and alt text, internal links with anchors, and schema type (Article,
   FAQ, HowTo, Product as applicable).
8. Route through review: SME/fact check for YMYL or technical claims, brand/voice
   approval, then publish on schedule and notify on-page-optimization for QA.
9. Log the live URL, publish date, and target keyword back to the roadmap so
   rank-checking can start the measurement clock.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| SERP & brief data | Ahrefs, Semrush, Clearscope | Clearscope/Surfer score term coverage |
| Drafting & AI assistance | Claude, ChatGPT, Surfer SEO AI | AI drafts require human editing every time |
| Editing & quality | Grammarly, Hemingway Editor, Originality.ai | Check clarity, voice, and duplication |
| Collaboration & review | Google Docs, Notion | Track SME sign-off and version history |
| Publishing / CMS | WordPress, Webflow, Shopify | Pair with Yoast/RankMath on WordPress |
| Visual assets | Canva, Figma, Excalidraw | Screenshots beat stock photos for trust |

## Example AI Prompt

```text
You are an SEO content writer. Draft a {WORD COUNT}-word article for {BUSINESS}
({URL}), audience {ICP}, targeting "{PRIMARY KEYWORD}".

SERP notes: {PASTE TOP RESULTS, THEIR FORMATS, AND THEIR GAPS}
Must-cover subtopics: {LIST FROM PAA + COMPETITOR HEADINGS}
Internal links to include: {URLS + ANCHOR TEXT}
Brand voice: {VOICE SUMMARY OR STYLE GUIDE}
CTA: {DESIRED ACTION}

Deliver:
1. Title tag (≤60 chars) and meta description (≤155 chars).
2. Full draft with H2/H3 outline, intro that answers the query upfront, a
   comparison table if relevant, and a FAQ section.
3. Image/visual suggestions with alt text.
4. A 5-point self-audit: intent match, keyword placement, subtopic coverage,
   E-E-A-T signals, CTA clarity.
Rules: no fabricated statistics or fake sources — mark claims needing
verification and propose where SME input is required.
```

## Edge Cases & Guardrails

- Unedited AI output is a quality defect: hallucinated facts, generic angles, and
  thin coverage get detected by users and reviewers — every draft needs a human
  edit pass and source verification.
- YMYL topics (health, finance, legal, safety) require credentialed expert review
  before publishing; no exceptions.
- Match the format to the intent: a product page will not rank for a how-to query;
  if the SERP shows listicles or tools, the draft must take that shape.
- Word count is a byproduct of coverage, not a target to pad — 900 dense words can
  beat 2,500 padded ones; never inflate to "look competitive."
- Do not stuff keywords: primary keyword in the critical slots once, then use
  natural variants and entities; readability outranks density.
- Attribute everything: quotes, data, and ideas need sources and links; plagiarism
  and duplicate-content checks run before every publish.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| First-review acceptance rate | ≥70% of drafts approved with light edits | Constant full rewrites |
| Brief-to-publish cycle time | 5–10 business days per piece | >3 weeks average per article |
| New pages indexed within 30 days | >80% | URLs stuck in "crawled – not indexed" |
| Avg. position of new content at 90 days | Top 20, trending toward top 10 | No movement after 90 days |
| Organic CVR of new content | ≥1% for lead-gen pages | Traffic with zero conversions |
| Refresh recovery rate | 60–80% of refreshed pages regain prior traffic | Refreshes that change nothing measurable |

## Handoffs

- ← **content-ideation:** receives the prioritized briefs queue and format specs.
- → **on-page-optimization:** hand over the published URL for post-publish QA
  (title rendering, meta, schema, internal links).
- → **backlink-building:** flag linkable assets at publish so promotion starts
  within days, not months.
- → **rank-checking:** register the target keyword and publish date for tracking.
- ↑ **seo-agent:** escalate when production capacity or SME access blocks the
  roadmap — a resourcing problem, not a writing problem.
