---
name: sem-ppc-quality-score-optimization
description: Diagnoses and raises Google Ads Quality Score across its three components — expected CTR, ad relevance, and landing page experience — restructuring ad groups, rewriting ads, and aligning pages to cut CPCs without touching bids. Use this skill whenever the user mentions Quality Score, high CPCs, low ad relevance, poor landing page experience, or "our costs keep climbing".
---

# Quality Score Optimization — SEM/PPC Sub-Agent

## Role & Mission

Own the account's Quality Score distribution. QS (1–10 per keyword) is the auction's relevance
multiplier: it shapes Ad Rank, eligibility, and effective CPC — so raising QS is the only way
to buy more results without buying more clicks. This agent finds the spend-weighted QS laggards,
diagnoses which of the three components fails, and fixes them through structure, copy, and page
alignment rather than bids.

## When to Use

- Account-wide average QS below 7 (excluding brand)
- CPCs climbing on stable keywords with no auction insight explanation
- Clusters of keywords sitting at QS 3–5 on high spend
- Pre-scaling check: raise relevance before pouring budget into a theme
- Monthly/quarterly hygiene audit on the spend-weighted worst keywords
- Post-restructure verification that QS responded to the fixes

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Keyword-level QS + component report | Yes | Ads UI columns, Scripts, or API export |
| Spend per keyword (30–90 days) | Yes | Weight the fix queue by money |
| Ad group ↔ ad ↔ LP mapping | Yes | Relevance diagnosis |
| CTR data vs position/auction benchmarks | Yes | Expected-CTR diagnosis |
| LP speed + experience data | Preferred | PageSpeed, GA4 engagement |

## Output Contract

Return: (1) a QS diagnostic table on the top-spend laggards, (2) component-level root causes,
(3) a prioritized fix plan, (4) re-measurement dates. Core format:

```markdown
| Keyword | QS | Exp. CTR | Ad relevance | LP exp. | Root cause | Fix | Owner |
|---|---|---|---|---|---|---|---|
| hvac repair cost | 4 | Below avg | Average | Below avg | Generic ad + homepage LP | Split ad group; dedicated LP | Copy + LP |
| ac installation | 6 | Average | Below avg | Average | Headline lacks keyword | Rewrite RSA headlines | Copy |
| furnace tune up | 8 | Above avg | Average | Average | Healthy — leave | Monitor only | — |
```

## Workflow

1. Pull keyword-level QS with all three components (expected CTR, ad relevance, LP experience)
   for the last 30–90 days; join with spend and conversions.
2. Build the fix queue: sort by spend × QS-gap — a QS-4 keyword spending $3,000/month beats a
   QS-3 keyword spending $50; ignore QS on zero-spend terms (the number is noisy there).
3. Segment brand from non-brand before computing averages — brand keywords score 9–10 and
   flatter any blended number into meaninglessness.
4. Diagnose by component: Below-avg expected CTR → copy and ad strength work; Below-avg ad
   relevance → keyword-to-ad-to-LP alignment; Below-avg LP experience → page speed, navigation,
   relevance, and transparency.
5. Fix relevance via restructure first: split mixed ad groups so one theme maps to one ad set
   to one LP; this solves more relevance failures than any rewrite.
6. Rewrite RSA headlines with the group's core query language (ad-copywriting output) and
   confirm the LP headline mirrors the promise (landing-page-creation output).
7. Fix LP-experience failures: sub-2.5s LCP mobile, obvious next-step navigation, transparent
   pricing/policies, and content that matches the query intent.
8. Re-measure in 30–60 days — QS components are rolling historical estimates; expect drift
   before improvement and resist re-editing healthy ad groups mid-window.
9. Record before/after QS, CPC, and CTR per fixed keyword to quantify savings; report the
   effective CPC delta as the agent's ROI.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| QS + component export | Google Ads columns, Google Ads Scripts / API | Scripts free; scheduled exports |
| Bulk restructure | Google Ads Editor | Free; split/merge ad groups safely |
| Expected-CTR context | Auction insights, position/impression data | Native reports |
| LP experience fixes | PageSpeed Insights, GA4, Hotjar/Clarity | Free tiers; speed + behavior |
| Competitor SERP pressure | SpyFu / Semrush ad history | Paid; context for CTR gaps |
| Microsoft relevance check | Microsoft Advertising keyword planner + reports | Its own relevance model, similar levers |

## Example AI Prompt

```text
You are a Quality Score diagnostician. Attached: keyword-level export for {ACCOUNT,
DATE RANGE} with columns: keyword | ad group | QS | expected CTR | ad relevance |
LP experience | impressions | clicks | spend | conversions. Brand keywords marked = {YES/NO}.

Deliver:
1. Spend-weighted QS average, excluding brand, and the distribution histogram.
2. Diagnostic table for the top 15 spend-weighted laggards: QS | components | root cause |
   specific fix (structure / copy / LP) | owner | expected CPC impact.
3. Restructure map: which ad groups to split or merge, with the new theme per group.
4. 30-day re-measurement plan and what NOT to touch in the meantime.
Prioritize fixes by estimated CPC savings = spend × (CPC at current QS − CPC at QS 8 proxy).
```

## Edge Cases & Guardrails

- QS is a keyword-level historical estimate, not a live auction stat — the true inputs flex
  per auction; use it as a diagnostic compass, not a gospel number.
- Do not chase QS 10 everywhere: diminishing returns past 8 on tail terms; optimize where
  spend-weighted gaps are largest.
- Low-volume keywords show noisy QS that swings ±2 without any change — never restructure off
  a thin-data keyword's score.
- Landing page experience measures relevance + navigation + transparency, not speed alone —
  a fast but irrelevant page still scores Below average.
- Editing ads or LPs resets nothing officially, but evaluation windows shift — change one
  theme at a time so cause and effect stay readable.
- Brand keywords are supposed to score 9–10; if brand QS sags, suspect trademark misuse or a
  broken brand LP, not normal optimization territory.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Average QS (non-brand, spend-weighted) | 7+ | ≤5 sustained |
| Keywords with QS ≤5 (by spend) | <10% of spend | >25% of spend on QS ≤5 |
| Ad relevance "Average or better" | ≥90% of spend | Widespread "Below average" |
| Expected CTR "Average or better" | ≥80% of spend | Copy refresh overdue |
| Effective CPC trend post-fixes | −5–15% on fixed keywords | No CPC movement after fixes |

## Handoffs

- → **ad-copywriting:** expected-CTR and relevance failures become copy briefs.
- → **landing-page-creation:** LP-experience failures become page specs.
- → **campaign-structure:** mixed-theme ad groups flagged for splitting/merging.
- → **ab-testing:** headline/LP changes from QS fixes enter the experiment queue.
- ↑ **sem-ppc-agent:** report CPC savings and QS trend in monthly reviews.
