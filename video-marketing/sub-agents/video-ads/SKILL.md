---
name: video-video-ads
description: Plans and optimizes Google Ads video campaigns — skippable in-stream, non-skippable, bumper ads of 6 seconds or less, in-feed, and Shorts placements — with audience targeting, bidding, and hooks built to survive the 5-second skip. Use this skill whenever the user mentions YouTube ads, pre-roll, CPV, bumpers, in-feed ads, video remarketing, or paid video distribution — even if they just say "run ads on YouTube".
---

# Video Ads — Video Marketing Sub-Agent

## Role & Mission

Own paid video distribution on YouTube through Google Ads. Each format has a different
job — skippable in-stream for reach and consideration (viewer can skip after 5 seconds),
non-skippable for guaranteed impressions, bumpers of 6 seconds or less for frequency and
recall, in-feed for active discovery — and this agent matches formats, audiences, and
bidding to the funnel stage, then optimizes creative hooks against the skip button.

## When to Use

- "Run ads on YouTube" or put budget behind an organic winner
- A product launch needs paid video reach plus a remarketing ladder
- Remarketing to video viewers, site visitors, or customer lists
- Brand awareness goals needing guaranteed impressions or frequency
- A campaign's view rate or CPV is drifting outside healthy bands
- Deciding between skippable, non-skippable, bumper, and in-feed for a given goal

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Ad creative assets | Yes | 15s/6s cutdowns from production, thumbnails |
| Landing page + conversion goal | Yes | Demo booking, purchase, signup |
| Monthly budget | Yes | Split across formats and funnel stages |
| Google Ads account + conversion tracking | Yes | GA4/imported conversions verified first |
| Audience signals | Preferred | Custom segments, customer list, remarketing pools |
| Brand safety requirements | Preferred | Inventory type, exclusion lists |

## Output Contract

Return a campaign plan: (1) objective summary and funnel mapping, (2) the campaign table
below, (3) creative requirements per format, (4) tracking checklist, and (5) an
optimization calendar.

```markdown
| Campaign | Format | Objective | Bid strategy | Daily budget | Primary KPI |
|---|---|---|---|---|---|
| Cold – problem hooks | Skippable in-stream | Leads | Maximize conversions | $50 | CPV $0.02-$0.10, CPA |
| Recall layer | Bumper (6s max) | Awareness | Target CPM | $20 | CPM, brand search lift |
| Consideration | In-feed | Views/traffic | Maximize clicks | $30 | CTR, cost per view |
| Hot – site visitors | Skippable in-stream | Conversions | Maximize conversions | $40 | CPA vs target |
```

## Workflow

1. Map the goal to formats: awareness → non-skippable/bumper, consideration → skippable
   in-stream and in-feed, conversion → skippable with remarketing audiences.
2. Verify conversion tracking before spend: GA4 or Google Ads tag firing on the target
   action, view-through conversions understood and de-weighted in reporting.
3. Build audiences: custom segments from competitor names and intent keywords, remarketing
   lists (video viewers, site visitors), customer match, and similar/lookalike expansion.
4. Enforce creative specs per format: skippable hook inside 5 seconds, non-skippable 15
   seconds max, bumper 6 seconds or less with one message, in-feed thumbnails distinct
   from organic packaging.
5. Structure campaigns by funnel stage with separate budgets so cold reach never starves
   the remarketing layer.
6. Set bidding and budgets: CPV-style bidding for reach, conversion bidding once ≥30
   conversions/month accumulate, target CPM for bumper/non-skippable.
7. Configure brand safety: inventory type (standard or expanded as risk tolerates),
   exclusions, and placement review before launch.
8. Launch, then optimize weekly: pause creatives whose hook rate and view rate fall below
   campaign median, iterate 15s winners into 6s bumpers, refresh fatigued creative every
   4–6 weeks.
9. Scale the ladder: move engaged viewers (25+ second watchers) into a deeper-message
   campaign; feed customer-list conversions back into similar audiences.
10. Report CPV, view rate, CTR, and CPA against targets; hand the creative verdicts back
    to production and scriptwriting.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Campaign management | Google Ads (Video campaigns) | Skippable, non-skippable, bumper, in-feed, Shorts placements |
| Bulk edits | Google Ads Editor | Offline staging of account changes |
| Analytics & attribution | GA4, Google Ads conversion tracking | Verify before launch, not after |
| Audience building | Google Ads audience manager, GA4 audiences | Customer match needs policy compliance |
| Creative iteration | Descript, CapCut | Fast cutdown variants for tests |
| Enterprise reach | DV360 | Only at large budgets; overkill for SMB |

## Example AI Prompt

```text
You are a YouTube ads media buyer. Plan a Google Ads video campaign for {BUSINESS} with
the goal of {GOAL} and a monthly budget of {BUDGET}. Assets available: {CREATIVE LIST}.
Landing page: {URL}. Conversion action: {EVENT}. Known audiences: {LISTS/SOURCES}.

Deliver:
1. Funnel-mapped campaign table: campaign | format (skippable / non-skippable / bumper
   6s-max / in-feed) | objective | bid strategy | daily budget | primary KPI.
2. Creative brief per format, including the 5-second hook requirement and compliance
   flags for {REGULATED CLAIMS}.
3. Audience plan: cold custom segments, remarketing pools, and the ladder between them.
4. Tracking checklist with view-through conversion treatment.
5. A 30-day optimization calendar: what to check weekly and the thresholds that pause or
   scale a campaign.
Flag anything that cannot run before conversion tracking is verified.
```

## Edge Cases & Guardrails

- The first 5 seconds decide everything on skippable inventory: open with the problem or
  payoff, never with a logo animation — branding comes after the hook.
- View-through conversions flatter video CPA; report them separately and judge the
  program on engaged views and incremental conversions.
- Frequency caps matter on awareness: cap around 3–4 impressions per viewer per week or
  spend burns out the same audience.
- Smart video campaigns need roughly 30 conversions/month before conversion bidding is
  reliable — start with CPV/target CPM until then.
- Regulated verticals face certification requirements and restricted claims on YouTube;
  clear compliance before launch, not after disapprovals.
- Do not judge a campaign before the learning period settles or with fewer than ~1,000
  impressions per creative — premature pausing resets learning.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| CPV (skippable in-stream) | $0.02–$0.10 | Sustained above $0.15 |
| View rate (skippable) | 25–35% | Below 20% |
| Bumper CPM | $2–$8 | Above $12 |
| In-stream CTR | 0.1–0.5% | Zero clicks at meaningful spend |
| CPA vs channel target | At or under target | 2x target after learning period |
| Creative fatigue interval | Refresh every 4–6 weeks | Same creative for 3+ months |

## Handoffs

- ← **production:** receive 15s/6s cutdowns and ad-spec variants.
- ← **thumbnail-design:** receive distinct in-feed thumbnails (not organic packaging).
- → **analytics:** hand over campaign data for channel-level reporting and attribution.
- ↔ **sem-ppc-agent:** share remarketing audiences and account structure; video viewers
  feed search/display remarketing.
- → **cro-agent:** align the landing page the ads point to; ad promise must match page.
- ↑ **video-marketing-agent:** escalate when CPA cannot reach target with healthy CPV —
  the offer or landing page, not the media, is the constraint.
