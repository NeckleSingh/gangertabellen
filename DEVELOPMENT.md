Träna Matte — Development Guide
This document describes the enduring product and engineering principles for Träna Matte (formerly Gångertabellen). Read it before proposing or making changes. Preserve these principles unless the project owner explicitly chooses to revise them.
Purpose
Träna Matte is a simple, encouraging arithmetic-practice game for children. Its aim is to build fluency in multiplication, addition, subtraction and division through repetition, make practice enjoyable, and help children recognise their own progress.
Product principles
1. Keep it simple. Children should be able to use the app independently, with little explanation and few decisions. Avoid unnecessary screens, settings, and features.
2. Encourage continued practice. Treat mistakes as part of learning. Use constructive, positive feedback rather than punishment, pressure, or shame.
3. Preserve repetition. Arithmetic recall practice is the core experience. Changes must not obscure or interrupt the basic question–answer–feedback loop.
4. Respect local data ownership. Player profiles and practice history stay in the browser. No account, cloud database, analytics tracking, or external transfer of children's data is needed. Users understand that clearing browser/site data may erase their history; do not add cloud sync or backup systems unless explicitly requested.
5. Work as a browser app. The app must run directly in a normal browser and remain suitable for “Add to Home Screen” use on phones and tablets. A native app is not required.
6. Treat Swedish and English as equal, permanent languages. Both languages are core to the product, not optional extras. New and changed player-facing features must work naturally in both languages. Do not remove or weaken language switching without the owner's explicit approval.
7. Remain approachable. Support touch and keyboard interaction, responsive layouts, readable text, and accessibility.
Learning rules and staged rollout
- Multiplication keeps its original 1–10 and 11–20 levels: first factor within the selected range, second factor 1–10.
- Addition has strict answer ranges 1–50 and 51–100; each number being added is at least 1 (so 1 is not itself an achievable sum). Do not include 0 as an addend.
- Subtraction (planned separately) uses a starting number at most 50, never produces a negative answer, and may produce 0.
- Division (planned separately) uses a dividend at most 80 with whole-number answers only; never divide by 0.
- An operation should not be shown as selectable until its gameplay and history handling are implemented.
- Correctly solved questions must not repeat within a game; skipped questions can reappear. Keep the current 100-correct-answer limit per game unless explicitly revised.
- Require an explicit operation choice for each game, and a level choice when the operation has multiple levels. Single-level operations do not need an additional level choice.
- One correctly solved question in a saved game earns one lifetime point. Calculate points from existing saved sessions rather than storing a second counter.
- Older saved sessions without an operation or level are basic multiplication games. Preserve their history and scores as stored.
Architecture and dependencies
- The current app is a static, browser-native project with its interface, CSS, and JavaScript in index.html, plus static assets and GitHub Pages domain configuration.
- Prefer HTML, CSS, and plain JavaScript. Do not introduce a framework, package manager, build step, backend, or other dependency without an explicit, demonstrated need and the owner's approval.
- A single HTML file is acceptable while it remains easy to navigate. Do not split it into multiple files solely to imitate a larger project; modularise only when it genuinely improves maintainability.
- Prefer built-in browser APIs. Keep the app fast, lightweight, and functional without server-side logic.
Languages and localization
- Swedish and English are supported first-class languages. Every new or changed player-facing message, button, label, instruction, result, and accessibility announcement must be available in both.
- Keep language-specific text in the existing translation mechanism rather than introducing scattered hard-coded text or separate gameplay logic for each language.
- Write natural, child-friendly language; do not rely on literal word-for-word translations where they sound unnatural.
- Ensure switching languages updates the relevant interface without changing player data, scores, or gameplay state. Preserve the app's existing language-choice behavior unless a change is explicitly requested.
- Test important flows in both Swedish and English, including error states, retries, results, and screen-reader text when relevant.
Data safety and compatibility
- Browser storage is the only intended persistent data store. Never send stored player information to a server or third party.
- Existing profiles and completed games must continue to load after an update.
- Do not rename storage keys, change stored data shapes, discard existing fields, or clear stored data without an explicit compatibility plan and approval.
- When a storage change is unavoidable, validate older data and provide a safe migration. Handle missing, corrupted, or unexpected data gracefully.
- Do not quietly change the meaning of recorded scores, attempts, or timings.
- Do not treat browser data loss from user-initiated clearing as a defect requiring accounts or remote backup.
Code quality and documentation
- Optimise for clarity over cleverness. Use descriptive names, small functions with clear responsibilities, and straightforward control flow.
- Add concise comments to explain why non-obvious decisions exist, including timing logic, storage compatibility, game rules, and browser-specific behaviour. Do not comment on every obvious line.
- Remove obsolete code when safe. Avoid duplicating logic or introducing abstractions for hypothetical future features.
- Preserve semantic HTML, safe DOM manipulation, keyboard accessibility, reduced-motion support, and responsive behaviour.
- Avoid unrelated formatting or refactoring during a bug fix, so the actual change stays easy to review.
Change workflow
1. Define the bug or requested behaviour, including how to reproduce it and what success looks like.
2. Make a dedicated Git branch for one focused fix or related set of changes. Do not work directly on main.
3. Make the smallest clear change. Explain any trade-offs before introducing new complexity.
4. Test locally in a browser, including existing stored data. Test on mobile Safari / the Home Screen experience when relevant.
5. Open a pull request with a short explanation, the files changed, the tests performed, and any known limitations.
6. The project owner reviews and decides whether to merge into main.
Minimum regression checklist
For every behavioural change, check the relevant items and explicitly state which were not tested:
- App loads normally in a desktop and mobile browser.
- Existing players and saved sessions remain intact after refresh or reopening.
- Player selection, creation, and dashboard still work.
- All implemented operation question ranges, incorrect attempts, retries, and completion still behave correctly; check multiplication for regressions.
- Results, scores, session history, and timing remain consistent.
- Both Swedish and English are complete and natural throughout affected screens, feedback, errors, results, and accessibility labels; language switching still works.
- Touch input, keyboard input, small-screen layout, and relevant accessibility behaviours still work.
- The Home Screen launch experience is not unintentionally changed.
Automated tests are welcome when they provide practical value, but do not add a substantial toolchain just to satisfy a process requirement.
Decision rule
When two solutions work, prefer the one that is easier to understand, easier to test, requires fewer dependencies, preserves browser-local data, and keeps learning enjoyable. If a proposed change conflicts with these principles, flag the conflict and ask the owner before implementing it.