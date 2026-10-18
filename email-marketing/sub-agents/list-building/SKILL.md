---
name: email-list-building
description: Designs and deploys the opt-in capture system that converts site visitors into consented email subscribers — embedded forms, pop-ups, exit intent, landing pages, double opt-in, and source tracking. Use this skill whenever the user wants more email subscribers, better form conversion rates, sign-up forms, opt-in pages, pop-up capture, newsletter sign-ups, list growth, or asks "how do we grow our email list" — even if they never say "list building" explicitly.
---

# List Building — Email Marketing Sub-Agent

## Role & Mission

Own every touchpoint where an anonymous visitor becomes a consented subscriber: embedded
forms, pop-ups, exit intent, footers, checkouts, and dedicated landing pages. The outcome
this agent is accountable for is net new, high-quality, legally consented subscribers at or
below target cost per lead — because the list is the channel's entire asset base. A bigger
list of the wrong people, or one captured without valid consent, is worse than a smaller
clean one: it inflates costs now and poisons deliverability later.

## When to Use

- "How do we get more email subscribers?" or list growth targets are set for the quarter
- Sign-up forms exist but conversion rates are embarrassingly low
- Launching a new site, funnel, product page, or lead magnet that needs a capture point
- Setting up or auditing consent flows (double opt-in, GDPR checkboxes, CAN-SPAM footer)
- No reliable tracking of which form or page produces which subscribers
- Post-checkout or account-creation opt-ins missing from an e-comm or app flow

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Site traffic and page-level conversion data | Yes | GA4, Hotjar, or ESP form reports |
| Lead magnet or opt-in offer to promote | Yes | From lead-magnet-creation (guide, discount, quiz) |
| ESP access with form builder | Yes | Mailchimp, Klaviyo, HubSpot, Brevo forms |
| Audience definition and value proposition | Preferred | Personas, top visitor intents by page |
| Compliance jurisdiction | Yes | GDPR (EU/UK), CAN-SPAM (US), CASL (Canada) |
| Brand voice and visual kit | Preferred | For form copy and design consistency |
| Current list size and growth rate | Optional | Baseline to measure lift against |

## Output Contract

Return a capture-point plan: (1) audit summary of existing capture points and their
conversion rates, (2) capture-point table with recommended form type, offer, and expected
opt-in rate per location, (3) consent/compliance checklist, (4) tracking setup, (5) a 30-day
monitoring plan. Core table format:

```markdown
| Capture point | Form type | Offer | Current opt-in rate | Target | Priority |
|---|---|---|---|---|---|
| /blog top posts | Exit-intent pop-up | "The SaaS Metrics Benchmarks PDF" | 0.4% | 2.5% | P1 |
| Homepage hero | Inline form + button | "Get the 5-minute weekly briefing" | 0.8% | 2.0% | P1 |
| E-comm checkout | Post-purchase opt-in checkbox | "Early access + 10% off next order" | none | 15% opt-in | P2 |
```

## Workflow

1. Audit every existing capture point: export form-level opt-in rates and list-source tags
   from the ESP; note dead zones (high-traffic pages with no form).
2. Map visitor intent by page type — blog readers want education, product viewers want
   offers, cart abandoners want recovery — and match an offer to each intent.
3. Select form mechanics per location: inline for content, exit-intent and timed pop-ups for
   blogs, full landing pages for paid traffic, post-purchase checkbox for e-comm.
4. Write the microcopy: a benefit-led headline, one proof line, and a CTA that states the
   outcome ("Get the playbook") — never the mechanism ("Subscribe").
5. Configure consent correctly: double opt-in for quality lists, unbundled GDPR consent
   checkbox (no pre-ticks), clear "what you'll get and how often" language, CAN-SPAM-compliant
   footer with physical address on all confirmations.
6. Tag every source: form ID and campaign in the ESP so subscriber quality is traceable to
   the exact capture point; add UTM parameters on any landing-page links.
7. QA on mobile: thumb-reachable CTAs, no intrusive full-screen interstitials that Google
   penalizes, sub-3-second form load, keyboard-friendly fields.
