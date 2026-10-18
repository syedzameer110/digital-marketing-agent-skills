---
name: email-email-design
description: Builds and maintains responsive, client-proof email templates — modular HTML layouts that render correctly in Outlook, Gmail, and Apple Mail, survive dark mode, pass accessibility checks, and carry brand styling with fast load times. Use this skill whenever the user needs an email template, email design, responsive email layout, HTML email coding, dark-mode fixes, broken rendering, render testing, or says "our emails look broken in Outlook" — even if they never say "email design" explicitly.
---

# Email Design — Email Marketing Sub-Agent

## Role & Mission

Own the visual and technical layer of every send: the modular template system that carries
brand identity into the inbox and renders correctly wherever it lands. The outcome this
agent is accountable for: templates that pass render tests across the major clients,
remain readable with images off and in dark mode, load fast, and can be assembled by
non-designers in the ESP — because email design is the only design discipline where the
"browser" is 15+ rendering engines, including one (Outlook) that uses a word-processor
engine from the 1990s.

## When to Use

- New template needed for campaigns, flows, or a rebrand
- "Our email looks broken in Outlook" or images stack oddly on mobile
- Dark mode is inverting brand colors and making text unreadable
- Accessibility complaints or zero alt-text discipline
- Template governance: everyone builds something different in the ESP
- Migrating ESPs and templates must be rebuilt and re-tested

## Inputs

| Input | Required? | Example / Source |
|---|---|---|
| Brand kit (colors, fonts, logo, imagery) | Yes | Design system or brand guidelines |
| Client/device mix data | Yes | ESP per-campaign client reports |
| Campaign content and structure needs | Yes | From copywriting: sections, CTA count |
| ESP template builder constraints | Yes | Drag-and-drop vs custom HTML support |
| Past render issues | Preferred | Screenshots of failures in Outlook/Gmail |
| Legal footer requirements | Yes | Physical address, unsubscribe (CAN-SPAM/GDPR) |
| Accessibility target | Optional | WCAG AA color contrast, alt-text policy |

## Output Contract

Return a template package: (1) modular block inventory, (2) design spec (widths, type
scale, spacing, colors with dark-mode-safe pairings), (3) render-test report table, (4)
accessibility checklist results, (5) usage guide for the ESP builder. Core render report:

```markdown
| Client | Version | Layout | Images | Dark mode | CTA tap target | Verdict |
|---|---|---|---|---|---|---|
| Gmail | iOS app, dark mode | Intact | Loaded, alt text OK | Safe (adjusted pairs) | 44px, passes | Pass |
| Outlook 2019 | Windows | Intact (VML hero) | Loaded | n/a | Pass | Pass with fallback |
| Apple Mail | iOS, dark mode | Intact | Loaded (MPP prefetch) | Body inverted — fixed via padded color blocks | Pass | Pass after fix |
```

## Workflow

1. Pull the client/device mix from the ESP: establish which 6–8 clients actually matter
   (typically Gmail app/web, Apple Mail iOS, Outlook Windows/web, mobile web) and design
   evidence-based, not for every client ever made.
2. Define the modular block system: header/nav, hero, text, image+text, product grid,
   testimonial, single CTA, footer — every email assembles from these blocks.
3. Build on bulletproof fundamentals: 600px max width, table-based layout with inline CSS,
   web-safe font stacks with graceful web-font fallback, PNG/JPG under ~1MB total weight.
4. Engineer the failure modes: VML or solid-color fallbacks for Outlook background images,
   preheader text, alt text on every image, live-text headlines (never one big image),
   and dark-mode-safe color pairs (avoid pure black/white and thin weight fonts).
5. Run render tests in Litmus or Email on Acid across the target client matrix; screenshot
   and fix every layout break before stakeholders ever see it.
6. Run the accessibility pass: 4.5:1 text contrast, 14px+ body size, 44px tap targets,
   semantic structure, meaningful alt text.
7. Load the blocks into the ESP as locked, reusable modules with swappable content zones;
   document which blocks exist and when to use each.
