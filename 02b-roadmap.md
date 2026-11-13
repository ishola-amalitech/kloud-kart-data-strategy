# Kloud Kart: 12-month data roadmap

**For:** Nana Adjei · **Plan starts:** Monday 7 December 2026 · **Written:** 12 November 2026

**In one line:** stop reports slowing the shop, give Operations and Finance one revenue number, know where every customer list is, and only then talk about forecasting.

**Rough cost:** GHS 60,000–90,000 in year one for a second computer and tools (my estimate, to be confirmed by quotes), plus the two hires the board has already budgeted. The problems I could put a number on cost roughly GHS 225,000–410,000 a year, so the hires are justified mainly by board credibility and legal safety, not by savings alone.

Every line below can be checked by you, or by one phone call, without asking an engineer.

| When | Who is better off, and what changes | How you check it |
|---|---|---|
| **Q1** Dec–Feb | **Shoppers and Nana:** from Mon 11 Jan, Monday reports run from a second computer holding a copy of the shop's records, not from the shop itself. | Pages load as fast during the 07:00 report as in any other hour; the developer shows the board a before-and-after chart; no "site is slow" complaints on Mondays to 28 Feb. |
| | **Nana and the board:** by Fri 18 Dec, if a complaint about a deleted customer is already open, its received date and a written answer plan are on file. By Fri 29 Jan, Kloud Kart's entry is on the Data Protection Commission's public register, with its renewal date in the diary. | Read the complaint note; search the public register yourself. |
| | **Nana and Finance:** by Fri 29 Jan, both sign one page that says what "revenue" means. | You read it unaided; Finance quotes the same words. |
| | **Developer and Nana:** by Fri 29 Jan, review how checkout reserves and updates stock across orders, payments, cancellations, returns and adjustments; document where oversells or count mismatches can occur and agree what operational decisions need support. | Read the flow and findings; confirm any gaps and requirements with the developer. |
| | **Marketing lead:** by Fri 26 Feb, can say how many copies of the customer list exist and who holds each. | Ask for the number and the names; any file not on the list is deleted. |
| | **Nana:** by Fri 26 Feb, first data hire has accepted an offer (starts 1 Mar); she gets a monthly count of orders spoiled by wrong stock as a baseline, not a fix. | Signed offer; first monthly count in your inbox. |
| **Q2** Mar–May | **Nana:** from Mon 29 Mar, Monday numbers come from one report she opens herself by 07:30. No CSV rebuilding. | Open it on the first Monday; compare with your old method for April. |
| | **Finance:** by Wed 7 Apr, March month-end revenue matches Nana's report to the cedi. | Ring Finance. |
| | **Marketing lead and Nana:** by Fri 30 Apr, a customer deletion request is finished everywhere within 5 working days, with a written list of every place their data was held. | We run a test using a staff member's dummy account; you read the list. |
| | **Nana and the developer:** by Fri 30 Apr, decide which operational stock safeguards, if any, are needed based on the Q1 audit and the decisions staff need to make. Keep live stock decisions in the shop application; do not assume a refresh cadence or dashboard before requirements are agreed. | Read the agreed decision and owner; if changes are needed, check the implementation and test plan. |
| | **Nana:** by Mon 31 May, the Monday report still arrives on time when the developer is away for two days. | The developer takes the two days. |
| **Q3** Jun–Aug | **Nana:** second hire starts Tue 1 Jun. By 30 Jun, any stock safeguards approved after the audit are implemented and tested; if no gap was found, record that decision instead. | Developer demonstrates the agreed safeguards and their tests, or Nana shows the documented no-change decision. |
| | **Nana:** by 31 Aug, review whether stock discrepancies and oversells are falling after any agreed changes. | Monthly share of wrong counts caught before an oversell; target 8 in 10. Use the shop's operational records for live decisions; use warehouse reporting only for historical measurement. |
| | **Nana:** by 31 Aug, she answers her five most common questions (list agreed in June) from the report herself. | She demonstrates it. |
| | **Finance:** by 31 Aug, Nigeria orders appear in the same report, in cedis at Finance's month-end rate. | Finance matches the August Nigeria total. |
| **Q4** Sep–Nov | **The board:** by 30 Sep, a practice complaint about a deleted customer is answered in 5 working days (the legal limit is 90). | The board reads the drill record. |
| | **Nana and Finance:** by 31 Oct, three month-ends in a row (Aug, Sep, Oct) match to the cedi. | Ring Finance. |
| | **The board:** by 15 Nov, one page says yes or no to demand forecasting. Yes only if 12 months of clean daily history exists and a named person will act on it. | The page exists and names that person. |
| | **The board:** by 30 Nov, a one-year scorecard: Monday slowdowns, revenue mismatches, uncounted customer-list copies, oversold orders. | Four numbers, each against its January starting point. |

**Deliberately not in this plan**

- **Stock dashboards and alerts:** stock correctness belongs in the operational shop application, not the ETL dashboard. The Q1 audit and staff needs will determine whether a live stock or low-stock/replenishment view or alerts are useful and how fresh they need to be; they are not assumed as a fix for overselling.
- **Buying Snowflake or BigQuery now:** 40 GB does not need it, and before any customer data goes to a cloud service we must be able to say where it would live and who can reach it. Revisit when data passes 150 GB, the nightly job passes 3 hours, or a second big data source arrives.
- **Demand forecasting:** a decision gate in November, not a project now; forecasts built on unreconciled numbers would be wrong with confidence.

**Decided for you, since you were unavailable** (change any of these by telling me): Finance owns the definition of revenue; the first hire is the pipeline builder, the second the analyst; no third hire, and a Finance lead is named as the person answerable for customer-data requests.
