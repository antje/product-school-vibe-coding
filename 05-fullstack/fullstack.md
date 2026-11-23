# Full-Stack: Data, Access Rules, Edge Cases, Deploy

> Module 5 · Full-Stack. Add data schemas, access rules, and edge cases; stress-test and deploy.

## Deployed link

[Metric Moment Compass](https://metric-moment-compass.anajuana.chatgpt.site/)

Published as Sites version 7 on November 22, 2026, from source commit `2a020c6abf3c17a73cc3501a86939ce43f23a18b`. The dashboard remains public. Saved account investigations are private.

## Data schema

Module 5 connects the application to the existing private-note table. The five Module 4 tables remain unchanged. Hosted dashboard metrics remain **illustrative data**.

| Entity | Key fields | Notes |
|---|---|---|
| `dataset_versions` | `id` (text primary key), `is_sample`, `label` | Identifies the public `sample-v1` dataset and its provenance. |
| `activation_cohorts` | `dataset_id` (foreign key), `week_index`, `eligible`, `activated` | Composite key: dataset + week. Eight mature weekly cohorts drive the headline and trend. |
| `acquisition_channels` | `dataset_id`, `id`, `name`, `previous_eligible`, `previous_activated`, `current_eligible`, `current_activated` | Composite key: dataset + channel. Counts reconcile with the cohorts. |
| `campaigns` | `dataset_id`, `id`, `name`, `previous_eligible`, `previous_activated`, `current_eligible`, `current_activated` | Composite key: dataset + campaign. Counts reconcile with the paid channel. Ordered reads support up to 5,000 campaigns. The UI shows 10 per page, with totals across all rows. |
| `investigation_notes` | `user_id` (UUID primary key, foreign key to `auth.users.id`), `dataset_id`, `investigation`, `custom_investigation`, `rationale`, `unknown_text`, `evidence`/`observations` (JSONB), `created_at`/`updated_at` | One saved note per account. Upsert replaces it. Timestamps are server-owned. Deleting the Auth user deletes its note. |
| Supabase Auth | User ID, email, managed authentication credentials/session | Provides identity for note ownership. Passwords are handled by Auth, outside the application tables. |

Guest notes stay in browser storage. Account drafts and observations use per-user keys. Save captures observations in the private note. Guest import requires confirmation and a separate save, preserving the original.

## Access rules

- **Public dashboard:** visitors can read the designated illustrative dataset. Browser roles cannot edit metrics or read other datasets.
- **Private notes:** authenticated users can read, create, update, and delete their own row. RLS checks `auth.uid() = user_id`, including the proposed owner on updates. The session supplies the owner.
- **Account changes:** sign-out and switching clear the previous private view. Late responses cannot restore it. Local drafts are account-scoped, but anyone using the same browser profile can access browser storage.
- **Authentication:** email/password signup and login are implemented with confirmation enabled. Custom SMTP is off, and the default sender restricts delivery. Test accounts were created and confirmed manually. Public signup email delivery remains unverified.

## Edge cases hardened

| Case | Before | After |
|---|---|---|
| Empty / first-run state | Notes were browser-local, with no account-specific first visit. | A confirmed empty account shows “Get started.” An unreadable note shows an error instead of a false empty state. Guest content is imported only by explicit choice. |
| Bad / malicious input | Local validation checked required fields. Account ownership had no application flow to exercise it. | Validation rejects unknown choices, unsafe observation links, titles over 2,000 characters, reasoning/unknowns over 10,000 each, more than three allowed signals, and more than 20 observations. The database also bounds observation JSONB at 100,000 bytes. RLS remains the authority for ownership. Invalid edits stay available for correction. |
| Failure / offline | Hosted metric errors already offered Retry. Notes had no network transaction. | Reads show loading states and use 15-second request deadlines. Errors offer inline recovery. Failed saves retain drafts and never claim success. An uncertain write requires checking the saved note before retrying. A metric failure leaves the note accessible. Pending guards prevent duplicate submissions. The last accepted save replaces the previous note. |

## Stress test results

Verified on November 22, 2026. Lab 2 uses **Spam Click** as its selected stress test, alongside the offline kill switch. Automated checks, live Data API checks, and browser observations are distinguished below.

| Check | Result |
|---|---|
| Automated regression suite | **Passed:** 148 tests, TypeScript, and the production build. Coverage includes field limits, private save/read, failed-save draft retention, duplicate submissions, account switching during delayed requests, cancelled import, and request deadlines. |
| Authentication recovery | **Passed, automated:** same-user reauthentication restores saving and retains the draft. A late sign-in response cannot undo sign-out. |
| Pagination and data bounds | **Passed, automated:** totals include off-page rows, smaller server pages do not truncate data, 5,000 campaigns load, and a 5,001st row triggers an error. Live capacity is unmeasured. |
| First account / empty state | **Passed, live:** a newly created, confirmed account logged in and showed “Get started,” without inheriting the guest note. Application signup and confirmation delivery remain pending. |
| Slow network | **Partially verified:** reload and navigation preserved the session, and the published overview displayed its loading state before hosted metrics arrived. Slow 4G was enabled in a separate test tab, so these observations do not establish behavior under throttling. Loading skeletons have automated coverage. |
| Persistent save | **Passed, live Data API:** both accounts logged in. Account A created and updated a note with server-owned timestamps, then retrieved it in a fresh authenticated session. The browser subsequently saved the recovery-test note and retained its contents and server timestamp after refresh. |
| Two-account isolation | **Passed, live Data API:** account B’s attempts to read, update, or delete A’s note returned no rows. Creating a note with A’s identity and transferring A’s ownership to B were denied. B saved its own independent note. Delayed browser account changes are covered by automated regressions. |
| Offline kill switch and recovery | **Passed, browser:** with Chrome Network set to Offline, Save showed an unconfirmed-save error, retained the draft and signed-in identity, and disabled another write. After connectivity returned, Check saved note restored saving. The confirmed save survived refresh. Separate per-URL blocking was not run. |
| Spam Click: five rapid Save clicks | **Passed, browser:** five rapid clicks on Save changes put the form into its disabled Saving state. After refresh, the account showed one saved investigation with unchanged content and an updated server timestamp. **Passed, live Data API:** five concurrent upserts also left one row. The database primary key enforces one note per account. |
| Successive saves from two sessions | **Passed, live Data API:** two sessions saved in sequence, and the last accepted write replaced the earlier revision. Simultaneous conflicting edits were not tested. The product does not merge edits. |
| Database limits and cleanup | **Passed, live Data API:** a 10,001-character field was rejected without replacing the saved revision. The run removed only its test notes and signed out both verification sessions. The report recorded **19 passed, 0 failed**. |
| Module 5 publication | **Passed:** Sites version 7 published successfully at the existing public URL. The public overview loaded hosted metrics, sign-in succeeded, and the saved recovery note appeared from a separate origin. The direct Social campaign route also loaded correctly. Title, favicon, and share-image metadata are present. |

**Ship decision: SHIP for the class prototype and confirmed test accounts.** No P0 blocker was observed in the tested save, access-control, offline-recovery, or five-click flows. The public dashboard remains available without login. **NO-SHIP for broad self-service account onboarding** until custom SMTP is configured and signup confirmation succeeds end to end.

**Known gaps:** throttled-network behavior and a separate blocked-request test remain unverified. The 5,000-row boundary has automated fixture coverage, with live capacity unmeasured. Simultaneous edits use replacement rather than merging. These implementation checks do not validate the Module 2 usability hypothesis.

Evidence: [public overview](assets/public-overview.jpg), [sign-in screen](assets/sign-in.jpg), [confirmed cloud note](assets/cloud-note.jpg), [saved note after five rapid clicks and refresh](assets/spam-click-persisted.jpg), and [live verification report](live-verification.txt).

Presentation copy: [Integrations & Data Model and Edge Cases & Known Gaps](deck-sections.md).
