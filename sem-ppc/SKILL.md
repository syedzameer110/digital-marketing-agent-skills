---
name: sem-ppc-agent
description: Manages and optimizes paid search end to end across Google Ads, Microsoft/Bing Ads, Shopping, and Performance Max — keyword targeting, campaign structure, ad copy, bidding, Quality Score, negative keywords, budgets, conversion tracking, and shopping feeds. Use this skill whenever the user mentions PPC, paid search, Google Ads, Bing, ad spend, CPC, ROAS, Quality Score, shopping ads, or wants more leads or lower CPA from ads — even if they never say PPC.
---

# SEM / PPC (Paid Search) — Main Agent (Command Hub)

## Channel Overview

Paid search buys intent: your ad appears the moment someone searches for a solution you sell,
which makes SEM/PPC the fastest, most measurable customer-acquisition channel in the mix. A
well-built account can produce its first conversions within days and reach optimization maturity
in 60–90 days — a contrast to the 3–6 month ramp of SEO. The trade-off is that traffic stops the
moment spend stops: every click is rented, so channel economics live or die on conversion rate,
average order value or lead quality, and the efficiency of the auction (Quality Score).

This channel wins when demand already exists in the search results, the unit economics support
the click price (search CPCs typically run $1–$3 in mainstream verticals, $5–$8+ in legal,
insurance, and finance), and you can act on conversion data weekly. It underperforms for
categories with no search demand, low margins that cannot absorb auction prices, or pure
awareness goals — route those to display, social, or content channels. Costs are media-heavy:
typical managed programs run $2,000–$50,000+/month in ad spend plus 10–20% in tooling and labor.
Google Ads is the primary auction; Microsoft Advertising (Bing) adds incremental, usually
cheaper volume (CPCs commonly 20–35% below Google) on a near-identical workflow.

The operating loop this hub enforces is: measure correctly → target the right queries →
structure for control → write for the click → land on a converting page → bid to the economics
→ cut waste → test relentlessly. Skipping any link breaks the chain: smart bidding on broken
tracking, great ads on a weak landing page, and cheap clicks on irrelevant searches all produce
the same symptom — spend that never becomes revenue.

## Agent Hierarchy

```text
sem-ppc-agent (command hub)
└── sub-agents/
    ├── keyword-research-targeting/    → pick the searches worth bidding on
    ├── campaign-structure/           → account architecture: campaigns, ad groups, segmentation
    ├── ad-copywriting/               → responsive search ads that win CTR
    ├── landing-page-creation/        → conversion-dedicated pages for paid traffic
    ├── bidding-strategy/             → manual, Maximize, tCPA, tROAS selection & tuning
    ├── negative-keyword-management/  → cut irrelevant searches and wasted spend
    ├── ad-extensions/                → sitelinks, callouts, snippets, calls, promos
    ├── quality-score-optimization/   → expected CTR, ad relevance, LP experience
    ├── ab-testing/                   → statistically sound ad & landing page tests
    ├── budget-management/            → allocation, pacing, budget-limited diagnosis
    ├── conversion-tracking/          → tags, GA4, enhanced conversions, offline imports
    └── shopping-campaigns/           → Merchant Center feeds & product listing ads
```

## Sub-Agent Routing Table

| Sub-agent | Call when… | Key inputs | Depends on |
|---|---|---|---|
| keyword-research-targeting | New account, new market, CPC inflation, or quarterly refresh of bid terms | Offer, geography, target CPA, competitor domains | None (entry point) |
| campaign-structure | Building or rebuilding the account; budget control or reporting is muddled | Keyword plan, product lines, budget envelope | keyword-research-targeting |
| ad-copywriting | New ad groups, CTR below 3%, ad strength "Poor/Average", new offers | Ad group themes, USPs, brand voice, LP URLs | campaign-structure |
| landing-page-creation | Paid traffic lands on homepage, CVR below 2–5%, new offer needs a page | Offer details, audience, form/CRM mapping | ad-copywriting (for message match) |
| bidding-strategy | Launch, 30+ conversions/month available, targets missed, spend volatility | Conversion volume, historical CPA/ROAS, margins | conversion-tracking |
| negative-keyword-management | Weekly search-terms hygiene, broad match expansion, wasted spend >10% | Search terms report, intent tiers, shared lists | keyword-research-targeting |
| ad-extensions | Asset coverage gaps, low CTR vs competitors, promotions, call-driven businesses | Site sections, USPs, phone, GBP, promo calendar | campaign-structure |
| quality-score-optimization | Average QS below 7, CPCs climbing, many QS 3–5 keywords | Keyword QS report, ads, LP mapping | ad-copywriting, landing-page-creation |
| ab-testing | Stable volume, ad or LP variants to compare, before/after big changes | Baseline metrics, test candidates, MDE | ad-copywriting or landing-page-creation |
| budget-management | Monthly planning, budget-limited winners, overspend, seasonal peaks | Total budget, campaign performance, lost IS data | bidding-strategy, campaign-structure |
| conversion-tracking | New account, GA4 migration, smart bidding prep, tracking discrepancies | Site access, GTM, GA4, CRM, conversion definitions | None (entry point) |
| shopping-campaigns | E-commerce launches, feed disapprovals, Shopping/PMax decisions | Product catalog, Merchant Center, margins | conversion-tracking (values) |

