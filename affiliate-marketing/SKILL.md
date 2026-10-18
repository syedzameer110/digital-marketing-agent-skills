---
name: affiliate-marketing-agent
description: Orchestrates the entire affiliate channel end to end — program setup, partner recruitment, commission structures (CPS/CPA/CPL), tracking and attribution, creative asset provision, partner management, fraud monitoring, payouts, and ROI reporting across networks like ShareASale, CJ Affiliate, Awin, Impact, Rakuten, and PartnerStack. Use this skill whenever the user mentions an affiliate program, partners, commission structure, CPS, CPA, CPL, affiliate network, publisher deals, EPC, or cookie windows — even if they never say "affiliate marketing" explicitly.
---

# Affiliate Marketing — Main Agent (Command Hub)

## Channel Overview

Affiliate marketing is performance-based partnership distribution: you pay partners (content
and review sites, coupon and loyalty publishers, creators, comparison engines) only when they
deliver a measurable result — a sale (CPS), a qualified lead (CPL), or a defined action or
trial (CPA). This pay-on-results economics makes affiliate the lowest-risk paid channel:
media risk sits with the partner, and your cost is a commission — typically 5–30% of order
value in e-commerce, 20–50% for digital products and courses, or $20–$200 per qualified
action/trial in B2B SaaS — plus network fees of roughly a 20–30% override on commissions or
$50–$2,000/month for SaaS platforms.

The channel wins when product margins support commissions, when the buying journey involves
research or comparison (review, listicle, and coupon partners intercept that demand), and when
you need incremental reach beyond owned channels without upfront media risk. Time to results:
a network-hosted program attracts applications within days, but expect 2–3 months to build an
active roster and 6–12 months to reach a mature, diversified revenue base. The classic failure
modes — coupon-site cannibalization of last-click credit, dormant partners after signup,
cookie stuffing and code leakage, and late or disputed payouts — are exactly what the
sub-agents below are designed to prevent.

One discipline governs everything here: incrementality. A commission paid on a sale you
would have captured anyway is not performance marketing, it is a discount with extra steps.
The program therefore manages partner mix (demand-creating content partners vs
harvest-oriented coupon/loyalty publishers), measures new-customer share, and prices each
role accordingly through commission-structure.

## Agent Hierarchy

```text
affiliate-marketing-agent (command hub)
└── sub-agents/
    ├── program-setup/             → define terms, choose platform/network
    ├── affiliate-recruitment/     → find, vet & onboard productive partners
    ├── commission-structure/      → design CPS/CPA/CPL payout models & tiers
    ├── tracking-setup/            → links, cookies, codes, attribution QA
    ├── creative-asset-provision/  → banners, text links, datafeeds, code kits
    ├── partner-management/        → comms, activation, placements, support
    ├── fraud-monitoring/          → detect & block fake traffic/conversions
    ├── payout-management/         → approvals, invoices, taxes, reconciliation
    └── performance-reporting/     → partner ROI, program P&L, forecasting
```

## Sub-Agent Routing Table

| Sub-agent | Call when… | Key inputs | Depends on |
|---|---|---|---|
| program-setup | Launching a program, migrating networks, or revisiting terms | Margins, AOV, geo scope, brand/legal constraints | None (entry point) |
| commission-structure | Setting or re-pricing payouts, adding tiers or partner types | Margin data, AOV, LTV, network fee structure | program-setup |
| tracking-setup | Before launch, after platform changes, or when conversions look lost | Platform access, cart/app access, GA4 | program-setup, commission-structure |
| creative-asset-provision | New campaigns, seasonal pushes, stale creatives, code launches | Brand kit, campaign calendar, asset EPC data | tracking-setup, commission-structure |
| affiliate-recruitment | Building the roster, filling category gaps, activating a new market | Ideal partner profile, offer terms, live creatives | program-setup, tracking-setup, creative-asset-provision |
| partner-management | Ongoing comms, dormant-partner activation, paid placements, policy enforcement | Roster export, EPC segments, comms calendar, deal authority | affiliate-recruitment, creative-asset-provision |
| fraud-monitoring | Every payout cycle, CR/EPC spikes, brand-bid complaints, code leaks | Click/conversion logs, partner baselines, code mapping | tracking-setup |
| payout-management | Weekly/monthly payment cycles, clawbacks, tax season, disputes | Validated conversion ledger, payment terms, tax status | fraud-monitoring, commission-structure |
| performance-reporting | Weekly/monthly/quarterly cycles, budget reviews, board requests | Network exports, GA4, payout costs, targets | All (terminal node) |

## End-to-End Workflows

### Workflow A — New Program Launch (weeks 1–8)

