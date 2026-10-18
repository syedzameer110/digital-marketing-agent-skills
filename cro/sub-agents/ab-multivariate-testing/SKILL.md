---
name: cro-ab-multivariate-testing
description: Designs, powers, and reads statistically valid A/B, split-URL, and multivariate experiments — hypothesis scoring, sample-size math, MDE planning, QA, no-peeking rules, and post-test analysis — using VWO, Optimizely, Convert, AB Tasty, or A/B Smartly. Use this skill whenever the user wants to run an A/B test, split test, multivariate test, or experiment, asks "which version converts better", or mentions conversion lift, p-values, sample size, or test winners — even if they just say "let's test it".
---

# A/B & Multivariate Testing — CRO Sub-Agent

## Role & Mission

Own experiment integrity for the whole channel: design tests that can actually detect the
effect at hand, run them without statistical self-sabotage, and produce decisions the
business can trust. The outcome is not "a winner" — it is validated lifts implemented, dead
hypotheses killed fast, and type-I errors held at the planned 5%. A program that peeks at
results and ships noise loses more than it wins within a year.

## When to Use

- "Which version converts better?" — hero copy, layouts, offers, checkout flows
- Stakeholders disagree on a design and opinion wars are burning time
- funnel-analysis or user-testing produced a hypothesis worth quantifying
- The page has ~1,000+ conversions/month and a test can reach 80% power in 4–8 weeks
- Post-rebuild validation: proving a landing page rebuild beat the old version
- Deciding whether to roll a change site-wide or keep it template-scoped

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Scored hypothesis backlog | Yes | From funnel-analysis / user-testing |
| Baseline stats per page | Yes | Visitors, conversions, CVR by week (8–12 weeks) |
| Experiment platform access | Yes | VWO, Optimizely, Convert, AB Tasty, A/B Smartly |
| Primary + guardrail metrics | Yes | Plan starts; guardrails: AOV, refunds, support load |
| Dev/design capacity | Preferred | Hours per sprint for variation builds |
| Campaign calendar | Preferred | To avoid launching mid traffic-mix shift |

## Output Contract

Return (1) an experiment plan (hypothesis, design, sample size, runtime, decision rule),
(2) a QA checklist, (3) a results report with per-segment breakdown, (4) a ship/kill decision
with implementation notes. Core payload format:

```json
{
  "test_id": "AB-2025-014",
  "page": "/pricing",
  "hypothesis": "Surfacing the save-20% annual toggle above the fold will lift plan starts",
  "design": "A/B",
  "arms": ["control", "annual-toggle-above-fold"],
  "baseline_cvr": 0.020,
  "mde_relative": 0.15,
  "power": 0.80,
  "alpha": 0.05,
  "sample_size_per_arm": 35000,
  "est_runtime_weeks": 6,
  "primary_metric": "plan_starts_per_visitor",
  "guardrails": ["refund_rate", "support_tickets_per_100_orders"],
  "result": { "control_cvr": 0.0198, "variant_cvr": 0.0241, "lift": 0.217, "p_value": 0.009, "decision": "ship_winner" },
  "novelty_recheck_week": 4
}
```

## Workflow

1. Pull the next hypothesis from the prioritized backlog; reject unscored ideas — a test
   without a problem-cause-effect chain is a coin flip with extra steps.
2. Compute baseline stats for the target page: weekly visitors, conversions, and CVR for the
   last 8–12 weeks; adjust for known seasonality or campaign spikes.
3. Set the MDE honestly. Example: a 2% baseline CVR with a +10% relative lift target needs
   ~78,000 visitors per arm at 80% power (α=0.05, two-sided) — use Evan Miller's calculator
   or the platform's planner and write the number down before building anything.
4. Run the feasibility check: if required runtime exceeds 4–8 weeks, raise the MDE, pick a
   higher-traffic page, or switch to sequential/qualitative methods. Do not launch a test
   that cannot reach power — underpowered flat results mean nothing in either direction.
5. Choose the design: A/B for single changes; split-URL for redesigns; full-factorial
   multivariate only for 2–3 factors — each added factor doubles the cells (3 two-level
   factors = 8 cells), and traffic multiplies with them.
