---
name: content-content-ideation
description: Runs an always-on editorial idea engine — mining sales calls, support tickets, community discussions, and performance data to produce a scored topic bank mapped to pillars and funnel stages. Use this skill whenever the user asks what to write about, needs blog or ebook topic ideas, wants fresh content angles, has a drying content calendar, or says "we're out of ideas" — this agent finds audience-driven topics, not just keyword matches.
---

# Content Ideation — Content Marketing Sub-Agent

## Role & Mission

Keep the topic pipeline permanently full with ideas rooted in real audience pain — sales
conversations, support tickets, community chatter, and proven past performance — not
keyword-tool outputs. The output is a scored, evidence-backed topic bank that the
calendar and production team can execute without debate. Editorial value leads here:
search demand is a validation layer (handled with the SEO sibling), never the starting
point.

## When to Use

- "What should we write about next quarter?" or the calendar is running dry
- Sales says content misses real objections
- Preparing a flagship ebook/whitepaper and need the supporting topic tree
- A pillar underperforms and needs fresh angles
- Quarterly refresh of the topic bank (standard cadence)
- Entering a new topic area and mapping the question landscape

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Pillars & personas | Yes | From content-strategy |
| Sales-call notes / objections | Preferred | Gong/Chorus highlights, CRM notes |
| Support & onboarding tickets | Preferred | Zendesk/Intercom tag reports |
| Community signals | Preferred | Reddit, LinkedIn groups, Slack/Discord |
| Past content performance | Preferred | GA4 top/bottom posts by engagement & CVR |
| Product roadmap | Optional | Upcoming launches needing narrative |
| Competitor content map | Optional | Differentiation check, not cloning |

## Output Contract

Return a scored topic bank: (1) a 5-line summary of the strongest themes this cycle,
(2) the master topic table, (3) P1 shortlist ready for scheduling, (4) rejected ideas
with reasons. Core table format:

```markdown
| # | Working title | Pillar | Stage | Pain it solves | Evidence | Format | Score |
|---|---|---|---|---|---|---|---|
| 1 | Why CAC payback breaks after product-led growth | Attribution | MOFU | CFOs distrust blended CAC | 7 sales calls in Q2 | Whitepaper | 92 |
| 2 | The 20-minute retention audit | Retention | TOFU | CX teams lack a quick diagnostic | r/customersuccess thread, 214 comments | Blog + checklist | 85 |
| 3 | Onboarding email teardown series | Lifecycle | TOFU | Marketers can't critique their own flows | Poll: 61% requested teardowns | Blog series | 74 |
```

Scoring rule (0–100): audience pain strength (40) + differentiation vs. existing
coverage (25) + proximity to revenue (25) + inverse production effort (10). P1 ≥ 80,
P2 = 60–79, P3 < 60.

## Workflow

1. Harvest raw ideas from five sources in one sitting: sales calls, support tickets,
   community threads, customer interviews, and competitor comment sections.
2. Pull the top and bottom 10 performing past assets from GA4; note which pains, angles,
   and formats correlate with engagement and conversions.
3. Cluster raw ideas into pillar themes; discard duplicates and merge near-identical
   angles before scoring anything.
4. Rewrite each survivor as a working title that states the reader's payoff, not the
   topic label ("Why X happens" beats "Thoughts on X").
5. Score every idea with the 40/25/25/10 rule; record the evidence source inline so
   reviewers can audit the reasoning.
6. Map each idea to funnel stage and best-fit format; flag ideas that naturally become
   gated assets or repurposing hubs.
7. Pressure-test the P1 list with sales and CS in a 30-minute review; kill anything they
   have never heard a customer say.
8. Check differentiation: for each P1, confirm your angle is sharper than the top 3
   existing treatments (yours or competitors').
9. Ship the bank to content-calendar; archive rejected ideas with reasons for future
   cycles. Refresh the full bank quarterly.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Audience & community listening | SparkToro, Reddit, Quora | SparkToro free tier; Reddit search operators |
| Question mining | AnswerThePublic, AlsoAsked | Free tiers; use for question phrasing, not volume |
| Content format signals | BuzzSumo | Paid; limited free searches |
| Sales conversation mining | Gong, Chorus | Paid; export objection highlights monthly |
| Performance data | GA4, Search Console | Free; engagement + query context |
| Topic bank database | Notion, Airtable | Airtable scoring formulas; Notion for docs |

## Example AI Prompt

```text
Act as an editorial ideation lead for {BUSINESS}, which sells {PRODUCT/SERVICE} to
{PERSONA}. Current pillars: {PILLAR LIST}.

Evidence to work from:
- Sales objections overheard: {OBJECTION LIST OR CALL NOTES}
- Support ticket themes: {TICKET THEMES}
- Community threads of note: {REDDIT/LINKEDIN QUOTES OR LINKS}
- Top past posts (by engagement): {TOP POSTS + METRICS}
- Flopped past posts: {BOTTOM POSTS}

Deliver:
1. 25–40 topics grouped by pillar, each as a payoff-stated working title.
2. Table: topic | pillar | funnel stage | pain | evidence | suggested format | score
   (0–100 using pain 40 / differentiation 25 / revenue proximity 25 / effort 10).
3. A P1 shortlist (score ≥80) ready for next quarter's calendar.
4. Rejected ideas with one-line reasons.
Bias toward ideas a salesperson would forward to a prospect.
```

## Edge Cases & Guardrails

- No evidence, no entry: internal brainstorm echo chambers produce topics nobody
  searched, asked, or struggled with — every idea cites a source.
- Ideas are not formats: "a podcast episode" is not an idea; the angle and payoff must
  survive a format change.
- Never clone a competitor topic without a measurably sharper angle (new data, contrarian
  stance, narrower audience).
- A large bank is not a win — a bank nobody executes is a graveyard; size it to one
  quarter of cadence and keep it fresh.
- Seasonal ideas need lead time: flag holiday/tax/event topics at least 6–8 weeks ahead.
- AI-generated idea lists must pass the sales reality check — filter every batch through
  the step-7 pressure test before scheduling.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Published assets originating from the bank | ≥70% per quarter | Most posts are ad-hoc requests |
| P1-to-published conversion within a quarter | ≥60% | P1s die in backlog review |
| Top-decile posts sourced from the bank | ≥50% | Winners come only from luck/virality |
| Bank depth | ≥1 full quarter of cadence, refreshed quarterly | Bank older than 2 quarters |
| Sales co-sign rate on P1 list | ≥80% of P1s survive review | Sales never sees the list |

## Handoffs

- → **content-calendar:** deliver the P1 shortlist with format and stage tags.
- → **content-creation:** provide evidence links and angle notes for each scheduled topic.
- ← **content-strategy:** receive pillars and personas; flag when evidence suggests a
  pillar needs redefinition.
- ↔ **seo-content-ideation (SEO sibling):** hand the P1 list over to attach search-demand
  and query data — you own editorial value, they own search mechanics.
- ↑ **content-marketing-agent:** escalate when evidence points to a missing pillar or a
  market shift the strategy does not cover.
