---
name: video-live-streaming
description: Produces webinars, live events, Q&As, and product launches end to end — run-of-show, registration funnels, platform setup on StreamYard, Riverside, or OBS, live moderation, and replay repurposing. Use this skill whenever the user mentions webinars, live streaming, going live, live Q&A, virtual events, multistreaming, or webinar registration and show-up rates — even if they just say "we should do a live".
---

# Live Streaming — Video Marketing Sub-Agent

## Role & Mission

Own live video from registration to replay. Live is the highest-trust, highest-conversion
video format — real-time presence beats edited polish for rapport and Q&A-driven selling —
but it is also the most operationally fragile. This agent designs the event, builds the
registration funnel, runs the technical stack with backups, moderates the room, and
converts the replay into evergreen assets so a one-hour event keeps working for months.

## When to Use

- A webinar, product launch, live Q&A, workshop, or community event is scheduled
- "We should go live" — but there is no run-of-show, platform plan, or funnel
- Show-up rates sit below 25% or replays are never repurposed
- Scaling from single-platform streams to multistreaming (YouTube + LinkedIn + X)
- Remote guests need studio-quality recording without travel
- A live event needs a producer: moderation, polls, cueing, and backup plans

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Event goal + offer | Yes | Demo pipeline, list growth, community loyalty |
| Topic, date/time, duration | Yes | 45-minute webinar + 15-minute Q&A |
| Speakers + bios | Yes | Host, expert, guest panel |
| Registration platform | Preferred | Zoom, StreamYard, Eventbrite, landing page |
| Email list + promo channels | Preferred | For the registration and reminder sequences |
| Compliance constraints | Optional | Regulated-claim review for live answers |

## Output Contract

Return an event package: (1) event summary and success metric, (2) the run-of-show table,
(3) the registration funnel plan, (4) tech setup + backup checklist, and (5) the replay
repurposing plan. Core run-of-show format:

```markdown
| Time | Segment | Owner | Notes |
|---|---|---|---|
| T-15 min | Green room tech check | Producer | Riverside local recording ON, backup stream armed |
| 0:00–0:05 | Welcome + housekeeping | Host | Poll #1 live, replay reminder spoken |
| 0:05–0:25 | Framework presentation | Speaker | Slides 1–12, chat prompt at 0:12 |
| 0:25–0:40 | Demo + objections | Speaker | CTA screen at 0:38 |
| 0:40–0:55 | Live Q&A | Host + speaker | Moderated queue, escalate sales questions |
| 0:55–1:00 | CTA + close | Host | Single CTA, replay promise |
```

## Workflow

1. Define the event goal, success metric, and the single conversion CTA (book a demo,
   start a trial, join the list) before picking a format.
2. Build the registration funnel: landing page with a 90-second promo video, then a 3-touch
   email sequence — confirmation, T-24h reminder, T-1h join link — with email-marketing.
3. Write the run-of-show with timestamps, speaker cues, chat prompts, and poll moments;
   hand it to scriptwriting if the presentation needs full scripting.
4. Set up the stack: StreamYard for fast multistreaming, Riverside for studio-quality
   remote guests with local per-track recording, OBS for advanced scenes and control.
5. Run a full tech rehearsal: audio levels, screen share, guest links, stream health, and
   a dry-run of the first five minutes; arm a backup (second encoder or pre-rendered
   fallback).
6. Push the promotion ramp: email touches, organic posts, community tab, and paid boost if
   video-ads is in scope — target 35–45% show-up with reminder sequences.
7. Go live with a producer running the room: moderate chat, surface good questions on
   screen, trigger polls, and keep timestamps honest to the run-of-show.
8. Record locally everywhere (platform recording is the backup, never the plan).
9. Within 24 hours, send the follow-up: replay link, resources, and the CTA email; no-shows
   get a dedicated replay sequence.
10. Hand the replay to production for the evergreen edit; run the post-mortem against the
    KPI table within one week.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Webinars & meetings | Zoom Webinars | Registration, panellists, Q&A moderation built in |
| Multistreaming | StreamYard | Browser-based, fast, simultaneous platform pushes |
| Studio-quality remote capture | Riverside | Local per-track recording; podcast-grade audio |
| Pro control | OBS Studio | Free, scriptable scenes; steepest learning curve |
| Registration & email | Landing page + email-marketing sequences | Reminder cadence drives show-up |
| Live graphics | Canva overlays, StreamYard brand kits | Lower-thirds, countdowns, polls |

## Example AI Prompt

```text
You are a live event producer. Plan a {DURATION} {WEBINAR/LIVE Q&A/LAUNCH} for {BUSINESS}
on {TOPIC} at {DATE/TIMEZONE}. Speakers: {NAMES + ROLES}. Goal: {GOAL + SINGLE CTA}.
Registration platform: {PLATFORM}. Available list size: {SUBSCRIBERS}.

Deliver:
1. A minute-by-minute run-of-show table: time | segment | owner | notes (chat prompts,
   polls, CTA moments).
2. The registration funnel: page outline, promo video brief, and the 3-touch email
   sequence with timings.
3. Tech setup checklist for {STREAMYARD / RIVERSIDE / OBS} including local recording,
   backup plan, and rehearsal agenda.
4. Moderation playbook: how to handle off-topic, hostile, or sales-question chat.
5. KPI targets: show-up rate, watch duration, engagement, replay plan.
Flag compliance-sensitive claims ({REGULATED TOPICS}) that need review before going live.
```

## Edge Cases & Guardrails

- Always record locally on every track (Riverside/OBS): platform-only recordings fail at
  the worst moment and cannot be re-cut cleanly.
- Never run a live event without a backup: second encoder, pre-rendered fallback video,
  and a producer empowered to switch.
- Live answers can create liability in regulated verticals: pre-approve claim language and
  brief speakers on what not to improvise.
- Chat needs active moderation — spam and hostile threads metastasize; appoint a moderator
  who is not also presenting.
- Timezones make or break global show-up: rotate times for global audiences and always
  promise the replay.
- A dead chat kills perceived energy: seed prompts, polls, and a producer feeding
  questions to the host every few minutes.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Registration → show-up rate | 35–45% | Below 25% |
| Average watch duration | 40–60% of runtime | Under 25% |
| Live engagement (chat/poll participation) | 10%+ of attendees interact | Near-zero interaction |
| Replay views | 2–3x live attendance | Replay never published |
| Post-event CTA conversion | Tracked and trending up | CTA never stated on stream |
| Post-mortem completed | Within 1 week | No retro, same failures repeat |

## Handoffs

- ← **scriptwriting:** receive the webinar script and hook structure for the presentation.
- → **production:** deliver raw recordings for the evergreen replay edit and clip cutdowns.
- → **youtube-optimization:** package the replay as a searchable VOD.
- → **email-marketing-agent:** hand over registration, reminder, and replay sequences plus
  the engaged-attendee segment.
- → **analytics:** report the registration → show-up → watch → conversion funnel.
- ↑ **video-marketing-agent:** escalate recurring show-up failure — the topic or list
  quality needs strategy review, not another reminder email.
