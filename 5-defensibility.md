# Defensibility under Ghana's Data Protection Act

**For:** Nana Adjei and the board · **Written:** 12 November 2026

**What this is, and is not.** This is my reading of the plan against Ghana's Data Protection Act, 2012 (Act 843), *as I understand Act 843*. It is not legal advice. I have worked from a law firm's country summary, an encyclopedia entry and the Data Protection Commission's own site. The Commission's site does not publish the Act's text, so before the board relies on any line below, counsel should read the Act itself.

## The one rule the plan is built around

**Every copy of a customer's data is a place a deletion request must reach.** Kloud Kart cannot answer a Commission complaint about a deleted customer unless it can say where that person's data existed and show that deletion reached all of it. Today that list includes the live database, every CSV Nana has ever exported, her spreadsheet, Finance's spreadsheet, anything emailed, and any backup of any of those. Nobody maintains it.

The plan therefore does two things: it **reduces the number of copies**, and it **makes every remaining copy a designed, listed one**. A system we built is a findable copy; a file on a laptop is not.

## What the Act asks, and what the plan does about it

| What the Act asks (as I understand it) | What the plan does | Where |
|---|---|---|
| **Register** with the Commission and renew the certificate. The register is public. | Check the public register for Kloud Kart's entry; if missing or lapsed, register. Put the renewal date in the diary. | Roadmap, by 29 Jan 2027 |
| **Lawful basis and stated purpose.** Collect only what you need for a stated purpose. | Every customer-list export records its purpose. The reporting database holds customer IDs only, no names, phones or emails. | ADR-005, ADR-002 |
| **Accuracy.** | The nightly check compares reports with the shop and tells the team not to publish if they disagree. | improvement.md |
| **Do not keep data longer than necessary.** | Exported files expire after 30 days. The reporting database is rebuilt nightly, not an ever-growing raw archive. Backups roll off after 35 days. | ADR-005, ADR-002 |
| **Secure it.** | One logged export route; export logins on the live database removed; each copy has a named owner. Watermarked files make a leak traceable. | ADR-005, ADR-001 |
| **Respect the person's rights**: they can ask what you hold and require correction or deletion, within a defined window. | A written deletion checklist, run from the register, with a 5-working-day target against the 90-day limit. | ADR-005 |
| **Breach handling.** | **Not covered in this plan.** Accepted risk, see below. | Gaps |
| **No selling or buying personal data.** | No plan item sells or buys data. Marketing's lists are only ever the company's own customers. | n/a |
| **Data leaving Ghana.** Act 843 does not appear to have a specific cross-border transfer regime, so I will not cite one. The principles still bind wherever data sits. | Everything stays on servers Kloud Kart controls. Before any cloud service is proposed, we answer "where would this data live, and who can reach it?" | ADR-002 |
| **Foreign customers.** A duty to honour the foreign law that applies to a foreign person whose data is sent to Ghana. | The Nigeria pilot's customers may carry Nigerian obligations. Counsel to confirm what applies before Nigerian customer data is loaded. | ADR-005 |

## The copy count

| Where customer data lives | Today | After the plan | Owner | How a deletion reaches it |
|---|---|---|---|---|
| Live shop database | Yes | Yes (the source of truth) | Developer | Delete or anonymise the record. Order totals stay, anonymised, pending counsel on record-keeping. |
| Read replica | No | Yes (a mirror of the shop) | Developer | Follows the live database automatically. |
| Reporting database | No | Customer IDs only, no names or contact details | Data engineer | Order rows are anonymised by the deletion checklist. |
| Backups | Unknown | Yes, kept 35 days | Developer | Rolls off within 35 days. Recorded as such, not hidden. |
| Marketing's 300,000-row list and its copies | Unknown number | Only logged exports, each with an ID and a 30-day expiry | Marketing lead | Expiry, plus the suppression record so a deleted person is not re-added. |
| Nana's and Finance's spreadsheets | Yes, uncounted | Retired once three month-ends match | Nana, Finance lead | Delete the files. |
| Anything emailed or on a laptop | Unknown | Reduced, not eliminated | Each person | Cannot be guaranteed. See gaps. |

The register is complete by 26 February 2027. The point is not to claim zero copies. It is to be able to say how many exist and who holds each.

## Answering a complaint inside 90 days

1. **Day 0:** write down the date the complaint was received. The 90 days run from there.
2. **Days 1–5:** run the register's checklist for that person; note each place checked, who checked it, and the date.
3. **Days 1–5:** confirm the exports log shows no live copy of any list containing them, and add them to the suppression record.
4. **By day 40:** backups containing them have rolled off.
5. **By day 90 at the latest:** reply to the Commission with the list of places, the dates, and what was done.

**If a complaint is already open**, the clock started when it was received, which I do not know. I assume it is live and treat it first. It is answered by hand, from whatever can be found this month, before any tooling exists. The honest answer will say what could not be found.

## What I am accepting, and when to revisit

The undercurrents I am not fully covering with two hires are accepted risks, not oversights.

| Gap | Why accepted | Revisit |
|---|---|---|
| **Breach handling.** No written plan for what to do if customer data leaks. | The first 12 months go to knowing where the data is. A breach plan depends on the register. | Draft in Q4; review 30 Nov 2027. |
| **Copies we cannot find** (a laptop, a personal email). | No design removes them. The export log and expiry shrink the problem going forward. | After the first deletion drill, 30 Sep 2027. |
| **Cost control of the platform.** | The fixed-cost design makes a surprise bill unlikely. | When any cloud service is proposed. |

## What I could not verify

- The text of Act 843 itself, including the exact deletion window and any rule on keeping tax or accounting records.
- Whether Kloud Kart is already registered, or whether a complaint is already open.
- What Nigerian law requires for the pilot's customers.
- Whether the shop's backups run daily and how long they are kept today. I set 35 days as a decision, not a finding.
