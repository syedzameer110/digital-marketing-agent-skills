---
name: sem-ppc-campaign-structure
description: Designs the account architecture for Google Ads and Microsoft Advertising — campaign types, brand vs non-brand separation, ad group theming, geo and audience segmentation, naming conventions, and Search vs Shopping vs Performance Max splits — so budgets, bids, and reporting stay clean at any spend scale. Use this skill whenever the user mentions building campaigns, account structure, ad groups, restructuring, or "our account is a mess".
---

# Campaign Structure — SEM/PPC Sub-Agent

## Role & Mission

Own the account architecture: how campaigns, ad groups, and segmentation layers are organized so
that every budget, bid strategy, and report maps to one clear business purpose. Structure is the
control surface of paid search — it decides what you can bid on separately, cap separately, and
report separately. A messy structure makes every later optimization slower or impossible; a good
one makes routine work mechanical.

## When to Use

- Building a brand-new account or migrating/merging accounts
- "Our reporting is a mess" or budgets can't be controlled per product/theme
- Campaign sprawl: dozens of tiny campaigns starving each other of conversion data
- Adding Shopping, Performance Max, or Microsoft Advertising to an existing search account
- Entering new geographies or languages that need isolated budgets
- Preparing for smart bidding — consolidation questions ("can we merge these?")

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Keyword plan with intent tiers | Yes | From keyword-research-targeting |
| Product/service lines + margins | Yes | For Shopping tiers and budget priority |
| Brand term list | Yes | Brand vs non-brand separation |
| Monthly budget envelope + goals | Yes | Shapes campaign count and types |
| Geography / language targets | Preferred | Multi-location or multi-market scoping |
| Existing account export | Optional | Google Ads Editor account dump for audits |

## Output Contract

Return: (1) an architecture tree (campaigns → ad groups → keyword/asset groups), (2) a campaign
spec table, (3) naming convention, (4) shared negative list assignments, (5) build order. Core
spec format:

```markdown
| Campaign | Type | Goal / bid strategy | Geo | Budget share | Ad groups | Notes |
|---|---|---|---|---|---|---|
| SRC-Brand-Core | Search | Leads / Max Conv → tCPA $110 | US-EN | 20% | 3 | Defend brand SERPs |
| SRC-HVAC-Repair | Search | Leads / Max Clicks $12 cap | Austin metro | 45% | 6 | Non-brand |
| SHOP-Cat-Cooling | Shopping (std) | Sales / tROAS 400% | US | 35% | 5 product groups | Margin tier A |
```

Naming convention pattern: `TYPE-Theme-Geo` (e.g., `SRC-Plumbing-Emergency-Dallas`) so exports
sort cleanly and dashboards group by prefix.

## Workflow

1. Map business priorities to campaign types: standard Search for intent control, Shopping for
   e-commerce catalogs, Performance Max for scale where query-level control is less critical.
2. Separate Brand from non-brand search — different CPCs, CTRs, and CVRs; blending them destroys
   every benchmark you will ever read.
3. Decide the geo and language segmentation: one campaign per market only when budgets or bids
   must differ; otherwise use geo-targeted ad scheduling and location reporting instead.
4. Theme ad groups around a single intent/product cluster (5–20 keywords) so one ad set and one
   landing page can serve the whole group with tight message match.
5. Assign conversion goals per campaign (calls vs form fills vs purchases) so smart bidding
   optimizes toward the right action, not a blended average.
6. Define shared negative lists (brand-protection, competitor, jobs/free/DIY terms) and attach
   them at account or campaign level.
7. Write the naming convention and apply it to every planned entity; document budget share,
   bid strategy, and owner per campaign in the spec table.
8. Build via Google Ads Editor / Microsoft Advertising Editor in bulk; QA settings (networks,
   locations options, ad rotation) before enabling.
9. Deliver the blueprint to copy, extensions, bidding, and budget agents; set a structure
   review every quarter or whenever a campaign's data outgrows its home.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Bulk build & edits | Google Ads Editor, Microsoft Advertising Editor | Free; offline work, post-and-verify |
| Blueprint modeling | Google Sheets / Excel | Spec table + budget shares before building |
| Feed structure (Shopping) | Google Merchant Center | Product groups map to feed attributes |
| Account audit of existing mess | Google Ads UI reports, Adalysis (optional) | Lost IS and overlap reports |
| Change governance | Change history + naming convention docs | Sheets; prevents drift |

## Example AI Prompt

```text
You are a PPC account architect. Design the campaign structure for {BUSINESS} with these
inputs: products/services = {LIST}; keyword plan tiers = {PASTE OR SUMMARIZE}; geographies =
{GEO}; monthly budget = {AMOUNT}; conversion goals = {GOALS}; brand terms = {BRAND LIST};
e-commerce? {YES/NO — if yes, note catalog size and margin spread}.

Deliver:
1. Architecture tree: campaigns → ad groups (or asset groups / product groups).
2. Campaign spec table: type (Search/Shopping/PMax) | bid strategy | geo | budget share |
   ad group count | notes.
3. Naming convention with 3 examples.
4. Shared negative lists to create and where to attach them.
5. Build order for the first 2 weeks.
Constraints: keep enough conversion volume per campaign for smart bidding (≥30/month);
never blend brand and non-brand search in one campaign.
```

## Edge Cases & Guardrails

- Over-fragmentation is the modern failure mode: 30 campaigns at 5 conversions/month each
  starve smart bidding — consolidate until campaigns clear ~30 conversions/month.
- Performance Max claims branded-search conversions that would have happened anyway — keep a
  separate brand search campaign and read PMax with brand-included vs brand-excluded views.
- Do not duplicate the same keyword across campaigns targeting the same geography — you bid
  against yourself and pollute data.
- Leaving "Search partners" or Display Network expansion defaults on pollutes search data —
  verify network settings at build time.
- Device-only campaigns are rarely justified now; use bid adjustments instead unless a device
  truly cannot convert (e.g., desktop-only B2B tools).
- Document every exception; undocumented "temporary" campaign settings become permanent debt.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Conversions per campaign per month | ≥30 (smart bidding fuel) | <10 — consolidate |
| Keywords per ad group | 5–20 tightly themed | 50+ mixed-intent keyword dumps |
| Lost IS (budget) on priority campaigns | <20% | >40% — structure or budget mismatch |
| Brand / non-brand separation | 100% separated | Blended brand campaign |
| Naming convention compliance | 100% of entities | Free-text naming, unsearchable exports |

## Handoffs

- → **ad-copywriting** and **ad-extensions:** deliver the ad-group themes and campaign specs to
  write against; tight themes enable tight ads.
- → **bidding-strategy** and **budget-management:** the spec's bid strategies and budget shares
  are their starting plan.
- → **shopping-campaigns:** for e-comm, feed the product-line segmentation into Shopping/PMax
  structure.
- → **conversion-tracking:** goal-per-campaign mapping must exist before smart bidding enables.
- ↑ **sem-ppc-agent:** escalate structural conflicts (e.g., PMax vs brand search cannibalization).
