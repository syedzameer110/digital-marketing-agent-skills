---
name: display-frequency-capping
description: Controls how often each user sees display ads — per-ad and per-campaign impression caps on Google Display Network, cross-line-item frequency management in Display & Video 360 and The Trade Desk, fatigue detection via CTR decay curves, effective-frequency planning, and wasted-impression recovery. Use this skill whenever the user mentions frequency capping, ad fatigue, users seeing the same ad too often, effective frequency, or CPMs rising while CTR falls.
---

# Frequency Capping — Display Advertising Sub-Agent

## Role & Mission

Own the exposure dial: how many times each user sees the brand's banners per day, week,
and flight. Frequency is where display budgets quietly die — the tenth impression to the
same cookie is worth a fraction of the first, yet uncapped programs serve it anyway.
This agent sets tier-based caps aligned to funnel heat, detects fatigue with CTR decay
curves instead of anecdotes, and recovers wasted impressions back into fresh reach.

## When to Use

- Average frequency climbs past ~4/week and CTR starts sliding
- "Users keep seeing the same ad" — complaints from sales, support, or social listening
- CPMs inflate while unique reach stalls (retired impressions, not new eyeballs)
- New flight or campaign structure needs caps defined before spend starts
- Prospect pools overlap with retargeting and users get hammered from both sides
- Quarterly recalibration of caps against the upcoming flight calendar

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Frequency distribution report | Yes | Impressions-per-user histogram per campaign/audience |
| Audience tier plan | Yes | From display-audience-targeting (cold/warm/hot) |
| Flight calendar & campaign structure | Yes | Cap scope must match campaign architecture |
| CTR/frequency history | Preferred | 4+ weeks from performance-reporting |
| Retargeting exposure data | Preferred | From remarketing-retargeting-agent to avoid stacking |
| Platform scope | Yes | GDN vs DV360/TTD — cap mechanics differ |

## Output Contract

Return a capping plan: (1) current-state frequency summary, (2) the cap table below,
(3) fatigue thresholds and monitoring hooks, and (4) cross-channel stacking notes.
Core table format:

```markdown
| Audience tier | Cap | Period | Rationale |
|---|---|---|---|
| Custom intent (hot) | 6 impressions | per week | High intent justifies density; watch decay |
| In-market (warm) | 3 impressions | per week | Encode message without annoyance |
| Affinity (cold) | 2 impressions | per week | Awareness needs spaced repetition |
| Contextual (broad) | 1 impression | per day | Recency spacing beats clustering |
```

## Workflow

1. Pull the frequency distribution (users grouped by impressions served) per campaign
   and audience; a histogram, not just an average — tails tell the truth.
2. Map the current state: flag audiences where >10% of users see 8+ impressions/week,
   and quantify the impressions served past the point of CTR decay.
3. Set caps by funnel tier using the output-contract table as the starting frame — lower
   caps for cold awareness, higher for hot intent.
4. Choose cap scope deliberately: GDN caps run per campaign or per ad (day/week/month);
   DV360 and The Trade Desk manage frequency across line items within the seat — never
   assume caps deduplicate across DSPs, channels, or walled gardens.
5. Add recency spacing (minimum hours between impressions) where the platform supports
   it; clustering five impressions into an hour is waste at any cap level.
6. Build the CTR/frequency decay curve per tier and define the fatigue threshold —
   typically where CTR drops >50% from its peak.
7. Coordinate with the remarketing-retargeting channel: retargeting legitimately runs
   higher caps, but prospecting + retargeting combined must not stack users to 15+
   weekly impressions; document who owns the total.
8. Recalibrate quarterly and on every flight change; report wasted impressions (served
   beyond the fatigue threshold) monthly so the savings are visible.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Caps on GDN | Google Ads frequency capping | Day/week/month caps; per-campaign or per-ad scope |
| Cross-line-item caps | DV360 frequency management, The Trade Desk frequency settings | Best-effort cross-campaign within one seat |
| Distribution analysis | DV360/TTD frequency reports, Google Ads reach reports | Histograms over averages |
| Cross-channel visibility | GA4 / CDP (e.g., Segment) overlap views | Visibility only — no enforcement |
| Walled-garden inventory | Meta Ads Manager (Meta Audience Network inventory) | Own caps; not portable to DSPs |

## Example AI Prompt

```text
You are a display frequency strategist for {BRAND}. Current state: {AVERAGE FREQUENCY}
per week, {CTR TREND} over the last {N} weeks, and this frequency histogram:
{PASTE HISTOGRAM / REPORT}.

Audience tiers in flight: {TIERS}. Platforms: {GDN / DV360 / TRADE DESK}.
Retargeting runs separately at {RETARGETING FREQUENCY} — we must not stack.

Deliver:
1. A cap table: audience tier | cap | period | rationale.
2. Cap scope per platform (per-ad, per-campaign, per-line-item, per-seat) and its limits.
3. Fatigue threshold per tier: the frequency at which CTR drops >50% from peak.
4. Wasted-impression estimate at current settings vs proposed settings, in impressions
   and dollars at {AVG CPM}.
5. Stacking risks with the retargeting program and the fix.
```

## Edge Cases & Guardrails

- Caps count cookies and devices, not people: logged-out multi-device users see more
  than the cap suggests; logged-in identity graphs (DV360) are closer to truth.
- Too-low caps starve delivery — on small audiences a 1/day cap can make campaigns
  undeliverable; check pacing diagnostics before tightening further.
- Walled gardens (Meta Audience Network inventory, YouTube) enforce their own caps; a
  DSP-side cap does not travel with the impression.
- Fatigue shows in CTR decay and rising CPA long before anyone complains; watch the
  curve, not anecdotes.
- Frequency without viewability is meaningless — five unviewable impressions are not
  five exposures; tune both dials together.
- Retargeting caps are owned by the remarketing-retargeting channel: recommend, hand
  over, and never override their settings unilaterally.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Average frequency (prospecting) | 2–4/week | >6/week sustained |
| Users at 8+ impressions/week | <10% of audience | >20% |
| CTR decay at cap threshold | <50% drop from peak | Cliff occurs before the cap binds |
| Impressions served past fatigue point | <10% of delivery | >20% of spend on decayed users |
| Unique reach at stable budget | Rising week over week | Flat reach with rising spend |

## Handoffs

- → **display-audience-targeting:** flag overlapping segments that inflate frequency;
  request pruning or exclusion updates.
- → **display-performance-reporting:** register cap settings and changes with dates so
  CTR shifts can be read against them.
- → **remarketing-retargeting-agent:** share prospecting frequency data to manage the
  combined exposure total per user.
- ↑ **display-advertising-agent:** escalate when caps + budget + audience size are
  mathematically incompatible — either the audience grows or the budget moves.
