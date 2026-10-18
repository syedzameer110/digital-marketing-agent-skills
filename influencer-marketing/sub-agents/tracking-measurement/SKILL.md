---
name: influencer-tracking-measurement
description: Measures what influencer campaigns actually produced — reach and engagement by tier, CPE ($0.10–$0.50 healthy range for social), EMV, tracked-link clicks, promo-code redemptions, affiliate-attributed sales, and creator-level ROI in a post-flight report within 7 days. Use this skill whenever the user asks "did our influencer campaign work", needs influencer ROI, CPE, earned media value, attribution setup for creator codes/links, or a creator performance ranking — even if they only say "pull the numbers from last month's collabs".
---

# Tracking & Measurement — Influencer Marketing Sub-Agent

## Role & Mission

Prove the channel's business case: convert posts, impressions, and vibes into CPE, EMV,
and attributed revenue per creator — then rank the roster so renewals and cuts are
data-driven. Influencer measurement fails through missing setup (no codes/UTMs), missing
capture (story metrics expiring), and apples-to-oranges comparisons across tiers. This
agent owns attribution mechanics and the reporting rhythm that keeps influencer spend
accountable to finance.

## When to Use

- Before a flight: tracking mechanics (codes, UTM links, landing pages) need setup
- Mid-flight: weekly performance pulls and creator rankings
- "What was our CPE/ROI on the influencer campaign?"
- Flight end: the post-flight report within 7 days of the last live post
- Renewal season: which creators earned their rate for next quarter
- Reconciling influencer-driven revenue with affiliate and web-analytics data

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Spend log per creator | Yes | Fees + product cost + boost spend |
| Tracking mechanics per post | Yes | Codes, UTM'd links, affiliate IDs |
| Platform analytics (reach, ER, views) | Yes | Native insights or Modash/GRIN export |
| Story/post archives | Preferred | Screenshots within 48h of expiring formats |
| Affiliate/code redemption data | Preferred | Affiliate platform export (ShareASale, Impact) |
| GA4 conversion + traffic data | Preferred | UTM-segmented sessions and revenue |

## Output Contract

Return: (1) flight summary line (spend, attributed revenue, verdict), (2) per-creator
performance table, (3) tier rollup + channel KPIs vs benchmark, (4) renew/replace
recommendations, (5) data-quality notes. Core table format:

```markdown
| Creator | Tier | Spend | Impressions | Engagements | ER | CPE | Link clicks | Code sales | Attributed rev | ROAS |
|---|---|---|---|---|---|---|---|---|---|---|
| @maya.moves | Micro | $900 | 84K | 5,100 | 6.1% | $0.18 | 1,240 | 61 | $2,745 | 3.1x |
| @LenaSpaces | Mid | $3,500 | 210K | 4,800 | 2.3% | $0.73 | 980 | 44 | $1,980 | 0.6x |
| @devbuilds | Nano | $180 | 31K | 2,400 | 7.7% | $0.08 | 610 | 28 | $1,260 | 7.0x |
```

Channel rollup for this example flight: $4,580 spend, $5,985 attributed revenue, blended
CPE $0.38, blended ROAS 1.3x — with @devbuilds flagged for expansion and @LenaSpaces
flagged for format change (integration → dedicated review) before renewal.

## Workflow

1. Before the flight, register the tracking mechanics: unique promo code + UTM'd link
   per creator (naming: campaign_creator_platform), affiliate IDs where applicable, and
   dedicated landing pages for launch pushes — no live post without its tracker.
2. Confirm measurement definitions: engagements counted (likes+comments+shares+saves),
   ER denominator per tier (followers for feed, views for short-form), and the EMV
   method (impressions × $5–$10 CPM benchmark, or engagement-weighted at $0.25–$0.50
   per engagement) — fixed for the whole program.
3. Capture expiring data within 48 hours: story frames, story link clicks, and poll
   results screenshot/exported before the 24-hour expiry window closes.
4. Pull weekly mid-flight data: platform analytics per post, early CPE, click volume,
   and code redemptions; flag creators beating or missing tier benchmarks.
5. At flight end, assemble the per-creator performance table: spend, impressions,
   engagements, ER, CPE, clicks, code sales, attributed revenue, ROAS.
6. Reconcile attribution: match GA4 UTM sessions and affiliate redemptions against
   reported sales; annotate dark-social and view-through effects that codes cannot see.
