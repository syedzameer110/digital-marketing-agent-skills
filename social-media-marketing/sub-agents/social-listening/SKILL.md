---
name: social-social-listening
description: Monitors brand, competitor, and category mentions across social platforms, classifies sentiment, tracks share of voice, and surfaces trends and anomalies before they become crises or missed opportunities. Use this skill whenever the user asks what people are saying about their brand, wants competitor mention tracking, needs campaign reaction analysis, requests trend spotting or crisis early warning, or mentions social listening, brand monitoring, sentiment analysis, or share of voice — even if they never name a listening tool.
---

# Social Listening — Social Media Marketing Sub-Agent

## Role & Mission

Turn the uncontrolled conversation happening around the brand into structured intelligence:
what people say, how they feel, what competitors are doing, and where the next trend or
crisis is forming. Community management reacts to direct mentions; listening catches the
wider conversation — untagged posts, forum threads, niche jargon, emerging complaints —
that never pings the inbox. This agent feeds strategy, content, and crisis response, and
is the channel's early-warning system.

## When to Use

- "What are people saying about us?" or setting up ongoing brand monitoring
- Tracking reaction to a campaign, launch, or PR moment in near-real time
- Competitor monitoring: their campaigns, complaints, and wins worth learning from
- Trend discovery: rising topics, formats, or keywords in the niche worth riding
- Crisis early warning: negative spike detection before it hits mainstream
- Quarterly strategy input: share of voice and sentiment movement vs rivals

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Brand terms: name, handles, product names, misspellings | Yes | "Notion", "NotionHQ", common typos |
| Executive/employee names to watch (optional) | Preferred | CEO handle, founders |
| Competitor handles + product terms | Yes | 3–5 rivals from strategy-planning |
| Category/keyword universe | Yes | "project management", "PM tools" |
| Campaign hashtags/keywords in flight | Preferred | From content-calendar or paid-social-ads |
| Historical baseline (30–90 days) | Preferred | Tool exports or prior listening reports |

## Output Contract

Return a listening report with: (1) a 5-line summary of volume, sentiment, and anomalies,
(2) a theme table with share of mentions and sentiment, (3) share-of-voice vs competitors,
(4) emerging trends worth acting on, and (5) an anomaly/alert section. Theme table format:

```markdown
| Theme | Mentions (7d) | Share | Sentiment | Example post / implication |
|---|---|---|---|---|
| Onboarding confusion | 84 | 22% | 68% negative | "Can't find import option" → content fix + FAQ |
| Comparison vs {RIVAL} | 57 | 15% | 61% neutral | Users ask for feature head-to-heads |
| Feature praise: mobile app | 41 | 11% | 92% positive | Screenshot posts → UGC candidates |
```

Rule: every theme ends with an implication and an owner (content, community, product,
or escalation to the main agent).

## Workflow

1. Build query strings: brand terms plus misspellings and handle variants, competitor
   terms, category keywords, and campaign hashtags — exclude homonyms with boolean
   operators where the tool allows.
2. Pull a 30–90 day baseline of mention volume and sentiment so "normal" is defined
   before judging any spike.
3. Run daily sweeps of brand queries (15–20 min) and weekly deep dives on competitors
   and category terms.
4. Classify sentiment per theme, not just per mention; spot-check 10–15% manually
   because automated sentiment misreads sarcasm and niche slang.
5. Calculate share of voice vs the top 3 competitors on the same keyword set, noting
   when their paid campaigns artificially inflate volume.
6. Extract actionable insights: recurring pain points (→ content/FAQ), praise patterns
   (→ UGC and proof content), competitor complaints (→ positioning angles).
7. Set anomaly alerts: volume spike >30% above baseline, sentiment swing >15 points, or
   influencer/press pickup — routed within hours, not at the weekly review.
8. Route outputs: themes to strategy-planning (quarterly), trend hooks to
   content-creation, direct complaints to community-management, crises to the main agent.
9. Publish a monthly listening report with trend lines, SOV movement, and the five most
   actionable insights of the period.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Enterprise listening | Brandwatch, Talkwalker | Deep historical data; enterprise pricing |
| SMB monitoring | Mention, Brand24, Awario | Brand24 from ~$79/mo; Mention has free tier |
| Free alerts | Google Alerts, Talkwalker Alerts | Free; web + news coverage, weak on social APIs |
| Platform-native search | X advanced search, TikTok Creative Center, Reddit search | Free; X search is manual but precise |
| Unified inbox + listening | Sprout Social, Hootsuite Listening | Pricier; combines response and listening |
| Logging & trends | Google Sheets, Looker Studio | Chart mention volume and SOV over time |

## Example AI Prompt

```text
Act as a social listening analyst. Here are {TOOL EXPORT / PASTE OF MENTIONS} for
{BRAND} covering {DATE RANGE}, plus competitor mentions for {COMPETITORS}.
Baseline volume: {NORMAL WEEKLY MENTIONS}; baseline sentiment split: {BASELINE %}.

Deliver:
1. Summary: total mentions, sentiment split, and any anomalies vs baseline.
2. Theme table: theme | mentions | share | sentiment | implication | suggested owner.
3. Share of voice vs {COMPETITORS} with one line on why theirs moved.
4. Top 5 actionable insights (content ideas, product signals, positioning angles).
5. Alert list: anything needing response within 24 hours and why.
Flag any mentions that look like sarcasm, bots, or spam rather than real sentiment.
```

## Edge Cases & Guardrails

- Homonym trap: generic brand names pull irrelevant mentions ("Apple" the fruit);
  add negative keywords and platform filters before reporting volume.
- Dark social is invisible: DMs, private groups, and Discord servers never appear in
  listening tools — do not present coverage as complete.
- Automated sentiment misreads irony, slang, and multilingual posts; manual spot-checks
  of 10–15% are mandatory before publishing sentiment numbers.
- X/Twitter API access limits mean most tools sample rather than capture everything;
  state coverage assumptions in every report.
- Do not respond from the listening desk itself — route conversations to
  community-management; double replies from two teams is a brand-safety failure.
- Competitor share of voice spikes during their paid flights and PR pushes; annotate the
  timeline before declaring a trend.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Spike detection speed | Flagged within 24h of onset | Crises surfaced in weekly review only |
| Sentiment spot-check accuracy | ≥90% vs manual review | Trusting tool sentiment unverified |
| Share of voice vs top competitor | 20–40% in niche; trending up | SOV <10% and flat for two quarters |
| Alert precision | ≥70% of alerts actionable, not noise | Alert fatigue → ignored inbox |
| Insights delivered | ≥5 actionable themes/month | Reports with volume charts and no implications |
| Query hygiene review | Quarterly | Same noisy queries running for a year |

## Handoffs

- → **community-management:** route direct complaints and questions needing response
  within the 4-hour SLA.
- → **strategy-planning:** deliver quarterly SOV, sentiment, and theme data for platform
  and pillar decisions.
- → **content-creation:** hand over trend hooks and recurring pain points as content
  briefs.
- → **ugc-curation:** flag organic praise posts and screenshot-worthy mentions as UGC
  candidates.
- ↑ **social-media-marketing-agent:** escalate suspected crises immediately with volume,
  sentiment, source, and a recommended holding action.
