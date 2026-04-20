# CashFlow Web Deploy Bundle

Everything in `public/` is ready to push to your `cash-flow-red` Vercel repo on GitHub.
Vercel will auto-deploy within 30 seconds of the push.

## Contents

| File | URL after deploy | Purpose |
|---|---|---|
| `public/index.html` | `cash-flow-red.vercel.app/` | Main CashFlow app (the full prototype) |
| `public/couriers.html` | `cash-flow-red.vercel.app/couriers.html` | Courier waitlist landing page |
| `public/privacy.html` | `cash-flow-red.vercel.app/privacy.html` | Privacy Policy (Apple-mandatory) |
| `public/terms.html` | `cash-flow-red.vercel.app/terms.html` | Terms of Service |
| `public/support.html` | `cash-flow-red.vercel.app/support.html` | Support / Help Centre (Apple-mandatory) |

## What's in this version

All of the following are baked into these files:

- **Fee cap at 20%** (was 50%) — both Courier dashboard and CashPoint slider
- **Cash preset values**: £20, £40, £60, £80, £100, £150, £200, £300, £500 — applied to Request amount, Courier cash-on-hand, and CashPoint float
- **CashPoint free-typing input removed** — presets are now the only way to set cash values
- **Colour-scheme meta tag** — prevents browser auto-dark mode from messing with the rendering
- **Footer FCA reference removed** + **FAQ regulatory language softened** (no overpromising pre-FCA)
- **Footer legal links wired** — Privacy / Terms / Support links now work
- **Terms of Service §7** reflects the new 1–20% fee range

## How to push this to GitHub (3 minutes)

### Option A — command line
```bash
# In your cash-flow-red repo
cd /path/to/cash-flow-red

# Copy all five files over
cp /path/to/downloaded/public/*.html public/

# Commit and push
git add public/*.html
git commit -m "feat: 20% fee cap + preset cash values + legal pages"
git push
```

### Option B — GitHub web UI
1. Go to `github.com/YOUR_USERNAME/cash-flow-red`
2. Navigate to the `public/` folder
3. Drag and drop all five `.html` files from this bundle (GitHub accepts drag-and-drop)
4. Commit message: `feat: 20% fee cap + preset cash values + legal pages`
5. Commit directly to main

Vercel will auto-deploy within ~30 seconds of either approach.

## After the push — verify these URLs

Open each in your browser and confirm:

- https://cash-flow-red.vercel.app/ → main app loads on dark background
- https://cash-flow-red.vercel.app/couriers.html → waitlist page, amber accents
- https://cash-flow-red.vercel.app/privacy.html → privacy policy
- https://cash-flow-red.vercel.app/terms.html → terms of service
- https://cash-flow-red.vercel.app/support.html → support page

If any of them 404, your Vercel project root directory setting may need to be `public/` — check Vercel dashboard → Settings → Build & Development → Output Directory.

## Files NOT in this bundle (they deploy elsewhere)

These don't go to GitHub/Vercel — they go to other systems:

| File | Deploys to |
|---|---|
| `003_courier_waitlist.sql` | Supabase SQL Editor (one-time paste) |
| `send-courier-welcome.ts` | Supabase Edge Function (`supabase functions deploy`) |
| `cashflow-ios.zip` | Your local machine → EAS Build → App Store |

## Spot-check before committing

If you want belt-and-braces: open each file locally first by double-clicking.

- `public/index.html` should load with dark background and show the login screen
- `public/couriers.html` should load with dark background, amber "Deliver cash" hero, and a sign-up form on the right

If either looks wrong (e.g. white background), do a hard refresh (Cmd+Shift+R / Ctrl+Shift+R) — browser cache bug, not a file issue.
