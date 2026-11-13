# Improvement beyond the brief: a nightly check that the report agrees with the shop

## The problem it solves

The brief asks for one revenue number Nana and Finance can both trust. It does not ask how anyone will know that number is still right next month. The cause is one of the six "undercurrents" a plan can silently omit: **DataOps**. A nightly build can run perfectly and still deliver a wrong figure: a dropped day, an order counted twice, a changed amount. Nobody shouts when that happens. The first sign would be Finance's total drifting away from Nana's again, in front of the board.

## What I built

`improvement/reconcile_check.py`, with tests in `improvement/test_reconcile.py`. After the nightly build it compares the last 7 complete days of the reporting tables with the shop's copy and says, in plain words, whether it is safe to publish.

It makes four checks:

1. **Order counts match** for every day.
2. **Order values match** for every day, to the pesewa.
3. **Yesterday is in the report**, so a build that silently did not run is noticed.
4. **No order is counted twice.**

On a good night it prints one line: *"All 4 checks passed. Safe to publish the Monday report."* On a bad night it names the day and the figures that disagree, for example *"2026-11-08: shop 40 orders, report 37"*. It exits with an error code, so the nightly job can notify the developer and the data engineer.

**How it was tested.** Three automated tests pass. A healthy night passes; a night with lost orders, a wrong amount, a duplicate and a missed day trips all four checks; and a single wrong amount is caught on its own. Run `python3 reconcile_check.py --demo` to see both nights.

**What it has not been tested on.** There is no Kloud Kart data in this lab, so it ran only on made-up orders in a throwaway database. The table and column names (`orders`, `fact_orders`, `total_amount`) are stand-ins. Wiring it to the real replica and the reporting database is an early task for the data engineer.

## What it is worth to Kloud Kart

- **For Nana:** a published number she can stand behind. If a check fails, she is told before the board sees it, not after.
- **For Finance:** the month-end match in the roadmap (7 April and three in a row by 31 October) becomes something the system checks every night. It is not left to someone remembering to compare.
- **For the board:** a line in the one-year scorecard, "nights the report disagreed with the shop", which is a number they can ask for.
- **For the Data Protection Act position:** the principle that data be accurate gets a daily record of evidence.

I cannot put a cedi figure on it honestly. The revenue-mismatch exposure in the diagnosis (about GHS 146,000 for a 0.1% gap) is an exposure, not a measured loss, and this check is what stops a gap from going unnoticed.

## What it cost

- **My time:** about half a day to design, write and test. No licence or server cost; it uses only what Python already includes.
- **To put in service:** roughly 1–2 days for the data engineer to connect it to the real databases and add the alert, plus a 15-minute weekly look at failures.
- **What it does not do:** it cannot tell if the *definition* of revenue is wrong, only whether the report faithfully matches the shop. That is ADR-004's job. It also checks only totals by day, so two errors that cancel each other out would pass.
