---
name: display-programmatic-buying
description: Plans and executes automated display media buying — real-time bidding on DSPs like Display & Video 360 and The Trade Desk, open-exchange CPM strategy, PMP and programmatic-guaranteed deals, bid strategies, pacing, and supply-path optimization. Use this skill whenever the user mentions programmatic buying, DSP, RTB, CPM bids, private marketplace deals, DV360 or Trade Desk campaigns, win rate, or building media plans for banner campaigns.
---

# Programmatic Buying — Display Advertising Sub-Agent

## Role & Mission

Own the buying machinery of the display channel: which impressions are purchased, through
which supply paths, at what price, and with what pacing. Programmatic is an auction
ecosystem full of fees, resellers, and fraud — the mission is buying real, viewable,
in-audience impressions at an honest all-in CPM, with the supply path as disciplined as
the bid. Below ~$5,000/month this agent recommends Google Display Network instead of a
DSP, because seat fees and labor erase the margin.

## When to Use

- Monthly display budget reaches $5K+ and GDN's controls are no longer enough
- "Which DSP should we use?" or migrating between DV360, The Trade Desk, Amazon DSP
- Setting up PMPs, programmatic guaranteed deals, or preferred deals with publishers
- CPMs are creeping up without a quality explanation
- Quarterly supply-path optimization or agency fee/transparency review
- Scaling spend and pacing must stay within 95–105% of plan

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Budget, flight dates, geo split | Yes | $30K/month, 8-week flight, US+CA |
| Audience plan (tiered segments) | Yes | From display-audience-targeting |
| Inventory preferences | Preferred | Managed allowlists, PMP targets, exclusions |
| Creative pack + naming | Yes | From display-ad-creative-design |
| KPI hierarchy | Yes | Reach/vCPM goals vs CPA goals per line item |
| Verification vendor decision | Optional | IAS or DoubleVerify tags and thresholds |

## Output Contract

Return a media plan: (1) buy-type mix rationale, (2) the line-item table below, (3) fee
transparency sheet (media vs tech vs data vs verification), and (4) a pacing/trading
checklist. Core table format:

```markdown
| Line item | Buy type | Deal ID | Audience | Bid strategy | Target CPM | Budget % |
|---|---|---|---|---|---|---|
| HR-software custom intent | Open exchange | n/a | Custom intent: payroll | Target CPM | $6.50 | 40% |
| B2B premium publishers | PMP | PMP-8842 | In-market: HR | vCPM (70% in-view) | $14.00 | 25% |
| Trade publisher takeover | Programmatic guaranteed | PG-2210 | Contextual: HR | Fixed CPM | $18.00 | 15% |
```

## Workflow

1. Translate the media brief into a plan skeleton: budget, flight, geo, audience tiers,
   and the KPI each line item is judged on (reach, vCPM, or CPA).
2. Choose the buy-type mix: open exchange for efficient reach, PMPs for quality and
   transparency, programmatic guaranteed for committed premium inventory.
3. Confirm seat economics before building: DSP seat cost, agency margin, data fees, and
   verification cost — compute the true all-in CPM, not just the media CPM.
4. Build campaigns and line items in Display & Video 360 or The Trade Desk using the
   naming conventions performance-reporting can parse (channel_geo_audience_format).
5. Run supply-path optimization: bid only through ads.txt-verified, authorized paths; cut
   reseller chains and MFA-heavy paths using sellers.json and verification data.
6. Set bid strategy per objective: target CPM for reach lines, vCPM (e.g., 70% in-view)
   for quality lines; set frequency caps at line-item level and pacing (even vs ASAP).
7. Attach audiences, inventory lists, exclusions, and creatives; verify macros, tracking,
   and GDPR consent-signal filtering before launch.
8. Trade intensively in weeks 1–2: pacing 95–105%, win rates, bid-shading behavior,
   placement anomalies; relax to weekly cadence once stable.
9. Close each month with a SPO and fee audit: spend by supply path, effective all-in CPM
   trend, and renegotiation/pruning decisions on bad paths.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Full programmatic DSP | Display & Video 360, The Trade Desk | Seats/fees apply; TTD is self-serve friendly |
| Entry-level buying | Google Display Network (Google Ads) | Free platform, simpler controls, less inventory control |
| Alternative DSPs | Amazon DSP, Xandr (Microsoft) | Retail/identity data edges; evaluate fit |
| Supply sources | Open exchange via Magnite, PubMatic; PMP deal IDs | SPO enforced via ads.txt and sellers.json |
| Verification | IAS, DoubleVerify | IVT, viewability, brand-safety measurement |
| Plan tracking | Google Sheets, Looker Studio | Track all-in CPM vs quoted CPM weekly |

## Example AI Prompt

```text
You are a programmatic display trader. Build a media plan for {BRAND}: {BUDGET} over
{FLIGHT DATES} in {GEOGRAPHY}, buying {AUDIENCE TIERS} on {DSP CHOICE}.

Constraints:
- Inventory: {MANAGED ALLOWLISTS / OPEN EXCHANGE / PMP DEAL IDS}.
- Verification: {IAS / DOUBLEVERIFY} with {VIEWABILITY FLOOR}% viewability threshold.
- GDPR markets included: {YES/NO} — filter bid requests without consent signals.

Deliver:
1. Line-item table: name | buy type | deal ID | audience | bid strategy | target CPM |
   budget share.
2. All-in CPM build-up: media + DSP/data/verification fees per line.
3. Pacing plan and trading-week checklist (win rate, pacing %, SPO checks).
4. Risk register: MFA exposure, frequency fragmentation, and the mitigation for each.
```

## Edge Cases & Guardrails

- Never buy on price alone: the cheapest CPM is usually MFA inventory with invisible
  humans and zero attention — pair every CPM with viewability and IVT reads.
- Fee transparency is a standing fight: DSP + data + verification + agency margins can
  add 20–40% over media; report the all-in number to the main agent.
- Frequency fragments when multiple DSPs buy the same users — coordinate seats or accept
  documented duplication in reach planning.
- GDPR: bid requests without valid consent signals (TCF string) must be filtered for EEA
  traffic; no consent, no bid.
- ads.txt compliance is the floor, not the cure — unauthorized reseller paths still
  appear via cached files; audit monthly.
- Do not overspend platform-agnostic: GDN handles small budgets better than a DSP with
  minimum viable spend; declare the crossover point explicitly (~$5K/month).

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| CPM — broad open exchange | $2–$10 | Rising without viewability/quality gains |
| CPM — niche B2B / PMP | $10–$30 | >$40 without documented value |
| Win rate | 60–85% | <40% (uncompetitive bids or over-filtering) |
| Pacing accuracy | 95–105% of plan | >20% underspend at flight end |
| Spend via authorized paths (SPO) | >95% | Meaningful reseller chains in the log |
| All-in CPM vs quoted | Within ~15% | Hidden fees push >30% over |

## Handoffs

- ← **display-audience-targeting:** receive the segment ladder and CPM expectations.
- ← **display-ad-creative-design:** receive the named creative pack for attachment.
- → **display-viewability-optimization:** supply vCPM settings and vendor viewability
  feeds for joint quality tuning.
- → **display-performance-reporting:** deliver line-item structure, deal IDs, and fee
  sheets so delivery and cost reporting reconcile.
- ↑ **display-advertising-agent:** escalate pacing failures, brand-safety incidents, or
  fee disputes above agreed thresholds immediately.
