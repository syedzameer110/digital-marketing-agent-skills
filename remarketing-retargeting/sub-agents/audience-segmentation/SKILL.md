---
name: remarketing-audience-segmentation
description: Builds decision-grade retargeting audiences from behavioral data — site visitors by page depth and recency, cart abandoners, product viewers, past purchasers, and engagement tiers — sized, deduplicated, and mapped to the right platform (Google Ads, Meta, GA4, customer match). Use this skill whenever the user mentions retargeting audiences, custom audiences, cart abandoner lists, visitor segments, audience membership windows, or asks who we should retarget — even if they never say audience segmentation.
---

# Audience Segmentation — Remarketing & Retargeting Sub-Agent

## Role & Mission

Turn raw tracker data into decision-grade retargeting audiences: site visitors by depth and recency, cart abandoners, product viewers, past purchasers, and engagement tiers — sized, deduplicated, and mapped to the right platform. Every impression in this channel is expensive because the pool is finite, so the mission is simple: no ad impression lands on someone whose behavior did not earn that message, and no high-intent user goes unsegmented.

## When to Use

- "Set up retargeting audiences" or launching any new retargeting program
- Tags are installed but audiences are empty, tiny, or undifferentiated
- Everyone currently sees the same generic ad regardless of what they did
- Customer match lists are needed from CRM or email data
- GA4 audiences should flow into Google Ads for RLSA or Demand Gen
- Quarterly audit of membership windows, overlaps, and segment sizing

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Live pixel/tag data | Yes | Meta Pixel + CAPI, Google tag with remarketing events firing |
| GA4 property access | Yes | Audience definitions, import to Google Ads |
| Conversion definitions | Yes | What counts as purchase, qualified lead, demo booked |
| E-commerce/CRM data | Preferred | Shopify/BigCommerce orders, CRM stages for customer match |
| Email list (hashed upload) | Preferred | Customer match / custom audience from list |
| Platform ad account access | Yes | Google Ads, Meta Business Manager, LinkedIn Campaign Manager |

## Output Contract

Return an audience register: (1) a 5-line summary of the segmentation logic and pool sizes,
(2) the master audience table, (3) the exclusion list, (4) gaps and next actions. Core table
format:

```markdown
| Audience | Platform(s) | Definition (rule) | Membership | Est. size | Bid tier | Message angle |
|---|---|---|---|---|---|---|
| Cart Abandoners 7d | Meta, Google Ads | add_to_cart AND NOT purchase, last 7 days | 7 days | 3,800 | Highest (+30%) | Objection handling + incentive |
| Product Viewers 14d | Meta | view_item in 2+ sessions, no add_to_cart | 14 days | 11,200 | Medium (+15%) | Social proof |
| Purchasers 180d | Google Ads, Meta | purchase event, last 180 days | 180 days | 6,400 | Exclude from acquisition | Cross-sell / replenishment |
```

Rule: every audience carries a membership duration matched to the purchase cycle, a bid tier,
and a message angle — an audience without a message angle is a list, not a strategy.

## Workflow

1. Inventory the events actually firing (view_item, add_to_cart, begin_checkout, purchase,
   lead, demo_booked) against the conversion map; fix gaps with pixel-tag-implementation
   before building lists on broken data.
2. Define the tier ladder by intent: all visitors (30–180d) → content/page viewers →
   product/plan viewers → cart or checkout abandoners → past purchasers. Hotter tiers get
   shorter windows.
3. Match membership duration to the purchase cycle: 7 days for impulse e-comm cart abandoners,
   30–90 days for considered purchases, 180–540 days for B2B and replenishment.
4. Size each segment against platform delivery minimums (roughly 100+ for Display/YouTube,
   1,000+ for search personalization via RLSA) and flag any that will not serve.
5. Build the audiences natively: Meta custom audiences from pixel events, Google Ads audience
   segments from the Google tag, GA4 audiences for import, LinkedIn Insight Tag segments for
   B2B.
