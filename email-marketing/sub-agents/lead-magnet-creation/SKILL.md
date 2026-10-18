---
name: email-lead-magnet-creation
description: Conceives, scores, and produces the incentives that trade real value for an email address — checklists, templates, calculators, quizzes, webinars, discount codes, and gated content — plus the delivery and follow-up wiring. Use this skill whenever the user wants a lead magnet, opt-in incentive, freebie, gated download, email course, quiz funnel, or says "our sign-up offer isn't converting" — even if they never use the phrase "lead magnet" explicitly.
---

# Lead Magnet Creation — Email Marketing Sub-Agent

## Role & Mission

Design the promise that makes a stranger hand over their email address — then make sure the
promise is kept instantly and leads somewhere commercially useful. The outcome this agent is
accountable for: an incentive with high perceived value, near-zero marginal fulfillment cost,
and demonstrable downstream quality (subscribers who open, click, and buy). Weak magnets
produce weak lists; mismatched magnets produce unsubscribes; overbuilt magnets burn
production budget on assets nobody downloads.

## When to Use

- "What should we offer people to join our list?" or opt-in rates lag with no offer at all
- Launching a new product, audience, or funnel that needs its own capture incentive
- An existing lead magnet underperforms on downloads or on downstream engagement
- Repurposing existing content (webinar, research, templates) into a gated asset
- Building a quiz, assessment, or calculator funnel
- Refreshing a stale magnet that has been live more than 12 months

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Audience pain points and jobs-to-be-done | Yes | Sales calls, support tickets, keyword research |
| Existing content assets to repurpose | Preferred | Webinars, reports, internal templates, docs |
| Product/service map | Yes | What the magnet should logically lead into |
| Competitor opt-in offers | Optional | 3–5 rivals' current gated offers |
| Brand voice and visual kit | Preferred | For consistent production |
| Fulfillment cost ceiling | Preferred | "No more than 3 days of design time" |
| Delivery mechanism | Yes | ESP automation, course platform, quiz tool |

## Output Contract

Return a lead-magnet brief: (1) a scored concept matrix, (2) a full production brief for the
winner (outline, format, length, delivery, CTA ladder), (3) the landing-page value proposition,
(4) the instant-delivery and follow-up wiring, (5) success metrics. Core scoring table format:

```markdown
| Concept | Format | Audience fit (1–5) | Perceived value (1–5) | Effort (1–5, lower=better) | Path to product | Score |
|---|---|---|---|---|---|---|
| "SaaS Pricing Page Teardown Checklist" | 4-page PDF + Google Sheet | 5 | 4 | 2 | Priced demo | 4.6 |
| "Email Deliverability Self-Audit" | Interactive quiz (12 questions) | 5 | 4 | 3 | Deliverability service | 4.2 |
| "2026 Marketing Salary Report" | 20-page gated PDF | 3 | 4 | 4 | Generic nurture | 3.1 |
```

## Workflow

1. Mine pain points from four sources: sales-call language, support tickets, keyword and
   "People Also Ask" data, and the top organic pages (demand already proven there).
2. Generate 4–6 concepts across formats — checklist, template, calculator, quiz, email
   course, webinar, discount — deliberately varying effort levels.
3. Score every concept on audience fit, perceived value, production effort, and path to
   product; kill anything that attracts tire-kickers rather than buyers (free-trial-only
   discounts for B2B, "win an iPad" for anyone).
4. Write the production brief for the winner: promise in one sentence, outline, format and
   length, and the instant-gratification rule (usable in under 10 minutes).
5. Produce the asset with the lightest viable format — a sharp 4-page checklist beats a
   flabby 30-page ebook; quality signals include real examples, not filler.
6. Build the delivery path: dedicated landing page with benefit-led headline, instant
   fulfillment email delivering the asset within 60 seconds, and a tagged ESP trigger.
7. Wire the follow-up: the magnet's topic dictates the next 2–3 touchpoints (welcome series
   content, related case study, product bridge) — a magnet with no follow-up is a dead end.
