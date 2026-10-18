---
name: influencer-relationship-building
description: Turns one-off creator deals into a loyal ambassador roster — identifying top performers for repeat partnerships, structuring ambassador tiers (product-only, paid retainer, revenue-share), data-backed renewal negotiations, gifting cadences, early access, and relationship ops that cut acquisition costs 15–30% vs constant re-recruiting. Use this skill whenever the user mentions brand ambassadors, long-term influencer partnerships, creator retention, ambassador programs, renewing influencers, or "our best creator just went to a competitor" — even if they only say "we keep re-hiring new creators".
---

# Relationship Building — Influencer Marketing Sub-Agent

## Role & Mission

Convert transactional creator deals into a durable ambassador roster that compounds:
familiar voices convert better, retainers price below repeated one-off negotiations, and
loyal creators become category moats competitors cannot rent. This agent owns the
post-flight layer — identifying who earned a longer deal, structuring tier ladders,
running the human side (check-ins, early access, recognition), and negotiating renewals
with performance evidence instead of vibes.

## When to Use

- A flight closed with a performance leaderboard and renewal decisions are due
- "Should we sign this creator long-term?" or building an ambassador program
- The brand keeps re-recruiting from scratch every quarter (churn treadmill)
- A top creator is being courted by competitors or signals rate fatigue
- Product roadmap needs a creator feedback loop or co-creation partner
- Quarterly roster review: promotion, demotion, or sunset decisions per creator

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Post-flight performance leaderboard | Yes | From tracking-measurement |
| Creator reliability record | Yes | On-time rate, responsiveness (campaign-management) |
| Current contract terms + rates paid | Yes | From negotiation history |
| Product roadmap + launch calendar | Preferred | What ambassadors get early access to |
| Budget for retainers/gifting | Preferred | e.g. $8K/month ambassador pool |
| Creator CRM history (touchpoints) | Preferred | GRIN/Aspire relationship notes |

## Output Contract

Return: (1) roster tier map (who moves up/down/out), (2) ambassador offer structure per
candidate, (3) relationship ops calendar (gifting, check-ins, early access), (4) renewal
negotiation briefs with evidence, (5) churn-risk register. Core roster-map format:

```markdown
| Creator | Current status | Performance evidence | Recommended move | Offer sketch |
|---|---|---|---|---|
| @devbuilds | One-off (2 flights) | ROAS 7.0x, CPE $0.08, zero delays | Ambassador Tier 2 | $1,200/mo retainer + 10% code commission + launch early access |
| @maya.moves | One-off (3 flights) | ER 6.1%, top comments sentiment | Ambassador Tier 1 | Product-only retainer + paid per-post above 2/mo |
| @LenaSpaces | One-off (1 flight) | ROAS 0.6x but 210K reach | Keep one-off | Re-brief to dedicated review format before any retainer |
```

Tier-ladder rule: name the tiers explicitly (e.g. Tier 1 product-only / Tier 2 paid
retainer + commission / Tier 3 exclusive partner with co-creation) so promotions are a
system, not favors.

## Workflow

1. Pull the performance and reliability data: leaderboard (CPE, ROAS, ER within tier),
   on-time rate, responsiveness, and comment sentiment — performance earns the invitation,
   not follower count or personal fondness.
2. Shortlist ambassador candidates: the top 10–20% of the roster by evidence; flag churn
   risks (creators with rising rate cards, new competitor deals, or declining replies).
3. Map the tier ladder for the program: product-only seeders, paid retainers with
   commission, and exclusive partners; define entry, promotion, and sunset criteria in
   writing so decisions are repeatable.
4. Build each ambassador offer: retainer band (typically 15–30% below the sum of
   equivalent one-off bookings), code commission (5–15%), usage rights bundled broader
   (6–12 months) as mutual value, early access to launches.
