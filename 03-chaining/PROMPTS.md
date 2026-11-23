# PROMPTS.md: Living Prompt Pack

> Module 3 · Prompt Chaining. Re-architect the build with prompt chains; capture the reusable ones here.

**Status:** Executed November 10, 2026. Expand and Behavior implemented; Refine completed with a verified no-change result.

## How to use this pack

Run Expand → Behavior → Refine, one prompt at a time. Review each plan and verify its output before running the next prompt. Expand applies **Sequential Logic**, Behavior uses **Constraint Grounding**, and Refine uses a **Reflection Prompt** to decide whether a change is justified.

Use the existing Metric Moment Compass M2 build. Attach the [M2 supporting-evidence screenshot](../02-validation/assets/prototype-v3-supporting-evidence.png) for Steps 1 and 3. Keep the [M2 overview](../02-validation/assets/prototype-v3-overview.png) available as a second reference. These are the visual references named in the prompts.

The prompts are filled in for this project. When reusing the chain, replace these inputs consistently:

| Reusable input | This project's value |
| --- | --- |
| `{{screen A}}` | Campaign comparison |
| `{{screen B}}` | Campaign detail |
| `{{list}}` | Paid-acquisition campaign list |
| `{{reference}}` | Attached M2 supporting-evidence screenshot |
| `{{element}}` | Campaign detail page-heading block |
| `{{data}}` | The illustrative campaign rows specified in Step 1 |

## Prompt chain: Activation investigation drill-down

### Step 1: Expand: add the two missing screens

```text
Extend Metric Moment Compass for a product lead investigating first-project activation. Work in this order and keep the existing overview, trend drawer, browser-local notes, and M1 comparison working.

First, correct the M2 flow: keep reasoning and uncertainty fields blank, and show the prewritten evidence facts only inside the supporting-evidence section after it is opened. Do not supply an investigation answer in the note form.

1. Add "Campaign comparison" at /campaigns. Link to it from the paid-acquisition row in the existing channel comparison. Show the two paid campaigns below across the same Previous 4 weeks and Last 4 weeks periods.
2. Add "Campaign detail" at /campaigns/:id. Clicking a campaign opens its detail using the same record and counts. Show signup counts, first-project completions, calculated activation rates, and the change in percentage points. Back returns to Campaign comparison; a clear link returns to the overview's investigation note. An unknown campaign has a not-found message and a way back.
3. Match both screens to the attached M2 supporting-evidence screenshot: existing typography, blue accents, table density, borders, and spacing.

Use exactly these new illustrative rows, stored in one bundled JSON fixture:
- search, "Search": previous signups 200, completions 80; current signups 240, completions 96.
- social, "Social": previous signups 120, completions 16; current signups 240, completions 48.

The fixture must reconcile to paid's existing totals: previous 320 signups/96 completions; current 480 signups/144 completions. Calculate rates from counts, never average row percentages. For zero eligible signups display "—", not 0%. Both periods use completed seven-day observation windows. Retain the existing period labels; do not invent calendar dates.

Label the new data illustrative. Do not invent costs, retention, causal conclusions, or automatic recommendations. Keep authentication, backend integrations, exports, and experiment execution out of scope.

Return the two screen URLs and check the overview → comparison → detail → back path. Report whether all counts reconcile. Stop before adding the loading/empty/error behavior in Step 2.
```

**Expects in:** Existing M2 build, the attached visual reference, and the exact sample rows above.

**Produces out:** Two linked screens, one shared fixture, and the corrected evidence-before-reasoning sequence. The working flow becomes the input to Step 2.

