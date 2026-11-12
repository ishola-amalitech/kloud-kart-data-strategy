# ADR-003: Real-time applies only to stock at checkout; every dashboard refreshes daily

- **Status:** Accepted
- **Date:** 2026-11-12
- **Decision owner:** Ishola (consulting lead); client sign-off: Nana Adjei

## Context

Investors asked about "real-time analytics", and a board member saw a live dashboard at another portfolio company. The brief says stock counts cannot go stale (that is how the company oversells) and that everything else can refresh daily. The root cause of the overselling is not documented, so I assume order, payment, cancellation and return events update stock at different moments.

## Decision

No streaming platform. Stock is made correct inside the shop: stock is reserved inside the checkout transaction, and every change to stock is written to one movement ledger. A light check runs every 15 minutes on the live database (a small, indexed query) and alerts the developer if the shop's stock count and the ledger disagree. Dashboards and reports refresh once a day by 06:00. If the developer's audit in December finds checkout already reserves stock safely, only the ledger check is added.

## Alternatives considered

### Alternative A: Stream changes from the shop into live dashboards

- **How it would work:** Capture every database change as it happens and feed live dashboards.
- **Why it is attractive:** It matches the investors' words and looks impressive in a board meeting.
- **Why rejected:** It needs new infrastructure and skills nobody here has. Nothing Nana decides changes between 06:00 and noon, so the speed buys nothing. It also would not fix overselling, because a dashboard displays stock but does not protect it.

### Alternative B: Hourly refresh for everything

- **How it would work:** Run the nightly build every hour.
- **Why it is attractive:** A cheap middle ground that sounds responsive.
- **Why rejected:** It adds load, creates an expectation of "fresh" numbers that nobody will act on, and leaves the real stock problem untouched.

## Consequences

- **What this buys:** Real-time where money is lost, daily where it is not, at almost no extra cost. A clear one-sentence answer for investors.
- **What this costs:** The developer must change checkout code, which is the riskiest part of the shop. Anyone who wants intraday sales figures has to wait or ask for a one-off.
- **What it costs the client if I am wrong:** If a team genuinely needs intraday figures (for example, a flash sale), the board hears "no" once and pays a small fix: an hourly refresh of one table, not a platform.
- **What would make me revisit this:** A named person describes a decision that loses money when data is more than a day old; flash sales become regular; stock discrepancies stay above the January baseline after the fix.

## What this survives

- **Flash-sale traffic of several times normal:** The reservation lock must be load-tested before the first flash sale. That is a condition of this ADR, not something I have proven.
- **The Nigeria pilot adds stock locations:** The ledger design allows per-location stock, but the checkout check is only as good as the rules the developer writes for it.
- **Replication lag:** Irrelevant to stock, because stock never reads from the replica (ADR-001).
- **It does not survive** a decision to hold stock in two systems at once. That would need its own ADR.
