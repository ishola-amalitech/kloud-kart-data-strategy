# ADR-004: Revenue has one definition, owned by Finance, calculated once in code and published as the only Monday report

- **Status:** Draft
- **Version:** 0.1
- **Date:** 12 November 2026
- **Decision owner:** Data strategy lead; client review: Head of Operations and Finance lead

## Context

Nana rebuilds her Monday numbers from CSV exports, Finance keeps its own spreadsheet, and the two never match. The brief gives no written definition of revenue, no agreed cut-off, and no routine comparison with the source. This is the problem most likely to embarrass Nana in front of the board, so it needs a firm answer, and Nana is unavailable to give one.

## Decision

I am proposing this definition; Finance must sign it by 29 January 2027. **Revenue for a period** is the value of goods delivered in that period, after discounts, minus refunds and returns processed in that same period, and excluding VAT, levies and delivery fees. Periods end at midnight Accra time. A refund reduces the month it is processed in, so closed months never change. "Orders placed" is reported separately under a different name so two numbers never share one label. Nigeria revenue is shown in cedis at the month-end rate Finance sets. If delivery date is not recorded, dispatch date is used until it is. The definition is implemented once, as a version-controlled SQL file with automatic tests, and the two existing spreadsheets are retired once three month-ends match.

## Alternatives considered

### Alternative A: Keep both spreadsheets and reconcile them every month

- **How it would work:** Operations and Finance continue as they are and compare totals at month-end.
- **Why it is attractive:** No one gives up their own tool and nothing needs building.
- **Why rejected:** Reconciliation is the problem, not the answer. It costs 1–2 hours a week now, the two numbers keep existing side by side in front of the board, and each month the gap has to be explained again.

### Alternative B: Buy a metrics or business-intelligence tool and let it settle the definitions

- **How it would work:** Install a tool with a "single source of truth" feature and configure revenue in it.
- **Why it is attractive:** It looks like a one-step fix and gives Nana a polished dashboard.
- **Why rejected:** The disagreement is about what to count, not about software. A tool bought before the definition is agreed would only display the dispute faster. The definition comes first, and the tool, if needed at all, comes later.

## Consequences

- **What this buys:** One number, one page of explanation, and a month-end Nana can defend by phone.
- **What this costs:** The first report will probably differ from figures already shown to the board, so we publish a three-month bridge from old to new. Someone's number will be "wrong", which is a people problem I cannot fully solve in writing.
- **What it costs the client if I am wrong:** If the definition clashes with tax or audit treatment, it is a one-file change, but any figure already given to the board would have to be restated.
- **What would make me revisit this:** The company's accountant or auditor objects; marketplace or consignment sales arrive; Nigeria needs different tax treatment.

## What this survives

- **A refund spike:** Refunds hit the month they are processed, so past months stay closed.
- **Late data at month-end:** Reports are stamped "as at" a date and time, and the cut-off rule is written down.
- **The developer or analyst leaves:** The definition exists in plain English and in tested code.
- **Nana asks "why doesn't this match last quarter?":** The bridge answers it.
- **It does not survive** Finance refusing to sign. In that case, Nana's two spreadsheets stay, and I would escalate to the board as a governance issue, not a data one.
