# Agent Instructions — Gångertabellen

Before reviewing, proposing, or changing code in this repository, **read `DEVELOPMENT.md`**. It is the authoritative guide to the product's principles, architecture, coding standards, and change workflow.

## Non-negotiable defaults

- Preserve a simple, browser-native multiplication practice game focused on repetition and encouraging feedback.
- Keep player data in browser storage only. Never add accounts, external analytics, cloud storage, or data transmission without explicit owner approval.
- Preserve compatibility with existing browser-stored profiles and game history. Never clear or silently reset stored data.
- Prefer HTML, CSS, and vanilla JavaScript; add no dependencies, frameworks, backend, or build process without explicit approval.
- Keep the app usable in a browser and via “Add to Home Screen,” especially on mobile Safari.
- Maintain Swedish and English text, responsive design, keyboard/touch accessibility, and reduced-motion behaviour.
- Make small, focused changes with readable code and comments that explain non-obvious intent; avoid unrelated refactors.
- Do not change `main` directly. Prepare a focused branch and pull request, describe tests performed, and leave the merge decision to the owner.

If a request conflicts with the development guide, clearly identify the conflict before making the change. Ask for approval rather than silently changing the product philosophy.