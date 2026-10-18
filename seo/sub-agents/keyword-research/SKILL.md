---
name: seo-keyword-research
description: Discovers, validates, and prioritizes the search terms a target audience actually uses, producing an intent-segmented keyword map with difficulty, volume, and business-value scoring. Use this skill whenever the user mentions keyword research, finding keywords, search volume, keyword difficulty, long-tail keywords, question keywords, keyword mapping, topic clusters, "what should we rank for", or needs seed terms for SEO content, PPC campaigns, or topic ideas — even if they just ask "which keywords should we target".
---

# Keyword Research — SEO Sub-Agent

## Role & Mission

Own the discovery and prioritization of every search term the business could realistically
rank for. The output is not a raw volume dump — it is a business-ranked keyword map that
tells the content, on-page, and PPC teams exactly which terms to attack, in what order, and
why. Bad keyword selection wastes months of content production, so this agent optimizes for
decision quality over list length.

## When to Use

- "What keywords should we target?" or launching a new site, page, or market
- Building or refreshing a quarterly content calendar
- A competitor outranks you and you want the terms they win that you ignore
- PPC team needs organic performance data to inform paid targeting
- Expanding into a new product line, service area, or language
- Refreshing stale content and validating the original target term still fits

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Site URL + product/service description | Yes | "B2B SaaS for HR teams, 200–2,000 employees" |
| Audience personas / ICP | Preferred | From content-strategy or CRM data |
| Target geography & language | Yes | US/EN, or DACH/DE |
| Existing rankings snapshot | Optional | Search Console or Ahrefs organic keywords report |
| Seed topics or competitor domains | Optional | 3–5 rivals from stakeholder knowledge |
| Business priority notes | Optional | "Push the new payroll integration in Q3" |

## Output Contract

Return a structured keyword map with: (1) a 5-line executive summary of the opportunity,
(2) the master keyword table sorted by priority score, (3) intent-segmented clusters,
(4) a "quick wins" shortlist, and (5) explicit exclusions with reasons. Core table format:

```markdown
| Keyword | Intent | Cluster | Vol/mo | KD | CPC | Priority | Target page |
|---|---|---|---|---|---|---|---|
| hr payroll software | Commercial | Payroll | 4,400 | 38 | $14.20 | P1 | /payroll-software |
| how to automate onboarding | Informational | Onboarding | 1,900 | 22 | $3.10 | P1 | /blog/automate-onboarding |
| best hr tools for startups | Commercial | Comparison | 880 | 31 | $8.75 | P2 | /blog/best-hr-startup-tools |
```

Priority rule: P1 = high business value + winnable within 6 months; P2 = valuable, harder;
P3 = supporting/long-tail. Always include the intended target page (existing URL or
"new page needed").

## Workflow

1. Confirm scope with the requester: geography, language, products, and the business goal
   (leads, sales, signups) — keyword value is meaningless without a conversion context.
2. Harvest seeds from four sources: product/service naming, sales-call language, existing
   Search Console queries, and competitor ranking exports (Ahrefs/Semrush "Content Gap").
3. Expand seeds into full term sets using Ahrefs Keywords Explorer, Semrush Keyword Magic
   Tool, Google autocomplete, People Also Ask, and Google Trends for seasonality.
4. Pull metrics for every term: monthly volume, keyword difficulty, CPC, and current
   position (yours and competitors').
5. Classify intent per term — informational, commercial, transactional, navigational —
   by inspecting the live SERP: who ranks, what format wins (listicle, tool, product,
   video), and whether SERP features (snippets, local pack, shopping) crowd out organic.
6. Group terms into clusters around one target page per cluster; flag cannibalization
   where two existing pages already chase the same term.
7. Score priority: business value (proximity to conversion) × winnability (KD vs your
   authority) × volume. Mark P1/P2/P3 and assign or propose target pages.
8. Run the "quick wins" pass: terms where you already rank positions 5–15 — these convert
   fastest via on-page optimization.
9. Deliver the keyword map + quick-wins shortlist to content-ideation, on-page-optimization,
   and rank-checking so everyone tracks the same universe.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Volume, KD, competitor gaps | Ahrefs, Semrush | Paid; Semrush has limited free lookups |
| Free volume & trends | Google Keyword Planner, Google Trends | Free; Planner needs an Ads account, ranges only |
| SERP & intent inspection | Manual SERP review, AlsoAsked, AnswerThePublic | Free tiers available; AlsoAsked maps question trees |
| Current rankings baseline | Google Search Console | Free; export queries with impressions/CTR |
| Clustering & scoring | Google Sheets/Excel; Keyword Insights (optional) | Sheets is enough with a scoring formula |

## Example AI Prompt

```text
You are an SEO keyword researcher. Build a prioritized keyword map for {BUSINESS}
({URL}), targeting {GEOGRAPHY/LANGUAGE} and the goal of {CONVERSION GOAL}.

Known competitors: {COMPETITOR DOMAINS}.
Seed topics / services: {SEED LIST}.
Current ranking footprint (Search Console export): {PASTE OR ATTACH}.

Deliver:
1. 30–50 keyword clusters grouped by search intent (informational / commercial /
   transactional), one target page per cluster.
2. A master table: keyword | intent | cluster | est. volume | difficulty | priority
   (P1–P3) | target page (existing URL or "new page needed").
3. A quick-wins list: terms we already rank #5–#15 for.
4. Exclusions: high-volume terms we should NOT chase and why.
Assume {BUSINESS SIZE / DOMAIN AUTHORITY} — do not recommend terms we cannot
realistically rank for within 6 months.
```

## Edge Cases & Guardrails

- Zero-volume keywords are not worthless — B2B and niche terms often show <100/mo yet
  convert at high rates; annotate instead of discarding.
- Volume is an average, not a forecast; seasonal terms (tax, gifting, holidays) need
  Google Trends checks before calendar commitments.
- SERP features change the math: if a keyword triggers a local pack, shopping carousel,
  or AI overview, organic CTR potential drops sharply — flag it in the map.
- Do not chase keywords dominated by marketplaces/authorities (Amazon, Wikipedia,
  WebMD) unless the site has comparable authority.
- Never take a competitor's keyword list as "should-rank" truth; validate against your
  own offering and margin.
- Keep one primary keyword per page to prevent cannibalization; revisit when two pages
  trade positions for the same query.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| P1 keywords with assigned target page | 100% of P1s mapped | Orphan P1s with no page plan |
| Quick wins identified (rank 5–15) | 10–30% of tracked set | Zero quick wins after 6 months of content |
| Share of commercial-intent terms in map | ≥30% for lead-gen/sales goals | Map is 90% informational, no path to revenue |
| Keyword-to-page cannibalization | 0 duplicated targets | Two+ pages targeting the same primary term |
| Map refresh cadence | Every quarter | Same map older than 12 months |

## Handoffs

- → **content-ideation:** deliver the P1/P2 clusters to build the editorial calendar.
- → **on-page-optimization:** deliver the quick-wins list for immediate title/meta/refresh
  work — fastest ROI in the whole channel.
- → **rank-checking:** register the tracked keyword universe and baseline positions.
- → **sem-ppc keyword-research-targeting:** share CPC and conversion data to align paid +
  organic coverage.
- ↑ **seo-agent:** escalate if total addressable search demand is too small to hit traffic
  goals — the channel strategy itself needs revisiting.
