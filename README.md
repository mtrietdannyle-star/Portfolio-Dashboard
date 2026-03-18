# Portfolio Monitor — Bloomberg Terminal Theme

Personal portfolio dashboard with Bloomberg Terminal aesthetics, live Yahoo Finance data (1-minute refresh), blended benchmark tracking, and CTR calculations.

## Features

- **Live Yahoo Finance data** — auto-fetches every 60 seconds with proxy rotation to avoid throttling
- **Blended benchmark** — define N benchmark components with custom weights (e.g., 60% SPY / 40% ACWI). Weights are normalized automatically. Daily alpha calculated vs blended benchmark return.
- **Bloomberg Terminal UI** — black background, orange accents, Helvetica, dense data layout
- **Portfolio vs Benchmark chart** — cumulative return performance (add daily snapshots to build)
- **Holdings table** — daily P&L, total return, weight, and CTR for every position
- **ETF & Stock sleeve breakdowns** — separate performance metrics per sleeve
- **Live ticker panel** — real-time prices for all positions + benchmark components
- **Rebalance log** — track buys, sells, trims, rotations with thesis notes
- **Data persistence** — localStorage + JSON export/import

## Deploy to GitHub Pages

1. Create a new GitHub repository
2. Upload `index.html` to the repo root
3. Go to **Settings → Pages → Source → main branch / root**
4. Live at `https://<username>.github.io/<repo-name>/`

## Blended Benchmark

Click **CFG** to configure benchmark components:

| Ticker | Weight | Label |
|--------|--------|-------|
| SPY    | 60     | S&P 500 |
| ACWI   | 40     | MSCI ACWI |

Weights don't need to sum to 100 — they're normalized automatically. The blended daily return is the weighted average of each component's daily change. The summary strip shows daily alpha (portfolio return minus blended benchmark return).

For the performance chart, the snapshot form auto-populates the blended benchmark value from the live feed.

## API Details

Yahoo Finance's unofficial v7 quote API has no formal rate limit or authentication requirement. At 1-minute intervals, the dashboard rotates across three CORS proxies (corsproxy.io, allorigins.win, codetabs.com) to distribute load. Falls back to v8 chart endpoint per-symbol if the batch endpoint fails. The status indicator and fetch counter in the top bar show connection health.

## CTR Calculation

**Contribution to Return** = Position Weight × Position Daily Return

Shows how many basis points each holding contributed to portfolio daily performance.
