# ADR-005: Customer lists leave the system only through one logged export, files expire after 30 days, and deletion follows a checklist within 5 working days

- **Status:** Accepted
- **Date:** 2026-11-12
- **Decision owner:** Ishola (consulting lead); client sign-off: Nana Adjei and a Finance lead named as answerable for customer-data requests

## Context

Marketing holds a list of about 300,000 people and nobody knows how many copies exist or where. Ghana's Data Protection Act gives people rights over their data, and the Data Protection Commission can require a response within 90 days when a deleted customer's data turns up. Today the company could not prove where a person's data is, so it could not prove it was deleted. I am not a lawyer; the points below need confirming with counsel.

## Decision

1. **One way out:** Customer lists are produced only by a single export that records who asked, why, how many rows, when, and where the file went. Each file carries an export ID.
2. **Expiry:** Every file expires after 30 days, and its owner confirms deletion. Marketing re-exports for each campaign instead of reusing old lists.
3. **A register:** One list names every place customer data lives (the shop, the replica, backups, the reporting database, any email tool, files) and who is answerable for each. It is complete by Friday 26 February 2027.
4. **Keep identity out of reporting:** The reporting database holds customer IDs only (ADR-002).
5. **Deletion checklist:** A deletion request runs the register's checklist: delete or anonymise in the shop, clear exports, and anonymise reporting rows so order totals survive. Target is 5 working days; backups roll off within 35 days, so full erasure completes well inside the 90-day limit.
6. **Suppression:** A minimal record of deleted people, subject to counsel's approval, stops them being re-added from an old file.

## Alternatives considered

### Alternative A: A written policy telling Marketing not to keep copies

- **How it would work:** Circulate a rule and rely on people to follow it.
- **Why it is attractive:** Free, quick, and no friction for Marketing.
- **Why rejected:** The current mess is what a policy with no tracking produces. There would be no evidence that copies were deleted, which is what a regulator asks for.

### Alternative B: Buy a customer data or consent platform first

- **How it would work:** Move the 300,000 contacts into a vendor tool that handles segments and consent.
- **Why it is attractive:** Marketing gets better tools and the vendor gives a consent trail.
- **Why rejected:** It puts everyone's data into a new vendor before the company knows where its data already is. The register must come first; a platform may follow.

## Consequences

- **What this buys:** A defensible answer to "where is this person's data, and when was it deleted?", and a plan that fits the 90-day window with room to spare.
- **What this costs:** Marketing loses the freedom to email themselves lists, and the developer builds one export and a deletion checklist (days, not weeks).
- **What it costs the client if I am wrong:** A complaint that finds data in a copy not on the register. The register cannot catch files created before it existed, which is why Q1 includes a hunt for existing copies.
- **What would make me revisit this:** More than about 5 deletion requests a month, a move to a vendor email platform, or counsel saying anonymising orders is not enough.

## What this survives

- **Twenty times more deletion requests:** At 1 a month, hand-run is fine. Above about 5 a month, the checklist is scripted in Q3.
- **A complaint during the Nigeria pilot:** Nigerian customers fall under Nigerian law too; counsel must confirm what applies.
- **A Marketing staff member leaves with a copy:** Watermarks and expiry make it traceable and shorter-lived; they cannot prevent it.
- **Tax or accounting records that must be kept:** Orders are anonymised, not deleted, pending counsel's view on retention.
- **It does not survive** an unregistered file on someone's personal device. Training and the export log reduce this risk but cannot remove it.