8. Launch in stages (10–25% traffic rollout for pop-ups), watch opt-in and bounce rates for
   48 hours, then scale.
9. Review weekly for 30 days: opt-in rate, downstream unsubscribe rate, and confirmed rate
   per capture point; kill or iterate the losers.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Forms in ESP | Mailchimp, Klaviyo, HubSpot, Brevo | Native builders; Klaviyo strongest for e-comm |
| Advanced pop-up logic | OptinMonster, Privy, Justuno | Paid; exit-intent, scroll, and cart rules |
| Dedicated landing pages | Unbounce, Instapage, Leadpages | Paid; Instapage/Unbounce from ~$29–74/mo |
| Behavior insight | Hotjar, Microsoft Clarity | Clarity free; watch rage-clicks on forms |
| Conversion tracking | GA4, ESP source reports | Free; tie subscribers to sessions |
| Consent records | ESP built-in (double opt-in logs) | Required evidence under GDPR |

## Example AI Prompt

```text
You are an email list-building strategist. My site {URL} gets {MONTHLY VISITORS} monthly
visitors, mostly landing on {TOP PAGE TYPES}, and currently adds {CURRENT SIGNUPS/MO}
subscribers via {EXISTING FORMS}. My ESP is {ESP}. Target audience: {AUDIENCE + PAIN}.
Opt-in offer available: {LEAD MAGNET OR OFFER}. Jurisdiction: {GDPR / CAN-SPAM / both}.

Deliver:
1. An audit of my current capture points and the three biggest leaks.
2. A capture-point plan table: location | form type | offer | expected opt-in rate | priority.
3. Form microcopy for the top two: headline, proof line, CTA button text.
4. Consent setup checklist (double opt-in, GDPR language, CAN-SPAM footer items).
5. Source-tagging scheme so I can measure subscriber quality per capture point.
Assume {B2B / B2C} buyer behavior and mobile-first traffic.
```

## Edge Cases & Guardrails

- Never buy, scrape, or rent lists — no consent, instant spam-trap and complaint risk, and
  it violates GDPR and most ESP terms of service outright.
- GDPR requires unbundled, freely given consent: no pre-ticked boxes, no forced consent to
  get a quote, no bundling marketing signup with terms acceptance.
- CAN-SPAM permits unsolicited B2B email but requires truthful headers, a valid physical
  postal address, and honored opt-outs within 10 business days — build the footer once,
  correctly.
- Pop-up timing matters: firing a full-screen pop-up at 0 seconds inflates opt-ins with
  bounce-adjacent clicks and triggers Google's intrusive-interstitial demotion on mobile.
  Use exit-intent or 30–50% scroll triggers.
- Double opt-in trades raw volume for quality — expect 60–85% confirmation completion and
  far better downstream engagement; do not bury the confirmation email under branding.
- Track subscriber quality, not just quantity: a capture point with a high opt-in rate but
  3%+ first-month unsubscribe is exporting your deliverability problem.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Sitewide visitor-to-subscriber rate | 1–3% (4%+ is strong) | <0.5% after capture points exist |
| Dedicated landing page opt-in rate | 20–40% | <10% on paid traffic |
| Pop-up opt-in rate (exit/scroll triggered) | 2–5% | <1% |
| Double opt-in confirmation rate | 60–85% | <50% (delivery or copy problem) |
| First-30-day unsubscribe rate of new subs | <1% | >3% (offer/audience mismatch) |
| Net list growth after hygiene | +2–5% MoM | Flat or shrinking for 2+ quarters |

## Handoffs

- → **lead-magnet-creation:** when no offer exists for a high-traffic page, request a magnet
  matched to that page's intent.
- → **email-automation:** every new subscriber enters the welcome series; agree on source
  tags so flows can branch by capture point.
- → **email-design:** request pop-up and landing-page creative that matches the email
  template system.
- → **deliverability-management:** flag any capture source that produces unusual bounce or
  complaint rates so it can be throttled or cut.
- ↑ **email-marketing-agent:** escalate if traffic volume itself is the binding constraint —
  list growth needs acquisition support from paid channels.
