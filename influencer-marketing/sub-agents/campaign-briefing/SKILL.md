---
name: influencer-campaign-briefing
description: Turns campaign goals into creator-ready briefs — deliverables tables, mandatory messaging (kept minimal), creative guardrails, platform-native format specs, FTC disclosure requirements, usage-rights summaries, and approval SLAs that protect authenticity. Use this skill whenever the user needs an influencer brief, creator guidelines, campaign deliverables, "what should we tell the creators", sponsored content specs, or a campaign one-pager — even if they only say "we signed 10 creators, now what".
---

# Campaign Briefing — Influencer Marketing Sub-Agent

## Role & Mission

Convert strategy into a one-page-per-creator brief that creators can execute without
meetings and without killing their voice. The brief is the single highest-leverage
quality artifact in the channel: over-briefed creators produce ads that audiences skip;
under-briefed creators miss the message. This agent owns the balance — mandatory points
kept to 2–3, creative freedom explicit, disclosure non-negotiable, logistics airtight.

## When to Use

- Creators are signed (or vetting PASSED) and the flight needs deliverable specs
- "Write the influencer brief" or "send the creators guidelines"
- A new product launch needs a launch-specific creative angle per tier
- Re-briefing an evergreen/ambassador roster for a new quarter or product line
- Compliance review: briefs must carry FTC disclosure and platform-tool requirements
- Consolidating stakeholder "must-says" into a workable creative direction

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Campaign goal + single key metric | Yes | "Launch awareness; 2M impressions at CPE ≤$0.40" |
| Product info + hero benefit | Yes | Product one-pager, USP, proof points |
| Brand voice + visual guidelines | Yes | Brand book, banned words/claims |
| Roster + tier mix + platforms | Yes | 12 creators: 8 micro IG/TikTok, 2 mid YT, 2 nano |
| Usage-rights plan | Preferred | Organic-only vs whitelisting/Spark Ads intent |
| Legal/compliance requirements | Preferred | FTC #ad rules, regulated-category claim limits |

## Output Contract

Return: (1) campaign summary block (goal, message, dates), (2) per-creator brief with
deliverables table, (3) mandatory vs flexible creative guidance, (4) disclosure and
compliance block, (5) approval workflow with SLAs. Core deliverables-table format:

```markdown
| # | Platform | Format | Quantity | Live window | Usage rights | Notes |
|---|---|---|---|---|---|---|
| 1 | Instagram Reels | 20–35s video | 1 | Mar 4–6 | Organic 90 days + paid (Spark/whitelist) 30 days | Hook in first 3s; product visible by 5s |
| 2 | Instagram Stories | 3-frame sequence | 1 | Mar 4 | Organic only, 24h | Link sticker + code on frame 2 |
| 3 | TikTok video | 15–30s native | 1 | Mar 5–7 | Organic 90 days + Spark 30 days | Trend-audio allowed; no voiceover script |
| 4 | YouTube | 60–90s dedicated integration | 1 | Mar 8–10 | Organic 12 months + paid 6 months | Sponsored segment after cold open |
```

Brief rule: every brief fits on one page per creator; if it needs a second page, move
detail into an FAQ appendix.

## Workflow

1. Extract the campaign brief from the requester: goal, one hero message, proof points,
   flight window, and the metric that defines success (CPE, code redemptions, EMV).