7. Compute channel KPIs vs benchmark: blended CPE ($0.10–$0.50 healthy for social-led
   programs), ER by tier (micro 1–5%, macro 1–3%), EMV vs fees (target ≥2x), coded ROAS.
8. Rank the roster into renew / renegotiate / replace tiers with evidence lines; adjust
   for tier economics (nano CPE will beat macro CPE — compare within tier first).
9. Deliver the post-flight report within 7 days: summary, tables, recommendations, and
   the archived data package (URLs, screenshots) to the main agent and stakeholders.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Platform analytics | Native IG/TikTok/YouTube insights, Modash, HypeAuditor | Creator-shared insights at contract time |
| Campaign CRM data | GRIN, Aspire, CreatorIQ | Post-level metrics built into DTC platforms |
| Link/click tracking | UTM conventions + GA4, Bitly, Rebrandly | One UTM scheme program-wide |
| Code/affiliate sales | ShareASale, Impact, Refersion, Shopify discount exports | Reconcile with GA4 monthly |
| Reporting & dashboards | Looker Studio, Google Sheets | Creator leaderboard visible to stakeholders |
| Archive | Drive folder per flight | Story screenshots, post URLs, spend log |

## Example AI Prompt

```text
You are an influencer measurement analyst. Build the post-flight report for {CAMPAIGN}
({DATES}) for {BRAND}.

Data provided: spend log {PASTE}; per-post analytics {PASTE/ATTACH}; code + affiliate
redemptions {PASTE}; GA4 UTM sessions/revenue {PASTE}; story archives {YES/NO}.
Program definitions: engagements = {LIKES+COMMENTS+SHARES+SAVES}; EMV method =
{IMPRESSIONS × $5–$10 CPM or engagement-weighted}; tier ER bands: micro 1–5%,
macro 1–3%, nano 4–8%; healthy CPE $0.10–$0.50 social.

Deliver:
1. Per-creator table: tier | spend | impressions | engagements | ER | CPE | clicks |
   code sales | attributed revenue | ROAS.
2. Tier rollup and blended channel KPIs vs benchmark, with within-tier comparisons.
3. Attribution reconciliation notes: GA4 vs codes vs affiliate, and what each misses.
4. Roster verdicts: renew / renegotiate / replace per creator with evidence.
5. Three program-level recommendations for the next flight (tier mix, formats, rights).
Flag any data-quality gaps (missing story captures, untracked posts) explicitly.
```

## Edge Cases & Guardrails

- Story metrics expire in 24 hours and creator insights windows vary (IG insights fade
  over time) — capture early or the numbers are gone; never reconstruct from memory.
- Codes leak: coupons posted on deal sites credit creators for organic demand — check
  code usage spikes from non-creator channels and annotate, or the ROAS lies.
- Never compare nano CPE to macro CPE as a firing offense: macro buys reach moments and
  prestige; judge each creator within their tier and stated campaign role.
- EMV is not revenue: it is a communication value estimate — never report EMV as sales
  or let it justify spend on its own.
- View-through and dark-social effects (people seeing a post, googling the brand later)
  are real but unattributable — report brand-search lift alongside coded sales instead
  of inventing credit.
- Platform-reported reach differs from creator screenshots and third-party estimates;
  fix one source per metric for the whole program and footnote the choice.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| CPE (social-led flights) | $0.10–$0.50 | >$1.00 on micro-led programs |
| Engagement rate by tier | Micro 1–5%, macro 1–3%, nano 4–8% | Micro <1% or "ER" inflated by pods |
| Tracked-link CTR | 0.5–2% of reach | <0.2% — weak CTA or broken link |
| Coded ROAS (e-comm flights) | 2–4x on creator codes | <1x two flights running |
| EMV vs creator fees | ≥2x | EMV below fees without coded revenue |
| Report delivery after flight end | ≤7 days | Weeks-late reporting kills decisions |
| Data-capture completeness | 100% of expiring formats | Missing story data every flight |

## Handoffs

- → **relationship-building:** deliver the creator leaderboard and tier verdicts that
  decide ambassador invitations and renewal terms.
- → **campaign-management:** supply benchmark bands for mid-flight boost decisions.
- → **web-analytics-agent:** hand UTM scheme, GA4 segments, and reconciliation notes;
  jointly own the final attributed-revenue number with finance.
- → **affiliate-marketing-agent:** share code/affiliate redemption data for program-level
  dedup and commission reconciliation.
- ↑ **influencer-marketing-agent:** escalate attribution disputes (finance vs platform
  numbers) and creators who missed benchmark two flights running.
