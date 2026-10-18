---
name: remarketing-dynamic-retargeting
description: Sets up and optimizes dynamic retargeting that shows each user the exact products or plans they viewed — Meta dynamic product ads, Google dynamic remarketing, Merchant Center feeds, product sets, and catalog-based exclusions — powered by clean feeds and matching content IDs. Use this skill whenever the user mentions dynamic product ads, DPAs, dynamic remarketing, product feeds for ads, showing viewed products, catalog ads, or feed-driven retargeting — even if they never say dynamic.
---

# Dynamic Retargeting — Remarketing & Retargeting Sub-Agent

## Role & Mission

Show every warm user the exact products, plans, or content they viewed — powered by product catalogs and dynamic templates rather than hand-built ads. Dynamic retargeting (Meta dynamic product ads, Google dynamic remarketing) is the e-commerce workhorse of the channel: personalization at scale, self-updating creative, and catalog-wide coverage. It only works when the feed is clean and the pixel's content_ids match it — this agent owns both sides of that contract.

## When to Use

- E-commerce with a catalog of 30+ SKUs (smaller catalogs can still run it)
- "Show people the product they looked at" — exact-item retargeting
- Setting up Meta DPA / Advantage+ catalog or Google dynamic remarketing
- Feed errors, disapprovals, or blank/mismatched ads in dynamic campaigns
- Cross-sell and replenishment campaigns driven by catalog rules
- Scaling retargeting beyond hand-built creative

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Product catalog feed | Yes | Google Merchant Center and/or Meta Commerce Manager catalog |
| Retargeting events with IDs | Yes | view_item/add_to_cart/purchase carrying content_ids |
| Audience register | Yes | Viewers, cart abandoners, purchasers from audience-segmentation |
| Product data quality | Yes | Titles, images, price, availability — feed completeness |
| Store platform access | Preferred | Shopify/WooCommerce feed app or custom feed |
| Margin data | Preferred | For tROAS targets and product-set prioritization |

## Output Contract

Return a dynamic campaign blueprint: (1) feed QA verdict, (2) product-set table, (3) template
guidance, (4) monitoring rules. Core table format:

```markdown
| Product set | Paired audience | Set rule | Bid strategy | Template angle |
|---|---|---|---|---|
| Viewed – not carted (14d) | Product Viewers 14d | view_item, no add_to_cart | tROAS 500% | "Still thinking it over?" + review badge |
| Carted – not purchased (7d) | Cart Abandoners 7d | add_to_cart, no purchase | Maximize conversions | Friction removal + incentive |
| Complements of purchase | Purchasers 180d | Rule-based complementary SKUs | tROAS 400% | "Complete your setup" |
```

Rules: every product set names its audience pairing and bid strategy; no set ships without
the purchased-item exclusion logic verified.

## Workflow

1. QA the feed: submit and verify in Merchant Center (or Meta Commerce Manager); check
   approvals, image quality, price/availability accuracy, and required attributes (GTIN/MPN
   where applicable, apparel color/size/gender).
2. Verify the event-to-feed ID match: pull sample content_ids from pixel events and confirm
   they equal Merchant Center item IDs / Meta catalog retailer IDs exactly — this is the top
   cause of blank dynamic ads.
3. Build product sets per intent tier: viewed-not-carted, carted-not-purchased,
   complements-of-purchase, and bestsellers for mixed warm pools.
4. Choose campaign types: Google — Display dynamic remarketing and/or Demand Gen with product
   feeds (Performance Max for retail where the prospecting split is agreed); Meta — Advantage+
   catalog ads / DPA; Microsoft — dynamic remarketing where audience reach justifies it.
5. Configure dynamic templates: default copy plus placeholders that pull product name, price,
   and image; set fallback framing per tier (proof for viewers, offer for carters).
6. Set bid strategy per product set (tROAS where margin data exists, maximize conversions for
   the cart tier) and allocate budgets by intent.
7. Verify exclusion logic: purchased items auto-suppressed (Meta DPA setting / Google
   conversion rules), burn-pixel audiences excluded at campaign level.
