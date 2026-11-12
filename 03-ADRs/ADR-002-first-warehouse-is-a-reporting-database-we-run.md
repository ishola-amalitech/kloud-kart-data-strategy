# ADR-002: The first warehouse is a separate reporting database on the second server, not a cloud warehouse

- **Status:** Accepted
- **Date:** 2026-11-12
- **Decision owner:** Ishola (consulting lead); client sign-off: Nana Adjei

## Context

The developer wants to "just buy Snowflake or BigQuery". Finance flinched. The company has about 40 GB of structured data, one developer who knows PHP and MySQL, nobody who has run a warehouse, and a board that has budgeted two hires. Customer data is covered by Ghana's Data Protection Act.

## Decision

Run the reporting database as a second MySQL instance on the second server, next to the replica from ADR-001 but separate from it. Every night it is rebuilt from the replica with plain SQL scripts kept in version control, copying raw tables first and then building the reporting tables from them. It holds no names, phone numbers or email addresses, only customer IDs. We buy a managed cloud warehouse only when a named trigger fires (see below). I assume MySQL 8 or later; if the shop runs 5.7, upgrading the reporting instance comes first.

## Alternatives considered

### Alternative A: Buy Snowflake or BigQuery now

- **How it would work:** Load a copy of the shop data into a managed warehouse each night and point reports at it.
- **Why it is attractive:** There is no server to run, it scales well past our size, and most reporting tools connect to it. At 40 GB the storage bill is small, so cost alone is not my objection.
- **Why rejected:** The person who would run it is the developer who already runs the shop. It brings a new vendor, access settings and billing to watch, and per-query billing can surprise a team new to analytics. Moving customer data out of Ghana raises a Data Protection Act question we have not answered. None of the benefits matter at this size.

### Alternative B: A lakehouse

- **How it would work:** Land raw files in cloud storage and query them with a lakehouse engine.
- **Why it is attractive:** It suits very large or messy data and sounds modern to investors.
- **Why rejected:** Kloud Kart's data is small and tidy: orders, stock, customers. A lakehouse adds the most moving parts for the least benefit.

## Consequences

- **What this buys:** A fixed, predictable cost, a tool the developer already knows, customer identity staying out of reporting, and one fewer vendor.
- **What this costs:** Analytical SQL is somewhat clumsier on MySQL, and we run the server and its backups ourselves. The replica and the reporting database share one server, so a heavy nightly build can slow replication; builds run at 02:00 and are timed.
- **What it costs the client if I am wrong:** About 2–4 weeks to move to a managed warehouse, because the logic is plain SQL in version control and raw tables are kept. That is cheap insurance.
- **What would make me revisit this:** Reporting data past 150 GB; the nightly build taking over 3 hours; a second large data source that needs joining; or the second hire recommending a move after their first 90 days.

## What this survives

- **Data doubles (for example, the Nigeria pilot succeeds):** At 20% a year, 40 GB takes about four years to reach 80 GB. Even a faster doubling is well inside the 150 GB trigger.
- **The developer leaves, or a hire leaves:** Plain SQL and a one-page definition per table can be read by the next person.
- **Finance's concern about cost:** The fixed bill is easy to defend, and the migration path is already costed.
- **It does not survive** a requirement for many people querying at once or for large unstructured data. Either would trigger the move, and the plan does not pretend otherwise.
