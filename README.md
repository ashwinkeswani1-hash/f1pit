# F1Pit — Setup Guide
**Fully free. Fully automated. Live in ~30 minutes.**

---

## Files in this zip

| File | What it does |
|---|---|
| `index.html` | The entire website |
| `races.json` | Race results — auto-updated each race |
| `fetch-results.js` | Fetches OpenF1 data + generates Groq commentary |
| `.github/workflows/update-races.yml` | Fires automatically 20 min after every 2026 race |

---

## Step 3 — Upload files to GitHub

In your empty `f1pit` repo on GitHub:
1. Click **Add file** → **Upload files**
2. Drag all 4 files/folders in (including the `.github` folder)
3. Click **Commit changes**

---

## Step 4 — Get your free Groq API key

1. Go to **console.groq.com** → Sign up free (no credit card)
2. Click **API Keys** → **Create API key**
3. Copy the key

Then in GitHub:
1. Your repo → **Settings** → **Secrets and variables** → **Actions**
2. Click **New repository secret**
3. Name: `GROQ_API_KEY`
4. Value: paste your key
5. Click **Add secret**

---

## Step 5 — Deploy to Vercel

1. Go to **vercel.com** → Sign up with GitHub
2. Click **Add New Project** → Import your `f1pit` repo
3. Click **Deploy** — done, no config needed
4. Vercel gives you a URL instantly (e.g. `f1pit.vercel.app`)

Every time `races.json` is updated → Vercel auto-redeploys → site updates in ~30 seconds.

---

## Step 6 — Connect your domain

1. In Vercel → your project → **Settings** → **Domains**
2. Add your domain (e.g. `f1pit.live`)
3. Vercel shows you 2 DNS records to add
4. In your domain registrar → DNS settings → add those 2 records
5. Wait 5–10 min → your site is live at your domain

---

## How automation works

GitHub Actions fires automatically ~20 minutes after each race ends.
All 24 race times for 2026 are hardcoded in the workflow file.

It:
1. Calls **OpenF1** → gets race result (free, no key needed)
2. Calls **Groq** → generates witty commentary (free tier)
3. Updates `races.json` and commits
4. Vercel detects commit → redeploys → site updates

You do nothing. Check the site Monday morning, result is there.

---

## Manual trigger

If a race was missed: GitHub repo → **Actions** → **Update Race Results** → **Run workflow**

---

## Updating standings manually

After each race, update the `DRIVERS` and `TEAMS` arrays in `index.html`.
Search for `const DRIVERS` — it's clearly labelled.

---

## Total cost

| Item | Cost |
|---|---|
| GitHub | Free |
| Vercel | Free |
| OpenF1 API | Free |
| Groq API | Free |
| Domain | ~$6–10/year |
