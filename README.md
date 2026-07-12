# CI/CD Web App Pipeline

A small Node.js/Express app with a complete GitHub Actions pipeline demonstrating
lint → test → Docker build → push to GitHub Container Registry (GHCR) → automated deploy to Render.

![CI/CD Pipeline](https://github.com/guesmimontassar8-cloud/Full-CI-CD-Pipeline-for-a-Web-App/actions/workflows/ci-cd.yml/badge.svg)

🔗 **Live demo:** https://full-ci-cd-pipeline-for-a-web-app.onrender.com

## Architecture

- **Lint**: ESLint checks code style on every push and PR.
- **Test**: Jest + Supertest run unit tests against the Express app.
- **Build & Push**: On merge to `main`, a Docker image is built and pushed to
  `ghcr.io/guesmimontassar8-cloud/full-ci-cd-pipeline-for-a-web-app`, tagged with both
  the short commit SHA and `latest`.
- **Deploy**: On merge to `main`, a Render deploy hook is triggered automatically,
  redeploying the live app with the latest code.

## Tech stack

- Node.js 20 / Express
- Jest + Supertest for testing
- ESLint for linting
- Docker
- GitHub Actions
- GitHub Container Registry (GHCR)
- Render (hosting)

## Running locally

```bash
npm install
npm start        # runs on http://localhost:3000
npm test         # run tests
npm run lint      # run linter
```

## Running with Docker

```bash
docker build -t cicd-webapp-pipeline .
docker run -p 3000:3000 cicd-webapp-pipeline
```

## Setting this up on your own GitHub

1. Push this repo to GitHub.
2. Go to **Settings → Actions → General → Workflow permissions** and enable
   "Read and write permissions" so the workflow can push to GHCR.
3. Create a free Web Service on [Render](https://render.com), connecting it to
   this repo (Render auto-detects the `Dockerfile`).
4. Copy the Render **Deploy Hook** URL from your service's Settings tab.
5. Add it as a GitHub secret named `RENDER_DEPLOY_HOOK` under
   **Settings → Secrets and variables → Actions**.
6. Push to `main` and watch the **Actions** tab run the full pipeline —
   lint → test → build & push → deploy.
7. Your image will appear under your GitHub profile's **Packages** tab, and
   your live app will update automatically at your Render URL.
