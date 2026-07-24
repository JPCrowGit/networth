# Net Worth Tracker

A static, single-page dashboard for a personal net worth Google Sheet:

- Historical net worth and asset-composition charts, read straight from
  the sheet.
- A Monte Carlo "what if" retirement simulator (2,000 randomized paths of
  annual market returns) — the one thing the sheet's own flat-average
  projection can't do.

No backend, no build step, no framework. `index.html` is the entire app.
The Google Sheet stays the single source of truth for actual net worth
history; this app never writes back to it.

## Setup

1. In the Google Sheet: **File > Share > Publish to web**, choose the
   sheet tab, format **Comma-separated values (.csv)**, click **Publish**.
   Copy the resulting URL.
2. Open the app (locally or deployed) and paste that URL into the
   "Published CSV URL" field, then click **Load data**.
   - The URL is remembered in your browser's local storage so you only
     need to paste it once per device.
   - The published link is reachable by anyone who has the exact URL
     (not indexed/searchable) — the sheet's aggregate totals are exposed,
     not any account numbers.
3. Fill in the Monte Carlo inputs (current age, retirement age, monthly
   contribution, expected return) and click **Run simulation**.

Expected sheet columns (matched by fuzzy name, not exact position):
`Date` (MM/YYYY), `Vanguard`, `Checking`, `Home Equity`, `Car Value`,
`Net Worth`. Net worth is taken directly from the sheet's own `Net Worth`
column rather than recomputed, since it already accounts for how you
track home equity. Rows whose `Date` isn't `MM/YYYY` (e.g. the sheet's
own `Proj. *` rows) are skipped.

## Running locally

No build step — just serve the directory and open it:

```
python3 -m http.server
```

then visit `http://localhost:8000`.

## Deploying

Push to `main` on GitHub and enable GitHub Pages (Settings > Pages >
Deploy from branch > `main` / root). No Actions workflow needed.
