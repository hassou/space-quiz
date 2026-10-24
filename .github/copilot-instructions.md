# Copilot Instructions

## Project structure and architecture

`index.html` is the entire application: it contains the welcome, quiz, and results markup; all CSS; the question data; and the browser-side quiz logic. The app is intentionally a static, dependency-free page that can be opened directly in a browser.

The `questions` array is the source of truth for quiz content. `renderQuestion()` updates the active prompt and creates its answer buttons; `chooseAnswer()` handles scoring, feedback, and progress; `showView()` switches between screens; and `showResults()` selects the final reaction. Keep quiz totals derived from `questions.length`.

## Commands and validation

There is no package manifest, build system, test runner, or linter configured, so there are no build, test, lint, or single-test commands. For behavior changes, open `index.html` in a browser and exercise the affected screen and answer flow.

## Repository-specific conventions

- Keep application changes self-contained in `index.html`; do not introduce a server, build step, or external runtime dependency.
- Question objects use `category`, `text`, `answers`, a zero-based `correct` answer index, and a short `fact` shown as feedback.
- The three screens are toggled with the `hidden` attribute. Keep interactive controls as native buttons and preserve the existing live feedback and progress-bar semantics.
- Theme colors are CSS custom properties in `:root`, with light-mode overrides in `@media (prefers-color-scheme: light)`. Preserve both themes and the reduced-motion override when changing visual effects.
