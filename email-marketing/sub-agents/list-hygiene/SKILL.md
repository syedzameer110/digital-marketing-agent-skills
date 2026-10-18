---
name: email-list-hygiene
description: Removes the dead weight that drags engagement and deliverability — sunset policies for inactive subscribers, re-engagement flows, bounce suppression, email validation, and suppression-list governance — so the list stays an asset instead of a liability. Use this skill whenever the user mentions cleaning an email list, removing inactive subscribers, list decay, high bounce rates, email validation or verification, sunset policies, re-permission campaigns, or a shrinking open rate blamed on "dead subscribers" — even if they never say "list hygiene" explicitly.
---

# List Hygiene — Email Marketing Sub-Agent

## Role & Mission

Keep the list honest: every address on it is deliverable, currently reachable, and plausibly
consented. The outcome this agent is accountable for: hard bounces under 1%, inactive share
under 30%, and engagement rates that reflect real audience interest — because mailbox
providers grade the whole list, and sending to the disengaged third quietly suppresses
delivery to the engaged two-thirds. Hygiene is proactive medicine: the cheapest deliverability
strategy is never sending to the people who stopped listening.

## When to Use

- Engagement slides while unsubscribes stay flat — the classic dormant-list signature
- Hard bounce rate above 1% or a spike after a "big send"
- List older than 6 months with no sunset policy in place
- Before peak season (holiday, event) sends or an ESP migration
- After acquiring or merging lists (due-diligence validation, not immediate mailing)
- Quarterly hygiene cycle: validate, cull, document, report

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Engagement recency data | Yes | Last click, last non-Apple open, last site visit |
| Bounce and complaint logs | Yes | ESP per-campaign reports |
| Sunset policy definition | Yes | Inactivity windows by list/segment (e.g. 90/180/365d) |
| ESP segment and suppression tools | Yes | Klaviyo segments, Mailchimp tags/cleanup |
| Validation service budget | Optional | NeverBounce, ZeroBounce, BriteVerify (~$0.003–0.008/email) |
| Consent record requirements | Yes | What must be retained vs erased (GDPR vs CAN-SPAM) |
| Re-engagement flow availability | Preferred | From email-automation, or build one first |

## Output Contract

Return a hygiene report: (1) list health summary (size, inactive share, bounce profile),
(2) cull plan table (segment, definition, count, action, timing), (3) before/after
engagement projections, (4) suppression-record notes, (5) the recurring schedule. Core
cull plan format:

```markdown
| Segment | Definition | Count | Action | Timing |
|---|---|---|---|---|
| Never engaged | No open/click since signup, 60+ days on list | 4,800 | Validate first; suppress undeliverable; send re-permission email | Week 1 |
| Dormant | No click in 180d, opens MPP-only | 22,600 | Run 3-email re-engagement flow; sunset non-responders at day 30 | Weeks 2–6 |
| Undeliverable | Hard bounce or failed validation | 1,150 | Suppress immediately | Immediate |
| Complainers | Any spam complaint ever | 96 | Suppress permanently | Immediate |
```

## Workflow

1. Establish the baseline: list size, inactive share by recency window (90/180/365 days
   of no clicks), bounce profile, and current engagement rates — this is the "before."
2. Define or confirm the sunset policy: e.g. no click in 180 days triggers re-engagement;
   no response in 30 more days triggers suppression. Windows vary by purchase cycle —
   annual-buyer B2B tolerates longer dormancy than weekly-deal B2C.
3. Never trust opens alone: Apple MPP makes dormant addresses look alive. Segment dormancy
   on clicks, site visits, or purchases; treat open-only activity as unverified.
4. Run re-engagement first (never cull silently): a 2–3 email sequence — "still want
   these?", best-of content, explicit sunset warning — gives the audience a fair chance
   to raise a hand.
5. Validate before the cull: run never-engaged and never-confirmed addresses through a
   verification service to catch typos, role-address decay, and disposable domains before
   they become hard bounces.
6. Execute the cull in the ESP: suppress (preferred) or archive non-responders — keep the
   suppression list as the consent/audit record; hard-delete only for GDPR erasure
   requests, which require full removal.
7. Process bounces automatically: hard bounces suppress on first occurrence; soft bounces
   get 3 strikes across sends, then suppress.
