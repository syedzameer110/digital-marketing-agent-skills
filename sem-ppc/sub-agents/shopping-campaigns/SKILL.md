---
name: sem-ppc-shopping-campaigns
description: Runs product listing ads end to end — Merchant Center feed optimization, standard Shopping vs Performance Max for Retail structure, product segmentation by margin and best-sellers, bid management, and feed diagnostics — for Google Shopping and Microsoft product ads. Use this skill whenever the user mentions Shopping campaigns, product listing ads, Merchant Center, feed errors, PLA, or e-commerce product ads.
---

# Shopping Campaigns — SEM/PPC Sub-Agent

## Role & Mission

Own product listing ads: the image + title + price auction that drives e-commerce revenue.
Unlike text search, Shopping targets through the product feed — the feed IS the keyword list —
so feed quality, campaign segmentation, and bid tiers decide profitability. This agent takes a
catalog from Merchant Center to a margin-aware Shopping/PMax structure that holds target ROAS
without starving best-sellers.

## When to Use

- An e-commerce store launches paid product ads for the first time
- Feed disapprovals, missing GTINs, or price mismatches are blocking ads
- "Shopping ROAS is below target" or PMax vs standard Shopping questions arise
- New products, categories, or seasonal collections enter the catalog
- Best-sellers lose impression share while long-tail SKUs absorb budget
- Expanding to Microsoft Merchant Center or local inventory ads

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Product catalog + margin data | Yes | SKU, price, cost, margin tier, stock |
| Merchant Center account access | Yes | Feed, diagnostics, policies |
| Store conversion values (verified tracking) | Yes | From conversion-tracking |
| Shipping/tax/return policy data | Yes | Merchant Center compliance fields |
| Competitor pricing signals | Preferred | Price competitiveness report |
| Brand vs generic product mix | Preferred | Segmentation + exclusions |

## Output Contract

Return: (1) a feed fix list, (2) a campaign + product-group structure table, (3) bid/target
tiers, (4) an exclusions plan, (5) monitoring cadence. Core structure format:

```markdown
| Campaign | Type | Product group / tier | SKUs | Target | Notes |
|---|---|---|---|---|---|
| SHOP-Cooling-BestSellers | Standard Shopping | Category: AC > best-sellers | 85 | tROAS 420% | Top 20% margin + velocity |
| SHOP-Cooling-Longtail | Standard Shopping | Category: AC > all others | 610 | tROAS 300% | Discovery tier |
| PMax-Retail-All | PMax (retail) | All products (brand-excluded) | 695 | tROAS 350% | Scale + remarketing reach |
```

Feed fix format: attribute | affected SKUs | issue | fix (e.g., title | 212 SKUs | brand
missing, keyword buried | rewrite ≤70 chars: Brand + Model + Key attribute).

## Workflow

1. Verify Merchant Center foundations: account verified and linked to Ads, shipping and tax
   configured, return policy published, and no account-level suspensions pending.
2. Audit the feed with Merchant Center diagnostics: item-level issues (missing GTIN, image
   quality, price/availability mismatch with the landing page) — disapproved SKUs earn zero
   impressions, so fix before structuring.
3. Optimize product titles: front-load brand + product + key attributes (color, size, model)
   within ~70 characters to match how shoppers search; write descriptions that carry the
   long-tail attributes titles cannot.
4. Decide the structure: standard Shopping for control (keyword negatives, per-product-group
   bids, clean query data) plus Performance Max for retail for scale (audience signals, YouTube/
   Gmail/GDN inventory) — a hybrid is the common operating model; keep brand queries excluded
   from PMax and covered by the brand search campaign.
5. Segment product groups by economics: best-sellers, high-margin, mid, long-tail discovery —
   separate groups so bids and targets reflect margin reality, not catalog averages.
6. Set tiered targets with bidding-strategy: tROAS per tier anchored to margin break-even
   (e.g., 300% discovery floor, 400%+ best-sellers); avoid one catalog-wide target that
   over-bids junk and under-bids winners.
