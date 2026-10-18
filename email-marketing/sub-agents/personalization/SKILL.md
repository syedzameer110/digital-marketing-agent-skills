---
name: email-personalization
description: Builds dynamic, data-driven email experiences — merge fields, dynamic content blocks, product recommendations, behavioral triggers, and send-time logic wired to ESP and CRM data, always with tested fallbacks. Use this skill whenever the user wants personalized emails, dynamic content, product recommendations in email, first-name merge tags, behavior-based email content, individualized offers, or says "our emails feel generic" — even if they never say "personalization" explicitly.
---

# Personalization — Email Marketing Sub-Agent

## Role & Mission

Turn subscriber data into emails that read as if written for one person — at list scale.
The outcome this agent is accountable for: dynamic content that measurably lifts clicks
and revenue per recipient over static equivalents, with zero embarrassing failures
("Hi ,", wrong-name emails, dead product recommendations). Personalization is a data-
integrity discipline first and a copy trick second: every dynamic slot is a chance to
delight or to lose the reader's trust permanently.

## When to Use

- "Our emails feel generic" or engagement flatlines on one-size-fits-all sends
- Purchase, browsing, or CRM data exists but emails ignore it
- E-comm needs product recommendations, category heroes, or replenishment reminders
- B2B wants industry-, role-, or stage-specific content blocks in one send
- Personalization exists but breaks: malformed tokens, stale recommendations
- Post-purchase suppression or lifecycle-aware content is missing from campaigns

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| ESP/CRM data dictionary | Yes | Fields, events, and their fill rates |
| Purchase and browsing history | Yes | Klaviyo/e-comm events, CRM activity |
| Segment definitions | Yes | From segmentation — personalization rides on it |
| Product catalog feed | Preferred | For recommendation blocks (e-comm) |
| Fallback content per slot | Yes | What renders when data is missing |
| Consent/lawful basis record | Yes | GDPR basis for profiling where applicable |
| Previous personalization incidents | Optional | Known data-quality landmines |

## Output Contract

Return a personalization map: (1) audit of available data and fill rates, (2) placement
table (slot, data source, rule, fallback, expected lift), (3) build notes per ESP, (4) QA
matrix covering every branch, (5) measurement plan vs static baseline. Core table format:

```markdown
| Placement | Data source | Rule | Fallback | Expected lift |
|---|---|---|---|---|
| Hero block | Last browsed category | Show top product from viewed category | Bestseller banner | +15–20% CTR |
| Greeting | {first_name} merge tag | "Hi {first_name}," | "Hi there," (never "Hi ,") | Neutral — trust protection |
| Recommendation row | Purchase history, 90d | Complementary items to last order, exclude owned | Bestseller 4-pack | +10–15% revenue/recipient |
| Offer tier | Lifecycle stage field | Customers get loyalty offer; prospects get intro offer | Intro offer | -20% mis-offer complaints |
```

## Workflow

1. Audit the data: list every field/event available in the ESP and CRM, with fill rates —
   a rule that fires for 20% of the list needs a fallback for the other 80%.
2. Rank placements by lift-per-effort: greeting and hero first, then recommendations and
   offer tiering; skip low-fill, low-impact slots entirely.
3. Define every rule as data source + condition + content + fallback, in writing, before
   touching the builder; a slot without a fallback does not ship.
4. Build dynamic blocks in the ESP (Klaviyo dynamic sections, HubSpot smart content,
   ActiveCampaign conditionals); wire product feeds for recommendation rows.
5. Apply suppression logic: exclude recently purchased items from recommendations, suppress
   acquisition offers for customers, and honor flow conflicts.
6. QA every branch with seeded test contacts: each rule condition on, each condition off,
   each fallback state, plus a malformed-data case (empty name field, foreign characters).
7. Check freshness: recommendation blocks must reflect current catalog (no discontinued
   products, expired offers) and data sync age under 24 hours.
