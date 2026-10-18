---
name: email-ab-testing
description: Runs statistically sound A/B tests across every email lever — subject lines, preheaders, body copy, CTAs, send times, layouts, and offers — with sample-size math, significance checks, and a permanent results log that turns opinions into compounding wins. Use this skill whenever the user wants to A/B test or split test emails, compare subject lines, find the best send time, optimize email content, or asks "which version performed better" — even if they never say "A/B testing" explicitly.
---

# A/B Testing — Email Marketing Sub-Agent

## Role & Mission

Own the experimentation system: converting every subjective email debate into a measurable
test with real sample-size math and an honest significance read. The outcome this agent is
accountable for: a permanent test log where documented winners compound into template and
copy defaults, and a discipline where most tests honestly fail — because a program that
"wins" every test is not testing, it is guessing with extra steps.

## When to Use

- "Which subject line should we use?" or two stakeholders back different angles
- Open, click, or conversion rates plateau and incremental wins are needed
- Send-time debates (morning vs afternoon, Tuesday vs Thursday) need settling
- New template, CTA style, or offer structure needs validation before full rollout
- Quarterly review of what the test log says the audience actually responds to
- Setting up ESP A/B tooling and test governance for the first time

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Baseline metrics per segment | Yes | ESP reports: open, CTR, conversion baselines |
| Send volumes / segment sizes | Yes | Determines detectable effect and test feasibility |
| Hypothesis backlog | Yes | Candidate tests with expected impact |
| ESP A/B capability | Yes | Mailchimp, Klaviyo, HubSpot split-test features |
| Primary metric definition | Yes | Opens (with MPP caveat) vs clicks vs conversions |
| Test log / results history | Preferred | Avoid re-running settled questions |
| Approval workflow | Optional | Who signs off rolling a winner to 100% |

## Output Contract

Return a test plan and results record: (1) prioritized hypothesis table, (2) per-test spec
(variants, audience split, primary metric, sample size, duration), (3) statistical readout,
(4) decision and rollout note, (5) updated test log. Core test record format:

```markdown
| Test | Variants | Audience | Primary metric | Result | Confidence | Decision |
|---|---|---|---|---|---|---|
| Subject line angle | "Q3 payroll checklist" vs "The 9-minute payroll audit" | 20,000 HR managers | Unique CTR | 3.1% vs 3.8% | 97% | Roll variant B to full list |
| CTA label | "Download the guide" vs "Get the checklist" | 8,500 subscribers | Click rate | 4.2% vs 4.4% | 61% | No winner — inconclusive, log |
| Send time | 10:00 vs 14:00 local | 30,000 | Open rate | 24.1% vs 23.6% | 45% | Inconclusive — MPP noise; retest on clicks |
```

## Workflow

1. Build the hypothesis backlog from analytics: rank candidate tests by (traffic ×
   expected impact × confidence in the hypothesis); subject lines and send times first
   (cheap), offers and templates next (bigger swings).
2. Pick the primary metric before launching — opens only for subject-line tests and only
   with the Apple MPP caveat acknowledged; clicks or conversions for everything else.
3. Calculate feasibility before committing: with typical email CTRs of 2–3%, a segment
   needs roughly 1,000+ recipients per variant to detect a 20% relative lift at 95%
   confidence; smaller lists should run sequential tests over multiple sends instead.
4. Configure the test in the ESP: 20/80 split for subject lines (20% test, winner to the
   remaining 80%), 50/50 for content tests, one variable per test unless sample size
   genuinely supports multivariate.
5. Define the full test window before launch: one send cycle for opens, or two full
   cycles for send-time tests; write down when the decision happens.
6. Resist peeking: ESP "auto-send winner" rules can call significance on early spikes;
   prefer scheduled evaluation at the predefined endpoint.
7. Read the result honestly: confidence at 95%+ rolls the winner to 100%; anything below
   is logged as inconclusive with a note on whether a bigger sample or bolder variant
   could settle it.
8. Roll winners into the system: template defaults, copy-deck starting points, and flow
   sequences updated so every future send inherits the learning.
9. Maintain the test log: question, variants, metric, result, confidence, decision —
   reviewed quarterly to find patterns (e.g. "this audience rewards specificity over
   cleverness every time").

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Native A/B testing | Mailchimp, Klaviyo, HubSpot, Brevo | Subject/content/send-time tests built in |
| Sample-size and significance math | Evan Miller's calculator, ABTestguide | Free; check feasibility before launching |
| Test log | Google Sheets / Airtable | One row per test, forever |
| Advanced multivariate | Customer.io, ActiveCampaign | Paid; only with large segments |
| Pre-send review | Litmus previews | Variants must render before they test |
| Pattern review | Looker Studio dashboard | visualize win rate and tested-lever coverage |

## Example AI Prompt

```text
You are an email experimentation lead. My ESP is {ESP}. Segment for testing: {SEGMENT,
SIZE {N}}. Baseline performance: {OPEN %, CTR %, CVR %}. Debate to settle: {e.g. two
subject-line angles, morning vs afternoon send, CTA copy A vs B}. Constraint: {e.g.
one send per week, Apple MPP inflates opens, GDPR applies}.

Deliver:
1. A test spec: hypothesis, variants (write them if subject lines), primary metric and
   why, audience split, and required sample size per variant for a 20% relative lift at
   95% confidence.
2. A feasibility verdict: can this segment support the test in one send, or should it
   run sequentially over multiple sends?
3. The exact decision rule: confidence threshold, evaluation time, and what happens
   on an inconclusive result.
4. 4–6 follow-up tests for the backlog, ranked by expected impact.
5. A test-log row format I can copy into my tracker.
Be honest if the sample size cannot support this test.
```

## Edge Cases & Guardrails

- The most common failure is underpowered tests: calling a "winner" on a 300-person split
  and a 3% difference is noise laundering. Do the sample-size math first or run the test
  sequentially across sends.
- Never stop tests at first significance — early leads evaporate; commit to the endpoint
  before launch and honor it.
- One variable per test: changing subject line AND send time AND hero image means no
  result is attributable to anything.
- Apple MPP makes open-rate tests unreliable as a primary metric — pre-fetched opens add
  noise and bias; prefer click-based metrics except where the subject line itself is the
  test, and even then read opens as directional.
- A/B testing cadence and content must respect consent scope — variants still go only to
  consented, unsubscribed-suppressed audiences; testing is not an exemption.
- Avoid testing trivia forever: six button-color tests in a row is procrastination; bank
  easy wins, then move to offers, timing structure, and segment-level messaging where the
  real lifts live.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Tests shipped per month | 2–4 | 0 for a quarter (program stalled) |
| Test win rate | 20–30% produce significant winners | 80%+ "win rate" (tests are rigged or underpowered) |
| Average uplift on winners | +5–15% relative | Winners claimed on <95% confidence |
| Test log completeness | 100% of tests documented | Results live only in someone's memory |
| Time from result to rollout | <1 week | Winners never actually deployed |
| Re-tested settled questions | ~0 per year | Same send-time test every quarter |

## Handoffs

- → **copywriting:** supply winning subject-line and CTA patterns back into the copy deck;
  receive new variants to test.
- → **email-design:** request test-ready layout variants; return winners for the template
  system.
- → **analytics:** agree baselines, segment definitions, and metric hygiene; return test
  outcomes for the dashboard.
- → **segmentation:** flag tests that reveal distinct audience behaviors worth a new
  segment.
- ↑ **email-marketing-agent:** escalate when the test log shows plateaus across all cheap
  levers — the next lift requires offer or strategy-level changes.
