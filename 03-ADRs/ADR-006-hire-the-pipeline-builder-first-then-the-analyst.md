# ADR-006: Hire a data engineer first and a data analyst second; forecasting waits for a November decision gate

- **Status:** Draft
- **Date:** 2026-11-12
- **Decision owner:** Ishola (consulting lead); client sign-off: Nana Adjei and the board

## Context

The board has budgeted two data hires, not three. The developer is the only technical person and also runs the shop. Investors mentioned machine learning for demand forecasting. Nana is not technical and wants to see her own numbers.

## Decision

**Hire 1, data engineer (offer accepted by 26 February, starts Monday 1 March 2027).** Strong SQL, some Python, and experience building and operating scheduled data pipelines. The role owns the reporting pipeline and also develops warehouse models and analysis using SQL, tests, and business rules agreed with Finance and Operations. First 90 days:
- *Days 1–30:* shadow the developer on the replica and its runbook; inventory the source tables; turn the agreed revenue definition into tested SQL transformations.
- *Days 31–60:* build and monitor the scheduled refresh with row-count and reconciliation checks; deliver the report Nana opens on Monday 29 March and support the March month-end match by 7 April.
- *Days 61–90:* document the reporting data and deletion checklist with Marketing and the developer; improve data-quality checks and write handover notes; prove the report survives two days of the developer's absence. Any stock-application change remains with the shop developer and depends on the stock-flow audit and agreed requirements.

**Hire 2, data analyst (starts Tuesday 1 June 2027).** Strong with business questions and reporting, not a pipeline builder. First 90 days:
- *Days 1–30:* sit with Nana through her Mondays; agree her five most common questions.
- *Days 31–60:* build the self-serve report for those questions; add Nigeria in cedis.
- *Days 61–90:* take over the controlled customer export for Marketing; assess whether the history is clean enough for forecasting.

**Forecasting:** no hire and no project. The board gets a yes/no page by 15 November 2027. Yes only if 12 months of clean daily history exist and a named person will act on the output. **No third role:** a Finance lead is named as answerable for customer-data requests.

## Alternatives considered

### Alternative A: Analyst first

- **How it would work:** Hire a reporting analyst in Q1 to give Nana better reports straight away.
- **Why it is attractive:** The pain Nana feels is reports, and an analyst is the person she would talk to.
- **Why rejected:** Without a reliable pipeline and tested warehouse models, an analyst builds more spreadsheets from CSV exports, which is today's problem with a salary attached. The data engineer establishes that foundation; the analyst's self-service reporting depends on it.

### Alternative B: A data scientist first, for forecasting

- **How it would work:** Hire a machine-learning specialist to build forecasting while the basics are fixed in parallel.
- **Why it is attractive:** It answers the investors' wish and signals ambition.
- **Why rejected:** Forecasts built on unreconciled numbers are wrong with confidence. There is also under a year of clean history. A data scientist would spend the first six months cleaning data, and that is not the job they were hired for.

## Consequences

- **What this buys:** Each hire has a clear first 90 days and a number Nana can verify at the end of it. The data engineer establishes the pipeline and trusted warehouse models before the analyst builds self-service reporting.
- **What this costs:** Q1 depends on the developer alone, at roughly 6–8 working days, so shop work slips. From March to June, Nana has a data engineer but no analyst, so some ad-hoc questions wait. Salary assumptions of about GHS 15,000–25,000 a month for the data engineer and GHS 10,000–16,000 for the analyst are planning figures, not market quotes.
- **What it costs the client if I am wrong:** If Hire 1 never starts, Q2's outcomes slip. If the wrong skill mix is hired, six months are lost.
- **What would make me revisit this:** No acceptable candidate by 28 February (then use a 3-month contractor for the same 90-day plan, or swap the order); the developer cannot spare the Q1 time.

## What this survives

- **Hire 1 resigns at month 6:** The definitions, runbook, pipeline and tests exist on paper and in code; the analyst and developer can keep reporting running for a quarter.
- **Only one hire is approved in the end:** Hire 1 alone still delivers ADRs 001, 002, 004 and 005. Nana gets her Monday report, and the analyst work is postponed.
- **Budget is cut or the pilot in Nigeria fails:** Neither role depends on Nigeria.
- **It does not survive** losing the developer and Hire 1 together. That needs an outside contractor on retainer, and I would raise it with the board as a key-person risk.
