# Copilot instructions

## Project shape

This is a dependency-free, single-page quiz. The HTML, responsive styling, theme rules, question data, and application logic all live in the root `index.html`; open that file directly in a browser to run it. There is no build or server step.

The script keeps the quiz state (`currentQuestion`, `score`, and `answered`) in memory. `renderQuestion()` builds answer buttons from the `questions` array, `chooseAnswer()` handles feedback and progress, `showResults()` renders the final score and reaction, and `restart()` resets the quiz. Keep changes consistent across these transitions rather than adding a second state path.

## UI and accessibility conventions

- Keep the page self-contained: do not introduce a framework, package dependency, network-loaded asset, or server requirement.
- Use the CSS custom properties in `:root` for shared colors, and provide matching overrides in `@media (prefers-color-scheme: dark)`. Preserve the existing system light/dark theme behavior.
- Respect `@media (prefers-reduced-motion: reduce)` when adding animation or transitions.
- Answers and navigation are native buttons. Preserve keyboard focus visibility, disabled answered choices, the live feedback and score regions, and the progress bar's accessible name and `aria-valuenow`.
- Keep question content in the `questions` data array and update its answer indices and explanatory facts together when editing a question. Render answer text with `textContent` rather than treating question data as HTML.

## Build, test, and lint

There are no defined build, lint, or automated test commands, package manifest, or test runner. To run the app, open `index.html` directly in a browser. For a manual smoke test, answer questions correctly and incorrectly, check score and progress after each answer, finish all ten questions to inspect the results screen, and use **Explore again** to verify reset behavior. There is no automated single-test command.
