---
name: email-email-automation
description: Builds the triggered email flows that run without a human pressing send — welcome series, drip campaigns, abandoned cart, browse abandon, post-purchase, re-engagement, and win-back sequences with entry/exit rules and conflict handling. Use this skill whenever the user wants a welcome series, drip campaign, automated sequence, lifecycle emails, abandoned-cart emails, nurture flow, onboarding emails, or asks "what should happen when someone subscribes" — even if they never say "email automation" explicitly.
---

# Email Automation — Email Marketing Sub-Agent

## Role & Mission

Design, build, and maintain the always-on email machine: triggered flows that convert and
retain subscribers 24/7 without campaign labor. The outcome this agent is accountable for:
an automation portfolio that reliably generates 25–40% of email revenue (or the B2B
equivalent — accelerated pipeline) and degrades gracefully instead of embarrassing the
brand. Automations out-earn campaigns because they fire at peak intent — the moment someone
subscribes, abandons a cart, or goes quiet — and every month without them is revenue
permanently forfeited.

## When to Use

- "We need a welcome series" or new subscribers currently get nothing (or one blast)
- E-comm store lacks abandoned-cart, browse-abandon, or post-purchase flows
- B2B pipeline needs drip nurture sequences by stage or persona
- Re-engaging lapsed subscribers before a list-hygiene cull
- Flows exist but nobody has audited timing, conflicts, or exit conditions in months
- Migrating ESPs and the automation library must be rebuilt correctly

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Customer journey map with trigger points | Yes | Subscribe, first visit, cart, purchase, lapse |
| ESP automation builder access | Yes | Klaviyo, ActiveCampaign, HubSpot, Customer.io |
| Brand voice and content assets | Yes | From copywriting; case studies, help docs |
| Offer ladder | Yes | Lead magnet → trial → demo, or first-order discount |
| Purchase/site-event data streams | Preferred | Klaviyo/e-comm events, product catalog feed |
| Suppression and consent rules | Yes | Who must never enter which flow |
| Existing flow inventory | Optional | What runs today, entry counts, revenue |

## Output Contract

Return a flow blueprint: (1) prioritized flow backlog with rationale, (2) per-flow sequence
table (emails, delays, goals, CTAs, metric targets), (3) entry/exit/conflict rules, (4)
build checklist per ESP, (5) launch-QA script. Core sequence table format:

```markdown
| # | Email | Delay | Goal | Primary CTA | Target metric |
|---|---|---|---|---|---|
| 1 | Welcome + deliver magnet | Immediate (<=60s) | Deliver promise, set expectations | Download the guide | Open 55%+, click 15%+ |
| 2 | Story + proof | Day 2 | Build trust, show relevance | Read the case study | Open 35%+ |
| 3 | Objection-crusher + soft offer | Day 4 | Convert intent to action | Book a demo | Click 8%+ |
```

## Workflow

1. Map the journey and list every triggerable moment; prioritize flows by revenue impact:
   welcome series first, then abandoned cart (e-comm), then post-purchase, browse abandon,
   win-back, and date-based flows.
2. Define each flow's single job and KPI — a welcome flow onboards, a cart flow recovers;
   flows that try to do both do neither.
3. Draft the sequence: 3–5 emails per flow, explicit delays, and a value-before-ask cadence
   (deliver, teach, prove, then sell).
4. Set entry and exit rules before building: who qualifies, who is excluded (purchasers exit
   cart flow), and how the flow interacts with sibling flows (one email per day cap,
   priority order).
5. Build in the ESP using dynamic content and merge fields; wire event triggers (cart value,
   viewed product, plan stage) where the platform supports them.
6. Load copy and a responsive template from email-design; keep each email single-CTA.
7. QA every path with test contacts: trigger each email state (subscriber with/without
   purchase history, guest checkout, existing-customer cart), check links, personalization
   fallbacks, and unsubscribe placement on every message.
8. Launch at low volume, verify event firing and timing in the first 48 hours, then release
   to full traffic.
