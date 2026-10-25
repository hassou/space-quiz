# Orbit — Space Exploration Quiz

Orbit is a small, dependency-free space exploration quiz. Answer questions about space, get immediate feedback and a fact for each answer, and see your final score at the end.

## Run locally

No installation or build step is required. Open `index.html` in a browser, or serve the repository root with Python:

```powershell
python -m http.server 8000
```

Then visit <http://localhost:8000>.

## Deployment

GitHub Actions publishes the static site to GitHub Pages whenever a commit reaches `main`. The workflow uploads the repository root as the Pages artifact; no compilation is needed.