**Execution result:** Completed. The paid-acquisition row opens [Campaign comparison](https://metric-moment-compass.anajuana.chatgpt.site/campaigns/). Search and Social open their own detail screens, including [Social detail](https://metric-moment-compass.anajuana.chatgpt.site/campaigns/social/). Both Back paths work; returning to the overview reopens supporting evidence. The initial note form no longer exposes the evidence answers, and reasoning and uncertainty remain blank until entered.

| Campaign | Previous completions / signups | Last completions / signups | Activation change |
| --- | --- | --- | --- |
| Search | 80 / 200 = 40% | 96 / 240 = 40% | 0 pp |
| Social | 16 / 120 = 13.3% | 48 / 240 = 20% | +6.7 pp |
| All paid campaigns | 96 / 320 = 30% | 144 / 480 = 30% | 0 pp |

Totals reconcile to the existing paid-acquisition channel. Combined rates are calculated from summed counts. The displayed campaign rates are rounded to one decimal place where needed.

**Screenshots:** [Comparison](assets/campaign-comparison.png) · [Detail](assets/campaign-detail.png) · [Mobile comparison](assets/campaign-comparison-mobile.png) · [Mobile detail](assets/campaign-detail-mobile.png).

### Step 2: Behavior: handle loading, empty and error states

```text
Use the Campaign comparison and Campaign detail produced by Step 1. Harden the campaign-list loading flow without changing the fixture counts, calculations, visual system, or navigation.

Load the same bundled campaign JSON asynchronously from a same-origin static asset. This is a sample-data request, not a live analytics integration. Do not add a backend. Detail must use the same data source and remain usable when opened directly.

Define these states:
- Loading: replace campaign rows with a table skeleton and show "Loading campaigns…". Keep the heading and Back navigation usable.
- Success: show the list and enable the existing campaign links.
- Empty: after a successful request with no records, show "No campaigns are available for this period." Do not render an empty chart or fabricated zero totals.
- Error: on a failed request or invalid data, show "We couldn't load campaign data. Try again." with a Retry button. Hide stale rows. Retry returns to loading and restores the list on success.

Preserve the current page on failure. A valid response with an unknown campaign ID shows "Campaign not found." with a Back to campaigns action; it is not a network failure. Preserve the overview's existing form validation and storage-error handling.

Make the states testable through documented, opt-in demo URLs for loading, empty, error, and success. Normal navigation must use the real static-asset request. Demo modes must be visibly labeled and must not appear as controls in the normal walkthrough. In forced-error mode, Retry must clear the forced error and attempt the normal request.

Verify a loading skeleton, empty response, request failure, Retry recovery, direct campaign-detail access, and an unknown ID. Also block the campaign-data request to test a real fetch failure; do not count a forced demo error as that check. Report actual results and stop before visual refinement.
```

**Expects in:** Step 1's connected screens and shared fixture.

**Produces out:** A campaign list with explicit state transitions, a working recovery path, and documented ways to trigger each state. The stable detail screen becomes the input to Step 3.

**Execution result:** Completed. Both screens request the same bundled sample data. Loading keeps navigation usable; empty responses show no fabricated totals; failed requests and invalid data show the specified message and Retry. Unknown campaign IDs have a separate not-found state and Back link.

| Check | How to reproduce | Observed result |
| --- | --- | --- |
| Loading | [Loading preview](https://metric-moment-compass.anajuana.chatgpt.site/campaigns/?demo=loading) | Skeleton rows and “Loading campaigns…”; heading and Back remain visible. |
| Empty | [Empty preview](https://metric-moment-compass.anajuana.chatgpt.site/campaigns/?demo=empty) | Exact empty message; no campaign rows or zero totals. |
| Error and recovery | [Error preview](https://metric-moment-compass.anajuana.chatgpt.site/campaigns/?demo=error), then Retry | Retry clears the preview mode, requests the sample asset, and restores the list on the same page. |
| Success | [Success preview](https://metric-moment-compass.anajuana.chatgpt.site/campaigns/?demo=success) | The actual sample request supplies both campaigns and their combined totals. |
| Direct detail | Open [Search](https://metric-moment-compass.anajuana.chatgpt.site/campaigns/search/) or [Social](https://metric-moment-compass.anajuana.chatgpt.site/campaigns/social/) in a fresh page | Details load independently of the comparison page. |
| Unknown ID | Open [an unknown campaign](https://metric-moment-compass.anajuana.chatgpt.site/campaigns/missing) | “Campaign not found.” with Back to campaigns. |
| Actual request failure | Temporarily remove the sample asset from the local built site, then restore it and click Retry | The request returned HTTP 404 and showed the recovery state. Retry made a new request, received HTTP 200, and restored the rows. |

Preview URLs are explicitly labeled on screen. Normal navigation does not force a preview state. Automated checks also cover valid empty responses, malformed data, missing denominators, and browser-note validation and persistence.

**Screenshots:** [Loading](assets/campaign-loading.png) · [Empty](assets/campaign-empty.png) · [Error preview](assets/campaign-error.png) · [Actual request failure](assets/campaign-request-failure.png).

### Step 3: Refine: polish one thing on one screen

```text
Audit only the Campaign detail page-heading block against the attached M2 supporting-evidence screenshot.

1. List up to three observed differences in heading typography and spacing. If fewer exist, report fewer; do not invent defects.
2. Fix the most important difference by adjusting only this heading block's font size, weight, line height, or surrounding spacing to match the existing dashboard style.

Keep the title text, data, calculations, routes, controls, and loading/empty/error behavior unchanged. Do not restyle shared components or other screens. If the heading already matches, report that and make no unnecessary change.

Return before/after screenshots of that block and name the exact styling change. Recheck navigation and the Step 2 states to confirm they still work.
```

**Expects in:** The stable detail screen from Step 2 and the attached M2 reference screenshot.

**Produces out:** One scoped visual refinement, or a documented no-change result, with evidence that the established flow still works.

**Execution result:** Audited the Campaign detail heading against the M2 reference and retained it unchanged. It already uses the established Inter Tight heading treatment: 24 px, weight 600, 30 px line height on desktop, with the existing 21 px mobile scale. The title, description, and surrounding space remain legible at both sizes. There was no material typography or spacing gap that justified a change.

[Before](assets/campaign-heading-before.png) and [after](assets/campaign-heading-after.png) captures document the no-change result. Navigation and the loading, empty, error, and recovery paths remain intact. Desktop, tablet, and mobile checks found no horizontal overflow.

## Reusable techniques learned

- **Give each step a clear input and output.** Expand established the screens and shared counts. Behavior then added request states to that working flow. Refine evaluated only the finished detail heading.
- **Define constraints that can be checked.** Exact counts, period labels, messages, and a rule for zero denominators made it possible to detect data or behavior drift.
- **Specify failure and recovery together.** An error message alone is incomplete. Retry must clear the forced state, make a new request, and restore the same screen.
- **Test the mechanism as well as the preview.** A labeled error preview makes the state easy to demonstrate. Removing the actual asset proved the normal request path also handles failure.
- **Check direct links as well as clicks.** A working local route does not guarantee a shared URL works on a static host. Both entry paths need verification.
- **Use reflection to decide whether a change is needed.** The heading already matched the visual reference. Keeping it avoided unrelated edits to a stable flow.

## What broke (and the fix)

A separate mega-prompt comparison was not run. The concrete issue found during this chain was direct routing: an unknown campaign URL could reach a blank hosting 404 instead of the app's “Campaign not found.” screen, even though the local router handled it.

The targeted fix was to retain prerendered pages for the known routes and add a static fallback that starts the app for unmatched URLs. The unknown-ID screen then loads the shared data, reports that the campaign is missing, and provides a Back path. This required no analytics backend. Retesting covered direct entry and the normal comparison → detail → back flow.

The return link also needed to reopen the overview's collapsed evidence section. Handling that arrival explicitly preserves the investigation path. Separating expansion, behavior, and refinement made these navigation issues visible before considering visual changes.

## Prompt cold-read feedback

Peer prompt cold-read feedback has not been recorded. The build checks above document execution, not a peer usability result.