8. QA the full journey as a fresh subscriber: form, confirmation, delivery, links, mobile.
9. Instrument and review: track landing-page conversion, download-to-first-email-open, and
   magnet-source conversion to revenue at 30/60/90 days; schedule a refresh review at 12 months.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| PDF/doc production | Canva, Google Docs/Slides, Figma | Canva free tier suffices for most magnets |
| Quizzes and calculators | Typeform, Tally, Outgrow | Tally has a generous free tier |
| Email courses | ConvertKit (Kit), ActiveCampaign | Drip-by-tag sequence per subscriber |
| Landing page | Unbounce, Instapage, or ESP-native | ESP-native pages are fine to start |
| Demand validation | Google Keyword Planner, AnswerThePublic | Free; confirm search demand exists |
| Webinar delivery | Zoom Webinars, WebinarJam | Higher effort; best for high-ACV B2B |
| Delivery + tracking | ESP automation (Klaviyo, HubSpot) | Tag source magnet on every subscriber |

## Example AI Prompt

```text
You are a lead magnet strategist. Business: {BUSINESS DESCRIPTION}, selling {PRODUCT} to
{AUDIENCE}. Their top pain points: {PAIN LIST}. Existing assets I can repurpose:
{ASSET LIST}. Competitors currently offer: {COMPETITOR OFFERS}. Constraints: {EFFORT
CEILING, e.g. "max 3 days production"}, and the magnet must lead naturally toward
{COMMERCIAL GOAL}.

Deliver:
1. Six lead-magnet concepts across different formats (checklist, template, quiz, calculator,
   email course, webinar) with a one-sentence promise each.
2. A scored matrix: audience fit, perceived value, effort, path to product (1–5 scales).
3. A full production brief for the winner: outline, format, target length, and the
   "usable in 10 minutes" test.
4. Landing page copy: headline, 3 bullet benefits, CTA button text, and a risk-reverser.
5. The follow-up ladder: what the 3 emails after delivery should cover and what they
   should drive the subscriber toward.
Flag any concept that would attract freebie-seekers rather than buyers.
```

## Edge Cases & Guardrails

- The promise-performance gap is the classic failure: a magnet that overdelivers on the
  landing page and underdelivers in the inbox trains the audience to distrust everything
  that follows. Ship the smallest asset that fully keeps the headline's promise.
- Discount-led magnets attract deal-seekers, not buyers — for B2B and services, exchange
  knowledge, not money; save discounts for e-comm cart recovery and post-purchase flows.
- "Gated" does not mean hidden: if the same asset ranks in Google or is published elsewhere,
  the form is friction without justification. Either gate exclusive depth or ungate and use
  content upgrades instead.
- Delivery must be instant and foolproof — every hour between signup and asset delivery
  bleeds confirmation rates and trust. Never deliver magnets as "we'll send it manually."
- Refresh or retire magnets annually: dated statistics, screenshots of old UIs, and stale
  benchmarks quietly convert a 30% landing page into a 12% one.
- Consent still applies: the magnet download is an exchange, not a license to email
  anything, forever — state frequency at signup and honor unsubscribes immediately.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Landing page opt-in rate | 20–40% (quiz formats often 30–50%) | <10% |
| Download-to-first-email-open | 60–80% | <40% (delivery broken or buried) |
| Magnet-sourced unsubscribe at 30 days | <2% | >5% (audience mismatch) |
| Magnet-source conversion to lead/trial/sale in 90 days | 2–5% | 0% after 500+ downloads |
| Production effort per magnet | 1–5 person-days | Multi-week builds with no demand validation |
| Magnet refresh cadence | Every 12 months | Same asset live 2+ years unreviewed |

## Handoffs

- → **list-building:** hand over the finished magnet plus its landing-page value prop so
  capture forms can deploy it across the site.
- → **email-automation:** provide the topic map so the welcome series continues the magnet's
  narrative and bridges to the product.
- → **copywriting:** share the magnet's language (headlines, phrases) — the campaign copy
  that echoes a proven promise lifts CTR.
- → **analytics:** register the magnet as a tracked list source so its downstream revenue
  can be judged, not just its download count.
- ↑ **email-marketing-agent:** escalate when the best-scoring concepts all require
  significant budget (research reports, webinars) — that is a channel-level investment call.
