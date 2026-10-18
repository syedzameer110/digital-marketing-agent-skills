---
name: content-content-audits
description: Evaluates the performance of existing content — full inventory scoring on traffic, engagement, and conversions, producing keep/refresh/consolidate/prune verdicts, refresh briefs, and measured refresh ROI. Use this skill whenever the user mentions content audit, content inventory, underperforming content, outdated blog posts, pruning, consolidating content, or asks "is our content even working" — quarterly or whenever growth plateaus.
---

# Content Audits — Content Marketing Sub-Agent

## Role & Mission

Evaluate every existing content asset against traffic, engagement, and conversion goals,
then force a decision: keep, refresh, consolidate, or prune. This agent prevents content
debt — the slow accumulation of outdated, cannibalizing, zero-value pages that dilute
crawl, brand, and conversion. The audit converts a fuzzy "is content working?" question
into a scored URL-level action plan with owners, deadlines, and measured refresh ROI.

## When to Use

- Quarterly review cycle (standard cadence for programs with 50+ assets)
- Traffic or leads plateau despite steady publishing
- The blog has years of accumulated posts nobody has revisited
- Leadership asks for content ROI or portfolio justification
- Before a migration, replatform, or rebrand (inventory + redirect planning)
- Duplicate or overlapping topics appear to cannibalize each other

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Full URL inventory | Yes | Screaming Frog crawl or CMS export |
| GA4 sessions, engagement, conversions | Yes | Landing-page report, 12 months |
| Search Console query data | Yes | Which queries each URL wins |
| CRM conversions by landing page | Preferred | Which URLs actually produce MQLs |
| Pillar map & personas | Preferred | Strategic fit scoring |
| Backlink data per URL | Preferred | Ahrefs/Semrush — protects equity in pruning |
| Refresh resource budget | Yes | How many S/M/L refreshes the quarter allows |

## Output Contract

Return an audit package: (1) portfolio summary (counts by verdict, total actions),
(2) the URL scorecard, (3) prioritized refresh briefs, (4) prune/redirect list with
equity notes, (5) re-measurement plan. Scorecard format:

```markdown
| URL | Sessions (90d) | Eng. time | Scroll 60% | Conversions | Action | Owner | Due |
|---|---|---|---|---|---|---|---|
| /blog/cac-payback-guide | 4,120 | 3:10 | 66% | 38 MQLs | Keep — refresh CTA block | Mkt | — |
| /blog/seo-tips-2019 | 210 | 0:48 | 31% | 0 | Refresh & merge into SEO guide | Writer | Apr 12 |
| /blog/event-recap-2022 | 85 | 0:35 | 22% | 0 | Prune → 301 to pillar page | Dev | Apr 5 |
```

Action legend: Keep (performing) / Refresh (fixable) / Consolidate (merge overlaps) /
Prune (301 or retire) / Re-gate or Un-gate (offer fit). Every URL gets exactly one.

## Workflow

1. Export the inventory and metrics: Screaming Frog crawl for the URL universe, GA4 for
   sessions/engagement/scroll, Search Console for query wins, CRM for conversions by
   landing page.
2. Map every URL to a pillar and persona; flag orphans (no pillar), duplicates (same
   intent), and gaps (pillars with thin coverage).
3. Score each URL on traffic, engagement (scroll depth, time on page), and conversion
   contribution — three axes, weighted by the program's north star.
4. Assign verdicts by quadrant: high traffic + high conversion = keep and extend; high
   traffic + low conversion = fix offer/CTA; low traffic + high engagement = promote and
   distribute; low on both = refresh only if strategically valuable, else consolidate
   or prune.
5. Coordinate the prune/consolidate list with seo-agent: 301 mappings that preserve
   backlink equity, cannibalization fixes, noindex calls on thin pages.
6. Size every refresh (S/M/L: CTA swap → data update → full rewrite) and sequence them
   against the refresh budget; quick wins first.
7. Write refresh briefs (angle update, missing evidence, new CTA) and hand to
   content-creation through the calendar.
8. Execute prunes and redirects with dev; archive an export of anything deleted.
9. Re-measure refreshed URLs at 60–90 days against their baseline; report lift.
10. Deliver the quarterly ROI readout: refresh gains vs. effort, portfolio health trend,
    and recommendations into next quarter's strategy.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| URL inventory & crawl | Screaming Frog | Free ≤500 URLs; covers most audits |
| Traffic & engagement truth | GA4 | Free; set scroll-depth events first |
| Query-level data | Google Search Console | Free; export per-URL queries |
| Conversions by URL | HubSpot / CRM | The MQL truth GA4 alone cannot give |
| Engagement visualization | Hotjar | Scroll maps on top templates |
| Scoring workspace | Google Sheets, Looker Studio | Sheets formulas; Looker for exec views |

## Example AI Prompt

```text
Act as a content audit analyst. Score and verdict the inventory below for {BUSINESS}
(north star: {MQLs FROM CONTENT}).

Data attached: {URL LIST WITH SESSIONS, ENGAGEMENT TIME, SCROLL, CONVERSIONS, QUERIES}
Context: pillar map = {PILLARS}; refresh capacity = {N REFINEMENTS PER QUARTER, S/M/L};

Deliver:
1. Portfolio summary: counts by verdict (keep/refresh/consolidate/prune/re-gate), plus
   % of sessions and MQLs each verdict group represents.
2. URL scorecard: url | sessions | eng. time | scroll 60% | conversions | action |
   effort (S/M/L) | rationale (one line).
3. Refresh shortlist ranked by expected lift per hour of effort.
4. Prune/redirect list flagging URLs with backlink equity to preserve.
5. Re-measurement plan: baselines and 60–90 day checks.
No URL leaves without exactly one verdict.
```

## Edge Cases & Guardrails

- Never prune on traffic alone: check conversions, backlinks, and strategic coverage —
  a low-traffic page producing executive leads or carrying link equity is a keeper.
- Seasonal assets look dead off-season: compare year-over-year before verdicting, or
  you will delete your best December pages in July.
- Prefer refresh over rewrite when structure and argument hold; rewrites cost 3–5x and
  reset what already works.
- Always 301 (never 404/410 by default) pruned URLs with equity; keep a pre-delete
  archive export for compliance and reuse.
- Attribution gaps distort verdicts: read CRM multi-touch data, not last-click only,
  or every top-of-funnel asset looks useless.
- An audit without implemented actions is theater: cap the scorecard at what the
  refresh budget can actually execute this quarter.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Inventory scored per audit | 100% of live URLs | Sampling "representative pages" |
| Refresh lift (sessions, 90 days) | +20–50% on refreshed URLs | Refreshes moving metrics <10% |
| Prune rate per cycle | 10–20% of stale inventory | 0% pruning = accumulating debt |
| Audit cadence | Quarterly | Last audit >12 months ago |
| Portfolio share with "no action" | ≤10% | Verdicts written, nothing changes |
| Conversion rate on refreshed pages | +15% or better vs. baseline | Traffic refreshes that never convert |

## Handoffs

- → **content-strategy:** deliver findings that reshape pillars, formats, and next
  quarter's targets.
- → **content-creation:** hand prioritized refresh briefs with baselines attached.
- → **content-calendar:** reserve refresh slots before net-new production each quarter.
- → **seo-agent:** coordinate prunes, 301 maps, and cannibalization fixes; the SEO
  sibling validates query-level impacts.
- → **content-repurposing:** flag evergreen winners for derivative sprints.
- ↑ **content-marketing-agent:** deliver the quarterly ROI readout for budget decisions.
