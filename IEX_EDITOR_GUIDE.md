# IEX 2026 — one website and one publishing source

Official website: https://iex2026.dbr77.com/
Repository: https://github.com/DBR77/AutomateUSA
Editable page: `iex2026/index.html`
Styles and images: `iex2026/assets/`

Railway project `iex2026`, service `web`, production: publish `main` from root `/iex2026`. Do not deploy the repository root or edit `events/iex/index.html`: that file only redirects the old GitHub Pages URL. GitHub Pages excludes `iex2026/` from its own publication.

## Editing

Clone or pull the repository, inspect AGENTS.md if present and preserve other work. Create a branch, edit only the requested IEX content, preview with a local static server rooted at `iex2026`, and check desktop/mobile, images and speaker biography dialogs. Use English content. Keep the approved October 28, 2026 date and Charlotte/Berlin times unless explicitly asked to change them. Preserve registration consent and HubSpot integration.

Commit and open a PR into `main`; after merge, check Railway SUCCESS and https://iex2026.dbr77.com/ before claiming publication. A GitHub commit alone is not evidence that the live site changed. An editor needs GitHub Write; routine website editing does not require Railway administrator credentials.

## Consolidation — 2026-10-08

Primary live design, date/time pairs and existing registration script were preserved. Panel 05 speaker cards, images, biographies and NC WTA partner from commit 761b7d7 were retained. The old page https://automate.dbr77.com/events/iex/ now redirects to the official page, preserving query parameters and fragments when JavaScript is enabled. GitHub Pages only supports a client redirect here, not an HTTP 301.

Earlier AI editing prompts pointing to `events/iex/index.html` are superseded by this guide.
