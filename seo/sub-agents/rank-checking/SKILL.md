---
name: seo-rank-checking
description: Tracks keyword positions and SERP visibility over time across devices and locations, attributes movement to causes, and alerts on money-keyword losses. Use this skill whenever the user wants rank tracking, position monitoring, "where do we rank for X", visibility share reporting, algorithm-update impact assessment, or before/after measurement of SEO changes — even if they just ask "did our rankings change".
---

# Rank Checking — SEO Sub-Agent

## Role & Mission

Track keyword positions and SERP visibility over time, accurately enough to drive
decisions. This agent owns the tracked keyword universe, scope settings (device,
location), movement attribution, and anomaly alerts. Rankings are a diagnostic —
the mission is turning daily position noise into clear signals: what moved, why,
and who needs to act on it.

## When to Use

- "Track our rankings" or set up ongoing position monitoring
- Measure the impact of a publish, optimization, or link campaign
- Quantify the blast radius of an algorithm update or site migration
- Weekly/monthly reporting needs movement data for the pack
- "Where do we rank for {keyword}?" from sales or leadership
- Competitor position comparison on the shared keyword set

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Tracked keyword list | Yes | Money terms + P1/P2 from keyword-research |
| Device & location scope | Yes | US desktop+mobile; city-level for local |
| Rank tracker access | Yes | Ahrefs Rank Tracker, Semrush Position Tracking |
| Change log (publishes, optimizations, migrations) | Preferred | From on-page/content/technical work |
| Baseline positions | Yes | First run establishes the reference point |
| Competitor keyword set | Optional | Shared terms for visibility comparison |

## Output Contract

Return a rank report: (1) movement summary (gainers/losers, distribution), (2)
position distribution across top 3/10/50, (3) notable-moves table with attribution
hypotheses, (4) volatility annotations (Google updates, SERP feature changes), and
(5) alerts routed to owners. A tracker-style JSON payload:

```json
{
  "date": "2025-07-01",
  "scope": { "location": "US", "device": "mobile" },
  "summary": { "tracked": 420, "top3": 38, "top10": 121, "top50": 305,
               "gainers": 47, "losers": 22, "new": 6, "dropped": 2 },
  "notable_moves": [
    { "keyword": "hr payroll software", "was": 14, "now": 9,
      "url": "/payroll-software", "hypothesis": "title rewrite shipped 06-24" },
    { "keyword": "onboarding checklist", "was": 8, "now": 21,
      "url": "/blog/onboarding-checklist",
      "hypothesis": "competitor refresh entered top 3; needs triage" }
  ],
  "alerts": [ { "keyword": "payroll pricing", "was": 5, "now": 12,
                "owner": "on-page-optimization" } ]
}
```

## Workflow

1. Define the tracked universe with keyword-research: all money keywords, P1/P2
   targets, and quick wins — track what maps to decisions, because per-keyword
   costs scale fast.
2. Set scope precisely: country/city, language, and desktop vs mobile as separate
   tracked contexts; mixed scopes produce averages that describe nothing.
3. Capture a 7-day baseline before judging anything — daily variance is normal and
   single-day comparisons manufacture false alarms.
4. Schedule checks: weekly for the core set, daily for money keywords during
   campaigns, migrations, or high-volatility windows.
5. Annotate the timeline continuously: publishes, optimizations, redirect work,
   and confirmed Google updates (name and date) joined to the position history.
6. Segment movement by template, intent cluster, device, and location —
   aggregate-only views hide cluster-wide problems until they are expensive.
7. Flag anomalies: money terms losing 5+ positions, mass movement across one
   template, and SERP feature changes (AI Overviews, local packs) displacing
   organic results without a true position loss.
8. Cross-verify significant moves in Search Console (impressions and CTR) before
   escalating; trackers estimate, GSC corroborates.
9. Deliver the movement report to reporting on cadence, route loser URLs to
   on-page-optimization or content-creation for triage, and keep the alert list
   owned — no alert without an owner and a deadline.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Rank tracking (primary) | Ahrefs Rank Tracker, Semrush Position Tracking | Weekly auto-checks + on-demand |
| Truth-checking | Google Search Console Performance | Free; corroborate big moves |
| Local rank grids | BrightLocal, Whitespark, Local Falcon | Grid scans beat city averages |
| SERP volatility context | Semrush Sensor, MozCast (free) | Attribute movement to updates |
| Dashboards & digests | Looker Studio, Google Sheets | Automated weekly snapshots |
| SERP feature tracking | Ahrefs/Semrush SERP features reports | Watch AI Overviews and local packs |

## Example AI Prompt

```text
You are an SEO rank analyst. Analyze this rank-tracker export for {SITE}
(scope: {LOCATION/DEVICE}, period {RANGE}, {N} keywords). Confirmed Google
updates in the window: {UPDATE NAMES/DATES}. Our changes: {CHANGE LOG}.

Tasks:
1. Movement summary: top-3/top-10 counts vs prior period, biggest gainers and
   losers with URLs.
2. Attribution per notable move: our change, Google update, competitor action,
   SERP feature shift, or unexplained (flag for investigation).
3. Segmented view: movement by page template and intent cluster; call out any
   cluster-wide declines.
4. Alerts list: money keywords that lost 5+ positions, each with the URL and a
   suggested owner (on-page vs content vs technical).
5. Five plain-English bullets for the monthly report — outcomes first, losses
   included, no metric without a "so what".
Do not average away losses; surface wins and declines with equal weight.
```

## Edge Cases & Guardrails

- Rankings are personalized, localized, and volatile: never report a single position
  as fact — report distributions and ranges, with device and location stated.
- SERP features can shrink organic clicks at the same position (AI Overviews, local
  pack, shopping carousels); track feature presence, not just blue-link rank.
- Position is not traffic: a #4 with a weak title can underperform a #7 with a
  strong one — pair rank data with Search Console CTR before judging.
- Never mix device or location scopes in one average; mobile and desktop rankings
  diverge materially on many queries.
- Trackers sample from data-center locations; hyper-local pack rankings need grid
  tools (Local Falcon, BrightLocal), not city-level estimates.
- Rank tracking without a change log is trivia: movement attribution requires the
  annotation discipline to be kept live, not reconstructed after the fact.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Tracked keywords in top 10 | Growing quarter over quarter (20–30% of set) | Stagnant or shrinking share |
| Money keywords in top 3 | 25–40% of money terms | Key revenue terms stuck on page 2 |
| Anomaly triage time | Losses routed within 7 days | Weeks of unattributed decline |
| Tracker vs GSC consistency | Directionally aligned | Persistent contradictions unexplained |
| Alert coverage | 100% of alerts have owner + deadline | Dashboard nobody acts on |
| Tracking scope accuracy | Device/location split matches business footprint | One blended global average |

## Handoffs

- → **reporting:** deliver the weekly/monthly movement data and attribution notes.
- ← **keyword-research:** receives the tracked universe and baseline positions.
- → **on-page-optimization:** route loser URLs in positions 5–15 for optimization.
- → **content-creation / technical-seo:** route cluster-wide declines and
  template-level crashes for deeper diagnosis.
- ↑ **seo-agent:** escalate algorithm-update events and money-term collapses
  immediately — these trigger recovery workflows at hub level.
