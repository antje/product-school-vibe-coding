# Iteration Sprint Brief: Carry a Saved Investigation into a Discussion

**Product:** Metric Moment Compass  
**Live URL (before):** https://metric-moment-compass.anajuana.chatgpt.site/  
**Owner:** Antje Barth  
**Date:** November 22, 2026  
**Status:** Copy summary implemented, verified, and published as version 8. Decision: Iterate.

## 1 · Problem & Hypothesis

**Problem statement:** Product leads investigating a fall in first-project activation need supporting context to choose and explain what to investigate next. A headline alone does not explain the change or justify an intervention. The [Living PRD](../04-production/PRD.md#problem) anchors the flow: headline → supporting evidence → campaign drill-down → investigation note.

**M2 hypothesis:** A first screen with one headline metric, a plain-language takeaway, and accessible supporting context will help a product lead choose and explain a sensible next investigation without spreadsheet export or help. The [validation brief](../02-validation/validation-brief.md#hypothesis) requires a new peer, after a three-minute unaided walkthrough, to name an investigation, support it with the headline and at least one related signal, and identify a relevant unknown.

**Current confidence:** The current-build review produced those three reasoning elements. It is qualitative review evidence, not a representative user study or a validation of the hypothesis. The PRD's problem and hypothesis remain the anchor. Its older implementation inventory predates the current private-note flow.

## 2 · The Metrics

No product-usage analytics report is available in the inspected project. The following are review observations and evidence gaps, not usage counts. Full context is in [What the evidence says](iteration.md#what-the-evidence-says).

| Signal | Available evidence | Read and limit |
|---|---|---|
| Review walkthrough | 2 minutes 14 seconds from usable overview to final saved-note view | One review timing, not average session duration or an independent user-success rate. |
| Investigation workflow | Opened channels and campaigns, collected Social evidence, and saved a question, rationale, and unknowns | Establishes that the reviewed guest path completed. It does not measure how often users complete it. |
| Saved-note continuity | The note and its observation remained after navigation away and back | An interaction check, not retention. |
| Carrying the note into a discussion | No visible copy, download, or sharing control on the saved-note screen | A candidate handoff gap. No abandonment or demand has been measured. |
| Visitors, sessions, bounce, return, and task-success rates | Unmeasured | No production baseline, target, or trend can be calculated from this review. |

The dashboard's 42% → 38% activation change is illustrative business data. The course's 60% bounce and 74% spreadsheet-export figures are scenario inputs. Neither is a measurement of this product's usage. No broken navigation or failed save was established in the reviewed flow. Private account saving was outside this review.

## 3 · Peer Feedback

The November 22 current-build review supplied qualitative feedback. It is a single review, so there is no recurring theme established by multiple independent people. The [recorded feedback](iteration.md#peer-feedback) distinguishes current observations from historical Module 1 feedback.

- **Metric clarity:** “the overview defines activation and shows both 336/800 and 304/800 behind 42% → 38%.” This makes the sample arithmetic inspectable.
- **Evidence stays with the investigation:** “adding Social carried its activation, signup share, counts, period, and source link into the saved investigation.” This supports preserving the same context when the note is copied.
- **Handoff candidate:** “I did not see a copy, download, or sharing control there.” The proposed next step is a copyable summary for a discussion. This is an expectation gap, not a demonstrated user need.
- **Evidence limit:** “The arithmetic describes the sample; it does not establish a cause.” The copied summary must retain that limitation alongside the evidence.

The review considered the product credible as a focused demonstration. It did not establish real business impact, adoption, or independent user understanding.

## 4 · AI Analysis: Ranked Backlog

**Ranking method:** Qualitative impact versus effort, following *Decision rules* and *Prioritization* in the Product Playbook. “Impact” means likely contribution to the product lead's investigation workflow or the next product decision. Reach and effect size are unknown, so numerical scores would imply evidence we do not have.

| Rank | Improvement | Likely impact and rationale | Evidence, assumption, and scope |
|---|---|---|---|
| 1 | Add **Copy summary** to a saved investigation | **Medium, direct workflow impact.** It lets the question, rationale, unknowns, and collected evidence travel together into a discussion, preserving the purpose of the saved note. It is a small, reversible extension. | The missing control is observed. The benefit to discussions is a hypothesis. Selected for this sprint, with no claim that it improves activation, retention, or the M2 reasoning criteria. |
| 2 | Repeat the unaided reasoning test with fresh representative product leads | **Medium, decision impact.** It would reveal whether the intended users can choose and explain an investigation and identify uncertainty without coaching. | The missing evidence is observed. No usability failure is inferred. Follow-up research using the existing three criteria, after the change is verified. If any criterion fails, revise that step before further expansion. |
| 3 | Define a measurement plan and collect a real workflow baseline | **Lower immediate workflow impact, useful for later prioritization.** Counts of visits, context exploration, observation collection, saved notes, and returns could show where further investigation is needed. | Usage counts are absent. No ghost feature or drop-off point is inferred. Instrumentation, consent and data handling, and live-data integration need separate scope and are deferred. Event counts alone would still not establish reasoning quality. |

**Cut from this sprint:** Analytics integration and live-data replacement are larger work. A shared-link service, downloads, account changes, collaborative editing, and new analysis screens are unnecessary for testing a plain-text handoff. Revisit them only when user evidence identifies a need that copying a saved summary does not meet.

**Original analysis prompt, preserved:**

```text
Use the following evidence to rank the top three improvements for Metric Moment Compass by likely impact on its stated problem. Explain the evidence, assumption, expected benefit, effort, and reason to defer for each. Choose one reversible product change for this sprint.

Problem: product leads investigating declining first-project activation need context to choose and explain what to investigate next. The flow is headline → supporting evidence → campaign detail → investigation note.

M2 hypothesis: after a three-minute unaided walkthrough, a new peer can name an investigation, connect the headline and at least one related signal to it, and identify a relevant unknown without coaching or spreadsheet export. This remains unvalidated by a user study.

Evidence: a November 22 public guest-flow review took 2 minutes 14 seconds from usable overview to final saved-note view. It opened channels and campaigns, collected Social evidence, saved a rationale and unknowns, and found the saved note intact after navigation away and back. No broken navigation or failed save was established. Private account saving was not exercised. No product-usage analytics report is available. Visitors, sessions, bounce, retention, demand, and user-success rates are unmeasured. The displayed activation rates are illustrative, and course dashboard-use statistics are scenario inputs.

Feedback: the headline has definitions and counts, collected evidence preserves metrics, periods, and source links, and the screens state what remains unknown. The saved-note screen has no visible copy, download, or sharing action. A copyable summary could help carry the investigation into a discussion, but that benefit and demand are unmeasured.

Do not invent bugs, usage counts, recurring feedback, or causal impact. Rank independent user evidence and measurement as follow-up evidence gaps, not proven product failures. Keep this sprint to one finding and one change. Classify the chosen move as Persona, Branching, or Guardrail according to what primarily changes.
```

**Analysis rerun, November 22:** The original prompt above did not begin with the lesson's required phrase. The following rerun uses the same baseline inputs after implementation verification. It confirms the ranking without rewriting the prompt history.

```text
Based on the data showing that the November 22 public guest-flow review completed an investigation, retained the saved note after navigation, and found no visible copy, download, or sharing action, rerun the ranking of the top three improvements to Metric Moment Compass.

Use the same problem and M2 hypothesis recorded above: help a product lead choose and explain an investigation from the activation headline and a related signal, and identify an unknown after a three-minute unaided walkthrough. The hypothesis remains unvalidated by a user study.

The review took 2 minutes 14 seconds, opened channels and campaigns, collected Social evidence, and saved rationale and unknowns. No broken navigation or failed save was established. Private account saving was not exercised in that baseline review. The headline has definitions and counts, observations retain metrics, periods, and source links, and the screens state what remains unknown. Copying may help carry that context into a discussion, but demand and benefit are unmeasured.

No product-usage analytics report is available. Visitors, sessions, bounce, retention, and user-success rates are unmeasured. Activation figures are illustrative, and course dashboard-use statistics are scenario inputs. Rank by likely impact, state assumptions, and keep one reversible product change. Do not invent bugs, recurring feedback, usage counts, or causal impact. Treat independent user evidence and measurement as follow-up evidence gaps. Classify the selected move as Persona, Branching, or Guardrail.
```

**Rerun result:** The ranking remains **1. Copy summary**, **2. Repeat the unaided reasoning test**, **3. Define measurement and collect a baseline**. Copying is the concrete, reversible workflow extension supported by the review. Independent user testing is the next check on the underlying hypothesis. Measurement follows as separate work to support later prioritization. The chosen move remains **Branching**. The review does not establish the frequency or value of the copying need.

## 5 · The One Finding

- **Chosen finding:** A saved investigation preserves the reasoning and evidence inside the product, but the reviewed screen has no direct way to copy that complete context into a discussion.
- **Why this one:** It is the only concrete workflow extension suggested by the current review. The summary can preserve the question, evidence, and uncertainty together without requiring the reader to reconstruct them elsewhere. Its usefulness remains a hypothesis to test.
- **Move type: Branching.** Extend the saved note into a portable summary. Saved-state and privacy rules constrain that extension, but the primary move is adding a handoff to the investigation flow.
- **Expected behaviour:** After saving, a reader can copy the saved investigation as plain text with its supporting observations and sample-data caveat intact. Unsaved edits do not enter that summary.
- **Completion rule:** One saved-summary action works for guest and private notes. It reports clipboard success truthfully and offers selectable text when copying fails. Existing note editing, saving, clearing, account separation, and evidence snapshots continue to work.

## 6 · Implementation Prompt

```text
Based on the data showing that the November 22 public guest-flow review completed and retained a saved investigation but found no visible copy, download, or sharing action, add one Copy summary action to saved investigation notes in Metric Moment Compass. This is qualitative review evidence, not usage counts or proven demand. The intended benefit is carrying a saved investigation into a discussion with its evidence and uncertainty intact.

Apply the same action to existing saved guest and signed-in private notes. Build the plain-text summary from the SAVED note snapshot, never the current draft or the separate working observation collection. Include the investigation question, rationale, unknowns, saved supporting evidence where represented in the saved note, and every saved observation's title, metrics and counts, comparison period, and source URL. Preserve the stored observation text and values. Resolve stored relative source paths to usable absolute URLs. Include the explicit caveat: Illustrative sample data. These observations do not establish a cause or measure product impact.

Copy only the investigation content. Exclude account email, user IDs, authentication data, secrets, and internal storage metadata. Copying must not save a draft, overwrite a note, import guest content, write to the backend, or change access permissions. Hide or disable the action when there is no saved note. Make it clear that the action copies the saved version if an unsaved draft exists.

Show accessible inline feedback. Display Copied only after the clipboard write succeeds. If the clipboard API is absent or rejects the write, display the same summary in a selectable text field with a clear manual-copy instruction. Do not claim success for that fallback. Clear previous success or fallback feedback when the saved note changes or disappears, including note replacement, clearing, sign-in, sign-out, and account changes. Do not let an earlier asynchronous copy result restore feedback or private summary text after that change.

Keep all existing functionality working. Add focused checks for the saved snapshot versus an unsaved draft or changed working collection, the summary's evidence and caveat, clipboard success and failure, and feedback reset when the note or account changes. Check the visible action and fallback through real interaction. Keep this to one change. Do not add analytics, tracking, new backend work, downloads, shared links, new data sources, or a dashboard redesign.
```

**Tested?** Yes. All 158 tests across 18 files passed, including 10 new copy-summary tests. TypeScript and the production build passed. Reviews against the spec, coding standards, and security requirements reported no findings.

**What broke and was fixed:** The first full-suite run exposed five ambiguous status queries after adding the copy announcement. Save and copy now have distinct accessible names. The existing save assertions target the save announcement, and the complete suite passes.

**Browser evidence:** Local interaction verified the actual clipboard text for a saved private note. It retained the saved investigation and evidence, excluded a cancelled unsaved draft, and contained neither account email nor local-preview URLs. The public version 8 guest-note check also passed: **Copied** appeared and the clipboard retained Social's counts, comparison period, canonical source URL, and exact illustrative-data caveat. Missing or denied clipboard access and the selectable fallback were verified in automated UI tests only.

## 7 · Result & Redeployed URL

- **Before → after:** The saved note had no visible copy action → published version 8 provides **Copy summary** for the saved investigation, evidence, source URLs, and illustrative-data caveat. Clipboard failure exposes the same summary for manual selection without a false success message.
- **Observed result:** Public guest-note and local private-note clipboard checks passed. A cancelled draft was excluded. Automated tests covered clipboard fallback. These results establish implementation behaviour. Usage and usability improvement remain unmeasured.
- **Evidence:** [Before](assets/before-copy-summary.jpg) · [Published after](assets/after-copy-summary.jpg) · [Actual copied summary](assets/copied-investigation-summary.txt) · [Local private-note check](assets/local-private-copy-summary.jpg).
- **Redeployed live URL:** https://metric-moment-compass.anajuana.chatgpt.site/
- **Deployment verification:** Version 8 deployed successfully on November 22, 2026. Source commit: `a9d03cf3cc907e90ce559a0a89a4f1bd2b4dd6a3`. The public guest-note check verified rationale, 16/120 and 48/240 counts, the comparison period, the Social source URL, and the caveat in the actual clipboard output.
- **Folded into:** [iteration.md](iteration.md) records the sprint result and recommendation. The [README](../README.md) records completed Labs 1–2 and the outstanding final showcase.
- **Recommendation:** **Iterate.** The reviewed guest workflow supports a coherent investigation, and the copy-summary implementation passed verification and is live. Independent user understanding, actual usage, and the usefulness of the handoff remain unmeasured. Test those assumptions before expanding scope.

The next validation uses a fresh representative product lead and the existing unaided reasoning criteria. Assess whether the saved summary can support a discussion separately, after the reasoning explanation is recorded, so the new control does not become a cue in the M2 test.
