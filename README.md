# CI/CD Web App Pipeline

A small Node.js/Express app with a complete GitHub Actions pipeline demonstrating
lint → test → Docker build → push to GitHub Container Registry (GHCR) → deploy.

![CI/CD Pipeline](https://github.com/YOUR_USERNAME/cicd-webapp-pipeline/actions/workflows/ci-cd.yml/badge.svg)

## Architecture

```
push/PR --> lint --> test --> build & push Docker image (main only) --> deploy
```

- **Lint**: ESLint checks code style on every push and PR.
- **Test**: Jest + Supertest run unit tests against the Express app.
- **Build & Push**: On merge to `main`, a Docker image is built and pushed to
  `ghcr.io/YOUR_USERNAME/cicd-webapp-pipeline`, tagged with both the short commit
  SHA and `latest`.
- **Deploy**: Placeholder step you can wire up to Render, Railway, Fly.io, or a
  self-hosted server.

## Tech stack

- Node.js 20 / Express
- Jest + Supertest for testing
- ESLint for linting
- Docker
- GitHub Actions
- GitHub Container Registry (GHCR)

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
3. Push to `main` and watch the **Actions** tab run the pipeline.
4. Your image will appear under your GitHub profile's **Packages** tab.
5. (Optional) Add a deploy hook secret (e.g. `RENDER_DEPLOY_HOOK`) in
   **Settings → Secrets and variables → Actions** and uncomment the deploy step
   in `.github/workflows/ci-cd.yml`.
