---
name: automation-behavioral-targeting
description: Turns raw user actions into automated responses — browse and cart abandonment, pricing-page visits, content consumption, product usage, and churn-risk signals mapped to segments, branches, and personalized follow-ups in near real time. Use this skill whenever the user mentions behavioral targeting, event-based triggers, browse abandonment, product-qualified leads, usage-based segments, personalization based on site or app behavior, "follow up when someone visits…", or wiring event schemas via Segment or GTM.
---

# Behavioral Targeting — Marketing Automation Sub-Agent

## Role & Mission

Turn raw user actions into automated responses: browse and cart abandonment, pricing-page
visits, content consumption streaks, product-usage signals, and churn-risk behaviors mapped
to segments, workflow branches, and personalized follow-ups in near real time. This agent
sits between the event pipeline (Segment/GTM/app analytics) and the automation platform and
owns the difference between a database that merely receives campaigns and one that responds
to what people actually do — the core mechanism behind automation's 2–5x per-message
advantage over batch sends.

## When to Use

- "We want to follow up when someone visits the pricing page" or abandons a cart or form
- High-intent behaviors happen daily but trigger nothing
- PLG/product-qualified lead (PQL) motions need usage-based routing and alerts
- Site/app personalization: returning visitors should see segment-aware content
- Event tracking exists in analytics but the automation platform never uses it
- Win-back/churn-risk programs need behavioral early-warning signals

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Event inventory + schema | Yes | view_pricing, add_to_cart, feature_used, plan_limit_hit |
| Analytics platform access | Yes | GA4, Amplitude, Heap, Mixpanel |
| Automation platform access | Yes | Klaviyo, Customer.io, Braze, HubSpot |
| Segment/value definitions | Preferred | What counts as "high intent" per behavior |
| Consent & privacy rules | Yes | Cookie consent states, regional tracking limits |
| Behavior→conversion history | Preferred | Which behaviors actually predict buying |

## Output Contract

Return: (1) behavior playbook summary, (2) the playbook table (below), (3) segment/branch
specs for the platform, (4) test evidence that each behavior fires the intended action.
Core playbook format:

```markdown
| Behavior | Signal source | Automated response | Timing | Success metric |
|---|---|---|---|---|
| add_to_cart, no purchase in 60 min | Klaviyo event (web + app) | 3-step cart recovery flow | 1h / 24h / 72h | 5–15% cart recovery |
| 3+ pricing-page views in 7 days (lead) | GA4 → Segment → HubSpot | +40 behavior score, sales alert | Within 1 business day | MQL→SQL ≥15% |
| Seat utilization >80% (customer, PLG) | Amplitude → Customer.io | Expansion nudge + AE task | Weekly check | Expansion pipeline created |
| 30 days no login after week-4 activation | Product events | Re-onboarding drip | Day 30/37/44 | Reactivation ≥8% |
```

## Workflow

1. Inventory candidate behaviors from the event schema and analytics: page views, cart and
   checkout events, content consumption, form starts, product usage, support signals.
2. Rank behaviors by predictive value: pull behavior→conversion rates from analytics (e.g.
   pricing viewers convert 4x baseline) and prioritize the top 5–10 signals.
3. Define thresholds and windows that separate intent from noise: "3 pricing views in 7
   days", not "1 ever"; sustained behaviors beat single events.
4. Validate the data path: confirm each event actually reaches the platform (Segment
   debugger, Klaviyo event feed, Customer.io activity log) with correct properties.
5. Build segments and branches in the automation platform: behavior-based segments, score
   bumps via lead-scoring, and entry into dedicated behavior workflows.
6. Design the responses: timed follow-ups, content referencing the behavior (cart items,
   feature names), and sales alerts for human-touch-worthy signals.
7. Set tone and privacy guardrails: reference the action helpfully ("your cart is saved"),
   never creepily ("we watched you view our pricing four times").
8. Test with dummy users: fire each behavior in staging and on production-safe test
   accounts; verify timing, personalization, and that exits (purchase, churn) suppress it.
9. Monitor monthly: per-behavior conversion, retire signals that stopped predicting, and
   add new ones as the product and site evolve.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Event pipeline / schema | Segment, Rudderstack, GTM dataLayer | Segment free tier covers early stage |
| Product analytics | Amplitude, Heap, Mixpanel | Usage signals for PQL motions |
| Behavioral email/SMS | Customer.io, Braze, Klaviyo | Customer.io has the strongest event-branch UX |
| Web personalization | Mutiny (B2B), Optimizely, HubSpot smart content | Segment-aware on-site content |
| E-commerce behavior | Klaviyo (Shopify/Magento native events) | Cart/browse events pre-built |
| Verification | Segment debugger, platform activity logs, dummy accounts | Never assume a fire; verify it |

## Example AI Prompt

```text
You are a behavioral targeting strategist. Build the behavior playbook for {BUSINESS}
({B2B SAAS / ECOMMERCE}) using {PLATFORM} and {EVENT PIPELINE (Segment / GTM / app)}.

Event inventory with volumes: {EVENT LIST + FREQUENCIES}.
Behavior→conversion data: {PASTE ANALYTICS EXPORT OR "none — use typical patterns"}.
Lifecycle stages: {SUBSCRIBER/LEAD/MQL/SQL/CUSTOMER}.

Deliver:
1. Ranked behavior list: behavior | predictive rationale | priority (top 5–10 only).
2. Playbook table: behavior | source | automated response | timing | success metric.
3. Segment and branch specs for {PLATFORM}, including score impacts and exits.
4. Tone guardrails: example copy that references behavior helpfully, not creepily.
5. Dummy-record test plan per behavior.
Constraints: {CONSENT RULES, PRIVACY LIMITS, SALES ALERT CAPACITY}.
```

## Edge Cases & Guardrails

- Single events lie: one pricing view is curiosity, three in a week is intent — threshold
  behaviors before acting, or sales drowns in false-positive alerts and mutes you.
- Exit-before-send applies doubly here: a purchase, churn, or support escalation must
  suppress behavior flows immediately — "ready to buy?" emails sent after checkout are a
  brand-damaging race condition.
- Tone-test every message: "Complete your checkout" helps; "We noticed you viewed X four
  times" reads like surveillance — reference the action, not the stalking.
- Consent gates tracking itself: EU/CCPA consent states must control which events fire at
  all; a behavior program built on non-consented events is a legal liability, not a tactic.
- Filter QA/dev environments: localhost cart tests and staging events must never trigger
  real customer-looking flows — filter by environment or domain.
- Don't boil the ocean: five well-tuned behaviors beat forty noisy ones; every behavior
  needs an owner, a metric, and a retirement criterion.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Behavioral vs batch conversion lift | +30–50% relative per message | No lift over campaigns |
| Cart recovery rate | 5–15% of abandoned carts | <3% after 90 days |
| Event coverage of priority actions | >90% firing correctly | Core events missing >1 week |
| Real-time trigger latency (event → action) | <30 minutes | Next-day responses to live intent |
| False-positive sales alerts | <10% rejected by sellers | Sales mutes the alert channel |
| Playbook review cadence | Quarterly | Behaviors unreviewed after 12 months |

## Handoffs

- → **trigger-setup:** hand validated events + thresholds to wire as workflow entries.
- → **lead-scoring:** request behavior-point weights and confirm score bumps land.
- → **nurturing-sequences:** supply behavior-referenced personalization (cart items,
  feature names) for flow copy.
- → **web-analytics-agent:** keep the event schema identical across GA4 and the platform.
- ↑ **marketing-automation-agent:** escalate when high-intent programs need new data
  infrastructure or when personalization raises privacy concerns.
