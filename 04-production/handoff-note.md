# Engineering Handoff Note

> Module 4 · Production Specs. Open the black box, make the build legible to an engineer.

**Updated November 22, 2026, for M5/M6:** This handoff describes published Sites version 8, source commit `a9d03cf3cc907e90ce559a0a89a4f1bd2b4dd6a3`. The [Module 4 snapshot](https://github.com/antje/product-school-vibe-coding/blob/21f662c1907ad114cd9253bd89da93f9c4190f00/04-production/handoff-note.md) preserves the earlier state.

## What this is

[Metric Moment Compass](https://metric-moment-compass.anajuana.chatgpt.site/) helps a product lead investigate a decline in first-project activation. Users follow the headline into channel and campaign evidence, save their next investigation and unknowns, and copy a summary for discussion. We have not yet validated whether they can explain that choice without spreadsheet export or coaching. The build groups code by feature and reads illustrative metrics from Supabase PostgreSQL. Guests save locally. Signed-in users save one private account note. Public signup confirmation delivery remains unverified, so account use is limited to confirmed test accounts.

## Architecture (plain language)

- **Frontend:** React and TypeScript with TanStack routing, Tailwind, Radix, and Recharts. Sites hosts the prerendered app and browser assets from `dist/client`. Generated server output is used during the build, not as a deployed product API. Route files in `src/routes` point to named screens under `src/features`: `activation`, `auth`, `campaigns`, `investigation`, `research`, and `original-prototype`. Shared components live in `src/components`. The app README covers routes, setup, and storage behavior.
- **Backend / data:** Supabase project `abmavcuiwevkdlqqgngg` holds `dataset_versions`, `activation_cohorts`, `acquisition_channels`, `campaigns`, and `investigation_notes`. The published client reads the first four tables with a browser-safe publishable key. A shared data provider validates responses and cohort → channel → campaign reconciliation before rendering metrics. Failures offer Retry without substituting fixtures. All five tables have Row Level Security. Public users can read only designated sample metrics. The signed-in session identifies the owner of private note reads, upserts, and deletes. One row per account uses server-owned timestamps and last-accepted-write replacement. Email Auth requires confirmation. Storage is provisioned but unused.
- **Key flows:** `/` → channel comparison → `/campaigns/` → `/campaigns/search/` or `/campaigns/social/` → collected observation → `/#investigation-note` → Copy summary. The trend drawer switches between four and eight weeks using the active cohorts. `/research/` holds course quotes and baselines, separate from activation data. `/module-1/` preserves the earlier prototype and bundled sample. Guest import requires confirmation and a separate account Save. Guest originals remain local. Account changes clear the private view and ignore stale responses.

**Source map:** Paths below are relative to the application root.

| Concern | Entry points |
|---|---|
| Session and sign-in | `src/features/auth/AuthContext.tsx`, `AuthDialog.tsx`, `AccountControl.tsx` |
| Hosted metrics | `src/features/activation/activation-dataset.ts`, `ActivationDatasetContext.tsx` |
| Note lifecycle | `src/features/investigation/useInvestigationNote.ts` selects `useGuestInvestigationNote.ts` or `usePrivateInvestigationNote.ts`. `investigation-note-model.ts` validates content. |
| Persistence and recovery | `src/features/investigation/private-note-repository.ts` owns validated remote operations and deadlines. `investigation-note-storage.ts` and `observation-storage.ts` preserve guest keys and account-scoped drafts/collections. |
| Saved note and copying | `src/features/investigation/SavedInvestigationNote.tsx`, `investigation-summary.ts`, `CopyInvestigationSummary.tsx` |
| Database contract | `supabase/migrations/202611150001_core.sql`, `supabase/README.md`, `supabase/verify.sql` |

## What's solid vs. what's duct tape

| Area | State | Notes |
|---|---|---|
| Naming and organization | solid | Named screens, note validation, storage, state transitions, and views are separated. Existing routes, focus behavior, and browser-storage keys are preserved. |
| Metric data path | solid | PostgreSQL reads return 8 cohorts, 2 channels, and 2 campaigns. The client validates metadata, counts, duplicate IDs, and reconciliation. Overall activation is 336/800 = 42% previously and 304/800 = 38% currently. Eight-week activation is 640/1,600 = 40%. |
| Failure and recovery | solid | Data appears only after validation. Failed requests offer Retry. Missing campaigns, empty results, request failures, and unknown routes have distinct states. Labeled demo states remain available. |
| Guest and account note lifecycle | solid | Save captures observations. Drafts restore separately. Cancel restores saved reasoning and evidence, while Clear retains the working collection. Guest work imports only by explicit choice. Account drafts and collections use owner-specific local keys. |
| Hosted access controls | solid | Module 5 live Data API checks exercised real authenticated sessions, owner isolation, timestamp ownership, field limits, and one-row replacement. Failed or uncertain saves retain drafts, and Check saved note resolves uncertainty before another write. |
| Accounts and cloud notes | solid for confirmed test accounts | Account notes persist remotely. Sign-out/switching clears private UI and ignores stale responses. The original guest keys remain intact. Collaborative editing and history are absent. Simultaneous conflicting edits have not been tested. |
| Copy summary | solid | Saved guest/private reasoning and observations copy with public source links and the sample-data caveat. Draft edits and account identity are excluded. Missing or denied clipboard access exposes selectable text. Browser verification covered successful copying. Failure recovery has automated coverage only. |
| Public onboarding | rough | Signup/login controls exist, but custom SMTP is off and public signup confirmation delivery is unverified. Test accounts were manually confirmed. |
| Data and measurement | rough | Counts are illustrative, periods are relative, and live analytics ingestion and behavior tracking are absent. Account notes have dataset ID and server timestamps. Guest records lack both, and selected signal labels use the current dataset. Implementation checks do not establish usability or production readiness. |

**Verification:** The [Module 6 record](../06-iteration/iteration.md) reports 158 tests across 18 files, TypeScript, and the production build passing for version 8. Actual clipboard output was checked for a saved private note locally and a guest note on the public site. A cancelled draft was excluded. Clipboard failure and selectable fallback were checked only in automated UI tests.

The [Module 5 record](../05-fullstack/fullstack.md) preserves the earlier live integration evidence: 19 Data API checks passed, including two-account isolation and fresh-session retrieval. Browser checks covered offline-save recovery, five rapid Save clicks, and persistence after refresh. Throttled-network behavior was only partially verified, and a separate blocked-request test was not run. The 5,000-campaign limit has automated fixture coverage, with live capacity unmeasured. Historical Module 4 checks and screenshots remain in the linked snapshot and `docs/module-4.md`. No human-study result or production-readiness claim follows from these checks.

## Risks & assumptions for the team

1. **Product:** Run the three-minute unaided test from the [validation brief](../02-validation/validation-brief.md). A reader must name an investigation, support it with the headline and at least one related signal, and identify an unknown. Supplied explanations may cue an answer, so working controls alone cannot validate the hypothesis.
2. **Engineering, first task:** Configure custom SMTP and verify application signup, confirmation email delivery, and return to the intended site. Confirmed test accounts support the class prototype, but broad self-service onboarding remains a no-ship decision. Complete throttled-network and separate blocked-request checks before extending reliability claims.
3. **Data:** The current contract supports one fixed eight-week sample with organic and paid channels. Real data needs dated cohorts that have completed the activation window, attribution rules, a timezone, freshness information, and dataset versions. Preserve exact denominators and reconcile all counts. Resolve inconsistent zero-denominator handling: campaign rates show “—”, while overview and trend helpers return 0.
4. **Reliability and operations:** Assign owners and agree on retention, account deletion, availability, monitoring, backup/recovery, and concurrent note edits. Last accepted save replaces the prior note, with no merge or revision history. Browser-local drafts and observations remain accessible to others using the same browser profile. The project uses the free tier. Metric-table reads are validated together but do not share a database snapshot transaction. Public configuration is embedded at build time, so changes require a rebuild. No runtime AI or telemetry service is connected.
5. **Scope:** Keep testing the usability hypothesis. Real acquisition data, costs, retention, release and error history, template-use history, experiment execution, and file uploads remain outside this build.

## How to run it

Get the application source from the Sites project owner at source commit `a9d03cf3cc907e90ce559a0a89a4f1bd2b4dd6a3`. The course repository contains the deliverables only. Requires Bun and a supported Node.js version. Run these commands from the application root:

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

Set `VITE_SUPABASE_URL=https://abmavcuiwevkdlqqgngg.supabase.co` and copy `VITE_SUPABASE_PUBLISHABLE_KEY` from the project's API Keys settings. Git ignores `.env.local`. Never use a secret or service-role key in a browser setting. Omitting both settings selects fixture mode without accounts. Partial or invalid configuration produces an error. Use a confirmed account to exercise private notes in hosted mode. Configure Auth site/redirect URLs for the intended origin, and do not treat a visible signup form as proof of email delivery.

The migration `supabase/migrations/202611150001_core.sql` was applied through the SQL Editor. Module 5 reuses it without a replacement migration. Do not rerun it against the existing tables. `supabase/verify.sql` checks the database and rolls back every test write. It does not test Auth sign-in. The application README, `docs/module-4.md`, and `docs/module-5.md` contain setup and implementation evidence. The course [Module 6 record](../06-iteration/iteration.md) links the copy-summary checks and screenshots.

Keep the existing Sites identity in `.openai/hosting.json` and publish `dist/client` through the Sites workflow. Version 8 is the current publication. Restore a saved Sites version to roll back, without rewriting source history. Version 5 preserves the pre-refactor baseline.
