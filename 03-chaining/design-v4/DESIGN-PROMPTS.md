# Dashboard v4: Design prompts

A design revision of Metric Moment Compass, following the completed Module 3 build.

## Design brief

A calm, precise workspace for investigating activation changes. Make related signals easy to compare, keep the original question visible during drill-down, and let users carry evidence into their own reasoning. Use restrained blue accents, deliberate typography, and compact comparisons.

Keep the existing sample counts, period definitions, routes, trend drawer, loading/empty/error states, and browser-local note workflow. Preserve Module 1. Facts stay distinct from hypotheses. No backend, automatic causal diagnosis, or invented time-series data.

## Baseline

The published Module 3 build is preserved as Sites version 3. Its completed prompt pack and ten screenshots remain in the parent folder. Current overview captures were added before the design revision:

- [Overview](before/overview.png)
- [Supporting evidence](before/supporting-evidence.png)
- [Mobile overview](before/overview-mobile.png)
- [Campaign comparison](../assets/campaign-comparison.png)
- [Campaign detail](../assets/campaign-detail.png)

## Prompt 1: Clarify the overview and supporting evidence

```text
Refine the existing activation overview into a calm analytical workspace. Preserve the blue-and-white identity and Inter Tight typography, all actual sample counts, the existing routes, trend interaction, and note form behavior.

Give the first screen a clear hierarchy: the activation change, its exact counts and periods, then the next comparison. Reduce repeated explanatory copy and excess vertical spacing. Keep sample provenance clear. Keep the supplied research quotes and dashboard-use metrics accessible in the research section.

In the opened channel comparison, show activation rate and signup share as paired previous/current comparisons. Use one directly labeled 0–100% scale, consistent period encoding, and visible numeric values. Keep exact counts beside the rates. Show the evidence only after the supporting comparison is opened. Do not supply the person's investigation rationale.

Keep the note editor readable and give collected evidence a clear place beside the person's reasoning. Make the previous/current pairs consistent on mobile. Improve spacing and typography without adding decorative graphics, unsupported recommendations, or more metrics unrelated to this task.
```

## Prompt 2: Make campaign drill-down explain the relationship

```text
Refine Campaign comparison and Campaign detail using the same calm blue-and-white analytical workspace.

Carry the original question into each drill-down: overall activation 42% → 38%, with paid signup share 40% → 60%. Use concise navigational context rather than repeating the whole overview.

In Campaign comparison, show two measures together for each campaign: activation rate and share of paid signups. Calculate both from the shared fixture and pooled denominators. Search activation is 40% → 40%; Social is 13.3% → 20%. Search's share of paid signups is 62.5% → 50%; Social's is 37.5% → 50%. Paid activation remains 30% in both periods. These are arithmetic observations, not evidence of why the change occurred.

Use aligned, directly labeled paired bars and exact counts. Make campaign names clearly clickable. Include an Add observation action for each campaign, with visible confirmation and a route to the investigation note.

On Campaign detail, make the activation-rate comparison and percentage-point change the visual focus. Put signup mix and exact eligible/completed counts underneath as supporting evidence. Keep both periods side by side on mobile, with consistent positions. Preserve unknowns and the existing loading/empty/error/Retry/not-found states. Avoid invented weekly charts: only two period totals exist at campaign level.
```

## Prompt 3: Connect evidence to the investigation note

```text
Let a reader add a campaign observation to their investigation note without writing their reasoning for them.

Each saved observation must include a stable ID, campaign name, both period labels, activation rates, exact completion/signup counts, share of paid signups, and a source link back to the campaign. Derive the text from the same data shown on screen. Deduplicate repeated additions, show success only after storage succeeds, and provide removal in the note editor.

Keep selected evidence separate from the person's investigation, rationale, and uncertainty. Never fill those fields automatically. Preserve existing saved notes and the previous overview evidence selections. Unsaved writing should survive visiting a campaign and returning. Keep all storage local to the browser and explain the limitation. If storage is unavailable or full, show an honest recoverable message instead of claiming that the observation was saved.

Verify adding from comparison and detail, duplicate prevention, return to the note, removal, refresh persistence, existing-note compatibility, and storage failure. Keep the shared source data and loading states unchanged.
```

## Prompt 4: Review the result independently

```text
Review the current dashboard screenshots against the baseline and the design brief. Evaluate the rendered result without relying on implementation effort or earlier praise.

Check whether the reader can see the important change first, compare activation with signup mix, understand the relationship to the original investigation, and carry an observation into their own note. Inspect desktop and mobile layouts, focus visibility, text contrast, data labels, empty/loading/error states, and the distinction between facts and unknown causes.

Name only material problems, with the specific screen and element, the effect on the user's task, and a focused correction. Do not request decorative novelty or unrelated features. A visual review is not evidence that the usability hypothesis passed.
```
