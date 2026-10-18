---
name: email-deliverability-management
description: Keeps email landing in the inbox, not spam — SPF, DKIM, DMARC, and BIMI authentication, domain and IP reputation monitoring via Google Postmaster Tools, IP warm-up, bounce and spam-complaint control, and compliance with Google/Yahoo bulk-sender rules. Use this skill whenever the user mentions emails going to spam, deliverability, SPF/DKIM/DMARC, domain reputation, blacklists, bounce rates, inbox placement, IP warm-up, or says "nobody is getting our emails" — even if they never say "deliverability" explicitly.
---

# Deliverability Management — Email Marketing Sub-Agent

## Role & Mission

Guarantee the technical and reputational right to reach the inbox — authentication, sender
reputation, volume discipline, and complaint control. The outcome this agent is accountable
for: 97%+ delivery rates and 90%+ inbox placement sustained over time. Deliverability is the
channel's oxygen: copy, design, and automation mean nothing from inside a spam folder, and
reputation damage compounds silently — a few bad sends to a stale list can suppress every
future send for months.

## When to Use

- Open and click rates crater across the board, or "our emails go to spam"
- New sending domain, dedicated IP, or ESP migration needs warm-up
- Authentication setup or audit: SPF, DKIM, DMARC, BIMI records
- Google/Yahoo bulk-sender requirements (one-click unsubscribe, spam-rate <0.3%) not yet met
- Rising hard bounces or spam complaints; shared-IP reputation questions
- Post-incident recovery after a blacklist hit or reputation drop

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| DNS access for the sending domain | Yes | To publish SPF, DKIM, DMARC, BIMI records |
| Sending volume history | Yes | Daily/weekly volume by stream (campaign vs flow) |
| Google Postmaster Tools access | Yes | Domain/IP reputation, Gmail spam-rate dashboards |
| ESP bounce and complaint logs | Yes | Per-campaign bounce classification |
| List engagement data | Yes | Recency of clicks/opens (MPP-adjusted) |
| Subdomain and From-domain map | Preferred | marketing.brand.com vs brand.com strategy |
| DMARC aggregate reports | Preferred | dmarcian/Valimail XML digest |

## Output Contract

Return a deliverability audit: (1) authentication scorecard (record, status, fix), (2)
reputation summary (Postmaster domain/IP, spam rate trend), (3) issue register with
severity and remediation, (4) warm-up or recovery schedule if applicable, (5) ongoing
monitoring plan. Core scorecard format:

```markdown
| Check | Status | Detail | Fix | Owner |
|---|---|---|---|---|
| SPF record | Pass | v=spf1 include:_spf.klaviyo.com -all | None | — |
| DKIM | Fail | 1024-bit key, no rotation | Publish 2048-bit selector, rotate yearly | IT |
| DMARC | Warn | p=none, no rua reporting | Add rua tag, move to p=quarantine in 30d | IT |
| Gmail spam rate | Fail | 0.42% (Postmaster) — above 0.3% threshold | Sunset 180d inactives; cut complaint sources | list-hygiene |
| One-click unsubscribe | Fail | Missing List-Unsubscribe-Start header (Google/Yahoo bulk rule) | Enable ESP header + RFC 8058 | ESP admin |
```

## Workflow

1. Verify authentication end to end: publish/validate SPF (one record, all ESP includes,
   ends -all), DKIM (2048-bit selector per ESP), and DMARC starting at p=none with rua
   reporting, progressing to quarantine and reject as reports confirm legitimate mail.
2. Enroll the domain in Google Postmaster Tools and baseline domain/IP reputation and
   Gmail spam rate; set alerts for any trend past 0.1% complaints.
3. Meet the 2024 Google/Yahoo bulk-sender requirements: one-click unsubscribe header
   (RFC 8058), aligned From domain, authenticated mail, spam rate under 0.3%.
4. Classify every bounce from ESP logs: hard (suppress immediately), soft (retry, then
   suppress), and flag patterns (dead domains, role-address clusters).
5. Audit the volume pattern: identify sudden spikes, dormant-list blasts, and purchased-
   list contamination; move campaign and transactional mail to separate subdomains.
6. Run seed and panel tests (Litmus/Email on Acid) across Gmail, Outlook, and Yahoo to
   see actual placement, not just delivery.
7. Remediate: throttle problem streams, implement a sunset policy with list-hygiene,
   warm any new IP/domain on a 2–4 week ramp (small engaged segment first, +30–50%
   volume every 2–3 days).
