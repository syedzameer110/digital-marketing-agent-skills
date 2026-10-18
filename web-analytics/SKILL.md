---
name: web-analytics-agent
description: Orchestrates the complete web analytics stack — GA4 setup and event tracking, conversion and key-event definitions, dashboards, attribution modeling, heatmaps, session recordings, and data analysis. Use this skill whenever the user wants to install or fix tracking, define KPIs, build a dashboard, find insights in traffic or funnel data, audit a measurement setup, reconcile channel attribution, or mentions GA4, Google Tag Manager, Looker Studio, BigQuery, heatmaps, consent mode, or "the numbers look wrong" — even if they never say analytics.
---

# Web Analytics — Main Agent (Command Hub)

## Channel Overview

Web analytics is the measurement backbone every other marketing channel depends on: SEO, paid media, email, automation, and CRO all report their results through this instrumentation, so a broken tag or a mislabeled conversion silently poisons decisions everywhere. The discipline is garbage-in-garbage-out — no dashboard or analysis can recover meaning from events that never fired, or from "conversions" defined three different ways in three tools. That is why this channel leads with implementation quality and definitions before anything visual or statistical gets built, and why it holds veto power over channel launches: nothing goes live unmeasured.

Modern measurement is event-based: GA4 records everything as an event with parameters (snake_case names, max 40 characters, up to 25 custom parameters per event, 50 custom dimensions and 50 custom metrics per standard property), sessions default to a 30-minute timeout, and conversions are key events marked from the event registry. Implementation splits into client-side tagging (Google Tag Manager firing in the browser — simple and free, but exposed to ad blockers and browser privacy limits that typically drop 5–15% of hits) and server-side tagging (a GTM server container on Cloud Run receiving and forwarding hits from a first-party endpoint — more control, longer cookie life, data filtering and redaction, at roughly $40–80/month plus maintenance). Privacy is a hard constraint, not a preference: GDPR/CCPA consent requirements and Google's Consent Mode v2 (ad_storage, analytics_storage, ad_user_data, ad_personalization) must gate what fires and when, which makes a consent management platform (Cookiebot, OneTrust) table stakes for EU traffic. Privacy-first alternatives (Fathom, Plausible) trade attribution depth for cookieless simplicity. Costs are mostly tools and labor — $0–$500/month covers the free stack for most SMBs — and expect 2–4 weeks from property setup to trustworthy first reports, then continuous hygiene forever after.

## Agent Hierarchy

```text
web-analytics-agent (command hub)
│
├── sub-agents/tracking-setup/
│   └── owns: GA4 property architecture, GTM client + server containers,
│       event taxonomy, consent wiring, tag QA and health checks
├── sub-agents/goal-conversion-setup/
│   └── owns: key-event registry, counting modes, funnel definitions,
│       KPI dictionary, revenue-value assignments, CRM/finance reconciliation
├── sub-agents/dashboard-creation/
│   └── owns: Looker Studio / BigQuery reporting surfaces, metric governance
│       on dashboards, scheduled delivery, stakeholder adoption
├── sub-agents/data-analysis/
│   └── owns: insight reports, funnel and segment deep-dives, anomaly triage,
│       the data-quality gate that precedes any analysis
├── sub-agents/attribution-modeling/
│   └── owns: model comparison, cross-platform deduplication, unassigned-traffic
│       hygiene, incrementality tests, the channel truth table
└── sub-agents/heatmaps-session-recording/
    └── owns: Hotjar/Clarity/Mouseflow research design, recording review,
        friction backlog, test-ready behavioral hypotheses
```

## Sub-Agent Routing Table

