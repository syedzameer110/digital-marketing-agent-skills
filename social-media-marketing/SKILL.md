---
name: social-media-marketing-agent
description: Orchestrates organic and paid social media across Instagram, Facebook, TikTok, LinkedIn, X, YouTube, and Pinterest — strategy, content calendars, post/story/reel creation, community management, social listening, hashtag research, paid campaigns, UGC curation, and analytics reporting. Use this skill whenever the user wants to grow followers or engagement, plan a posting schedule, manage comments or DMs, monitor brand mentions, boost posts, run paid social ads, or names any social platform — even if they never say "social media" explicitly.
---

# Social Media Marketing — Main Agent (Command Hub)

## Channel Overview

Social media marketing builds audience, trust, and demand on the platforms where people
already spend hours daily. It combines an organic engine (content, community, UGC) with a
paid amplifier (Meta, TikTok, LinkedIn, X, Pinterest ads) — the two feed each other, since
organic winners become the cheapest, best-performing ad creative. Unlike SEO, results do
not compound slowly for months: engagement signals move within 2–4 weeks of a consistent
cadence, and paid social can produce clicks and conversions within days. The catch is that
reach is rented from algorithms — which is why this channel works hardest at converting
attention into owned assets (email lists, community, UGC rights). Organic and paid must
run as one system: organic content produces the creative insights, paid scales the proven
winners, and community management protects the brand while both are in motion.

This channel wins when the target audience demonstrably lives on the chosen platforms and
the brand can sustain a native-feeling cadence (4–7 posts/week minimum on core platforms).
It loses to SEM/PPC when demand is urgent and search-based, and it should not carry a
pipeline alone in B2B without LinkedIn focus or paid support. Cost profile: organic is
mostly labor and creative ($1,000–$8,000/month for serious SMB programs), paid social
scales from $500/month in tests to $50,000+ in growth stages, and tooling runs 10–15% of
budget. Expect 60–90 days from program start to a stable, reportable engagement baseline.
Platform mix is a resource decision, not a checkbox: two platforms executed at full
cadence outperform six half-maintained accounts in every measurable way.

## Agent Hierarchy

```text
social-media-marketing-agent (command hub)
└── sub-agents/
    ├── strategy-planning/       → goals, platform selection, pillars, voice, roadmap
    ├── social-listening/        → brand/competitor mentions, sentiment, trends, alerts
    ├── hashtag-research/        → tiered, platform-specific hashtag sets per pillar
    ├── content-calendar/        → dated multi-platform publishing plan + scheduling
    ├── content-creation/        → posts, stories, reels, carousels, threads, video
    ├── community-management/    → comments, DMs, mentions, SLA, crisis triage
    ├── ugc-curation/            → rights-cleared customer content + whitelisting
    ├── paid-social-ads/         → Meta/TikTok/LinkedIn/X/Pinterest campaign engine
    └── analytics-reporting/     → cross-platform KPIs, benchmarks, insights
```

## Sub-Agent Routing Table

| Sub-agent | Call when… | Key inputs | Depends on |
|---|---|---|---|
| strategy-planning | Program kickoff, quarterly review, entering a new platform, or flat engagement with no direction | Business goals, personas, competitor handles, current analytics, resources | None (entry point) |
| social-listening | Need to know what is said about the brand or rivals, track campaign reaction, or catch spikes early | Brand terms + misspellings, competitor handles, category keywords | None (parallel-safe) |
| hashtag-research | New content pillar, declining discovery reach, campaign launch, banned-tag hygiene check | Pillar topics, platform list, account sizes, campaign names | strategy-planning |
| content-calendar | Monthly/weekly planning, campaign timing, cadence slipping, multi-platform repurposing | Pillars, key dates, asset status, platform cadence, team capacity | strategy-planning |
| content-creation | A calendar slot needs copy or assets; repurposing long-form into posts; hooks and video scripts | Calendar entry, brand voice, raw assets, trend notes | content-calendar, hashtag-research |
| community-management | Comments/DMs piling up, complaints, giveaways, ongoing response-time SLA | Inbox access, FAQ, escalation contacts, voice guide | strategy-planning (voice) |
| ugc-curation | Customers posting about the brand, need authentic assets, creator whitelisting for ads | Branded tags/mentions, rights templates, product seeding list | community-management, social-listening |
| paid-social-ads | Amplify organic winners, hit lead/sales targets, retargeting, new-audience tests | Budget, objective, pixel/CAPI, creative, landing pages | content-creation, ugc-curation |
| analytics-reporting | Weekly/monthly/quarterly cycles, "is social working", benchmarking, platform kill decisions | Native analytics exports, paid data, KPI targets | all |

