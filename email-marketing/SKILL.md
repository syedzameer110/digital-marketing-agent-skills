---
name: email-marketing-agent
description: Orchestrates the full email marketing workflow — list building, lead magnets, segmentation, automation and drip campaigns, email design, copywriting, A/B testing, personalization, deliverability, list hygiene, and analytics. Use this skill whenever the user wants to launch or improve email campaigns, newsletters, welcome series, drip sequences, or abandoned-cart flows, grow or clean a subscriber list, lift open and click rates, fix spam placement, or mentions Mailchimp, Klaviyo, HubSpot, ActiveCampaign, Brevo, or Customer.io — even if they never say "email marketing" explicitly.
---

# Email Marketing — Main Agent (Command Hub)

## Channel Overview

Email is the only major channel where the audience is owned rather than rented: no algorithm
sits between the brand and the inbox, sends are nearly free at the margin, and every message
reaches a person who explicitly raised a hand. Consistently cited among the highest-ROI
marketing channels, with widely used industry rule-of-thumb estimates of $30–$40 returned per
$1 spent for mature opt-in programs. Costs are dominated by platform subscriptions (Mailchimp,
Klaviyo, HubSpot, ActiveCampaign, Brevo, Customer.io) and labor — copy, design, and automation
builds — rather than media spend, making it the cheapest channel to operate once a list exists.

Email wins when there is permission and a repeat relationship: nurture, retention, lifecycle,
and reactivation. It underperforms as a cold-acquisition tool — route net-new demand to SEM/PPC
or paid social, then convert that traffic into subscribers. Time-to-results is fast by channel
standards: a well-built welcome or abandoned-cart flow pays for itself within weeks, while
list-growth engines compound over 3–6 months. Platform choice follows business model —
Klaviyo for e-comm revenue tracking, HubSpot or ActiveCampaign for B2B nurture and CRM joins,
Brevo or Mailchimp for SMB budgets, Customer.io for event-driven product messaging. Two
persistent traps shape all strategy: Apple Mail Privacy Protection (MPP) pre-fetches images
and inflates open rates (35%+ open rates are common and often fake), so run the program on
clicks and conversions; and deliverability is fragile — one sloppy send to a stale list can
poison domain reputation for months.

## Agent Hierarchy

```text
email-marketing-agent (command hub)
└── sub-agents/
    ├── list-building/              → capture forms, opt-ins, sign-up funnels
    ├── lead-magnet-creation/       → incentives that convert visitors into subscribers
    ├── segmentation/               → divide lists by behavior, demographics, interests
    ├── email-automation/           → welcome series, drip campaigns, lifecycle flows
    ├── email-design/               → templates, responsive layouts, render testing
    ├── copywriting/                → subject lines, body copy, CTAs
    ├── ab-testing/                 → test subject lines, content, send times
    ├── personalization/            → dynamic content from user and CRM data
    ├── deliverability-management/  → SPF/DKIM/DMARC/BIMI, reputation, spam placement
    ├── list-hygiene/               → sunset policies, inactive-subscriber removal
    └── analytics/                  → opens, clicks, conversions, revenue attribution
```

## Sub-Agent Routing Table

| Sub-agent | Call when… | Key inputs | Depends on |
|---|---|---|---|
| list-building | Growing the subscriber base, forms underperform, new site or funnel launch | Site traffic data, lead magnet, ESP form tools, consent requirements | None (entry point) |
| lead-magnet-creation | Need an incentive to trade for an email address; opt-in rates lag | Audience pain points, existing content assets, brand voice, fulfillment cost limits | None (entry point) |
| segmentation | Blasts underperform, before any major campaign, or new data fields arrive | ESP data (behavior, purchases, demographics), campaign calendar | list-building |
| email-automation | Building welcome series, drip campaigns, abandoned-cart, or win-back flows | Journey map, triggers, offer ladder, brand voice | segmentation |
| email-design | New template, poor rendering, rebrand, dark-mode or accessibility complaints | Brand kit, ESP builder, client/device mix data, campaign content | copywriting (content brief) |
| copywriting | Any send needs subject lines, preheaders, body copy, or CTA variants | Campaign brief, segment profile, offer details, voice guide, past winners | segmentation |
| ab-testing | Improving opens/clicks/conversions, debates over subject lines or send times | Baseline metrics, hypothesis backlog, ESP A/B capability, list size | analytics (baseline) |
| personalization | Dynamic content from user data; mid-size+ lists with CRM or purchase data | ESP/CRM fields, purchase and browsing history, fallback rules | segmentation |
| deliverability-management | Opens crater, mail lands in spam, new sending domain, Google/Yahoo sender requirements | DNS access, sending domain, Google Postmaster Tools, ESP logs | None (parallel-safe) |
| list-hygiene | Engagement slides, bounces rise, list older than 6 months, pre-holiday cleanup | Engagement recency data, bounce/complaint logs, ESP segments | analytics |
| analytics | Weekly/monthly reporting, campaign post-mortems, revenue attribution questions | ESP exports, GA4 or e-comm data, CRM, attribution model choice | all |

