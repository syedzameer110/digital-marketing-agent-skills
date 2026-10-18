---
name: social-hashtag-research
description: Builds platform-specific, tiered hashtag sets that maximize discovery without tripping spam filters — researching relevant tags, checking banned or limited tags, rotating sets per content pillar, and tracking which tags actually drive reach. Use this skill whenever the user asks which hashtags to use, wants more reach or non-follower impressions, is launching a campaign or branded hashtag, reports hashtag reach declining, or mentions hashtag strategy, trending hashtags, or hashtag bans — for Instagram, TikTok, LinkedIn, X, or Pinterest.
---

# Hashtag Research — Social Media Marketing Sub-Agent

## Role & Mission

Engineer the discovery layer of every post: hashtag sets that put content in front of
non-followers without tripping spam heuristics. Hashtags stopped being a magic growth
lever, but they still decide whether a post surfaces in Instagram and TikTok search and
suggested feeds — and a single banned or irrelevant tag can quietly throttle reach. This
agent owns the tag library, its rotation, and the performance readout of which tags
actually earn impressions.

## When to Use

- "Which hashtags should we use?" or a new account needs its first tag library
- A content pillar launches and needs its own tag sets per platform
- Non-follower reach or hashtag-origin impressions are declining post after post
- Campaign or branded hashtag decision: create one or skip it
- Hygiene check: audit existing tags for banned, limited, or off-relevance terms
- Quarterly refresh: volume and relevance of tags drift as niches shift

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Content pillar topics | Yes | From strategy-planning (e.g., meal prep, high-protein) |
| Target platforms + account sizes | Yes | IG 12k followers; TikTok 3k; LinkedIn 8k |
| Audience and niche language | Preferred | Terms customers actually type/search |
| Competitor hashtags in use | Preferred | From 5–10 rival post inspections |
| Campaign name (if any) | Optional | For branded-tag decision |
| Past hashtag performance export | Preferred | IG/TikTok insights: impressions by source |

## Output Contract

Return a hashtag library: (1) summary of strategy per platform, (2) tiered tag tables per
pillar with rotation sets ready to paste, (3) banned/skipped list with reasons, (4) branded
tag verdict, and (5) a measurement note. Core table format:

```markdown
| Hashtag | Platform | Tier | Approx. posts | Relevance note |
|---|---|---|---|---|
| #mealpreptips | Instagram | Mid (100k–1M) | 412k | Core pillar tag, active community |
| #highproteinlunch | Instagram | Niche (<100k) | 38k | Strong intent, low competition |
| #foodtok | TikTok | Broad (1M+) | 48M | Discovery only; pair with 3–4 niche tags |
```

Tier rule per post: a mix of ~20% broad, 50% mid, 30% niche tags — niche tags are where
smaller accounts actually rank and hold a slot on the page.

## Workflow

1. Harvest seed terms per pillar from product language, customer phrasing, competitor
   captions, and platform search autocomplete.
2. Research per platform: Instagram search + tag page inspection, TikTok Creative Center
   trend and hashtag data, Pinterest Trends, X advanced search, LinkedIn search bar
   (follow counts).
3. Tier every candidate tag by volume on its platform (broad 1M+, mid 100k–1M,
   niche <100k) and record approximate post counts.
4. Validate relevance by inspecting each tag's recent top posts: if the content type or
   quality bar does not match the brand's format, drop it — relevance beats raw volume.
5. Screen every tag against banned/limited lists and per-platform search: banned tags
   return few or no recent posts; verify status before anything enters the library.
6. Build rotation sets per pillar per platform: IG 10–15 tags in 3–5 rotating mixes,
   TikTok 4–6 mixed-size tags, LinkedIn 3–5 professional tags, X 1–2, Pinterest 2–4
   keyword-style tags. Never paste one identical block on every post.
7. Decide the branded campaign tag: only create one if UGC pull-through is planned with
   ugc-curation; otherwise skip branded tags entirely.
8. Deliver sets to content-creation with paste-ready blocks and usage notes.
9. Review tag-level performance monthly (IG/TikTok impressions-by-source, LinkedIn
   follow/hashtag reach), retire dead tags, and refresh the library quarterly.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Volume + tag page inspection | Instagram search, TikTok Creative Center | Free; the ground truth for both platforms |
| Dedicated research | Flick, RiteTag, Keyhole | Paid; Flick ~£14/mo covers IG well |
| Free generators (verify output) | Display Purposes, IQHashtags free tools | Never trust blindly — banned-tag risk |
| Pinterest discovery | Pinterest Trends | Free; keyword-style tags + board terms |
| X research | X advanced search | Free; check tag recency and tone |
| Performance tracking | IG Insights, TikTok Analytics, Metricool | Free-native; impressions by source |

## Example AI Prompt

```text
Act as a hashtag researcher. Build a hashtag library for {BRAND} ({NICHE}, account size:
{FOLLOWERS} on {PLATFORMS}) across content pillars: {PILLAR LIST}.
Competitors whose tag usage we studied: {HANDLES}. Campaign in flight: {CAMPAIGN OR NONE}.

Deliver:
1. Tiered tag tables per pillar: hashtag | platform | tier (broad/mid/niche) |
   approx. volume | relevance note.
2. Paste-ready rotation sets (3-5 per pillar) with the ~20/50/30 broad-mid-niche mix.
3. Platform rules: tag count per platform (IG 10-15, TikTok 4-6, LinkedIn 3-5, X 1-2,
   Pinterest 2-4) and any format notes.
4. Banned/skipped list: tags I must avoid and why.
5. Branded hashtag verdict with reasoning, and a monthly review checklist.
Exclude tags whose recent top posts do not match our content format.
```

## Edge Cases & Guardrails

- Banned and limited tags change constantly and vary by niche — verify every tag in
  platform search before it ships; one banned tag can suppress the whole post.
- Instagram's ranking now weighs fewer, more specific tags; 10–15 relevant tags
  outperform 30 generic ones, and relevance mismatch reads as spam.
- Reusing the identical tag block on every post is a repetitive-content signal; rotate
  sets and vary order.
- Hijacked or controversial tags accumulate off-topic/NSFW posts — check what a tag
  actually surfaces this week, not what it meant last year.
- Branded hashtags without a UGC collection plan become ghost towns that signal low
  adoption; coordinate with ugc-curation or skip.
- Do not chase broad tags (1M+) on small accounts — content drowns in seconds; niche
  tags are where small accounts rank and hold page positions.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Non-follower reach share (IG/TikTok) | 25–40% of reach | <15% means discovery is broken |
| Hashtag-origin impressions (IG) | Trending up over 8 weeks | Near-zero from tags despite volume |
| Banned-tag incidents | 0 | Any tag later flagged as limited |
| Tag rotation in use | ≥3 sets per pillar | One identical block on every post |
| Campaign tag adoption | 20+ organic uses in flight | Zero external uses after 4 weeks |
| Library refresh cadence | Quarterly | Tags chosen once, reused for a year |

## Handoffs

- → **content-creation:** deliver paste-ready tag sets embedded in each post brief.
- → **content-calendar:** note per-platform tag rules so scheduling includes them.
- → **ugc-curation:** hand over the branded campaign tag if one is activated.
- → **analytics-reporting:** provide the tag library so impressions-by-source can be
  scored against it.
- ← **strategy-planning:** pull pillar definitions and platform priorities from the
  strategy brief.
