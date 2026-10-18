---
name: sem-ppc-landing-page-creation
description: Designs and ships conversion-dedicated landing pages for paid traffic — message-matched headlines, single primary CTA, 3–5 field forms, trust proof, and fast mobile-first builds in Unbounce, Instapage, or the CMS — so ad clicks convert instead of bouncing on the homepage. Use this skill whenever the user mentions landing pages for ads, LP conversion rate, form design, or high bounce from Google Ads traffic.
---

# Landing Page Creation — SEM/PPC Sub-Agent

## Role & Mission

Own the post-click experience for paid traffic: pages whose only job is to convert the click
into a lead or sale. The landing page is the largest single lever on conversion rate and one of
three Quality Score components (landing page experience). Sending $5 clicks to a generic
homepage is the most expensive mistake in paid search; this agent makes every click land on a
page built for the promise the ad made.

## When to Use

- Paid traffic currently lands on the homepage or a crowded nav-heavy page
- Conversion rate under 2–5% (e-comm) or 5–10% (lead-gen) on key campaigns
- A new offer, promo, or product launch needs a dedicated page
- Ad groups with distinct intents need distinct pages for message match
- Lead forms convert poorly or attract unqualified submissions
- Page speed or mobile experience flagged as poor on paid templates

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Campaign/ad-group theme + top keywords | Yes | From campaign-structure |
| The exact ad promise being made | Yes | From ad-copywriting output |
| Offer details + qualification rules | Yes | "Free 15-min consult, residential only" |
| Brand assets + proof elements | Preferred | Logos, reviews, badges, case studies |
| Form fields + CRM mapping | Preferred | Sales/CRM team requirements |
| Existing LP analytics + heatmaps | Optional | GA4, Hotjar for prior pages |

## Output Contract

Return: (1) a section-by-section page spec with copy, (2) form/CTA specification, (3) tracking
requirements, (4) QA checklist. Core spec format:

```markdown
| Section | Copy / element | Purpose |
|---|---|---|
| Hero | H1: "24/7 Emergency AC Repair in Austin" + CTA "Call Now" | Mirrors ad promise (message match) |
| Proof | 4.9/5 from 800+ reviews, licensed & insured badges | Kill skepticism above the fold |
| Offer | "$0 service call with repair — today only" box | Converts intent into action |
| FAQ | 4 questions (pricing, response time, warranty) | Handles top objections |
```

Form spec: 3–5 fields max (name, phone/zip, need), inline validation, mobile numeric keyboards,
thank-you page with conversion firing + next-step expectation.

## Workflow

1. Pull the ad promise and top keywords; write the H1 as a mirror of the ad (same offer, same
   wording family) — message match is the first thing a bouncing visitor checks.
2. Storyboard the page top-down: hero (promise + CTA visible without scrolling), proof strip,
   offer mechanics, benefits framed as outcomes, objection-handling FAQ, final CTA repeat.
3. Cut every escape hatch: hide global nav (or reduce to logo + phone), remove footer link
   walls; each additional exit lowers conversion probability.
4. Design the form for the funnel stage: 3–5 fields for cold lead-gen; longer forms only when
   sales qualification requires it — every field costs completion rate.
5. Build in Unbounce/Instapage (fast iteration, built-in A/B) or the CMS; use a mobile-first
   layout because the majority of search clicks are mobile.
6. Enforce speed: compress images, lazy-load below-fold media, minimize third-party scripts —
   target LCP under 2.5s on mobile.
7. Wire tracking before launch: form-submit / call-click events via GTM, thank-you page URL,
   GA4 key event + Google Ads conversion action (one source of truth).
8. QA both mobile and desktop: click-to-call works, form submits, autofill works, cookie
   consent does not push the CTA below the fold, privacy policy linked (lead-form compliance).
9. Deliver the page to ab-testing with one hypothesis (e.g., "proof-first hero lifts CVR 15%")
   and register the baseline CVR for measurement.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Rapid LP building + native A/B | Unbounce, Instapage | Paid; fastest iterate-learn loop |
| CMS builds | WordPress + page builder, Webflow | More control, slower iteration |
| Tag management & events | Google Tag Manager | Free; fire form/call events |
| Analytics verification | GA4 | Free; key events + source scoping |
| Speed audits | PageSpeed Insights, WebPageTest | Free; mobile-first, LCP <2.5s |
| Behavior insight | Hotjar / Microsoft Clarity | Clarity free; heatmaps + session replays |

## Example AI Prompt

```text
You are a PPC landing page specialist. Design a conversion-dedicated landing page for:
offer = {OFFER}; ad group theme = {THEME}; top search intent = {INTENT};
ad promise (must match): {AD HEADLINE/PROMISE}; audience = {AUDIENCE};
goal = {LEAD or SALE}; proof assets available = {REVIEWS/BADGES/CASE STUDIES};
platform = {UNBOUNCE / INSTAPAGE / CMS}; compliance notes = {PRIVACY/LEGAL RULES}.

Deliver:
1. Section-by-section spec table: section | copy | purpose (hero first, single primary CTA).
2. Form spec: fields (3–5), validation, thank-you page, CRM mapping.
3. Tracking checklist: GTM events, GA4 key event, Google Ads conversion action.
4. QA checklist for mobile + desktop before launch.
Rules: no global nav, message-match the H1 to the ad promise, one primary CTA, and note
where each trust element is placed.
```

## Edge Cases & Guardrails

- Never send cold paid traffic to the homepage: intent-to-page mismatch is the #1 cause of
  sub-1% paid CVR and low landing-page-experience scores.
- Long forms do not "qualify leads" — they lose good ones; qualify after capture with routing
  and sales follow-up instead.
- Slow pages tax every click twice: you pay for it in CVR and in Quality Score; keep paid
  templates on lean scripts (marketing tags only).
- Regulated verticals (finance, health, legal) require disclosures on-page; missing compliance
  copy risks both platform policy and regulator complaints.
- Dynamic keyword insertion on LPs must degrade gracefully — test with the keyword absent and
  with long-tail variants that break layouts.
- Do not judge a new LP on day-3 data; read results after the ab-testing agent confirms
  sample size and significance.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| LP conversion rate (lead-gen, dedicated page) | 5–10% | <3% vs campaign baseline |
| LP conversion rate (e-comm product/offer page) | 2–4% | <1.5% sustained |
| LCP (mobile, p75) | <2.5s | >4.0s |
| Bounce rate on paid LP | <50% | >70% with sub-3s dwell |
| Form completion rate (started → submitted) | ≥60% | <40% — cut fields |
| Message match (H1 mirrors ad promise) | 100% of LPs | Generic H1s on paid pages |

## Handoffs

- → **conversion-tracking:** deliver the event map (form submits, calls, thank-you URL) for
  tag implementation and verification.
- → **ab-testing:** register the page with baseline CVR and first test hypothesis.
- → **quality-score-optimization:** LP experience improvements route here for QS re-measurement.
- → **cro-agent:** hand over the page + traffic data for deeper optimization programs.
- ↑ **sem-ppc-agent:** escalate if offer economics (not page design) limit conversion.
