---
name: cro-agent
description: Orchestrates conversion rate optimization across the full funnel — funnel drop-off diagnostics, A/B and multivariate testing, landing page optimization, form friction reduction, CTA and offer optimization, exit-intent capture, and user research. Use this skill whenever the user wants to raise conversion rates, fix checkout or funnel drop-offs, run split tests, improve landing pages, reduce form abandonment, capture leaving visitors, or mentions CRO, CVR, heatmaps, or "why traffic doesn't convert" — even if they never say CRO.
---

# Conversion Rate Optimization (CRO) — Main Agent (Command Hub)

## Channel Overview

CRO multiplies every marketing dollar the business already spends. Traffic channels buy or
earn visitors; CRO raises the value of each one — a 20% CVR lift equals cutting CAC by
roughly 17% with zero additional media, and that gain compounds across every channel that
sends traffic to the same pages. Unlike SEO or content, results do not depend on algorithms
or search volatility: a validated lift is permanent until the page changes, which is why
CRO typically shows the highest ROI per hour of any optimization discipline. The discipline
is empirical by design — opinions lose to experiments, and the experiment log becomes the
company's most defensible growth asset.

The constraint is statistical, not creative: reliable A/B testing on a key page needs roughly
1,000 conversions per month of baseline traffic — below that threshold, tests take quarters
instead of weeks, so smaller sites should prioritize qualitative research (funnel analysis,
session replays, usability tests) and structural rebuilds over classic experimentation.
Individual tests resolve in 2–6 weeks; a program shows compounding site-wide movement in
1–2 quarters. Costs are tooling (experimentation platform, behavior analytics), dev/design
capacity, and research budget — no media spend. CRO wins wherever traffic already exists
and the gap between visits and outcomes is the bottleneck; it loses when the real problem
is traffic volume or offer-market fit, which no button copy can fix.

## Agent Hierarchy

```text
cro-agent (command hub)
└── sub-agents/
    ├── funnel-analysis/           → locate where and for whom visitors drop out
    ├── user-testing/              → discover why they hesitate or struggle
    ├── ab-multivariate-testing/   → prove which variation wins, statistically
    ├── landing-page-optimization/ → rebuild pages for message match & clarity
    ├── form-optimization/         → remove field-level friction in sign-ups
    ├── cta-optimization/          → sharpen buttons, offers & CTA hierarchy
    └── exit-intent-strategies/    → recover visitors about to leave
```

## Sub-Agent Routing Table

| Sub-agent | Call when… | Key inputs | Depends on |
|---|---|---|---|
| funnel-analysis | Program kickoff, a conversion-rate drop, quarterly diagnostics, or before choosing what to test | GA4 access with conversion events, funnel step URLs, behavior-tool data | None (entry point) |
| user-testing | Drop-offs are found but unexplained; before redesigns; small-traffic sites that cannot reach test sample sizes | Research questions, participant screener, live URLs/prototypes, replay exports | funnel-analysis (recommended) |
| ab-multivariate-testing | Hypotheses are queued and the page has ~1,000+ conversions/month; stakeholders disagree on design | Hypothesis backlog, baseline CVR, weekly traffic, platform access, dev capacity | funnel-analysis, user-testing |
| landing-page-optimization | A page converts below benchmark, a new campaign needs a page, or message mismatch is suspected | Page URL + analytics, ad/creative context, brand voice, proof inventory | funnel-analysis, user-testing |
| form-optimization | Form abandonment is 65%+, completion lags, or field-level errors/refills spike | Form analytics access, form URLs, CRM required-field constraints | funnel-analysis |
| cta-optimization | CTA click-through is low, CTAs compete, or a new offer needs button/offer treatment | Click maps, CTA inventory, offer/margin data, test platform | funnel-analysis, landing-page-optimization |
| exit-intent-strategies | High-traffic pages leak visitors without capture; cart abandoners leave; list growth lags | Exit-page analytics, offer economics, ESP/automation integration | funnel-analysis |

## End-to-End Workflows

### Workflow A — CRO Program Kickoff & Baseline (weeks 1–8)

1. Run **funnel-analysis** across the primary conversion funnel (visit → product → cart →
   checkout → purchase, or visit → form → qualified lead) to locate and dollar-size every
   drop-off. Output: drop-off register ranked by revenue opportunity.
2. Run **user-testing** on the two worst steps — usability tests plus session-replay mining —
   to explain the "why" behind the numbers. Output: evidence-backed insight backlog.