## End-to-End Workflows

### Workflow A — New Brand / Channel Launch (weeks 1–8)

1. Run **strategy-planning** to translate business goals into platform choices, pillars,
   voice, and KPI targets. Output: 90-day strategy brief with a platform scorecard.
2. Run **social-listening** to baseline brand and competitor mention volume, sentiment,
   and recurring themes. Output: theme map + alert queries.
3. Run **hashtag-research** to build tiered tag sets per pillar per platform. Output:
   hashtag library with rotation sets.
4. Feed pillars, cadence, and dates into **content-calendar** and schedule the first four
   weeks. Output: live calendar, 2-week approved buffer.
5. Run **content-creation** to produce the first 20–30 assets (reels, carousels, stories,
   threads) against platform specs. Output: approved asset pack.
6. Switch on **community-management** from day one: sub-4-hour response SLA, escalation
   matrix, proactive engagement. Output: response log + first advocate list.
7. Put $500–$1,500 behind **paid-social-ads** tests on the best early posts to buy
   learning fast. Output: first CTR/CPA/ROAS read by audience and format.
8. Stand up **analytics-reporting** with baseline dashboard; hold week-4 and week-8
   reviews to reallocate platforms, pillars, and budget.
9. Lock the learnings into the next 90-day cycle: kill criteria scored, pillar mix
   adjusted, paid budget shifted toward what the data proved.

### Workflow B — Monthly Organic Growth Engine (recurring)

1. **analytics-reporting** closes last month: what won, what stalled, and why (format,
   topic, hook, timing). Output: ranked recommendations.
2. **social-listening** refresh: new themes, competitor moves, trend candidates. Output:
   5+ content-worthy signals.
3. **strategy-planning** (quarterly touch) tunes pillars and platform mix from the data.
4. **content-calendar** builds next month: slots, hooks, asset briefs, approvals.
5. **content-creation** produces weekly batches; **hashtag-research** keeps tag sets fresh.
6. **ugc-curation** rights-clears and schedules the best customer content (UGC typically
   out-engages brand content by 20–40%).
7. **community-management** runs the daily SLA loop and logs themes back into the calendar.
8. **analytics-reporting** sends the weekly pulse; adopted recommendations are logged
   and scored next cycle, so the loop measures decisions, not just impressions.

### Workflow C — Product Launch Amplification (4-week paid flight)

1. **strategy-planning** writes the launch brief: goal, offer, audiences, success metrics.
2. **content-creation** builds hero assets plus 3–5 hook variants per format.
3. **paid-social-ads** structures prospecting + retargeting campaigns and verifies
   tracking (Pixel/CAPI, TikTok Events API) before spend.
4. **ugc-curation** whitelists 3–5 creators (TikTok Spark Ads, Meta partnership ads) for
   authentic ad creative.
5. **hashtag-research** decides the campaign tag (only if UGC pull-through is realistic).
6. **community-management** runs launch-week rapid response on ad comments and DMs.
7. **analytics-reporting** delivers mid-flight optimization and the wrap report; winners
   get scaled, losers paused within 72 hours.
8. Roll launch learnings into evergreen: winning hooks, audiences, and creators migrate
   into the base prospecting and retargeting programs.

## KPI Dashboard

North-star metric: **social-attributed conversions per month** (leads, sales, signups with
social in the path) — engagement rates are the leading indicator, conversions pay the bills.

| Metric | Source tool | Cadence | Healthy range |
|---|---|---|---|
| Engagement rate | Native insights / Metricool | Weekly | IG 1–5%; LinkedIn 2–6%; X 0.5–1.5%; Facebook 0.5–1.5%; TikTok 4–8% |
| Follower growth | Native insights | Monthly | +2–5%/mo established; +8–15%/mo launch phase |
| Median response time | Sprout Social / Meta Business Suite | Weekly | <4h business hours (target <2h) |
| Non-follower reach share | IG / TikTok insights | Weekly | 25–40% (discovery healthy) |
| Video completion rate | TikTok / Reels analytics | Weekly | 50%+ signals strong creative |
| Paid ROAS / CPA | Ads Managers | Weekly | ROAS 2–4x DTC prospecting; CPA within 120% of target |
| Link-in-bio CTR | Native insights / shortlink stats | Weekly | 0.5–2% of post reach |
| UGC assets rights-cleared | ugc-curation log | Monthly | 8–15 secured/month (SMB) |
| Campaign tag adoption | Branded tag search / listening | Monthly | 20+ organic uses during flight |
| Share of voice | Brandwatch / Mention | Monthly | Trending up vs top 3 competitors |

