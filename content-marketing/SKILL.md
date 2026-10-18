---
name: content-marketing-agent
description: Commands the full content marketing operation — content strategy, editorial ideation, publishing calendars, blogs, ebooks and whitepapers, conversion copywriting, editing, distribution, repurposing, lead magnets, and content audits. Use this skill whenever the user mentions content strategy, editorial calendar, blog posts, whitepapers, ebooks, lead magnets, gated content, repurposing, content audits, brand voice, or thought leadership — even if they never say "content marketing" explicitly.
---

# Content Marketing — Main Agent (Command Hub)

## Channel Overview

Content marketing builds audience trust and demand through owned editorial assets — blogs,
ebooks, whitepapers, newsletters, podcasts, videos — that educate and persuade before a
sales conversation starts. It is the channel that feeds every other channel: SEO needs
content to rank, email needs content to send, social needs content to share, and sales
needs material to nurture. Its unique demand-generation weapon is the gated asset: a
well-matched ebook or template converts 20–40% of its landing-page visitors into
identifiable leads, something no ad format replicates at similar cost.

This channel wins when buying cycles are considered (B2B SaaS, professional services,
education, high-ticket B2C), when the category needs education, and when the brand can
publish consistently for 3–6 months before judging results. It underperforms when demand
must be captured today (route to SEM/PPC), when editorial quality cannot be sustained, or
when leadership demands direct-response attribution from day one. Costs are labor-heavy
rather than media-heavy: expect $1,500–$15,000+/month depending on volume, formats, and
whether video or podcast production is in scope. Realistic time-to-results: engagement
signals improve within 90 days, organic traffic within 6 months, content-sourced pipeline
within 9–12 months.

## Agent Hierarchy

```text
content-marketing-agent (command hub)
└── sub-agents/
    ├── content-strategy/         → audience, pillars, format mix, goals, voice
    ├── content-ideation/         → evidence-based topic bank from audience signals
    ├── content-calendar/         → dated publishing schedule, owners, SLAs
    ├── content-creation/         → blogs, ebooks, whitepapers, infographics, podcasts
    ├── copywriting/              → conversion copy: landing pages, CTAs, headlines
    ├── editing-proofreading/     → quality gate: substance, voice, accuracy
    ├── content-distribution/     → amplification, syndication, advocacy, native paid
    ├── content-repurposing/      → atomize pillar assets into derivative formats
    ├── lead-magnets/             → gated assets + landing pages that capture leads
    └── content-audits/           → portfolio scorecards, refresh/prune decisions
```

## Sub-Agent Routing Table

| Sub-agent | Call when… | Key inputs | Depends on |
|---|---|---|---|
| content-strategy | Program kickoff, annual/quarterly planning, ICP shift, or traffic without leads | Business goals, personas, sales objections, capacity | None (entry point) |
| content-ideation | Strategy approved and a scored topic bank is needed | Pillars, personas, sales-call notes, community signals | content-strategy |
| content-calendar | Topics approved and dates, owners, and SLAs are needed | Topic bank, team capacity, campaign dates | content-ideation |
| content-creation | A calendar entry moves to "in production" | Brief, voice guide, SME availability, deadline | content-calendar |
| copywriting | Gated-asset landing pages, CTAs, headlines, or promo copy need conversion focus | Offer details, audience pain, proof points, metrics | content-creation, lead-magnets |
| editing-proofreading | Any draft is ready before publish; voice drift; compliance-sensitive claims | Draft, style guide, source list | content-creation |
| content-distribution | An approved asset needs reach beyond organic search | Asset URL, channel list, UTM scheme, paid budget | editing-proofreading |
| content-repurposing | A pillar asset overperforms and derivatives would extend its reach | Performance data, source asset, platform specs | content-audits, content-creation |
| lead-magnets | Traffic exists but lead capture lags, or a new gated asset is scoped | Topic demand, design capacity, CRM form fields | content-creation, copywriting |
| content-audits | Quarterly review, traffic plateau, portfolio bloat, or pre-migration | GA4/GSC exports, URL inventory, conversion data | None (entry point) |

## End-to-End Workflows

### Workflow A — Launch a Content Program from Zero (weeks 1–12)

1. Run **content-strategy** to produce the strategy on a page: personas, 3–5 pillars,
   format mix by funnel stage, KPI tree, and editorial standards. Output: north-star
   MQL target plus the voice charter every writer follows.