6. Upload hashed customer match lists (email/phone) from CRM or the email platform; set
   auto-refresh where the integration supports it.
7. Configure exclusions: converted users, existing customers (where acquisition-only), and
   active email subscribers for incentive ads — coordinate the event logic with burn-pixels.
8. Check overlaps between audiences (Google Ads audience insights / Meta overlap tool);
   consolidate anything sharing more than 20–30% membership to avoid double-serving and
   stacked frequency.
9. Document the register (name, rule, window, platform, owner) in a shared sheet and hand the
   tier map to retargeting-ad-creation and dynamic-retargeting.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Pixel-event audiences | Meta Events Manager, Google Ads Audience Manager, Google tag | Free with ad accounts |
| Analytics-based audiences | GA4 Audience Manager | Free; import to Google Ads for RLSA/Demand Gen |
| Tag configuration | Google Tag Manager | Free; event triggers and parameters |
| List uploads | Google Ads Customer Match, Meta custom audiences from list, LinkedIn Matched Audiences | Hashing required; 1,000+ minimum on Google |
| B2B segments | LinkedIn Insight Tag, HubSpot/CRM exports | Insight Tag free with Campaign Manager |
| Register documentation | Google Sheets / Airtable | Single source of truth, reviewed quarterly |

## Example AI Prompt

```text
You are a retargeting audience architect. Business: {BUSINESS} selling {PRODUCT/SERVICE},
platform stack: {META / GOOGLE ADS / GA4 / LINKEDIN}, average purchase cycle: {DAYS}.
Events firing today: {EVENT LIST}. Email list size: {N}. CRM stages: {STAGES}.

Deliver:
1. A tiered audience ladder (intent tiers from cold-visitor to past-purchaser) with the exact
   rule, membership window, and platform for each list.
2. A register table: audience | platform | rule | membership | expected size | bid tier |
   message angle.
3. Exclusions: converted users, existing customers, any suppressed groups — with the mechanism
   for each platform.
4. Sizing warnings for any segment below delivery minimums (1,000 for search personalization).
5. The two segments you would launch first and why.
Constraints: {SENSITIVE CATEGORY / PRIVACY NOTES} — flag any segment that platform policy
prohibits building from these behaviors.
```

## Edge Cases & Guardrails

- Small catalogs and low-traffic sites may never reach search-personalization minimums
  (1,000 users) — build for social/display delivery instead and note RLSA as a later unlock.
- Membership windows that outlive intent (180-day "cart abandoners") put stale users in hot
  tiers — windows must match the purchase cycle, not platform defaults.
- Never build audiences from sensitive pages (health conditions, financial status, sexual
  orientation, religion) — Google and Meta both prohibit it, and the risk is account-level.
- iOS ATT means Meta pixel audiences skew Android/desktop; expect 20–40% smaller iOS pools and
  rely on CAPI and first-party data to backfill.
- Customer match uploads must be hashed and sourced from opted-in data only; never upload
  scraped or purchased lists.
- Overlapping audiences silently double-charge and inflate frequency — audit overlaps before
  blaming creative for fatigue.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Visitor capture rate | >90% of site visitors land in at least one audience | Major traffic missing from all lists |
| Cart-abandoner CVR lift | 2–5x the all-visitors segment | Hot tier converts same as cold visitors |
| Customer match rate | 40–70% of uploaded list matched | <30% (data quality or hashing problem) |
| Audience overlap | <20–30% between funded segments | Same users in 3+ live campaigns |
| Register freshness | Reviewed every quarter | Windows/rules unchanged for 12+ months |

## Handoffs

- ← **pixel-tag-implementation:** receive verified events; escalate missing or mislabeled
  events immediately.
- → **retargeting-ad-creation:** deliver the register with message angles so creative maps to
  mindset.
- → **dynamic-retargeting:** deliver viewer and cart segments for product-set pairing.
- → **frequency-management:** deliver the tier map so caps scale with intent.
- ↑ **remarketing-retargeting-agent:** escalate if pools are too small to sustain the channel
  plan.