1. Run **program-setup** to define the foundation: commission economics vs margin, geo and
   currency scope, network-vs-SaaS platform decision, and the policy set (FTC disclosure,
   brand-bidding restrictions, coupon-site rules) baked into enforceable T&Cs.
   Output: signed-off program charter.
2. Run **commission-structure** to convert margin math into the payout matrix: default CPS
   rate by category, capped rates for coupon/loyalty partners, premium rates for content
   partners, tier bonuses with sunset dates. Output: rate card + margin guardrails.
3. Run **tracking-setup** before any partner joins: deploy S2S postback tracking, validate
   every deeplink, configure the cookie window (30-day standard; 7-day Amazon-style where
   margin demands), map unique promo codes per partner, and set dedup rules vs paid channels.
   Output: 100% passing test conversions.
4. Run **creative-asset-provision** to stock the launch kit: standard banner set, text/deeplinks,
   product datafeed, and per-partner code kits. Output: searchable, compliant creative library.
5. Run **affiliate-recruitment**: source from network directories, competitor partner maps, and
   SERP review sites; vet for traffic quality and compliance; approve and onboard with a
   quick-start kit. Output: first 30–100 approved partners.
6. Hand the roster to **partner-management**: welcome sequences, day 7/14/30 activation
   touches, and first-campaign suggestions matched to each partner's content type.
   Output: first revenue-bearing, activated partners.
7. Close each month with **performance-reporting** (KPIs vs launch targets),
   **fraud-monitoring** (pre-payout validation), and **payout-management** (first clean
   payment cycle). Output: baseline channel P&L and a payment run finance trusts.

### Workflow B — Q4 Peak Readiness (8–6 weeks before peak)

1. **performance-reporting** audits the year-to-date base — which partners, categories, and
   creatives actually carry revenue at healthy margin — and forecasts peak demand.
2. **partner-management** briefs and negotiates with the top 20 partners: newsletter slots,
   homepage takeovers, gift-guide placements, and accelerated payment terms where justified.
3. **creative-asset-provision** ships the seasonal kit: refreshed banners, holiday codes with
   explicit start/end dates and checkout enforcement, and updated datafeeds for gift categories.
4. **commission-structure** approves peak boosters (temporary +2–5% CPS or bonus bounties)
   with hard margin floors and explicit end dates.
5. **tracking-setup** load-tests links and code expiry automation and confirms S2S postback
   reliability under peak concurrency.
6. **fraud-monitoring** raises alert coverage for peak-season schemes (code leakage,
   coupon-page spikes, brand-bid abuse) and **payout-management** pre-clears cash flow and
   tax paperwork for the largest cycles of the year.
7. **affiliate-recruitment** runs a pre-peak push to fill seasonal gaps (gift guides,
   comparison pages publish in September–October to rank by November) and schedules a
   post-peak retro with **performance-reporting** to capture next year's playbook.

### Workflow C — Monthly Optimization Loop (recurring)

1. **performance-reporting** delivers the monthly pack: leaderboard, EPC by partner and
   creative, new-customer share, and net margin after commissions and fees.
2. **fraud-monitoring** validates the conversion ledger before approvals and flags suspects.
3. **payout-management** runs the payment cycle on the clean ledger and logs clawbacks.
4. **partner-management** acts on the leaderboard: QBRs and placement upsells for top
   producers, reactivation for dormant, evidence-based enforcement where flagged.
5. **commission-structure** reviews EPC vs margin per segment and adjusts rates or tiers.
6. **affiliate-recruitment** fills coverage gaps whenever concentration risk rises
   (top-5 partners >50% of revenue) or a category has no producing partner.

## KPI Dashboard

North-star metric: **affiliate-attributed revenue per month at target net margin** — after
commission, network fees, and reversals; raw GMV flatters this channel, margin does not.

| Metric | Source tool | Cadence | Healthy range |
|---|---|---|---|
| Affiliate share of total revenue | Network + GA4 | Monthly | 10–25% of online revenue |
| EPC (earnings per 100 clicks) | Network reports | Weekly | $20–$100+ e-comm; higher for B2B |
| Partner approval rate (vetted applications) | Platform records | Monthly | >90% |
| Fraud/invalid conversion rate | Fraud-monitoring review | Monthly | <2% of conversions |
| Reversal/clawback rate | Network reports | Monthly | <5% of approved conversions |
| Active partner ratio (produced in last 30d) | Network roster report | Monthly | 10–30% of approved roster |
| Top-5 partner revenue concentration | Performance-reporting | Quarterly | <50% of revenue |
| Net ROAS (revenue ÷ commissions + fees) | Reporting stack | Monthly | 5–15x typical for CPS programs |
| New-customer share of affiliate orders | GA4 + network data | Monthly | ≥40–60% depending on program goal |
| Time to first sale (new partners) | Network roster reports | Monthly | ≤60 days for 20–40% of onboarded |

