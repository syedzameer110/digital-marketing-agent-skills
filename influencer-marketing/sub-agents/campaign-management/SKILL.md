---
name: influencer-campaign-management
description: Runs the live influencer campaign calendar end to end — master posting schedule across creators and time zones, go-live checklists (link, code, disclosure, tracking), late-post escalation, top-performer boost decisions within 48 hours, and UGC capture for social proof. Use this skill whenever the user mentions managing an influencer campaign, creator timelines, "did everyone post", coordinating multiple creators, campaign flight oversight, or boosting influencer posts as ads — even if they just say "our creators go live next week".
---

# Campaign Management — Influencer Marketing Sub-Agent

## Role & Mission

Deliver every contracted post, on time, compliant, and tracked — then squeeze more from
the flight by boosting winners while they are hot. Research and negotiation create
potential; this agent converts it into shipped deliverables and live-moment decisions.
It owns the master calendar, the per-post go-live checklist, creator communication
cadence during the flight, and the quick-turn decisions (boost, extend, escalate) that
separate managed campaigns from posted-and-prayed ones.

## When to Use

- Creators are approved and the flight window opens within days
- "Manage the campaign" or "keep the creator posts on track"
- Multiple creators posting across platforms and time zones in one flight
- A creator missed a live window or a post needs pulling/editing
- A post is over-performing and should become a Spark Ad / whitelisted ad quickly
- Product or launch-date changes ripple through the creator calendar

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Approved-content package per creator | Yes | From content-collaboration |
| Deliverables calendar + live windows | Yes | Dates, platforms, time zones |
| Go-live checklist (code, link, disclosure) | Yes | From briefing + tracking setup |
| Boost/amplification rules | Preferred | Boost threshold, Spark/whitelist rights |
| Escalation contacts (creator + internal) | Preferred | Agents, Slack channels |
| Flight budget for boosts | Optional | e.g. $2K amplification reserve |

## Output Contract

Return: (1) flight status board (live vs plan), (2) per-post go-live checklist results,
(3) exception log with resolutions, (4) boost decisions with rationale, (5) end-of-flight
delivery summary. Core status-board format:

```markdown
| Creator | Deliverable | Scheduled | Posted | Checklist | Early metrics (24h) | Action |
|---|---|---|---|---|---|---|
| @maya.moves | IG Reel | Mar 5, 11:00 ET | Mar 5 11:04 | PASS | 3.1K likes, 412 comments, ER 4.2% | Boost candidate — send to paid review |
| @devbuilds | TikTok | Mar 6, 17:00 PT | Missed | — | — | Escalated to agent; new window Mar 8 |
| @LenaSpaces | YT integration | Mar 9 | Mar 9 09:00 | PASS (code in desc.) | 18K views, 240 clicks | Feature in monthly report |
```

Go-live checklist rule: every post clears 5 gates before "live" is recorded — content
matches the approved file, disclosure visible, code/link correct and firing, live window
respected, screenshot/URL archived.

## Workflow

1. Build the master flight calendar: every deliverable with platform, date-time (with
   time zone), code/UTM assignment, and the creator's local posting habit — stagger
   nano/micro first for social proof, mid/macro at reach moments.
2. Run a T-48h readiness sweep: confirm with each creator (or agent) that the approved
   file is in hand, product is with them, and any link-in-bio/sticker setup is ready.
3. On posting day, verify each go-live within 2 hours: correct content, disclosure
   prominent, code/link working (click-test the UTM), and archive the URL/screenshot —
   stories vanish in 24 hours, so capture immediately.
4. Monitor early metrics at the 24-hour mark: ER vs tier band, views, comments sentiment;
   flag underperformers (silent boosted-audio failure, wrong link) for creator fixes.
5. Make the boost call within 48 hours: posts beating tier ER benchmarks and CPE
   projections get proposed for Spark Ads / whitelisting (rights permitting) with the
   amplification budget owner.
6. Manage exceptions daily: missed windows get a new committed slot within 24 hours;
   off-brand or error posts get edit/delete requests logged with creator response times.
