# Proposed improvement beyond the brief: reconcile selected report data with the read replica

## The problem it solves

The brief asks for one revenue number Nana and Finance can both trust. A scheduled build can run and still produce a report that differs from its source: a missing day, a duplicated order, or a changed amount. A reconciliation check is a proposed DataOps safeguard that could flag selected discrepancies for investigation.

## Proposed check

After a scheduled warehouse build, compare selected reporting-table counts and values with the corresponding data on the MySQL read replica, the reporting source described in ADR-001. A possible initial scope is the last 7 complete days:

1. Compare order counts by day.
2. Compare order values by day.
3. Check that the latest complete day expected from the build is present.
4. Check for duplicate orders in the reporting output.

If implemented, a failed check could identify the affected day and differing values for investigation; it should not by itself declare a report accurate or safe to publish.

**Implementation status:** This is a proposal, not a built feature. The repository contains no implementation or test artifacts for this check, and it has not been run against Kloud Kart systems or data. The comparison fields, date handling, duplicate criteria, failure handling, and publication workflow need to be agreed and tested before use.

## What it is worth to Kloud Kart

- **For Nana and Finance:** selected discrepancies could be surfaced for investigation instead of waiting for a manual month-end comparison.
- **For the board:** after implementation, the team could track how often these checks find a mismatch.
- **For data protection:** the check could provide limited evidence that selected reporting counts and values agree with the replica. It would not establish that the source data is accurate or that the agreed revenue definition is correct.

The diagnosis estimates risk-weighted exposure of about GHS 150,000 for a 0.1% revenue discrepancy; this is not a measured loss. The proposed check would not prevent all reporting errors or eliminate that exposure.

## Implementation considerations

- **To implement:** effort and operating cost need estimating after the comparison scope and publication workflow are agreed. The data engineer could develop the reporting-side checks with input from the developer.
- **Limitations:** A match to the replica would not validate the source data, the *definition* of revenue (ADR-004), or transformations that are wrong in the same way on both sides. Aggregate checks can also miss errors that cancel each other out.
