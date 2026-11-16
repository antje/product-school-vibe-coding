# Engineering Handoff Note

> Module 4 · Production Specs. Open the black box, make the build legible to an engineer.

## What this is

_One paragraph an engineer can read in 60 seconds._

[Metric Moment Compass](https://metric-moment-compass.anajuana.chatgpt.site/) helps a product lead investigate a decline in first-project activation. Users follow the headline into channel and campaign evidence, then record their next investigation and what remains unknown. We have not yet validated whether they can explain that choice without spreadsheet export or coaching. The Module 4 build groups code by feature, separates data access from display, and reads illustrative metrics from Supabase PostgreSQL. Notes save only in the browser. Account sign-in and cloud note saving are unfinished.

## Architecture (plain language)

- **Frontend:** React and TypeScript with TanStack routing, Tailwind, Radix, and Recharts. Sites hosts the prerendered app and browser assets. Route files in `src/routes` point to named screens under `src/features`: `activation`, `campaigns`, `investigation`, `research`, and `original-prototype`. Shared components live in `src/components`. The app README covers routes, setup, and storage behavior.
- **Backend / data:** Supabase project `abmavcuiwevkdlqqgngg` holds `dataset_versions`, `activation_cohorts`, `acquisition_channels`, `campaigns`, and `investigation_notes`. The published client reads the first four tables with a browser-safe publishable key. A shared data provider validates the responses and checks that cohort, channel, and campaign counts reconcile before rendering. It shows a loading state during requests and offers Retry on failure, without silently substituting local data. All five tables have Row Level Security. Public users can read only the designated sample metrics, and authenticated users can access only their own note row. Email Auth requires email confirmation. Storage is available but unused because uploads are outside scope.
- **Key flows:** `/` → channel comparison → `/campaigns/` → `/campaigns/search/` or `/campaigns/social/` → collected observation → `/#investigation-note`. The trend drawer switches between four and eight weeks using the active cohorts. `/research/` holds course quotes and baselines, separate from activation data. `/module-1/` preserves the earlier prototype and bundled sample. Note validation lives in `investigation-note-model.ts`, browser reads and writes in `investigation-note-storage.ts`, state transitions in `useInvestigationNote.ts`, and rendering in the note components. Campaign observation construction, storage, and display are also separate.

## What's solid vs. what's duct tape

| Area | State | Notes |
|---|---|---|
| Naming and organization | solid | Named screens, note validation, storage, state transitions, and views are separated. Existing routes, focus behavior, and browser-storage keys are preserved. |
| Metric data path | solid | PostgreSQL reads return 8 cohorts, 2 channels, and 2 campaigns. The client validates metadata, counts, duplicate IDs, and reconciliation. Overall activation is 336/800 = 42% previously and 304/800 = 38% currently. Eight-week activation is 640/1,600 = 40%. |
| Failure and recovery | solid | Data appears only after validation. Failed requests offer Retry. Missing campaigns, empty results, request failures, and unknown routes have distinct states. Labeled demo states remain available. |
| Browser note lifecycle | solid | Save captures the observation collection. Drafts restore separately. Cancel restores saved reasoning and evidence, while Clear retains the working collection. Failed writes and incomplete draft cleanup show accurate warnings. |
| Hosted access controls | solid | Live SQL checks passed for constraints, read-only metrics, and isolation between two user IDs. All temporary rows were rolled back. These checks verify database policies, not an application sign-in flow. |
| Accounts and cloud notes | rough | The owner-protected notes table exists, but the current app does not write to it. No cross-device sync, account isolation for local notes, collaborative editing, or note history is implemented. |
| Data and measurement | rough | Counts are illustrative, periods are relative, and live analytics ingestion and behavior tracking are absent. Saved evidence lacks a dataset version and timestamp. Selected signal labels use the active dataset. Implementation checks do not establish usability or production readiness. |

**Verification:** All 105 automated tests, TypeScript, and the production build passed. Public Data API reads matched the sample records. Browser checks covered the overview, four/eight-week trends, channel filtering, campaign comparison and detail, evidence collection, and saved-note restoration after refresh. Navigation to a page section now waits for hosted data to load, with regression tests for the fix. The overview fits a 390 px viewport without horizontal overflow. Live SQL checks passed for grants, constraints, user isolation, timestamps, and rollback cleanup. Sites version 6 was published from source commit `89658f01b4d8078b53a79289ceaeec0bfbbd80e9`. Its public overview loaded the hosted dataset correctly.

## Risks & assumptions for the team

1. **Product:** Run the three-minute unaided test from the [validation brief](../02-validation/validation-brief.md). A reader must name an investigation, support it with the headline and at least one related signal, and identify an unknown. Supplied explanations may cue an answer, so working controls alone cannot validate the hypothesis.
2. **Engineering, first task:** Start with `src/features/investigation/investigation-note-storage.ts`, `useInvestigationNote.ts`, and `supabase/README.md`. Add sign-in and a note adapter that saves each user's note to `investigation_notes`. Preserve drafts and saved snapshots, require explicit import of local notes, and test two separate authenticated sessions before claiming cross-device persistence. Check Auth site and redirect URLs, and verify email delivery.
3. **Data:** The current contract supports one fixed eight-week sample with organic and paid channels. Real data needs dated cohorts that have completed the activation window, attribution rules, a timezone, freshness information, and dataset versions. Preserve exact denominators and reconcile all counts. Resolve inconsistent zero-denominator handling: campaign rates show “—”, while overview and trend helpers return 0.
4. **Reliability and operations:** Assign owners and agree on production requirements for availability, monitoring, backup and recovery, and concurrent note edits. The project uses the free tier. The four metric-table reads are validated together but do not share a database snapshot transaction. Public configuration is embedded at build time, so changes require a rebuild. No runtime AI or telemetry service is connected.
5. **Scope:** Keep testing the usability hypothesis. Real acquisition data, costs, retention, release and error history, template-use history, experiment execution, and file uploads remain outside this build.

## How to run it

Get the application source from the Sites project owner. The course repository contains the deliverables only. Run these commands from the application root:

```bash
bun install --frozen-lockfile
cp .env.example .env.local
# For fixture mode, leave both settings blank.
# For the hosted dataset, set the project URL and publishable key in .env.local.
bun run dev --host 127.0.0.1 --port 5173

# In another terminal, from the same application root:
bun run test
bunx tsc --noEmit
bun run build
bun run preview --host 127.0.0.1 --port 4173
```

Set `VITE_SUPABASE_URL=https://abmavcuiwevkdlqqgngg.supabase.co` and copy `VITE_SUPABASE_PUBLISHABLE_KEY` from the project's API Keys settings. Git ignores `.env.local`. Never use a secret or service-role key in a browser setting. Omitting both settings selects fixture mode. Partial or invalid configuration produces an error.

The migration `supabase/migrations/202611150001_core.sql` was applied through the SQL Editor. Do not rerun it against the existing tables. `supabase/verify.sql` checks the database and rolls back every test write. It does not test Auth sign-in. The application README and `docs/module-4.md` contain the source map, prompts, checks, and screenshots. Keep the existing Sites identity in `.openai/hosting.json` when publishing. Sites version 5 preserves the pre-refactor baseline.
