---
name: video-marketing-agent
description: Owns the end-to-end video marketing workflow — video strategy and platform planning, scriptwriting and storyboards, filming and editing, YouTube SEO, thumbnail design, video ads (in-stream, bumper, in-feed), live streaming and webinars, and watch-time analytics. Use this skill whenever the user mentions YouTube growth, video content, scripts, video production, pre-roll ads, live streams, webinars, thumbnails, or watch time — even if they never say "video marketing" explicitly.
---

# Video Marketing — Main Agent (Command Hub)

## Channel Overview

Video is the highest engagement-per-minute format available to marketers: nothing else
transfers trust, demonstrates products, and holds attention the way moving image and sound
do. YouTube doubles as the world's second-largest search engine, so video compounds like
SEO — a video that ranks keeps earning views, watch time, and subscribers for years at
near-zero marginal cost. The channel runs on two engines: short-form (YouTube Shorts,
TikTok, Reels — 15–60 seconds, cheap to produce, optimized for reach and top-of-funnel
discovery) and long-form (8–20+ minute YouTube videos and webinars — more expensive, but
they build watch time, authority, subscribers, and conversions). Short-form buys attention;
long-form converts it into relationship and revenue.

Costs split three ways: production (a DIY talking-head setup needs $100–$500 in gear;
freelance editing adds $300–$800 per long-form video; agency explainer animation runs
$2,000–$10,000 per finished minute), media (YouTube ads at $0.02–$0.10 CPV for skippable
in-stream), and time (1–2 weeks per long-form video from script to publish, and 3–6 months
of consistent publishing before a channel gains traction — 6–12 months before YouTube
search rankings stabilize). Video wins when trust, demonstration, or education drives the
purchase decision — considered purchases, complex products, founder-led brands, and
communities all benefit — and it underperforms when nobody can commit to publishing
consistently for months, in which case route budget to paid channels instead.

## Agent Hierarchy

```text
video-marketing-agent (command hub)
└── sub-agents/
    ├── video-strategy/           → platform, format & cadence planning
    ├── scriptwriting/            → hook-first scripts, storyboards, run-of-shows
    ├── production/               → filming, animation, editing, multi-format exports
    ├── youtube-optimization/     → titles, descriptions, tags, chapters, playlists
    ├── thumbnail-design/         → click-worthy packaging that wins the CTR battle
    ├── video-ads/                → skippable, non-skippable, bumper & in-feed campaigns
    ├── live-streaming/           → webinars, live events, Q&As
    └── analytics/                → watch time, retention, engagement reporting
```

## Sub-Agent Routing Table

| Sub-agent | Call when… | Key inputs | Depends on |
|---|---|---|---|
| video-strategy | Starting or rebooting a video program, choosing platforms, or quarterly planning | Business goals, audience personas, channel access, budget, capacity | None (entry point) |
| scriptwriting | A topic is approved and needs a script, storyboard, or hook rework | Topic, target keyword, video goal and CTA, brand voice, length | video-strategy |
| production | A script is approved and needs filming, animation, or editing | Approved script, shot list, brand assets, gear/tooling access | scriptwriting |
| youtube-optimization | Before/after any YouTube publish, or when views underperform | Final video file, target keyword, channel Studio access | production |
| thumbnail-design | Every YouTube upload, or when CTR drops below 2% | Final cut, candidate still frames, brand kit | production |
| video-ads | Budget exists to amplify a video, launch a product, or remarket | Hero creative, cutdowns, landing page, budget, conversion tracking | production, thumbnail-design |
| live-streaming | A webinar, Q&A, launch event, or community live is scheduled | Topic, date, speakers, registration platform | scriptwriting |
| analytics | Weekly/monthly reviews, or before planning the next batch of videos | YouTube Studio access, GA4, Wistia/Vimeo hosting analytics | All (terminal node) |

## End-to-End Workflows

### Workflow A — YouTube Channel Launch (weeks 1–10)

1. Run **video-strategy**: audit the existing presence, pick the platform mix (YouTube
   long-form plus Shorts cutdowns as the default), define 3–5 content pillars, and set a
   cadence the team can sustain for six months. Output: channel plan with KPI tree.
2. Hand the pillar map to **scriptwriting**: draft the first three long-form scripts,
   hook-first — the first 30 seconds locked before anything else is written. Output:
   approved scripts + storyboards.
