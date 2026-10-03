# Case Study — *SparshCare*
## A Field-Screening, Teleconsultation & Referral System for Early Detection of Leprosy

**HIT701 — Software Development & Lifecycle Management · PGDM HHM 2025–27**
**Sister case to the CoWIN/U-WIN case in your reader (pp. 82–104). Read this before Day 1.**

> **A note on figures:** names, the facility, and all numbers below are *illustrative*, constructed for this studio so you can elicit, specify, and model against a realistic but self-contained brief. They are close to real NLEP field conditions but should not be quoted as official statistics.

---

## 1. Context: leprosy, the last mile, and the digital gap

Leprosy (Hansen's disease) is curable with multi-drug therapy, yet India still records the largest share of new cases globally. The clinical tragedy is rarely the disease itself — it is **delay**. When a case is caught early, before nerve damage, the person recovers with no disability. When it is caught late, the person develops **Grade-2 disability** (visible deformity — claw hand, foot drop, lagophthalmos), which is irreversible and carries lifelong social **stigma**.

Under the **National Leprosy Eradication Programme (NLEP)**, early detection depends on **frontline health workers** — **ASHAs** (Accredited Social Health Activists) and **ANMs** (Auxiliary Nurse Midwives) — who screen people in villages during house-to-house campaigns (e.g., the *Sparsh* Leprosy Awareness Campaign) and refer suspected cases to a **Medical Officer (MO)** at the **Primary Health Centre (PHC)** for confirmation.

**Our setting (illustrative):** the block PHC at **Kondagaon**, serving a cluster of tribal and forest-fringe villages. Realities the software must survive:
- **Connectivity is intermittent** — ASHAs screen in villages with 2G or no signal; the PHC has patchy broadband.
- **Devices are basic** — entry-level Android phones (≈2 GB RAM), shared or personal.
- **Digital & health literacy is low** — for many ASHAs the phone keyboard is the hard part, not the clinical judgement.
- **Stigma is severe** — a leaked "leprosy suspect" status can cause a person to be ostracised; **confidentiality is a safety requirement, not a feature.**
- **Specialists are scarce** — a dermatologist/leprologist may sit at the District Hospital, hours away; **teleconsultation** is the only realistic way to give a high-risk villager expert eyes quickly.

---

## 2. The clinical primer students need (kept deliberately simple)

Field screening looks for the **WHO cardinal signs** of leprosy:
1. A **pale (hypopigmented) or reddish skin patch** with **definite loss of sensation**.
2. A **thickened / enlarged peripheral nerve**, with loss of sensation and/or weakness of the muscles it supplies.
3. Presence of the bacillus on a slit-skin smear (a lab test, not done in the field).

In the field the ASHA records simple findings — number of skin patches, whether a patch has lost sensation (tested with cotton wool), any numbness/weakness in hands or feet, any visible deformity. From these, a **risk stratification** is needed:
- **Routine / low concern** → health education, re-screen next campaign.
- **Suspected case → refer to MO** at PHC for confirmation and to start treatment.
- **High-risk** (e.g., multiple patches, nerve involvement, or any visible deformity) → fast-track to a **specialist teleconsultation** *and* a PHC referral.

> **Why this makes the software a candidate Medical Device (SaMD):** the moment software *computes who is high-risk*, it is influencing a clinical decision. If it wrongly says "low", a case can be missed until disability sets in. Students must treat the risk logic as safety-critical (IEC 62304 / ISO 14971; reader pp. 40–55).

---

## 3. The problem today (As-Is)

Screening findings are written on **paper campaign forms**. Referral is **word-of-mouth or a paper chit** ("go to the PHC and meet the doctor"). Consequences the project must fix:
- Suspected cases **never reach** the PHC — no tracking, no follow-up, no closure of the referral loop.
- The MO's **appointment book is manual**; a villager who travels hours may find the MO away.
- **High-risk cases wait weeks** for a specialist because there is no fast path.
- Programme managers get **aggregate paper reports weeks later** — too late to act on a cluster.
- **No confidentiality control** — paper forms pass through many hands.

---

## 4. The vision (To-Be) — what *SparshCare* must do

A system that lets a frontline worker screen a person in the field, get an **immediate risk stratification**, and — depending on risk — either educate, **book a referral appointment with the PHC Medical Officer**, or **fast-track an online Zoom consultation** with a specialist, while **tracking every referral to closure** and **protecting the person's confidentiality**.

### The three core workflows (these anchor every artifact this week)

**Workflow A — Field screening & risk stratification**
ASHA identifies/registers a beneficiary (offline), records screening findings, and the app computes a risk category *even with no network*, syncing when signal returns.

**Workflow B — High-risk online teleconsultation**
For high-risk cases, the system schedules a **Zoom** consultation with an available specialist, notifies both sides, and records the specialist's opinion and next action.

**Workflow C — Referral-appointment booking with the PHC Medical Officer**
For suspected/high-risk cases, the system **books a specific appointment slot** with the MO at the PHC, sends the beneficiary a confirmation (SMS/IVR in local language), and tracks whether the person actually attended — closing the loop.

---

## 5. Scope

**In scope:** beneficiary registration/identification; offline screening capture; the risk-stratification rules; teleconsult scheduling (Zoom); PHC appointment booking & referral tracking; confidentiality/consent; local-language low-literacy UI; programme dashboard (basic).

**Out of scope (for this studio):** the multi-drug therapy supply chain, laboratory (slit-skin smear) systems, hospital billing, and full ABDM certification. Assume identity via **ABHA (ABDM)** is *available to integrate* but not something you build.

---

## 6. Stakeholders (summary — full interview personas in `04_Stakeholder_Persona_Prompts.md`)

| Stakeholder | Role in the system | What they care about most |
|---|---|---|
| **ASHA / ANM (frontline worker)** | Primary field user; screens & captures data | Simplicity, works offline, doesn't add hours to her day, local language |
| **Beneficiary / community member** | The person screened & referred | Confidentiality, dignity, not travelling in vain, being believed |
| **Medical Officer (PHC)** | Confirms diagnosis; receives referrals & bookings | Reliable referral info, manageable appointment load, no duplicate work |
| **Dermatologist / Leprologist** | Conducts Zoom teleconsult for high-risk | Enough clinical context before the call, good-enough image/data, scheduling that respects her time |
| **District Leprosy Officer (NLEP)** | Programme monitoring & targets | Timely data, cluster detection, referral-closure rates, no false reporting |
| **IT / System Administrator** | Runs the system, user & data management | Security, roles, offline sync integrity, uptime, auditability |

*(Note: these stakeholders will disagree — e.g., the District Officer wants lots of data fields; the ASHA wants almost none. Surfacing and resolving that conflict is part of Day 1.)*

---

## 7. Constraints & assumptions
- **Offline-first** capture with later sync is mandatory, not optional.
- Target device: entry-level Android; screening screen must be usable one-handed, low-literacy, in the local language.
- **Confidentiality by design**: role-based access; "leprosy suspect" status visible only to authorised roles; explicit **consent** captured before referral/teleconsult.
- **Zoom** is the mandated teleconsultation platform (integrate, don't rebuild).
- **ABHA / ABDM** for identity where available; graceful fallback when a beneficiary has no ABHA.
- Notifications via **SMS/IVR** (many beneficiaries don't use smartphones).
- Regulatory frame to keep in view: **IEC 62304**, **SaMD**, **ISO 14971**, **AAMI TIR45**, ABDM data-privacy expectations.

---

## 8. Success criteria (what "good" looks like)
- **No high-risk case is lost:** every high-risk screening results in a scheduled teleconsult *and* a tracked PHC referral.
- **Referral loop closes:** the system knows whether a referred person attended the PHC.
- **Field-usable:** an ASHA can complete a screening in the field, offline, in under ~3 minutes.
- **Confidential:** no unauthorised role can see a person's leprosy status.
- **Timely programme view:** the District Officer sees new suspected cases within a day of sync, not weeks.

---

## 9. Glossary
- **ASHA / ANM** — community frontline health workers.
- **PHC** — Primary Health Centre; first medical-officer-staffed facility.
- **MO** — Medical Officer (doctor) at the PHC.
- **NLEP** — National Leprosy Eradication Programme.
- **WHO cardinal signs** — the three diagnostic signs of leprosy (Section 2).
- **Grade-2 disability** — visible, irreversible deformity; the outcome early detection prevents.
- **Risk stratification** — computed category (routine / suspected-refer / high-risk) driving next action.
- **Teleconsultation** — remote specialist consult (Zoom) for high-risk cases.
- **SaMD** — Software as a Medical Device (reader pp. 40–55).
- **ABHA / ABDM** — Ayushman Bharat Health Account / Digital Mission (national digital identity for health).
- **FHIR** — Fast Healthcare Interoperability Resources (health data exchange standard).
- **Offline-first / sync** — capture data without network; upload when connectivity returns.