| Sub-agent | Call when… | Key inputs | Depends on |
|---|---|---|---|
| tracking-setup | New property, Universal Analytics migration, missing events, tag debugging, consent/CMP setup, pre-launch measurement checks | Site access, GA4/GTM admin rights, business goals, funnel map | None (entry point) |
| goal-conversion-setup | Defining what counts as success; conversion counts disagree across tools; KPI reset after a redesign | Business goals, CRM/finance definitions, implemented event registry | tracking-setup |
| dashboard-creation | Stakeholders need live numbers; reporting is manual screenshots; two teams quote different figures | Metric dictionary, data-source access, audience list, cadence | goal-conversion-setup |
| data-analysis | "Why did traffic/conversions drop?", trends, funnel leaks, business cases, anomaly triage | GA4/BigQuery access, the decision being served, change log | tracking-setup, goal-conversion-setup |
| attribution-modeling | Budget disputes, platform numbers disagree with GA4, unassigned traffic, channel credit questions | GA4 attribution settings, platform exports, CRM revenue | goal-conversion-setup, data-analysis |
| heatmaps-session-recording | Pages underperform with no obvious cause; UX friction questions; pre-CRO hypothesis hunting | Page list, behavior tool installed, traffic volume, funnel context | tracking-setup (parallel-safe after base tag) |

## End-to-End Workflows

### Workflow A — New Property Setup to First Insight Report (weeks 1–4)

1. Run **tracking-setup**: inventory existing tags (legacy UA, gtag, CMS plugins), design the
   tracking plan (event taxonomy, parameter dictionary, data streams), deploy GA4 + GTM, wire
   Consent Mode v2 and the CMP, add internal-traffic filters and the unwanted-referral list.
   Output: live property + versioned tracking plan.
2. Run **goal-conversion-setup**: translate business goals into a key-event registry (5–15 key
   events with counting modes and values) plus funnel stage definitions, aligned with CRM and
   finance semantics. Output: the KPI dictionary.
3. QA loop with **tracking-setup**: verify every key event in DebugView with expected parameters,
   test granted/denied consent states, confirm internal-traffic exclusion, and validate 48 hours
   of stable volumes including one test transaction. Output: signed QA checklist.
4. Run **dashboard-creation**: interview stakeholders for the decisions they make weekly, then
   build executive and channel-team Looker Studio boards from the validated definitions — one
   source of truth per metric, scheduled delivery, access controls. Output: live dashboards.
5. Run **data-analysis** on the first two weeks of clean data: baseline read, segment quality
   check, funnel structure verification, and a 3–5 recommendation insight report with owners.
   Output: first insight report.
6. Hand the baseline channel scorecard to **attribution-modeling** for the first model comparison
   (data-driven vs last-click vs platform-reported). Output: initial channel truth table.
7. Distribute verified definitions and baselines to the channel agents (SEO, paid, email) so every
   team reports from the same registry. Output: signed-off measurement contract.
8. Set the operating rhythm: monthly **tracking-setup** health check, monthly insight report from
   **data-analysis**, quarterly audit and attribution re-baseline.

### Workflow B — Measurement Health Audit (quarterly)

1. Run **tracking-setup** in audit mode: tag error rates, (not set) share, consent rate, PII leaks,
   cross-domain integrity, and event-volume anomalies vs the trailing 90 days.
   Output: health scorecard with severities.
2. Run **goal-conversion-setup**: re-validate that active key events still match current business
   goals; prune vanity events and document drifted definitions. Output: updated registry — no
   mid-quarter edits to active definitions without annotation.
3. Run **data-analysis** to quantify the damage from any gaps found: how long each was broken,
   affected volume, and which past conclusions need correcting. Output: impact estimate.
4. Ship fixes through **tracking-setup** with a developer ticket per issue; re-verify with a
   two-week before/after read. Output: remediation log.
5. Update **dashboard-creation** artifacts for any changed metrics or renamed definitions.
   Output: refreshed dashboards with updated footnotes.
6. Re-run **heatmaps-session-recording** coverage on any template whose tracking was silently
   broken during the period. Output: behavioral backfill where relevant.
7. Close with an **attribution-modeling** re-baseline if coverage shifted materially; publish the
   audit summary to leadership. Output: quarterly measurement report.

