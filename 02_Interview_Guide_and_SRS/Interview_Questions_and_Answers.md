# SparshCare: Interview Guide (Questions and Answers)

**Simulation project.** I acted as the business analyst for SparshCare, a fictional offline-first phone app that helps village health workers screen for early leprosy, refer people to a doctor, and track whether the referral actually happened. All six stakeholders were AI-played personas (Claude role-play), and all names and figures are illustrative.

This guide has prepared answers to the questions I expect about the project. Every example comes from my Interview Log or my SRS (`SRS_SparshCare_corrected.docx`).

---

## 1. How the documents connect

| Step | Document | What it holds |
|---|---|---|
| 1 | **Stakeholder Interview Log** | 6 interviews, 89 questions, all on 17 August 2026. Every answer is tagged as Functional, Non-functional, Business rule, Constraint or Emotional/cognitive, and as a *need* or a *solution*. |
| 2 | **Requirements register** (inside the log) | 253 entries: 104 functional, 60 non-functional, 33 business rules, 36 constraints, 20 emotional/cognitive. |
| 3 | **Detailed Requirements Document** | 16 stakeholder requirements (STR) and 19 user stories (US). |
| 4 | **SRS** (18 August 2026) | **47 functional and 26 non-functional requirements**, a release plan and a traceability matrix. |

The 164 functional and non-functional statements in the log overlap heavily, because several stakeholders raised the same need. I merged the duplicates and prioritised the rest to get the SRS set of 47 + 26.

---

## 2. Core questions

### Q1. Why did you interview 6 stakeholders, and what did each one want?

A system like this has several different users, and each needs something different. If I had spoken to only one, I would have built something that works for that person and fails for the rest. So I interviewed one person from each user group, with the same question structure each time so I could compare answers.

| Stakeholder | Biggest pain | Where it shows up in the SRS |
|---|---|---|
| **Sunita, ASHA** (21 questions) | Stigma makes everything covert; she refers people and never learns the outcome; paper records get lost. | FR-A03 (never lose a record), FR-A10 (outcome returned to her), FR-A12 (PIN before clinical screens) |
| **Dr. Rao, Medical Officer** (16) | Referrals arrive with no clinical detail, and appointments ignore his real availability. | FR-M05 (he confirms every slot; no double-booking), FR-M07 (he can override risk) |
| **Dr. Meera, Specialist** (13) | Blind calls that start from zero, and interruptions that wreck her calendar. | FR-S01 (pre-call case packet), FR-S03 (opinion without a live video call) |
| **Mr. Verma, District Officer** (13) | Referrals are never closed, clusters are found too late, and he can't tell "found nothing" from "didn't look". | FR-D02 (closure figure), FR-D04 (cluster detection), FR-D05 (reasoned nil reporting) |
| **Ramesh, Beneficiary** (13) | Exposure through the health system itself, and wasted trips costing about ₹420–430 and a day's wage. | QR-11 (no disease terms in SMS), FR-B01 (appointment confirmation), FR-A09 (consent) |
| **Priya, IT Admin** (13) | Silent data loss during sync, no record of who viewed a file, and one administrator for about 1,100 users. | FR-X02 (read and write audit), FR-X04 (field-level merge), QR-10 (account recovery without her) |

### Q2. Give one example of a functional requirement and one non-functional requirement.

**Functional (what the system does): FR-A08, "High-risk opens two items."**
For every high-risk screening, the system creates both a specialist consultation request and a PHC referral, and neither can be closed while the other is open. It exists because the case study's first success criterion is that no high-risk case is lost.

**Non-functional (how well it does it): QR-01, "ScreeningEffort."**
An ASHA must be able to record one screening offline in a median of 90 seconds or less, using 12 taps or fewer. It is measured by timing 10 ASHAs across 20 screenings each. It exists because Sunita told me long forms are impossible in the field.

**Why the second one is non-functional:** it has a scale, a measurement method and a target. All 26 of my non-functional requirements are written this way, so a tester can say whether each one passes.

### Q3. How did you decide what was a Must and what was a Should?

I used MoSCoW, and I let the stakeholders' own rankings decide instead of my opinion. In the interviews each person was asked to rank their needs, and where someone put one item below another, I kept that order. For example:
- **ASHA:** confidentiality and never losing data.
- **Medical Officer:** making the screened person exist as a trackable record.
- **Specialist:** the pre-call case packet.
- **District Officer:** closing the referral loop before cluster alerts.

I then grouped the requirements into 3 releases, in dependency order. Release 1 covers screening, referral and appointments, the two workflows that decide whether a person is seen at all. Release 2 adds the specialist loop, because a case packet cannot be built before screening data exists. Release 3 adds the district dashboard.

### Q4. What is a traceability matrix and why did you build one?

It is a table linking each stakeholder requirement to the system requirements that deliver it, and to the screen where it appears. For example, STR-01 (offline capture and retention) is delivered by FR-A03 and by QR-02, QR-20 and QR-23.

I built it for three reasons:
1. **Nothing is invented.** Every requirement traces back to something a stakeholder said.
2. **Nothing is missed.** All 16 stakeholder requirements are covered, and the matrix shows it.
3. **Change is manageable.** If a stakeholder changes their mind, I can see which requirements are affected.

---

## 3. Conflicts between stakeholders

The log records several conflicts. These are the ones I can explain best.

