# Situation Diagnosis – Kloud Kart Data Strategy Engagement

## Problem 1 – Reporting Exports Slow the Live Website

### A. Symptom

Monday reporting exports have caused the live website to become extremely slow on two occasions in the past month.

### B. Root Causes

- Reporting queries run against the same MySQL database that supports the live website.
- The website and database share a single server, meaning reporting activity competes with customer transactions for computing resources.
- Exports are initiated manually rather than through a controlled and scheduled process.
- There is no separate reporting copy or server, despite the recurring reporting workload.
### C. Lifecycle Stages Affected

- Ingestion: Operations and Finance may use different extracts, snapshots or refresh times.
### D. Undercurrents

- Architecture: Operational and reporting workloads share the same database server.
- Orchestration: A person manually initiates the extraction.
- DataOps: There is no scheduled, monitored and performance-tested extraction process.
- Security/governance: Downstream CSV copies are not inventoried or controlled.
### E. Data Dimensions Affected

- Availability: The web application may become unavailable to users.
- Timeliness: Manual reporting takes a long time, which may explain why investors want real-time information.
### F. Cost

### 1. Direct Cost

- 4,000 orders per day ⇒ 165 orders per hour ⇒ 650 orders competing with reporting activity, assuming the export takes four hours.
- If 10% of orders are affected by the slowdown and the average purchase value is GHS 100, the estimated loss is GHS 6,500 per week and GHS 340,000 per year.
### 2. Wasted Labour

- Four hours of export and reporting work per week × 52 weeks per year = 208 hours per year.
- Assuming a 40-hour working week: 208 ÷ 40 ≈ 5 weeks.
- Applying the same estimate to Finance results in a combined total of 10 weeks.
- At an assumed labour cost of GHS 50 per hour, the estimated cost is GHS 20,000.
### 3. Risk-Weighted Exposure

Not applicable (N/A).

## Problem 2 – Operations and Finance Report Inconsistent Revenue

### A. Symptom

- Operations’ Monday revenue figure does not match the figure in Finance’s spreadsheet.
### B. Confirmed Process

- Operations reconstructs Monday’s figures from CSV exports, while Finance maintains a separate spreadsheet. The brief does not provide a common definition of revenue or a shared transformation process.
### C. Root Causes

- There is no agreed, documented definition of revenue.
- Operations and Finance calculate results independently.
- Spreadsheet formulas and filters are not version-controlled or centrally tested.
- Extraction timing and reporting cut-off rules are not specified.
- No routine reconciliation between source data and reported figures is described.
### D. Lifecycle Stages

- Ingestion: Operations and Finance may use different extracts, snapshots or refresh times.
- Transformation: Different formulas, statuses, dates and refund rules can produce different totals.
- Serving: Conflicting figures are presented to decision-makers.
### E. Undercurrents

- Data management: There is no common definition or ownership of the revenue metric.
- DataOps: Spreadsheet logic is not tested, versioned or monitored.
- Architecture: Reporting depends on uncontrolled extracts rather than a shared reporting source.
### F. Data-Quality Dimensions Affected

- Consistency: The same business concept is defined differently across the two reports.
- Accuracy: At least one result may not reflect the intended definition.
### G. Cost

### 1. Wasted Labour

- The Head of Operations and a Finance employee may spend one to two hours each week trying to reconcile the figures.
- This represents 52–104 hours per year, equivalent to approximately 2.6–5.2 working weeks.
- At an assumed labour cost of GHS 50 per hour, the estimated cost is GHS 2,600–5,200.
### 2. Direct Loss

- No direct financial loss is confirmed in the brief.
- Potential direct losses could include excess tax, unnecessary bonuses, avoidable expenditure or hiring costs, but only if such payments have already been made using an incorrect revenue figure.
- None of these losses has been verified.
### 3. Risk-Weighted Exposure

- At 4,000 orders per day and an average order value of GHS 100, annual order value is approximately GHS 150,000,000.
- A discrepancy of 0.1% would represent approximately GHS 150,000 per year.
- This could contribute to decisions based on incorrect figures, such as over-hiring or excessive spending.
## Problem 3 – Marketing Exports Create Customer-Data Protection Risk

### A. Symptom

- Marketing uses a customer list containing approximately 300,000 people, but the company does not track how many copies exist or where they are stored.
### B. Root Causes

- Customer data can be exported without a documented and controlled process.
- There is no demonstrated record of who exported customer data, when it was exported, the purpose of the export, or where the file was stored or sent.
### C. Lifecycle Stages

- Ingestion: Customer data is exported without recording its ownership, purpose or destination.
- Storage: An unknown number of files exist without verified access, retention or deletion controls.
- Transformation: Segmentation and filtering may create additional derived copies.
- Serving: Customer data may continue to be used by Marketing or third parties after the source record has been deleted.
### D. Undercurrents