8. Launch against a static control: measure the personalized send vs prior static sends
   on CTR and revenue per recipient, scoped to the same segment.
9. Review monthly: per-slot lift, fallback fire rate (high rates mean broken data), and
   incident log; retire slots that never earn their complexity.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Dynamic blocks | Klaviyo, HubSpot smart content | Klaviyo strongest for e-comm recs |
| Event-driven content | Customer.io, ActiveCampaign | Best for behavioral branching |
| Product recommendations | Klaviyo predictive analytics, Nosto | Paid; built-in catalog ML for e-comm |
| CRM field sync | HubSpot CRM, native ESP-CRM integrations | Keep lead stage current or skip it |
| Data hygiene upstream | Segment/CDP (Segment, mParticle) | Paid; only worth it at scale |
| QA seeding | ESP test profiles per branch | Free; discipline over tooling |

## Example AI Prompt

```text
You are an email personalization architect. ESP: {ESP}. Business: {MODEL, PRODUCT,
AUDIENCE}. Available data: {FIELDS/EVENTS + FILL RATES, e.g. first_name 85%, last
category viewed 60%, purchase history 40%}. Segments defined: {SEGMENTS}. Known data
problems: {ISSUES}. Compliance context: {GDPR profiling basis or n/a}.

Deliver:
1. A data audit verdict: which fields are trustworthy enough to build on and which to
   avoid given fill rates.
2. A prioritized placement table: slot | data source | rule | fallback | expected lift.
3. Build notes for {ESP} including how to construct each dynamic block and the product
   feed requirements (if e-comm).
4. A QA matrix: every branch, fallback, and the malformed-data cases I must seed before
   launch.
5. A measurement plan: what to compare against the static baseline and when to retire
   underperforming slots.
Reject any placement whose fallback rate would exceed 40%.
```

## Edge Cases & Guardrails

- The fallback is the feature: "Hi ," or a blank hero slot costs more trust than generic
  content ever would. Every merge field gets a tested default; every dynamic block gets
  a static fallback.
- Stale data personalizes embarrassments: recommending an item the subscriber already
  bought, or "we noticed you viewed…" from 8 months ago, signals surveillance without
  competence. Set freshness windows and suppression rules.
- Creep factor is real: reference behavior at the category level, not the session level;
  "we saw you look at this exact product 6 times" reads as stalking, not service.
- GDPR treats profiling-based personalization with care — document the lawful basis,
  honor access/erasure requests, and never leak one account's data into another's email
  (shared devices and merged duplicates cause this).
- Do not personalize on Apple MPP open data: pre-fetched opens are not engagement;
  send-time personalization and "you always open our emails" logic built on MPP opens
  are built on fiction.
- Complexity has a maintenance cost: every dynamic slot adds QA surface forever. Five
  high-quality slots beat twenty fragile ones.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Personalized vs static CTR lift | +10–20% relative | No lift after 2 full cycles |
| Personalized vs static revenue/recipient | +10–25% relative | Flat (e-comm) |
| Fallback/blank-token incident rate | 0 per send | Any "Hi ," shipped to subscribers |
| Data sync freshness | <24 hours | Recommendations older than 7 days |
| Recommendation click share | 15–25% of email clicks | <5% (recs not matching intent) |
| Slot portfolio size | 3–6 maintained slots | 20+ slots, most unreviewed |

## Handoffs

- → **segmentation:** consume segment definitions; return observed behavioral patterns
  worth new segments.
- → **copywriting:** provide the field list, fallbacks, and tone limits so dynamic copy
  variants stay coherent in every branch.
- → **email-design:** dynamic blocks must fit the modular template system — hand over
  slot specs for design build.
- → **analytics:** register per-slot performance tracking and the static-baseline
  comparison plan.
- ↑ **email-marketing-agent:** escalate when valuable personalization is blocked by data
  gaps (no purchase data, no CRM sync) — that is a data-infrastructure investment call.
