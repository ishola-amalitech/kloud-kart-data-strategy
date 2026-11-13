# ADR-001: All reporting and exports read from a replica on the second server, never from the live shop database

- **Status:** Draft
- **Version:** 0.1
- **Date:** 12 November 2026
- **Decision owner:** Data strategy lead; client review: Head of Operations

## Context

Orders, stock and customer accounts share one MySQL database, on the same box as the website. Twice last month a Monday export slowed the shop to a crawl. A second server or read replica is already pre-approved, and MySQL and the site must stay up while we change anything.

## Decision

Stand up a MySQL read replica on the pre-approved second server by 11 January 2027. From that date every report and export reads only from the replica, and the database logins that people use for exports on the live database are removed. Monitor replication lag and show each report's data time. If lag exceeds the provisional 15-minute warning threshold, withhold affected reports and exports, alert the developer and data engineer, and resume only after the replica is within threshold and its sync health is confirmed. Never fall back to reporting reads on the production database. The replica is never used to answer "how much stock is there?".

## Alternatives considered

### Alternative A: Keep exporting from the live database, but throttle and schedule it

- **How it would work:** Run the Monday export with row limits, low priority and a quiet-hours window; add a query timeout.
- **Why it is attractive:** Costs nothing and could be done in a day.
- **Why rejected:** Nana needs Monday-morning numbers, which is not a quiet hour. It fixes this one export but not the next analyst query, and every other query still shares the box's CPU and disk. A 15–20% yearly growth rate steadily narrows any safe window.

### Alternative B: Nightly dump of the live database, restored onto the second server

- **How it would work:** A scheduled full backup is copied and restored on the second box; reports use that copy.
- **Why it is attractive:** No replication to learn, and no lag to explain.
- **Why rejected:** Dumping 40 GB loads the live box every night, which recreates the original problem at a smaller scale, and reports would be a day old by definition.

## Consequences

- **What this buys:** The cause of the slowdowns is removed, not managed. Reporting can grow without touching the shop.
- **What this costs:** One more server to pay for and run (my estimate GHS 2,500–4,500 a month, to be quoted), and replication to learn for a one-developer team. Some schema changes on the live database can break replication and need a runbook.
- **What it costs the client if I am wrong:** If replication breaks, reports go stale but the shop is unaffected, so the failure is embarrassing, not expensive. If the live box itself is the real bottleneck, the replica will not fix general slowness, which is why we time the site before and after.
- **What would make me revisit this:** Replication lag regularly above 15 minutes; the replica above 70% CPU for hours; the database passing about 150 GB.

## What this survives

- **Traffic doubles:** Replication adds a small, steady load to the live box, while reports add none. It is the right shape for growth.
- **Nigeria pilot spikes:** Same, as long as the shop's own capacity is sized separately; this ADR does not size the shop.
- **The developer is away:** The runbook and lag alert go to two people, not one.
- **The replica dies:** The shop is unaffected, and reports return once it is rebuilt from the live database.
- **It does not survive** the live server itself failing. That needs tested off-box backups, which is outside this ADR but is a Q1 task for the developer.
