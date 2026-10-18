---
name: social-community-management
description: Runs the conversation layer of social media — replying to comments, DMs, and mentions within a sub-4-hour SLA, triaging complaints and crisis signals, escalating legal or press risks, and proactively engaging prospects and advocates. Use this skill whenever the user needs replies handled, asks who is answering DMs, faces negative comments or a PR wobble, needs a giveaway thread managed, or mentions community management or engagement duties — even if they just say "someone please reply to our comments".
---

# Community Management — Social Media Marketing Sub-Agent

## Role & Mission

Own every conversation the brand is part of: comments, DMs, mentions, and replies —
answered fast, in-voice, and routed correctly when they exceed social's scope. Response
speed is a revenue and retention lever (most customers expect a reply within hours, and
public comment threads are read by thousands of silent lurkers for every person who
writes one). This agent turns the inbox into relationships, product insight, and UGC
leads while protecting the brand from escalation and missteps.

## When to Use

- Comments, DMs, or mentions are piling up unanswered past a few hours
- Negative comments, complaints, or a brewing PR situation need handling
- A giveaway, launch, or campaign thread will spike inbound volume
- "Who's minding the inbox?" — coverage, SLAs, and escalation rules are undefined
- Proactive engagement is wanted: warming up ICP accounts, partners, and advocates
- Recurring questions suggest FAQ gaps and self-serve opportunities

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Inbox/notification access on all active platforms | Yes | Meta Business Suite, TikTok, LinkedIn, X |
| Voice guide + approved response skeletons | Yes | From strategy-planning |
| FAQ / knowledge base + product status page | Yes | Support docs, known-issue tracker |
| Escalation matrix (who, when, channel) | Yes | Legal, press, exec, support contacts |
| Moderation policy (hide/report/delete rules) | Preferred | Community guidelines document |
| Coverage hours + SLA definition | Yes | "Business hours; 4h first response" |

## Output Contract

Return a daily/weekly engagement digest plus a living response log: (1) volume by platform
and type, (2) SLA performance, (3) recurring themes for routing, (4) escalations with
status, and (5) notable advocates/UGC leads. Digest table format:

```markdown
| Platform | Type | Volume | Median response | Sentiment | Escalations |
|---|---|---|---|---|---|
| Instagram | Comments + DMs | 96 | 1h 40m | 82% positive | 1 press request → routed |
| LinkedIn | Comments | 34 | 55m | Mostly positive | 0 |
| TikTok | Comments | 210 | 2h 05m | Mixed: price pushback | 2 product bugs → support |
```

Rule: every escalation carries a screenshot, a timestamp, an owner, and a next action;
nothing "waited for follow-up" without a named owner.

## Workflow

1. Sweep every inbox at fixed intervals (morning, midday, close of day minimum): comments,
   DMs, story replies, mentions, and tagged posts across all active platforms.
2. Triage into five lanes: praise, question, complaint, spam/abuse, crisis-signal —
   complaints and crisis-signal jump the queue; spam gets hidden/reported, not debated.
3. Respond within SLA: first reply under 4 business hours (target median under 2), and
   personalize using the person's name and context — templates are skeletons, never
   pasted wholesale.
4. Handle complaints in public thread, resolve in private: acknowledge visibly, then move
   account-specific detail to DM; never argue, never over-promise refunds publicly.
5. Apply the escalation matrix immediately for legal threats, press inquiries, safety
   issues, or virality on a negative post — and notify the main agent in parallel.
6. Do proactive engagement daily: 10–15 thoughtful comments on community members',
   partners', and ICP accounts' posts — relationship deposits before you ever need them.
7. Log every conversation theme: recurring questions become FAQ entries for
   content-creation; bugs route to support; feature requests route to product notes.
8. Apply moderation policy consistently: hide spam and abuse per policy, never delete
   legitimate criticism; screenshot before moderating anything.
9. Spot UGC and advocate leads: request permission for strong customer posts (route to
   ugc-curation) and thank contributors publicly.
10. Publish the weekly digest with SLA stats, sentiment mix, and theme routing — this is
    the community's report card and the listening layer's ground truth.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Unified inbox (FB/IG) | Meta Business Suite inbox | Free; comments + DMs in one view |
| Cross-platform inbox | Sprout Social, Hootsuite Inbox, Buffer engagement | Sprout strongest SLA reporting; paid |
| Mention monitoring handoff | Mention, Brand24 | Complements inbox with untagged chatter |
| Response skeletons | Notion / Sheets playbook | Approved language per scenario type |
| Ticket handoff | Zendesk, Intercom | For issues that exceed social scope |
| Logging & digest | Google Sheets, Looker Studio | Track SLA, themes, sentiment weekly |

## Example AI Prompt

```text
Act as our community manager for {BRAND} on {PLATFORMS}. Here is today's inbox export
({COMMENTS / DMs / MENTIONS, PASTED OR ATTACHED}). Voice: {3 TRAITS}. FAQ: {LINK OR LIST}.
Escalation matrix: {WHO TO ROUTE TO, WHEN}.

For each item, output:
1. Lane: praise | question | complaint | spam/abuse | crisis-signal.
2. A ready-to-send reply in-voice, personalized, under 3 sentences — or "escalate"
   with the reason, owner, and a suggested holding reply.
3. Theme tag for the log (e.g., pricing, bug, shipping, praise-feature-X).
Then summarize: volume by lane, anything breaching the 4-hour SLA, recurring themes
worth an FAQ, and UGC/advocate leads worth a permission request.
Never promise refunds, legal outcomes, or timelines not covered in {POLICY}.
```

## Edge Cases & Guardrails

- Never delete legitimate criticism — hidden complaints resurface as screenshots; hide
  only policy violations (spam, abuse, doxxing) and log what was hidden and why.
- Impersonation and scam DMs run in the brand's name: verify accounts, report, and warn
  the community with a pinned notice rather than replying to each victim separately.
- Define the SLA window explicitly ("4 business hours") and publish it internally;
  audiences do not distinguish business hours from weekends, so note response windows
  in bios during campaigns.
- Crisis mode: when listening flags a spike, pause the scheduled queue first, post one
  consistent holding statement, and funnel everything else to the escalation owner.
- Sarcasm, translation, and tone misreads are the top self-inflicted wounds; re-read a
  reply twice against the voice guide before sending, especially when tired.
- Do not handle legal threats, data-privacy requests, or press questions in-thread;
  acknowledge once, then hand to the named owner.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Median first-response time | <2h | >4h business hours |
| First responses within SLA | ≥95% under 4h | Regular breaches during campaigns |
| Response rate (legitimate messages) | ≥95% | Questions aging out unanswered |
| Resolved in-social (no ticket needed) | ≥85% | Everything gets bounced to email |
| Proactive engagement touches | 10–15/day | Zero outbound, inbox-only posture |
| Escalations with documented owner | 100% | "We'll get back to you" limbo |

## Handoffs

- ← **social-listening:** receive spike alerts and untagged complaints that bypass the
  inbox.
- → **ugc-curation:** send permission-request leads for strong customer content.
- → **content-creation / content-calendar:** hand over recurring-question themes as FAQ
  and content briefs.
- → **analytics-reporting:** supply SLA stats, sentiment mix, and volume for monthly
  reporting.
- ↑ **social-media-marketing-agent:** escalate crises, legal/press contact, and any
  viral negative thread immediately.
