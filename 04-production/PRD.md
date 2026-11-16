# Living PRD

> Module 4 · Production Specs. Refactor for readability. Extract a living PRD that stays true as the build evolves.

## Problem

_What user problem does this solve? Tie to the validated hypothesis._

Product leads investigating a fall in first-project activation need context to choose what to investigate next. A headline alone does not explain the change or justify an intervention. Earlier feedback challenged the proposed starter-template nudge and asked for audience and campaign context.

[Metric Moment Compass](https://metric-moment-compass.anajuana.chatgpt.site/) connects headline → supporting evidence → campaign drill-down → investigation note. This PRD was updated November 15, 2026, after the Lab 2 refactor and Supabase connection. The original Lab 1 findings remain as historical context.

**Hypothesis:** One headline metric, a plain-language takeaway, and accessible supporting context will help a product lead choose and explain a next investigation without spreadsheet export or coaching. The [validation brief](../02-validation/validation-brief.md) defines success: after a three-minute unaided walkthrough, a new reviewer can name an investigation, connect the headline and at least one related signal to it, and identify a relevant unknown. The three-minute window comes from the course's silent walkthrough.

**Validation status:** Not yet validated. Prior feedback informed the build. Successful form submissions and functional checks do not establish independent reasoning. If any of the three criteria fails in the next unaided test, revise that step and retest before expanding scope. Production adoption, reduced spreadsheet use, and improved activation have not been measured. Production readiness remains unproven.

## Users & jobs

- **Primary user:** A product lead reviewing a decline in first-project activation before deciding what to investigate or change.
- **Job to be done:** When activation falls, compare its trend, acquisition mix, and relevant campaigns. Record a defensible next investigation, supporting evidence, and remaining uncertainty without spreadsheet export or coaching.

## Scope

- **In:** A responsive, publicly accessible prototype with an activation overview, four/eight-week trend drawer, channel comparison and filter, campaign comparison/detail, observation collection, one browser-local investigation note and draft, research context, and the preserved Module 1 experience. Supabase stores the illustrative metrics. Auth is enabled, and an owner-protected note schema exists for future integration.
- **Out (explicitly):** Live analytics ingestion, arbitrary date ranges, application sign-in, account-backed, shared or cross-device notes, note history, exports, campaign management, automated diagnosis, AI inference, notifications, file uploads, and experiment execution. Cost, retention, release/error history, and template-use data are absent. Those investigation topics have no corresponding analysis screens.

**Screen map and flow**

| Screen or state | Entry and behavior |
|---|---|
| Activation overview `/` | View the headline and takeaway, open the trend drawer or channel comparison, filter channels, select supporting signals, and write, edit, save, or clear an investigation note. |
| Activation trend drawer | Opens from the headline or View trend. Four/eight-week selection changes the drawer's chart and aggregate only. |
| Campaign comparison `/campaigns/` | Opens from Paid acquisition or the sidebar. Compare Search and Social, add an observation, or open a campaign. |
| Campaign detail `/campaigns/:id/` | Search/Social rates, signup mix, exact counts, and unknowns. Links return to campaigns or the note. Loading, empty, error, and unknown-ID states are distinct. |
| Research context `/research/` | Three supplied user quotes and four course dashboard-use metrics, separate from activation data. Links return to Overview. |
| Preserved prototype `/module-1/` | Earlier activation screen with the shared trend drawer and expandable proposed starter-template test. The proposal does not send anything or run an experiment. |

Shared navigation links to Overview, Campaigns, the investigation note, Research context, and the original prototype. An unmatched route opens Page not found with a home link.

## Requirements

| # | Requirement | Priority | Acceptance criteria |
|---|---|---|---|
| 1 | Explain the activation change | Must | Overview shows 38% (304/800) versus 42% (336/800), down 4 percentage points. It defines activation as completing a first project within seven days and labels the data illustrative. |
| 2 | Explore the activation trend | Must | Selecting Last 4 weeks shows 304/800 = 38%. Last 8 weeks shows 640/1,600 = 40%. Weekly points and tooltip counts update. Closing the drawer returns to the underlying screen. |
| 3 | Compare channel performance and mix | Must | Opening the comparison reveals activation rates, signup shares, exact counts, and supporting-signal checkboxes. All channels, Direct & organic, and Paid acquisition filters change the displayed rows. Share denominators remain all 800 signups in each period. The text distinguishes arithmetic from an unknown cause. |
| 4 | Follow campaign evidence | Must | Paid acquisition opens Campaign comparison. Search and Social open matching detail records, including on direct entry. Both screens use the same active dataset. The comparison total pools campaign counts, and detail signup shares use the summed paid-signup denominators. No weekly campaign trend is invented. |
| 5 | Handle loading, empty, and error states | Must | Loading replaces rows with a skeleton. A valid empty campaign collection shows “No campaigns are available for this period.” In hosted mode, empty campaigns are valid only when they reconcile with paid-channel totals. Request/JSON/schema/reconciliation failure shows “We couldn't load campaign data. Try again.” with Retry and no stale rows. Retry reloads the selected data source on the same route. |
| 6 | Separate missing records from failures | Must | After a valid response, an unknown campaign displays “Campaign not found.” with Back to campaigns. An unrelated unknown route displays Page not found with Go home. The root error boundary offers Try again and Go home. |
| 7 | Collect campaign observations | Must | Add observation stores campaign rates, completion/signup counts, signup-share percentages, period labels, and a source link. Adding the same campaign/period twice creates one item. The editor can remove an item. Successful writes update the confirmation. |
| 8 | Record the reader's reasoning | Must | Investigation selection, rationale, and unknown must be nonblank. Choosing a custom investigation also requires its title. Invalid save focuses the first invalid field. Evidence selection is optional. Saving does not grade reasoning or verify that it uses the headline and a supporting signal. |
| 9 | Preserve drafts and saved evidence | Must | Edits persist as a separate draft and restore after navigation/refresh when storage works. Save captures the current observation collection in the note. Cancel restores saved reasoning and its evidence snapshot. It does not undo changes to the separate working collection. Clear note removes the note and draft, leaving collected observations. |
| 10 | Report storage limits honestly | Must | Failed storage writes do not claim persistence. Note writing can continue on the current page with a loss-on-refresh warning. Invalid stored content produces a recovery message. If the collection cannot be read during save, the prior snapshot is retained and the limitation is reported. |
| 11 | Keep research provenance accessible | Should | Research context shows all three course quotes and the 60% bounce, 12 charts, 6 clicks, and 74% export baselines. These are identified as scenario inputs, not results measured by the prototype. |
| 12 | Preserve the comparison experience | Should | The original prototype remains accessible. Its proposed test is expandable and marked unexecuted. Desktop and mobile layouts retain visible labels and paired previous/current figures. |

Must requirements support the core investigation or protect its correctness. Should requirements support context and comparison. These priorities describe prototype behavior, not production readiness.

## Data & events

_What gets stored, what gets tracked._

**Technical reality:** React and TanStack routing run as a static site hosted through Sites. With hosted settings, one provider loads and validates the complete sample dataset from Supabase PostgreSQL before rendering. Request or validation failure shows an error and Retry without substituting local data. Omitting both Supabase settings selects bundled fixtures, including `/data/campaigns.json`. Both modes use illustrative metrics. Email Auth is enabled with confirmation. Storage is provisioned and unused. Notes remain browser-local because the app has no sign-in UI or remote note adapter. Prompts are development artifacts. No model runs inside the dashboard.

**Data sources and business rules**

- `src/features/activation/activation-dataset.ts`: reads hosted `sample-v1` metadata, cohorts, channels, and campaigns from `dataset_versions`, `activation_cohorts`, `acquisition_channels`, and `campaigns`. It validates metadata, counts, duplicate IDs/weeks, and cohort → channel → campaign reconciliation. `ActivationDatasetContext.tsx` shares the dataset and Retry across active screens. The migration and seed are in `supabase/migrations/202611150001_core.sql`.
- `src/features/activation/activation-sample.ts` and `channel-data.ts`: bundled cohorts and channels used when hosted settings are omitted. Each of the eight sample cohorts has 200 eligible signups and a completed seven-day observation window. The preserved `/module-1/` screen uses this bundled sample.
- `src/features/activation/supporting-signals.ts`: supporting-signal labels derived from the active cohorts and channels. Investigation choices live in `src/features/investigation/investigation-options.ts`.
- `src/features/research/research-context-data.ts`: course quotes and dashboard-use baselines, separate from first-project activation data.
- `public/data/campaigns.json`: fixture-mode campaign `id`, `name`, and previous/current `{eligible, activated}`. `src/features/campaigns/campaign-data.ts` rejects invalid/duplicate IDs, blank names, negative or noninteger counts, and completions above eligible signups.

| Sample segment | Previous 4 weeks: completed / eligible | Last 4 weeks: completed / eligible |
|---|---|---|
| Overall | 336/800 = 42% | 304/800 = 38% |
| Direct & organic | 240/480 = 50% | 160/320 = 50% |
| Paid acquisition | 96/320 = 30% | 144/480 = 30% |
| Search, within paid | 80/200 = 40% | 96/240 = 40% |
| Social, within paid | 16/120 = 13.3% | 48/240 = 20% |

Rates divide completions by eligible signups. Paid's share of all signups changes from 40% to 60%. Within paid, Search's share changes from 62.5% to 50% and Social's from 37.5% to 50%. Combined campaign rates use pooled counts, not averages of row percentages. A zero denominator displays “—” for campaigns and 0 in overview/trend helpers. Resolve this inconsistency before introducing real data. Periods use relative labels without calendar dates, attribution history, or freshness metadata.

**Browser-local storage**

| Storage key | Contents and behavior |
|---|---|
| `activation-investigation-note-v1` | One saved note: investigation ID, custom title, rationale, unknown, selected evidence IDs, and optional observation snapshots. A later save replaces it. |
| `activation-investigation-draft-v1` | The same note shape for unfinished edits. A valid draft takes precedence on restore. Save and Cancel attempt to clear it. |
| `activation-observations-v1` | A separate working collection. Each observation has `id`, `title`, `summary`, `detail`, `href`, and `periodLabel`. IDs deduplicate a campaign and the fixed comparison periods. |

Snapshots include campaign completion/signup counts and displayed rate/share percentages, but omit the paid-share denominator totals. Browser-local records have no user ID, timestamp, or dataset version. The unused `investigation_notes` database contract includes those fields and owner-based access rules. Local notes have no remote sync, multi-note history, or account separation. Other users of the same browser profile can access them, and clearing browser storage removes them.

**Events and measurement:** `activation-observations-changed` and the browser's `storage` event refresh the working collection. `hashchange` opens supporting evidence. No workflow events or success metrics are sent to an analytics service. The three-minute test requires manual observation and assessment.

Conditional Lovable error-reporting hooks remain in the source. Neither hook was present in the Lab 1 public-page inspection, so production monitoring remains unverified. The opt-in `?demo=loading`, `?demo=empty`, and `?demo=error` URLs force labeled campaign states. Fixture-mode previews skip the campaign request. In hosted mode, the shared provider may still fetch context. `?demo=success` and normal navigation use the selected data source. Retry removes the forced mode and reloads that source.

## Open questions

**Look under the hood: historical Lab 1 findings**

These findings describe the pre-refactor build preserved in the [Lab 1 PRD snapshot](https://github.com/antje/product-school-vibe-coding/blob/b02576c470ad7e66395e6e3993c80700dcf66cd2/04-production/PRD.md).

- **Naming:** `CampaignComparison`, `CampaignDetail`, `ResearchContext`, and `useCampaignData` described their roles. `ValidationDashboard` and `validation-data.ts` reflected earlier course terminology. Routes lived in `src/routes`, not `src/pages`.
- **Separation:** Campaign fetching, schema validation/calculation, and observation persistence were separate from display. `ValidationDashboard.tsx` still mixed note validation, storage, form behavior, and rendering. Fixtures spanned three files, so replacing sample data required changes in more than one place.
- **Documentation:** The app README covered setup, tests, builds, sample data, and hosting, but described the Module 2 build and only two prerendered routes. It omitted the campaign/research flow, storage contract, and recovery behavior needed for an engineering handoff.

**Lab 2 resolution:** Screens are grouped by feature. Note validation, browser persistence, transitions, and rendering are separate. The app README covers current routes, setup, and storage behavior. Supabase sample reads and rollback-only database checks passed, including grants, constraints, and two-user row isolation. Application sign-in and remote note saving remain unfinished. The [engineering handoff](handoff-note.md) covers the current source map, verification, and next task.

**Decisions before production**

1. **Product:** Does the revised flow pass all three unaided reasoning criteria with representative product leads? Supporting text explains the sample's audience-mix arithmetic, so a correct answer may reflect those cues. Repeat the test before declaring the hypothesis validated or approving production hardening.
2. **Product and data engineering:** What real source, attribution rules, calendar boundaries, timezone, cohort-maturity policy, and refresh cadence replace the fixtures? Who owns reconciliation and a consistent missing/zero-data rule?
3. **Product and engineering:** Should notes remain personal to one browser, or use the owner-protected Supabase note table? Before connecting accounts, decide retention and explicit import of existing local notes. Sharing, history, and export remain separate scope decisions.
4. **Product and analytics:** Which events and manual rubric will measure a defensible investigation? A production baseline, target, and measurement period remain undefined. Current course metrics are not production targets.
5. **Engineering:** What error monitoring, data provenance, versioned evidence snapshots, and conflict handling are needed once data or users become real? The current collection sync does not provide collaborative note editing.
6. **Engineering, next task:** Start with `src/features/investigation/investigation-note-storage.ts`, `useInvestigationNote.ts`, and `supabase/README.md` to add sign-in and an owner-scoped note adapter. Preserve drafts and saved snapshots, make local-note import explicit, and verify two separate authenticated sessions plus Auth redirect/email behavior before claiming cross-device persistence.