7. Keep a communication heartbeat: daily check-in thread during flight weeks, instant
   praise on strong posts (relationship capital compounds), no radio silence.
8. Capture social proof as it happens: top comments, creator posts, and screenshots flow
   to social-media and content teams for organic reuse and landing-page proof.
9. Close the flight: reconcile the delivery summary (planned vs posted vs exceptions),
   hand the complete per-post data package to tracking-measurement, and file lessons
   (late creators, compliance catches) for the next briefing cycle.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Master calendar | Notion / Airtable / Google Sheets | One row per deliverable, status colors |
| Campaign + creator ops | GRIN, Aspire, CreatorIQ | Product seeding, postings, and comms in-platform |
| Live-post verification | Manual checks + platform analytics | Within 2 hours of each go-live |
| Boost setup | TikTok Ads Manager (Spark Ads), Meta Ads Manager (partnership ads) | Needs contracted ad access |
| Team comms | Slack (campaign channels) | Daily flight heartbeat |
| Archiving | Drive folder per flight + screenshots | Stories/metrics expire fast; evidence first |

## Example AI Prompt

```text
You are an influencer campaign manager. Run flight week for {CAMPAIGN NAME}
({DATES}, {N} creators, platforms: {PLATFORMS}).

Assets: approved-content calendar {PASTE/ATTACH}; codes/UTMs {SCHEME}; boost rights
{SPARK/WHITELIST WHERE CONTRACTED}; amplification budget {AMOUNT}; escalation contacts
{AGENTS/INTERNAL}.

Deliver:
1. A master calendar with staggered posting order (nano/micro proof first, macro at
   reach moments) with dates, times, and time zones.
2. A go-live checklist per post: approved file match | disclosure | code/link firing |
   window respected | archive captured.
3. A daily monitoring plan: 24-hour metric checks vs tier ER bands, sentiment scan,
   underperformer diagnostics.
4. Boost decision rules: which posts qualify within 48 hours and the approval flow.
5. An exception playbook: missed window, wrong link, disclosure miss, negative comments.
Output the flight status board you will maintain and the end-of-flight summary format.
```

## Edge Cases & Guardrails

- Boosting without contracted ad rights is a contract breach: verify Spark/whitelist
  terms per creator before boosting; if absent, route to negotiation for a quick
  rights addendum or skip the boost.
- Never edit a live creator post unilaterally — captions and content are the creator's
  voice; request edits, document responses, and only pull posts for compliance breaches.
- Story metrics expire in 24 hours: capture screenshots/exports within 48 hours or the
  reporting baseline is permanently incomplete.
- Time-zone drift causes missed windows: state every slot in the creator's local time
  and UTC; "11:00" alone posts at midnight somewhere.
- A late creator is escalated within 24 hours, not "given space" — the flight calendar,
  paid amplification, and launch embargoes all depend on the slot.
- Negative comment storms on a live post trigger the brand-safety playbook: slow the
  boost, alert the main agent, and agree the response posture with the creator.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| On-time post rate | ≥95% of contracted deliverables | <85% or repeated same-creator misses |
| Go-live checklist completion | 100% of live posts | Any post live with broken link/code |
| Boost decision turnaround | ≤48h from posting | Winners identified after the peak |
| Exception resolution time | <24h per issue | Multi-day unresolved escalations |
| Posts archived (URL/screenshot) | 100% | Missing story data at reporting time |
| Early-metric coverage | 24h check on 100% of posts | Posts discovered "live" days later |

## Handoffs

- → **tracking-measurement:** deliver the complete per-post data package (URLs, archives,
  early metrics, spend status) for attribution and the post-flight report.
- → **negotiation:** flag missed-deliverable disputes and rights gaps found mid-flight
  (boost requests without contracted ad access).
- → **relationship-building:** pass creator reliability and responsiveness records —
  flight behavior is ambassador-candidate evidence.
- ↔ **social-media-marketing-agent:** hand rights-cleared top posts and UGC captures for
  organic reuse; receive trend/timing guidance for posting slots.
- ↑ **influencer-marketing-agent:** escalate compliance breaches, comment storms, and
  any decision to pull a live post.
