# Defensibility under Ghana's Data Protection Act

**For:** Nana Adjei and the board · **Written:** 12 November 2026

**What this is, and is not.** This is my reading of the plan against Ghana's Data Protection Act, 2012 (Act 843), *as I understand Act 843*. It is not legal advice. I have worked from [DLA Piper's Ghana country guide](https://www.dlapiperdataprotection.com/index.html?t=law&c=GH), an encyclopedia entry and the Data Protection Commission's own site. The Commission's site does not publish the Act's text, so before the board relies on any line below, counsel should read the Act itself.

## The one rule the plan is built around

**Every copy of a customer's data is a place a deletion request must reach.** Kloud Kart cannot answer a Commission complaint about a deleted customer unless it can say where that person's data existed and show that deletion reached all of it. Today that list includes the live database, every CSV Nana has ever exported, her spreadsheet, Finance's spreadsheet, anything emailed, and any backup of any of those. Nobody maintains it.

The plan therefore does two things: it **reduces the number of copies**, and it **makes every remaining copy a designed, listed one**. A system we built is a findable copy; a file on a laptop is not.

## What the Act asks, and what the plan does about it

| What the Act asks (as I understand it) | What the plan does | Where |
|---|---|---|
| **Register** with the Commission and renew the certificate. The register is public. | Check the public register for Kloud Kart's entry; if missing or lapsed, register. Put the renewal date in the diary. | Roadmap, by 29 January 2027 |
| **Lawful and transparent collection; stated purpose and minimisation.** Tell people what is collected, by whom, why, whether it is required, who receives it, and about access/rectification rights; collect only what is needed. | ADR-005 proposes recording export purpose; ADR-002 limits reporting identifiers. The collection notice, lawful basis, and recipient information still need to be verified and documented. | ADR-005, ADR-002; verify with counsel |
| **Accuracy.** | A proposed reconciliation check would compare selected report counts and values with the read replica and flag discrepancies. Passing those checks would not prove the revenue definition or overall data accuracy. | [6-improvement.md](./6-improvement.md) |
| **Do not keep data longer than necessary.** | Exported files are proposed to expire after 30 days. The reporting database is rebuilt nightly, not an ever-growing raw archive. Backup retention is proposed at 35 days, pending necessity and counsel's review. | ADR-005, ADR-002 |
| **Secure it.** | One logged export route; export logins on the live database removed; each copy has a named owner. Watermarked files make a leak traceable. | ADR-005, ADR-001 |
| **Respect the person's rights.** The reference describes access and rectification rights; deletion handling and applicable timeframes require legal confirmation. | ADR-005 proposes a register-based deletion checklist with a 5-working-day internal target. Separately, the lab brief requires responding to a Data Protection Commission complaint about a deleted customer's data within 90 days. This is a lab constraint, not presented here as the statutory deadline for an individual deletion request. | ADR-005; lab brief; verify rights and timeframes with counsel |
| **Breach handling and security.** Apply safeguards and ensure processors apply security measures. The reference says notify the Commission and affected person as soon as reasonably practicable when there are reasonable grounds to believe personal data was accessed or acquired without authorisation. | The current plan lacks an incident-response procedure. Add one covering escalation, assessment, notification, and system-integrity restoration; confirm process and applicability with counsel. Check processor safeguards before using a vendor. | Gap; counsel and processor review |
| **No improper sale, purchase, obtaining, or disclosure.** The reference prohibits sale/purchase and addresses knowingly obtaining or knowingly or recklessly disclosing personal data. | No sale or purchase is planned. The export log and access controls should also govern who may obtain or disclose customer data; confirm the direct-marketing rules below. | ADR-005; verify controls with counsel |
| **Direct marketing.** The reference says prior written consent is required for use, obtaining, procuring, or providing personal data for direct marketing. | The current plan does not establish that consent for Marketing's 300,000-person list. Verify the consent basis and evidence before using the list for direct marketing. | ADR-005; verify with counsel |
| **Data leaving Ghana.** The reference reports no specific transfer provisions in Act 843, but says principles still apply wherever data sits and prohibits sale/purchase and certain obtaining/disclosure. | Before any cloud service or processor is proposed, establish where data will live, who can access it, and what safeguards apply. | ADR-002; assess processor safeguards |
| **Foreign data subjects.** The reference says foreign-jurisdiction rules apply where personal data originating in that jurisdiction is sent to Ghana for processing. | Before processing Nigeria-originating personal data in Ghana, counsel should confirm applicable Nigerian requirements. | ADR-005 |

## The copy count

| Where customer data lives | Today | After the plan | Owner | How a deletion reaches it |
|---|---|---|---|---|
| Live shop database | Yes | Yes (the source of truth) | Developer | Delete or anonymise the record. Order totals stay, anonymised, pending counsel on record-keeping. |
| Read replica | No | Yes (a mirror of the shop) | Developer | Follows the live database automatically. |
| Reporting database | No | Customer IDs only, no names or contact details | Data engineer | Order rows are anonymised by the deletion checklist. |
| Backups | Unknown | Proposed 35-day retention, subject to necessity and counsel's review | Developer | Proposed expiry; confirm backup schedule and deletion behavior. |
| Marketing's 300,000-row list and its copies | Unknown number | Proposed logged exports, each with an ID and 30-day expiry, subject to purpose/consent and retention review | Marketing lead | Proposed expiry, plus a suppression record if counsel approves it. |
| Nana's and Finance's spreadsheets | Yes, uncounted | Retired once three month-ends match | Nana, Finance lead | Delete the files. |
| Anything emailed or on a laptop | Unknown | Reduced, not eliminated | Each person | Cannot be guaranteed. See gaps. |

The target is to complete the register by 26 February 2027. The point is not to claim zero copies. It is to be able to say how many exist and who holds each.

## Responding to the lab's 90-day complaint requirement

The lab brief requires a response to a Data Protection Commission complaint about a deleted customer's data within 90 days. This is distinct from the proposed 5-working-day internal target for carrying out a deletion checklist. Confirm statutory obligations and individual-rights timeframes with counsel.

1. **Day 0:** write down the date the complaint was received. The 90 days run from there.
2. **Days 1–5:** run the register's checklist for that person; note each place checked, who checked it, and the date.
3. **Days 1–5:** confirm the exports log shows no live copy of any list containing them, and add them to the suppression record.
4. **By day 40 under the proposed retention setting:** backups containing them should have rolled off; verify the actual backup schedule and deletion behavior.
5. **By day 90 at the latest under the lab brief:** reply to the Commission with the list of places, the dates, and what was done.

**If a complaint is already open**, the clock started when it was received, which I do not know. I assume it is live and treat it first. It is answered by hand, from whatever can be found this month, before any tooling exists. The honest answer will say what could not be found.

## Gaps in this plan, and when to revisit

The undercurrents below are not fully covered by this plan. Listing them does not mean they have been formally accepted as risks.

| Gap | Why it remains a gap | Revisit |
|---|---|---|
| **Breach handling.** No written plan for what to do if customer data leaks. | The first 12 months go to knowing where the data is. A breach plan depends on the register. | Draft in Q4; review 30 Nov 2027. |
| **Copies we cannot find** (a laptop, a personal email). | No design removes them. The export log and expiry shrink the problem going forward. | After the first deletion drill, 30 Sep 2027. |
| **Cost control of the platform.** | The fixed-cost design makes a surprise bill unlikely. | When any cloud service is proposed. |

## What I could not verify

- The text of Act 843 itself, including the exact deletion window and any rule on keeping tax or accounting records.
- Whether Kloud Kart is already registered, or whether a complaint is already open.
- What Nigerian law requires for the pilot's customers.
- Whether the shop's backups run daily and how long they are kept today. I set 35 days as a decision, not a finding.
