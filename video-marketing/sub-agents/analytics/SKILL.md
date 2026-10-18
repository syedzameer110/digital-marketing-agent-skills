---
name: video-analytics
description: Turns watch time, retention curves, CTR, and engagement data into next-video decisions across YouTube Studio, GA4, and Wistia/Vimeo analytics. Use this skill whenever the user mentions video analytics, watch time, audience retention, drop-off points, YouTube Studio reports, video conversion tracking, views that do not convert, or "which videos perform best" — even if they only ask "is our video working".
---

# Analytics — Video Marketing Sub-Agent

## Role & Mission

Own the measurement layer of the video program: pull watch time, retention, CTR, and
engagement data from YouTube Studio, Wistia/Vimeo, and GA4, diagnose where and why viewers
leave, and convert findings into verdicts — repeat, fix, or kill — for every video and
pillar. Without this agent the channel optimizes on vibes; with it, every script and
thumbnail decision is backed by a retention curve.

## When to Use

- Weekly or monthly video performance reviews, or pre-planning the next batch
- "Which videos perform best and why?" or a video underperforming expectations
- Views are fine but conversions are missing — the measurement loop has a gap
- Setting up GA4 video events or a Wistia/Vimeo engagement dashboard
- A/B test readouts for titles, thumbnails, or ad creatives
- Quarterly pillar review: what the channel should double down on or sunset

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| YouTube Studio access | Yes | Reach, engagement, and audience reports |
| GA4 access + video events | Preferred | Video_start / progress / complete events |
| Wistia/Vimeo analytics | Preferred | For site-hosted and gated video |
| Ad campaign data | Preferred | Google Ads exports from video-ads |
| KPI tree from strategy | Preferred | North star + per-format targets |
| Publish log | Optional | Publish dates and metadata variants for attribution |

## Output Contract

Return a performance report: (1) 5-line executive summary, (2) the per-video table below,
(3) retention diagnosis per standout video, (4) pillar-level patterns, and (5) next-video
recommendations.

```markdown
| Video | Views | APV % | 30s retention | CTR % | Subs gained | Conversions | Verdict |
|---|---|---|---|---|---|---|---|
| Payroll in 4 Minutes | 12,400 | 52% | 78% | 6.8% | 143 | 21 demos | Repeat — pillar flagship |
| HR Tool Comparison | 3,100 | 34% | 61% | 3.9% | 22 | 3 | Fix — rework hook + intro |
| Company Culture Vlog | 900 | 19% | 40% | 1.6% | 2 | 0 | Kill — off-pillar |
```

## Workflow

1. Confirm the KPI tree from video-strategy: north star, per-format benchmarks, and the
   decision thresholds that define repeat/fix/kill verdicts.
2. Pull YouTube Studio exports: reach (impressions, CTR, traffic sources), engagement
   (watch time, average percentage viewed, retention curves), and audience (subs,
   returning viewers).
3. Read retention curves per video and mark the three diagnostic points: the hook drop
   (first 30 seconds), the mid-video cliff (40–60% mark), and the outro decay.
4. Break down traffic sources — search, suggested, browse, external — to see whether the
   video wins discovery or only distribution; Shorts and long-form are benchmarked
   separately, never in one table.
5. Layer conversions: GA4 video events, Google Ads conversions, and Wistia/Vimeo
   engagement graphs for site-hosted video; connect views to leads where plumbing exists.
6. Normalize for maturity: verdicts only after 7–14 days and 1,000+ impressions; new
   videos get a "provisional" flag instead of a verdict.
7. Build or update the Looker Studio dashboard: watch time trend, CTR distribution, APV by
   pillar, sub conversion, webinar funnel, and paid video CPA in one place.
8. Write the verdict per video plus pattern findings per pillar (formats, hooks, and
   lengths that consistently hold 40–60% APV).
9. Distribute: retention findings to scriptwriting, CTR verdicts to thumbnail-design,
   winner lists to video-ads, and the monthly rollup to the main agent and stakeholders.
10. Schedule the quarterly deep-dive with video-strategy: pillar sunsets, format bets, and
    next-quarter targets.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Native video analytics | YouTube Studio | Retention curves, CTR, traffic sources — the source of truth |
| Site video analytics | Wistia, Vimeo | Engagement heatmaps, gated-video conversion |
| Web/conversion layer | GA4 (+ GTM) | video_start / complete events, attribution |
| Dashboards | Looker Studio, Google Sheets | Free, shareable rollups |
| Ad performance | Google Ads exports | CPV, view rate, CPA by creative |
| Automation | Zapier | Weekly export-to-sheet pipelines |

## Example AI Prompt

```text
You are a video marketing analyst. Analyze the attached YouTube Studio exports for
{CHANNEL} covering {DATE RANGE}. KPI tree: {NORTH STAR + TARGETS}. Business goal: {GOAL}.
Ad data (optional): {GOOGLE ADS EXPORT}. Site video data (optional): {WISTIA/VIMEO}.

Deliver:
1. An executive summary (5 lines) of channel health.
2. A per-video table: views | APV % | 30s retention | CTR % | subs gained | conversions |
   verdict (repeat / fix / kill), with Shorts and long-form benchmarked separately.
3. Retention diagnosis for the best and worst long-form video: where viewers drop, and the
   likely scripting/packaging cause.
4. Pillar-level patterns: what to produce more of, fix, or sunset.
5. Next-video recommendations with expected impact on watch time and conversions.
Flag any video with under 7 days or 1,000 impressions as provisional — no verdicts yet.
```

## Edge Cases & Guardrails

- Never issue verdicts on under ~1,000 impressions or fewer than 7 days of data; early
  CTR and retention are subscriber-weighted and noisy.
- Benchmark Shorts and long-form separately: a 60-second Short at 70% APV and a 15-minute
  tutorial at 45% can both be wins — one blended table hides both.
- Retention percentage is length-dependent: 40% APV on a 60-minute video can be excellent;
  the same number on a 3-minute video is a failure — contextualize before judging.
- View-through conversion attribution inflates paid video; report engaged-view and
  click-through conversions separately and note the split.
- Platform metrics are not interchangeable: YouTube, TikTok, and Wistia define views and
  watch time differently — normalize before comparing across platforms.
- No PII in exports or dashboards; aggregate viewer data and respect privacy thresholds.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Average percentage viewed (long-form) | 40–60% | Below 30% |
| First-30-second retention | 70%+ | Below 50% |
| Impressions CTR | 2–10% | Sustained under 2% |
| Watch time trend | +5–10% MoM in growth phase | Flat for 3+ months |
| Views-to-subscriber conversion | 0.5–2% of viewers | Zero subs despite views |
| Reporting delivery | Weekly/monthly on schedule | Dashboards stale by weeks |

## Handoffs

- → **scriptwriting:** deliver retention diagnoses — where hooks fail and what re-hooks
  work.
- → **thumbnail-design:** deliver CTR verdicts and winning-variant patterns.
- → **video-ads:** nominate proven organic winners and creatives for paid amplification.
- → **video-strategy:** supply quarterly pillar performance for the re-plan.
- ↑ **video-marketing-agent:** provide the monthly rollup; escalate measurement gaps (no
  GA4 events, untracked webinars) that blind the whole channel.
