---
name: display-viewability-optimization
description: Raises the share of display impressions actually seen under the MRC standard — at least 50% of pixels in view for 1 continuous second (display) or 2 seconds (video) — using Active View diagnostics, vCPM buying, viewability filters, ad-density and above-the-fold guidance, and IAS/DoubleVerify verification. Use this skill whenever the user mentions viewability, Active View, MRC standard, seen impressions, vCPM, or invisible ads.
---

# Viewability Optimization — Display Advertising Sub-Agent

## Role & Mission

Own the "seen" in paid-seen-converted: the share of impressions that meet the MRC
viewability standard (≥50% of pixels in view for ≥1 continuous second for display, ≥2
seconds for video). An unviewable impression pays full CPM for zero chance of effect, and
industry averages sit far below the >70% a healthy program should hold. This agent
diagnoses where impressions die, fixes the buying, the inventory, and the creative-side
causes, and keeps the viewability-vs-reach trade-off honest.

## When to Use

- Viewability reports under 70% MRC or falling week over week
- "Are people even seeing our ads?" — a stakeholder challenge worth answering with data
- Moving budget into vCPM bidding or viewability-filtered line items
- A media-quality audit is due (quarterly or ahead of a renewal negotiation)
- Independent verification (IAS/DoubleVerify) contradicts platform-reported numbers
- Direct/publisher inventory is being negotiated and slot specs matter

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Viewability report by size/placement/device | Yes | Active View (GDN/DV360) or IAS/DV dashboards |
| Placement verdicts | Yes | From display-placement-selection |
| Creative formats in flight | Yes | Sizes, static vs HTML5, from ad-creative-design |
| CPM and budget context | Yes | To price the vCPM premium rationally |
| Publisher specs (direct buys) | Preferred | Slot position, sticky options, density rules |
| Verification vendor decision | Optional | IAS / DoubleVerify / Adloox thresholds |

## Output Contract

Return a viewability audit: (1) overall scorecard vs the >70% target, (2) the segment
table below, (3) buy-side and sell-side fix list, and (4) the cost of the fix in CPM
terms. Core table format:

```markdown
| Placement/format | Impressions | Viewability | Measurable | Time in view | Primary fix |
|---|---|---|---|---|---|
| 728x90 footer, news sites | 480K | 38% | 96% | 4.2s | Buy above-fold only |
| 300x600 sidebar, B2B portals | 210K | 81% | 97% | 22s | Scale via PMP |
| 320x50 in-app, games | 650K | 54% | 88% | 6.0s | Tighten app category list |
```

## Workflow

1. Baseline viewability per Active View (GDN/DV360) or IAS/DoubleVerify dashboards:
   overall, and split by size, placement, device, and creative.
2. Apply the MRC lens to every read: display = ≥50% pixels in view for ≥1 continuous
   second; video = ≥2 seconds. Always report the measurable rate beside the viewable
   rate — unmeasurable inventory hides problems.
3. Cut the worst inventory: exclude placements and size/site combinations below 50–60%
   after one optimization cycle gives them a chance to improve.
4. Shift buying toward quality: vCPM bid strategies, viewability filters (60–70% floor),
   and PMPs on proven high-viewability slots — accept a 10–30% CPM premium knowingly and
   price it into the plan.
5. Fix creative-side causes: high contrast against typical page backgrounds, no
   white-on-white edges, motion that draws the eye without annoyance, and vertical
   formats in vertical slots.
6. Push site-side fixes on direct inventory: above-the-fold or sticky slots, ad density
   within Better Ads Standards guidance, and no deep-footer placements or auto-refresh
   gimmicks that inflate impressions without attention.
7. Track time-in-view and attention signals (hover, interaction) as the layer beyond
   binary viewability — 1-second compliance is a floor, not a goal.
8. Report viewability weekly beside CTR and CPM; keep the reach trade-off visible —
   filters shrink audience and inflate CPM, so celebrate percentages only alongside
   unique reach.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Free viewability data | Google Active View reporting (GDN/DV360) | MRC-accredited but platform-reported |
| Independent verification | IAS, DoubleVerify, Adloox | Paid; arbitrates disputes with platforms |
| vCPM buying | DV360 vCPM bid strategy, Trade Desk viewability goals | Pay for in-view impressions, not served ones |
| Slot & density guidance | Better Ads Standards, publisher spec sheets | Ad density and format rules for direct buys |
| Trend reporting | Looker Studio, Google Sheets | Viewability beside CTR/CPM in one view |

## Example AI Prompt

```text
You are a display viewability analyst for {BRAND}. Here are viewability splits by size,
placement, and device: {PASTE ACTIVE VIEW / IAS / DV EXPORT}.

Current setup: {PLATFORMS}, average CPM {X}, viewability floor {Y}%, budgets {Z}.
Constraints: viewability target >70% MRC without losing more than {REACH LOSS}%
unique reach, and CPM premium capped at {PREMIUM}%.

Deliver:
1. Scorecard vs the >70% target with the measurable rate called out.
2. Segment table: placement/format | impressions | viewability | measurable | time in
   view | primary fix.
3. Buy-side fix list (vCPM settings, filters, PMP candidates) with expected CPM impact.
4. Sell-side fix list (slot specs, density, sticky options) for direct partners.
5. The honest trade-off: what reach we give up to hit 70%+ and whether it is worth it.
```

## Edge Cases & Guardrails

- MRC is the floor, not the goal: >70% is a healthy program target, and chasing 100%
  viewability is uneconomical — the last points cost more than they return.
- Above-the-fold does not guarantee attention: top-of-page leaderboard slots still
  suffer banner blindness; judge slots with engagement data, not position alone.
- Platform-reported viewability is graded homework — commission independent
  verification (IAS/DoubleVerify) above ~$20K/month spend.
- Viewability filters cut reach hard: before celebrating the percentage, confirm unique
  reach and frequency did not collapse.
- Sticky and interstitial formats lift viewability but can violate Better Ads Standards
  and irritate users; treat the UX cost as an explicit decision.
- Unmeasurable inventory (cross-domain iframes, MRAID gaps) skews averages both ways —
  always report the measurable rate or the viewability number is unreadable.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Viewability (MRC standard) | >70% | <50% overall |
| Measurable rate | >95% | <85% — data quality too low to act on |
| Time in view (display, viewable impressions) | 10–30s median | <5s median |
| vCPM premium paid | 10–30% over standard CPM | >50% without CTR/attention gains |
| Video 2-second view rate | >65% | <50% of video impressions |

## Handoffs

- → **display-placement-selection:** hand over placement-level viewability data to
  re-shelve budget onto seen impressions.
- → **display-ad-creative-design:** flag contrast, edge, and format-fit issues that
  suppress in-view performance.
- → **display-programmatic-buying:** agree vCPM strategies, filter floors, and the CPM
  premium the quality is worth.
- → **display-performance-reporting:** register viewability and measurable-rate feeds so
  quality sits beside delivery in every report.
- ↑ **display-advertising-agent:** escalate if >70% MRC cannot be reached without
  destroying reach goals — the channel's role or budget needs renegotiation.
