# ADR-003: Reassess stock controls and freshness after auditing operational flows

- **Status:** Draft
- **Version:** 0.1
- **Date:** 13 November 2026
- **Decision owner:** Kloud Kart leadership, with input from the shop developer

## Context

The business has identified a risk that stale stock could lead to orders that cannot be fulfilled, but the cause and the decisions staff need to make from stock information have not yet been established. Possible causes include checkout reservation, order/payment/cancellation/return handling, stock adjustments, or other operational processes. A live dashboard or data pipeline may report a discrepancy, but reporting by itself does not prevent an invalid sale.

Specific stock controls and refresh cadence should not be prescribed before the stock-flow audit or freshness requirements have been confirmed. Streaming and hourly refreshes should likewise be evaluated against actual requirements rather than accepted or rejected in advance.

## Decision

The shop application remains the authority for stock availability and checkout decisions. The data warehouse is for analytical use and must not become a second source of truth for live stock.

First audit the current stock flows and agree which operational decisions need support. Then choose the needed controls, monitoring, data freshness, and any staff-facing stock or low-stock interface based on those findings. This ADR does not prescribe a streaming architecture, refresh interval, alert cadence, ledger design, or admin dashboard.

Any change to checkout or other shop application behavior is owned by the shop developer. The data engineer may support warehouse analysis, agreed business rules, and measurement of outcomes, but does not own operational stock controls.

## Consequences

- The team avoids building a dashboard or pipeline as a substitute for fixing the operational cause of overselling.
- The stock solution and freshness requirement remain open until the audit and business needs are understood.
- Historical stock analysis may use warehouse data under an agreed refresh approach; live availability decisions stay in the shop application.

## What would make us revisit this

- The audit identifies the operational cause of overselling or recurring count discrepancies.
- Staff identify a concrete decision that requires stock information at a particular freshness.
- Evidence shows current operational controls do not prevent or detect the identified failures.
