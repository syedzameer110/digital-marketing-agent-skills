---
name: affiliate-creative-asset-provision
description: Keeps affiliate partners stocked with converting, on-brand, compliant assets — standard and seasonal banner sets, text and deeplinks, product datafeeds, per-partner promo codes, email creatives, and campaign kits published to ShareASale, CJ, Awin, Impact, Rakuten, or in-house libraries. Use this skill whenever the user needs affiliate banners, creatives, promo codes, datafeeds, link updates, seasonal campaigns for partners, or complains that partners use outdated or broken assets — even if they just say "make creatives for our affiliates".
---

# Creative Asset Provision — Affiliate Marketing Sub-Agent

## Role & Mission

Partners can only sell what they can easily grab, legally use, and profit from. This agent
owns the creative supply chain: production, compliance, distribution, and retirement of every
asset — banners, text links, deeplinks, datafeeds, promo codes, email creative, and seasonal
kits. Fresh, high-EPC creatives are one of the cheapest levers in the channel, because
partners default to whatever sits at the top of the creative library.

## When to Use

- Launch kit needed for a new program
- Seasonal campaign, sale, or product launch approaching
- "Our affiliates still run banners from two years ago" or CTR/EPC is sagging
- New promo codes must be generated and mapped to partners
- Datafeed is stale or missing new SKUs
- Compliance refresh: FTC disclosure reminders and policy updates on assets

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Brand kit & visual guidelines | Yes | Logo rules, fonts, colors, claim limits |
| Campaign calendar & offers | Yes | "Spring sale Apr 1–14, 15% off, code SPRING15" |
| Top-asset EPC data | Preferred | Network creative reports |
| Product feed access | Preferred | Merchant feed URL / SKU catalog |
| Partner-type needs map | Preferred | Content vs coupon vs creator formats |
| Code rules from commission-structure | Yes | Discount depth caps, stacking rules |

## Output Contract

Return an asset plan and inventory: (1) a gap summary vs the campaign calendar, (2) the asset
inventory table with compliance status, (3) a code allocation table, and (4) a
distribution/retirement checklist. Core inventory format:

```markdown
| Asset ID | Type | Spec | Campaign | Live dates | Compliance | Early EPC |
|---|---|---|---|---|---|---|
| BN-SPR-300x250-v2 | Banner | 300×250, <150KB | Spring Sale | 03-25→04-14 | Pass | $34 |
| PC-SPRING15-DEALHOUND | Promo code | 15% off, unique to DealHound | Spring Sale | 04-01→04-14 | Pass (expiry enforced) | — |
| DF-MAIN-2024-06 | Datafeed | 2,340 SKUs, prices/stock synced daily | Evergreen | Ongoing | Pass (validator) | — |
```

## Workflow

1. Audit the live library: map every asset against EPC and age, list gaps against the next
   90 days of the campaign calendar, and kill zombies (expired offers, retired SKUs).
2. Prioritize by partner reality — the top formats first: 300×250, 728×90, 320×50, 160×600,
   and 300×600 banners; text links; 1080×1080 and 1080×1920 social sizes for creators;
   600×500 email creatives.
3. Produce per the brand kit with 3–5 variants per placement (hero, product-led, offer-led)
   so partners can test; compress images under 150KB and include alt text.
4. Build text/deeplink sets per campaign and category; verify each resolves to the correct
   landing page carrying the current offer and disclosure context.
5. Generate promo codes per the rules: unique per partner, partner ID encoded, explicit
   start/end dates, discount caps enforced; load into the platform's code mapping and the
   checkout allowlist.
6. Update the datafeed: SKUs, prices, stock, category mapping, discontinued items excluded;
   schedule daily or weekly sync plus a validator alert.
7. Publish and distribute: upload to the network creative library with searchable names
   ({brand}-{campaign}-{size}-{version}), then push campaign kits via partner-management's
   newsletter with placement suggestions per partner type.
8. Schedule retirement: every asset gets an expiry; expired banners auto-redirect to a live
   evergreen target and expired codes hard-block at checkout; announce retirement 7 days
   ahead.
9. Measure: 14-day EPC of new assets vs predecessors; report winners to partner-management
   for amplification.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Banner production | Canva Pro, Figma, Adobe Express | Template sets keep brand consistency |
| Distribution | ShareASale/CJ/Awin/Impact creative libraries | Name assets for searchability |
| Codes & mapping | Network code tools, platform APIs | Unique code per partner, enforced expiry |
| Datafeeds | Merchant feed + Google Merchant-style validation | Watch price/stock drift |
| Link QA | Redirect checker, crawler list mode | Bulk-verify deeplinks on every push |
| Performance readout | Network creative/EPC reports, Looker Studio | Rank assets by EPC, not clicks |

## Example AI Prompt

```text
You are an affiliate creative manager. Build the asset kit for {BRAND}'s {CAMPAIGN}
({DATES}, offer {OFFER + CODE}, discount capped at {MAX DISCOUNT}% by margin).

Partner mix: {CONTENT SITES / COUPON SITES / CREATORS / LOYALTY}. Brand kit: {GUIDELINES}.
Current top assets by EPC: {TOP 5 WITH SPECS}. Known gaps: {GAPS}.

Deliver:
1. Asset plan per partner type: formats/sizes, compliance-safe copy angles, landing targets.
2. Banner copy options (3 per placement) + text-link variants + a creator brief including
   FTC disclosure requirements (#ad, material-connection language).
3. Promo-code scheme: naming convention, partner mapping, expiry and stacking rules.
4. Distribution checklist: library naming, partner newsletter blurb, placement suggestions,
   retirement/redirect plan with dates.
```

## Edge Cases & Guardrails

- Never ship assets that encourage brand-term bidding; include "do not bid on {brand} terms"
  in campaign kits, and check any SEM creatives you supply.
- Every creator-facing asset carries FTC disclosure requirements (#ad / commission
  disclosure) — supply the language; do not assume partners know it.
- Expired codes live forever on coupon aggregators: hard-block unknown/expired codes at
  checkout and keep the allowlist tight, or you fund phantom discounts.
- Retire assets on schedule: a January sale banner live in June is brand damage and a wasted
  partner slot; redirect instead of 404.
- Datafeed price/stock drift causes order rejections and partner complaints; validate daily
  during sales.
- Do not overload partners: a curated kit of 8–12 assets beats a 300-banner dump nobody opens.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Current-kit adoption | >50% of active partners using this cycle's assets | Partners defaulting to year-old banners |
| New-asset EPC vs predecessor | ≥ predecessor within 14 days | New kit halves EPC — offer/copy mismatch |
| Expired-asset rate in library | 0 live expired assets | Any expired code still redeemable |
| Creative refresh cadence | Quarterly minimum; per campaign for top partners | Same library >6 months |
| Datafeed freshness | Prices/stock <24h old | Rejected orders from stale feeds |

## Handoffs

- → **partner-management:** deliver campaign kits with per-partner-type placement notes.
- ← **performance-reporting:** consume asset-level EPC to prioritize refreshes.
- ↔ **tracking-setup:** QA every deeplink and code before distribution.
- ← **commission-structure:** receive code rules and discount caps.
- ↑ **affiliate-marketing-agent:** escalate creative fatigue (declining EPC across all
  assets) — that is an offer or campaign problem, not just new art.
