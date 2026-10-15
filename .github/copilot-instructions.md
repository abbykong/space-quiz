# Orbit space quiz

## Running and checking

Open `index.html` directly in a browser; from PowerShell in the project root:

```powershell
Start-Process .\index.html
```

For the integrated browser, open the workspace's `index.html` using its absolute `file:///` URL. Reload after edits.

Validation is browser-based. For a focused score/feedback check, reload, choose Mars on question 1, and verify one point, green feedback, disabled choices, and progress of 1/10. Reload and choose Venus to check zero points, red shake feedback, and Mars revealed as correct.

For the full flow, the correct zero-based answer indices are `[1, 2, 3, 0, 2, 1, 3, 0, 2, 1]`. Verify results after exactly ten answers and replay resetting the score, progress, and question. Check rank boundaries at 4/10, 5/10, 7/10, and 8/10. Exercise native Tab/Shift+Tab and Enter/Space when browser tooling supports real key input; programmatic focus and `.click()` checks do not verify native keyboard navigation.

## Architecture

The application is entirely in `index.html`: inline CSS, semantic HTML, inline SVG artwork, and a plain browser script. Keep it usable directly from disk with no server, dependencies, external fonts, or network requests.

The `questions` array contains ordered records with `topic`, `question`, four `answers`, a zero-based `correct` index, and an explanatory `fact`. State lives in `current`, `score`, and `answered`; reloading starts a fresh quiz.

`showQuestion()` creates answer buttons, `selectAnswer()` locks the question and displays feedback, `updateProgress()` synchronizes the score and completion indicator, and `showResults()` switches from quiz to results. Next advances only after an answer; replay resets state. The `$` helper resolves the HTML IDs that connect these functions to the page.

## Behavior and presentation conventions

- Use American English spelling in user-facing text, documentation, and new comments.
- Code comments should explain intent or non-obvious decisions. Never add comments that merely describe what the code does.
- One correct answer earns one point; incorrect answers earn zero. Completion measures questions answered, not correct answers. Preserve the `answered` guard and disabled buttons to prevent double-counting.
- Result tiers use accuracy: Commander at 80% or above, Navigator at 50% or above, otherwise Cadet. Each tier has its own emoji and message.
- When changing question count, synchronize the array, intro copy, progress bar's `aria-valuemax`, and final-score denominator. Other counts and accuracy calculations already use `questions.length`.
- Theme colors come from `:root` custom properties overridden by `prefers-color-scheme: dark`. Reuse these tokens for UI surfaces and feedback. The centered `.shell` is capped at 540px; body text is 15px sans-serif, with a monospace mission-control treatment scoped to `#question`.
- Correct answers use `.correct` with the green `pop` animation; incorrect selections use `.wrong` with red `shake`. Reveal the correct answer even after an incorrect selection, and keep the fact visible until Next.
- The star field uses non-interactive `body` pseudo-elements beneath `.shell`, with twinkling enabled only under `prefers-reduced-motion: no-preference`. The reduce-motion rule disables all animations and transitions, including pseudo-elements.
- Preserve native answer buttons, the answer group's `aria-labelledby`, feedback's `role="status"`, live score announcements, and progress ARIA values. Focus moves to Next after answering, the question heading after advancing/replaying, and the results heading on completion; headings use `tabindex="-1"` for programmatic focus.
- Use `textContent` and DOM creation for question/answer/fact content. Toggle screen visibility with `hidden`, supported by `[hidden] { display: none !important; }`.