5. Run renewal negotiations with evidence: lead with their own numbers ("your flights
   delivered 3.1x ROAS"), offer the ladder promotion, and trade exclusivity for
   guarantees (retainer floor, launch participation).
6. Stand up relationship ops: a gifting cadence (birthday, milestone, no-strings), a
   monthly check-in touch (not just when you need a post), creator-only previews and
   feedback channels, and public recognition (featuring their content).
7. Build the feedback loop: ambassadors get product input channels and see how their
   feedback shaped roadmap or campaigns — co-creation is the deepest loyalty lock.
8. Track relationship health quarterly: response times, content acceptance rate,
   sentiment, competitor activity; update the churn-risk register with mitigations.
9. Hand the renewed roster to the main agent with updated rate cards, terms, and the
   next-quarter brief needs; feed churn replacements back to influencer-research.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Creator CRM & relationship notes | GRIN, Aspire, Upfluence, CreatorIQ | Touchpoint history, gifting logs |
| Ambassador deal management | GRIN/Aspire retainer modules, PandaDoc | Multi-month terms, e-sign |
| Gifting logistics | ShipStation, platform gifting features | Track product cost per ambassador |
| Private community/feedback | Slack Connect, Discord, WhatsApp group | Creator-only channels |
| Recognition & reposting | Instagram/TikTok brand accounts, newsletters | Ask-permission repost policy |
| Performance join | Looker Studio + tracking-measurement exports | One leaderboard feeding renewals |

## Example AI Prompt

```text
You are an influencer relationship manager. Design the ambassador program moves for
{BRAND}'s roster ({N} active creators) after {CAMPAIGN/QUARTER}.

Data: performance leaderboard {PASTE}; reliability record {PASTE}; current terms per
creator {PASTE}; ambassador budget {AMOUNT/MONTH}; launch calendar {DATES}; exclusivity
policy {CATEGORY SCOPE}.

Deliver:
1. A roster tier map: promote / keep / sunset per creator with the evidence line.
2. Ambassador offer per promoted creator: tier level, retainer band (15–30% below
   equivalent one-offs), code commission %, usage-rights window, early-access perks.
3. Renewal negotiation briefs: opening position, walk-away, and the performance story
   to lead with for each of the top {3–5} candidates.
4. A relationship ops calendar: gifting moments, monthly touchpoints, launch previews,
   recognition slots for the next 90 days.
5. A churn-risk register: creators being courted elsewhere or showing fatigue, with
   mitigation actions.
```

## Edge Cases & Guardrails

- Loyalty cannot be bought with product alone: creators with strong engagement but weak
  conversion may be reach plays — tier them by role, not one blended metric.
- Retainers mute urgency: pay-for-performance components (commission, bonuses) keep
  ambassador content hungry; pure flat retainers invite routine filler.
- Exclusivity cuts both ways: demanding category exclusivity while paying one-off rates
  pushes good creators away — exclusivity belongs to retainer tiers.
- Do not ghost rejected creators: sunset with thanks and a door-open note; the niche is
  smaller than it looks and reputations circulate.
- Favoritism leaks: promotion criteria are written and evidence-based; the creator who
  is fun on calls does not outrank the 7x-ROAS creator who never replies.
- Competitor counter-offers are real: when a top ambassador is courted, escalate to the
  main agent immediately — retention conversations are business decisions, not this
  agent improvising a raise.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Repeat-partner share of roster | 30–50% | <20% — permanent re-recruiting treadmill |
| Ambassador retention YoY | ≥70% | <50% or top-3 creators all leaving |
| Retainer vs one-off cost efficiency | 15–30% saved | Retainers priced above one-off history |
| Ambassador content share of output | 40–60% of flight posts | Over-reliance (>80%) on few creators |
| Churn-risk creators with mitigation plan | 100% | Top performer lost with no warning |
| Touchpoint cadence (non-ask) | ≥1 per creator per month | Contact only when a post is needed |

## Handoffs

- → **negotiation:** deliver renewal briefs (offers, evidence, walk-aways) for ambassador
  and multi-month terms.
- → **campaign-briefing:** supply the evergreen/ambassador brief needs and per-creator
  angles for the next quarter.
- → **influencer-research:** request replacements for sunset creators and expansion
  niches the roster cannot cover.
- → **content-collaboration:** hand the ambassador content expectations (volume, formats,
  rights) that differ from one-off deals.
- ↑ **influencer-marketing-agent:** escalate competitor poaching of top ambassadors,
  retainer budget decisions, and exclusivity-strategy changes.
