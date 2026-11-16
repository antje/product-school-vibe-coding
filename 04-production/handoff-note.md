# Engineering Handoff Note

> Module 4 · Production Specs. Open the black box, make the build legible to an engineer.

## What this is

_One paragraph an engineer can read in 60 seconds._

[Metric Moment Compass](https://metric-moment-compass.anajuana.chatgpt.site/) helps a product lead investigate a decline in first-project activation. The flow connects a headline to channel and campaign evidence, then asks the reader to record a next investigation and what remains unknown. The hypothesis is that this supports a defensible decision without spreadsheet export or coaching; it remains unvalidated. The Module 4 build separates features, data access, and display, and reads illustrative metrics from Supabase PostgreSQL. Notes still save only in the browser. Database persistence is real; the figures are sample data, and account sign-in and cloud note saving are unfinished.

## Architecture (plain language)

- **Frontend:** React and TypeScript, using TanStack routing, Tailwind, Radix, and Recharts. Sites publishes the prerendered app and browser assets. Thin files in `src/routes` point to named screens in `src/features/activation`, `campaigns`, `investigation`, `research`, and `original-prototype`. Shared frame/components live in `src/components`. The app README explains the routes, feature map, setup, and persistence contract.
- **Backend / data:** Supabase project `abmavcuiwevkdlqqgngg` holds `dataset_versions`, `activation_cohorts`, `acquisition_channels`, `campaigns`, and `investigation_notes`. The published client uses a browser-safe publishable key to read the first four tables. One shared dataset provider validates and reconciles cohorts → channels → campaigns before rendering. It shows loading/error/Retry instead of silently substituting local data. All tables have Row Level Security. Public access is limited to the designated sample metrics; note policies allow an authenticated user to access only their own row. Email Auth is enabled with email confirmation. Storage is provisioned but unused because uploads are outside scope. The app has no account sign-in UI or remote note adapter yet.
- **Key flows:** `/` → channel comparison → `/campaigns/` → `/campaigns/search/` or `/campaigns/social/` → collected observation → `/#investigation-note`. The trend drawer switches four/eight-week views using the same active cohorts. `/research/` holds course quotes/baselines, separate from activation data. `/module-1/` preserves the earlier prototype and its bundled sample. Note validation is in `investigation-note-model.ts`, browser reads/writes in `investigation-note-storage.ts`, transitions in `useInvestigationNote.ts`, and rendering in the note components. Campaign observation construction is separate from its storage and display.

## What's solid vs. what's duct tape

| Area | State | Notes |
|---|---|---|
| Naming and organization | solid | Screens have descriptive names. The former combined dashboard is separated into screen composition, note model/storage/controller, and display components. Routes, focus behavior, and browser keys were preserved. |
| Metric data path | solid | PostgreSQL-backed reads return 8 cohorts, 2 channels, and 2 campaigns. The client validates metadata, counts, duplicates, and reconciliation. Overall rates remain 336/800 = 42% and 304/800 = 38%; eight-week activation is 640/1,600 = 40%. |
| Failure and recovery | solid | Loading hides data until validated. Failed requests expose Retry. Campaign missing-record, empty, request-error, and generic missing-route states remain distinct. Labeled demo states remain available. |
| Browser note lifecycle | solid | Save captures the current observation collection. A draft restores separately; Cancel restores saved reasoning/evidence, and Clear retains the working collection. Failed writes and partial draft cleanup report their actual outcomes. |
| Hosted access controls | solid | Live SQL checks passed for constraints, read-only metrics, and isolation between two user IDs, with all temporary rows rolled back. This verifies database policies, not an application sign-in flow. The browser uses only a publishable key. |
| Accounts and cloud notes | rough | The owner-protected notes table exists, but the current app does not write to it. No cross-device sync, account isolation for local notes, collaborative editing, or note history is implemented. |
| Data and measurement | rough | Counts are an illustrative seed, periods are relative, and no live analytics ingestion or behavior tracking exists. Saved evidence lacks a dataset version/timestamp; selected signal labels use the active dataset. No production-readiness or usability claim follows from implementation checks. |

**Verification:** 105 automated checks, TypeScript, and the production build passed. Live public Data API reads matched the expected seeded records. Browser checks covered the overview, four/eight-week trends, channel filtering, campaign comparison/detail, evidence collection, and saved-note restoration after refresh. Delayed hash navigation was fixed and regression-tested. The 390 px mobile overview has no horizontal overflow. Live SQL checks passed for grants, constraints, ownership isolation, timestamps, and rollback cleanup. Sites version 6 was published successfully from source commit `89658f01b4d8078b53a79289ceaeec0bfbbd80e9`; the public overview loaded the hosted dataset correctly.

## Risks & assumptions for the team

1. **Product:** Run the three-minute unaided test from the [validation brief](../02-validation/validation-brief.md). A reader must name an investigation, connect the headline and at least one supporting signal, and identify an unknown. Supplied explanations can cue an answer, so functional success is insufficient.
2. **Engineering, first task:** Open `src/features/investigation/investigation-note-storage.ts` and `useInvestigationNote.ts`, then `supabase/README.md`. Build the account sign-in and owner-scoped note adapter against `investigation_notes`. Preserve drafts and saved snapshots, make local-note import explicit, and test two separate authenticated sessions before claiming cross-device persistence. Confirm Auth site/redirect URLs and email delivery as part of that work.
3. **Data:** The current contract is one fixed eight-week sample with organic/paid channels. Real ingestion needs dated mature cohorts, attribution rules, timezone, freshness, and dataset versioning. Keep exact denominators and reconcile every level. Resolve the existing zero-denominator inconsistency: campaign rates show “—”, while overview/trend helpers return 0.
4. **Reliability and operations:** Free-tier availability, monitoring, backups/recovery, and concurrent note edits need an owner and a production decision. Four metric-table reads are validated together but are not one database snapshot transaction. Publishable settings are embedded at build time, so configuration changes require a rebuild. No runtime AI or telemetry service is connected.
5. **Scope:** Continue as a testable prototype while the usability hypothesis is unresolved. Real acquisition data, costs, retention, release/error history, template-use history, experiment execution, and file uploads remain outside this build.

## How to run it

Get the application source checkout/export from the Sites project owner. This course repository holds the deliverables, not the app source. From the application root:

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

Hosted settings are `VITE_SUPABASE_URL=https://abmavcuiwevkdlqqgngg.supabase.co` and `VITE_SUPABASE_PUBLISHABLE_KEY`, copied from the project's API Keys settings. `.env.local` is ignored. Never use the secret or service-role key in a browser setting. Both settings omitted means fixture mode; partial/invalid configuration produces an error.

`supabase/migrations/202611150001_core.sql` was applied once through the project's SQL Editor. Do not rerun it against the existing tables. `supabase/verify.sql` contains rollback-only database checks, separate from Auth sign-in verification. The application README and `docs/module-4.md` contain the detailed source map, prompts, checks, and screenshots. Reuse the existing Sites identity in `.openai/hosting.json` when publishing. Sites version 5 preserves the pre-refactor baseline.
