# Vibe Coding Project: Living Repo

> **Metric Moment Compass:** help a product lead investigate an activation decline with enough context to explain the next step.

My final project for Product School's **AI Vibe Coding** certification follows **Scenario 04: The Dashboard Nobody Reads**, locked for Modules 2–6.

Module 1 exposed the gap: peers understood the metric and suggested action, but could not judge why a starter-template nudge would address the decline. Module 2 adds supporting context so the user can choose and justify an investigation.

- **The bet:** A focused activation headline plus accessible supporting evidence helps a product lead choose a next investigation, explain the evidence, and identify what remains unknown without spreadsheet export or coaching.
- **Try the build:** [Module 2 v3](https://metric-moment-compass.anajuana.chatgpt.site/) · [preserved Module 1 v2](https://metric-moment-compass.anajuana.chatgpt.site/module-1/).
- **Read the main deliverable:** [Validation brief](02-validation/validation-brief.md), then [v3 build and screenshots](02-validation/prototype-v3.md).
- **Evidence today:** Module 1 peer feedback informed the changes. The [v3 feedback](02-validation/show-and-swap-notes.md) connected the headline to channel mix but flagged prewritten answer cues. Course baselines and illustrative activation data remain separate.
- **Biggest unknown and next test:** Can a product lead explain a defensible investigation without following supplied answer cues? Revise the evidence-to-reasoning flow, then repeat the cold read. The usability hypothesis has not passed yet.

This repository holds the course write-ups, screenshot evidence, and share links.

---

## Deliverables at a glance

| # | Module | Deliverables | Status | Folder |
|---|---|---|---|---|
| 1 | **Velocity** | [v1](01-velocity/prototype-v1.md) · [v2](01-velocity/prototype-v2.md) · [reflection](01-velocity/confidence-line-reflection.md) | Complete, including both peer reads | `01-velocity/` |
| 2 | **Validation** | [brief](02-validation/validation-brief.md) · [v3](02-validation/prototype-v3.md) · [peer notes](02-validation/show-and-swap-notes.md) | Brief, build, and review feedback recorded; next iteration proposed | `02-validation/` |
| 3 | **Prompt Chaining** | [Living Prompt Pack](03-chaining/PROMPTS.md) · [design prompts](03-chaining/design-v4/DESIGN-PROMPTS.md) · [results and screenshots](03-chaining/design-v4/RESULT.md) | Chain executed; results and reflection recorded; prompt peer read pending | `03-chaining/` |
| 4 | **Production Specs** | [Living PRD](04-production/PRD.md) · [engineering handoff](04-production/handoff-note.md) | PRD and handoff complete. Refactor and Supabase verified. | `04-production/` |
| 5 | **Full-Stack** | [Data, access rules, edge cases, and deploy](05-fullstack/fullstack.md) | Published. Private persistence, access rules, and offline recovery verified. Signup email delivery remains a known gap. | `05-fullstack/` |
| 6 | **Evals & Iteration** | final showcase + go/iterate/kill recommendation | Not started | `06-iteration/` |

## My scenario

**Chosen scenario:** Scenario 04, The Dashboard Nobody Reads. Locked November 5, 2026.

**Primary risk:** Usability. A product lead sees a fall in first-project activation but needs related signals to decide what to investigate. The prototype tests that decision-making task. It does not test whether a template nudge improves activation.

## The three ingredients (visible in every build)

1. **Hypothesis:** The specific usability bet and observable pass/fail rule in the [validation brief](02-validation/validation-brief.md).
2. **Domain data:** Four course-provided dashboard baselines on screen, separate from the illustrative activation and channel comparison.
3. **User voice:** Three verbatim course-provided quotes, connected to the choices in the [v3 build](02-validation/prototype-v3.md).

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
│   └── PROMPTS.md                  ← M3: the Living Prompt Pack
├── 04-production/
│   ├── PRD.md                      ← M4: living PRD
│   └── handoff-note.md             ← M4: engineering handoff
├── 05-fullstack/
│   └── fullstack.md                ← M5: data, access rules, edge cases, deploy link
└── 06-iteration/
    └── iteration.md                ← M6: analytics + go/iterate/kill recommendation
```