- Security
- Data management
- DataOps
- Orchestration
### E. Data-Quality Dimensions Affected

Not applicable (N/A).

### F. Cost

### 1. Wasted Labour

- If each deletion request takes approximately two hours to locate and delete customer data, and one request is received per month, this represents 24 hours per year. At GHS 50 per hour, the estimated labour cost is GHS 1,200.
### 2. Direct Loss

- No penalty, legal fee, compensation payment or customer loss is confirmed in the brief.
- Direct financial loss is therefore currently unquantified.
### 3. Risk-Weighted Exposure

- Potential legal fees and reputational damage may arise if the company is unable to answer questions about how customer data is deleted. Bried does not provided enough info to answer this.
## Problem 4 – Stale Inventory Creates Overselling Risk

### A. Symptom

Stock counts must remain current because outdated availability information may allow customers to order products that cannot be fulfilled.

### B. Root Causes

- Stock reservation and deduction rules are not documented in the information provided.
- Delays or synchronisation issues between order placement, payment, cancellation, returns and inventory adjustments may be contributing factors.
### C. Undercurrents

- DataOps
- Data architecture
### D. Data-Quality Dimensions Affected

- Accuracy and consistency.
### E. Cost

### 1. Wasted Labour

Planning assumptions: 4,000 orders per day; 365 days per year; 0.2% of orders experience an inventory discrepancy; 40% of affected orders require manual intervention; and each intervention takes 15 minutes.

Annual orders: 4,000 × 365 = 1,460,000. Orders affected: 1,460,000 × 0.2% = 2,920. Orders requiring manual intervention: 2,920 × 40% = 1,168. Time spent: 1,168 × 15 minutes = 292 hours per year, or approximately 7.3 standard 40-hour working weeks.

At an assumed labour cost of GHS 50 per hour, the estimated cost is GHS 15,000.

### 2. Direct Loss

There is insufficient information to quantify direct loss.

### 3. Risk-Weighted Exposure – Lost Contribution

Planning assumptions: average order value of GHS 100; 40% of affected orders are cancelled rather than recovered through an alternative product or location; and contribution margin is 25%. The brief does not provide actual values for these measures.

Cancelled orders: 1,460,000 × 0.2% × 40% = 1,168. Sales value associated with those cancellations: 1,168 × GHS 100 = GHS 116,800. Estimated lost contribution: GHS 116,800 × 25% = GHS 29,200 per year. Contribution is used rather than total sales value because the company would have incurred variable costs to fulfil the orders.

## Summary of Estimated Costs

| Problem | Wasted Labour (GHS) | Direct Loss (GHS) | Risk-Weighted Exposure (GHS) |
| --- | --- | --- | --- |
| Exports slowing the server | 20,000 | 340,000 | N/A |
| Inconsistent revenue calculations | 5,200 | N/A | 150,000 |
| Marketing customer-data exports | 1,200 | N/A | N/A |
| Stale stock | 15,000 | N/A | 29,200 |

## Cost Prioritisation Methodology

To rank the identified problems, a Weighted Business Cost Score (WBCS) was developed. The method recognises that, for a startup, immediate and measurable costs are generally more relevant to decision-making than uncertain future exposures.

The following weights were assigned:

- Wasted labour: 40% – captures staff time and productivity lost through inefficient processes.
- Direct loss: 40% – captures immediate financial losses or revenue impact on the business.
- Risk-weighted exposure: 20% – captures potential future costs, such as regulatory, operational or reputational consequences.
Each cost category was normalised against the highest value in that category, using a scale of 0–100. Where a problem had an N/A value, that category was excluded and the remaining weights were adjusted proportionally. N/A therefore means that a cost was not quantified, rather than that the cost is zero.

## Normalised Cost Scores

| Problem | Normalised Labour | Normalised Direct Loss | Normalised Risk Exposure | Final Score |
| --- | --- | --- | --- | --- |
| Exports slowing the server | 100.00 | 100.00 | N/A | 100.00 |
| Inconsistent revenue | 26.00 | N/A | 100.00 | 50.67 |
| Marketing customer-data exports | 6.00 | N/A | N/A | 6.00 |
| Stale stock | 75.00 | N/A | 19.47 | 56.49 |

## Ranking Results

1. Exports slowing the server – 100.00: This is the highest priority because of its substantial labour and direct financial costs.
1. Stale stock – 56.49: This ranks second by cost score, driven by wasted labour and potential lost contribution from inventory discrepancies.
1. Inconsistent revenue calculations – 50.67: This is the third priority, driven mainly by its risk-weighted financial exposure.
1. Marketing customer-data exports – 6.00: This has the lowest quantified cost, but this should not be interpreted as low business priority. Customer-data protection and the 90-day complaint-response requirement make it an important compliance issue.