3. Run **production**: batch-film all three in one session (batching cuts cost ~30%), then
   edit to final cuts with captions, and cut 2–3 vertical Shorts per video. Output:
   3 long-form masters + 6–9 Shorts.
4. Run **thumbnail-design** and **youtube-optimization** in parallel on each video:
   packaging (title, thumbnail, chapters, description) is finished before publish day, not
   after. Output: publish-ready uploads.
5. Publish on the agreed cadence; pin a CTA comment and seed early engagement via the
   email list and community tab.
6. After each video has 7–14 days of data, run **analytics**: retention curves, CTR, and
   traffic sources per video. Output: verdicts per pillar — repeat, fix, or kill.
7. Feed verdicts back to **scriptwriting** and **video-strategy**: double down on formats
   that hold 45%+ average percentage viewed; sunset pillars that sit below 30% for two
   consecutive videos.

### Workflow B — Product Launch Video + Paid Amplification (3–4 weeks)

1. **video-strategy** scopes the launch: hero explainer (2–3 min), ad cutdowns, launch
   webinar, and a landing-page video. Output: launch video brief with budget split.
2. **scriptwriting** writes the hero script, the 15s/30s/6s ad cutdowns, and the webinar
   run-of-show in one pass. Output: master script pack.
3. **production** films and edits the hero video, ad cutdowns, and landing-page variants
   in 16:9, 9:16, and 1:1. Output: full launch asset library.
4. **thumbnail-design** produces the hero thumbnail plus distinct ad creative variants for
   split testing. Output: complete packaging set.
5. **video-ads** launches the campaign ladder: skippable in-stream for reach, bumpers
   (6 seconds or less) for frequency, in-feed for consideration, then remarketing to
   hero-video viewers. Output: live campaigns against CPV and CPA targets.
6. **live-streaming** runs the launch webinar; **production** trims the replay into 5–10
   clips; **youtube-optimization** publishes the replay as an evergreen VOD.
7. **analytics** closes the loop: cost per view vs conversions, best-performing hook,
   creative fatigue signals, and the scale/kill recommendation for each campaign.

### Workflow C — Evergreen Webinar Engine (recurring monthly)

1. **analytics** nominates the topic: the highest-retention video themes and YouTube
   search terms with commercial intent. Output: webinar topic shortlist.
2. **scriptwriting** builds the 45-minute webinar script plus a 90-second registration-
   page promo video script.
3. **live-streaming** runs registration (target 35–45% show-up rate), the live event, and
   hands the follow-up sequence spec to email-marketing. Output: executed event + list of
   engaged attendees.
4. **production** edits the replay into a tight 25–30 minute evergreen version plus
   short-form clips. Output: replay asset package.
5. **youtube-optimization** packages the evergreen replay with chapters and end screens.
6. **analytics** reports the registration → show-up → watch → conversion funnel, names the
   best-converting segment, and nominates next month's topic from what the audience
   actually asked during live Q&A.

## KPI Dashboard

North-star metric: **watch time hours from the target audience** — YouTube's ranking
currency and the closest proxy for real attention — tied to conversions through
video-attributed leads and sales.

| Metric | Source tool | Cadence | Healthy range |
|---|---|---|---|
| Watch time (hours) | YouTube Studio | Weekly | +5–10% MoM during growth phase |
| Average percentage viewed (long-form) | YouTube Studio | Weekly | 40–60%; good content still retains 40–60% of viewers at the video midpoint |
| Thumbnail impressions CTR | YouTube Studio | Weekly | 2–10% for long-form; judge Shorts on completion instead |
| Views-to-subscriber conversion | YouTube Studio | Monthly | 0.5–2% of viewers subscribe |
| Engagement rate (likes + comments / views) | YouTube Studio | Monthly | 2–5% |
| Paid view rate / CPV | Google Ads | Weekly | View rate 25–35%; CPV $0.02–$0.10 on skippable in-stream |
| Webinar registration → show-up | Registration platform | Per event | 35–45% |
| Shorts completion rate | YouTube Studio | Weekly | 70%+ (judge Shorts here, not CTR) |
| Returning viewers share | YouTube Studio audience tab | Monthly | 20%+ and rising |
| Video-attributed conversions | GA4 / CRM | Monthly | Trending up; share of total pipeline reported to leadership |