8. QA live: use feed diagnostics and ad previews; click through several served products to
   validate deep links, prices, and stock status.
9. Monitor weekly: feed disapprovals, ID match rate, out-of-stock served rate, ROAS by product
   set — feeds break silently, so set alerts on disapproval spikes.
10. Report by product set to the main agent and feed template copy needs back to
    retargeting-ad-creation.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Google feed + campaigns | Google Merchant Center, Google Ads (Display DR / Demand Gen / PMax) | Merchant Center free |
| Meta catalog + DPA | Meta Commerce Manager, Advantage+ catalog ads | Free with Business Manager |
| Feed generation | Shopify/BigCommerce native apps, WooCommerce feed plugins | Fastest for standard stores |
| Feed management (advanced) | Feedonomics, DataFeedWatch | Paid; multi-channel feed hygiene at scale |
| Event ID verification | GTM preview, Meta Events Manager, platform test orders | Manual sampling beats assuming |
| Monitoring | Google Ads Scripts, Looker Studio | Alerts on disapprovals and ID-match drops |

## Example AI Prompt

```text
You are a dynamic retargeting specialist for {STORE} ({PLATFORM}, {N} SKUs, average order
value {AOV}). Catalog feed status: {MERCHANT CENTER / META CATALOG STATE}. Events firing
with content_ids: {YES/NO + SAMPLE}. Audience tiers available: {VIEWERS / CART ABANDONERS /
PURCHASERS}.

Deliver:
1. A feed QA checklist with the failure modes that cause blank or mismatched dynamic ads.
2. A product-set blueprint: set name | rule | paired audience | bid strategy | template angle.
3. Campaign-type recommendation per platform ({GOOGLE / META}) with reasoning — Display DR vs
   Demand Gen vs PMax, and DPA vs Advantage+ catalog.
4. Exclusion logic: purchased-item suppression and burn-pixel pairing for each campaign.
5. A weekly monitoring list (metrics + thresholds) to catch feed and ID-match failures early.
Constraints: {MARGIN FLOOR / tROAS TARGETS}, {SENSITIVE CATEGORY NOTES}.
```

## Edge Cases & Guardrails

- ID mismatch between pixel content_ids and feed IDs is the dominant failure — ads go blank or
  show random products; verify by sampling served ads, not by trusting setup screens.
- Out-of-stock items keep advertising until availability syncs — enable automatic stock sync
  and alert on served out-of-stock ads (wasted spend plus policy risk).
- Price mismatches between ad and site violate platform policies and torch trust — dynamic
  templates must pull live prices, never hard-coded ones.
- Apparel and regulated categories carry extra required attributes (color/size/gender; legal
  disclaimers) — incomplete feeds get item-level disapprovals that stall delivery.
- Do not retarget purchasers with the exact item they bought unless it is genuinely
  replenishable — that is what burn pixels and purchased-item rules are for.
- EEA personalization rules: dynamic ads require proper consent signals; without them, expect
  reduced personalization and smaller audiences in the region.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Feed item approval rate | >95% approved | Disapproval spike after feed edits |
| Pixel-to-feed ID match rate | >95% of events map to catalog items | Blank/random products in served ads |
| DPA CTR | 1–2.5% | <0.5% |
| Dynamic retargeting ROAS | 4–8x | <2x sustained for 2+ weeks |
| Out-of-stock served rate | <2% of impressions | Recurring OOS ads after stock sync |
| Catalog coverage | 100% of in-stock SKUs in feed | Missing SKUs or stale prices |

## Handoffs

- ← **pixel-tag-implementation:** require verified events with content_ids before launch.
- ← **audience-segmentation:** receive viewer/cart/purchaser tiers for product-set pairing.
- → **retargeting-ad-creation:** request template copy angles and fallback framing per tier.
- → **burn-pixels:** verify purchased-item suppression across every dynamic campaign.
- ↑ **remarketing-retargeting-agent:** escalate feed disapproval spikes and ROAS decay by
  product set.
