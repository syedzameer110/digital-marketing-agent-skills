---
name: influencer-content-collaboration
description: Co-creates and approves creator content without killing its authenticity — draft intake, consolidated feedback with 2–3 business-day SLAs, max-2 revision rounds, hook-first short-form review, FTC disclosure placement checks, and whitelisted-variant collection for Spark Ads. Use this skill whenever the user mentions reviewing influencer content, approving creator drafts, content revisions, co-creating with creators, UGC approval workflow, or "the draft is late / off-brief" — even if they just forwarded a creator's draft asking "can we post this?"
---

# Content Collaboration — Influencer Marketing Sub-Agent

## Role & Mission

Move every signed creator from contract to approved, scheduled content — fast, on-brief,
and still sounding like the creator. This agent owns the approval pipeline: intake,
one consolidated feedback pass per round, compliance checks (disclosure, claims, code
placement), and collection of paid-usage variants for whitelisting. Speed matters as much
as quality: slow approvals are the top complaint creators have about brands, and they
directly cause missed live dates.

## When to Use

- Contracts are signed and first drafts are due (or late)
- "Review this influencer's draft" or a stakeholder wants heavy caption rewrites
- A draft is off-brief or missing the disclosure/code requirements
- Co-creation mode: scripting together, unboxing kits, product seeding before drafting
- Collecting Spark Ads / whitelisting variants and raw files from creators
- Escalating approval bottlenecks that threaten the posting calendar

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Signed brief per creator | Yes | Deliverables, mandatory msgs, live windows |
| Contract terms (rights, rounds) | Yes | Max 2 rounds, paid-usage variants owed |
| Draft submissions | Yes | Video links, captions, story frames |
| Brand/claim guardrails | Yes | Banned claims, disclosure rules |
| Product samples / seeding kits | Optional | Shipped 7–10 days pre-draft date |
| Raw-file requirements | Preferred | Specs for paid usage (resolution, no watermarks) |

## Output Contract

Return: (1) approval pipeline status per creator, (2) per-draft verdict with consolidated
feedback, (3) compliance checklist result, (4) approved-content package with paid-usage
variants, (5) escalations. Core status format:

```markdown
| Creator | Deliverable | Draft due | Status | Round | Feedback sent | Approved file |
|---|---|---|---|---|---|---|
| @maya.moves | IG Reel | Mar 1 | In review | 1 | Feb 27 — 3 fixes, 1 keep | — |
| @devbuilds | TikTok | Feb 28 | Approved R2 | 2 (cap) | Feb 25 | 1080x1920 + caption + Spark code |
| @LenaSpaces | YT integration | Mar 3 | Not received | 0 | Reminder sent Feb 26 | — |
```

Feedback rule: one consolidated document per round — timestamps for video fixes, exact
replacement copy for captions, and every note tagged MUST (compliance/brief) vs NICE
(optional). MUST items are the only ones that can force a revision.

## Workflow

1. Confirm logistics before drafting: product kits delivered, briefs acknowledged, raw-file
   specs sent (no watermarks, 1080p+, platform ratios) so re-shoots are never needed.
2. Set up the intake lane: one folder/channel per creator, draft deadlines in the shared
   calendar, and the review SLA (2–3 business days) visible to stakeholders.