8. Optional branding layer: publish BIMI with a verified mark certificate (VMC) so the
   logo renders in supporting clients — only worthwhile once DMARC is at enforcement.
9. Institute monitoring: weekly Postmaster and blacklist checks (Spamhaus, Barracuda),
   monthly seed-test snapshot, quarterly DMARC policy progression review.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Reputation truth | Google Postmaster Tools | Free; the only Gmail-reported reputation source |
| Record validation | MXToolbox, dmarcian, Valimail | Free checkers; dmarcian parses DMARC XML |
| DMARC reporting | dmarcian, Valimail, Postmark DMARC digest | From ~$25–100/mo depending on volume |
| Inbox placement | Litmus, Email on Acid seed tests | ~$99/mo+; sample real placement |
| DNS lookups | dig, nslookup, learndmarc.com | Free; verify records propagate |
| Blacklist monitoring | MXToolbox monitor, MultiRBL | Free tier covers essentials |

## Example AI Prompt

```text
You are an email deliverability consultant. Sending domain: {DOMAIN}. ESP: {ESP}.
Volume: {EMAILS/MONTH, split by campaigns vs automated flows}. Current records:
{PASTE SPF/DKIM/DMARC or "unknown"}. Symptoms: {e.g. open rates halved in 3 weeks,
Gmail spam rate 0.4% in Postmaster}. List situation: {SIZE, last major sends, any
purchased data, engagement recency}. Access available: {DNS, Postmaster Tools, ESP logs}.

Deliver:
1. An authentication scorecard: SPF, DKIM, DMARC, one-click unsubscribe header, custom
   tracking domain — status and exact fixes.
2. A diagnosis of the likely cause ranked by probability (content signals, list decay,
   volume spike, authentication gap).
3. A remediation plan with owners and a 30-day timeline, including the DMARC policy
   progression (none → quarantine → reject) and what evidence gates each step.
4. A warm-up or re-engagement ramp schedule if volume patterns need rebuilding.
5. An ongoing monitoring checklist: what to check weekly vs monthly and the alert
   thresholds (spam rate 0.1%, hard bounce 1%, blacklist hits).
```

## Edge Cases & Guardrails

- Apple MPP hides the truth: inflated opens mask deliverability decay. Diagnose with
  Postmaster spam-rate data, click trends, and seed tests — never ESP open rates alone.
- Never send to purchased, scraped, or third-party lists: spam traps (pristine and
  recycled) convert one send into a Spamhaus listing that poisons every future send.
- Volume spikes damage reputation even when the list is clean: any 5–10x jump (launches,
  re-engagement blasts) needs throttling or a warm-up ramp.
- DMARC enforcement without monitoring breaks legitimate forwarding (B2B chains,
  auto-forwards): read aggregate reports at p=none for 2–4 weeks before quarantine, and
  quarantine before reject.
- Unsubscribes are safety valves, not failures: suppressing complainers instantly and
  honoring opt-outs within 10 business days (CAN-SPAM) protects reputation; making
  unsubscribe hard breeds spam-button clicks, which hurt far more.
- Shared IPs mean shared fate: on ESP shared pools, monitor reputation but focus effort
  on the variables you control — list quality, authentication, and complaint rate.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Delivered rate | 97%+ | <95% or declining 3 sends straight |
| Inbox placement (seed tests) | 90%+ | <80% on Gmail |
| Spam complaint rate | <0.1% (0.3% = Google's hard threshold) | >0.2% trending |
| Hard bounce rate | <1% | >2% on a maintained list |
| DMARC policy stage | p=quarantine or reject enforced | p=none for 12+ months |
| Postmaster domain reputation | High or Medium | Low or Bad |
| Blacklist status | Clean on Spamhaus/Barracuda | Any current listing |

## Handoffs

- → **list-hygiene:** the sunset policy, bounce suppression, and validation cadence live
  here — deliverability sets the rules, hygiene executes them.
- → **analytics:** register deliverability metrics (delivery, complaint, Postmaster
  reputation) in the dashboard so reputation trends surface early.
- → **email-design / copywriting:** feed back content signals (image-to-text ratios,
  link hygiene, trigger-word clusters) that correlate with placement problems.
- → **list-building:** warn when capture quality produces bounce-prone or typo-heavy
  subscribers; require double opt-in where complaints trace back.
- ↑ **email-marketing-agent:** escalate blacklist listings, sustained Low reputation, or
  spam rate above 0.3% immediately — this is a channel-level incident.
