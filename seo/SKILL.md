---
name: seo-agent
description: Orchestrates the full Search Engine Optimization workflow — keyword research, content, on-page and technical SEO, backlinks, local SEO, audits, rank tracking, competitor analysis, and reporting. Use this skill whenever the user wants to grow organic traffic, rank for keywords, fix search visibility, plan SEO strategy, recover from ranking drops, or mentions SEO, Google rankings, organic search, backlinks, or search console data — even if they never say "SEO" explicitly.
---

# SEO (Search Engine Optimization) — Main Agent (Command Hub)

## Channel Overview

SEO earns organic visibility by making a site the best answer for the searches its audience
runs. Unlike paid channels, traffic compounds: a page that ranks well keeps delivering
visits at near-zero marginal cost, which is why SEO typically delivers the lowest long-term
customer acquisition cost of any marketing channel. The trade-offs are time and uncertainty
— most campaigns need 3–6 months to show meaningful movement in competitive niches, and
algorithm updates can reshuffle results overnight.

This channel wins when demand already exists (people actively searching for solutions),
when the business can sustain a 6–12 month investment horizon, and when content or product
pages can genuinely satisfy searcher intent. It underperforms for brand-new categories with
no search volume, pure brand-awareness goals, or urgent lead-gen needs — route those to
SEM/PPC or paid social instead. Costs are mostly labor (strategy, content, links, dev work)
rather than media spend: expect $1,500–$10,000+/month for serious programs depending on
niche competitiveness and content volume.

What separates winning programs from stalled ones: (1) technical hygiene is fixed BEFORE
content scales, (2) every page targets one validated keyword cluster with a clear intent,
(3) link acquisition runs continuously rather than in bursts, and (4) reporting ties
rankings to revenue instead of vanity traffic. Use the sub-agents below as an assembly
line — sequence matters more than volume.

## Agent Hierarchy

```text
seo-agent (command hub)
└── sub-agents/
    ├── keyword-research/          → find & prioritize target search terms
    ├── content-ideation/          → turn keywords into a content roadmap
    ├── content-creation/          → brief, draft & optimize rank-worthy content
    ├── on-page-optimization/      → titles, metas, headings, URLs, internal links
    ├── technical-seo/             → speed, crawlability, mobile, schema, indexation
    ├── backlink-building/         → outreach, guest posts, digital PR, links
    ├── link-analysis/             → audit backlink profile, disavow toxic links
    ├── rank-checking/             → track keyword positions & visibility over time
    ├── competitor-analysis/       → reverse-engineer rival keywords & strategies
    ├── local-seo/                 → Google Business Profile, citations, reviews
    ├── seo-audits/                → full site health checks
    └── reporting/                 → traffic, rankings, conversions, insights
```

## Sub-Agent Routing Table

| Sub-agent | Call when… | Key inputs | Depends on |
|---|---|---|---|
| keyword-research | Starting a new site, entering a new market, or refreshing targets quarterly | Site URL, product/service list, target geography | None (entry point) |
| content-ideation | Keywords are validated and you need topics mapped to funnel stages | Priority keyword list, audience personas | keyword-research |
| content-creation | A topic is approved and needs a brief, draft, or full rewrite | Content calendar entry, keyword map, brand voice guide | content-ideation |
| on-page-optimization | Pages exist but underperform, or new content ships | Target URL, target keyword, Search Console data | content-creation |
| technical-seo | Traffic plateaus despite content work, migration, indexation issues, Core Web Vitals alerts | Crawl access, Search Console, sitemap | None (parallel-safe) |
| backlink-building | Content assets are live and need authority; Domain Rating lags competitors | Linkable assets list, competitor backlink gaps | content-creation, competitor-analysis |
| link-analysis | Penalty risk review, quarterly link hygiene, or before/after link campaigns | Backlink export (Ahrefs/GSC), anchor text data | backlink-building |
| rank-checking | Ongoing monitoring, after publishing/optimizing, or algorithm update hits | Tracked keyword list, device & location scope | keyword-research |
| competitor-analysis | Losing share of voice, new market entry, quarterly strategy review | 3–5 competitor domains, target keyword set | keyword-research |
| local-seo | Business has physical locations or serves defined local areas | Locations, GBP access, service areas | None (parallel-safe) |
| seo-audits | Program kickoff, traffic drops, quarterly health check, pre-migration | Site access, CMS, Search Console, analytics | None (entry point) |
| reporting | Weekly/monthly/quarterly cycles or stakeholder requests | GA4, Search Console, rank tracker exports | rank-checking, all |

## End-to-End Workflows

### Workflow A — New Site / New Market Launch (weeks 1–12)

1. Run **seo-audits** on the existing site (or staging) to establish a health baseline and
   catch blocking issues before investing in content. Output: prioritized fix list.
2. Hand the site profile to **keyword-research**: build the master keyword map (500–2,000
   terms) segmented by intent and difficulty. Output: prioritized keyword targets.
3. Run **competitor-analysis** on the 3–5 domains already winning those keywords to find
   content gaps and realistic link benchmarks. Output: gap analysis + attack plan.
4. Feed the keyword map to **content-ideation**, then **content-creation**: ship the first
   8–12 pages (money pages first, then 2–4 supporting info pieces each). Output: live,
   optimized pages.
5. Run **on-page-optimization** across every shipped page and **technical-seo** on the
   backlog from step 1 (indexation, speed, schema). Output: clean crawl + polished pages.
6. Start **backlink-building** against the 3 strongest assets while **local-seo** locks down
   GBP and citations (if applicable). Output: first 10–20 quality links, consistent NAP.
7. Switch on **rank-checking** for the tracked keyword set and go into monthly
   **reporting** loops; iterate quarterly.

