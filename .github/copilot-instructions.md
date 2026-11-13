# Copilot instructions

## Project shape

This repository is a dependency-free static web app. The complete application is in
`index.html`; it contains the semantic HTML, inline CSS, and inline JavaScript for the
Orbit Quest space quiz. There is no package manifest, bundler, server, automated test
suite, or lint configuration.

The page has three UI states:

- The intro section (`#intro`) is shown initially.
- The quiz section (`#quiz`) is activated after starting and renders one question at a time.
- The results section (`#results`) is activated after the tenth answer.

Quiz content is stored in the `questions` array. `current`, `score`, and `answered`
are the application state. `renderQuestion()` rebuilds the answer buttons from the
current question; `chooseAnswer()` disables all answers, marks the correct/selected
answers, updates the score, and reveals the next button; `showResults()` populates
the final score and message.

## Run and validate

There are no build, test, or lint commands. Open `index.html` directly in a browser;
it is intentionally designed to run without a server or build step. The integrated
browser can load it with a `file:///` URL.

For a focused manual smoke test:

1. Start the quiz and confirm question 1, the progress bar, and `0 pts` appear.
2. Select a wrong answer and confirm the correction feedback appears without increasing
   the score.
3. Select a correct answer on the next question and confirm the score increments.
4. Use keyboard focus/Tab navigation through the native buttons and activate controls
   with the keyboard.
5. Complete all 10 questions and confirm the results view shows the final score,
   score-dependent message, trophy emoji, and restart button.
6. Toggle the theme from both the intro and quiz/results states and confirm the
   theme-aware colours remain readable.

## Conventions to preserve

- Keep the app self-contained in `index.html`; do not introduce a framework, package
  manager, server, or build tool unless the project requirements change.
- Use the existing CSS custom properties in `:root` and `[data-theme="light"]` for
  colours, surfaces, text, accents, and shadows. Theme changes are made by setting
  `document.body.dataset.theme`.
- Keep quiz answers zero-based in each question object's `answer` field. The answer
  buttons are generated from `options`, and the displayed A-D key is derived from
  the array index.
- Preserve the current state model and rendering flow when changing quiz behaviour:
  update state, call `renderQuestion()` for a new question, and use the existing
  feedback/result elements rather than adding duplicated UI state.
- Use native `<button>` controls for all actions so the quiz remains keyboard
  focusable. Keep the existing `aria-label` on the theme toggle, `aria-live` on the
  quiz section, and `role="status"` on feedback.
- Keep decorative layers (`body::before` hex grid and `.stars`) non-interactive with
  `pointer-events: none`; preserve their stacking order behind `main`.
- Follow the existing visual language: `Space Grotesk` for headings/display text,
  `DM Sans` for body text, rounded translucent cards, gradients, restrained motion,
  and responsive rules under `520px`.
- Keep visual-only emoji and decorative elements from becoming required information;
  question text, answer text, feedback, and scores must remain understandable without
  relying on emoji or colour alone.