7. Add negative keyword hygiene (standard Shopping): harvest search terms weekly and negate
   irrelevant, off-brand, and unprofitable queries; maintain brand exclusions for PMax.
8. Monitor weekly: Merchant Center diagnostics, price competitiveness vs competitors, lost
   impression share on best-sellers, out-of-stock churn, and ROAS by tier.
9. Iterate monthly: promote winning long-tail SKUs into best-seller tiers, refresh seasonal
   titles/images, and rebalance budgets between standard Shopping and PMax based on marginal
   return — document every move.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Feed management & diagnostics | Google Merchant Center (Next) | Free; item-level issue reports |
| Feed optimization at scale | Feedonomics, DataFeedWatch | Paid; rules-based transforms |
| Campaign management | Google Ads (standard Shopping, PMax retail) | Product groups + asset groups |
| Microsoft expansion | Microsoft Merchant Center + product ads | Similar flow; smaller volume |
| Search-term harvesting | Shopping search terms report + Scripts | Standard Shopping only |
| Title QA | Sheets title templates + length checks | ≤70 chars, attributes front-loaded |

## Example AI Prompt

```text
You are a Shopping campaigns specialist. Store = {STORE}; catalog size = {N SKUs};
margin spread = {TIER EXAMPLE: 55% best-sellers, 20% mid, 8% long-tail}; goal ROAS floor =
{BREAK-EVEN ROAS}; Merchant Center status = {LINKED? ISSUES?}; PMax in use = {YES/NO}.

Deliver:
1. Feed audit checklist: the top issue classes to fix (titles, GTIN, images, price parity,
   availability) with a title template rule for the catalog.
2. Structure table: campaigns (standard Shopping tiers + PMax retail) | product-group
   segmentation | SKU counts | tROAS per tier | rationale tied to margin.
3. Exclusions plan: PMax brand exclusions, starter negative keyword list for Shopping.
4. Weekly monitoring list (diagnostics, lost IS, price competitiveness) and a monthly
   tier-promotion process for winning long-tail SKUs.
Never propose a single catalog-wide ROAS target; tiers must reflect margin reality.
```

## Edge Cases & Guardrails

- Feed disapproval = zero ads for those SKUs: price or availability mismatch with the landing
  page, bad images, and missing GTINs (where required) are the usual causes — check
  diagnostics before touching bids.
- Sale prices must flow into the feed promptly; ads showing stale prices breach policy and
  destroy trust (and CVR).
- PMax reports less query-level data than standard Shopping — control what you can via brand
  exclusions, account-level negatives, and audience signals; keep a standard Shopping tier to
  preserve query intelligence.
- One ad group per catalog is the over-consolidation trap: margin-heterogeneous SKUs under one
  target subsidize junk products.
- Out-of-stock churn wastes budget history: pause or exclude sold-out SKUs quickly, and keep
  IDs stable so re-listed products retain performance history.
- Shopping CPCs run lower than search (often $0.30–$0.80) but the auction weighs feed quality
  and price competitiveness — a cheap product with a weak title still loses the impression.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Shopping CTR | 0.8–2% | <0.5% — titles/images failing |
| Shopping CVR | 1.5–3.5% | <1% sustained |
| Disapproved SKUs | <1% of catalog | >5% or account-level suspension |
| ROAS by tier | Each tier ≥ its margin-based target | One blended target masking losses |
| Lost IS (budget) on best-sellers | <20% | Best-sellers starved by long-tail |
| Feed title compliance | 100% follow template | Free-text titles, brand buried |

## Handoffs

- ← **conversion-tracking:** verified purchase values power tROAS; escalate value gaps.
- → **bidding-strategy:** tiered targets and margin data become the bidding plan.
- → **budget-management:** seasonal pushes and tier rebalancing get pre-planned budgets.
- → **negative-keyword-management:** Shopping search-term harvesting and PMax exclusions.
- ↑ **sem-ppc-agent:** escalate feed suspensions and margin-vs-target conflicts.