## End-to-End Workflows

### Workflow A — Launch a List Growth Engine (new program, weeks 1–8)

1. Run **lead-magnet-creation** to produce the incentive: mine pain points, score 4–6 concepts,
   build the strongest (checklist, template, quiz, or discount). Output: magnet + delivery page.
2. Run **list-building**: deploy capture points (embedded, exit-intent, dedicated landing page)
   with double opt-in and GDPR/CAN-SPAM-compliant consent language. Output: live forms + tracking.
3. Run **deliverability-management** before any volume: authenticate the sending domain with
   SPF, DKIM, and DMARC, verify the From domain, and warm up if on a dedicated IP. Output:
   clean authentication scorecard.
4. Run **email-automation** to build the welcome series (3–5 emails) that delivers the magnet,
   sets expectations, and makes the first offer. Output: live flow with entry/exit rules.
5. Run **copywriting** then **email-design** to produce flow copy and a modular, responsive
   template that renders in Outlook, Gmail, and Apple Mail (Litmus/Email on Acid tests).
   Output: reusable template + approved copy deck.
6. Run **ab-testing** on capture forms (headline, offer, timing) and welcome subject lines.
   Output: documented winners rolled into the template.
7. Switch on **analytics** dashboards with MPP-adjusted open reporting and weekly cadence.
   Output: growth dashboard + first monthly readout.

### Workflow B — Quarterly Revenue Campaign Sprint (B2B or e-comm, 4–6 weeks)

1. Run **analytics** for the baseline: segment-level performance, revenue per recipient,
   flow vs campaign contribution, last quarter's winners. Output: opportunity memo.
2. Run **list-hygiene** before the sprint: sunset 180-day inactives, validate never-engaged
   addresses, purge hard bounces. Output: leaner list, protected reputation.
3. Run **segmentation** to define campaign audiences by lifecycle stage and engagement recency.
   Output: segment blueprint with sizes and purposes.
4. Run **personalization** to add dynamic blocks (product recommendations, industry-specific
   hero, offer tier) with safe fallbacks. Output: personalization map + built blocks.
5. Run **copywriting** and **email-design** to produce the campaign set (announcement, reminder,
   last-chance). Output: campaign-ready emails, QA'd across clients.
6. Run **deliverability-management** as the pre-send gate: spam-rate check, seed test, volume
   plan across the send window. Output: go/no-go verdict.
7. Send with **ab-testing** on subject lines (20/80 split), then close with **analytics**:
   post-campaign readout and backlog for next quarter.

### Workflow C — Deliverability Rescue (mail hits spam, opens crater)

1. Run **analytics** to scope the damage with MPP in mind: compare click-based engagement and
   Postmaster spam-rate data, not raw opens. Output: diagnosis memo.
2. Run **list-hygiene**: aggressive cull of 90+ day inactives, validation of the remainder.
   Output: suppressed list + validation report.
3. Run **deliverability-management**: fix or harden SPF/DKIM/DMARC, move DMARC toward
   quarantine/reject, restart warm-up, implement one-click list-unsubscribe headers.
   Output: remediation plan with a 30-day recovery timeline.
4. Run **segmentation** to rebuild the send universe around the engaged core.
5. Run **email-automation** to replace batch-and-blast with triggered flows (re-engagement,
   win-back) that restore steady, wanted mail. Output: rebuilt flow portfolio.
6. Run **ab-testing** on re-permission campaign subject lines ("still want these emails?").
7. Run **list-building** to rebuild capture with double opt-in so growth resumes on a
   quality footing. Output: hardened capture points.
8. Track recovery with **analytics** for 60 days before scaling volume back.

## KPI Dashboard

North-star metric: **Email-attributed revenue (or qualified pipeline) per month** — opens and
clicks pay no bills; every review ties back to conversions and revenue per recipient.

