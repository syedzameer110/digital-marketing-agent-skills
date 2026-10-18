---
name: seo-on-page-optimization
description: Optimizes every on-page ranking element — meta titles, meta descriptions, heading structure, URL slugs, image alt text, and internal links — with before/after tracking so impact is measurable. Use this skill whenever the user wants to optimize a page, rewrite titles or metas, fix duplicate meta tags, improve click-through rate from Google, restructure URLs, fix heading hierarchy, or act on quick-win keywords — even if they just say "this page isn't ranking".
---

# On-Page Optimization — SEO Sub-Agent

## Role & Mission

Own every ranking lever that lives on the page: title tags, meta descriptions,
headings, URL structure, image signals, and internal links. This agent converts
existing content into its maximum SERP performance — the fastest ROI in the channel,
because pages ranking 5–15 can often reach page one with optimization alone, without
new content or links. Every change is logged so movement can be attributed.

## When to Use

- "Optimize this page" or a page ranks 5–15 and needs a push to page one
- Low CTR in Search Console despite healthy impressions
- Duplicate, missing, or truncated titles and meta descriptions at scale
- New content shipped and needs its publish QA pass
- Quick-wins list arrived from keyword-research
- URL/slug restructuring or a sitewide meta refresh is planned

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Target URL(s) + primary keyword(s) | Yes | Keyword map or page inventory |
| Search Console data (impressions, CTR, position) | Yes | Performance report per URL |
| Crawl export (titles, metas, H1s, slugs) | Preferred | Screaming Frog SEO export |
| CMS edit access | Yes | WordPress, Webflow, Shopify |
| Quick-wins list | Preferred | Output of keyword-research |
| Brand name & character conventions | Optional | Title suffix rules, voice limits |

## Output Contract

Return an optimization changelog: (1) per-URL before/after table, (2) sitewide title
and meta templates where patterns repeat, (3) internal-link additions with anchors,
(4) priority and expected impact per URL, (5) recheck date for measurement. Core
format:

```markdown
| URL | Element | Before | After | Rationale |
|---|---|---|---|---|
| /payroll-software | Title | Payroll Software – Home – {Brand} | Payroll Software for HR Teams | {Brand} | Keyword first; 38→24 avg pos, truncated display |
| /payroll-software | Meta | (missing) | Run payroll for your whole team in minutes. See pricing, integrations, and a live demo. | Missing meta = Google rewrite risk on money page |
| /blog/hr-audit | H1 | Insights | HR Compliance Audit: 12-Step Checklist | H1 ignored the target keyword entirely |
```

## Workflow

1. Pull the working set with metrics: Search Console queries, impressions, CTR, and
   average position per URL; segment money pages from supporting content.
2. Audit title tags: unique per page, primary keyword front-loaded, ≤60 characters,
   brand suffix last, and phrased to earn the click rather than just name the topic.
3. Rewrite meta descriptions: ≤155 characters, keyword + concrete benefit + implicit
   CTA, unique per URL; fix every duplicate and missing meta before anything else.
4. Verify heading structure: exactly one H1 that matches the page's target intent,
   logical H2/H3 nesting, secondary keywords and entities in subheads where natural.
5. Review URL slugs: short, hyphenated, keyword-bearing, no dates, parameters, or
   stop-word clutter; if a slug must change, plan the 301 redirect in the same ticket.
6. Fix image signals: descriptive filenames, accurate alt text, compression, proper
   dimensions, and lazy-loading below the fold.
7. Repair the internal link graph: add 3–5 contextual links into the page from
   relevant pages with descriptive anchors, fix orphan money pages, and prune
   boilerplate "click here" anchors.
8. Resolve cannibalization: where two pages chase one term, differentiate intents,
   consolidate with a 301, or apply a canonical — never leave both live untouched.
9. Log every change in the before/after register with dates, then notify
   rank-checking to start the 4–8 week measurement window.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Crawl & meta audit | Screaming Frog (free ≤500 URLs) | Bulk export of titles, metas, H1s, slugs |
| CTR & position truth | Google Search Console | Free; the only source Google confirms |
| Content scoring | Surfer SEO, Clearscope | Term coverage vs top-ranking pages |
| WordPress helpers | Yoast SEO, Rank Math, Link Whisper | Templates + bulk editing + link suggestions |
| Bulk edits & tracking | Google Sheets | Changelog with before/after and dates |
| SERP display preview | Portent SERP preview tool, Rich Results Test | Check truncation before shipping |

## Example AI Prompt

```text
Act as an on-page SEO specialist. Optimize the pages below for {SITE}.
For each URL I provide: current title, meta description, H1, target keyword,
and Search Console stats (impressions, clicks, CTR, avg position).

{PASTE URL TABLE OR CRAWL EXPORT}

For every URL return:
1. Rewritten title tag (≤60 chars) and meta description (≤155 chars).
2. Recommended H1 and any H2 changes, with the exact wording.
3. A suggested slug — only if the current one hurts relevance — flagged for 301.
4. Three internal-link suggestions (source page + anchor text) pointing at it.
5. Priority (P1–P3) and the expected impact (position or CTR movement).
Constraints: brand = {BRAND}; titles must earn clicks, not just contain
keywords; no keyword stuffing; keep language natural for humans first.
```

## Edge Cases & Guardrails

- Never mass-edit titles and metas site-wide in one day: batch changes and measure
  per batch, or attribution becomes impossible when rankings move.
- Changing URLs without 301s destroys accrued equity — only change slugs when the
  relevance win justifies migration risk, and never during peak season.
- Google rewrites a large share of titles; front-load the keyword and keep the brand
  short so even truncation or rewriting preserves relevance signals.
- Meta descriptions are a CTR lever, not a direct ranking factor — still never leave
  duplicates at scale, but do not expect meta text alone to lift positions.
- Re-check the live SERP before rewriting anything: if the page targets the wrong
  intent, no title tweak will save it — escalate to content-creation instead.
- Do not optimize against tracker noise: wait out volatility and use Search Console
  as the tiebreaker when third-party tools disagree.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Title tag compliance (unique, ≤60 chars) | 100% of indexable pages | >5% duplicates or missing |
| Meta description coverage | >95% unique and populated | Missing metas on money pages |
| Organic CTR at positions 1–3 | 25–40% | <15% while impressions grow |
| Orphaned money/content pages | 0 | Key landing pages with no internal links |
| Position lift after optimization | +2–5 positions in 4–8 weeks | No movement after 90 days |
| Cannibalized keyword targets | 0 | Two+ pages trading positions for one term |

## Handoffs

- ← **keyword-research:** receives the quick-wins list — the highest-ROI input.
- ← **content-creation:** receives published URLs for the post-publish QA pass.
- → **rank-checking:** register every optimized URL and its change date.
- → **reporting:** feed the before/after changelog for movement attribution.
- → **technical-seo:** route slug changes and redirect plans that need dev work.
- ↑ **seo-agent:** escalate when optimization alone cannot close the gap and
  content investment is required.