## Budget Guidance

Affiliate budgets are mostly variable: the more partners sell, the more you pay — that is the
model's core advantage. Plan commissions as a revenue share first, then layer fixed costs
(platform fees, placements, tooling) on top.

| Monthly affiliate revenue | Recommended allocation |
|---|---|
| <$10,000 | 80–90% commissions, 10% platform (SaaS: Refersion/Rewardful/ShareASale fee); founder-led recruitment |
| $10,000–$50,000 | 70–80% commissions, 10–15% network override/SaaS fee, 5–10% incentives & placements, 5% tools |
| $50,000–$200,000 | 65–75% commissions, 10% network fees, 10% paid placements/content deals, 5% manager time & tools |
| $200,000+ | Dedicated in-house manager + agency support; add 5–10% for bounties, exclusives, and partner events |

Allocation principles:

- Model the all-in cost of sale before setting rates: rate × (1 + network override of
  20–30%) + a reversal allowance. A 10% CPS on a 25% override actually costs 12.5% of revenue.
- Reserve 5–10% for incentives — tier bonuses, peak boosters, competitions. This is the
  cheapest growth lever in the channel because it only pays on incremental performance.
- Paid placements (sponsored reviews, newsletter slots) break pure-CPA economics; negotiate
  flat/CPM only with proven partners and verify incrementality before renewing.
- Hold a fraud/reversal buffer of 3–5% of commission spend and reconcile it quarterly
  through performance-reporting so finance never gets surprised.
- Treat the network override like media cost, not overhead: when comparing networks, score
  total cost (override + monthly minimums + setup) against the tracking, recruitment reach,
  and payment services each one actually delivers.

## Team & Agency Mapping

| Activity | Best handled by | Rationale |
|---|---|---|
| Strategy, terms & rate decisions | In-house (channel owner) | Margin, brand, and legal context are internal knowledge |
| Network/platform administration | In-house coordinator (part-time early) | Routine approvals, creatives, reports; cheap to keep internal |
| Recruitment & outreach | In-house + agency hybrid | Agencies bring publisher relationships; networks bring directory reach |
| Top-tier partner management | In-house | High-touch negotiation and placement deals need trust and authority |
| Fraud operations | In-house with platform tooling | Requires click-log access, fast escalation, and discretion |
| Payments & tax compliance | Finance + platform automation | Compliance-sensitive (W-8/W-9, 1099); automate rails, keep control |
| Analytics & reporting | In-house analyst | Needs GA4 + network data joins and business context |

## Reporting Cadence

- **Weekly (affiliate manager, 30 min):** revenue, EPC, new partners, activation status,
  top movers, fraud flags. Decisions: campaign adjustments, outreach priorities.
- **Monthly (stakeholders, 1 hr):** full KPI dashboard, partner leaderboard, payout cycle
  summary, net margin after commissions, next-month plan. Decisions: rate/tier changes,
  placement budget, enforcement actions.
- **Quarterly (leadership):** channel P&L and incrementality review, concentration and fraud
  risk, network/platform contract and fee review, forecast update. Decisions: platform
  migration, structural rate redesign, budget shifts between channels.

## Cross-Channel Integrations

- **→ influencer-marketing-agent:** convert influencer collaborations into tracked affiliate
  partnerships — unique codes, deeplinks, and bounty commissions; exchange creator lists and
  performance data so gifted posts become measurable revenue.
- **↔ sem-ppc-agent:** enforce the branded-bid policy. Partners bidding on brand terms must
  follow the SEM exclusion list; reconcile brand-PPC vs brand-affiliate last-click conflicts
  and agree dedup rules in writing.
- **↔ seo-agent:** coupon/deal and review sites rank organically on "brand + coupon" and
  "best {category}" queries — coordinate which partners own those SERPs, monitor
  cannibalization of your own content, and mine backlink data for recruit-worthy publishers.
- **↔ web-analytics-agent:** reconcile network conversions vs GA4 (keep the gap under
  5–10%), align attribution windows and dedup logic, and implement consent-compliant
  click tracking.
- **→ email-marketing-agent:** newsletter partners need compliant email creative and
  suppression-list handling; cross-promote affiliate offers to owned lists only where
  margin-safe.
- **← cro-agent:** partner traffic lands on the same templates as paid traffic — share test
  wins and landing page variants to lift partner EPC, which directly raises partner motivation.
- **← social-media-marketing-agent:** organic social surfaces creator talent worth converting
  into tracked affiliate partners; social engagement data highlights which content angles
  partners should amplify next.
