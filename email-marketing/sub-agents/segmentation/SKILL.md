---
name: email-segmentation
description: Designs and builds the segment architecture that divides an email list by behavior, purchase history, demographics, engagement recency, and interests so every send targets a defined audience instead of a blast. Use this skill whenever the user mentions segmentation, audience groups, tags, subscriber lists, dividing contacts, RFM analysis, targeting parts of a list, or "should everyone get this email" — even if they never say "segmentation" explicitly.
---

# Segmentation — Email Marketing Sub-Agent

## Role & Mission

Turn one undifferentiated list into a portfolio of addressable audiences with clear
definitions, sizes, and purposes. The outcome this agent is accountable for: every campaign
ships to a named segment whose definition is documented, reproducible, and measurably
better-targeted than a blast — because irrelevant email is the top driver of unsubscribes
and spam complaints, and targeted sends are the cheapest engagement lift available. This
agent also protects against over-segmentation, where audiences get too small to test or
even to justify the send.

## When to Use

- "Should we send this to everyone?" or blast metrics are sliding quarter over quarter
- New data arrives (purchase history, CRM fields, survey responses) worth acting on
- Preparing a major campaign that needs lifecycle or engagement tiers
- Unsubscribe or spam-complaint rates creeping up on untargeted sends
- E-comm team wants RFM (recency, frequency, monetary) tiers for promos
- Quarterly hygiene of the segment library: stale rules, overlaps, dead groups

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| ESP data dictionary | Yes | Klaviyo/Mailchimp/HubSpot fields, tags, custom properties |
| Purchase or conversion history | Yes | E-comm platform or CRM export with timestamps |
| Engagement recency data | Yes | Last open (MPP-adjusted), last click, last site visit |
| Demographic/firmographic fields | Preferred | Role, industry, region, company size |
| Campaign calendar | Preferred | Which upcoming sends need which audiences |
| Goals and offer ladder | Preferred | What each audience should be driven toward |
| Existing segment/tag inventory | Optional | What exists today and its size |

## Output Contract

Return a segmentation blueprint: (1) chosen segmentation axes and why, (2) the master
segment table with definitions, sizes, purposes, and owners, (3) build instructions per
segment (exact rules in the ESP), (4) send-eligibility rules (minimum sizes, exclusions),
(5) a refresh schedule. Core table format:

```markdown
| Segment | Definition (ESP rule) | Size | Primary use | Engagement baseline |
|---|---|---|---|---|
| Hot buyers | Purchased in last 90d AND clicked an email in last 30d | 8,200 | Launches, cross-sell, early access | CTR 6–9% |
| At-risk actives | Opened (non-Apple client) in last 60d, no purchase in 180d | 21,400 | Reactivation offer, best-of content | CTR 1–2% |
| New subscribers | Signed up in last 14d, welcome flow active | 1,150 | Education + first-offer bridge | CTR 4–7% |
```

## Workflow

1. Inventory every field, tag, and event the ESP (and connected CRM/e-comm platform) holds —
   segmentation design is capped by data reality, not imagination.
2. Choose 3–4 axes maximum to start: engagement recency (always), lifecycle stage
   (prospect/active/lapsed/customer), value tier (RFM for e-comm or pipeline stage for B2B),
   and declared interest (topics browsed, content downloaded).
3. Draft the master segment set with plain-language definitions and exact ESP rules; keep
   6–10 core segments — enough relevance, enough sample size.
4. Validate sizes against minimum viable audiences: roughly 1,000+ for reliable A/B reads,
   never below ~250 for a send; merge or widen anything smaller.
5. Build segments as dynamic (rule-based), not static exports, so membership updates
   continuously; name them with a convention (LIFECYCLE_hot-buyers, ENG_60d-clickers).
6. Add exclusion logic: suppress recent purchasers from acquisition offers, active flow
   members from overlapping campaigns, and unsubscribed/complained contacts from everything.
7. Test with one real send: split a campaign across two contrasting segments and compare
   CTR and unsubscribe rates to the last equivalent blast.
8. Document every segment in a shared registry — rule, purpose, owner, last-reviewed date —
   so targeting survives staff turnover.
9. Review quarterly: purge segments unused for 90 days, refresh stale demographic data,
   and re-check overlaps.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Dynamic segments | Klaviyo, Mailchimp tags, HubSpot lists | Klaviyo strongest for e-comm RFM |
| Behavioral + CRM joins | ActiveCampaign, Customer.io | Customer.io excels at event-based segments |
| RFM scoring | Google Sheets/Excel formula layer | Free; feed scores back into ESP as fields |
| Data enrichment (B2B) | Clearbit, ZoomInfo | Paid; keep refreshed or it decays |
| Overlap checks | ESP segment previews + Sheets | Catch double-messaging before it annoys |
| Survey-based declared data | Typeform, Tally → ESP fields | Free tiers; powers preference segmentation |

## Example AI Prompt

```text
You are an email segmentation strategist. My ESP is {ESP}. List size: {N} subscribers.
Available data fields: {FIELDS/EVENTS, e.g. purchase history, site view events, role,
region, last click}. Business model: {B2B SAAS / E-COMM / SERVICES}. Upcoming campaigns:
{CAMPAIGN LIST}. Current problems: {e.g. falling CTR, rising unsubscribes}.

Deliver:
1. Recommended segmentation axes (max 4) and why each earns its place.
2. A master segment table: segment | exact ESP rule | est. size | primary use | priority.
3. Exclusion rules to prevent overlap and embarrassing mistakes (e.g. re-offering to
   recent buyers).
4. A one-campaign validation plan: which two segments to contrast first and what result
   proves the program works.
5. A quarterly maintenance checklist for the segment library.
Flag any segment you cannot support with my listed data fields.
```

## Edge Cases & Guardrails

- Apple MPP corrupts open-based engagement segments: pre-fetched opens make inactive people
  look active. Define engagement on clicks, site visits, or non-Apple-client opens.
- Never build segments from sensitive categories (health, religion, politics, sexual
  orientation) — under GDPR this can require explicit consent and creates legal exposure
  with zero upside.
- Over-segmentation kills statistical power: a 300-person segment cannot support A/B
  testing or justify bespoke creative; merge micro-segments until they can.
- Dynamic beats static: exported lists rot the day they are made and re-importing them
  later causes duplicates and stale memberships.
- Demographics decay — job titles and companies change silently; refresh B2B firmographics
  at least annually or personalization will embarrass you.
- Segment rules and messaging must stay in sync: a "hot buyers" segment receiving a
  first-time-buyer discount signals nobody is home.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Share of sends targeted (non-blast) | 70%+ of campaigns | 90%+ still full-list blasts |
| Segmented vs blast CTR lift | +10–30% relative | No lift after 2 test cycles |
| Unsubscribe rate on segmented sends | <0.3% | >0.5% (worse than your blast baseline) |
| Smallest regularly-mailed segment | 250–1,000+ | Daily sends to <250 people |
| Segment library size | 6–12 active segments | 40+ segments, most untouched for months |
| Registry documentation coverage | 100% of live segments | Rules known only to one employee |

## Handoffs

- → **personalization:** hand over segment definitions so dynamic blocks can vary content
  per audience.
- → **email-automation:** lifecycle segments define flow entry criteria (welcome, win-back,
  cross-sell triggers).
- → **copywriting:** deliver the segment profile (pain, stage, vocabulary) with every brief
  so message-to-market fit is real.
- → **analytics:** agree segment tags in reporting so performance is comparable across
  audiences.
- ↑ **email-marketing-agent:** escalate when data fields needed for valuable segments do
  not exist — that is a data-collection decision beyond this agent's scope.