### Workflow B — Traffic Recovery Sprint (after an algorithm update or ranking drop)

1. Run **rank-checking** scoped to the last 90 days to isolate which page groups and query
   themes lost visibility. Output: affected-URL list.
2. Run **link-analysis** to rule out penalty/toxic-link causes; prepare a disavow file if
   needed. Output: link verdict.
3. Run **seo-audits** focused on the affected URLs (technical + content quality).
4. Route findings to **on-page-optimization** and **content-creation** for refreshes;
   **technical-seo** for crawl/render fixes discovered.
5. Re-monitor via **rank-checking** for 4–8 weeks and close the loop with **reporting**.

### Workflow C — Quarterly Growth Cycle (recurring)

1. **competitor-analysis** refresh → 2. **keyword-research** gap review → 3. **content-ideation**
   for the next quarter's calendar → 4. monthly **content-creation** + **backlink-building**
   production sprints → 5. continuous **rank-checking** → 6. quarterly **reporting** with
   strategy adjustments.

Each cycle should also include one **link-analysis** hygiene pass and one **seo-audits**
spot-check on newly shipped templates, so technical debt never accumulates silently.
The output of every quarterly cycle is a revised keyword map, an updated content calendar,
and a refreshed forecast — the same three artifacts the next quarter consumes as inputs.

## KPI Dashboard

North-star metric: **Organic conversions per month** (traffic vanity metrics do not pay
bills — tie everything to leads/sales from organic landing pages).

| Metric | Source tool | Cadence | Healthy range |
|---|---|---|---|
| Organic sessions | GA4 | Weekly | +5–10% MoM in growth phase |
| Organic conversions / CVR | GA4 | Weekly | 1–3% of organic sessions (lead gen) |
| Tracked keywords in top 3 / top 10 | Rank tracker (Ahrefs/Semrush) | Weekly | Top-10 share trending up QoQ |
| Referring domains (net new, quality) | Ahrefs/Semrush | Monthly | +5–15/month (SMB) |
| Core Web Vitals pass rate | PageSpeed/CrUX | Monthly | >75% of URLs "Good" |
| Index coverage errors | Search Console | Monthly | <1% of submitted URLs |
| GBP actions (calls, direction requests) | Google Business Profile | Monthly | Trending up vs prior period |
| Share of voice (top-10 visibility vs competitors) | Ahrefs/Semrush | Quarterly | Rising or stable QoQ |
| Content decay (top pages losing >20% traffic) | GA4 + GSC | Quarterly | <10% of top-20 pages |

## Budget Guidance

| Monthly budget | Recommended allocation |
|---|---|
| $1,000–$2,500 | 60% content creation, 20% tools, 20% links/digital PR; founder-led outreach |
| $2,500–$7,500 | 40% content, 25% link building, 20% technical/retainer, 15% tools |
| $7,500–$20,000 | 35% content (2–4 writer team), 30% links/PR agency, 20% technical retainer, 15% tools & data |
| $20,000+ | Dedicated in-house lead + agency support; split 40/30/20/10 with enterprise tooling |

Allocation principles:

- Content and links earn the ranking; tooling only informs it — cap tools at ~15%.
- In hyper-competitive niches (finance, legal, SaaS), shift 10–15% from content volume
  toward link acquisition and digital PR.
- Never spend on links before technical-seo clears crawl and indexation blockers.
- Fund refreshes of proven pages before net-new pages — updating a decayed top-10 page
  usually returns faster than publishing a new one.
- Reserve a 10% contingency for algorithm-recovery sprints.

## Team & Agency Mapping

| Activity | Best handled by | Rationale |
|---|---|---|
| Strategy & reporting | In-house (or fractional) | Needs business context and stakeholder access |
| Content creation | In-house writer + editor, or vetted freelancers | Subject-matter depth beats generic agency content |
| Technical SEO | Agency/consultant (audit + dev liaison) | Specialist skill, periodic intensity |
| Link building / digital PR | Agency or specialist freelancer | Process-driven outreach; scales externally |
| Local SEO | In-house admin with checklist | Routine GBP/citation/review upkeep |
| Rank checking & tooling | In-house (automated) | Low effort once dashboards exist |
| Content ideation & calendar | In-house marketing lead | Needs product roadmap and sales input |

## Reporting Cadence

- **Weekly (in-house, 30 min):** rankings movement, conversions, published content, links
  shipped, technical incidents. Decision: sprint adjustments.
- **Monthly (stakeholders, 1 hr):** traffic/conversions vs plan, top gaining/losing pages,
  content pipeline status, link velocity, next-month priorities.
- **Quarterly (leadership):** channel ROI, share-of-voice vs competitors, strategy shifts,
  budget reallocation, annual forecast update.

## Cross-Channel Integrations

- **→ content-marketing:** keyword map and content gaps feed the editorial calendar;
  SEO briefs become blog/whitepaper productions.
- **→ sem-ppc:** high-CTR paid queries reveal conversion-ready keywords to target
  organically; PPC landing pages share CRO learnings.
- **→ social-media-marketing:** published content needs distribution; social engagement
  data signals topics worth expanding.
- **→ web-analytics:** SEO reporting depends on GA4 event/conversion configuration and
  attribution models.
- **→ cro:** top organic landing pages are the highest-leverage CRO test candidates.
- **← email-marketing:** email drives return visits and branded search, lifting SEO;
  newsletters redistribute new content.
- **← display-advertising / remarketing-retargeting:** paid exposure to non-converting
  visitors recovers demand that organic alone would lose; high-traffic organic pages feed
  retargeting audience pools.
- **→ influencer-marketing:** digital-PR link assets double as influencer briefing
  material; co-created content earns both links and reach.
