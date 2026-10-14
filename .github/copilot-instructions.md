# Copilot instructions

## Build, test, and lint

- There are no configured build, test, or lint commands or dependencies.
- Run the app by opening `index.html` directly in a browser; it does not need a server.
- For browser smoke checks, verify answer selection and feedback, score and progress updates, manual advancement through all ten questions, results, and restart.

## Architecture

- The app is a self-contained static page. Markup, styles, quiz content, and stateful behavior all live in `index.html`; there is no bundler or runtime framework.
- The `questions` array is the source of truth for each prompt, its four choices, the zero-based correct-choice index, and the explanation shown after answering.
- The script renders one question at a time, updates the score and mission-progress display, reveals feedback, waits for the player to continue, and then shows results or resets the quiz.
- CSS custom properties in `:root` define the dark theme; `prefers-color-scheme: light` overrides them for light mode. Keep new colors aligned with these theme variables.

## Codebase conventions

- Keep application changes in the single self-contained `index.html` unless the user asks to change the architecture.
- Keep question data in the existing `questions` array. Choice indices are zero-based; update the question text, choices, answer index, and explanatory fact together.
- `questionIndex` tracks the current question, while progress represents completed questions. Keep the visible percentage, progress-bar width, `aria-valuenow`, and `aria-valuetext` in sync.
- Answer selection marks the correct choice, gives correct/incorrect feedback, and updates score only for correct answers. Do not auto-advance: the player reads the feedback and activates the continue button.
- Use native buttons for actions, retain the existing focus movement and live feedback behavior, and preserve semantic progress-bar attributes when changing quiz interactions.
- User-provided question and feedback text should be assigned as text, not interpolated into HTML. Preserve the reduced-motion media query when adding animations.
