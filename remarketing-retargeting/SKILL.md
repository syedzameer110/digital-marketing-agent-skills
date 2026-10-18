---
name: remarketing-retargeting-agent
description: Orchestrates the full remarketing and retargeting program — behavioral audience segmentation, pixel and Conversions API tag implementation, segment-specific ad messaging, dynamic product ads, frequency capping, burn-pixel conversion exclusion, and cross-device tracking. Use this skill whenever the user mentions retargeting, remarketing, cart abandonment ads, dynamic product ads, RLSA, customer match, pixel audiences, ad frequency caps, or re-engaging site visitors with paid ads — even if they never say "remarketing" explicitly.
---

# Remarketing & Retargeting — Main Agent (Command Hub)

## Channel Overview

Remarketing (retargeting) is the highest-intent paid channel in the mix: instead of renting cold attention, it re-engages people who already visited the site, browsed products, or filled a cart and stopped. Because that audience has already raised a hand, retargeting typically delivers 2–3x the ROAS of prospecting campaigns — mature programs reach 4–8x — at conversion rates 2–5x cold traffic. It is also the cheapest place to be persuasive: a warm user already knows the brand, so ads can spend their limited characters on objections, proof, and offers instead of introductions. The discipline is precision, not volume — the audience pool is finite, CPMs run above prospecting rates, and the job is the right message, the right frequency cap, and airtight exclusion of converted users. Time-to-results is the fastest in paid media: audiences form within days and meaningful performance reads land in 2–4 weeks.

The structural risk is privacy, not price. Apple's App Tracking Transparency sharply reduced Meta's visibility into iOS users, third-party cookies are being phased out, and EEA traffic requires Google Consent Mode v2 (mandatory since March 2024). Winning programs respond by owning first-party infrastructure: Meta Conversions API and server-side tagging, customer match lists from CRM and email, GA4 audience imports, and logged-in identity for cross-device continuity. Typical cost profile: retargeting CPMs of $2–$10 on social and display, RLSA click prices that track search, and a budget slice of 10–30% of total paid spend. Launch order matters more than budget: tags first, then audiences, then exclusions, then creative — every shortcut in that sequence is repaid in wasted spend. Underperformers treat retargeting as a set-and-forget annuity; without exclusion hygiene, frequency caps, and creative rotation, CPMs inflate and ROAS decays within a quarter.

## Agent Hierarchy

```text
remarketing-retargeting-agent (command hub)
└── sub-agents/
    ├── pixel-tag-implementation/    → Meta Pixel + CAPI, Google tag, GTM, Consent Mode v2
    ├── audience-segmentation/       → behavioral lists: visitors, cart abandoners, purchasers
    ├── retargeting-ad-creation/     → segment-tailored messaging and offers
    ├── dynamic-retargeting/          → catalog-driven ads showing exact viewed products
    ├── frequency-management/         → caps, fatigue detection, creative rotation
    ├── burn-pixels/                  → exclude converted users, stop wasted spend
    └── cross-device-tracking/        → identity across mobile, desktop, tablet
```

## Sub-Agent Routing Table

| Sub-agent | Call when… | Key inputs | Depends on |
|---|---|---|---|
| pixel-tag-implementation | Launching retargeting, relaunching a site, empty audiences, consent compliance, or suspected signal loss | Site/CMS + GTM access, ad account IDs, event map, CMP details | None (entry point) |
| audience-segmentation | Tags are live and lists are needed; everyone sees the same ad; segments too small to deliver | Pixel/event data, GA4, CRM and email lists, conversion definitions | pixel-tag-implementation |
| retargeting-ad-creation | Segments exist and need messaging; CTR declining; new offer or seasonal push | Segment definitions, brand voice, promo calendar, objection notes | audience-segmentation |
| dynamic-retargeting | E-commerce catalog; show the exact product viewed; feed-driven scale | Merchant Center/Meta catalog, event content_ids, product data quality | audience-segmentation, pixel-tag-implementation |
| burn-pixels | Ads keep chasing purchasers; lead-gen needs demo-booked suppression; budget leaks to existing customers | Conversion events, thank-you page URLs, CRM status | pixel-tag-implementation |
| frequency-management | Campaigns are live; frequency climbing; CTR decaying; "your ads follow me" complaints | Frequency reports, campaign structure, creative inventory | All live-campaign agents (parallel-safe once live) |
| cross-device-tracking | Users browse on one device and buy on another; attribution gaps; identity coverage questions | Login data, GA4/Google Ads/Meta access | pixel-tag-implementation (parallel-safe) |

## End-to-End Workflows

### Workflow A — E-commerce Cart-Abandonment Machine (weeks 1–6)

1. Run **pixel-tag-implementation**: deploy Meta Pixel + Conversions API and the Google Ads
   remarketing tag via GTM with Consent Mode v2; verify view_item, add_to_cart, begin_checkout,
   and purchase events carrying content_ids that match the catalog. Output: verified event
   stream and clean dataLayer spec.
2. Run **burn-pixels** before a dollar is spent: confirm the purchase event doubles as the burn
   trigger and configure purchaser exclusions on every platform. Output: clean exclusion layer
   with test evidence.