## Budget Guidance

| Monthly budget | Recommended allocation |
|---|---|
| $0–$1,000 | DIY everything: smartphone + lav mic ($100–$300), free editors (DaVinci Resolve, CapCut), Canva thumbnails, no paid media |
| $1,000–$3,000 | 2–4 long-form/month: freelance editor ($300–$800/video), $100–$200 tools, $300–$800 ad testing |
| $3,000–$10,000 | Weekly long-form + Shorts engine: dedicated editor, freelance thumbnail designer, webinar stack, $1,500–$4,000 media |
| $10,000+ | In-house creator/crew or a production retainer plus agency-run YouTube ads; roughly 40–50% media, 40–50% production, 10% tools |

Allocation principles:

- Spend on audio before camera: bad audio kills retention faster than bad image quality.
- The script — especially the first 30 seconds — is the cheapest retention lever; never
  film from an unwritten outline.
- Every long-form video should yield 2–4 cutdowns; cutdowns triple short-form output at
  roughly 10% of the original production cost.
- Reserve 10–15% of budget for thumbnail and hook experiments, plus a 10% contingency for
  a launch or live-event spike.
- Buy editing capacity before buying gear: a $600/month freelance editor outperforms a
  $2,000 one-time camera purchase for the first year.
- Host webinars on hardware you already own (laptop + USB mic) before renting studio time;
  show-up rate and follow-up discipline matter more than production value.

## Team & Agency Mapping

| Activity | Best handled by | Rationale |
|---|---|---|
| Strategy & analytics | In-house | Needs business context, budget authority, and fast iteration loops |
| Scriptwriting | In-house or specialist freelancer | Voice and subject-matter depth beat generic agency scripts |
| Filming & editing | Freelance videographer/editor; agency for animation | Skill-based, episodic work that scales externally |
| YouTube optimization | In-house (checklist + tools) | Routine per upload; TubeBuddy/vidIQ make it procedural |
| Thumbnail design | Freelance designer | High-leverage, low-hours role; cheap to outsource with a style guide |
| Video ads | In-house media buyer or PPC agency | Usually lives beside search/social ads in the same account structure |
| Live streaming | In-house host + producer | On-camera trust is brand-owned; production support can be contracted |

## Reporting Cadence

- **Weekly (in-house, 30 min):** retention curves and CTR of newly published videos, watch
  time trend, ad view rate and CPV. Decision: what the next script and thumbnail test.
- **Monthly (stakeholders, 1 hr):** watch time and subscriber growth vs plan, top and
  bottom videos, webinar funnel, paid video CPA vs other channels, next-month slate.
  Decision: pillar and budget adjustments.
- **Quarterly (leadership):** channel ROI, video-attributed pipeline/revenue, platform mix
  review, competitive channel audit, back-catalog shelf-life review, annual forecast
  update.

## Cross-Channel Integrations

- **→ seo-agent:** YouTube keyword research feeds VideoObject schema and video embeds on
  ranking pages; video transcripts become blog posts; optimized videos can earn Video
  SERP features. Conversely, the seo keyword map tells scriptwriting what to film next.
- **→ social-media-marketing-agent:** every long-form video spawns native clips for
  TikTok, Reels, LinkedIn, and X; the social team redistributes and re-cuts all uploads.
- **→ email-marketing-agent:** webinars and premieres are promoted to the list; replays
  and new uploads become newsletter content; video thumbnails in email lift click-through.
- **→ cro-agent:** testimonial, demo, and explainer videos embedded on landing pages are
  among the highest-leverage CRO assets; page conversion data feeds back into script
  priorities and video selection.
- **← web-analytics-agent:** GA4 video events (start, progress, complete) and attribution
  plumbing make video conversions reportable at the business level.
- **← sem-ppc-agent:** video viewers build remarketing audiences for search and display;
  search query reports surface topics with proven paid demand worth filming.
- **← influencer-marketing-agent:** creator collaborations supply authentic video assets
  and borrowed audiences; whitelisted creator videos often outperform brand-produced ads.
- **← cro-agent (reverse flow):** landing-page video completion and conversion lift tell
  the video team which messages deserve expansion into full productions.