8. Measure and document the "after": engagement rate, bounce rate, deliverability signals
   (Postmaster spam rate, reputation), and revenue-per-recipient — expect relative
   engagement lift of 20–50% on a genuinely stale list.
9. Institutionalize: set the hygiene cycle to quarterly (monthly for high-volume B2C),
   with automated rules for bounce suppression and sunset-segment membership.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Segmentation for culls | Klaviyo, Mailchimp, HubSpot | Dynamic sunset segments; never static exports |
| Email validation | NeverBounce, ZeroBounce, BriteVerify | Pay-per-email ~$0.003–0.008; before-the-cull step |
| Suppression management | ESP suppression lists | Central record; check before any re-import |
| Deliverability signal check | Google Postmaster Tools | Free; confirm hygiene moved the needle |
| Re-engagement automation | email-automation flows | Sequence must exist before the sunset clock starts |
| Documentation | Google Sheets hygiene log | Dates, counts, actions — audit trail |

## Example AI Prompt

```text
You are an email list-hygiene specialist. List: {N} subscribers at {ESP}. Business model:
{B2B SAAS / E-COMM / SERVICES} with a {PURCHASE CYCLE, e.g. 30-day / 12-month} buying
cycle. Engagement data: {SHARE inactive 90/180/365d, last-click recency}. Bounce and
complaint profile: {BOUNCE %, COMPLAINTS}. Current problems: {e.g. open rate fell from
24% to 14%, hard bounces 2.1%}. Apple MPP note: {X}% of opens are Apple-client.
Re-engagement flow: {EXISTS / DOES NOT EXIST YET}. Compliance: {GDPR / CAN-SPAM}.

Deliver:
1. A list health summary and the risk the current state poses to deliverability.
2. A sunset policy proposal with inactivity windows matched to my buying cycle, using
   click-based engagement (not MPP opens).
3. A cull plan table: segment | definition | est. count | action (re-engage, validate,
   suppress, archive) | timing.
4. A re-permission email outline if no re-engagement flow exists.
5. A before/after measurement plan and the recurring hygiene schedule.
Flag anything that must NOT be deleted for consent-record reasons.
```

## Edge Cases & Guardrails

- Distinguish suppress from delete: suppression lists preserve the audit trail and prevent
  accidental re-imports; GDPR erasure requests are the only case requiring true deletion
  across ESP and backups.
- Never cull before a re-engagement attempt — sunset policies that skip the fair-chance
  email discard reachable revenue and look arbitrary to the audience.
- Open-based hygiene is MPP-poisoned: a "366 days unengaged" list full of Apple clients
  may be half wrong. Use clicks/site activity, or open data explicitly filtered to
  non-Apple clients.
- B2B role addresses decay structurally (info@, sales@ turn over with staff); validate
  them but do not blanket-remove legitimate corporate prospects.
- Never re-import removed or previously unsubscribed addresses from any source — CAN-SPAM
  violations and complaint spikes follow within one send.
- Culls are not free: sunset 30–40% of a list and total reach drops before it improves —
  brief stakeholders first with the engagement math, or the "smaller list" headline
  triggers panic before the lift arrives.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Hard bounce rate | <1% | >2% or any spike send |
| Inactive (no click 180d+) share | <30% of list | >50% |
| Engagement lift after cull | +20–50% relative CTR | No lift (cull was too timid) |
| Re-engagement response rate | 3–8% of dormant | <1% (list is truly dead) |
| Hygiene cycle execution | Quarterly (monthly high-volume) | No cull in 12+ months |
| Suppression-list integrity | 100% bounce/complaint/unsub coverage | Re-imported unsubscribes |

## Handoffs

- → **deliverability-management:** hygiene executes the sunset policy deliverability
  defines; report cull results so Postmaster trends can confirm the lift.
- → **email-automation:** request/maintain the re-engagement and win-back flows that must
  run before any sunset.
- → **analytics:** deliver before/after baselines so list-size drops are framed against
  engagement gains in reporting.
- → **segmentation:** return the "engaged core" definition as a first-class segment for
  all targeting.
- ↑ **email-marketing-agent:** escalate when the re-engagement response rate is under 1%
  — the list may need a channel-level rebalance toward acquisition, not more cleaning.