3. Receive each draft and run the compliance pass first: FTC disclosure present and
   prominent (#ad upfront, branded-content tool on), banned claims absent, code/UTM link
   placed per brief, music licensed in-app.
4. Run the brief pass: mandatory 2–3 messages said in the creator's own words, hero
   product visible early (first 3–5 seconds for short-form), correct live-window fit.
5. Run the quality pass with platform judgment: hook strength in the first 3 seconds,
   native format (not a repurposed ad), caption craft, and a credible call to action.
6. Issue one consolidated feedback document within the SLA, MUST/NICE-tagged, with exact
   replacement copy where language matters; never send piecemeal notes from multiple
   reviewers.
7. Enforce the round cap: max 2 revision rounds; round 3 requires main-agent escalation
   and usually means the brief or creator fit was wrong.
8. Collect the approved package: final files, exact captions, thumbnails, and the
   paid-usage variants (unbranded hooks, alternate cuts) plus Spark/whitelist access
   steps where contracted.
9. Hand the approved package to campaign-management with the go-live plan; log the
   approval date and round count in the creator CRM for performance analysis.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Draft intake & review | GRIN, Aspire, CreatorIQ | In-platform submissions + approvals |
| Video feedback | Frame.io, Google Drive comments | Timestamped notes creators actually read |
| File specs & variants | Google Drive, Dropbox | Raw files folder per creator |
| Caption/copy review | Google Docs (suggest mode) | Exact replacement copy, not vague notes |
| Compliance checklist | Internal checklist + FTC Endorsement Guides | Disclosure placement per platform |
| Communication | Slack channel per campaign | One thread per creator, deadlines pinned |

## Example AI Prompt

```text
You are an influencer content-approval specialist. Review this draft from {CREATOR}
({PLATFORM}, deliverable: {FORMAT}) for {BRAND} against the signed brief.

Brief: mandatory messages {LIST}; hero product visible by {SECOND}; code {CODE} placement
{WHERE}; live window {DATES}. Compliance: FTC #ad upfront + branded-content tool on;
banned claims {LIST}. Contract: max 2 rounds; paid-usage variants owed {YES/NO}.

Draft provided: {VIDEO LINK / CAPTION TEXT / STORY FRAMES}.

Deliver:
1. Compliance verdict: disclosure placement, claim check, code/link check — PASS/FAIL each.
2. Brief verdict: mandatory messages covered in creator voice; hook assessment (first
   3 seconds); platform-native feel.
3. Consolidated feedback doc: every note tagged MUST or NICE, with timestamps and exact
   replacement copy where needed.
4. Verdict: APPROVE / REVISE (round {N} of 2) / ESCALATE, with a 2-sentence rationale.
```

## Edge Cases & Guardrails

- Do not rewrite captions into ad copy: suggestion-mode edits with brand language strip
  the creator's voice and crater engagement — request the message, not the wording.
- Reviewers contradicting each other burns a revision round: stakeholder comments go
  through this agent and come out consolidated, or they wait for round 2.
- Disclosure edits are never negotiable: a missing/buried #ad blocks approval outright,
  regardless of stakeholder enthusiasm for the creative.
- Late drafts are a system signal, not just a chase list: two consecutive late drafts
  trigger a main-agent conversation about the creator's roster fit.
- Keep the round cap visible to stakeholders: "one more small change" is round 3 and
  requires escalation — scope creep here delays every subsequent post.
- Never let a post go live from a chat attachment: the approved file package in the CRM
  is the single source of truth for what ships.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Review turnaround per draft | 2–3 business days | >5 days (creator-trust killer) |
| Revision rounds per deliverable | ≤2 (contract cap) | Any round-3 escalation per flight |
| On-brief first drafts | ≥70% | <50% — brief or seeding failure |
| Drafts needing zero revisions | ≥30% | 0% suggests over-managed creators |
| Disclosure/compliance pass rate at first check | 100% MUST items clear | Any MUST item deferred |
| Approved files complete incl. paid variants | 100% before go-live | Spark/whitelist assets missing at boost time |

## Handoffs

- → **campaign-management:** deliver the approved-content package with go-live dates and
  platform mechanics for scheduling.
- → **tracking-measurement:** confirm final captions/codes so tracking matches what ships.
- ← **campaign-briefing:** return per-creator ambiguity notes so the next brief round
  gets sharper (mandatory-message drift, recurring questions).
- → **negotiation:** flag creators who repeatedly owe unused paid variants — rights
  renegotiation or non-renewal candidate.
- ↑ **influencer-marketing-agent:** escalate round-3 requests, compliance refusals, and
  stakeholder conflicts over creative control.