3. Ship the obvious structural fixes without waiting for tests: **landing-page-optimization**
   on message match and hierarchy, **form-optimization** on field cuts and validation.
   Output: rebuilt pages with clear before/after baselines.
4. Hand debatable changes to **ab-multivariate-testing**, with **cta-optimization** supplying
   offer and copy variants. Output: 2–4 powered experiments in flight.
5. Deploy **exit-intent-strategies** on the highest-traffic exit pages so otherwise-lost
   visitors are captured while tests run — the fastest payback in the program.
6. Archive every validated change in a pattern library (what won, where, and why) so future
   pages inherit proven components instead of restarting from zero.
7. Re-run **funnel-analysis** at week 8; fold validated learnings into the quarterly sprint
   backlog and the reporting dashboard, and re-baseline all KPIs.

### Workflow B — Quarterly CRO Sprint (recurring, 12 weeks)

1. **funnel-analysis** refresh: re-rank drop-offs, retire solved items, refresh the register.
2. **user-testing** sprint on new pages, new audiences, or unexplained drop-offs.
3. Score the backlog (impact × evidence × effort) and cut to the top 5; **landing-page-
   optimization** and **cta-optimization** produce variation designs.
4. Verify measurement one last time with web-analytics-agent: test events, hold-out logic,
   and conversion definitions agreed before anything launches.
5. **ab-multivariate-testing** runs 3–6 experiments back-to-back — every test planned at
   80% power with a fixed horizon and no peeking.
6. **form-optimization** owns one checkout or lead-form experiment per quarter; forms rarely
   win inside general page tests.
7. **exit-intent-strategies** refreshes offers and creatives quarterly to counter fatigue.
8. Ship winners permanently within two sprints; a winner stuck in a backlog is a lift the
   business never banked.
9. Re-measure the funnel, update the experiment log, and report cumulative validated lift
   with revenue impact — the quarterly number leadership actually reads.

### Workflow C — Checkout Rescue Program (weeks 1–6)

1. **funnel-analysis** isolates checkout steps (cart → shipping → payment → confirm) and
   segments by device and traffic source. Output: worst-step verdict with $ opportunity.
2. **user-testing** mines 100+ abandoned-checkout replays and runs 5–8 moderated tests.
   Output: friction taxonomy — costs, trust, effort, errors.
3. **form-optimization** cuts fields, adds inline validation, fixes error states and mobile
   keyboards. Output: checkout v2 shipped behind the experiment platform.
4. **cta-optimization** sharpens the payment button, trust badges, and cost-transparency
   messaging. Output: revised pay CTA and reassurance strip.
5. **ab-multivariate-testing** validates the rebuild against control — or ships as a staged
   rollout with before/after guardrail metrics if checkout traffic is thin.
6. **exit-intent-strategies** adds a cart-abandonment capture offer; recovered emails hand
   off to the email and automation flows.
7. **form-optimization** monitors payment-step error rates for 2–4 weeks; regressions roll
   back within a day, not a sprint.
8. **funnel-analysis** re-measures cart abandonment against the 60–80% e-comm baseline and
   quantifies recovered revenue for the ROI report.

## KPI Dashboard

North-star metric: **conversion rate on the primary action** — revenue per visitor (RPV) for
e-commerce, lead conversion rate for lead-gen. Every test and fix must trace to it.

| Metric | Source tool | Cadence | Healthy range |
|---|---|---|---|
| Site-wide conversion rate | GA4 | Weekly | 1–3% e-comm; 2–5% lead-gen |
| Revenue per visitor (RPV) | GA4 e-commerce | Weekly | Upward trend QoQ |
| Test win rate | Experiment platform | Quarterly | 10–30% of tests significant |
| Statistical power of shipped tests | Experiment platform | Per test | ≥80% planned, fixed horizon |
| Typical MDE per test | Test plan | Per test | 5–15% relative lift |
| Test velocity | Experiment platform | Monthly | 1–4 tests/month on key templates |
| Experiment coverage (% sessions on a tested template) | GA4 + platform | Monthly | Rising; 0% two months running = stalled program |
| Winner implementation lag | Sprint board | Monthly | ≤2 sprints from readout to live |
| Research insights shipped per quarter | Research log | Quarterly | ≥6 insights converted to tests/fixes |
| Cart abandonment (e-comm) | GA4 | Monthly | 60–80% typical; >85% investigate |
| Form abandonment (key forms) | Form analytics | Monthly | 65%+ typical; fix field-level spikes |
| Exit-capture opt-in rate | Popup platform | Monthly | 1.5–4% of shown visitors |

