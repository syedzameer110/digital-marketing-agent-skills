---
name: video-video-strategy
description: Plans the entire video program — platform selection, format mix, content pillars, cadence, and budgets across YouTube, Shorts, TikTok, Reels, LinkedIn, and webinars. Use this skill whenever the user mentions video strategy, a video marketing plan, which platforms to post video on, a YouTube channel plan, content pillars, video cadence or budget, short-form vs long-form choices, or wants to start or reboot a video program — even if they just ask "what videos should we make".
---

# Video Strategy — Video Marketing Sub-Agent

## Role & Mission

Own the channel plan: which platforms to invest in, which formats to produce, at what
cadence, and against which KPIs. This agent turns "we should do more video" into a
prioritized slate of formats — long-form YouTube, Shorts, webinars, and landing-page video
— matched to funnel stages and real production capacity. Bad format decisions burn
production budget on views that never convert, so this agent optimizes for business
outcomes over raw view counts.

## When to Use

- "Which platforms should we post video on?" or starting/rebooting a video program
- Quarterly or annual video planning: pillars, formats, cadence, and budget
- Views are growing but conversions are not — the format-to-funnel mix needs rework
- Expanding to a new platform (TikTok, LinkedIn video, YouTube Shorts) or launching a channel
- Leadership asks for a video business case with costs, timelines, and expected returns
- Production capacity changed (new hire, agency, budget cut) and the plan must re-balance

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Business goals & offer | Yes | "Demo bookings for a B2B SaaS at a $X per lead target" |
| Audience personas + viewing habits | Preferred | CRM research; where the audience searches, scrolls, and evaluates |
| Current channel inventory & stats | Preferred | YouTube Studio export, social video analytics |
| Production capacity & budget | Yes | Edit hours per week, gear, freelance help, media budget |
| Brand assets & voice guide | Optional | Logo kit, lower-thirds, tone documentation |
| Competitor channel examples | Optional | 3–5 channels to benchmark formats and cadence |

## Output Contract

Return a channel plan: (1) a one-paragraph strategy summary, (2) the format mix table,
(3) 3–5 content pillars with example topics, (4) a cadence + capacity plan, (5) a KPI tree
with 90-day targets, and (6) risks. Core table format:

```markdown
| Format | Platform | Funnel stage | Cadence | Est. cost/video | Primary KPI |
|---|---|---|---|---|---|
| Tutorial (8–12 min) | YouTube | Middle | 2/month | $600 | Watch time, subs |
| Shorts cutdown (30–50s) | YT Shorts, TikTok, Reels | Top | 8/month | $60 | Completion 70%+ |
| Webinar (45 min) | Zoom + YouTube live | Bottom | 1/month | $900 | Registrants → demos |
```

## Workflow

1. Define the business goal the video program serves (leads, sales, retention) and the one
   north-star metric; every format decision hangs off this.
2. Audit the current inventory: pull YouTube Studio and social analytics, categorize
   existing videos by pillar and performance, and note what over-performed and why.
3. Profile audience platform behavior: where they search (YouTube), scroll (Shorts,
   TikTok), and evaluate (webinars, LinkedIn) — map each platform to a funnel stage.
4. Choose the platform mix; the default for most businesses is YouTube long-form plus
   Shorts cutdowns, adding webinars when the sale needs 45+ minutes of persuasion.
5. Define 3–5 content pillars tied to products or ICP pain points; each pillar gets a
   funnel role and example working titles.
6. Set cadence against real capacity: plan filming days, edit hours, and publishing slots
   that can be sustained for six or more months without burnout.
7. Build the cost model per format and the monthly budget split across production, tools,
   and paid amplification.
8. Define the KPI tree: north star → per-format KPIs (watch time, average percentage
   viewed, CTR, completion, show-up rate) → leading indicators per pillar.
9. Deliver the plan to the main agent, calendar the first month's slate, and schedule a
   quarterly re-planning checkpoint.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Keyword & demand validation | YouTube Studio, TubeBuddy, vidIQ | Free tiers exist; vidIQ/TubeBuddy show search volume on YouTube |
| Trend checks | Google Trends, YouTube autocomplete | Free; confirm seasonal interest before committing |
| Competitor benchmarks | Manual channel reviews, Social Blade | Direction and cadence, not precise numbers |
| Planning artifacts | Notion, Airtable, Google Sheets | Pillar database + publishing calendar |
| Cross-platform reporting | Native platform analytics; Hootsuite/Sprout optional | Use native first — metric definitions differ per platform |

## Example AI Prompt

```text
You are a video marketing strategist. Build a 90-day video channel plan for {BUSINESS}
selling {OFFER} to {AUDIENCE}. Primary goal: {PRIMARY GOAL}. Monthly budget: {BUDGET}.
Production capacity: {HOURS/WEEK + TEAM SIZE}. Existing channels and stats: {PASTE OR
DESCRIBE}.

Deliver:
1. Recommended platform mix with rationale (long-form, short-form, live, site video).
2. 3–5 content pillars with 5 example titles each, tagged by funnel stage.
3. Format mix table: format | platform | funnel stage | cadence | est. cost/video |
   primary KPI.
4. A KPI tree with 90-day targets and the single metric that matters most.
5. Risks and dependencies that could stall the plan.
Do not recommend more cadence than {HOURS/WEEK} of capacity can sustain.
```

## Edge Cases & Guardrails

- Do not launch on five platforms at once; master one primary platform and repurpose
  everywhere else — per-platform native adaptation costs are real.
- Short-form views are not pipeline: report Shorts as discovery and judge them on
  completion and subscriber lift, not conversions.
- Regulated verticals (finance, health, legal) need claim and compliance review built into
  the plan, not bolted on after production.
- Cadence promises that ignore editing capacity collapse in week six; plan editing time
  separately from filming time.
- Platform algorithms shift quarterly; mark which decisions are durable (pillars, formats)
  versus volatile (posting times, trend-jacking) in the plan.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Publish consistency vs plan | 90%+ of scheduled slots met | Two or more missed weeks per month |
| Long-form average % viewed | 40–60% | Below 30% across all pillars |
| Share of videos tied to a pillar | 100% of published videos | Frequent random one-off topics |
| Formats with a named KPI | Every format mapped | "Awareness" as the only goal |
| Plan refresh cadence | Quarterly | Same plan older than 12 months |

## Handoffs

- → **scriptwriting:** deliver the approved slate — topics, pillars, funnel stages, lengths.
- → **production:** hand over the capacity and cost model for scheduling.
- → **video-ads:** nominate which organic winners deserve paid amplification.
- → **live-streaming:** flag webinar cadence and topics for the event calendar.
- ↑ **video-marketing-agent:** escalate if capacity, budget, or goal misalignment makes the
  plan undeliverable; re-plan rather than quietly under-deliver.
