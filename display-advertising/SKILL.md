---
name: display-advertising-agent
description: Commands the full display advertising workflow — banner creative in IAB sizes, audience targeting, programmatic buying, placement selection, frequency capping, viewability optimization, and CPM/CTR performance reporting across Google Display Network, Display & Video 360, and The Trade Desk. Use this skill whenever the user mentions display ads, banner campaigns, programmatic buying, GDN, DSP campaigns, CPM campaigns, ad placements, or wants cheap awareness reach at scale — even if they never say "display" explicitly.
---

# Display Advertising — Main Agent (Command Hub)

## Channel Overview

Display is the internet's cheapest reach. Programmatic banners put a brand in front of
millions of targetable users at CPMs of $2–$10 on broad inventory ($10–$30+ on niche B2B
or premium placements), making the channel the default engine for awareness, prospecting,
and reminder at scale. The cost of that reach is intent: display CTR runs 0.3–0.7% versus
3–6% for paid search, so judge the channel on efficient, viewable, in-audience reach plus
assisted conversions and brand lift — not last-click CPA alone. Expect a standing
view-through-attribution debate: a banner seen before a branded search is a plausible
assist, not proof of causation, and naive last-click models under-credit display exactly
as naive view-through models over-credit it.

Two structural risks define the craft. Banner blindness means users habitually ignore
ad-shaped slots, so creative quality, format, and placement matter as much as audience
data. Brand safety means a banner can render next to harmful or made-for-advertising (MFA)
content unless category exclusions, ads.txt-verified supply paths, and placement
supervision are in place. Setup is fast — 1–2 weeks on Google Display Network, 2–4 weeks
for a Display & Video 360 or The Trade Desk build (walled-garden inventory such as Meta
Audience Network stays on its own seat) — and spend starts immediately, but credible
brand-lift and incrementality signals need 4–8 weeks of consistent exposure.

Display earns its keep in three situations: building awareness where search demand does
not yet exist, feeding upper-funnel volume into retargeting pools owned by the
remarketing-retargeting channel, and defending share of voice against competitors'
always-on programmatic presence. It is the wrong primary channel for urgent lead gen
(route to sem-ppc-agent), bottom-funnel capture, or conversion goals that cannot afford
prospecting economics. Run it as a portfolio: cheap open-exchange reach at the bottom of
the CPM range, verified PMP quality in the middle, and premium direct deals only where
viewability and attention justify niche CPMs of $10–$30.

## Agent Hierarchy

```text
display-advertising-agent (command hub)
└── sub-agents/
    ├── ad-creative-design/         → IAB-size banners, HTML5 & responsive display ads
    ├── audience-targeting/         → demographics, interests, in-market, custom intent
    ├── programmatic-buying/        → RTB, DSPs, deals, CPM strategy, supply paths
    ├── placement-selection/        → websites/apps choice, exclusions, ads.txt checks
    ├── frequency-capping/          → exposure limits per user, fatigue control
    ├── viewability-optimization/   → MRC-standard seen-ness, Active View, ad density
    └── performance-reporting/      → impressions, CPM, CTR, view-through, brand lift
```

## Sub-Agent Routing Table

| Sub-agent | Call when… | Key inputs | Depends on |
|---|---|---|---|
| ad-creative-design | Launch, CTR fatigue, new size/format, policy disapprovals | Brand guide, offer/USP, landing URLs, size list | None (entry point) |
| audience-targeting | New campaign, segment refresh, CPA too high on broad reach | Personas, GA4/CRM lists, product taxonomy | None (entry point) |
| programmatic-buying | Budget ≥$5K/month, quality demands beyond GDN, deal access | Budget, targeting brief, inventory preferences | audience-targeting, placement-selection |
| placement-selection | Spend concentration, placement audit, brand-safety incident | Placement reports, ads.txt data, exclusion lists | None (parallel-safe) |
| frequency-capping | Frequency >4/week, CTR decaying, CPM inflating | Flight dates, audience sizes, current caps | audience-targeting |
| viewability-optimization | Viewability <70%, media-quality audit, vCPM decisions | Active View/IAS/DoubleVerify reports, placement data | placement-selection, programmatic-buying |
| performance-reporting | Weekly/monthly cycles, attribution disputes, exec reviews | Platform exports, GA4, verification data | all |

