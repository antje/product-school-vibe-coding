# Validation Brief

> Module 2 · Validation. Frame the riskiest assumption, then build to test it.

**Status:** Published November 5, 2026. Review feedback and the decision to iterate are recorded in [show-and-swap-notes.md](show-and-swap-notes.md). The hypothesis remains unvalidated.

## Scenario

**Scenario 04: The Dashboard Nobody Reads.** A product lead sees first-project activation declining and needs to decide what to investigate before choosing an intervention.

The lesson's **Problem Framework** defines the scope:

- **Goal:** Help the reader choose and explain a next investigation.
- **Problem:** Module 1 placed an action beside a metric without enough evidence to judge their connection.
- **Context:** A product lead reviewing an activation decline before committing to a response.
- **Constraints:** One headline → one supporting comparison → one investigation note. No live analytics, automated intervention, or full-dashboard expansion.
- **Success:** The three observable criteria below, without coaching or spreadsheet export.
- **Explore:** Does supporting context enable reasoning, or does the reader still need another tool or person?

## Riskiest assumption

A focused headline and accessible supporting context will let a product lead choose a defensible next investigation without spreadsheet export or explanation from someone else.

I previously narrowed too quickly to a starter-template nudge. Module 1 peers questioned why it followed from the metric and wanted audience context and related signals. This test examines whether the dashboard supports that reasoning; it does not test the nudge's effectiveness. See [Module 1 feedback](../01-velocity/prototype-v2.md).

## Hypothesis

> We believe **a first screen with one headline metric, a plain-language takeaway, and a clear path to supporting context** will help **product leads investigating a drop in first-project activation** **choose and explain a sensible next investigation without spreadsheet export or help**. The first usability test passes when **a new peer, after a three-minute unaided walkthrough, names an investigation, supports it with the headline and at least one related signal, and identifies what remains unknown**.

Three minutes comes from the lab's silent walkthrough. The evidence and uncertainty requirements address the specific reasoning gap in Module 1. These are provisional formative criteria, not an adoption benchmark. One peer cannot establish a representative success rate.

## Risk type

- [ ] Value (do they want it?)
- [x] Usability (can they use it?)
- [ ] Feasibility (can we build it?)
- [ ] Viability (should we?)

The clickable prototype tests whether a person can use the context to reason about a next step. Whether they return to the dashboard is a later value question.

## Kill switch

At the November 5, 2026 Module 2 peer swap, **I will stop advancing this version if any criterion below is missing** after the three-minute unaided walkthrough. **All three must pass**, without coaching or spreadsheet export.

| Criterion | Observable evidence required |
| --- | --- |
| Choose an investigation | Name a specific question or check consistent with the displayed evidence. Selecting a menu option alone is insufficient. |
| Explain the evidence | Connect the activation headline and at least one related signal to the investigation in their own words. Ticking boxes or repeating labels alone is insufficient. |
| Identify uncertainty | Name a relevant fact the dashboard cannot establish, without treating a possible cause as proven. |

A different investigation can pass if the peer explains its connection to the evidence and missing information. There is no required audience-mix answer. Saving a note is optional, not another timed criterion.

**Consequence:** Revise the failed step's information hierarchy, context, or navigation before adding features, then test with a fresh peer. If information is absent, revise the data requirements. A failure challenges this version; it does not disprove the entire dashboard concept.

**Blind Show and Swap protocol:**

1. Use a new peer and share only the URL. Give no hypothesis, task explanation, rubric, suggested answer, or verbal setup. Use a clean browser session if sharing a device so no earlier saved note is visible.
2. Start when the page is usable. Observe three silent minutes. Record discovery of supporting context, confusion, and requests for help/export. Do not rescue the flow or restart because they struggle.
3. Immediately afterward, preserve any note and ask neutrally: “What would you investigate next, and why? What can you not tell from this dashboard?” Record their explanation before teaching or pointing to content. Score each criterion; verbal reasoning is sufficient.
4. Ask the lab's three credibility questions in [show-and-swap-notes.md](show-and-swap-notes.md). Discuss the intended hypothesis afterward. Coached follow-up is separate from the unaided result.

An exposed prior answer or rubric invalidates the cold read and requires a fresh peer. Needing help during a correctly set up run is a usability failure.

## The three ingredients

### Real data (domain metrics): course scenario context

These are course-provided case baselines, not measurements from our prototype:

| Metric | Baseline | Design implication |
| --- | --- | --- |
| Dashboard bounce | 60% of sessions under 15 seconds with no interaction | Make the first screen's purpose apparent. |
| Default-view charts | 12 | Prioritize one headline. |
| Access to the most-requested metric | 6 clicks | Make supporting context directly accessible. |
| Spreadsheet export | 74% of users export to analyze | Support reasoning within the dashboard. |

The prototype's 38% activation rate and channel comparison are illustrative analytics inside the dashboard. They measure something different from dashboard bounce; their counts and arithmetic appear in [prototype-v3.md](prototype-v3.md).

### User voice (verbatim quotes)

- **Marketing manager:** “I open it, see twelve charts, and have no idea which one I'm supposed to act on. So I close it.”
- **Growth analyst:** “The number I need is in there, but it takes six clicks and three filters to find it.”
- **Product lead:** “It tells me *what* happened but never *what to do about it*. I still export to a spreadsheet to think.”

These quotes come from the course's Context Data Pack, not interviews I conducted.

### Hypothesis

Defined above. The [build prompt](context-injected-build-prompt.md) carries the selected quotes, metrics, and hypothesis into the prototype.

## Build scope and next step

**Validation Lens Loop:** Hypothesis and constraints defined → clickable build complete → feedback captured → revise and retest. The feedback exposed answer cues that weaken the assessment of independent reasoning.

The [published v3](prototype-v3.md) implements headline → acquisition-channel comparison → investigation note. Funnel analysis, product errors, and template history remain possible later investigations, not additional screens or invented evidence. M1 remains available for comparison.

Next, revise the note’s premature evidence cues and repeat the cold read. Keep the three criteria fixed and record the explanation before coaching. A pass supports testing with representative product leads and their data. It does not establish reduced bounce, less spreadsheet use at work, improved activation, or a proven cause.
