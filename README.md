# SparshCare: Requirements Engineering Simulation

> **Simulation project.** I acted as the business analyst for a fictional healthcare system. All six stakeholders are AI-played personas and all names, places and figures are illustrative. This is practice for requirements elicitation and specification, not a real client engagement.

## 1. The problem

**SparshCare** is a fictional offline-first phone app for a rural district health programme. Village health workers (ASHAs) screen people for early signs of leprosy, refer suspected cases to a doctor, and the programme tracks whether each referral ends in a diagnosis.

The business problem: referrals are made on paper, outcomes are never reported back, cases are found late, and the stigma attached to the disease means every design choice has privacy consequences. Villages often have 2G or no signal, so the system must work offline.

My task was to find out what each stakeholder actually needs, resolve the conflicts between them, and write a specification a development team could build from.

## 2. Stakeholders interviewed

| Stakeholder | Role | Their main concern |
|---|---|---|
| Sunita | ASHA (frontline health worker) | Speed in the field, privacy, and never learning what happened to people she referred |
| Dr. Rao | Medical Officer, primary health centre | Referrals with clinical detail, real appointment availability, and software that never closes a case as "low risk" |
| Dr. Meera | Specialist (dermatologist) | A case packet before the consultation, and remote opinions without a live call |
| Mr. Verma | District Leprosy Officer | Closing the referral loop, finding clusters early, and trustworthy figures |
| Ramesh | Beneficiary (person screened) | Confidentiality and avoiding wasted trips |
| Priya | IT Administrator | Safe sync, an audit trail, and a workable setup for about 1,100 users with a very small admin team |

## 3. What I did

| Step | Output | Size |
|---|---|---|
| 1. Prepared a case brief and six persona prompts | Case study and persona files | 6 personas |
| 2. Ran structured interviews, one per stakeholder | Interview log, every answer tagged by type (functional, non-functional, business rule, constraint, emotional) and as a need or a solution | 6 interviews, 89 questions |
| 3. Built a requirements register from the log | Raw requirement statements | 164 functional and non-functional statements |
| 4. Consolidated and prioritised | Stakeholder requirements and user stories | 16 stakeholder requirements, 19 user stories |
| 5. Wrote the specification | Software Requirements Specification (IEEE 830 style) | **47 functional and 26 non-functional requirements** |
| 6. Checked completeness | Traceability matrix and line-by-line reconciliation | All 164 log lines accounted for |

## 4. How the requirements were derived

**Interview technique.** Each interview followed the same order: rapport, the current process, a concrete example of something going wrong, pain points, constraints, a deliberate conflict probe, and solution ideas last. Each ended with a read-back so the stakeholder could confirm and rank their priorities.

**Need versus solution.** Every answer was tagged as either a need or a proposed solution, so that each proposed fix could be traced back to the problem behind it.

**Writing the SRS.** Requirements are written as testable "shall" statements. Each of the 26 non-functional requirements has a scale, a measurement method and a target. For example, QR-01: an ASHA records one screening offline in a median of 90 seconds or less, using 12 taps or fewer, measured with 10 ASHAs across 20 screenings each.

**Prioritisation.** MoSCoW, using each stakeholder's own ranking, then grouped into 3 releases in dependency order: screening, referral and appointments first; the specialist consultation loop second; the district dashboard third.

## 5. Key decisions and conflicts