## Budget Guidance

| Monthly budget | Recommended allocation |
|---|---|
| Under $1,500 | Free stack (GA4, Microsoft Clarity, sample-size calculators, Sheets); spend mostly on dev/design hours + light research |
| $1,500–$5,000 | ~30% tooling (VWO/Convert starter + Hotjar), ~50% dev/design for variations, ~20% research panel credits |
| $5,000–$15,000 | ~25% tooling (AB Tasty/Optimizely tier, Mouseflow/Zuko), ~45% dev/design, ~30% research (Maze/UserTesting studies) |
| $15,000+ | In-house CRO lead + enterprise experimentation platform + standing research retainer; ~20/50/30 split with agency dev support |

Allocation principles:

- Traffic decides tooling: classic A/B testing needs ~1,000+ conversions/month on the page
  being tested — below that, fund research and rebuilds instead of experimentation licenses.
- Dev capacity is the real bottleneck; a test platform without design/dev hours produces a
  backlog, not lifts.
- Research before redesign: replays and usability studies are the cheapest defense against
  confidently wrong changes.
- Reserve ~10% of budget for measurement fixes — broken event tracking invalidates every
  result downstream.
- Fund implementation, not just discovery: every budget line for testing should carry a
  matching line for shipping winners within two sprints.
- Pay for qualitative research even at small scale — 5-user usability studies and replay
  mining fit almost any budget and de-risk every redesign.
- Discount-based levers (exit offers, checkout incentives) need a margin guardrail agreed
  with finance before the first coupon fires.

## Team & Agency Mapping

| Activity | Best handled by | Rationale |
|---|---|---|
| Program strategy & prioritization | In-house (or fractional CRO lead) | Requires margin and business context |
| Test development & QA | In-house dev, or CRO agency retainer | Iteration speed sets test throughput |
| UX research & usability testing | Specialist freelancer/agency or trained in-house researcher | Process- and panel-driven work |
| Statistical analysis & readouts | In-house analyst | Guards against peeking and false winners |
| Landing page builds | LP platform + freelancer (Unbounce/Instapage) | Volume work with fast turnaround |
| Research operations (recruiting, panels) | Agency panel (Maze/UserTesting) or in-house ops | Scheduling and incentives are process-heavy |
| Exit-intent offers & capture forms | In-house marketer with tool admin | Low risk, fast iteration |

## Reporting Cadence

- **Weekly (CRO lead, 30 min):** running-test status (readouts at completion only, never
  interim peeking), funnel movement, shipping queue. Decisions: launch, pause, or iterate.
- **Monthly (stakeholders, 1 hr):** KPI dashboard, winners implemented, revenue impact of
  validated lifts, research findings, next test queue. Decisions: backlog re-prioritization
  and resourcing.
- **Quarterly (leadership):** cumulative validated lift and program ROI, win rate, velocity
  vs plan, tooling and budget review, offer-margin health. Decisions: scale up, pivot focus,
  or re-platform.

## Cross-Channel Integrations

- **↔ web-analytics-agent:** the measurement backbone — conversion-event design, experiment
  tracking, and the funnel exports this channel runs on; send test assignments and hold-out
  definitions, receive clean event schemas, experiment QA, and attribution checks.
- **↔ sem-ppc-agent:** paid search landing pages are the highest-leverage test candidates;
  receive ad copy and keyword context so landing-page-optimization can enforce ad-to-page
  message match; return validated variants to protect Quality Score.
- **↔ social-media-marketing-agent (paid social):** align campaign creative angles with
  landing page heroes; social traffic often needs its own LP variants and proof styles.
- **↔ email-marketing-agent:** exit-intent captures feed list growth; validated offer tests
  flow into campaigns and cart-recovery sequences; email click patterns return as CTA and
  landing-page hypotheses.
- **↔ marketing-automation-agent:** recovered abandoners and form leads are routed to
  nurture journeys; progressive-profiling data flows back into form design; automation
  platforms (HubSpot, Klaviyo) also host the capture forms exit-intent-strategies ships.
- **↔ display-advertising-agent:** funnel drop-off segments become remarketing audiences;
  test-validated messages carry into display creative variants.
- **↔ seo-agent:** high-traffic organic landing pages are prime CRO targets; coordinate so
  experiments and exit overlays never destabilize ranking pages.
