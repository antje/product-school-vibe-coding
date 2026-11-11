# Dashboard v4: Design revision

[Open the dashboard](https://metric-moment-compass.anajuana.chatgpt.site/) · [Research context](https://metric-moment-compass.anajuana.chatgpt.site/research/) · [Design prompts](DESIGN-PROMPTS.md)

## What changed and why

- Adopted the selected [Profound reference](https://mobbin.com/screens/8dfd92df-f43e-4951-8c89-d1f23e3cddbf): quiet navigation, a compact period bar, white panels, thin borders, and aligned numerical comparisons. This makes related evidence easier to scan.
- Paired activation rate with signup share at both channel and campaign level. Counts and denominators stay visible, and all bars use the same 0–100% scale. The display separates changes in performance from changes in audience mix.
- Kept the original investigation visible during drill-down: overall activation moved from 42% to 38%, while paid signup share moved from 40% to 60%.
- Added observation collection with figures, period labels, and source links. The reader still chooses the investigation and writes the rationale and unknowns. Drafts survive navigation, and saved notes retain their own evidence snapshot.
- Moved the course research quotes and dashboard-use figures to a separate Research context page. They remain available for Module 2 while the main dashboard focuses on activation and the investigation.

## Screenshots

The baseline captures were saved before the design work. The completed Module 3 screenshots remain in the parent assets folder.

| Screen | Before | After |
|---|---|---|
| Overview | [Desktop](before/overview.png) | [Desktop](after/overview.png) |
| Channel evidence | [Desktop](before/supporting-evidence.png) | [Desktop](after/supporting-evidence.png) |
| Campaign comparison | [Desktop](../assets/campaign-comparison.png) | [Desktop](after/campaigns.png) · [Mobile](after/campaigns-mobile.png) |
| Campaign detail | [Desktop](../assets/campaign-detail.png) | [Desktop](after/campaign-detail.png) · [Mobile](after/campaign-detail-mobile.png) |
| Mobile overview | [Mobile](before/overview-mobile.png) | [Mobile](after/overview-mobile.png) |
| Collected evidence in note | — | [Desktop](after/investigation-note.png) |
| Research context | Included in overview | [Desktop](after/research-context.png) · [Mobile](after/research-context-mobile.png) |

State captures: [Loading](after/loading.png) · [Empty](after/empty.png) · [Error](after/error.png) · [Unknown campaign](after/not-found.png). Loading, empty, and error captures use the explicitly labeled state previews. Retry returns to the normal data request.

## Checks completed

- 54 automated tests passed, covering sample arithmetic, routes, request states, observation persistence, duplicate prevention, storage failures, saved-note compatibility, drafts, and research content.
- TypeScript and the production build passed.
- Desktop and 390px mobile screens were inspected. Previous/current pairs remain together, and the mobile screens fit without horizontal page overflow.
- Browser interactions verified campaign navigation, adding an observation, duplicate prevention, returning to a preserved draft, saving and refreshing a note, and error recovery through Retry.
- A focused correction ensures Edit → remove a working observation → Cancel leaves the saved note’s evidence intact. The saved snapshot and working collection are explicitly distinguished.

## Limits

This remains a prototype using illustrative activation and campaign data. The research quotes and dashboard-use metrics are supplied by the course scenario. Notes and observations are stored only in the current browser. Visual and functional checks do not establish that the three-minute usability hypothesis has passed.
