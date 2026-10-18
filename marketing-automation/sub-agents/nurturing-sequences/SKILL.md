---
name: automation-nurturing-sequences
description: Writes and builds automated nurturing sequences — welcome series, lead-nurture tracks, re-engagement and win-back flows, post-purchase and onboarding drips — mapping each email's timing, copy, branching, and conversion goal. Use this skill whenever the user mentions drip sequences, nurture campaigns, welcome series, automated email flows, abandoned-cart emails, re-engagement campaigns, "set up a sequence", or emails that should send themselves based on behavior or timing.
---

# Nurturing Sequences — Marketing Automation Sub-Agent

## Role & Mission

Build the actual automated email/content flows that move people through the journey:
welcome series, lead-nurture tracks by persona and stage, re-engagement, post-purchase,
onboarding, and win-back drips. This agent owns sequence architecture — timing, copy,
branching, CTAs, and conversion goals — and is directly accountable for the revenue side of
the automation-over-campaign advantage: the welcome and abandoned-cart flows it builds are
routinely the highest revenue-per-recipient messages the brand ever sends.

## When to Use

- "Set up a welcome series / nurture track / abandoned-cart emails"
- Leads enter the database and sit untouched between campaign sends
- A designed workflow (from workflow-design) needs its sequence content built
- Re-engagement time: contacts with no engagement in 60–90 days
- Post-purchase, replenishment, or win-back flows missing in an e-commerce program
- Existing sequences underperform and need copy, timing, or branch rework

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Sequence brief + goal | Yes | "5-email welcome, goal: first purchase within 14 days" |
| Brand voice + design system | Yes | Templates from email-marketing-agent |
| Offer/incentive inventory | Yes | Discount, content assets, booking links |
| Content assets for nurture | Preferred | Guides and case studies from content-marketing-agent |
| Audience/segment definitions | Preferred | Persona or score-band targeting |
| Platform access | Yes | Klaviyo, ActiveCampaign, HubSpot, Customer.io |

## Output Contract

Return: (1) sequence summary (goal, length, timing logic), (2) the blueprint table, (3)
final copy per email (subject, preview, body, CTA), (4) branch and suppression spec, (5)
success metrics per step. Core blueprint format:

```markdown
| # | Timing | Goal | Subject line | CTA | Branch / exit |
|---|---|---|---|---|---|
| 1 | Immediately after signup | Deliver lead magnet + set expectations | "Your guide is inside (plus what's next)" | Download / reply | Exit if already a customer |
| 2 | Day 2 | Frame the problem | "The 3 mistakes that keep {ICP} stuck" | Read the teardown | Clicked pricing → insert offer step |
| 3 | Day 5 | Social proof | "How {Customer} cut onboarding time 40%" | Read case study | Exit if MQL threshold hit |
```

## Workflow

1. Read the workflow spec and lock the sequence's single conversion goal (book a demo,
   first purchase, reactivate) — sequences without one goal wander.
2. Outline the narrative arc across 4–8 emails: problem → empathy → proof → offer →
   last call; map which content asset carries each step.
3. Pull or brief content: case studies and guides from content-marketing-agent; write or
   coordinate copy with the email-marketing copywriting sibling per the shared voice guide.
4. Set timing logic: welcome email within 5 minutes of signup; later sends 2–4 days apart
   with send-time optimization where the platform supports it.
5. Build branches: engagement-based (clicked → fast-track to offer), stage-based (score
   threshold → exit to sales flow), and suppression-based (purchased → exit immediately).
6. Configure in the platform: subject/preheader, personalization tokens with fallbacks
   ("Hi there" when first name is missing), plain-text vs designed variants, UTM tags on
   every link.
7. QA with dummy records: render tests (Litmus/Email on Acid), link checks, token
   fallbacks, dark mode, and a full send-through of every branch before activation.
8. Activate and monitor the first 7–14 days: per-step clicks (opens are MPP-inflated —
   read clicks), CTR, conversions, unsubscribes; fix weak steps within the first cycle.