## Budget Guidance

| Monthly budget | Recommended allocation |
|---|---|
| Under $1,000 | Organic-only: 60% content production time/tools, 25% community management, 15% scheduling/listening tools; skip paid until organic signals a winner |
| $1,000–$5,000 | 45% paid amplification of proven posts, 30% content/creative, 10% UGC or micro-creator seeding, 15% tools |
| $5,000–$15,000 | 55% paid (prospecting + retargeting split), 20% content studio/UGC, 10% listening + community tooling, 15% testing new platforms/formats |
| $15,000+ | 60% multi-platform paid, 20% creative team or agency, 10% listening/enterprise tools, 10% community & experiments |

Allocation principles:

- Let organic be the lab and paid the megaphone: never boost a post that has not earned
  engagement organically or through strong early paid signals.
- On TikTok, creative IS the targeting — reserve 30%+ of paid budget for new creative
  variants, not audience tweaks.
- Cap tooling at 10–15% of total; scheduling and listening subscriptions rarely justify
  more.
- Hold a 10% contingency for trend-jacking moments and launch-week amplification.
- Judge platforms quarterly on contribution, not comfort — consolidate or cut
  underperformers and move budget toward proven engagement quality.

## Team & Agency Mapping

| Activity | Best handled by | Rationale |
|---|---|---|
| Strategy & platform decisions | In-house (founder/marketing lead) | Requires business context and resource authority |
| Calendar & publishing ops | In-house coordinator | Daily rhythm, fast edits, ownership of buffers |
| Content creation | In-house creator or freelancer; agency for volume | Native-feeling content needs brand immersion |
| Community management | In-house (junior) with agency backup | Voice intimacy and escalation speed matter most |
| Social listening | In-house analysis on tool alerts; agency for enterprise scale | Interpretation beats collection |
| Paid social ads | In-house under $5k/mo spend; freelancer/agency above | Media-buying craft pays for itself at scale |
| UGC curation | In-house coordinator | Rights handling and creator rapport are trust work |
| Launch/campaign creative sprints | Freelance creator or agency | Burst capacity beats adding headcount |
| Platform specialists (TikTok, LinkedIn) | Freelancer at scale | Niche craft rotates as the platform mix shifts |
| Analytics & reporting | In-house with automated dashboards | Low marginal effort once Looker Studio exists |

## Reporting Cadence

- **Weekly (in-house, 30 min):** engagement rates per platform vs target, response-time
  SLA, published vs planned posts, paid spend pacing, top/last posts. Decision: next
  week's creative and budget tweaks. Paid pacing and creative-fatigue checks are part
  of the same review.
- **Monthly (stakeholders, 1 hr):** follower and reach growth, engagement trend, UGC
  volume, paid CPA/ROAS vs target, share of voice, theme performance. Decision: pillar
  and platform mix adjustments.
- **Quarterly (leadership):** channel ROI and social-attributed conversions, benchmark
  movement vs competitors, platform kill/scale calls, budget reallocation, next-quarter
  strategy refresh.

## Cross-Channel Integrations

- **→ content-marketing-agent:** social listening themes and top-performing hooks feed
  blog/editorial topics; long-form content returns as carousels, threads, and short video.
- **→ seo-agent:** social distribution drives branded search volume and discovery of
  link-worthy assets; SEO content gets a distribution pass through the social calendar.
- **→ influencer-marketing-agent:** UGC curation hands over vetted creators and rights
  status; influencer deliverables are whitelisted into paid social ads.
- **→ video-marketing-agent:** high-retention Reels/TikTok/Shorts concepts graduate into
  YouTube long-form; long-form video is cut down into platform-native shorts.
- **→ remarketing-retargeting-agent:** engagement audiences (video viewers, page
  engagers, profile visitors) and social clickers feed retargeting pools with frequency
  caps coordinated.
- **← email-marketing-agent:** email captures followers into owned lists; newsletter
  content is atomized into social posts to close the loop.
- **← web-analytics:** GA4 UTM discipline and conversion events define whether social
  engagement turns into measurable revenue.
- **→ cro:** link-in-bio and paid landing pages carry high-intent social traffic and are
  prime CRO test candidates — social visitors behave differently from search visitors.
- **← affiliate-marketing-agent:** affiliate offers and creator promo codes are amplified
  through organic posts; social saves and shares signal which offers deserve more push.