6. Build and QA variations: tracking fires per arm, no flicker (measure anti-flicker cost),
   consistent experience across devices, split-URL tests use 302s or rel=canonical so SEO
   is untouched.
7. Launch with a pre-registered decision rule and a fixed horizon. No peeking — interim
   significance checks inflate false positives several-fold. If using a sequential engine
   (e.g. VWO SmartStats-style always-valid inference), commit to its stopping rule instead.
8. Run to completion regardless of early "winners"; monitor only guardrail metrics mid-flight
   and roll back on severe harm (crashing AOV, spiking refunds).
9. Read out at stop: overall lift, p-value, and per-segment breakdown (device, source);
   schedule a novelty-effect re-check at weeks 2–4 for big behavioral changes; implement the
   winner, log the experiment, and re-baseline with funnel-analysis.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Enterprise experimentation | Optimizely, VWO, AB Tasty, A/B Smartly | Full-stack testing + stats engines |
| Mid-market testing | Convert, VWO, GrowthBook (open source) | Convert: strong privacy posture |
| Sample size & power | Evan Miller's calculator (free), platform planners | Document MDE + power for every test |
| Readout verification | GA4, BigQuery, warehouse SQL | Verify platform numbers against analytics |
| Split-URL variant hosting | Unbounce, Instapage, Webflow | Fast variants without dev queues |

## Example AI Prompt

```text
Act as an experimentation strategist. I want to test {CHANGE / HYPOTHESIS} on {PAGE URL}.
Context: baseline CVR {X}% over the last {N} weeks; ~{V} visitors/week and ~{C} conversions/week
on this page; platform: {VWO / Optimizely / Convert / AB Tasty / A/B Smartly}; dev capacity:
{HOURS} per sprint. Upcoming calendar events: {CAMPAIGNS / SEASONALITY}.

Deliver:
1. A falsifiable hypothesis (problem → suspected cause → predicted effect) and primary metric.
2. Experiment design: A/B vs split-URL vs multivariate, number of arms, and why.
3. Sample-size math at 10% / 15% / 20% relative MDE (80% power, alpha 0.05) with estimated
   runtime per option.
4. A feasibility verdict: run now / raise MDE / choose a higher-traffic page / go qualitative.
5. Guardrail metrics, a QA checklist, and a no-peeking decision rule (fixed horizon or
   sequential — state which and why).
```

## Edge Cases & Guardrails

- Peeking kills significance: checking daily and stopping at the first p<0.05 can inflate
  false positives several-fold; fix the horizon or use sequential testing built for it.
- Novelty effects: short-term winners (new colors, popups) often fade — re-validate headline
  and flow changes at weeks 2–4 before declaring permanent victory.
- Multivariate explodes combinatorially: beyond 2–3 factors, traffic requirements become
  fantasy; run sequential A/B phases instead.
- A "flat" result from a 30%-power test proves nothing; never report underpowered tests as
  "no effect".
- Do not launch during major traffic-mix shifts (Black Friday, big PR) unless that mix IS the
  test context — the samples won't be comparable.
- Statistical winner ≠ business winner: check AOV, margin, refunds, and support load before
  shipping; guardrails exist to catch Pyrrhic victories.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Test win rate | 10–30% of tests significant | >60% (peeking or tracking bugs suspected) |
| Tests launched at ≥80% power | 100% | Repeated underpowered launches |
| Median runtime | 2–6 weeks | Tests exceeding 8 weeks |
| Winner implementation rate | ≥80% shipped within 2 sprints | Winners rotting in the backlog |
| Experiment velocity | 1–4 tests/month on key templates | 0–1 tests per quarter |

## Handoffs

- ← **funnel-analysis** and **user-testing:** supply the prioritized, evidence-backed backlog.
- → **landing-page-optimization:** permanent implementation of validated winners with final copy/design.
- → **cta-optimization** and **form-optimization:** their scoped experiments and readouts.
- → **web-analytics-agent:** metric definitions and experiment-event schemas for clean readouts.
- ↑ **cro-agent:** quarterly roll-up of validated lift, win rate, velocity, and program ROI.
