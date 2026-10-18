# Digital Marketing Agent Skills Library

A hierarchical agent-skills system covering all 14 digital marketing channels in the
standard **Agent Skills format** (`SKILL.md` + YAML frontmatter). Every channel ships as a
two-tier org chart: one **Main Agent** (channel command hub) that routes and sequences
work, and a folder of **Sub-Agents** (full playbooks) that each own one specialist activity.

```
Total: 134 SKILL.md files = 14 Main Agents + 120 Sub-Agents
```

## Library Map

| # | Channel folder | Main agent | Sub-agents | Covers |
|---|---|---|---|---|
| 1 | `seo/` | `seo-agent` | 12 | Keyword research, content, on-page, technical, backlinks, local, audits, reporting |
| 2 | `sem-ppc/` | `sem-ppc-agent` | 12 | Google/Microsoft Ads, bidding, shopping, Quality Score, budgets, tracking |
| 3 | `social-media-marketing/` | `social-media-marketing-agent` | 9 | Strategy, calendars, organic content, community, listening, paid social, UGC |
| 4 | `content-marketing/` | `content-marketing-agent` | 10 | Strategy, ideation, creation, copywriting, distribution, repurposing, lead magnets |
| 5 | `email-marketing/` | `email-marketing-agent` | 11 | List building, segmentation, automation, design, deliverability, analytics |
| 6 | `affiliate-marketing/` | `affiliate-marketing-agent` | 9 | Program setup, recruitment, commissions, tracking, fraud, payouts |
| 7 | `influencer-marketing/` | `influencer-marketing-agent` | 8 | Research, vetting, briefing, negotiation, collaboration, measurement, ambassadors |
| 8 | `video-marketing/` | `video-marketing-agent` | 8 | Strategy, scripts, production, YouTube SEO, thumbnails, video ads, live, analytics |
| 9 | `mobile-marketing/` | `mobile-marketing-agent` | 7 | SMS, ASO, push, in-app ads, geofencing, QR campaigns, mobile analytics |
| 10 | `display-advertising/` | `display-advertising-agent` | 7 | Creative, targeting, programmatic, placements, frequency, viewability, reporting |
| 11 | `remarketing-retargeting/` | `remarketing-retargeting-agent` | 7 | Audience lists, pixels, ad creation, dynamic retargeting, burn pixels, cross-device |
| 12 | `marketing-automation/` | `marketing-automation-agent` | 7 | Workflows, triggers, lead scoring, nurturing, CRM sync, behavioral targeting |
| 13 | `web-analytics/` | `web-analytics-agent` | 6 | GA4 setup, conversion goals, dashboards, analysis, attribution, heatmaps |
| 14 | `cro/` | `cro-agent` | 7 | Funnel analysis, A/B testing, landing pages, forms, user testing, exit intent, CTAs |

## How Each Skill File Is Built

Every `SKILL.md` uses YAML frontmatter (`name` + pushy trigger `description`) so agent
platforms can route to it automatically. Sub-agent playbooks follow one fixed template:

`Role & Mission → When to Use → Inputs → Output Contract → Workflow → Tools & Stack →
Example AI Prompt → Edge Cases & Guardrails → KPIs & Benchmarks → Handoffs`

Main-agent command hubs add: channel overview, agent hierarchy, sub-agent routing table,
end-to-end workflows, KPI dashboard, budget guidance, team/agency mapping, reporting
cadence, and cross-channel integrations.

## Directory Anatomy

```text
digital-marketing-skills/
└── seo/                                (one folder per channel)
    ├── SKILL.md                        ← Main Agent (command hub)
    └── sub-agents/
        ├── keyword-research/SKILL.md   ← Sub-Agent playbook
        ├── technical-seo/SKILL.md
        └── ...                         (12 total for SEO)
```

## How to Use

**Standalone (AI chat assistants).** Paste the relevant `SKILL.md` into the conversation
as system context, or just paste the frontmatter `description` + your task. The
`Example AI Prompt` section of each sub-agent is a ready-to-run template with
`{curly_placeholders}` — fill them and go.

**Agent platforms (Claude Code, GLM, ClawHub, Cursor, etc.).** Copy the channel folders
you need into your skills directory; the YAML frontmatter makes each skill discoverable
and triggerable. Names are globally unique (channel-prefixed, e.g. `email-copywriting`
vs `content-copywriting`), so installing multiple channels side by side is safe.

**Orchestration pattern.** Route the request to the channel's Main Agent first; it decides
which Sub-Agents to invoke and in what order (see each hub's `Sub-Agent Routing Table` and
`End-to-End Workflows`). Sub-agent `Handoffs` sections define how artifacts move between
agents and across channels.

## Customization Tips

- **Benchmarks:** KPI ranges are industry-typical starting points; recalibrate to your own
  baseline data after the first reporting cycle.
- **Tool stack:** recommended tools name popular free and paid options; swap in your
  actual stack without changing the workflows.
- **Placeholders:** all `{curly_placeholder}` fields in Example AI Prompts are meant to be
  filled per engagement — they encode the minimum context each agent needs.
- **Extending:** to add an activity, duplicate a sibling sub-agent folder, rewrite the
  frontmatter (`name: <channel>-<new-activity>`), and add a routing-table row in the
  channel's main `SKILL.md`.

## Channels Included

SEO, SEM/PPC (Paid Search), Social Media Marketing, Content Marketing, Email Marketing,
Affiliate Marketing, Influencer Marketing, Video Marketing, Mobile Marketing, Display
Advertising, Remarketing/Retargeting, Marketing Automation, Web Analytics, and CRO
(Conversion Rate Optimization).