3. Run **audience-segmentation**: build the tier ladder — 30-day all visitors, 14-day product
   viewers, 7-day cart abandoners, 180-day purchasers — plus GA4 imports and email customer
   match. Output: sized, documented audience register.
4. Run **retargeting-ad-creation**: produce the creative matrix per tier — objection handling
   plus shipping/incentive for abandoners, social proof for viewers, bestseller cross-sell for
   purchasers. Output: 3–5 variants per segment with LP pairing.
5. Run **dynamic-retargeting**: connect the Merchant Center/Meta catalog, build product sets
   (viewed-not-purchased, carted, cross-sell pools), and launch DPA/dynamic remarketing with
   template copy. Output: personalized catalog campaigns.
6. Run **frequency-management**: apply caps (3–5/week warm, 5–7 hot abandoners), consolidate
   overlapping ad sets, and schedule the first creative rotation. Output: exposure guardrails.
7. Run **cross-device-tracking**: enable Google signals and verify cross-device conversion
   columns so mobile-research/desktop-purchase journeys join up. Output: unified journey view.
8. Enter the optimization loop: weekly review of ROAS by tier, CVR vs cold traffic, frequency,
   and exclusion health; scale winners, refresh fatigued creative, and reallocate budget
   between tiers monthly.

### Workflow B — B2B Content-to-Demo Funnel (weeks 1–8)

1. Run **pixel-tag-implementation**: Google tag + GA4 with enhanced conversions, Meta Pixel for
   reach; define lead and demo_booked events. Output: instrumented funnel.
2. Run **audience-segmentation**: engagement tiers from GA4 (pricing-page visitors, multi-post
   readers, webinar viewers), plus customer match from CRM and email lists imported to Google
   Ads and LinkedIn. Output: B2B audience ladder.
3. Run **retargeting-ad-creation**: case-study proof for blog readers, comparison messaging for
   pricing visitors, RLSA copy for brand-adjacent searches. Output: funnel-stage creative.
4. Run **cross-device-tracking**: enable Google signals + User-ID so a mobile-read whitepaper
   connects to a desktop demo booking. Output: unified identity view.
5. Run **burn-pixels**: burn on demo_booked (not raw form fill) and sync weekly CRM
   suppressions via customer match. Output: sales-aligned suppression.
6. Run **frequency-management**: cap at 3–4/week (B2B tolerance is lower and cycles longer),
   rotate proof angles monthly. Output: exposure discipline.
7. Monthly loop: review MQL-to-demo by engagement tier with marketing-automation and shift
   budget toward the tier producing SQLs.
8. Quarterly: re-rank engagement tiers from SQL outcomes, refresh proof creative, and re-test
   membership windows against the real sales cycle.

### Workflow C — Quarterly Health & Scale Cycle (recurring)

1. Run **frequency-management** audit: cap adherence, overlap map, fatigue log. Output:
   cap/consolidation actions.
2. Run **burn-pixels** audit: test-conversion propagation checks across all platforms.
   Output: exclusion health verdict.
3. Run **audience-segmentation** refresh: membership windows, sizing vs delivery minimums,
   overlap cleanup. Output: updated register.
4. Run **dynamic-retargeting** feed QA: disapprovals, ID match rate, stock and price sync.
   Output: feed health report.
5. Run **retargeting-ad-creation** refresh: 2–3 new concepts per tier from fresh objection
   mining. Output: rotation-ready creative.
6. Run **cross-device-tracking** verification: identity coverage and measured-vs-modeled
   labeling. Output: measurement update.
7. Close with the KPI review: ROAS vs prospecting, incrementality read, and the budget
   rebalance for next quarter.
8. Document every change in the channel changelog and re-baseline dashboard thresholds.
   Output: versioned program config.

## KPI Dashboard

North-star metric: **retargeting-attributed ROAS** — revenue from warm-audience campaigns
divided by their spend, always checked against an incrementality-adjusted view so view-through
credit does not inflate reality.

| Metric | Source tool | Cadence | Healthy range |
|---|---|---|---|
| Retargeting ROAS | Google Ads / Meta Ads Manager | Weekly | 4–8x; below 2x investigate fatigue, exclusions, or attribution |
| Retargeting CVR vs cold traffic | GA4 + platform reporting | Monthly | 2–5x higher than prospecting campaigns |
| Average frequency (combined) | Platform frequency reports | Weekly | 3–7 per week, capped; >10 burns money and goodwill |
| Retargeting CPM | Platform reporting | Weekly | $2–$10 social/display; >20% MoM inflation signals fatigue |
| RLSA CTR | Google Ads search reports | Monthly | 2–5% with CVR 1.5–3x standard search |
| Active segment depth | Audience managers | Monthly | ≥1,000 users per active segment (delivery minimums) |
| Converted-user exposure | Burn-pixel audit | Monthly | <2% of converted users served retargeting ads |
| Cart-abandonment recovery | GA4 + platforms | Monthly | 5–15% of abandoned carts recovered by ads + email combined |
| Audience pool growth | Audience managers | Monthly | +10–20% MoM during build phase; flat = prospecting problem upstream |
| Audience overlap | Audience insight tools | Monthly | <20–30% between funded segments |
| View-through share of conversions | Platform attribution | Monthly | Monitor only; distrust ROAS if >50% of conversions are view-through |

