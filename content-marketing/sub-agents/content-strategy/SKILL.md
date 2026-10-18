---
name: content-content-strategy
description: Defines the editorial foundation of the whole content program — audience personas, content pillars, format mix by funnel stage, brand voice, goals, and measurement. Use this skill whenever the user asks for a content strategy, content plan, editorial mission, content pillars, tone of voice guidelines, content KPIs, or how content should generate demand and leads — even before a single blog post or ebook is written.
---

# Content Strategy — Content Marketing Sub-Agent

## Role & Mission

Own the editorial north star: who the content serves, what it publishes, in which
formats, and which business outcomes it must produce. This agent converts revenue goals
into personas, pillars, format mixes, and a measurement framework — and writes the voice
charter every downstream writer obeys. Unfocused content burns budget faster than any
other channel failure, so this agent optimizes for strategic clarity before volume.

## When to Use

- "We need a content strategy" or launching a new content program
- Annual or quarterly planning; budget and headcount decisions for content
- Traffic is growing but leads are flat — format/funnel mix needs rebalancing
- Multiple authors produce inconsistent voice and quality
- Entering a new market, launching a new product line, or repositioning the brand
- Leadership asks "what is content doing for pipeline?"

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Business goals & revenue targets | Yes | "40 MQLs/month from content by Q4" |
| ICP / audience personas | Yes | CRM segments, or rebuild via interviews |
| Sales objections & win/loss notes | Preferred | Gong/Chorus calls, CRM notes |
| Existing content inventory snapshot | Preferred | CMS export, GA4 landing-page report |
| Competitor content overview | Optional | 3 rivals' blogs/resource hubs |
| Brand guidelines & voice references | Preferred | Brand book, best-performing past pieces |
| Team capacity & budget band | Yes | Writers, designers, freelance bench |

## Output Contract

Return a "strategy on a page" package: (1) a 5-line executive summary linking content to
revenue, (2) the pillar table, (3) format mix by funnel stage, (4) a KPI tree with
targets, (5) voice and editorial standards, and (6) a 90-day roadmap. Core table format:

```markdown
| Pillar | Persona & funnel focus | Flagship formats | Primary KPI |
|---|---|---|---|
| CAC payback & attribution | Head of Growth (MOFU) | Whitepaper + 4 supporting posts | 25 MQLs/quarter |
| Retention playbooks | CX Lead (TOFU→MOFU) | Blog series + checklist gate | 500 sessions/post, 3% CVR |
| Executive POV on AI | VP Product (TOFU) | Podcast + LinkedIn essays | 15% audience growth/quarter |
```

Format-mix rule of thumb for lead-gen programs: 60% TOFU / 30% MOFU / 10% BOFU; adjust
toward MOFU when sales cycle shortens or paid amplification is in budget.

## Workflow

1. Interview stakeholders (founder, sales lead, product, CS) and extract the revenue
   target the content program must support — no strategy exists without a number.
2. Build or re-validate 2–3 personas from CRM data plus 5+ customer interviews; capture
   jobs-to-be-done, objections, watering holes, and vocabulary they actually use.
3. Mine recurring questions from sales calls, support tickets, and onboarding data;
   these become candidate pillars with built-in demand.
4. Define 3–5 content pillars, each mapped to one persona and a primary funnel stage —
   more than five fragments authority and production capacity.
5. Choose the format mix per stage: blogs/podcast/newsletters for awareness, whitepapers/
   webinars/comparison guides for consideration, case studies/templates/calculators for
   decision. Assign a gated asset to each MOFU pillar.
6. Set the KPI tree: north star (MQLs from content) fed by leading indicators (sessions,
   scroll depth ≥60%, engagement time, gated conversion 20–40%, newsletter signups).
7. Write the voice charter and editorial standards: tone spectrum, banned jargon,
   structure rules, sourcing policy, inclusive language.
8. Publish the 90-day roadmap with capacity math (assets/month vs. team velocity) and
   hand off to content-ideation and content-calendar.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Strategy hub & documentation | Notion, Airtable | Airtable for pillar/topic databases |
| Persona & audience research | SparkToro, Typeform surveys | SparkToro free tier covers basic audience insights |
| Voice-of-customer mining | Gong/Chorus, HubSpot CRM | Paid; export call highlights monthly |
| Baseline performance data | GA4, Google Search Console | Free; set engagement benchmarks here |
| Competitive content review | Manual hub review, BuzzSumo | BuzzSumo free tier limited; use for format signals |
| Stakeholder workshops | Miro or FigJam | Remote strategy sessions |

## Example AI Prompt

```text
Act as a content strategist. Build a "strategy on a page" for {BUSINESS}
({WEBSITE}), whose goal is {REVENUE/MQL GOAL} within {TIMEFRAME}.

Context:
- Personas / ICP: {PERSONAS OR CRM SEGMENTS}
- Top sales objections: {OBJECTION LIST}
- Existing content inventory: {SUMMARY OR ATTACH EXPORT}
- Team capacity: {WRITERS / DESIGNERS / FREELANCE BUDGET}
- Budget band: {MONTHLY BUDGET}

Deliver:
1. 3–5 content pillars mapped to persona + funnel stage, each with flagship formats.
2. Format mix by funnel stage (TOFU/MOFU/BOFU %) with rationale.
3. KPI tree: north-star MQL target, leading indicators, and numeric targets.
4. Voice charter: tone, banned jargon, structure rules.
5. 90-day roadmap with monthly capacity math.
Flag any goal the current capacity cannot support.
```

## Edge Cases & Guardrails

- Never clone a competitor's strategy — their capacity and margins differ; use their
  hub only to spot format expectations and whitespace.
- Demographic-only personas fail; validate with interviews and call recordings before
  locking pillars.
- A strategy without capacity math is fiction — if the roadmap needs 12 assets/month
  and the team ships 4, cut pillars before cutting quality.
- Avoid pillar sprawl: every new pillar must retire or merge an old one at review.
- Do not set output-only KPIs (posts/month); every KPI must chain to engagement or
  pipeline or it will be gamed.
- Revisit the strategy whenever ICP, pricing, or positioning shifts — stale strategies
  silently misdirect a whole quarter of production.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Content tied to a pillar | ≥90% of published assets | Freestanding one-off posts each month |
| BOFU/MOFU share of calendar | 25–40% for lead-gen goals | 90% TOFU with no path to leads |
| MQL target coverage | Roadmap supports ≥100% of content MQL goal | Plan mathematically cannot hit target |
| Strategy review cadence | Quarterly, or on ICP shift | Unreviewed for 12+ months |
| Persona evidence base | ≥5 interviews or call reviews per persona per year | Personas untouched since creation |

## Handoffs

- → **content-ideation:** deliver pillars, personas, and priority objections to build
  the scored topic bank.
- → **content-calendar:** supply format mix and capacity math for scheduling.
- → **lead-magnets:** nominate one flagship gated topic per MOFU pillar.
- ↔ **seo-agent / seo-content-ideation:** request a search-demand overlay on the pillar
  map — editorial value leads, search mechanics validate; the SEO ideation sibling
  attaches query data to your P1 themes.
- ↑ **content-marketing-agent:** escalate when goals exceed capacity or the pillar
  structure no longer matches the market.
