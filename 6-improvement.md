# Proposed improvement beyond the brief: a nightly replica-to-report reconciliation check

## The problem it solves

The brief asks for one revenue number Nana and Finance can both trust. A scheduled build can run and still produce a report that differs from its source through missing days, duplicated orders, or changed amounts. The proposed improvement is a nightly reconciliation check that compares selected reporting data with the corresponding data on the MySQL read replica.

## Initial scope

For the last seven complete days, the check will:

1. Compare order counts by day.
2. Compare order values by day.
3. Confirm the latest complete day expected from the build is present.
4. Detect duplicate order identifiers in the reporting output.

The comparison will use matching date cut-offs and source watermarks so replication timing does not create false discrepancies. A failure will identify the affected day and values for investigation; a pass will mean only that these selected checks matched. It will not certify the report as generally accurate or safe to publish.

**Status:** Proposal only. No implementation or test artifacts are present in the repository, and the check has not been run against Kloud Kart systems or data. The data engineer should implement and test the check with the developer before it is used.

## What it is worth to Kloud Kart

- **For Nana and Finance:** the check can surface selected report/source discrepancies for investigation instead of waiting for a manual month-end comparison.
- **For the board:** once implemented, record how often the check finds a mismatch.
- **For accuracy:** this is a limited report-integrity control relevant to the Act 843 data-accuracy principle described in the defensibility assessment. It does not validate source data, the revenue definition, or all personal data. It does not track deletion requests or satisfy the lab brief's separate requirement to respond to a Data Protection Commission complaint within 90 days; the data-copy register and deletion checklist address that workflow.

The diagnosis estimates annual order value as 4,000 orders/day × GHS 100/order × 365 days = GHS 146,000,000 (about GHS 150 million). A 0.1% discrepancy is GHS 146,000, rounded to about GHS 150,000 for the risk-weighted estimate. This is exposure, not a measured loss; the check will not prevent all reporting errors or eliminate that exposure.

## Implementation considerations

- The data engineer owns the reporting-side check, with the developer confirming source fields, date cut-offs, and replica watermarks.
- Estimate implementation and operating effort before scheduling the work.
- A match to the replica does not validate the source data, the *definition* of revenue (ADR-004), or errors shared by both sides. Aggregate checks can also miss errors that cancel each other out.
