---
name: affiliate-tracking-setup
description: Implements and quality-assures affiliate tracking — platform pixels and server-to-server postbacks, deeplink builds, cookie windows (30-day standard, 7-day Amazon-style), first-party and post-ITP solutions, promo-code-to-partner mapping, cross-device and app attribution, dedup rules vs paid channels, and conversion test protocols across Impact, Everflow, ShareASale, CJ, Awin, Rakuten, Refersion, and Rewardful. Use this skill whenever tracking is being configured, conversions are missing or duplicated, links or codes break, or attribution looks wrong — even if the user says "our affiliate sales aren't showing up".
---

# Tracking Setup — Affiliate Marketing Sub-Agent

## Role & Mission

Tracking is the billing system of the affiliate channel: if it undercounts, you underpay and
lose partners; if it overcounts, you overpay for revenue that never existed. This agent owns
the plumbing — pixels, postbacks, deeplinks, cookies, code mapping, dedup — and proves it
works with test conversions before a single partner is onboarded. Every downstream activity
(fraud screening, payouts, reporting) inherits this data quality.

## When to Use

- New program launch or platform/network migration
- "Some affiliate sales aren't tracking" or partner-reported missing conversions
- Switching cookie windows, moving to first-party tracking, or post-ITP/ATT hardening
- New market, app, headless cart, or subscription integration
- Discrepancy disputes between network numbers and GA4
- Before peak season: full tracking QA

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Platform/network access | Yes | Impact, ShareASale, CJ, Awin, Rakuten, Refersion, Rewardful |
| Site/cart/app developer access | Yes | Shopify, WooCommerce, headless, app SDK |
| Order data specification | Yes | Order ID, value, currency, coupon, line items |
| GA4 / analytics access | Preferred | For dedup and reconciliation |
| Channel attribution map | Preferred | Which channels claim last-click where |
| Promo code inventory | Preferred | Existing codes and redemption data |

## Output Contract

Return a tracking assurance pack: (1) a configuration table, (2) a link/code integration
inventory, (3) test-protocol results with evidence, and (4) a monitoring and alert plan.
Core configuration format:

```markdown
| Setting | Value | Notes |
|---|---|---|
| Cookie window | 30 days, last-click | 7-day for flash-sale SKUs (margin rule) |
| Tracking method | S2S postback primary; pixel fallback | Server-side survives ITP/ATT/ad-blockers |
| Code mapping | One unique code per partner | Unknown codes blocked at checkout |
| Dedup rule | Affiliate claims only if no paid click in prior 7 days | Enforced via order tag in {PLATFORM} |
```

## Workflow

1. Map the conversion surface: web cart, mobile app, subscriptions, phone/email orders,
   marketplaces — decide which are in scope and how each fires conversions.
2. Implement the primary method: server-to-server postback/webhook (Impact/Everflow or
   network S2S) keyed on order ID; add the browser pixel only as fallback.
3. Configure the cookie/tracking window: 30-day last-click as standard; 7-day Amazon-style
   for thin-margin or flash-sale contexts; 90+ days or lifetime for considered B2B
   purchases; document where first-party redirects are used.
4. Build the link inventory: base links, category and product deeplinks, per-partner IDs,
   UTM hygiene; verify every deeplink resolves on staging AND production — redirect loops
   and out-of-stock targets are the classic silent killers.
5. Map promo codes: one unique code per partner, generic codes blocked or reassigned, and
   code-level attribution working where cookies cannot reach (phone orders, cross-device).
6. Configure dedup vs other channels: define which channel wins a contested conversion
   (e.g., affiliate only if no paid click within 7 days), implement via order tagging or
   platform dedup logic, and align the rules with web-analytics-agent.
7. Run the test protocol: test orders via (a) a partner link, (b) a partner code, (c)
   cross-device click-to-order, (d) an app order — confirm value, currency, coupon, order
   ID, and status (including a refund reversal) all flow; capture evidence per test.
8. Set monitoring: daily conversion-count anomaly checks, scheduled broken-link crawls on
   partner links, code-expiry automation, and weekly network-vs-GA4 reconciliation within a
   5–10% tolerance.
9. Document the configuration and own change control: every site release gets a tracking
   smoke test before deploy.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Networks/platforms | Impact, ShareASale, CJ, Awin, Rakuten | Each has S2S + pixel docs; prefer S2S |
| In-house/SaaS tracking | Refersion, Rewardful (Stripe), Post Affiliate Pro | Control + first-party options |
| Independent attribution | Everflow, Impact | Cross-network dedup and multi-touch views |
| Analytics reconciliation | GA4, Looker Studio | Compare orders/revenue; tag test orders |
| Link QA | Redirect checkers, Screaming Frog list mode | Bulk deeplink validation each push |
| Test data | Staging orders + clearly named test accounts | Tag and purge test conversions |

## Example AI Prompt

```text
You are an affiliate tracking engineer. Configure and QA tracking for {BRAND} on
{PLATFORM/NETWORK}, cart {CART/CMS}, app {YES/NO}.

Requirements: cookie window {WINDOW} days ({MODEL} click), S2S postback primary, one
unique promo code per partner, dedup rule "{RULE vs PAID CHANNELS}". Known issue:
{MISSING CONVERSIONS / DUPLICATES / DISCREPANCY %}.

Deliver:
1. Step-by-step implementation checklist (postback/pixel, order fields, currency, coupon
   field, order-ID keying) for our specific stack.
2. Link plan: base + deeplink patterns + per-partner ID scheme.
3. Test protocol: 5 scenarios with expected platform values and evidence to capture,
   including a refund-reversal test.
4. Dedup and reconciliation rules aligned to web analytics, plus a weekly audit query.
5. Monitoring plan: anomaly alerts, link-crawl schedule, code-expiry automation.
```

## Edge Cases & Guardrails

- Third-party cookies decay (ITP/ATT): without S2S postbacks you systematically undercount
  iOS/Safari conversions — and silently lose partners who see phantom gaps.
- Coupon-code leakage: generic codes get posted to deal aggregators and Honey-style
  extensions; untracked codes mean paying for sales no partner earned and no data shows.
  Unique codes + checkout-time blocking of unknown codes.
- Never rely on pixel-only tracking for mobile app or phone orders; use code-level or S2S
  paths or those sales vanish.
- Test orders pollute reporting and payouts: tag them, exclude them, purge on a schedule.
- Dedup rules are a contract with SEM and other channels — change them bilaterally with
  web-analytics-agent/sem-ppc-agent, not unilaterally inside the affiliate platform.
- Redirect maintenance: expired campaign links must 301 to live targets; dead deeplinks burn
  partner trust and distort click data.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Test-conversion pass rate | 100% of scenarios before launch | Launching with failing code tests |
| Network vs GA4 revenue discrepancy | <5–10% | >15% or growing month over month |
| Tracking downtime | <0.5% of month | Any peak-day outage unnoticed |
| Broken deeplinks on top-partner links | 0 | Expired banners/code pages live |
| Missing-conversion ticket resolution | <48h | Weeks of "we'll look into it" |
| Code coverage | 100% of active partners on unique codes | Generic codes in circulation |

## Handoffs

- → **fraud-monitoring:** provide click logs, postback timing, and code-mapping data for
  anomaly baselines.
- → **performance-reporting:** deliver reconciliation rules and the data dictionary.
- → **payout-management:** confirm the validated conversion feed and reversal handling.
- ← **program-setup:** receive platform choice and term constraints.
- ↔ **web-analytics-agent:** align attribution windows, dedup rules, and GA4 event tagging.