## End-to-End Workflows

### Workflow A — New Display Program Launch (weeks 1–6)

1. Run **audience-targeting**: build the segment ladder — affinity/in-market for reach,
   custom intent built from sem-ppc search queries for intent, contextual targeting for
   consent-light (GDPR) markets, first-party lists for seeding. Output: audience plan with
   sizes and expected CPM/CTR per tier.
2. Run **placement-selection**: choose managed allowlists vs curated open exchange, build
   category/topic exclusions, verify ads.txt on direct candidates. Output: inventory plan.
3. Run **ad-creative-design**: produce the IAB size matrix (300x250, 728x90, 320x50,
   160x600, 300x600, 970x250) with static and HTML5 variants plus responsive display ad
   assets; QA click tags, weights, and policy. Output: named creative pack.
4. Run **programmatic-buying** (or GDN build under $5K/month): configure line items, bid
   strategies, deals, and pacing; attach audiences, inventory, and creatives. Output:
   live campaigns with verified tracking.
5. Apply **frequency-capping** and **viewability-optimization** guardrails before scaling
   spend: per-tier caps, viewability floors, ad-density checks. Output: documented
   guardrail settings.
6. Switch on **performance-reporting** from day one: naming conventions, GA4 linkage,
   weekly delivery/quality review. Output: dashboard plus a creative-refresh loop every
   3–4 weeks against CTR-decay signals.
7. Hold settings stable through a 2-week learning window before judging results, then
   hand the program to the recurring optimization loop. Output: clean baseline locked
   for before/after reads.

### Workflow B — Performance Turnaround (CTR/CPA under water)

1. Run **performance-reporting** diagnostic segmented by placement, audience, creative,
   device, and supply path. Output: waste map naming where money burns.
2. Run **placement-selection**: cut MFA and app-spam inventory, enforce ads.txt-verified
   sellers, refresh category exclusions. Output: cleaned inventory list.
3. Run **ad-creative-design** refresh sprint: 2–3 new concepts per priority audience with
   a rotation calendar. Output: new creative pack.
4. Re-run **audience-targeting**: prune segments with CPA >2x target, add custom-intent
   segments from fresh search data. Output: revised audience plan.
5. Tighten **frequency-capping** and **viewability-optimization** settings per the revised
   plan; re-verify viewability ≥70% MRC. Output: updated guardrails.
6. Close with **performance-reporting**: two-week before/after readout with decisions
   logged.
7. Change one variable class at a time (inventory → creative → audience) so the recovery
   is attributable — never flip everything in the same week.

### Workflow C — Quarterly Programmatic Review (recurring)

1. **performance-reporting** quarter pack → 2. **programmatic-buying** supply-path and
   fee audit (win rates, all-in CPM, SPO) → 3. **viewability-optimization** media-quality
   audit → 4. **audience-targeting** segment refresh → 5. **ad-creative-design** full
   concept rotation → 6. **placement-selection** allowlist expansion → 7.
   **frequency-capping** recalibration against the next flight calendar.
   Output: a refreshed flight plan and budget allocation for the coming quarter.

## KPI Dashboard

North-star metric: **efficient, viewable, in-audience reach that lifts assisted
conversions and brand recall** — clicks are a secondary display currency.

| Metric | Source tool | Cadence | Healthy range |
|---|---|---|---|
| Display CTR | GDN / DV360 / Trade Desk | Weekly | 0.3–0.7% prospecting; 0.5–1.0% custom intent |
| CPM — broad open exchange | Platform | Weekly | $2–$10 |
| CPM — niche B2B / PMP / premium | Platform | Weekly | $10–$30 |
| Viewability (MRC: ≥50% pixels ≥1s) | Active View / IAS / DoubleVerify | Weekly | >70% |
| Average frequency | Platform | Weekly | 2–4/week prospecting |
| CPV — display video lines | Platform | Monthly | $0.02–$0.15 in-stream; $0.05–$0.25 outstream |
| Assisted + view-through conversions | GA4 model comparison | Monthly | Upward trend at stable CPA |
| Brand lift (ad recall, awareness) | Google Brand Lift / Kantar / panel survey | Quarterly | Positive, significant lift |
| Invalid traffic (IVT) rate | IAS / DoubleVerify | Monthly | <2% of impressions |
| Unique reach per flight | Platform reach reports | Monthly | Rising at stable frequency |
| Impressions on MFA inventory | IAS / DoubleVerify / SPO audit | Monthly | <5% |

