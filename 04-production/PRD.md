# Living PRD

> Module 4 · Production Specs. Refactor for readability; extract a living PRD that stays true as the build evolves.

## Problem

_What user problem does this solve? Tie to the validated hypothesis._

Product leads investigating a fall in first-project activation need enough related context to choose a sensible next investigation. A headline alone does not establish why activation changed or justify an intervention. Earlier feedback challenged the proposed starter-template nudge and asked for audience and campaign context.

[Metric Moment Compass](https://metric-moment-compass.anajuana.chatgpt.site/) supports headline → supporting evidence → campaign drill-down → investigation note. This is a record of the current prototype as of November 15, 2026, before the Lab 2 refactor or backend work.

**Hypothesis:** One headline metric, a plain-language takeaway, and accessible supporting context will help a product lead choose and explain a next investigation without spreadsheet export or coaching. Following the [validation brief](../02-validation/validation-brief.md), success means that after a three-minute unaided walkthrough, a new reviewer can name an investigation, connect the headline and at least one related signal to it, and identify a relevant unknown. The three-minute window comes from the course's silent walkthrough.

**Validation status:** Not yet validated. Prior feedback informed the build, but a successful form submission or functional check is not evidence of independent reasoning. If any of the three criteria fails in the next unaided test, revise that step and retest before expanding scope. Production adoption, reduced spreadsheet use, and improved activation have not been measured. This PRD documents the prototype; it does not establish production readiness.

## Users & jobs

- **Primary user:** A product lead reviewing a decline in first-project activation before deciding what to investigate or change.
- **Job to be done:** When activation falls, compare its trend and acquisition mix, examine relevant campaigns, and record a defensible next investigation with supporting evidence and remaining uncertainty, without exporting to a spreadsheet or needing someone to explain the dashboard.

## Scope

- **In:** A responsive, publicly accessible prototype with an activation overview, four/eight-week trend drawer, channel comparison and filter, campaign comparison/detail, observation collection, one browser-local investigation note and draft, research context, and the preserved Module 1 experience.
- **Out (explicitly):** Live analytics ingestion, arbitrary date ranges, user accounts, authentication, Supabase or another product database, shared/cross-device notes, note history, exports, campaign management, automated diagnosis, AI inference, notifications, and experiment execution. Cost, retention, release/error history, and template-use data are absent. Choosing those investigation topics does not open corresponding analysis screens.

**Screen map and flow**

| Screen or state | Entry and behavior |
|---|---|
| Activation overview `/` | Headline and takeaway; open the trend drawer or channel comparison; filter channels; select supporting signals; write, edit, save, or clear an investigation note. |
| Activation trend drawer | Opens from the headline or View trend. Four/eight-week selection changes the drawer's chart and aggregate only. |
| Campaign comparison `/campaigns/` | Opens from Paid acquisition or the sidebar. Compare Search and Social, add an observation, or open a campaign. |
| Campaign detail `/campaigns/:id/` | Search/Social rates, signup mix, exact counts, and unknowns; links return to campaigns or the note. Loading, empty, error, and unknown-ID states are distinct. |
| Research context `/research/` | Three supplied user quotes and four course dashboard-use metrics, separate from activation data; return to Overview. |
| Preserved prototype `/module-1/` | Earlier activation screen with the shared trend drawer and expandable proposed starter-template test. The proposal does not send anything or run an experiment. |

Shared navigation links to Overview, Campaigns, the investigation note, Research context, and the original prototype. An unmatched application route has a separate Page not found screen with a home link.

## Requirements

| # | Requirement | Priority | Acceptance criteria |
|---|---|---|---|
| 1 | Explain the activation change | Must | Overview shows 38% (304/800) versus 42% (336/800), down 4 percentage points. It defines activation as completing a first project within seven days and labels the data illustrative. |
| 2 | Explore the activation trend | Must | Selecting Last 4 weeks shows 304/800 = 38%; Last 8 weeks shows 640/1,600 = 40%. Weekly points and tooltip counts update. Closing the drawer returns to the underlying screen. |
| 3 | Compare channel performance and mix | Must | Opening the comparison reveals activation rates, signup shares, exact counts, and supporting-signal checkboxes. All channels, Direct & organic, and Paid acquisition filters change the displayed rows; share denominators remain all 800 signups in each period. The text distinguishes arithmetic from an unknown cause. |
| 4 | Follow campaign evidence | Must | Paid acquisition opens Campaign comparison. Search and Social open matching detail records, including on direct entry. Both screens use the same fixture. The comparison total pools campaign counts, and detail signup shares use the summed paid-signup denominators. No weekly campaign trend is invented. |
| 5 | Handle loading, empty, and error states | Must | Loading replaces rows with a skeleton. A valid empty response shows “No campaigns are available for this period.” Request/JSON/schema failure shows “We couldn't load campaign data. Try again.” with Retry and no stale rows. Retry starts a new request on the same route. |
| 6 | Separate missing records from failures | Must | After a valid response, an unknown campaign displays “Campaign not found.” with Back to campaigns. An unrelated unknown route displays Page not found with Go home. The root error boundary offers Try again and Go home. |
| 7 | Collect campaign observations | Must | Add observation stores campaign rates, completion/signup counts, signup-share percentages, period labels, and a source link. Adding the same campaign/period twice creates one item. The editor can remove an item; successful writes update the confirmation. |
| 8 | Record the reader's reasoning | Must | Investigation selection, rationale, and unknown must be nonblank; choosing a custom investigation also requires its title. Invalid save focuses the first invalid field. Evidence selection is optional. Saving does not grade reasoning or verify that it uses the headline and a supporting signal. |
| 9 | Preserve drafts and saved evidence | Must | Edits persist as a separate draft and restore after navigation/refresh when storage works. Save captures the current observation collection in the note. Cancel restores saved reasoning and its evidence snapshot; it does not undo changes to the separate working collection. Clear note removes the note and draft, leaving collected observations. |
| 10 | Report storage limits honestly | Must | Failed storage writes do not claim persistence. Note writing can continue on the current page with a loss-on-refresh warning. Invalid stored content produces a recovery message. If the collection cannot be read during save, the prior snapshot is retained and the limitation is reported. |
| 11 | Keep research provenance accessible | Should | Research context shows all three course quotes and the 60% bounce, 12 charts, 6 clicks, and 74% export baselines. These are identified as scenario inputs, not results measured by the prototype. |
| 12 | Preserve the comparison experience | Should | The original prototype remains accessible. Its proposed test is expandable and marked unexecuted. Desktop and mobile layouts retain visible labels and paired previous/current figures. |

Priorities identify behavior to preserve in the current prototype: Must supports the core investigation or protects its correctness; Should supports context and comparison. They are not claims that a production system exists.

## Data & events

_What gets stored, what gets tracked._

**Technical reality:** React and TanStack routing run as a static site hosted through Sites. Navigation, calculations, filters, form validation, and browser storage work. Campaign screens make a real same-origin HTTP request to `/data/campaigns.json`, but the response is a bundled sample file, not a live analytics API. No product backend, database, account, or auth layer is connected. The prompts used to build the app are development artifacts; no model runs inside the dashboard.

**Data sources and business rules**

- `src/lib/activation-sample.ts`: eight illustrative weekly cohorts, each with `week`, `eligible`, and `activated`; 200 eligible signups per cohort. Every displayed cohort is described as having completed its seven-day observation window.
- `src/lib/validation-data.ts`: channel counts, investigation choices, supporting-signal labels, and course quotes/metrics. The research baselines concern dashboard usage, not first-project activation.
- `public/data/campaigns.json`: campaign `id`, `name`, and previous/current `{eligible, activated}`. The parser rejects invalid/duplicate IDs, blank names, negative or noninteger counts, and completions above eligible signups.

| Sample segment | Previous 4 weeks: completed / eligible | Last 4 weeks: completed / eligible |
|---|---|---|
| Overall | 336/800 = 42% | 304/800 = 38% |
| Direct & organic | 240/480 = 50% | 160/320 = 50% |
| Paid acquisition | 96/320 = 30% | 144/480 = 30% |
| Search, within paid | 80/200 = 40% | 96/240 = 40% |
| Social, within paid | 16/120 = 13.3% | 48/240 = 20% |

Rates use completions divided by eligible signups. Paid's share of all signups changes from 40% to 60%. Within paid, Search's share changes from 62.5% to 50% and Social's from 37.5% to 50%. Campaign combined rates use pooled counts, not averages of row percentages. Campaign zero denominators display “—”; the existing overview/trend helpers return 0 for a zero denominator, an inconsistency to resolve before real data is introduced. Periods use relative labels, with no calendar dates, attribution history, or freshness metadata.

**Browser-local storage**

| Storage key | Contents and behavior |
|---|---|
| `activation-investigation-note-v1` | One saved note: investigation ID, custom title, rationale, unknown, selected evidence IDs, and optional observation snapshots. A later save replaces it. |
| `activation-investigation-draft-v1` | The same note shape for unfinished edits. A valid draft takes precedence on restore. Save and Cancel attempt to clear it. |
| `activation-observations-v1` | A separate working collection. Each observation has `id`, `title`, `summary`, `detail`, `href`, and `periodLabel`. IDs deduplicate a campaign and the fixed comparison periods. |

Snapshots include campaign completion/signup counts and the displayed rate/share percentages, but not the paid-share denominator totals. No record stores a user ID, timestamp, or dataset version. There is no remote sync, multi-note history, or account separation; other users of the same browser profile can access the stored content. Clearing browser storage removes it.

**Events and measurement:** `activation-observations-changed` and the browser's `storage` event refresh the working collection; `hashchange` opens supporting evidence. These are UI events, not product analytics. No workflow events or success metrics are sent to an analytics service. The three-minute test requires manual observation and assessment.

Conditional Lovable error-reporting hooks remain in the source. Both hooks were absent in the inspected public page, so they are not a verified production monitoring service. The opt-in `?demo=loading`, `?demo=empty`, and `?demo=error` URLs force labeled states without fetching; `?demo=success` and normal navigation fetch the fixture. Retry removes the forced mode and attempts the normal request.

## Open questions

**Look under the hood: Lab 1 findings**

- **Naming:** Mostly understandable: `CampaignComparison`, `CampaignDetail`, `ResearchContext`, and `useCampaignData` describe their roles. `ValidationDashboard` and `validation-data.ts` still reflect earlier course terminology. Routes live in `src/routes`, not `src/pages`.
- **Separation:** Partial. Campaign fetching, schema validation/calculation, and observation persistence are separated from display. `ValidationDashboard.tsx` still mixes note validation, storage, form behavior, and rendering. Fixtures span three files, so replacing sample data is not a one-file change.
- **Documentation:** An app README exists with setup, test, build, sample-data, and hosting instructions. It still describes the Module 2 build and only two prerendered routes. It omits the current campaign/research flow, storage contract, and recovery behavior. It helps someone start the app but is incomplete for an engineering handoff.

**Decisions before production**

1. **Product:** Does the revised flow pass all three unaided reasoning criteria with representative product leads? Supporting text still explains the sample's audience-mix arithmetic, so a correct answer alone may reflect answer cues. Repeat the test before declaring the hypothesis validated or approving production hardening.
2. **Product and data engineering:** What real source, attribution rules, calendar boundaries, timezone, cohort-maturity policy, and refresh cadence replace the fixtures? Who owns reconciliation and a consistent missing/zero-data rule?
3. **Product and engineering:** Should notes remain personal to one browser, or support accounts, sharing, history, and export? Decide ownership, access controls, retention, and migration of existing local notes before choosing a backend schema. Supabase is not connected yet.
4. **Product and analytics:** Which events and manual rubric will measure a defensible investigation? A production baseline, target, and measurement period remain undefined; current course metrics are not production targets.
5. **Engineering:** What error monitoring, data provenance, versioned evidence snapshots, and conflict handling are needed once data or users become real? The current collection sync does not provide collaborative note editing.
6. **Engineering, next lab:** Begin with the note lifecycle in `ValidationDashboard.tsx`, separate its persistence/validation from display, and update the app README to match all routes and states. Use the existing behavior checks to preserve the flow. Estimate implementation effort after the real-data and persistence scope is agreed. These are recommendations, not completed Lab 1 changes.
