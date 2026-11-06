# Show & Swap Notes

> Module 2 · Validation. Put the prototype in front of a peer. Their reaction is the data.

**Review date:** November 5, 2026. **Reviewer:** Codex subagent, given the public URL without the validation brief, source code, or build history.

## What I showed

[Metric Moment Compass, Module 2 v3](https://metric-moment-compass.anajuana.chatgpt.site/): an activation headline, a channel comparison, and a place to record the next investigation.

The reviewer opened a separate browser session with a blank investigation form. It explored the trend drawer, switched from four to eight weeks, opened the channel comparison, filtered to paid acquisition, and saved its own investigation note. The save confirmation and entered content were visible. Edit and Clear appeared but were not tested.

The browser walkthrough took 3 minutes 13 seconds including tool latency. This does not establish the brief's three-minute human task-speed criterion. The observations below concern comprehension, credibility, and the inspected interactions.

## What my partner understood (in their words)

**1. What do you think the core hypothesis or kill switch was?**

> I think the hypothesis was that showing one important metric, a clear comparison, and a place to record the next investigation would help someone move from “activation is down” to a useful question without exporting everything to a spreadsheet. I understood what first-project activation meant immediately, and the acquisition comparison gave me a reason to investigate audience mix.
>
> My inferred kill switch would be users still leaving without a defensible next question—or confidently treating the dashboard’s explanation as proof of the underlying cause. I did not see an explicit success threshold or kill criterion in the product, so that is my interpretation, not something the dashboard stated.

**What they would investigate next:**

> I would investigate which campaigns or audiences drove the increase in paid signups, and whether the change was intentional.
>
> I used the overall decline from 42% to 38%, the unchanged 50% direct/organic and 30% paid activation rates, and paid’s rise from 40% to 60% of signups. I also used the counts: paid activated users rose from 96 to 144, while direct/organic activated users fell from 240 to 160. That matters because “paid has a lower activation rate” is not enough reason to cut paid acquisition. It is bringing in more activated users than before, and I cannot judge their value without cost and retention information.
>
> The dashboard explains how the displayed mixture produces the overall rate. It does not establish why the mixture changed, whether attribution changed, which individual campaigns account for it, or whether errors affect subgroups hidden inside these broad channels. I would also want to know whether the seven-day activation measure predicts later retained value.

**My assessment against the brief:**

| Criterion | Evidence in the response |
| --- | --- |
| Name a next investigation | Identify which campaigns or audiences increased paid signups and whether that change was intentional. |
| Connect headline and related signal | Connect 42% → 38% overall activation to unchanged channel rates, a larger paid share, and the underlying activated-user counts. |
| Identify uncertainty | Name missing campaign detail, attribution changes, subgroup errors, costs, retention, and the relationship between activation and later value. |

All three reasoning elements appear in the response. However, the supplied answer cues described below weaken what this tells me about independent understanding. I am not recording an overall hypothesis pass from this review.

## Where they got confused / pushed back

**2. Where did the experience lose credibility?**

> For me, it lost credibility when the investigation became a worksheet with a fairly visible expected answer. Before I opened the channel comparison, the evidence checklist already said that channel activation rates were unchanged and paid share had increased. Then the comparison explained the conclusion, and the form asked me to repeat supporting observations. That makes the task easy to complete, but it leaves me unsure whether I independently understood the evidence or followed the supplied explanation.
>
> The next limitation was follow-through. I could record a question about audience quality, but the visible workflow ended at a note saved only in this browser. I could not continue into the campaigns or audiences responsible for the change through the controls I explored.
>
> The week labels and perfectly unchanged channel rates also made this feel like a constructed example. The page openly calls the data illustrative, which I appreciate. The separate “Why this dashboard needs to change” section, with course context and quotes about the dashboard, made the experience feel more like a prototype presentation than an everyday analytics workspace.

**3. Did the data make you feel like you were using a real product?**

> Partly. The counts alongside percentages, the seven-day activation definition, and the statement that all cohorts had completed their observation window made the metric more credible. The trend drawer worked, changing from four weeks to eight weeks changed its aggregate from 38% and 304/800 to 40% and 640/1,600, and the channel filter actually changed the table. Saving my note produced a clear confirmation with my reasoning, supporting signals, and unknowns preserved. Those behaviors made it more than a static mockup.
>
> But I would describe it as a working demonstration of a real analytical workflow, rather than evidence that I was looking at an operational product. I had broad channel buckets, generic week numbers, illustrative data, and a local-only note. I did not have the campaign detail, actual calendar periods, costs, retention, or event history I would need to make a business decision.

No broken control was reported in the inspected flow. The limitations were the answer cues, the depth of investigation, and operational realism. The review did not cover mobile, keyboard-only use, persistence after reopening, other investigation choices, or validation errors.

## What I'll change as a result

**The feedback that landed hardest:**

> That makes the task easy to complete, but it leaves me unsure whether I independently understood the evidence or followed the supplied explanation.

**My learning:** Adding context helped the reviewer form a more specific question, but I also supplied much of the interpretation before the evidence was explored. A completed investigation note can therefore overstate how much the reader understood independently.

**My next change:** Revise the investigation-note flow so it does not reveal prewritten evidence answers before the reader opens the supporting comparison. Keep the data accessible and ask for the reader's reasoning in their own words. Then repeat the same cold read and observe whether they can still connect the headline, related signal, and uncertainty. This is a proposed change; the published v3 has not been altered.

**The reviewer's most-wanted product improvement:**

> Let me click **Paid acquisition** and continue into a campaign-level comparison for the same two periods, with signup and activation counts. That would let me pursue the next question the dashboard itself helped me identify.

That is the next data requirement to explore after tightening the test. I would need campaign-level counts and matching calendar periods, with provenance, before presenting that drill-down as evidence. The current broad-channel example cannot supply those facts.

**Decision:** Iterate on the evidence-to-reasoning flow before claiming the hypothesis is validated. Preserve the working trend, channel filter, explicit counts, and uncertainty statements. Do not prioritize the template nudge or cut paid acquisition based on its lower activation rate alone.

For the after-class comparison: [M1 v2 screenshot](../01-velocity/assets/prototype-v2-public.png) · [M2 v3 screenshot](assets/prototype-v3-overview.png). The cohort message has not been sent.