| Metric | Source tool | Cadence | Healthy range |
|---|---|---|---|
| Open rate | ESP | Weekly | 20–25% opt-in B2B; 15–22% e-comm. 35%+ usually signals Apple MPP inflation — verify against click-based engagement |
| Click-through rate | ESP | Weekly | 2–3% of delivered |
| Click-to-open rate | ESP | Weekly | 8–12% |
| Unsubscribe rate | ESP | Per campaign | <0.5% |
| Spam complaint rate | ESP + Google Postmaster Tools | Per campaign | <0.1% (Google's bulk-sender threshold is 0.3%) |
| Deliverability | Google Postmaster Tools + seed tests | Monthly | 97%+ delivered, 90%+ inbox placement |
| Hard bounce rate | ESP | Per send | <1% |
| Automation revenue share | ESP / e-comm platform | Monthly | 25–40% of email revenue from automated flows |
| Net list growth (after hygiene) | ESP | Monthly | +2–5% MoM; shrinking two quarters straight is strategic |
| Revenue per recipient | ESP / e-comm platform | Monthly | Trending up vs prior period; flows should out-earn campaigns |

## Budget Guidance

| Monthly budget | Recommended allocation |
|---|---|
| < $1,000 | 40% ESP (Brevo/Mailchimp free or entry tier), 40% founder-led copy+design time, 20% lead magnet production |
| $1,000–$5,000 | 30% ESP (Klaviyo/ActiveCampaign/HubSpot tier), 45% freelance copy+design, 15% magnet+landing production, 10% Litmus/testing |
| $5,000–$15,000 | 25% ESP, 40% production team (copy+design), 15% automation builds (contractor), 10% tools, 10% deliverability & testing |
| $15,000+ | In-house email lead plus agency overflow; 30% ESP/CDP, 35% production, 15% automation, 10% tools, 10% experimentation |

Allocation principles:

- Build automation flows first: created once, they typically drive 25–40% of email revenue and
  keep earning while campaigns rotate.
- Cap tooling at ~25% of budget — copy and design decide revenue, tools only inform it.
- Never buy email lists; spend the same money on lead magnets and capture. Purchased lists
  destroy deliverability and violate GDPR/CAN-SPAM consent expectations.
- Reserve ~10% for deliverability and render testing (Litmus/Email on Acid, Postmaster
  monitoring) — invisible until a bad send makes it everything.
- Treat list hygiene as cost control: contact-based ESP pricing (Klaviyo, Mailchimp) bills
  dead addresses every month, so a sunset policy pays for itself twice.
- Switching ESPs is a data-migration project, not a procurement decision: flow history,
  segments, and consent records must move or the program restarts from zero.

## Team & Agency Mapping

| Activity | Best handled by | Rationale |
|---|---|---|
| Strategy, calendar, segmentation logic | In-house | Requires business context, sales alignment, data access |
| Copywriting | In-house or vetted freelancer | Brand voice consistency compounds across sends |
| Email design/templates | Freelancer or agency | Hand-coded HTML email (Outlook-safe, dark mode) is a niche skill |
| Automation flow builds | Contractor/agency or in-house power user | One-time builds; platform expertise pays off fast |
| Deliverability management | Specialist consultant, then in-house monitoring | DNS/authentication depth needed rarely but critically |
| List hygiene | In-house (automated rules) | Routine segment/suppression upkeep once policies exist |
| Analytics & reporting | In-house | Must connect ESP data to revenue systems |

## Reporting Cadence

- **Weekly (in-house, 30 min):** last sends and flows performance (opens with MPP caveat,
  CTR, conversions), list growth, deliverability alerts, spam complaints. Decision: next
  week's sends and any flow fixes.
- **Monthly (stakeholders, 1 hr):** revenue/pipeline attributed, segment and flow
  contribution, unsubscribe and complaint trends, hygiene status, next-month calendar.
  Decision: budget shifts, test priorities.
- **Quarterly (leadership):** channel ROI, list growth forecast, automation portfolio audit,
  deliverability posture (DMARC policy stage), strategy and ESP-configuration changes.
  Decision: annual plan and platform/vendor review.

## Cross-Channel Integrations

- **→ content-marketing-agent:** the newsletter redistributes blog posts and lead magnets;
  co-produce magnets from top content assets, and route email engagement signals back as
  topic-demand data for the editorial calendar.
- **→ marketing-automation-agent:** email is the execution arm of lifecycle automation —
  hand over trigger maps, lead scores, and flow blueprints; receive lead-stage definitions
  back to align welcome and nurture sequences.
- **↔ CRM:** sync subscriber records, lead scores, and sales-stage data bidirectionally with
  the CRM so segmentation and personalization use live customer truth, and sales sees email
  engagement on every account.
- **→ cro-agent:** sign-up forms, pop-ups, and landing pages are CRO test surface; exchange
  test results and route high-traffic email landing pages into the CRO backlog.
- **← sem-ppc / paid social:** paid campaigns feed the list via lead magnets; import paid
  audience insights (top-converting themes) into email segmentation.
- **← affiliate-marketing / influencer-marketing:** partner and creator promotions route
  through co-branded capture points; agree list-source tags and consent language before
  any joint send.
- **← content-marketing-agent (inbound):** gated content performance and topic-demand
  signals from email engagement loop back into the content roadmap.
- **→ web-analytics:** enforce UTM discipline on every link and mirror email conversion
  events in GA4 so reporting reconciles with site-side truth.