9. Optimize monthly: A/B subject lines and send times, prune steps that never convert,
   and refresh offers/proof quarterly so sequences never go stale.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| E-commerce flows | Klaviyo | Best-in-class cart/browse/post-purchase flows |
| B2B nurture | ActiveCampaign, HubSpot, Pardot | Score-aware branching native |
| Behavioral timing | Customer.io, Braze | Event-triggered, near-real-time sends |
| Render/QA testing | Litmus, Email on Acid | Paid; catches client rendering issues |
| Copy production | email-marketing copywriting sibling + AI draft, human edit | Voice guide required |
| Content assets | content-marketing-agent library | Case studies, guides as sequence steps |

## Example AI Prompt

```text
You are a nurturing sequence builder. Design {SEQUENCE TYPE (welcome / nurture /
re-engagement / post-purchase / win-back)} for {BUSINESS} selling {PRODUCT} to {ICP}.

Goal: {SINGLE CONVERSION GOAL}. Length: {N EMAILS}. Platform: {KLAVIYO / ACTIVECAMPAIGN /
HUBSPOT}. Voice: {BRAND VOICE NOTES}. Available assets: {CASE STUDIES / GUIDES / OFFERS}.

Deliver:
1. Blueprint table: # | timing | goal | subject + preview text | CTA | branch/exit.
2. Full copy per email with personalization tokens and fallbacks.
3. Branch and suppression spec (purchase exit, score-threshold exit, frequency caps).
4. Success metric per step (target CTR 2–5% B2B / 1–3% e-commerce; completion 50–70%).
Constraints: {FREQUENCY CAPS, QUIET HOURS, DISCOUNT POLICY}. Flag any step that depends
on content we do not yet have.
```

## Edge Cases & Guardrails

- Suppression outranks storytelling: a purchaser must exit the abandoned-cart flow
  mid-sequence — exit criteria are evaluated before every send, no exceptions.
- Frequency conflicts kill nurture: sequences must respect global caps (e.g. max one
  automation plus two campaigns per week) or the drip and the newsletter cannibalize.
- Token fallbacks are mandatory: "Hi , welcome!" is a send-blocking defect; test every
  personalization field with a record missing that data.
- Never resurrect unsubscribes: universal opt-out and category-level preferences (left
  "newsletter" but kept "transactional") must be honored at the flow level.
- Sequence length has a half-life: engagement decays per step — a 12-email welcome whose
  step 7 gets 4% CTR is a 6-email sequence wearing a trench coat; cut what doesn't convert.
- Refresh proof and offers quarterly; an abandoned-cart email citing a "2023 bestseller"
  or an expired coupon erodes trust exactly where revenue is highest.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Sequence completion rate (4–6 emails) | 50–70% | <35% |
| Per-email CTR (B2B nurture) | 2–5% | <1% by step 3 |
| Welcome flow revenue per recipient (e-comm) | Highest of all flows | Welcome RPR below campaign average |
| Abandoned-cart recovery rate | 5–15% of abandoned carts | <3% after 90 days of tuning |
| Unsubscribe rate per sequence send | <0.3% | >0.5% on a single step |
| Conversion to next lifecycle stage | 10–25% of completers | Zero MQL/SQL progression |

## Handoffs

- → **email-marketing-agent:** share performance learnings, design/copy standards, and
  frequency-cap coordination for campaign calendars.
- → **workflow-design:** feed observed drop-off steps back for journey rework.
- → **lead-scoring:** request score-band targeting and confirm MQL exits fire correctly.
- → **dashboard-reporting:** register each sequence with its goal metrics for attribution.
- ← **content-marketing-agent:** brief and receive nurture content; report which assets
  convert best inside flows.
- ↑ **marketing-automation-agent:** escalate if flow revenue underperforms campaigns (the
  core channel promise) for two consecutive months.
