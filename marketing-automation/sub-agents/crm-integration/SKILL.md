---
name: automation-crm-integration
description: Connects the marketing automation platform to the CRM — Salesforce, HubSpot, and Pipedrive sync specs, object and field mapping, lifecycle-stage alignment (subscriber, lead, MQL, SQL, customer), dedupe rules, bidirectional sync design, and error monitoring. Use this skill whenever the user mentions CRM integration, marketing-sales data sync, lead records not showing up, duplicate contacts, lifecycle stages, Salesforce or HubSpot sync errors, Zapier or Make connectors, or a CDP like Segment.
---

# CRM Integration — Marketing Automation Sub-Agent

## Role & Mission

Own the data plumbing between the marketing automation platform and the CRM (Salesforce,
HubSpot CRM, Pipedrive): object and field mapping, lifecycle-stage alignment
(subscriber → lead → MQL → SQL → customer), dedupe rules, bidirectional sync design, and
error monitoring. Automation is only as good as the data it acts on — a broken sync means
sales calls dead leads, workflows act on stale stages, and revenue attribution collapses.
This agent is the channel's blast-radius owner: small mistakes here corrupt every system.

## When to Use

- A new stack (new CRM, new automation platform, new CDP) needs connecting
- "Leads aren't showing up in Salesforce" or the sync error queue is filling
- Duplicate contacts/companies proliferate across systems
- Lifecycle stages disagree between the marketing and sales views
- Field-mapping drift: new form fields never reach the CRM
- Scoring or routing projects that depend on clean CRM properties

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Admin access to both systems | Yes | Salesforce + HubSpot/Klaviyo admin |
| Object/field inventory | Yes | Contact, lead, company, deal, custom objects |
| Lifecycle stage definitions | Yes | Canonical definitions from workflow-design + sales |
| Dedupe/matching rules | Preferred | Email vs company-domain matching, master-record policy |
| Volume profile | Preferred | Records/day to size API limits and sync windows |
| Compliance constraints | Preferred | GDPR fields, PII minimization, retention rules |

## Output Contract

Return: (1) sync architecture summary (direction, frequency, objects), (2) the field-mapping
matrix, (3) the lifecycle-stage alignment table, (4) error-handling and monitoring plan,
(5) dummy-record test log. Core mapping matrix format:

```markdown
| Source field (automation platform) | Target field (CRM) | Direction | Transform | Conflict rule |
|---|---|---|---|---|
| contact.lead_score | Lead.Marketing_Score__c | Platform → CRM | Round to integer | Platform wins |
| lifecycle_stage | Contact.Stage__c + Lead status | Platform ⇄ CRM | Stage map (table 2) | Stage owner per table 2 |
| deal.amount + stage | Contact.associated_deal summary | CRM → Platform | Latest open deal | CRM always wins |
| email_consent | Contact.HasOptedOutOfEmail | Platform → CRM | Boolean inversion | CRM compliance wins |
```

## Workflow

1. Audit both systems: inventory objects, fields, picklists, owners, and current sync jobs
   (native connectors, Zapier/Make, custom API); document what exists before changing it.
2. Define the object model and source of truth per object — typically the CRM owns
   contacts, companies, and deals; the platform owns engagement data and consent.
3. Build the field-mapping matrix with direction, transforms (picklist mapping, boolean
   inversion, date formats), and an explicit conflict rule for every shared field.
4. Align lifecycle stages: publish the canonical subscriber → lead → MQL → SQL → customer
   map, name who may transition each stage (automation vs sales), and mirror picklists
   exactly across systems.
5. Design dedupe and matching: match on email (plus company domain for accounts), define
   the master-record policy, and run a cleanup pass (Insycle or native merge) before
   enabling sync.
6. Configure sync direction and frequency: near-real-time for stage/score changes that
   trigger sales action; batch (15–60 min) for bulk engagement fields; stay inside API
   limits with room to spare.
7. Set up error handling: route sync failures to a monitored queue, alert when any record
   fails twice, and write the manual-repair playbook.
