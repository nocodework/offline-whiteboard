# Contributing

Thanks for considering a contribution! This project is deliberately tiny and dependency-free, and the goal is to keep it that way.

## Ground rules

- **One file.** The entire app lives in `index.html` — HTML, CSS and vanilla JS. No build step, no bundler, no npm, no framework.
- **Zero runtime dependencies.** No CDN links, no web fonts, no analytics. The page must make **0 network requests** so it keeps working fully offline / air-gapped. PRs that add a network call will be declined.
- **Keep it readable.** Plain JavaScript, small functions, clear comments.

## Running it

There's nothing to install. Open `index.html` in a browser (double-click, or `python3 -m http.server` and visit it). Edit the file, refresh.

## Before opening a PR

- Test the core flows by hand: create notes/shapes/text, draw arrows, move/resize, undo/redo, pan/zoom, export PNG, export & re-import JSON, reload (auto-save), `Clear`.
- Confirm there are still **no network requests** (DevTools → Network → reload).
- Keep the diff focused; describe what you changed and why.

## Ideas that fit

- Bug fixes and accessibility improvements
- New shapes or connector styles (without external deps)
- Better touch / mobile interactions
- Performance on very large boards

## Ideas that don't fit

- Anything requiring a server, account, or network call
- Heavy libraries or a build pipeline

By contributing you agree your work is licensed under the project's [MIT License](LICENSE).
