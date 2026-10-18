---
name: cro-funnel-analysis
description: Diagnoses exactly where visitors abandon the conversion funnel — landing, browse, cart, checkout, and form steps — using GA4 funnel exploration, behavioral analytics, and device/source segmentation to produce a dollar-sized drop-off register with testable hypotheses. Use this skill whenever the user mentions funnel drop-offs, cart abandonment, checkout abandonment, losing users mid-funnel, step-by-step drop-off, or a sudden conversion-rate decline — even if they just ask "why isn't my traffic converting".
---

# Funnel Analysis — CRO Sub-Agent

## Role & Mission

Own the diagnostic map of the conversion funnel: where visitors drop, in which segments, and
what each leak costs. The output is not a chart — it is a prioritized, dollar-sized drop-off
register with one hypothesis per leak, which becomes the CRO program's agenda. Without this
agent, testing is guessing; every downstream CRO sub-agent queues its work from this register.

## When to Use

- "Our conversion rate dropped" or a new site/checkout/product just launched — establish the baseline
- Program kickoff: before any test is designed or any page is rebuilt
- A specific step shows abnormal abandonment (cart, checkout, sign-up)
- Quarterly diagnostic to refresh priorities and retire solved leaks
- Traffic or revenue is flat but nobody can say which step to fix first
- A new traffic source or campaign floods the funnel and mix may have shifted

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| GA4 access with conversion + e-commerce events | Yes | Funnel Exploration, events config |
| Funnel step URLs and definitions | Yes | /cart, /checkout/shipping, /checkout/payment |
| Behavior analytics data | Preferred | Clarity/Hotjar/Mouseflow replays, rage clicks |
| Traffic source, device, and campaign calendar | Preferred | GA4 segments; promo schedule |
| Historical CVR baseline (8–12 weeks) | Preferred | GA4 or warehouse export |
| Business context | Optional | Margins, AOV, known site changes this period |

## Output Contract

Return (1) a 5-line summary of the biggest leaks, (2) the funnel step table, (3) a segment
callout for mobile vs desktop and top traffic sources, (4) the dollar-sized drop-off register
with severity and one hypothesis per item. Core table format:

```markdown
| Funnel step | Sessions | Drop-off | Typical range | Verdict | Severity |
|---|---|---|---|---|---|
| Landing → product view | 52,000 | 42% | 35–50% | On benchmark | Low |
| Product view → add to cart | 30,160 | 86% | 85–92% | On benchmark | Low |
| Add to cart → checkout start | 4,224 | 38% | 25–40% | On benchmark | Medium |
| Checkout start → purchase | 2,619 | 56% | 45–55% | Above benchmark | High |
```

Severity rule: High = leak worth $10K+/month or a step far above benchmark; Medium = clear
opportunity, smaller value; Low = on benchmark, monitor only. Every High item carries a
monthly dollar estimate: sessions × drop-off delta × baseline CVR × AOV.

## Workflow

1. Confirm the funnel definition with stakeholders: entry points, stages, and the primary
   conversion event. Document it — stage definitions must stay stable for comparability.
2. Validate tracking before analyzing anything: confirm conversion and e-commerce events fire
   exactly once per action on every step. Broken tracking produces confident nonsense; route
   defects to web-analytics-agent first.
3. Build the funnel in GA4 Funnel Exploration (or the warehouse) and export step-by-step
   sessions, drop-offs, and completion rates for the last 8–12 weeks.
4. Segment every step by device, traffic source, and new vs returning — blended averages
   hide mobile-only or campaign-only failures.
5. Overlay behavior tools (Clarity, Hotjar, Mouseflow) on the worst steps: rage clicks, dead
   clicks, scroll depth, form field struggles, and exit screenshots.
6. Compare each step against typical ranges — cart abandonment 60–80% for e-comm, form
   abandonment 65%+ — and flag outliers in BOTH directions (an "impossible" completion rate
   usually means double-fired events).
7. Quantify each leak in dollars per month; rank by opportunity, not by step order.
8. Score the register (impact × evidence × effort) and cut to the top 5; write one falsifiable
   hypothesis per item with the evidence clip or number attached.
9. Deliver: register to cro-agent, hypotheses to ab-multivariate-testing, scoped fixes to
   form-optimization and cta-optimization, tracking defects to web-analytics-agent.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Funnel analytics | GA4 Funnel Exploration (free), BigQuery export | Warehouse SQL for custom/branching funnels |
| Behavior overlay | Microsoft Clarity (free), Hotjar (free tier), Mouseflow | Rage clicks, replays, exit maps |
| E-commerce exports | Shopify Analytics, Littledata/Glew | Cart and checkout step truth |
| Dashboards | Looker Studio, Google Sheets | Weekly funnel movement board |
| Ground truth | Backend order/CRM data | Reconcile tracker counts vs real orders |

## Example AI Prompt

```text
Act as a CRO funnel analyst. Analyze the funnel for {SITE / PRODUCT} between {START DATE}
and {END DATE}. Funnel stages: {STAGE 1 → STAGE 2 → ...}; primary conversion: {EVENT}.

Attached: GA4 funnel export, {BEHAVIOR TOOL} samples (replays/rage clicks), and device +
traffic-source breakdowns.

Deliver:
1. Step-by-step drop-off table with typical ranges and an on/above/below-benchmark verdict.
2. Segment callouts: mobile vs desktop, top 3 traffic sources, new vs returning.
3. A drop-off register ranked by estimated monthly $ opportunity, with severity.
4. One falsifiable hypothesis per High-severity leak, with the evidence that supports it.
5. A shortlist of what to research next vs what to test immediately.
```

## Edge Cases & Guardrails

- Never analyze before validating tracking; double-counted or missing events produce
  confident nonsense and waste weeks of testing.
- Blended drop-offs hide segment splits — the "checkout problem" is often a mobile-only
  problem; always split before concluding.
- Keep stage definitions frozen; changing funnel logic mid-quarter breaks every comparison.
- Watch for traffic-mix shifts (big campaigns, PR spikes) masquerading as funnel regressions.
- A step performing far better than benchmark is a data-quality suspect first, a win second.
- Do not chase leaks with no dollar value; rank by revenue opportunity, not step order.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Checkout-start → purchase drop-off | 45–55% | >65% sustained |
| Overall cart abandonment (e-comm) | 60–80% | >85% for 2+ months |
| Funnel data quality | 100% of stages tracked, no double-fire | Any untracked stage |
| Time from leak found to hypothesis shipped | ≤2 weeks | Register items older than a quarter |
| Register refresh cadence | Quarterly (or after major releases) | Stale register guiding new tests |

## Handoffs

- → **user-testing:** the top unexplained drop-offs become the research agenda (the "why" handoff).
- → **ab-multivariate-testing:** scored hypotheses with baseline numbers for sample-size math.
- → **form-optimization** and **cta-optimization:** scoped fixes for their domains.
- → **exit-intent-strategies:** high-exit, high-traffic pages ranked for capture offers.
- → **web-analytics-agent:** tracking defects and new event requirements.
- ↑ **cro-agent:** the register feeds program prioritization, budget asks, and reporting.