### Workflow C — Channel Truth Reconciliation (monthly for paid-heavy programs)

1. Export platform-reported conversions (Google Ads, Meta Ads, LinkedIn Ads) alongside GA4 key
   events and CRM revenue for the same period, one row per channel per week.
2. Run **data-analysis**: segment by source/medium, campaign, and landing page; flag any channel
   where the platform-vs-GA4 gap exceeds 20%. Output: gap list with candidate causes.
3. Run **attribution-modeling**: compare data-driven vs last-click vs platform-reported, check
   unassigned traffic, deduplicate cross-platform claims, and produce the channel truth table.
   Output: reconciled conversion counts.
4. Route the verified numbers to **sem-ppc-agent** for bidding imports and to other channel agents
   for budget decisions — platform numbers are labeled optimization-only. Output: reconciliation memo.
5. Update **dashboard-creation** so every stakeholder reads reconciled numbers only; raw platform
   widgets get explicit "in-platform metric" labels. Output: corrected dashboards.
6. Escalate systematic mismatches (broken tags, double counting, consent-mode gaps) back to
   **tracking-setup** for same-week remediation. Output: fix tickets.

## KPI Dashboard

North-star metric: **Trustworthy measurement** — tracking coverage of planned key events, because every downstream decision in every channel inherits this data quality.

| Metric | Source tool | Cadence | Healthy range |
|---|---|---|---|
| Key-event tracking coverage | GA4 DebugView + GTM audit | Weekly | >95% of planned events firing |
| Tag error rate | GTM / server-side logs | Weekly | <2% of tags |
| Data freshness | GA4 report latency | Daily | Standard reports <24h |
| Consent accept rate | CMP (Cookiebot/OneTrust) | Monthly | 60–85% (geo- and design-dependent) |
| (not set) / (other) event share | GA4 | Monthly | <5% of events |
| Active key events | GA4 admin | Monthly | 5–15, matching the registry |
| Unassigned traffic (conversions) | GA4 | Monthly | <10% |
| Cross-platform reconciliation gap | Attribution truth table | Monthly | <15% unexplained after dedup |
| BigQuery export integrity | BigQuery daily tables | Weekly | 100% of days exported, no gaps |
| Sampled reports in circulation | Analysis reviews | Monthly | 0 unsampled-flagged decisions |
| Session-recording sampling coverage | Clarity/Hotjar config | Quarterly | Key templates at 2,000+ sessions |
| Privacy incidents (PII, pre-consent firing) | Audits | Quarterly | 0 |
| Dashboard adoption | Looker Studio viewers | Monthly | >60% of named stakeholders |
| Dashboard refresh SLA | Looker Studio schedules | Weekly | >95% of runs on time |
| Insight adoption | Analysis reports | Quarterly | >50% of recommendations actioned |
| Behavior research throughput | Friction backlog | Monthly | 3–5 ranked findings per sprint |

## Budget Guidance

| Monthly budget | Recommended allocation |
|---|---|
| <$500 | All-free stack: GA4, GTM, Microsoft Clarity, Looker Studio, BigQuery sandbox. Spend time, not money — on QA, definitions, and governance |
| $500–$2,000 | Add CMP license ($10–30/mo per domain), one paid behavior tool (Hotjar/Mouseflow), server-side GTM hosting (~$40–80/mo), ad-hoc dev hours for dataLayer work |
| $2,000–$5,000 | Fractional analyst retainer, active BigQuery usage, behavior research at full sampling, CMP enterprise tier, quarterly external audit |
| $5,000+ | Dedicated analytics engineer + consultant, near-real-time pipelines, org-wide BI; evaluate GA4 360 only at very high event volumes (tens of millions/month) |

Allocation principles:

