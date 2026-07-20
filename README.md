# Retirement Planner

A household retirement planning tool with full tax modelling, RMD calculations, Roth conversion analysis, and portfolio optimisation.

## Features

- **Year-by-year projection** — combined household portfolio from today through end of life
- **Full tax engine** — 2024 federal brackets (MFJ & Single), LTCG, NIIT, state income tax
- **RMD modelling** — IRS Uniform Lifetime Table, SECURE 2.0 age-75 start for those born 1960+
- **Roth conversion planner** — bracket-ceiling strategy with before/after comparison
- **Portfolio optimiser** — sweeps 64 SSN-age × Roth-ceiling combinations, ranked by final estate
- **Three scenarios** — Conservative (Base−2%), Base, Optimistic (Base+2%)
- **Excel export** — year-by-year projection + inputs worksheet (SpreadsheetML)
- **Multi-user auth** — Supabase-backed accounts, multiple named plans, auto-save
- **Guest mode** — works offline with localStorage, no account required

## Versions

| Version | Description |
|---------|-------------|
| v0.1    | Initial single-file implementation (localStorage, single household) |
| v0.2    | Multi-user auth (Supabase), account settings, guest mode |
| v0.3    | Multiple named plans, plan switcher, auto-save |
| v0.4    | Onboarding wizard, data isolation, account deletion, per-account contributions |
| v0.5    | Deployed to Vercel — public web app |

## Roadmap

- [x] Phase 1 — Multi-user auth (Supabase), account create / delete / settings
- [x] Phase 2 — Multiple named plans per user, auto-save, plan switcher
- [x] Phase 3 — Generalise UI, onboarding wizard, per-account contributions, Edge Function account deletion
- [x] Phase 4 — Web deployment (Vercel + custom domain)

## Running Locally

```bash
npx serve . -p 3010
```

Then open `http://localhost:3010` in your browser.

> **Note:** Supabase auth requires `http://` (not `file://`). Always use the served URL.

## Deployment (Vercel)

The app is a pure static single-file HTML — no build step required.

```bash
npm i -g vercel
vercel --prod
```

Vercel project settings:
- **Framework Preset:** Other
- **Build Command:** *(leave empty)*
- **Output Directory:** `.` (root)

After first deploy, add the production URL to Supabase:
1. Supabase dashboard → Authentication → URL Configuration
2. **Site URL** → set to your Vercel URL (e.g. `https://retirement-planner.vercel.app`)
3. **Redirect URLs** → add `https://retirement-planner.vercel.app/**`

## Supabase Setup

See [`SUPABASE_SETUP.md`](SUPABASE_SETUP.md) for full step-by-step instructions.
