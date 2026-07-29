# STACK — Crypto Portfolio & Market Terminal

A single-page, static crypto dashboard. No build step, no backend, no dependencies.
Live market data comes straight from public, keyless APIs (CoinGecko, alternative.me)
called from the browser at page load.

## What's in this repo

```
.
├── index.html      # the entire app (HTML + CSS + JS, self-contained)
├── vercel.json     # zero-config static deployment settings
└── README.md
```

## Deploy — GitHub → Vercel (recommended)

1. **Create a new GitHub repo**
   - Go to [github.com/new](https://github.com/new), name it (e.g. `stack-dashboard`), keep it public or private, don't initialize with a README (you already have one).

2. **Push this folder to it**
   ```bash
   cd stack-dashboard
   git init
   git add .
   git commit -m "Initial commit — STACK dashboard"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<your-repo>.git
   git push -u origin main
   ```

3. **Import into Vercel**
   - Go to [vercel.com/new](https://vercel.com/new)
   - Select "Import Git Repository" and pick the repo you just pushed
   - Framework preset: choose **Other** (it's static HTML — no build command, no output directory needed)
   - Click **Deploy**

   Vercel will give you a live URL (e.g. `stack-dashboard.vercel.app`) within seconds.

4. **Every future push to `main` auto-deploys** — no extra config needed.

## Deploy — Vercel CLI (alternative, no GitHub needed)

```bash
npm i -g vercel
cd stack-dashboard
vercel          # follow prompts, deploys a preview
vercel --prod   # promotes to your production URL
```

## Notes

- All data fetches (CoinGecko prices, alternative.me Fear & Greed Index) happen
  client-side in the visitor's browser — nothing to configure, no API keys, no
  environment variables required.
- If CoinGecko or alternative.me are unreachable or rate-limit the visitor, the
  dashboard falls back to a "data unavailable" state rather than showing stale
  or fake numbers.
- Not financial advice — this is a personal portfolio/news dashboard template.