## Budget Guidance

| Monthly total paid budget | Retargeting allocation |
|---|---|
| < $2,500 | $300–$600; one stack (Meta or Google), simple 3-tier ladder, basic dynamic ads |
| $2,500–$10,000 | 15–20% across Google + Meta; add RLSA, DPAs, and a creative rotation schedule |
| $10,000–$50,000 | 15–25%; full tier ladder, dynamic catalogs, dedicated burn-pixel and frequency ops |
| $50,000+ | 10–20%; prospecting dominates; fund incrementality testing and server-side infrastructure |
| $100,000+ | 10–15%; in-house center of excellence, server-side tagging standard, always-on incrementality |

Allocation principles:

- Retargeting earns the highest ROAS but farms a finite pool — pushing past 30% of paid budget
  usually means over-farming and rising CPMs.
- Fund tag infrastructure before creative: unverified pixels and broken exclusions waste more
  money than weak ads ever will.
- Weight spend by intent tier — cart abandoners and pricing-page visitors earn 2–3x the budget
  of casual page viewers.
- Treat platform-reported ROAS as directional until a holdout test confirms it; rebalance the
  prospecting/retargeting split quarterly on tested numbers.
- Hold 10–15% for tests: new segments, offer structures, and platform features (Demand Gen,
  Advantage+ catalog).
- Match measurement rigor to spend: below $2,500/mo, simple last-click reads are acceptable;
  above $10k/mo, incrementality testing is mandatory before scaling decisions.

## Team & Agency Mapping

| Activity | Best handled by | Rationale |
|---|---|---|
| Strategy, segmentation, budget | In-house marketer | Needs margin data, promo calendar, business context |
| Pixel, tag, and CAPI implementation | Developer + analytics consultant | One-time build, high breakage risk, dev-heavy |
| Ad creative and copy | In-house designer or freelancer | Speed and brand voice matter; retargeting refreshes fast |
| Dynamic feeds and catalogs | In-house e-commerce manager | Feed hygiene is daily operational work, not project work |
| Media buying and optimization | In-house buyer; agency at $50k+/mo or multi-market | Platforms are manageable in-house at SMB scale |
| Reporting and dashboards | In-house analyst (or automated) | Weekly cadence needs tool fluency, not headcount |
| Incrementality testing | Agency or analytics partner | Requires holdout discipline and statistical rigor |
| Frequency and exclusion ops | In-house media buyer | Needs daily platform access and fast reactions |
| Privacy/consent compliance | In-house owner + legal review | CMP and platform policy changes are ongoing operations |

## Reporting Cadence

- **Weekly (media buyer, 30 min):** spend pacing, ROAS by segment tier, frequency, CTR trend,
  exclusion health, and audience pool fill rates vs delivery minimums. Decisions: cap changes,
  budget shifts between tiers, fatigue flags.
- **Monthly (marketing stakeholders, 1 hr):** retargeting vs prospecting ROAS, cart-recovery
  rate, creative fatigue log, audience pool growth, cross-device notes, plus a view-through
  sanity check on every platform ROAS claim. Decisions: creative refresh, segment changes,
  offer updates.
- **Quarterly (leadership):** incrementality read, privacy/compliance audit (consent rates,
  platform policy changes), budget split vs prospecting, and platform roadmap items (Privacy
  Sandbox, modeled conversions) alongside the cookie-deprecation/ATT plan.
- **Ad hoc (within 24h):** pixel/tag breakage alerts, CMP or consent incidents, platform policy
  changes, competitor retargeting assaults on branded search. Decisions: containment first,
  then root cause.

## Cross-Channel Integrations

- **↔ sem-ppc-agent:** RLSA lists and bid adjustments for returning searchers; shared conversion
  tracking; exclude retargeting clickers from prospecting measurement so channel reads stay clean.
- **↔ display-advertising-agent:** shared GTM container; retargeting pool feeds display
  remarketing; display prospecting receives converter-exclusion lists to prevent double-serving.
- **↔ social-media-marketing-agent (social-paid-social-ads):** warm custom audiences built from
  engagers plus site visitors; converters seed lookalikes; frequency coordinated so boosted
  posts and retargeting do not stack.
- **↔ email-marketing-agent:** shared cart-abandoner segmentation — email owns the 1-hour/24-hour
  cadence, ads take over when email opens stall; customer match lists suppress subscribers from
  incentive ads (or target them deliberately for replenishment).
- **↔ web-analytics-agent:** GA4 audience definitions, conversion ownership, and attribution
  reconciliation between platform-reported, GA4, and incrementality views.
- **↔ marketing-automation-agent:** burn-pixel events enroll converted users into post-purchase
  flows; engagement-tier signals feed lead scoring; stage-based suppression prevents email and
  ads from double-messaging the same person.
- **↔ cro-agent:** cart-recovery and offer landing pages are the highest-traffic CRO test
  candidates; share win reports both ways and keep LP message match with the ad matrix.