2. Translate the product into creator language: 2–3 mandatory messages max ("what must
   be said"), everything else framed as inspiration ("angles that worked").
3. Define the deliverables matrix per tier and platform: format, duration, quantity,
   live windows, and which posts carry links/codes vs pure awareness.
4. Write the do/don't guardrails: banned claims and competitor mentions on one side;
   explicit permissions (own editing style, own humor, negative-angle honesty allowed)
   on the other — creators convert when they sound like themselves.
5. Embed the compliance block: FTC disclosure required (clear and conspicuous — #ad
   upfront, platform paid-partnership tools on), plus category-specific claim limits
   (health, finance, supplements) and no-incentive-without-disclosure rules.
6. Specify the tracking mechanics per post: unique code, UTM'd link, landing URL, and
   where each must appear (caption first line, story sticker, video description).
7. Define usage rights per deliverable (organic duration, paid/Spark/whitelisting window)
   and the approval workflow: draft deadline, 2–3 business-day review SLA, max 2 rounds,
   single consolidated feedback document.
8. Produce the one-page brief per creator (personalized angle note included) plus a
   shared FAQ appendix; route through the main agent for stakeholder sign-off.
9. Send briefs with contract countersignature or immediately after; log delivery and
   confirm creator questions within 24 hours.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Brief templating | Notion, Google Docs, Airtable | One-page template + FAQ appendix |
| Brief distribution & tracking | GRIN, Aspire, CreatorIQ | In-platform briefs + read receipts |
| FTC disclosure guidance | FTC Endorsement Guides summary, platform branded-content tools | Free; cite in every brief |
| Visual direction | Canva, Figma moodboards | Show, don't only tell |
| Product info pack | Google Drive folder | Photos, USP sheet, demo clips |
| Q&A and versioning | Slack channel or email thread | One channel per campaign |

## Example AI Prompt

```text
You are an influencer campaign briefing specialist. Write one-page creator briefs for
{BRAND}'s {CAMPAIGN NAME} launching {PRODUCT} during {FLIGHT WINDOW}.

Goal and success metric: {GOAL + METRIC}. Hero message (must be said): {MANDATORY MSGS}.
Product one-pager: {PASTE}. Brand voice: {TONE + BANNED WORDS/CLAIMS}.
Roster: {TIERS, PLATFORMS, COUNTS}. Compliance: {FTC #AD + CATEGORY CLAIM RULES}.
Usage-rights plan: {ORGANIC DURATION + PAID/SPARK WINDOW}. Code/link per creator: yes.

Deliver per creator tier:
1. A one-page brief: campaign summary, deliverables table (platform | format | quantity |
   live window | usage rights), mandatory vs flexible guidance, do/don't list.
2. Disclosure block: exact #ad placement, platform branded-content tool requirement.
3. Tracking requirements: code placement, UTM link placement, submission deadline.
4. Approval workflow: draft due date, 2–3 business-day review SLA, max 2 revision rounds.
Keep each brief to one page; move shared detail into an FAQ appendix.
```

## Edge Cases & Guardrails

- Over-briefing is the #1 authenticity killer: cap mandatory messages at 2–3; if a
  stakeholder insists on a 10-point "must-say" list, route the conflict to the main
  agent rather than shipping an ad script.
- Disclosure cannot be buried: #ad must appear before the "...more" fold and never in a
  hashtag pile at the end — platform tools (Paid Partnership label / branded content
  toggle) are required in addition, not instead.
- Vague live windows create drift: give exact date ranges and time zones; "next week"
  produces missed embargoes.
- Regulated categories (health, finance, supplements) carry claim risk — keep claim
  language verbatim from legal; creators may not paraphrase efficacy statements.
- Do not brief usage rights that were not contracted: if whitelisting was never
  negotiated, the brief cannot request Spark Ads access.
- Unanswered creator questions at briefing time resurface as revision rounds later;
  run a 24-hour Q&A window and update the FAQ appendix for everyone.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Brief delivered before contract close | 100% of signed creators | Briefs trailing signatures |
| Mandatory messages per brief | 2–3 | 5+ (scripted-ad territory) |
| First draft received within 5 days of brief | ≥70% of roster | Majority drafting in final week |
| On-brief first drafts | ≥70% | <50% means the brief was unclear |
| Approval rounds per draft | ≤2 | 3+ rounds signals briefing failure |
| Disclosure compliance at go-live | 100% | Any post live without clear #ad |

## Handoffs

- → **negotiation:** deliverables matrix and usage-rights plan feed the offer before
  signatures; changes after signing require renegotiation.
- → **content-collaboration:** hand the approved briefs plus approval SLA; approvals
  enforce the brief, not personal taste.
- → **campaign-management:** supply the deliverables calendar (dates, platforms, tracking
  mechanics) as the go-live checklist source.
- → **tracking-measurement:** deliver the code/UTM naming scheme so tracking is set up
  before the first post goes live.
- ↑ **influencer-marketing-agent:** escalate stakeholder message conflicts and compliance
  gray areas rather than embedding them silently.
