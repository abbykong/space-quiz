# Orbit space quiz

Orbit is a ten-question space exploration quiz with instant answer feedback,
explanatory facts, progress tracking, and optional shuffled question order.
Each correct answer earns one point. Finish as a Cadet, Navigator (50% or
higher), or Commander (80% or higher). From the results, show missed answers to
review your choices, the correct answers, and their explanations, or replay to
explore again with a fresh review.

The responsive interface supports light and dark themes, reduced motion, and
keyboard navigation. Everything lives in `index.html`: HTML, CSS, JavaScript,
and SVG artwork. There are no dependencies, external assets, or network requests
required to play.

## Run locally

Clone or download the repository, then open `index.html` in any modern browser.
From PowerShell in the project root:

```powershell
Start-Process .\index.html
```

No installation, build step, or development server is needed. Reload the page
after editing the file; reloading also starts a fresh quiz.

## GitHub Pages

Play online at **https://abbykong.github.io/space-quiz/**.

The [Pages workflow](.github/workflows/pages.yml) checks that `index.html` is
nonempty and packages it as a Pages artifact on pull requests and pushes to
`main`. Only `index.html` is published, not the repository's documentation or
configuration. After a push to `main`, the deployment job publishes the artifact
to the `github-pages` environment. You can also run the workflow manually from
the Actions tab on `main`.

In repository **Settings > Pages**, the build and deployment source must be
**GitHub Actions**. Deployment status and the published URL appear in the
workflow run and the repository's `github-pages` environment.
