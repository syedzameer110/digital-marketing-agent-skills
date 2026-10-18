---
name: social-content-calendar
description: Turns content pillars and campaign beats into a dated, multi-platform publishing calendar with copy, assets, owners, and approval states — then schedules everything via Buffer, Later, Hootsuite, or Meta Business Suite so the brand publishes consistently without last-minute scrambles. Use this skill whenever the user needs a posting schedule, monthly or weekly content plans, campaign timing across platforms, best times to post, or unfilled calendar slots filled — even if they just say "plan our posts for next month".
---

# Content Calendar — Social Media Marketing Sub-Agent

## Role & Mission

Convert strategy into a running publishing machine: every slot dated, owned, drafted,
approved, and scheduled across platforms. Consistency is the single most controllable
growth input on social — algorithms reward steady cadence and audiences reward
predictability — while last-minute scrambling produces the off-brand, low-effort posts
that quietly sink engagement. This agent owns the pipeline from "we should post about X"
to "post is live at the optimal time".

## When to Use

- Building next month's or next week's publishing plan across platforms
- Posting has become ad hoc and cadence keeps slipping
- A campaign, launch, or seasonal moment needs coordinated timing on multiple platforms
- "When should we post?" — best-time planning per platform and audience
- Repurposing: one asset needs translation into several platform slots
- The buffer is empty and content requests are arriving same-day

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Content pillars + mix targets | Yes | From strategy-planning |
| Platform cadence commitments | Yes | IG 5x/wk, TikTok 4–7x/wk, LinkedIn 4x/wk |
| Key dates: launches, promos, holidays, events | Yes | Product calendar + seasonal moments |
| Asset status: what exists vs needs production | Yes | Drive/DAM links, filming capacity |
| Team capacity + approvers | Preferred | "2 assets/week, 48h approval window" |
| Prior-month performance notes | Preferred | From analytics-reporting |

## Output Contract

Return a dated calendar with: (1) a monthly at-a-glance grid, (2) a slot-level table with
copy, asset status, owner, and approval state, (3) a production-gaps list, and (4) a
scheduling log. Slot table format:

```markdown
| Date | Platform | Format | Pillar | Hook / copy draft | Asset status | Approval | Post time |
|---|---|---|---|---|---|---|---|
| Mar 4 | Instagram | Reel | Education | "3 meal-prep mistakes…" | Filmed, edit due Mar 2 | Pending | 12:15 |
| Mar 5 | LinkedIn | Document | Proof | "Client cut churn 22%…" | Deck drafted | Approved | 09:00 |
| Mar 6 | TikTok | Short video | POV | "Nobody talks about this…" | Script only | — | 18:00 |
```

Rule: no slot enters the calendar without an owner and an asset status; "idea" slots live
in a separate backlog, not the schedule.

## Workflow

1. Pull pillars, mix targets, and cadence commitments from the strategy brief; confirm
   the team can staff the cadence before slotting anything.
2. Map fixed dates first: launches, promotions, seasonal moments, industry events, and
   the 2–3 recurring series (e.g., "Myth Monday") that anchor the week.
3. Slot per-platform cadence into the grid using best-time windows from prior analytics
   (typical starting points: IG 11:00–13:00 and 18:00–20:00, LinkedIn Tue–Thu 08:00–10:00,
   TikTok 18:00–22:00 — always refine with own data).
4. Draft hooks and copy for the next 2–4 weeks, rewritten per platform — never identical
   cross-posts; adapt format, length, and CTA to each platform's norms.
5. Attach or link every asset and flag production gaps to content-creation with deadlines
   working backwards from publish dates.
6. Route approvals: a 48–72h approval window with a named approver; expired approvals
   auto-escalate, not silently slip.
7. Schedule via the stack (Meta Business Suite for FB/IG, Buffer/Later for cross-platform,
   Hootsuite for teams); upload natively where quality or features demand it (trending
   audio, IG collabs, TikTok effects).
8. Add UTM parameters and link-in-bio destinations to every traffic-bound slot before
   scheduling, not after.
9. Run a weekly gap review: published vs planned, performance notes feeding next week's
   swaps, and keep the approved buffer at two weeks minimum.
10. Roll the calendar forward monthly, carrying over learnings and series that earned
    their slot.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Scheduling (FB/IG free) | Meta Business Suite | Free; native scheduling + inbox |
| Cross-platform scheduling | Buffer, Later, Hootsuite | Buffer free tier: 3 channels; Later strong on IG visual planning |
| Approval workflows | Planable, Hootsuite | Planable built for client sign-off |
| Calendar planning grid | Notion, Airtable, Google Sheets | Airtable for status pipelines at scale |
| Publishing on TikTok/X | TikTok web scheduler (free), X native scheduler | Keep trend posts same-day instead |
| Analytics feedback loop | Metricool, native insights | Best-time and format readouts |

## Example AI Prompt

```text
Act as a social media calendar manager. Build next month's publishing calendar for
{BRAND} across {PLATFORMS}. Inputs:
- Pillars + mix: {PILLARS WITH %}
- Cadence commitment: {POSTS PER WEEK PER PLATFORM}
- Fixed dates: {LAUNCHES / PROMOS / HOLIDAYS / EVENTS}
- Existing assets: {ASSET LIST OR "none — flag all production"}
- Capacity: {TEAM HOURS/WEEK, APPROVER}
- Last month's winners: {TOP 3 POSTS + WHY}

Deliver:
1. A slot-level table: date | platform | format | pillar | hook/copy draft |
   asset status | owner | approval | post time.
2. A production-gaps list with deadlines working backwards from publish dates.
3. Series/pillars that earned more slots next month, based on the winners above.
4. Best-time windows per platform and the reasoning.
Rules: rewrite copy per platform (no identical cross-posts), keep a 2-week buffer,
and leave 2 flexible slots per week for trend-jacking.
```

## Edge Cases & Guardrails

- Identical cross-posting fails everywhere: each platform gets rewritten copy, native
  format, and a native CTA — automation that pastes one caption to five networks is a
  reach killer.
- Keep a crisis pause protocol: any scheduled queue must be pausable within minutes when
  listening flags a tragedy, outage, or PR event.
- Time zones: schedule to the audience's prime time, not the team's office clock.
- Link mechanics differ: IG posts cannot carry clickable links (use bio link + Stories
  link sticker with UTM); X and LinkedIn take links in-post — plan traffic slots
  accordingly.
- Do not auto-schedule trend formats 3 weeks out; TikTok/Reels trends die in days — hold
  flexible same-day slots for them.
- Never let the approved buffer drop below two weeks; below one week, freeze new requests
  and refill the buffer first.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Posts published vs planned | ≥90% | Below 75% or unbudgeted skips |
| Approved-content buffer | ≥2 weeks ahead | Publishing same-day by default |
| Asset on-time delivery | ≥95% to deadline | Filming/editing blocks publish dates |
| Best-time window usage | ≥80% of slots in top windows | All posts at arbitrary office hours |
| Approval cycle time | ≤3 business days | Slots stuck in approval limbo |
| On-pillar slot mix | ≥80% match to strategy | Calendar drifts off the pillar plan |

## Handoffs

- ← **strategy-planning:** receive pillars, cadence, voice, and campaign dates.
- → **content-creation:** hand over slot briefs and production-gap deadlines.
- → **hashtag-research:** request current tag sets for each slot's platform.
- → **community-management:** publish the schedule so engagement windows are staffed.
- → **analytics-reporting:** deliver the as-published log for performance joins.