| Conflict | Positions | What happened | In the SRS |
|---|---|---|---|
| **Form length** | District wanted about 25 fields per person; Sunita refused. | She calculated about 5 minutes per person, roughly 8 hours of typing on a 100-person day, and predicted workers would enter false values. When I put this to Mr. Verma, he withdrew his position: "six fields I can trust" beat twenty-five he could not. Dr. Rao separately proposed a two-tier form. | FR-A04: a short minimum record captured in the field. Clinical detail is left to the doctor. |
| **Who decides risk** | Software that flags vs software that concludes. | Dr. Rao said the software may flag and prioritise but must never close a case as "low risk". A recorded negative stays on file for years. | FR-A07: no screening is ever concluded; routine cases are re-screened after 90 days. FR-M07: the doctor can override the risk category. |
| **Image quality** | Specialist needs clear photos; the field has cheap phones and 2G. | Dr. Meera's answer was to make structured findings mandatory and photos secondary, with quality checks at the point of capture. | FR-A13 (guided capture), FR-S03 (store-and-forward opinion) |
| **Recording vs privacy** | The programme must keep records; Ramesh must not be identifiable locally. | His fix was to restrict who can see a record, not whether it exists. | FR-D07 (coarse maps by default), QR-12 (least privilege), QR-11, FR-X02 |
| **Security vs speed** | Audit and login controls vs an ASHA covering about 40 houses a day. | Priya's fix: bind the account to a registered device, add one short PIN per working session, and let the ANM reset it. | FR-A12, QR-16 |
| **Clinician workload** | Monitoring would route every missed referral to the doctor. | Dr. Rao: routine follow-up belongs to the ASHA; only high-concern cases that fail to attend escalate to him. | Worklist design for the ASHA (FR-A10, FR-A11) |

I also logged one conflict that software cannot fix: the district's performance reviews punish honest bad figures. Mr. Verma said so himself, and I recorded it as a programme-management issue instead of pretending a requirement could solve it.

### Q5. How did you handle conflicting stakeholder needs?

I put one stakeholder's view to another in the interview, with evidence, and recorded the result. The clearest case was form length. Sunita rejected 25 fields and gave her own arithmetic. When I put that to Mr. Verma, he dropped his position on data-quality grounds: a field she cannot fill reliably gives him false data, not weak data. He then sorted fields into three groups: ones only the person standing there can supply, ones the system already knows, and ones that belong to the clinician. That sorting shaped the short minimum record in FR-A04.

Some conflicts stayed open. Dr. Rao's two-tier form had not yet been put to Sunita, so I flagged it for a joint working session instead of calling it settled.

### Q6. What was the most important requirement in the project?

FR-A07, **"No screening is ever concluded."** If the software calls someone low-risk and it is wrong, a case can be missed until disability sets in. Dr. Rao also pointed out that a recorded negative carries a timestamp and a name, and it will be retrieved years later if a missed case shows up. So a "routine" result never closes the record. It stays open until a clinician records an outcome, and routine cases return to the worklist after 90 days. The software flags risk; the clinical decision stays with a doctor.

---

## 4. Follow-up questions

### Q7. Why is the app offline-first?

The villages have 2G or no signal. If the app needed a network, the health worker could not use it where she works. Every screening is saved on the phone first (FR-A03) and synced later. QR-04 requires a full campaign day of 120 records to upload within 15 minutes on a 2G connection.

Priya also described a real failure in an earlier app: it merged records by "most recent timestamp wins", but device clocks were wrong, so valid data was overwritten. That is why FR-X04 merges at field level, keeps every earlier value, and ignores device clocks.

### Q8. How did you handle privacy?

Stigma is the biggest risk, so I treated confidentiality as a safety requirement. Examples from the SRS:
- Outbound SMS messages contain zero prohibited terms (QR-11), so a family member reading one learns nothing.
- A separate PIN is needed before any clinical screen opens (FR-A12), because Sunita described a family member reading over her shoulder and learning that someone is a suspect.
- Consent is recorded before any referral, consultation or photograph (FR-A09).
- Every read and write is audited (FR-X02), so the system can answer "who viewed this record".

### Q9. How did you run the interviews with AI?

I used one AI persona per stakeholder, each in a fresh chat. Each persona had hidden needs that only came out when I probed well, and some were designed to disagree with each other.

My question order was deliberate: rapport, then the current process, then concrete evidence (a time it went wrong), then pain, then constraints, then a deliberate conflict probe, with solution ideas last. I ended each interview with a read-back ("have I got that right, and which matters most?") so the stakeholder confirmed the priorities. I also tagged every answer as a *need* or a *solution*, so I could trace each proposed fix back to the problem behind it.

### Q10. Is this a real project? Are the numbers real?

No. It is a simulation. The stakeholders are AI personas, and the names, the facility and all figures are illustrative. They are close to real field conditions but must not be quoted as official statistics. The log lists, for each interview, the figures that were quoted from memory and would need checking against real records before design.

What the project does show is the method: structured elicitation, tagging, conflict handling, prioritisation and traceability.

### Q11. What would you do differently or next?

- Validate the requirements with real health workers and doctors.
- Hold the joint working session on the minimum field list that Dr. Rao and Sunita asked for.
- Build a clickable prototype and test it in the field.
- Add acceptance criteria and test cases to each requirement.
- Get a clinician to review the risk rules, since that is the most safety-critical part.

---

## 5. Quick facts

| Item | Number |
|---|---|
| Stakeholders interviewed | 6 |
| Interview questions | 89 (21, 16, 13, 13, 13, 13) |
| Functional / non-functional statements in the log | 104 / 60 |
| Stakeholder requirements | 16 |
| User stories | 19 |
| **Functional requirements in the SRS** | **47** |
| **Non-functional requirements in the SRS** | **26** |
| Releases | 3 |
| Core workflows | 3 (field screening, specialist teleconsultation, PHC referral booking) |
| Interview date / SRS date | 17 August 2026 / 18 August 2026 |
