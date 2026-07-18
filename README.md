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

## Versions

| Version | Description |
|---------|-------------|
| v0.1    | Initial single-file implementation (localStorage, single household) |

## Roadmap

- **Phase 1** — Multi-user auth (Supabase), account create / delete / settings
- **Phase 2** — Multiple named plans per user, auto-save, plan switcher
- **Phase 3** — Generalise UI (remove hard-coded names, generic Person 1 / Person 2)
- **Phase 4** — Web deployment (Vercel + custom domain)

## Running Locally

Open `index.html` directly in any modern browser — no build step required.