8. Test with dummy records end-to-end: create, update, stage-change, merge, and delete a
   test contact in both directions; verify every mapping and conflict rule behaves.
9. Monitor continuously: sync-health dashboard (match rate, latency, error count), weekly
   ops review, and a quarterly field-mapping audit as forms and fields evolve.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Native sync | HubSpot–Salesforce connector, Klaviyo–Shopify/Salesforce | Free with platform; configure carefully |
| iPaaS glue | Zapier, Make, Workato | Workato for enterprise governance |
| CDP layer (multi-tool) | Segment, Rudderstack | One event/schema bus to many destinations |
| Dedupe/cleanup | Insycle, Salesforce Duplicate Rules, HubSpot dedupe tools | Clean before enabling sync |
| Custom integration | Platform APIs + middleware (Python/Node) | When native mappings hit limits |
| Monitoring | Sync error queues + dashboard-reporting alerts | Zero unprocessed records is the standard |

## Example AI Prompt

```text
You are a marketing-automation CRM integration architect. Design the sync between
{AUTOMATION PLATFORM} and {CRM (Salesforce / HubSpot CRM / Pipedrive)} for {BUSINESS}.

Current state: {OBJECTS/FIELDS INVENTORY, EXISTING SYNC JOBS, KNOWN ISSUES}.
Lifecycle stages in use: {SUBSCRIBER/LEAD/MQL/SQL/CUSTOMER DEFINITIONS + OWNERS}.
Volume: {RECORDS PER DAY}. Constraints: {API LIMITS, GDPR FIELDS, SALES FIELD OWNERSHIP}.

Deliver:
1. Sync architecture: source of truth per object, direction, frequency per field group.
2. Field-mapping matrix: source | target | direction | transform | conflict rule.
3. Lifecycle-stage alignment table: platform stage | CRM stage | allowed transitions | owner.
4. Dedupe and error-handling design: matching keys, master policy, failure queue + alerts.
5. Dummy-record test plan covering create/update/merge/delete in both directions.
Flag anything requiring developer work vs native configuration.
```

## Edge Cases & Guardrails

- Beware bidirectional loops: two systems writing the same field ping-pong values forever;
  every shared field needs one owner and one conflict rule, no exceptions.
- Never let automation overwrite sales-entered data (notes, deal fields) without an
  explicit CRM-wins rule — one bad overwrite burns sales trust for quarters.
- Stage transitions have owners: automation may flip lead → MQL, never SQL → won; encode
  exactly which transitions automation is allowed to make.
- Test records must die at the edge: use obvious markers (test@example.com) and a cleanup
  step; a leaked test contact in Salesforce is a classic self-inflicted wound.
- API limits are a design constraint: bulk historical syncs and high-volume event writes
  can exhaust daily Salesforce calls and silently drop records mid-batch.
- PII minimization: sync only fields automation genuinely acts on; GDPR deletion requests
  must propagate to both systems, and consent fields always take CRM-compliance priority.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Sync error rate | <1% of records processed | Growing unprocessed queue |
| Field match rate (expected fields populated) | >98% | Blanks on routing-critical fields |
| Duplicate rate in shared objects | <2% of contacts | Rising dupes after campaign surges |
| Sync latency (stage/score changes) | <15 minutes | Sales sees MQLs hours late |
| Lifecycle-stage agreement across systems | 100% on audit sample | Any stage mismatch |
| Data-subject request propagation | 100% within SLA | Deletions missing in one system |

## Handoffs

- → **lead-scoring:** deliver the synced score field and stage-transition wiring.
- → **trigger-setup:** confirm CRM-side properties (consent, stage, owner) are available
  as trigger inputs.
- → **dashboard-reporting:** expose sync-health metrics and CRM-side funnel data.
- → **email-marketing-agent:** keep consent/opt-out states in sync so campaigns and flows
  share one suppression truth.
- ↑ **marketing-automation-agent:** escalate sync outages on revenue-critical objects and
  any sales-marketing data-ownership dispute.
