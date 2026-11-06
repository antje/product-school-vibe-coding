# Context-injected build prompt

Module 2, November 5, 2026. User-supplied prompt executed in Codex against Metric Moment Compass and published through Sites.

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

## Execution notes

- No new visual reference was attached with this prompt. The existing blue-and-white Module 1 dashboard supplies the visual pattern.
- The quotes and four dashboard-use metrics are course-provided scenario context, not research or telemetry collected from this prototype.
- The existing activation cohorts and the added acquisition-channel comparison are illustrative data. They support a usability task and do not establish a real-world cause or an effective intervention.
- The peer's rationale and remaining uncertainty must be entered by the peer, rather than generated as a passing test answer.
- A working interface does not establish that the hypothesis passed. Record the actual peer observation separately.

## Refinement recorded November 5, 2026, before peer testing

The original prompt above includes the hypothesis, success signal, quotes, and metrics, but omits an explicit risk type and kill switch. They were present in the validation brief. This is a gap in transferring the framing into the prompt; the original is preserved as executed.

The following addendum is prepared for a subsequent iteration. It has not been run as a separate build:

> **Risk type:** Usability. Test whether a product lead can reason from the available context to a defensible next investigation.
>
> **Kill switch:** After a three-minute unaided cold read, stop advancing this version if the peer cannot name an investigation, explain it using the activation headline and at least one related signal, and identify a relevant unknown. All three are required without coaching or export. Fix the failed step before adding capability.
>
> **Constraints:** Keep the headline → supporting comparison → investigation-note flow. Keep the peer's reasoning fields blank and avoid prescribing the answer. Selecting an option or saving a form must not be treated as validation. Preserve the separation between course context, illustrative analytics, and observed peer evidence.
>
> **Reference and output:** Use the existing Module 1 dashboard's visual pattern. Make only the change supported by the peer read, preserve the comparison build, and return a clickable flow that lets the same criteria be tested again.

No new build is needed just to restate these constraints. The next change must follow observed peer evidence. The [validation brief](validation-brief.md) is the canonical test protocol.