9. Review monthly: per-email contribution, drop-off points, stale content; schedule
   quarterly deep audits and refresh subject lines through ab-testing.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| E-comm lifecycle flows | Klaviyo | Category leader; deep Shopify/BigCommerce events |
| B2B nurture and lead scoring | HubSpot, ActiveCampaign | Native CRM joins; ActiveCampaign from ~$29/mo |
| Event-driven developer flows | Customer.io | Best-in-class API triggers and branching |
| SMB all-rounder | Brevo, Mailchimp Customer Journeys | Brevo free tier; generous send limits |
| Flow diagramming (pre-build) | Miro, Google Drawings | Free; agree logic before clicking build |
| QA and previews | Litmus, ESP test sends | Litmus from ~$99/mo; render-check every branch |

## Example AI Prompt

```text
You are an email automation architect. Business: {BUSINESS MODEL}, selling {PRODUCT} to
{AUDIENCE}. ESP: {ESP + available events/fields}. Journey triggers available:
{TRIGGER LIST}. Offer ladder: {OFFER LADDER}. Constraints: {e.g. max 4 emails in welcome,
compliance = GDPR}.

Deliver:
1. A prioritized flow backlog (welcome, abandoned cart, post-purchase, win-back, etc.)
   with expected revenue contribution logic for my model.
2. For the {PRIORITY FLOW}: a full sequence table — email #, delay, goal, primary CTA,
   subject-line direction, and target open/click (noting Apple MPP makes open targets
   directional only).
3. Entry, exit, and conflict rules, including which flows suppress each other and the
   frequency cap.
4. A build checklist specific to {ESP} and a QA script covering the edge paths
   (guest checkout, repeat purchaser, existing subscriber).
5. A monthly review scorecard for the flow.
```

## Edge Cases & Guardrails

- Conflict handling is where automations fail publicly: without exit conditions and a
  frequency cap, one subscriber can receive welcome, cart, and campaign emails in the same
  hour. Define one-email-per-day and flow-priority rules up front.
- Unsubscribe and suppression logic applies to every automated email without exception —
  automated flows are not exempt from CAN-SPAM opt-out handling or GDPR consent.
- Never sell immediately after purchase: suppress acquisition offers for a defined window
  (e-comm: cross-sell after delivery; B2B: onboard before upsell) or churn follows.
- Welcome-series opens of 50–60% decay hard after email 2–3; front-load value and judge
  flows by clicks and conversions, never opens (Apple MPP inflates them).
- Test every trigger path, especially the weird ones: guest checkouts, subscribers who buy
  before finishing welcome, repeat cart-abandoners. Unhandled branches send nonsense.
- Stale automation is a slow-motion brand accident — expired offers and dead links in
  flows keep sending for months; date-stamp every flow with a next-review date.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Automation share of email revenue | 25–40% (e-comm) | <10% after 90 days of flows live |
| Welcome email 1 open rate | 50–60% (MPP-inflated) | <30% |
| Abandoned-cart recovery rate | 6–12% of abandoned carts | <3% across 3+ email series |
| Flow completion / drop-off | <40% drop after email 1 | 80% vanish by email 2 (content gap) |
| Flows with entry/exit rules documented | 100% | Any flow with undefined conflict behavior |
| Flow content freshness review | Quarterly | No audit in 12+ months |

## Handoffs

- → **copywriting:** brief every sequence email (audience, stage, goal, constraints) and
  receive the copy deck back for build.
- → **email-design:** request flow templates with per-email layout variants (plain-text-feel
  for email 1, product-grid for cart emails).
- → **segmentation:** flow entry rules consume segment definitions; return observed
  behavior segments worth formalizing.
- → **analytics:** register flows as tracked sources so their revenue share is reported
  separately from campaigns.
- ↑ **email-marketing-agent:** escalate when the offer ladder has gaps (nothing to
  automate toward) — flow strategy needs channel-level product decisions.
