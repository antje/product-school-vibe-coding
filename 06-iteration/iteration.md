# Iteration: Analytics, Sprint, Final Recommendation

> Module 6 · Evals & Iteration. Read the analytics, run an iteration sprint, present with evidence.

## What the evidence says

- **Primary signal:** The review produced a specific audience-mix investigation, connected the activation headline to channel and campaign evidence, and identified missing causal information. These are the three reasoning elements in the [Module 2 validation brief](../02-validation/validation-brief.md).
- **What moved:** The reviewed flow supports a complete investigation: headline → channel comparison → campaign detail → collected observation → saved rationale and unknowns. Published version 8 adds **Copy summary** so the saved investigation can travel with its evidence and sample-data caveat. Browser checks confirmed copying for a public guest note and a local private note. A cancelled draft was excluded.
- **What didn't:** User drop-off, demand for copying, and any improvement in investigation quality remain unmeasured. The usability hypothesis still needs a user study.

**Evidence path:** qualitative review of the [public dashboard](https://metric-moment-compass.anajuana.chatgpt.site/), version 7, on November 22, 2026, before the sprint change. The walkthrough took 2 minutes 14 seconds from the usable overview to the final saved-note view. No product-usage analytics pipeline or provider analytics report is available in the inspected project. Visitors, page views, duration across sessions, bounce, retention, and user-success rates are **unmeasured**, not zero. The walkthrough duration is a single review timing, not an average session metric.

The displayed activation figures are illustrative. The course's 60% bounce and 74% spreadsheet-export figures are scenario inputs. Module 5 engineering tests establish functionality, persistence, and access controls, not adoption or independent user understanding.

| Signal | What the baseline review established | Limit |
|---|---|---|
| Reasoning from evidence | Chose to investigate the increase in paid signup share and audience changes within Social. Connected 42% → 38% overall activation to unchanged channel rates and Social's rising share. | Supports a coherent reading of the sample. It does not establish representative user success or a proven cause. |
| Core workflow | Opened channels and campaigns, collected Social evidence, and saved an investigation with rationale and unknowns. | Guest workflow only. No sign-in or signup was attempted in this review. |
| Continuity | The saved note and its Social observation remained after visiting Research context and returning. | Qualitative interaction check, not retention measurement. |
| Friction candidate | No visible copy/export/share action on the saved-note screen. | An expectation gap and candidate improvement, not an observed abandonment point or established demand. |
| Failures | No broken navigation or failed save was established in the reviewed flow. | No claim about all users, devices, or failure conditions. |

**Audit against the lab questions:** No ghost feature or repeated stall point can be identified without usage counts or repeated observations. The review is consistent with the intended evidence-to-investigation flow, but it does not establish that the M2 hypothesis has passed. Cohort reach, unaided completion rates, and repeated requests for explanation remain unmeasured.

## Iteration sprint

| Change | Hypothesis | Result |
|---|---|---|
| Add **Copy summary** to saved guest and private investigation notes. **Guardrail:** copy only saved content, and report success only after a confirmed clipboard write. | Carrying the saved question, rationale, unknowns, and evidence together may help a product lead bring the investigation into a discussion without reconstructing it. | Published as version 8. Public guest and local private-note clipboard checks passed. The summary preserved saved content, observations, source URLs, and the illustrative-data caveat. A cancelled draft was excluded. Usefulness in a discussion remains to be tested. |

**Why this change:** The baseline review identified one concrete extension: the saved-note screen had no copy/export/share action. The ranked backlog places copying first, fresh unaided user evidence second, and workflow measurement third. The latter two remain follow-up work. The [sprint brief](iteration-sprint-brief.md) preserves the evidence, ranking, exact prompts, and results.

**Verification:** All 158 tests across 18 files passed, including 10 new copy-summary tests. TypeScript and the production build passed. Reviews against the spec, coding standards, and security requirements reported no findings. Browser checks verified actual clipboard output for a saved private note locally and a guest note on public version 8. The public summary retained Social's 16/120 → 48/240 counts, comparison period, source link, and caveat. Account email and local-preview URLs were absent. Missing or denied clipboard access and the selectable fallback were verified in automated UI tests only.

**Evidence:** [Before](assets/before-copy-summary.jpg) · [Published after](assets/after-copy-summary.jpg) · [Actual copied summary](assets/copied-investigation-summary.txt) · [Local private-note check](assets/local-private-copy-summary.jpg).

## Peer feedback

Baseline public version 7 review, November 22, 2026. Qualitative feedback only, not a human-study result:

> It helps someone investigate a drop in first-project activation without jumping straight to a product fix. The overview starts with one metric, the channel and campaign screens separate activation rate from audience share, and the note asks for a next question, supporting evidence, and what remains unknown.

**Next investigation and evidence:**

> I would investigate why paid acquisition became a larger share of signups and which audiences changed within Social. Overall activation fell from 42% to 38%, while direct/organic and paid activation stayed at 50% and 30%. Social activation improved from 13.3% to 20%, even as its share of paid signups grew from 37.5% to 50%. Those observations make an audience-mix investigation more defensible than assuming onboarding got worse.

**What remains unknown:**

> The screens cannot tell me why that mix changed, whether targeting or spend changed, or what individual signups experienced. They explicitly say that product errors and template-use history are absent. The arithmetic describes the sample; it does not establish a cause.

Labelled feedback:

- **Compliment — Metric clarity:** the overview defines activation and shows the counts behind the percentage change.
- **Compliment — Evidence travels with the note:** adding Social preserved its activation, signup share, counts, period, and source link in the saved investigation.
- **Compliment — Clear limits:** the screens distinguish observed totals, missing causal information, illustrative activation data, and course-scenario research.
- **Feature Idea — Carry the investigation into a discussion:** no copy/export/share control was visible on the saved-note screen. A copyable summary with its evidence and illustrative-data caveat is a candidate improvement.

**Credibility:** suitable to show a VP as a focused product demonstration, with the sample-data limitation explicit. It is not evidence of actual business performance or measured product impact.

Historical [Module 1 peer feedback](../01-velocity/prototype-v2.md#show--swap-read-round-2) questioned the link between the activation decline and a template nudge, and asked for related metrics. It explains the shift toward investigation, but is not counted as feedback on this build.

## The recommendation

**Decision:** ☐ Go  ☑ Iterate  ☐ Kill.

The baseline guest workflow completed without an observed navigation or save failure and supported a coherent investigation. Lab 2 addressed the handoff candidate with one reversible change, **Copy summary**, verified its saved-content behaviour, and published it. This supports continued iteration. A broader launch needs evidence from intended users.

**Next decision gate, owned by Antje:** before prioritizing another feature, repeat the three-minute unaided reasoning test with a fresh representative product lead. Keep the original three criteria: name an investigation, connect the headline and a related signal to it, and identify an unknown. If any criterion fails, revise that step and repeat the test. If all three pass, continue validation with additional leads and their data before making an adoption claim. An unrun or coached test does not clear the gate. Assess the copied summary's usefulness separately, after the reasoning explanation, so the new control does not become a cue.

Modules 3–6 advanced the engineering work without establishing the original usability assumption. That is a limitation of the course build. The next investment is evidence about independent reasoning, rather than more capability.

Confidence has increased in implementation. Adoption, the quality of independent reasoning, and the value of the copied summary remain open questions.

## Final showcase

- **Demo link:** https://metric-moment-compass.anajuana.chatgpt.site/
- **Publication evidence:** Version 8 deployed successfully on November 22, 2026. The public guest-note copy check passed. Source commit: `a9d03cf3cc907e90ce559a0a89a4f1bd2b4dd6a3`.
- **The one-sentence story:** Metric Moment Compass turns an activation decline into a reasoned next investigation that carries its evidence and uncertainty into a discussion.
- **Where it landed on the Confidence Line (M2 → now):** The build has progressed from a clickable hypothesis test to a deployed investigation workflow with hosted sample data, private cloud notes, and a copyable summary. Engineering confidence has increased. The M2 usability hypothesis and real-world usefulness still need validation.
- **Showcase:** [Final presentation](../final-presentation.html), a self-contained HTML file. It carries the product, hypothesis, PRD, prompt chain, handoff, evidence, and Iterate decision into one story. The same file is staged at [docs/index.html](../docs/index.html) for optional Pages hosting.