Reading rules: never read CTR without viewability beside it; never read CPA without the
assisted-conversion column; treat platform-reported quality as self-graded until
verification data corroborates it; and any metric breaching its healthy range for two
consecutive weeks becomes a mandatory agenda item with a logged decision.

## Budget Guidance

| Monthly budget | Recommended allocation |
|---|---|
| $1,000–$5,000 | 85% GDN media (managed placements + responsive ads), 15% creative/tools; skip DSP overhead |
| $5,000–$20,000 | 75% media (60% open exchange / 25% PMP / 15% direct), 15% creative, 10% verification & tools |
| $20,000–$75,000 | 70% media via DV360/TTD with SPO discipline, 15% creative & refresh, 10% verification, 5% audience/data |
| $75,000+ | In-house trader + agency support; add brand-lift studies, CDP feeds, dedicated creative QA |

Allocation principles:

- Hold media at 70–85% of spend; creative is the lever that actually moves CTR, so fund
  refreshes, not just the launch pack.
- Never launch DSP programmatic below ~$5,000/month — seat fees, data, and verification
  erase the margin open exchange offers.
- Pay knowingly for quality: 10–30% CPM premiums for PMPs or vCPM floors are rational;
  unexplained premiums are not.
- Reserve ~10% for testing new formats, audiences, and supply paths each quarter.
- Fund verification before vanity: an IAS/DoubleVerify subscription costs less than one
  month of MFA spend it prevents.

## Team & Agency Mapping

| Activity | Best handled by | Rationale |
|---|---|---|
| Channel strategy & budget | In-house marketing lead | Owns brand, funnel role, cross-channel context |
| Programmatic trading | Agency or in-house trader (DV360/TTD seat) | Daily optimization, deal ops, seat economics |
| Banner creative | In-house designer or creative agency | Brand fluency plus HTML5 build skill |
| Audience/data strategy | In-house with analytics support | First-party data is a company asset |
| Verification & brand safety | Vendor (IAS/DoubleVerify) with in-house oversight | Independent measurement beats self-grading |
| Creative fatigue management | In-house (from performance data) | CTR decay is weekly, data-driven work |
| Reporting & dashboards | In-house (automated) | Low marginal effort once built |

## Reporting Cadence

- **Weekly (trader + channel lead, 30 min):** pacing, CPM, CTR, viewability, frequency,
  placement anomalies. Decisions: bid, cap, placement, and creative-rotation changes.
- **Monthly (stakeholders, 1 hr):** delivery vs plan, assisted/CPA outcomes, creative
  fatigue, segment performance, verification scores. Decisions: budget shifts, inventory
  changes, next-month flight plan.
- **Quarterly (leadership):** brand-lift readout, incrementality evidence, supply-path
  and fee audit, CPM/CTR trend lines, annual planning inputs.
- **Ad hoc (trader, same day):** brand-safety incidents, pacing breaks >20%, or sudden
  CTR cliffs trigger an out-of-cycle review before any money moves.

## Cross-Channel Integrations

- **→ remarketing-retargeting-agent:** display prospecting feeds audience pools and shared
  frequency planning, but retargeting campaigns belong to that channel — hand over pixel
  wiring and exclusions, not duplicate budgets.
- **→ sem-ppc-agent:** search query data powers custom-intent segments; display exposure
  lifts branded search. Reconcile branded-search lift and keyword-level synergy jointly.
- **→ video-marketing-agent:** video creatives and CPV-priced media extend display into
  YouTube and DV360 video lineups; share seats, assets, and verification vendors.
- **→ web-analytics-agent:** GA4 conversion configuration, UTM taxonomy, model-comparison
  and view-through measurement rules — display reporting depends on this foundation.
- **→ cro-agent:** banner landing pages are high-traffic CRO test candidates; share
  click-through cohorts and offer messaging for the experiment roadmap.
- **→ email-marketing-agent:** banner-driven visitors who do not convert can be captured
  by on-site email offers; sync creative calendars so email echoes the current banner
  offer instead of contradicting it.
- **← content-marketing / social-media-marketing:** messaging, offers, and audience
  insights flow in as creative briefs and targeting seeds.