## End-to-End Workflows

### Workflow A — New Account Launch (weeks 1–6)

1. Run **conversion-tracking** first: define the conversion taxonomy (lead, qualified lead,
   sale, calls), implement tags via Google Tag Manager, enable enhanced conversions, and verify
   with test conversions. Output: a trusted measurement foundation — never bid on unverified data.
2. Run **keyword-research-targeting**: build the bid-ready keyword plan with intent tiers,
   match types, and CPC forecasts. Output: prioritized keyword universe with spend forecast.
3. Run **campaign-structure**: convert the keyword plan into campaigns and themed ad groups
   (brand vs non-brand separated), with naming conventions and shared negative lists. Output:
   build-ready blueprint.
4. Run **ad-copywriting** and **ad-extensions** in parallel: RSAs per ad group (15 headlines,
   4 descriptions) plus the full asset library (sitelinks, callouts, snippets, calls). Output:
   launch-ready ads with maximum SERP footprint.
5. Run **landing-page-creation** for the top 2–3 campaigns: message-matched, single-CTA pages.
   Output: dedicated LPs wired to tracking.
6. Run **bidding-strategy** and **budget-management**: start on Maximize Clicks with CPC caps or
   Maximize Conversions (if ≥30 conv/month of history), set budgets at monthly ÷ 30.4 daily pace
   with a 10% test reserve. Output: launch bid + budget plan.
7. From week 2 onward, loop **negative-keyword-management** (weekly search-terms review),
   **ab-testing** (first ad/LP test), and **quality-score-optimization** (first QS audit at day 30).

### Workflow B — Performance Turnaround ("we're paying too much per lead")

1. Audit **conversion-tracking**: rule out double counting, missing values, or spam leads —
   misleading data is the most common cause of "bad" performance. Output: verified data verdict.
2. Run **negative-keyword-management** on 90 days of search terms; strip waste to <10% of clicks.
   Output: negative additions + shared list updates.
3. Run **quality-score-optimization** on the spend-weighted worst keywords; restructure, rewrite
   ads, and align LPs. Output: QS fix plan targeting average 7+.
4. Run **bidding-strategy**: re-anchor tCPA/tROAS to historically achievable levels, or step
   smart bidding down where data is thin. Output: revised bid plan.
5. Run **budget-management**: reallocate from high-CPA themes to proven winners in 10–20% steps;
   document expected CPA/ROAS per move. Output: reallocation memo.
6. Launch **ab-testing** on the two highest-spend ad groups to compound the gains; review in 30
   days against the turnaround baseline.

### Workflow C — E-commerce Shopping Scale-Up (recurring monthly)

1. Run **shopping-campaigns**: Merchant Center feed audit (titles, GTINs, availability, price
   parity), disapproval cleanup, then structure/refresh the standard Shopping + Performance Max
   split by margin tier. Output: feed fixes + product-group plan.
2. Feed product performance into **bidding-strategy** for tiered tROAS by margin band.
3. Run **budget-management** to shift spend toward high-mover, high-margin tiers; check lost
   impression share (budget) on best-sellers. Output: revised allocation.
4. Harvest standard Shopping search terms into **negative-keyword-management**; apply brand
   exclusions in PMax. Output: clean traffic mix.
5. Run **ab-testing** on product landing pages and **quality-score-optimization** where Google
   shows low LP experience. Close the month with allocation and ROAS review.

## KPI Dashboard

North-star metric: **revenue or qualified pipeline per dollar of ad spend** — ROAS for
e-commerce (mature target 3–5x, margin-dependent), cost per qualified lead for lead-gen.

| Metric | Source tool | Cadence | Healthy range |
|---|---|---|---|
| Search CTR (non-brand) | Google Ads / Microsoft Ads | Weekly | 3–6%; branded 10%+ |
| Search CVR | Google Ads / GA4 | Weekly | 2–5% e-comm; 5–10% lead-gen |
| Shopping CTR / CVR | Google Ads | Weekly | CTR 0.8–2%; CVR 1.5–3.5% |
| Average CPC | Google Ads / Microsoft Ads | Weekly | $1–$3 typical; $5–$8+ legal/finance |
| Quality Score (avg, non-brand) | Google Ads (keyword column) | Monthly | 7+; red flag below 5 |
| Impression share (non-brand search) | Google Ads | Weekly | 40–60% non-brand; 85%+ brand |
| Lost IS (budget) on priority campaigns | Google Ads | Weekly | <20% |
| Wasted spend on irrelevant search terms | Search terms report | Weekly | <10% of clicks |
| ROAS (e-comm) / CPA vs target (lead-gen) | Google Ads + GA4 | Weekly | ROAS 3–5x; CPA within ±15% of target |
| GA4 ↔ Ads conversion discrepancy | GA4 vs Google Ads | Monthly | <10% |
| Ad strength (Good/Excellent share) | Google Ads | Monthly | ≥80% of ad groups |
| LP conversion rate (dedicated pages) | GA4 / platform | Monthly | 5–10% lead-gen; 2–4% e-comm |
| Test velocity (concluded tests) | Test log | Quarterly | 2–6 verdicts per quarter |
| Microsoft Ads share of spend | Both platforms | Monthly | 10–15% where enabled |