- Implementation quality beats tooling: a $0 free stack with clean tagging outperforms $2,000 of tools on broken data — fund dev and QA time first.
- Never pay for what the free stack covers; graduate to paid tools only at a concrete, named limitation (sampling, seats, retention, support).
- Server-side tagging needs its own business case (ad-blocker loss, data control, cookie lifetime) — it is not a default upgrade.
- Privacy spending is non-negotiable: CMP + Consent Mode precede any EU traffic scaling; fines dwarf tool savings.
- Keep 10–15% unallocated for one-off projects: migrations, audits, property restructures, incident response.
- Re-audit tool ROI twice a year — analytics tooling is notorious for seats and features nobody uses.
- Buy data, not dashboards: a one-off BigQuery pipeline beats a perpetual SaaS subscription whenever the need is periodic.

## Team & Agency Mapping

| Activity | Best handled by | Rationale |
|---|---|---|
| Measurement plan & governance | In-house analyst or marketing lead | Requires business context and priority calls |
| Tag implementation (GTM, dataLayer) | Developer + analytics QA, or specialist freelancer | Code access and release-process coupling |
| Server-side infrastructure | Consultant / devOps support | Cloud Run, containers, cost monitoring |
| Dashboards & reporting | In-house analyst (freelancer for first build) | Iterates with real stakeholder access |
| Deep analysis & attribution | Fractional analyst or agency with BigQuery skills | Statistical rigor and cross-channel view |
| Heatmaps & session research | In-house CRO/UX owner | Context and institutional memory matter most |
| Consent/privacy compliance | Legal + CMP vendor, implemented by dev | Liability sits with the business, not the vendor |
| Training & documentation | In-house analytics lead | Adoption lives or dies with internal ownership |

## Reporting Cadence

- **Weekly (in-house, 30 min):** data health check — coverage, tag errors, consent rate, volume
  anomalies; dashboards auto-delivered. Decision: fix tracking fast; nothing else waits on broken data.
- **Monthly (stakeholders, 1 hr):** reconciled channel scorecard, funnel trends, insight report with
  3–5 recommendations. Decision: budget shifts, test backlog prioritization, learnings distribution.
- **Monthly (analytics + channel leads):** channel truth reconciliation for paid-heavy programs;
  sign-off on the numbers before they reach leadership decks.
- **Quarterly (leadership):** measurement audit results, attribution model review, KPI redefinitions,
  privacy/compliance status, tooling ROI. Decision: strategy, budget, annual plan inputs.
- **Annually (leadership + legal):** consent policy review, data-retention review, vendor and DPA
  review, measurement-stack consolidation. Decision: contracts, renewals, architecture changes.

## Cross-Channel Integrations

This channel feeds all others — every downstream agent inherits these definitions and this data quality:

- **→ seo-agent:** GA4 landing-page and conversion data underpin SEO reporting; verify organic
  key-event coverage before any organic performance claim is made.
- **→ sem-ppc-agent:** reconciled conversion definitions and counts for bidding imports; the UTM
  governance standard enforced here prevents "unassigned" chaos in paid reporting.
- **→ email-marketing-agent:** GA4 UTM-based attribution validates email-reported revenue; GA4
  audience segments feed email targeting and suppression logic.
- **→ marketing-automation-agent:** key events and funnel stages define lifecycle triggers —
  automation entry/exit criteria are only as good as this channel's event registry.
- **→ cro-agent:** heatmap and session-recording findings plus funnel leakage points become the CRO
  test backlog; this channel validates experiment results post-launch.
- **→ display/video/affiliate partners:** view-through and assist claims from media partners are
  accepted only after this channel's dedup rules are applied to the shared conversion pool.
- **→ remarketing/audience consumers:** GA4 audiences (purchasers, cart abandoners, high-intent
  viewers) export to ad platforms only after consent-safe collection is verified.
- **← all channels:** campaign launches, page releases, and platform migrations must loop through
  tracking-setup before going live — measure first, spend second.
- **← finance/CRM:** revenue definitions flow in from finance and CRM; this channel reconciles
  marketing-reported conversions against that truth monthly and annually.
