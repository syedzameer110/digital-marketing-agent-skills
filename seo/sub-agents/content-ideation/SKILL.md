---
name: seo-content-ideation
description: Brainstorms and prioritizes SEO content topics from keyword data, trends, sales calls, and competitor gaps, then maps them into a funnel-staged editorial calendar with formats, owners, and publish dates. Use this skill whenever the user asks what to write about next, wants a blog or content calendar, needs new content ideas, topic clusters, linkable asset concepts, or says "give me content ideas for SEO" — even if they never mention keywords explicitly.
---

# Content Ideation — SEO Sub-Agent

## Role & Mission

Convert validated keyword data and voice-of-customer signals into a prioritized content
roadmap. This agent owns the bridge between keyword-research (what people search) and
content-creation (what we ship): every topic it proposes carries a target keyword, a
funnel stage, a format, and a business goal. Poor topic selection burns months of writer
time, so the mission is decision quality — fewer, better topics that rank and convert.

## When to Use

- "What should we write about next?" or planning a monthly/quarterly content calendar
- Keyword research is complete and topics need to be mapped before production
- Organic growth has stalled and the content inventory needs new angles or refreshes
- The link team needs linkable assets (tools, studies, templates) worth pitching
- Entering a new topic cluster, service line, or audience segment
- Sales and support keep answering the same questions that content could absorb

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Keyword map with P1/P2 clusters | Yes | Output of keyword-research sub-agent |
| Audience personas / ICP | Yes | Content strategy docs, CRM segments |
| Existing content inventory | Preferred | CMS export or Screaming Frog URL list |
| Business priorities for the quarter | Preferred | "Push payroll integration launch in Q3" |
| Sales/support/FAQ themes | Optional | Gong/Chorus transcripts, ticket logs |
| Seasonality & industry events | Optional | Google Trends, trade show calendars |

## Output Contract

Return a content roadmap containing: (1) a short summary of the strategic themes chosen,
(2) a topic backlog table sorted by priority, (3) a publish calendar with owners and
effort, (4) 2–3 linkable-asset concepts for outreach, and (5) refresh candidates from
the existing inventory. Core backlog format:

```markdown
| # | Topic / working title | Target keyword | Funnel | Format | Effort | Priority | Publish |
|---|---|---|---|---|---|---|---|
| 1 | 2025 Payroll Compliance Checklist (template) | payroll compliance checklist | MOFU | Free template | M | P1 | Week 2 |
| 2 | How to Automate Employee Onboarding (7 steps) | how to automate onboarding | MOFU | Guide + screenshots | M | P1 | Week 3 |
| 3 | Best HR Software for Startups (compared) | best hr software for startups | BOFU | Comparison post | L | P1 | Week 4 |
```

Rules: one primary keyword per topic, one funnel stage per topic, and no topic that
duplicates an existing URL — propose a refresh instead.

## Workflow

1. Pull the keyword map from keyword-research and confirm which P1/P2 clusters are
   unlocked for production; note any quick-win terms needing refreshed pages.
2. Inventory existing content (CMS export or crawl) and tag duplicates, decaying
   traffic, and gaps — refresh candidates count as pipeline, not wasted slots.
3. Expand beyond the keyword tool: mine People Also Ask, AlsoAsked, Reddit/Quora
   threads, sales-call transcripts, support tickets, and review sites for real
   customer language and unanswered questions.
4. Check trend and timing signals in Google Trends and industry news; flag topics
   with seasonal windows or freshness pressure.
5. Map every candidate topic to a funnel stage (TOFU/MOFU/BOFU), a business goal,
   and a format that matches the live SERP (guide, comparison, template, tool,
   calculator, video, original-data piece).
6. Conceptualize 2–3 linkable assets — original surveys, free tools, definitive
   resources — sized against what earns links in this niche (check competitor
   most-linked pages).
7. Prioritize by business value × winnability × effort, and sequence a calendar
   with realistic dates, owners, and dependencies (design, dev, SME review).
8. Reserve 10–20% of calendar slots for reactive content (news, updates, trends)
   so the plan survives contact with the market.
9. Hand the briefs queue to content-creation, register new target keywords with
   rank-checking, and log the roadmap for reporting to track delivery.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Keyword-based topic mining | Ahrefs Content Explorer, Semrush Topic Research | Paid; bulk topic ideas with traffic data |
| Question discovery | AlsoAsked, AnswerThePublic, Google PAA | Free tiers; map question trees per cluster |
| Community listening | Reddit, Quora, niche Slack/Discord groups | Free; surface real phrasing and pains |
| Trend validation | Google Trends, Exploding Topics | Free/limited free; check seasonality |
| Voice-of-customer mining | Gong, Chorus, support desk exports | Transcripts reveal BOFU language tools miss |
| Backlog & calendar | Google Sheets, Notion, Trello | Sheets suffices with priority formulas |

## Example AI Prompt

```text
You are an SEO content strategist. Build a {TIMEFRAME} content roadmap for
{BUSINESS} ({URL}), audience {ICP}, goal {CONVERSION GOAL}.

Keyword clusters to cover: {PASTE P1/P2 CLUSTERS}
Existing content inventory: {PASTE URLS + TRAFFIC}
Business priorities: {QUARTERLY PRIORITIES}
Voice-of-customer notes: {SALES CALL THEMES / SUPPORT FAQ}

Deliver:
1. 15–25 topics mapped to funnel stage, each with one primary keyword, working
   title, format matched to the SERP, and business goal.
2. A prioritized calendar with effort (S/M/L), owner role, and publish week.
3. 2–3 linkable asset concepts (original data, tool, template) for outreach.
4. Refresh candidates from the existing inventory worth updating first.
5. Exclusions: obvious ideas you rejected and why (too competitive, no volume,
   duplicate of an existing page).
Do not propose two topics targeting the same primary keyword.
```

## Edge Cases & Guardrails

- Ideation volume is not value: every topic must name a business goal; a backlog of
  100 unprioritized ideas is a defect, not an asset.
- One primary keyword per topic — merging overlapping ideas into stronger pillars
  beats shipping thin competing pages.
- Trend topics decay fast; cap them at 10–20% of the calendar unless the niche is
  genuinely news-driven, and never let them displace money-page work.
- YMYL and regulated niches (health, finance, legal) need SME review built into the
  brief stage — flag those topics at ideation, not after drafting.
- AI Overviews and rich results compress organic clicks for simple informational
  queries; favor topics needing experience, tools, data, or depth.
- Do not cannibalize: check the inventory before greenlighting; if a page exists,
  the default answer is refresh, not a competing URL.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Topics accepted into calendar | ≥70% of proposals survive review | Constant rework or rejections |
| TOFU:MOFU:BOFU mix | ~40/30/30 for growth-stage programs | >70% TOFU with no conversion path |
| Calendar hit rate (shipped as scheduled) | ≥85% of dated topics | Slippage beyond one month |
| New pages indexed within 30 days | >80% of published URLs | Mass "crawled – not indexed" pages |
| Refresh share of output | 10–20% each quarter | Zero refreshes while existing pages decay |

## Handoffs

- → **content-creation:** deliver the briefs queue (topic, keyword, outline notes,
  format, deadline) in priority order.
- → **backlink-building:** hand over linkable-asset concepts before they are built
  so outreach angles shape the asset itself.
- → **rank-checking:** register every new target keyword when a topic is scheduled.
- ← **keyword-research:** receives the cluster map and quick-wins list as raw input.
- ↑ **seo-agent:** escalate when the niche's addressable topic demand is too thin
  to support traffic goals — the strategy needs revisiting, not more ideas.
