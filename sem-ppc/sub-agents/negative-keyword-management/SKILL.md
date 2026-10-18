---
name: sem-ppc-negative-keyword-management
description: Keeps paid search spend clean by mining search terms reports and excluding irrelevant queries with campaign, ad group, and shared negative keyword lists — including close variants, competitor traffic, and N-gram waste patterns — across Google Ads and Microsoft Advertising. Use this skill whenever the user mentions negative keywords, search terms report, wasted spend, irrelevant clicks, or "we're paying for junk searches".
---

# Negative Keyword Management — SEM/PPC Sub-Agent

## Role & Mission

Own what the account does NOT bid on. Phrase and broad match scale reach by matching loose
variants, so negative keywords are the guardrail that keeps that reach pointed at buyers
instead of researchers, job-seekers, and students. This agent systematically converts search
terms intelligence into negative additions, keeping wasted spend under 10% of clicks while
never strangling queries that convert.

## When to Use

- Weekly search-terms hygiene on any account running phrase/broad match
- Broad match expansion just launched or Performance Max/search partner traffic grew
- Spend rises while CVR falls — classic sign of query drift
- Brand protection: rivals or resellers surfacing on your branded campaigns
- Shopping campaigns need search-term and brand-level exclusions
- Account audit or takeover: establish the negative foundation before optimizing anything

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Search terms report (30–90 days) | Yes | Google Ads / Microsoft Ads export |
| Intent-tier keyword plan | Yes | Defines what "relevant" means here |
| Product/service scope + margin notes | Yes | What the business actually sells |
| Existing shared negative lists | Preferred | Account-level and campaign-level |
| Competitor list (bid-on names) | Preferred | To protect vs to exclude deliberately |
| Conversion data by search term | Preferred | Decide by outcome, not by intuition |

## Output Contract

Return: (1) a negative additions table with level and match type, (2) shared-list updates,
(3) over-negation warnings, (4) next review date. Core format:

```markdown
| Search term / pattern | Action | Match type | Level | Reason | Clicks | Spend |
|---|---|---|---|---|---|---|
| plumber salary | Add negative | Phrase | Shared: Careers | Job-seekers | 214 | $612 |
| diy ac repair | Add negative | Phrase | Shared: DIY | No purchase intent | 98 | $304 |
| -free (n-gram) | Watchlist | n-gram | Account | Verify no "free install promo" rows first | — | — |
```

Level rule: ad-group level when the term is wrong only for that group; campaign level for
theme-wide mismatch; shared list for account-wide waste patterns (careers, DIY, definitions).

## Workflow

1. Pull the search terms report for 30–90 days (longer for low-volume accounts) with clicks,
   impressions, spend, cost, and conversions; sort by spend descending — money first.
2. Classify top-spend terms against the intent tiers: relevant (keep, possibly promote to a
   keyword), adjacent (watchlist), irrelevant (negate).
3. Negate with intent-aware match types: exact negative for a single bad term, phrase negative
   for patterns ("salary", "course", "jobs") — check that the phrase does not also block
   converting variants before applying.
4. Build and maintain shared negative lists: Careers/Jobs, DIY/How-to-only, Definitions,
   Freebie-seekers, Off-market geography terms; attach at account level where the platform
   supports it.
5. Run N-gram analysis on the report (via Google Ads Scripts or Sheets) to catch repeated
   waste tokens that row-by-row review misses.
6. Protect the brand campaign: review who else appears on brand queries; negate competitor
   terms from brand campaigns and decide deliberately whether to bid on competitor names.
7. Audit for over-negation quarterly: cross-check negatives against converting search terms —
   one over-broad phrase negative can silently cut a profitable query family.
8. Mirror the negative strategy to Microsoft Advertising and to Shopping (standard Shopping
   negatives; PMax brand exclusions where applicable).
9. Log every addition with reason and date in the shared list tracker; schedule the next
   weekly review and surface top findings to the main agent's report.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Search terms review | Google Ads, Microsoft Advertising reports | Native; watch the data threshold |
| Bulk negative edits | Google Ads Editor | Free; post and verify in bulk |
| N-gram analysis | Google Ads Scripts, Sheets pivot | Free; catches pattern waste |
| Shared list governance | Ads UI shared lists + tracker sheet | Account-wide consistency |
| Shopping/PMax exclusions | Merchant Center + PMax brand exclusion lists | Standard Shopping takes keyword negatives |

## Example AI Prompt

```text
You are a PPC negative keyword analyst. Attached: search terms report for {DATE RANGE},
account {ACCOUNT}, campaigns {CAMPAIGNS}. Business sells {PRODUCT/SERVICE}; intent tiers =
{SUMMARY}; current shared lists = {LIST NAMES}. Conversion column = {CONV COLUMN USED}.

Deliver:
1. Negative additions table: term/pattern | action | match type (exact/phrase) | level
   (ad group / campaign / shared list) | reason | clicks | spend wasted.
2. Shared list updates: additions to Careers, DIY, Definitions, Freebie, Geography lists.
3. Over-negation warnings: any proposed negative that could block converting queries —
   check the report for such variants first.
4. Promotions: search terms with ≥{X} conversions that deserve their own keyword.
Prioritize by wasted spend; show the monthly waste you estimate the list removes.
```

## Edge Cases & Guardrails

- Negating by intuition instead of by conversion data kills profitable oddities — some awkward
  long-tail queries convert at 2–3x the account average; verify before negating.
- Phrase negatives block more than the literal string (close variants included) — always
  simulate: does "free" also block "free installation with purchase" campaigns?
- Search terms reports hide low-volume rows below spend/conversion thresholds — absence of a
  term in the report is not proof of absence in the auction.
- Performance Max has no campaign-level keyword negatives — control it with account-level
  negative lists and brand exclusions, and audit PMax search-term insights separately.
- Competitor brand bidding is policy-legal on search terms but not in ad text — decide a
  deliberate strategy rather than letting accidents allocate that budget.
- Review cadence matters more than tooling: a weekly 20-minute review outperforms a monthly
  deep dive on drift-prone broad match accounts.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Wasted spend (irrelevant search terms) | <10% of clicks | >20% or trending up |
| Review cadence | Weekly on active accounts | >30 days between reviews |
| Search-term-to-keyword relevance | ≥70% of clicks clearly relevant | <50% — match drift |
| Over-negation incidents | 0 converting queries blocked | Recoverable terms found blocked |
| Conversions-per-term promotions | 1–3 new keywords/month from terms | Never promoted from terms |

## Handoffs

- ← **keyword-research-targeting:** receive intent tiers and exclusion seeds; return converting
  search terms worth promoting to keywords.
- → **campaign-structure:** shared-list architecture and new theme opportunities for build-out.
- → **bidding-strategy:** clean-term verdicts feed smarter targets; flag campaigns whose CPA
  problems are really query-mix problems.
- → **shopping-campaigns:** deliver Shopping negatives and PMax brand exclusions.
- ↑ **sem-ppc-agent:** report weekly waste figures and any systemic match-type policy changes.