2. Hand pillars and personas to **content-ideation**: build a scored 60–100-topic bank
   from sales calls, support tickets, community listening, and past performance.
   Output: P1 topics with evidence and funnel mapping.
3. Pass the P1 list to **content-calendar**: lock a 90-day cadence with owners, SLA
   stages, and a 20% capacity buffer. Output: dated production board.
4. Enter the production loop: **content-creation** drafts each asset from a brief;
   **editing-proofreading** clears it through substantive, line, and proofread tiers.
   Output: 8–12 published assets at ≥85% first-pass QA rate.
5. Build the flagship offer in parallel: **lead-magnets** scopes and produces the gated
   asset and landing page; **copywriting** writes the hero, body, and CTA variants.
   Output: live gated asset targeting 20–40% landing conversion.
6. Ship every asset through **content-distribution**: per-channel angles, email
   features, syndication with canonical tags, and a small native paid test on winners.
   Output: 500–2,000 referral sessions per flagship asset in 30 days.
7. At day 90, run **content-audits**: score the young portfolio, refresh weak performers,
   and feed conclusions back to strategy. Output: recalibrated quarter-2 plan.

### Workflow B — Flagship Gated Asset Launch (ebook/whitepaper, weeks 1–6)

1. **content-ideation** validates the topic against sales objections and audience
   signals; **content-strategy** confirms it maps to a pillar and the MQL goal.
2. **content-creation** produces the asset: outline approval, SME interviews, design
   coordination, and a structured, repurposing-ready master document.
3. **copywriting** writes the landing page (hero, benefit blocks, objection handling)
   plus 5–10 headline options and A/B variants with hypotheses.
4. **lead-magnets** builds the landing experience: 2–3 form fields, CRM wiring,
   thank-you page with next-step CTA, delivery email, and nurture handoff to the
   marketing-automation channel.
5. **content-distribution** runs the launch plan: email feature, LinkedIn/founder posts,
   syndicated excerpt with rel=canonical, community seeding, and an Outbrain/Taboola
   test capped until cost per session proves out.
6. **content-repurposing** atomizes the asset within 60 days: carousel, clips, email
   mini-course, infographic — 8–12 derivatives scheduled into the calendar.
7. **content-audits** reviews landing conversion and MQL→SQL rate at day 30 and day 90;
   underperformers get repositioned or retired.

### Workflow C — Quarterly Portfolio Optimization Cycle (recurring)

1. **content-audits** scores every URL on traffic, engagement (scroll depth, time on
   page), and conversions → keep/refresh/consolidate/prune verdicts.
2. **content-strategy** absorbs the findings: retire weak pillars, double down on
   formats that generate MQLs.
3. **content-ideation** rebuilds the topic bank for the next quarter, weighted toward
   proven winners and uncovered objections.
4. **content-calendar** rebuilds the schedule, reserving slots for audit-mandated
   refreshes before net-new production.
5. Production loop runs monthly: creation → editing → distribution, with
   **content-repurposing** batching derivatives for every new pillar asset.
6. **lead-magnets** retires gates converting below 20%, tests new offers on
   high-traffic low-conversion posts identified by the audit.

## KPI Dashboard

North-star metric: **MQLs sourced from content each month** (sessions without leads is
audience-building; pipeline is the business outcome).

| Metric | Source tool | Cadence | Healthy range |
|---|---|---|---|
| Organic + referral sessions to content | GA4 | Weekly | +5–10% MoM in growth phase |
| Scroll depth on pillar posts | GA4 / Hotjar | Monthly | ≥60% of readers pass 60% depth |
| Avg. engagement time (long-form) | GA4 | Monthly | 2–4 minutes |
| Gated-asset landing conversion | HubSpot / Unbounce | Monthly | 20–40% of landing visitors |
| Reader-to-lead conversion (all content) | CRM + GA4 | Monthly | 0.5–2% of unique readers |
| MQL-to-SQL rate from content leads | CRM | Monthly | 15–25% |
| Newsletter signups from content | ESP | Weekly | 0.5–1.5% of readers |
| Repurposing yield | Notion / Airtable tracker | Quarterly | ≥8 derivatives per pillar asset |
| Cost per MQL from content | CRM + budget tracker | Monthly | Declining QoQ; benchmark vs. paid channels |
| Refresh lift on audited URLs | GA4 (audit re-measurement) | Quarterly | +20–50% sessions within 90 days |
| On-time publish rate | Calendar tool | Weekly | ≥90% |

