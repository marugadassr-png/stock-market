# Paw Pets

Static marketing site for Paw Pets. Plain HTML/CSS, no build step required.

```
paw-pets-app/
├── index.html              ← the site (served from repo root)
├── vercel.json             ← deploy config
├── package.json
├── .github/
│   └── workflows/
│       └── deploy.yml      ← CI workflow that deploys to Vercel on push
└── .gitignore
```

This is a zero-build static site — `index.html` sits at the project root, so Vercel serves it directly with no output-directory configuration needed.

## 1. Push this to GitHub

```bash
git init
git add .
git commit -m "Initial commit: Paw Pets site"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repo>.git
git push -u origin main
```

## 2. Connect to Vercel

You have two ways to deploy — pick one. Don't set up both, they'll conflict.

### Option A — Vercel's native Git integration (simplest, recommended)

1. Go to [vercel.com/new](https://vercel.com/new) and import the GitHub repo.
2. Framework preset: choose **Other**. Leave Build Command and Output Directory blank/default — there's nothing to build, `index.html` is served straight from the repo root.
3. Deploy. Vercel will now auto-deploy every push to `main` (and generate preview URLs for PRs) on its own — **you can delete `.github/workflows/deploy.yml`** in this case, since Vercel is already watching the repo directly.

### Option B — GitHub Actions workflow (this repo's `deploy.yml`)

Use this if you want deploys to run through GitHub Actions instead of Vercel's own Git integration (e.g. for custom CI steps, gating, or org policy reasons).

1. In Vercel, run this once locally to link the project and generate IDs:
   ```bash
   npm i -g vercel
   vercel link
   ```
   This creates a `.vercel/project.json` with your `orgId` and `projectId`.

2. Get a Vercel access token: [vercel.com/account/tokens](https://vercel.com/account/tokens).

3. In your GitHub repo, go to **Settings → Secrets and variables → Actions** and add:
   - `VERCEL_TOKEN` — the token from step 2
   - `VERCEL_ORG_ID` — from `.vercel/project.json`
   - `VERCEL_PROJECT_ID` — from `.vercel/project.json`

4. **In the Vercel dashboard, turn off "Auto Deploy" from Git** for this project (Project Settings → Git), so Vercel doesn't double-deploy alongside the Action.

5. Push to `main` — the workflow in `.github/workflows/deploy.yml` will build and deploy automatically. Pull requests get preview deployments; pushes to `main` go to production.

## Local preview

```bash
npm run dev
```

Serves the project root at `http://localhost:3000`.