## Budget Guidance

| Monthly ad spend | Recommended allocation |
|---|---|
| $1,000–$2,500 | 70% proven brand + high-intent exact/phrase search, 20% Shopping (if e-comm), 10% testing; skip broad match until negatives mature |
| $2,500–$10,000 | 50% non-brand search (best themes), 25% brand defense, 20% Shopping/PMax, 5–10% test budget; add Microsoft Ads mirror at 10–15% of Google spend |
| $10,000–$50,000 | 40% non-brand search, 20% brand, 30% Shopping/PMax by margin tier, 10% new-keyword/broad-match incubator with strict negatives |
| $50,000+ | Dedicated budgets per product line/geo; 10% always-on experimentation; portfolio bid strategies; full Shopping + PMax + Microsoft + YouTube demand capture |

Allocation principles:

- Brand search is cheap and high-converting — but don't let it flatter blended ROAS; judge
  non-brand on its own economics.
- Hold a 5–10% test reserve every month; accounts that stop testing decay within a quarter.
- Reallocate by marginal return, not average: a campaign at 4x ROAS with only 10% budget-limited
  impression share often returns less than a 2.5x campaign with headroom.
- Smart bidding needs fuel: keep ≥30 conversions per campaign per month or consolidate before
  switching strategies.
- Cover brand defense explicitly — a small, ring-fenced brand budget prevents rivals and
  resellers from buying your highest-intent traffic.
- Match the envelope to the goal honestly: if target CPA × realistic volume exceeds budget,
  escalate scope before launching rather than under-funding every campaign at once.
- Rebalance between Google and Microsoft only on converted-value parity, not on CPC arithmetic —
  cheaper clicks on worse-converting traffic is not a saving.

## Team & Agency Mapping

| Activity | Best handled by | Rationale |
|---|---|---|
| Strategy, budgets, stakeholder reporting | In-house (or fractional lead) | Needs business context, margin data, and fast decisions |
| Keyword research & account structure | Agency or senior in-house | Specialist craft; errors compound across the whole account |
| Ad copywriting | In-house with brand voice | Differentiators and offers live with the business |
| Landing pages | Freelancer/agency build + in-house approval | Page speed and CRO skill matter more than platform access |
| Bidding & budget ops | In-house (automated + weekly review) | Daily-ish judgment calls; agency turnaround is too slow |
| Shopping feeds & Merchant Center | Specialist (agency or freelancer) | Feed rules and diagnostics are a technical niche |
| Conversion tracking | Dev + analytics specialist | Touches GTM, GA4, CRM, and legal consent |
| Microsoft Advertising mirror | Agency or in-house (part-time) | Low-effort import of the Google structure; verify quarterly |

## Reporting Cadence

- **Weekly (in-house, 30–45 min):** spend pacing (±10%), search-terms waste, budget-limited
  campaigns, CPA/ROAS vs target, disapprovals. Decisions: negatives, budget nudges, pause calls.
- **Monthly (stakeholders, 1 hr):** full KPI dashboard, quality score trend, test results,
  reallocation plan, next-month forecast. Decisions: budget shifts, bid target changes, creative
  refreshes.
- **Quarterly (leadership):** channel ROI vs SEO/other channels, account structure audit,
  platform mix (Google vs Microsoft vs PMax), annualized CPA/ROAS trend, headcount or agency
  scope review.
- **Event-driven (same day):** budget pauses, feed suspensions, policy strikes, tracking
  failures, or auction shocks (competitor blowouts) — escalate outside the normal cadence.

## Cross-Channel Integrations

- **↔ seo-agent:** share search-terms waste and CPC data — expensive paid queries are prime
  organic targets, while top-ranking organic pages become high-Quality-Score paid landing pages.
  Coordinate brand: paid defends brand SERPs while SEO builds the organic moat.
- **→ remarketing-retargeting-agent:** export site-visitor, cart-abandoner, and converter
  audience lists (via GA4/Ads tags) for RLSA bid adjustments and remarketing campaigns.
- **→ web-analytics-agent:** hand off the conversion taxonomy, GA4 event configuration, and
  attribution decisions; receive funnel and cross-channel attribution readouts in return.
- **→ cro-agent:** paid traffic is the fastest legitimate test-lab — route LP variants and
  conversion data to cro-agent; adopt validated winning pages account-wide.
- **→ display-advertising-agent:** winning paid-search headlines and offer angles transfer to
  display creative; search audience signals (in-market, custom intent) seed display prospecting.
- **← remarketing-retargeting-agent:** remarketing performance on former site visitors informs
  RLSA bid adjustments and which search themes deserve warm-audience bids.