## Budget Guidance

| Monthly budget | Recommended allocation |
|---|---|
| $1,000–$2,500 | 55% freelance writing/design, 20% flagship gated asset, 15% tools, 10% paid amplification tests |
| $2,500–$7,500 | 45% creation (writer + designer), 20% gated assets, 15% distribution/syndication, 10% editing/ops, 10% tools |
| $7,500–$20,000 | 40% in-house creation team, 20% flagship assets/design, 15% distribution incl. native paid, 15% repurposing (video/podcast), 10% tools & data |
| $20,000+ | Dedicated in-house team + freelance/agency bench; 35% creation, 20% flagship assets, 20% distribution/paid, 15% repurposing, 10% tools/data |

Allocation principles:

- Fund quality over volume: one flagship gated asset per quarter beats four mediocre ones.
- Never promote unproven content — reserve 10–15% for paid amplification of assets that
  already earn engagement organically.
- Cap tooling at 10–15%; editing and editorial management are cheaper quality levers
  than any software line item.
- Hold a 10% contingency for reactive opportunities (newsjacking, competitor launches).
- Split budget across the funnel deliberately: if every dollar goes to TOFU blogs, the
  MQL line flatlines no matter how traffic trends.

## Team & Agency Mapping

| Activity | Best handled by | Rationale |
|---|---|---|
| Strategy & editorial standards | In-house (or fractional lead) | Needs business context and stakeholder access |
| Long-form creation | In-house writer + SMEs; freelance bench for overflow | Subject-matter depth beats generic agency output |
| Conversion copywriting | In-house or specialist freelancer | Tight loop with offer, forms, and test data |
| Editing & proofreading | In-house managing editor | Voice consistency across all authors |
| Design & infographics | Freelance designer or agency | Periodic intensity; template-driven |
| Distribution & syndication | In-house (paired with social team) | Coordination-heavy, judgment-light |
| Podcast / video production | Agency or studio | Equipment and editing skill; batch quarterly |
| Content audits | In-house analyst or outside consultant | An objective view catches blind spots |

## Reporting Cadence

- **Weekly (content ops, 30 min):** production pipeline status, published vs. plan,
  on-time rate, distribution results, gating incidents. Decision: unblock production,
  re-sequence the calendar.
- **Monthly (stakeholders, 1 hr):** sessions, scroll depth, engagement time, MQLs from
  content, gated-asset conversion, top/bottom performers, next-month plan. Decision:
  topic and format rebalance.
- **Quarterly (leadership):** content-sourced pipeline and ROI, audit outcomes, pillar
  performance, refresh/prune results, budget reallocation. Decision: strategy shifts,
  headcount, agency scope.

## Cross-Channel Integrations

- **↔ seo-agent:** receive keyword demand overlays and content-gap data to inform
  editorial topics — editorial value first, search mechanics second. Hand back
  published posts for on-page optimization; coordinate with the seo-content-ideation
  and seo-content-creation sub-agents as the SEO-flavored siblings of this channel's
  ideation and creation agents.
- **→ social-media-marketing-agent:** distribution kits, derivative assets, and
  per-channel angles for every published piece; social engagement data returns as an
  ideation signal.
- **→ email-marketing-agent:** newsletter features for new content, promo sequences
  for gated assets, and repurposed content for nurture streams.
- **→ marketing-automation-agent:** every gated-asset lead arrives tagged with source,
  topic, and funnel stage for scoring and nurture-track assignment.
- **→ cro:** gated-asset landing pages and high-traffic blog CTAs are the highest-
  leverage conversion test candidates.
- **→ web-analytics:** scroll-depth events, engagement-time definitions, and content
  attribution configuration live here; audits depend on clean GA4 data.
- **← video-marketing-agent:** webinar and video transcripts become source material
  for articles, whitepapers, and derivative content.
- **← sem-ppc-agent:** highest-converting paid headlines and angles reveal offer
  framing worth testing on gated landing pages; wasted ad angles warn against topics
  with weak message-market fit.
- **→ cro:** nurture-path microconversions (quiz starts, checklist downloads) supply
  intent signals that sharpen segmentation and remarketing lists.
