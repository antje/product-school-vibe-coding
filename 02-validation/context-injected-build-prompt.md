# Context-injected build prompt

Module 2 · Metric Moment Compass · November 5, 2026.

## Prompt

Build a high-fidelity, clickable prototype for The Dashboard Nobody Reads that tests one hypothesis, not just a nicer-looking screen.

Hypothesis: we believe a first screen with one headline metric, a plain-language takeaway, and a clear path to relevant supporting context will cause users to choose and explain a sensible next investigation without exporting to a spreadsheet or needing help for product leads investigating a drop in first-project activation. We'll know we're right when after a three-minute unaided walkthrough, a new peer can name a next investigation, support it with the headline and at least one related signal, and identify what remains unknown.

Ground it in real context. Put these ON SCREEN as real content, not placeholders:

User voice:
- “The number I need is in there, but it takes six clicks and three filters to find it.”, Growth analyst
- “I open it, see twelve charts, and have no idea which one I'm supposed to act on. So I close it.”, Marketing manager
- “It tells me *what* happened but never *what to do about it*. I still export to a spreadsheet to think.”, Product lead

Metrics to surface:
- 60%, Bounce rate: sessions under 15s with no interaction.
- 12, Charts on the default landing view.
- 6 clicks, To reach the most-requested metric.
- 74%, Users who export to a spreadsheet to actually analyse.

Match a clean, credible visual reference (I'll attach a screenshot, copy the pattern, not the brand). Build only the core screens that would prove or break the hypothesis.

## Design context

- **Visual reference:** The existing blue-and-white Module 1 dashboard.
- **Scenario inputs:** The quotes and four dashboard-use metrics come from the course Context Data Pack.
- **Analysis data:** The activation cohorts and acquisition-channel comparison are illustrative. Their purpose is to support the investigation task; they do not establish a real-world cause.
- **Test design:** The reader supplies their own reasoning and uncertainty.

## Next iteration

Proposed additions to the build prompt, using the risk and kill switch from the [validation brief](validation-brief.md). These have not yet been applied to the published build:

> **Risk type:** Usability. Test whether a product lead can reason from the available context to a defensible next investigation.
>
> **Kill switch:** After a three-minute unaided cold read, stop advancing this version if the peer cannot name an investigation, explain it using the activation headline and at least one related signal, and identify a relevant unknown. All three are required without coaching or export. Fix the failed step before adding capability.
>
> **Constraints:** Keep the headline → supporting comparison → investigation-note flow. Keep the peer's reasoning fields blank and avoid prescribing the answer. Selecting an option or saving a form must not be treated as validation. Preserve the separation between course context, illustrative analytics, and observed peer evidence.
>
> **Reference and output:** Use the existing Module 1 dashboard's visual pattern. Make only the change supported by the peer read, preserve the comparison build, and return a clickable flow that lets the same criteria be tested again.

The next change is to remove premature answer cues from the investigation note and retest the reader's explanation. See the [feedback and decision](show-and-swap-notes.md).