8. QA the footer once, perfectly: unsubscribe link (working, one-click where required),
   physical postal address, and preference-center link — required by CAN-SPAM and expected
   under GDPR.
9. Re-test after every brand change, ESP update, or new block; keep a versioned changelog
   and archive screenshots as regression baselines.

## Tools & Stack

| Task | Recommended tools | Notes |
|---|---|---|
| Render testing | Litmus, Email on Acid | ~$99/mo+; the industry standard pair |
| Coding (when custom) | MJML, Cerberus templates | MJML compiles table-safe HTML; Cerberus free |
| ESP builders | Klaviyo, Mailchimp, HubSpot | Locked modules beat free-form design |
| Design comps | Figma, Canva | Canva free tier for lightweight teams |
| Image optimization | TinyPNG, Squoosh | Free; keep total email weight low |
| Accessibility checks | built-in contrast checkers, screen-reader spot test | Manual pass on the master template |

## Example AI Prompt

```text
You are an email design engineer. Brand kit: {COLORS, FONTS, LOGO USAGE}. ESP: {ESP +
builder type}. Client mix (from ESP data): {e.g. Gmail iOS 30%, Apple Mail 25%, Outlook
Windows 20%, Gmail web 15%, other 10%}. Email types to support: {NEWSLETTER / PROMO /
FLOW / ALL}. Known past failures: {ISSUES, e.g. hero image drops in Outlook}.

Deliver:
1. A modular block inventory for this template system with when-to-use notes per block.
2. A design spec: max width, type scale, spacing rhythm, button specs, and dark-mode-safe
   color pairings (flag any brand colors that will break in dark mode).
3. Coding guidance per failure-prone element (backgrounds, custom fonts, stacked columns)
   with the Outlook/Gmail fallback for each.
4. A render-test matrix I should run in Litmus/Email on Acid, scoped to my client mix.
5. An accessibility and compliance checklist (alt text, contrast, tap targets, unsubscribe,
   postal address).
```

## Edge Cases & Guardrails

- Outlook renders HTML with the Microsoft Word engine: no border-radius, unreliable
  background images (needs VML), limited padding support. Bulletproof buttons and
  table layouts are non-negotiable, not stylistic preferences.
- Dark mode is not one thing — Gmail, Apple Mail, and Outlook each invert differently;
  the only safe approach is tested color pairs and avoiding pure #000/#FFF.
- Never send an email that is one giant image: with images blocked it renders blank,
  spam filters weigh image-to-text ratios, and screen readers get nothing.
- Apple MPP prefetches images for open tracking — image-loading stats are fictional;
  do not "optimize" design decisions around MPP-generated open data.
- Custom web fonts fail silently in many clients: always define a font stack fallback;
  a branded font that falls back to Times New Roman is worse than choosing Georgia.
- The compliance footer is design work: unsubscribe must be visible and functional,
  physical address present (CAN-SPAM), sender identification truthful — a template that
  hides the unsubscribe link is a lawsuit and a spam-folder ticket.

## KPIs & Benchmarks

| Metric | Healthy range | Red flag |
|---|---|---|
| Render-test pass rate (target client matrix) | 95%+ of clients | Any flagship client broken |
| Total email weight | <1MB, ideally <500KB | Multi-MB hero-driven emails |
| Alt-text coverage on images | 100% | Decorative-only emails |
| Body text size / tap targets | 14px+ / 44px | 10px text, 24px buttons |
| Template reuse (built from system blocks) | 80%+ of sends | Every campaign hand-built |
| Template audit cadence | Every 6 months | Unchanged since the last rebrand |

## Handoffs

- → **copywriting:** receive content structure (sections, CTA count, tone) and return
  layout constraints (headline lengths that fit, image zones).
- → **email-automation:** supply flow-specific template variants (plain welcome email,
  product-grid cart email).
- → **ab-testing:** implement design variants (button color/label, hero style) as testable
  modules; rebuild winners into the system.
- → **analytics:** request client-mix and click-map data to prioritize which clients and
  blocks get optimization attention.
- ↑ **email-marketing-agent:** escalate when brand guidelines themselves break in dark
  mode or Outlook — that is a brand-system conversation, not a template patch.
