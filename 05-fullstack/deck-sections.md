# Module 5: Final-project deck sections

## Integrations & Data Model

**A public analytics dashboard with private, persistent investigations.**

- Sites hosts the app. Supabase PostgreSQL stores the illustrative metrics and saved notes. Supabase Auth provides email/password identity.
- A dataset version links eight activation cohorts, acquisition channels, and campaigns. Rates use summed counts, including campaigns beyond the visible page.
- Each authenticated user owns one investigation note, linked to the dataset. Saving replaces that row and records a server timestamp.
- Row-level security permits public reads of the designated sample dataset and restricts note reads and writes to `auth.uid() = user_id`.
- Guest notes remain local. Importing a guest note requires an explicit choice and a separate save to the account.

**Evidence:** two real accounts passed isolation checks. A saved note survived a fresh session and browser refresh. [Live verification report](live-verification.txt): 19 passed, 0 failed.

## Edge Cases & Known Gaps

**Ship the class prototype for public exploration and confirmed accounts.**

| Stress case | Observed result |
|---|---|
| Offline save | Inline error retained the draft and session. Checking the saved note after reconnection restored saving. The confirmed save survived refresh. |
| Five rapid Save clicks | The form disabled during saving. Refresh showed one saved investigation. Five concurrent Data API upserts also left one row. |
| New confirmed account | An active empty state offered Get started. Guest content was not inherited. |
| Cross-account access | Read, update, delete, spoofed-owner insert, and ownership-transfer checks enforced isolation. |
| Data volume | Automated fixtures covered 5,000 campaigns and rejected a 5,001st row. Live load capacity is unmeasured. |

**Release boundary:** no P0 blocker was observed in the tested flows. Broad self-service signup is not ready: custom SMTP and end-to-end confirmation delivery remain outstanding. Throttled-network behavior and per-request blocking need direct verification. Successive saves replace the previous revision, and simultaneous conflicting edits are untested. Hosted metrics remain illustrative, and usability validation is still separate from these implementation checks.

**Live product:** [Metric Moment Compass](https://metric-moment-compass.anajuana.chatgpt.site/)

**Submission evidence:** [Full-stack record](fullstack.md) · [five-click result](assets/spam-click-persisted.jpg)
