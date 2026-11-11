# Vibe Coding Project: Living Repo

> **Metric Moment Compass:** help a product lead investigate an activation decline with enough context to explain the next step.

My final project for Product School's **AI Vibe Coding** certification follows **Scenario 04: The Dashboard Nobody Reads**, locked for Modules 2–6.

Module 1 exposed the gap: peers understood the metric and suggested action, but could not judge why a starter-template nudge would address the decline. Module 2 added supporting context so the user could choose and justify an investigation. Module 3 extends that flow through campaign comparison and detail, with explicit loading, empty, error, and recovery behavior. A subsequent design revision pairs activation with audience mix and lets users collect evidence while writing their own investigation notes.

- **The bet:** A focused activation headline plus accessible supporting evidence helps a product lead choose a next investigation, explain the evidence, and identify what remains unknown without spreadsheet export or coaching.
- **Try the build:** [Latest Module 3 dashboard](https://metric-moment-compass.anajuana.chatgpt.site/) · [Campaign comparison](https://metric-moment-compass.anajuana.chatgpt.site/campaigns/) · [preserved Module 1 v2](https://metric-moment-compass.anajuana.chatgpt.site/module-1/).
- **Read the deliverables:** [M3 Living Prompt Pack](03-chaining/PROMPTS.md) · [latest design and screenshots](03-chaining/design-v4/RESULT.md). The [M2 validation brief](02-validation/validation-brief.md) defines the hypothesis, with the [v3 build record](02-validation/prototype-v3.md) preserving that earlier iteration.
- **Evidence today:** Module 1 peer feedback informed the changes. The [v3 feedback](02-validation/show-and-swap-notes.md) connected the headline to channel mix but flagged prewritten answer cues. Course baselines and illustrative activation data remain separate.
- **Biggest unknown and next test:** Can a product lead explain a defensible investigation without following supplied answer cues? M3 keeps reasoning fields blank and reveals supporting facts through exploration. The next test is a three-minute unaided walkthrough of the revised flow. The usability hypothesis has not passed yet.

This repository holds the course write-ups, screenshot evidence, and share links.

---

## Deliverables at a glance

| # | Module | Deliverables | Status | Folder |
|---|---|---|---|---|
| 1 | **Velocity** | [v1](01-velocity/prototype-v1.md) · [v2](01-velocity/prototype-v2.md) · [reflection](01-velocity/confidence-line-reflection.md) | Complete, including both peer reads | `01-velocity/` |
| 2 | **Validation** | [brief](02-validation/validation-brief.md) · [v3](02-validation/prototype-v3.md) · [peer notes](02-validation/show-and-swap-notes.md) | Brief, build, and feedback recorded; follow-up implemented in M3 | `02-validation/` |
| 3 | **Prompt Chaining** | [Living Prompt Pack](03-chaining/PROMPTS.md) · [design prompts](03-chaining/design-v4/DESIGN-PROMPTS.md) · [results and screenshots](03-chaining/design-v4/RESULT.md) | Chain executed; results and reflection recorded; prompt peer read pending | `03-chaining/` |
| 4 | **Production Specs** | `PRD.md` · `handoff-note.md` | Not started | `04-production/` |
| 5 | **Full-Stack** | deployed share link + hardening notes | Not started | `05-fullstack/` |
| 6 | **Evals & Iteration** | final showcase + go/iterate/kill recommendation | Not started | `06-iteration/` |

## Module 3: Prompt Chaining

Executed November 10, 2026. The main deliverable is [PROMPTS.md: Living Prompt Pack](03-chaining/PROMPTS.md), containing the reusable **Expand → Behavior → Refine** chain, each step's inputs and outputs, execution results, techniques learned, and the routing issue found and fixed.

- **Expand:** Added [Campaign comparison](https://metric-moment-compass.anajuana.chatgpt.site/campaigns/) and [Campaign detail](https://metric-moment-compass.anajuana.chatgpt.site/campaigns/social/), with shared sample counts that reconcile to the existing paid-acquisition totals.
- **Behavior:** Verified loading, empty, failed-request, Retry, direct-link, and unknown-campaign states. [Execution screenshots](03-chaining/assets/) document the normal and recovery paths.
- **Refine:** Audited the campaign-detail heading against the reference. It already matched, so the chain records a verified no-change result with before/after captures.

The subsequent [design revision](03-chaining/design-v4/RESULT.md) uses the selected Profound reference to improve hierarchy and paired comparisons. It adds observation collection, drafts that survive navigation, and saved evidence snapshots. The [design prompts](03-chaining/design-v4/DESIGN-PROMPTS.md), [baseline screenshots](03-chaining/design-v4/before/), and [14 final screenshots](03-chaining/design-v4/after/) preserve the changes and their rationale.

Course quotes and dashboard-use metrics remain visible on the separate [Research context page](https://metric-moment-compass.anajuana.chatgpt.site/research/). The main dashboard focuses on activation and the next investigation. All activation and campaign figures are illustrative, and notes are stored only in the current browser.

The build passed 54 automated checks, TypeScript, and the production build, with desktop and mobile browser verification. Prompt cold-read feedback has not been recorded; these implementation checks do not establish a usability result.

## My scenario

**Chosen scenario:** Scenario 04, The Dashboard Nobody Reads. Locked November 5, 2026.

**Primary risk:** Usability. A product lead sees a fall in first-project activation but needs related signals to decide what to investigate. The prototype tests that decision-making task. It does not test whether a template nudge improves activation.

## The three ingredients (visible in every build)

1. **Hypothesis:** The specific usability bet and observable pass/fail rule in the [validation brief](02-validation/validation-brief.md).
2. **Domain data:** Four course-provided dashboard baselines on the [Research context page](https://metric-moment-compass.anajuana.chatgpt.site/research/), separate from the illustrative activation and channel comparison.
3. **User voice:** Three verbatim course-provided quotes on that same page, informing the [current design](03-chaining/design-v4/RESULT.md).

___

## How to submit

- Commit one artifact per module, the repo is the deliverable.
- Submit your repo URL (and deployed link) to the learning platform within 7 days of your cohort ending.

## Repo structure

```
product-school-vibe-coding/
├── README.md                       ← this dashboard
├── 01-velocity/
│   ├── prototype-v1.md             ← M1 Lab 1: first build + Show & Swap read
│   ├── prototype-v2.md             ← M1 Lab 2: two upgrade passes (toy → tool)
│   └── confidence-line-reflection.md ← M1: optional reflection
├── 02-validation/
│   ├── validation-brief.md         ← M2: hypothesis · risk · kill switch
│   ├── prototype-v3.md             ← M2: the build that tests it
│   └── show-and-swap-notes.md      ← M2: peer feedback
├── 03-chaining/
│   ├── PROMPTS.md                  ← M3: executed Living Prompt Pack + reflection
│   ├── assets/                     ← M3: flow, state, and heading screenshots
│   └── design-v4/
│       ├── DESIGN-PROMPTS.md       ← saved design prompts + selected reference
│       ├── RESULT.md               ← design decisions, checks, and screenshot index
│       ├── before/                 ← baseline screenshots
│       ├── after/                  ← final desktop, mobile, and state screenshots
│       └── reference/              ← selected Profound reference
├── 04-production/
│   ├── PRD.md                      ← M4: living PRD
│   └── handoff-note.md             ← M4: engineering handoff
├── 05-fullstack/
│   └── fullstack.md                ← M5: data, access rules, edge cases, deploy link
└── 06-iteration/
    └── iteration.md                ← M6: analytics + go/iterate/kill recommendation
```
