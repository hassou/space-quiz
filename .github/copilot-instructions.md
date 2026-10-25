# Copilot Instructions

## Project structure and architecture

`index.html` is the entire application: it contains the welcome, quiz, and results markup; all CSS; the question data; and the browser-side quiz logic. The app is intentionally a static, dependency-free page that can be opened directly in a browser.

The `questions` array is the source of truth for quiz content. `renderQuestion()` updates the active prompt and creates its answer buttons; `chooseAnswer()` handles scoring, feedback, and progress; `showView()` switches between screens; and `showResults()` selects the final reaction. Keep quiz totals derived from `questions.length`.

Quiz state is held in `currentQuestion`, `score`, and `answered`. Progress counts completed answers, not the currently displayed question. Choosing an answer locks all answer buttons and reveals the next-step button; advancing requires `answered` to be true. Replay returns to the welcome screen, and starting a quiz resets state.

`.github/workflows/deploy-pages.yml` deploys the repository root directly to GitHub Pages on pushes to `main` or manual dispatch. There is no compilation stage; files added to the root may become part of the published site.

## Commands and validation

Open `index.html` directly in a browser; no installation or server is required.

For behavior changes, exercise the affected flow in the browser: start at zero score, choose both correct and incorrect answers, confirm answers lock after selection, and check progress reaches 100% after the final answer. Verify results and replay reset. Result tiers are perfect (100%), stellar (at least 70%), nice orbit (at least 40%), and new adventure (below 40%).

For keyboard changes, use actual Tab, Shift+Tab, Enter, and Space input. Checking `tabIndex`, calling `.focus()`, or invoking `.click()` only verifies part of keyboard behavior; report that limitation if the browser tools cannot send real keystrokes. Wait for CSS transitions to settle before checking feedback colors.

## Repository-specific conventions

- Keep application changes self-contained in `index.html`; do not introduce a server, build step, or external runtime dependency.
- Question objects use `category`, `text`, `answers`, a zero-based `correct` answer index, and a short `fact` shown as feedback.
- The three screens are toggled with the `hidden` attribute. Keep interactive controls as native buttons and preserve the existing live feedback and progress-bar semantics.
- Preserve focus handoffs: the question heading after rendering, the next-step button after answering, the results heading on completion, and the welcome heading on replay. Headings use `tabindex="-1"` for programmatic focus without adding tab stops.
- Answer states combine `.correct`/`.wrong` styling, check/cross indicators, accessible labels, and live feedback text. Correct answers use the `pop` animation; incorrect selections use `shake` and reveal the correct answer.
- Insert question and answer content with `textContent`; the existing `innerHTML` snippets provide controlled button markup.
- `shareResult()` prefers the Web Share API, falls back to the Clipboard API, and reports unsupported access, cancellation, or failure in `#share-status`. Keep the share button disabled while the asynchronous operation is pending and restore it in `finally`.
- Theme colors are CSS custom properties in `:root`, with light-mode overrides in `@media (prefers-color-scheme: light)`. Preserve both themes and the reduced-motion override when changing visual effects.
- Keep the centered column at a maximum width of 520px and the body text at 15px; preserve the narrow-screen adjustments.