| Conflict | How it was handled |
|---|---|
| **Form length.** The district wanted about 25 fields per person; the ASHA calculated that this meant about 5 minutes per person, roughly 8 hours of typing on a 100-person day, and predicted false entries. | When this was put to the District Officer, he withdrew his position on data-quality grounds. The SRS uses a short minimum record (FR-A04), with clinical detail left to the doctor. |
| **Who decides risk.** Software that flags versus software that concludes. | FR-A07: no screening is ever concluded. A routine result stays open until a clinician records an outcome and returns to the worklist after 90 days. The doctor can override the risk category (FR-M07). |
| **Privacy versus programme records.** The programme must keep records, but a beneficiary must not be identifiable locally. | Restrict who can see a record instead of whether it exists. No disease terms in any message (QR-11), coarse maps by default (FR-D07), audited reads (FR-X02). |
| **Security versus field speed.** | A registered device plus one short PIN per working session, resettable by a supervisor (FR-A12, QR-16). |
| **Image quality versus field reality.** | Structured findings are mandatory and photos are secondary, with guided capture (FR-A13). |

Not every conflict ended in agreement. One example is the doctor's two-tier form idea, which was never put to the ASHA, so the reconciliation note records it as open.

## 6. Example requirements

| ID | Requirement | Why it exists |
|---|---|---|
| FR-A07 | No screening is ever concluded. | A wrong "low risk" result could mean a missed case and permanent disability. |
| FR-A08 | A high-risk screening opens both a specialist request and a PHC referral; neither can close while the other is open. | The programme's first success criterion is that no high-risk case is lost. |
| FR-A10 | The ASHA sees the outcome of every referral within 24 hours of a doctor recording it. | She had referred about twenty people and never been told one outcome. |
| QR-01 | Record one screening offline in a median of 90 seconds, 12 taps or fewer. | Long forms are impossible in the field. |
| QR-11 | Outbound SMS contains no prohibited disease terms. | A family member reading a message must learn nothing. |

## 7. Completeness check

Because the log has 164 statements and the SRS has 73 requirements, I mapped every log line to the SRS (or recorded why it was left out). See the [reconciliation note](02_Interview_Guide_and_SRS/Requirements_Reconciliation.md).

| Outcome | Lines |
|---|---|
| Covered by the SRS | 101 |
| Partly covered | 28 |
| Not in the SRS (backlog or review item) | 22 |
| Field practice, not software | 8 |
| Out of scope (treatment supply, post-treatment care, incentives) | 4 |
| Interface detail left to design | 1 |

The note also lists seven places where the SRS differs from what a stakeholder asked for, so each can be confirmed or changed.

## 8. Repository contents

```
SparshCare-Requirements-Simulation/
├── README.md
├── 01_Case_and_Personas/
│   ├── 01_Case_Study_SparshCare.md
│   └── 04_Stakeholder_Persona_Prompts.md
└── 02_Interview_Guide_and_SRS/
    ├── SRS_SparshCare_corrected.pdf / .docx
    ├── SparshCare_Interview_Log.pdf / .docx
    ├── Interview_Questions_and_Answers.md
    └── Requirements_Reconciliation.md
```

| To see... | Open |
|---|---|
| The specification | [SRS (PDF)](02_Interview_Guide_and_SRS/SRS_SparshCare_corrected.pdf) |
| The raw interviews | [Interview log (PDF)](02_Interview_Guide_and_SRS/SparshCare_Interview_Log.pdf) |
| How I would explain the project | [Interview guide](02_Interview_Guide_and_SRS/Interview_Questions_and_Answers.md) |
| How log lines became SRS requirements | [Reconciliation note](02_Interview_Guide_and_SRS/Requirements_Reconciliation.md) |
| The case brief and personas | [01_Case_and_Personas](01_Case_and_Personas/) |

## 9. Business analysis skills demonstrated
Requirements elicitation, stakeholder analysis, structured interviewing, conflict resolution, requirements documentation (SRS), user stories, MoSCoW prioritisation, release planning, traceability, gap analysis and reconciliation.

## 10. Limitations
- The stakeholders are AI personas. The method is real; the stakeholder input is not. Requirements would need validation with real users before any build.
- Figures such as costs, caseloads and population are illustrative and not official statistics.
- No prototype, test cases or user acceptance testing were produced.

## Tools
Claude (stakeholder persona role-play), Microsoft Word, Markdown.
