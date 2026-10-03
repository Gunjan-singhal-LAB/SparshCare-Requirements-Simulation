# SparshCare: Requirements Reconciliation

**Purpose.** The Interview Log holds **164 functional and non-functional requirement statements** (104 FR, 60 NFR). The SRS holds **47 functional and 26 non-functional requirements** (73). This note shows what happened to every log line, so the difference can be explained and defended.

This is a simulation project. The log's statements are raw stakeholder input from AI-played personas; the SRS is the consolidated specification.

## 1. Result at a glance

| Outcome | Lines | Meaning |
|---|---|---|
| Covered | 101 | A SRS requirement (or design constraint or interface in SRS section 2) delivers it. |
| Partly covered | 28 | The core is in the SRS but a detail is missing or changed. The note says what. |
| Backlog: not in SRS v1.0 | 22 | Not found in the SRS. Candidates for a later release or for a review decision. |
| Operational, not software | 8 | Field practice, training or facility arrangements that software cannot enforce. |
| Out of scope (SRS 1.2) | 4 | Excluded by the SRS scope (treatment supply chain, post-treatment care, programme incentives). |
| Design detail | 1 | An interface choice, left to design. |
| **Total** | **164** | |

So **101 of 164 (62%)** are fully covered and **28** more are partly covered. About 8% were deliberately excluded because software cannot deliver them or the SRS scope rules them out.

## 2. Why the SRS has fewer requirements than the log

1. **Duplicates merged.** Several stakeholders asked for the same thing, so one SRS requirement answers many log lines. For example, FR-A04 answers FR-01, FR-03, FR-66 and parts of others.
2. **Wishes rewritten as testable statements.** The SRS uses "shall" statements with a measurable target for non-functional items.
3. **Constraints and interfaces carry some lines.** SRS section 2 holds design constraints (DC-1 to DC-6) and system interfaces (SI-1 to SI-5). Many log NFRs trace to these instead of to a numbered FR or QR.
4. **Non-software items removed.** Room privacy, counselling and house-marking are field practice.
5. **Scope.** The SRS covers detection to examination. Treatment supply, post-treatment care and incentives are out.
6. **Conflicts resolved.** For example, the two-tier form (FR-18) was never agreed with the ASHA, so the SRS uses one minimum record.

## 3. Items to review before relying on this

These are the places where the SRS differs from the log or leaves something out. None breaks the SRS, but each is a decision someone should confirm.

| Item | Issue |
|---|---|
| NFR-06 vs QR-01 | Stakeholder asked for 1 minute per person; the SRS target is a 90-second median. |
| FR-66 vs FR-A04 | District Officer committed to eight items; the SRS fixes six. |
| FR-82, NFR-46 vs FR-A01 | The log says no family member's name beside a diagnosis; the SRS keeps the father/husband name for identity matching. |
| FR-42 | The specialist's urgent lane (2-hour packet) is not in the SRS. |
| FR-50 | Mode of detection is not captured, but the Grade-2 indicator needs it. |
| FR-104 | No breach-notification channel, although the DPDP Act is referenced. |
| FR-93, FR-96, NFR-58 | Bulk-reassignment authorisation, expiring grants and access anomaly flags are not in the SRS. |

## 4. Line-by-line mapping

Status key: **Covered**, **Partly**, **Backlog** (not in SRS v1.0), **Operational**, **Out of scope**, **Design**.

| Log ID | Log requirement (shortened) | Status | SRS reference | Note |
|---|---|---|---|---|
| FR-01 | Capture one screening record with a minimal field set only: person name, household locator,… | Covered | FR-A04, FR-A01 | Symptom duration moves to the specialist packet (FR-S01). |
| FR-02 | Record patch location by tapping a body diagram rather than typing a description | Design | – | Tap-vs-type is an interface choice; SRS statements avoid implementation. |
| FR-03 | Record the cotton (sensation) test as a single binary choice — this is the decisive field | Covered | FR-A04, FR-A06, FR-S02 | Sensation result with method and three-state logic. |
| FR-04 | Raise a referral for a flagged person without the disease name appearing on screen or on any… | Covered | FR-B02, QR-11, QR-13 | No disease name on screen, slip or message. |
| FR-05 | Return the referral outcome to the referring ASHA — minimally ‘attended / not attended’ with a… | Covered | FR-A10 | Outcome returned within 24 h. |
| FR-06 | Show the ASHA a list of persons she herself flagged earlier who have no recorded outcome, so… | Covered | FR-A11, FR-A10 | Open referrals on her worklist; "not yet attended" shown. |
| FR-07 | Prompt extra attention for higher-risk profiles observed in the field: elderly, living alone /… | Backlog | – | Risk rule (FR-A05) uses recorded findings only; age, living alone and duration are not inputs. |
| FR-08 | Provide a neutral, government-branded reassurance screen for the family (curable, free,… | Backlog | – | Family reassurance screen not in SRS; must be checked against QR-13 screen discretion. |
| FR-09 | Count each completed screening towards the ASHA’s task / incentive record automatically | Out of scope | – | Incentive/task-record accounting belongs to the state programme system. |
| FR-10 | Allow the sensitive clinical detail to be saved as an incomplete draft in the house and… | Partly | FR-A03, FR-A04 | Records are retained offline and the minimum record avoids sensitive detail at the doorstep; a private "complete later" step is not specified. |
| FR-11 | Create a persistent, shared record of every person screened at the moment of screening — name,… | Covered | FR-A01, FR-M01 | Person exists as a record at screening; PHC sees expected arrivals. |
| FR-12 | Deliver structured screening findings to the Medical Officer before or with the patient’s… | Covered | FR-M02 | Structured findings, date and worker name. |
| FR-13 | Publish the Medical Officer’s confirmed availability and allow booking only into slots he has… | Covered | FR-M05 | Booking only into slots he has marked available. |
| FR-14 | Propose-and-confirm booking: the system may propose and hold a slot; it must never commit… | Covered | FR-M05 | Propose, hold, confirm; no automatic commitment. |
| FR-15 | Notify the patient and the referring ASHA when a booked slot breaks — in time to stop the… | Covered | FR-M06 | Notification within 15 minutes of a broken slot. |
| FR-16 | Record and display “not checked” distinctly from “checked, normal” in every clinical field;… | Covered | FR-A06, FR-M03 | "Not checked" distinct from "normal". |
| FR-17 | Clinician override in both directions (escalate a low flag, close a high flag) with recorded… | Covered | FR-M07 | Override both ways with a recorded reason. |
| FR-18 | Two-tier screening form: Tier 1 (~1 min) for every person screened; Tier 2 (~3 min) opening… | Partly | FR-A04 | Two-tier form was never agreed with the ASHA (log 5A). SRS uses one minimum record and leaves detail to the clinician. |
| FR-19 | Free-text or voice note in the ASHA’s own words, presented verbatim to the Medical Officer… | Backlog | – | Free-text/voice note not in SRS v1.0. |
| FR-20 | Capture prior history: previously screened and told it was nothing; previously took or… | Partly | FR-S01, FR-A11 | Prior treatment is in the packet; findings carry forward on re-screen. "Previously told it was nothing" is not itemised. |
| FR-21 | Referral wrapper: identity, a working contact number, referring worker and date, booked slot,… | Partly | FR-M02, FR-A01, FR-B01 | Findings, date, worker and language are covered. Travel distance and female-attendant need are not. |
| FR-22 | Make non-attendance a visible state; route routine follow-up to the referring ASHA, never to… | Covered | FR-M08, FR-A10, FR-A11 | Routine chasing stays with the ASHA. |
| FR-23 | Actively escalate to the Medical Officer only high-concern flagged cases that fail to attend —… | Covered | FR-M08 | Active escalation of high-concern non-attenders only. |
| FR-24 | Auto-generate the monthly NLEP progress report, disaggregated, from data already captured —… | Covered | FR-M09 | Monthly return generated, not re-keyed. |
| FR-25 | Supervisory view for the Medical Officer: screening, referral and confirmation counts by… | Partly | FR-D01, FR-D05 | District-level supervisory view exists; a separate MO view by worker and panchayat is not specified. |
| FR-26 | Protect MDT follow-up capacity (25–30 concurrent patients, monthly) separately from… | Out of scope | – | Treatment-clinic capacity planning is beyond the detection-to-examination scope. |
| FR-27 | Photograph capture as supporting evidence only — explicitly never sufficient on its own for… | Covered | FR-S01, FR-S04, FR-A13 | Images never sufficient alone; inadequate image is not reassurance. |
| FR-28 | Prompt household contact examination and single-dose prophylaxis when a case is confirmed —… | Partly | FR-A04, FR-B05 | Household contact is captured and consent for contact visits is recorded. Prophylaxis prompting is treatment-side. |
| FR-29 | Design for later extension into the treatment tail: monthly supervised dosing, reaction… | Out of scope | – | Treatment tail and disability care are out of scope. |
| FR-30 | Deliver the full pre-call packet (who, story, examination, images, referral question) the… | Covered | FR-S01, QR-09 | Packet at least 12 h before the slot; readable in about 4 minutes. |
| FR-31 | Support a minimum-floor packet (six data points plus one photograph plus the referral… | Covered | FR-S01, FR-S05 | Mandatory items except image; opinion, action and review date. |
| FR-32 | Make the sensation-test field mandatory with method used and whether the patient’s eyes were… | Covered | FR-S02 | Method and eyes-closed status mandatory. |
| FR-33 | Capture nerve-palpation findings per named nerve, both sides — thickened Y/N and tender Y/N —… | Covered | FR-S01 | Per-nerve palpation status. |
| FR-34 | Capture the referral question (“why am I being called, what do you want from me”) at the top… | Covered | FR-S01 | Referral question in the packet. |
| FR-35 | Attach the reporting ASHA’s identity to every case for longitudinal reliability tracking. | Covered | FR-M02, FR-S01 | Screening worker named on every case. |
| FR-36 | Capture 2–3 daylight images per case, close, in focus, with a scale reference, cropped to… | Covered | FR-A13 | Daylight, scale object, face excluded. |
| FR-37 | Provide capture-time quality coaching on the ASHA’s device (wide site shot plus tight border… | Covered | FR-A13 | Coaching and focus check at capture. |
| FR-38 | Provide a sensitive-case flag and a private ASHA-to-specialist channel, settable before… | Partly | FR-S01 | Disclosure state is in the packet. A private ASHA-to-specialist channel is not specified. |
| FR-39 | Provide fixed weekly teleconsultation windows (candidate: Tuesday and Friday 15:30–17:00) with… | Backlog | – | Fixed weekly windows and capped capacity are a scheduling policy not written into the SRS. |
| FR-40 | Require same-morning attendance confirmation from the ASHA; if the patient is not present… | Partly | FR-S06 | Backfill after 3 minutes is covered; same-morning attendance confirmation is not. |
| FR-41 | Surface a confirmed-attendance count to the specialist by lunchtime on a consultation day. | Backlog | – | Confirmed-attendance count for the specialist not in SRS. |
| FR-42 | Provide a checklist-driven urgent lane (tender nerve, new weakness, sudden lesion change, eye… | Backlog | – | Checklist-driven urgent lane (2-hour packet) not in SRS. Closest: FR-A08, FR-M08. |
| FR-43 | When a scheduled slot is unfilled, surface the next reviewed store-and-forward case so the… | Covered | FR-S06 | Next reviewed store-and-forward case offered. |
| FR-44 | Send a patient-preparation prompt to the ASHA ahead of a scheduled appointment (what will… | Backlog | – | Patient-preparation prompt not in SRS. |
| FR-45 | Record the specialist’s opinion and recommended action, dated, attached to the patient’s… | Covered | FR-S05 | Dated opinion and action recorded. |
| FR-46 | Fire an automatic follow-up task on the action’s due date asking whether it happened; if… | Partly | FR-S05, FR-A11 | A review date is mandatory; an automatic due-date follow-up task is not. |
| FR-47 | Show treatment-started status (Y/N, date) on the case, retrievable on demand (pull) rather… | Backlog | – | Treatment-started status not in SRS. |
| FR-48 | Provide a weekly digest of exceptions — recommended actions that did not happen. | Backlog | – | Weekly exceptions digest not in SRS (see also NFR-21). |
| FR-49 | Provide calibration feedback — notify the specialist when a remote “not leprosy” opinion is… | Partly | – | Calibration feedback is cited in the SRS safety section but has no numbered requirement. |
| FR-50 | Capture mode of detection for every case (survey / self-presented / contact / school /… | Backlog | – | Mode of detection is not a captured field in SRS v1.0; needed for the Grade-2 indicator. |
| FR-51 | Hold a suspected case as an open item from the ASHA’s flag until an MO confirms or rules it… | Covered | FR-A07 | Open until a clinician records an outcome. |
| FR-52 | Provide single point-of-contact capture with no re-transcription downstream, underpinned by a… | Covered | FR-A01, FR-A02, DC-4, QR-26 | One capture, no re-transcription. |
| FR-53 | Run automated plausibility and ratio-exception checks at entry and at aggregation (implausible… | Backlog | – | Plausibility and ratio-exception checks not in SRS. |
| FR-54 | Capture reporting-behaviour metadata — record-created time versus submitted/sync time, and… | Backlog | – | Created-vs-sync-time metadata not in SRS; FR-D06 covers completeness only. |
| FR-55 | Record a three-state zero — assessed-negative / not-assessed / no-record — and never allow a… | Covered | FR-A06, FR-D05, FR-D06 | Three-state zero; unsynchronised unit never shown as zero. |
| FR-56 | Require mandatory reasoned nil reporting, one certifying act per round/day/area (not per… | Covered | FR-D05 | Reasoned nil return per round per unit. |
| FR-57 | Proactively surface and rank quiet or non-reporting units, without requiring the DLO to go… | Covered | FR-D01 | Quiet units surfaced. |
| FR-58 | Run continuous rolling spatio-temporal cluster detection across administrative and month… | Covered | FR-D04 | 3 cases within 1 km in 60 days, rolling. |
| FR-59 | Deliver alerts as assigned, dated, closable action items with an owner and a recorded response… | Covered | FR-D03 | Alerts are assigned, closable items. |
| FR-60 | Provide a daily-updating worklist of open items (unclosed referrals, geographic accumulations,… | Covered | FR-D01 | Worklist separate from monthly indicators. |
| FR-61 | Log the DLO’s own response actions against alerts, to support later outcome evaluation… | Covered | FR-D03 | Response action recorded. |
| FR-62 | Provide a bidirectional referral loop — a named open item visible to both the referring ASHA… | Covered | FR-M01, FR-A10, FR-M04 | Both sides see the open referral. |
| FR-63 | Provide an explicit referral closure outcome vocabulary: confirmed / examined and ruled out /… | Covered | FR-M04 | Six-value closure vocabulary. |
| FR-64 | Auto-populate system-derived fields (block, PHC, sub-centre, worker identifier, entry… | Partly | FR-X02 | User, device and timestamp are recorded in the audit entry; automatic filling of block/PHC/sub-centre is not stated as a requirement. |
| FR-65 | Derive equity / tribal-habitation reporting from classified geography rather than asking a… | Backlog | – | Equity/habitation category derived from geography not in SRS. |
| FR-66 | Support a minimum eight-item field-worker data set at first contact (who, where, when… | Partly | FR-A04 | SRS fixes a six-item minimum, not the eight items the District Officer committed to. |
| FR-67 | Capture clinical and classification detail (disability grading, MB/PB classification, lesion… | Partly | FR-M04, FR-M09 | Clinician-stage detail is deferred to the MO; individual classification fields (MB/PB, lesion count, smear) are not itemised. |
| FR-68 | Provide an optional, non-blocking contact/re-contact number field — never mandatory, never a… | Partly | FR-B01 | IVR fallback where no SMS-capable handset is registered; an optional contact field is not itemised. |
| FR-69 | Never allow any open item (referral, alert, nil report) to close by silence; every item… | Covered | FR-M04, FR-D03, FR-D05 | No item closes by silence. |
| FR-70 | Conduct any physical screening test (e.g. sensation testing) in a private, out-of-sightline… | Operational | – | Physical setting of a test is field practice and training. |
| FR-71 | Let the patient know, in plain terms, where his screening record travels and who can read it | Partly | FR-B05 | Consent records the action consented to; a plain-language "where your record goes" explanation is not specified. |
| FR-72 | Deliver a plain-language, private explanation of the condition — including that it can be… | Operational | – | Counselling content is clinical practice; SRS only controls message content (FR-B02). |
| FR-73 | Issue a referral only against a confirmed, verified provider slot for a named day and time —… | Covered | FR-M05, FR-B04 | Referral against a confirmed slot only. |
| FR-74 | Offer a voice-call reminder, in Hindi or Halbi, as an alternative to any written message | Covered | FR-B01 | IVR voice call in the recorded language. |
| FR-75 | Default any SMS/app notification to a contentless appointment reminder — day and time only, no… | Covered | FR-B02, QR-11 | Contentless reminders. |
| FR-76 | Support remote teleconsultation so the patient’s arm/lesion can be assessed without travelling… | Covered | FR-S03 | Remote consultation by store-and-forward or video. |
| FR-77 | Offer an alternate, unmarked medicine collection point instead of mandatory monthly home… | Out of scope | – | Medicine collection is the MDT supply chain. |
| FR-78 | Deliver any diagnosis in person, seated, by a human with time to sit with the patient — never… | Operational | – | In-person diagnosis is clinical practice; FR-B02 keeps diagnosis out of messages. |
| FR-79 | Let the patient control the timing and manner of disclosure to his own household, rather than… | Partly | FR-B03, FR-B05 | Right to receive nothing and consent; control over timing of household disclosure is not specified. |
| FR-80 | Let the patient nominate a single trusted escort (e.g. the ASHA) for a teleconsultation, and… | Backlog | – | Nominated single escort not in SRS. |
| FR-81 | Flag a sensation-test result taken in a public, socially-pressured setting as provisional,… | Backlog | – | Provisional flag for public-setting test not in SRS (FR-S02 covers method only). |
| FR-82 | Exclude any family member’s name (e.g. “daughter of…”) from a record that also carries the… | Partly | DC-2, FR-X01 | Field-level sensitivity applies, but FR-A01 keeps the father/husband name for identity matching. Confirm this trade-off. |
| FR-83 | Never issue a patient-held card, chit or paper that names the condition | Partly | FR-B02 | No condition name in messages; a rule against any patient-held paper is not explicit. |
| FR-84 | Never mark, paint or number the patient’s house in connection with the diagnosis | Operational | – | Marking houses is field practice and training. |
| FR-85 | Field-level, deterministic sync merge — no record-level “most recent timestamp wins”; every… | Covered | FR-X04 | Field-level deterministic merge. |
| FR-86 | Full change history retained on every record; nothing overwritten silently; every prior value… | Covered | FR-X04, QR-21 | Full version history. |
| FR-87 | No local deletion of an entry until server acknowledgement of receipt | Covered | FR-A03, QR-20 | Nothing deleted locally before acknowledgement. |
| FR-88 | Clean conflict presentation when two versions of a clinical fact disagree — both versions plus… | Partly | FR-X04 | Superseded values are retained; a side-by-side conflict view is not specified. |
| FR-89 | Clinical conflicts (treatment stage, classification) routed to the MO / leprosy programme… | Partly | FR-X04 | No silent resolution; routing of clinical conflicts to the MO is not explicit. |
| FR-90 | Supervisor-mediated (ANM/MO) credential and recovery capability, so a reset never requires the… | Covered | FR-X05 | ANM resets credential. |
| FR-91 | Device registration as a first-class, visible, revocable object per user | Covered | FR-X03 | Device registry. |
| FR-92 | Defined behaviour for a revoked device holding an undrained sync queue — proposed: may still… | Covered | FR-X06 | Revoked device may push, not read. |
| FR-93 | MO authorisation required, and logged as a disclosure event, for bulk caseload reassignment… | Backlog | – | MO-authorised bulk reassignment not in SRS. |
| FR-94 | Append-only access (read and write) logging capturing user, device, record, fields returned… | Covered | FR-X02 | Append-only read and write audit. |
| FR-95 | Supported query, usable by a non-engineer, answering “who has accessed this record and when”… | Covered | FR-X02, QR-17 | Answer within 5 minutes. |
| FR-96 | Access grants that expire by default, tied to a posting with a review date | Backlog | – | Expiring access grants not in SRS. |
| FR-97 | Delivery-state visibility for outbound SMS (“delivered” / “not delivered, call her”), with… | Covered | SI-2, QR-25 | Delivery state shown; undelivered becomes a work item. |
| FR-98 | Real host/slot availability checking before a teleconsultation booking is offered — never… | Covered | SI-3, FR-M05 | Real availability checked before offering a slot. |
| FR-99 | Defined in-app fallback on teleconsultation failure at point of use — reschedule, voice call,… | Covered | SI-3, DC-6, FR-S03 | Defined in-app fallback. |
| FR-100 | ABHA/identity verification optional at capture: patient created on a local identifier, record… | Covered | FR-A01, SI-1 | ABHA optional, never blocking. |
| FR-101 | Client-side error and sync telemetry (crashes, failed syncs, stuck queues) reported… | Covered | FR-X07 | Client telemetry. |
| FR-102 | A formal, consented, logged export interface for legitimate third-party data requests… | Covered | SI-5 | Formal consented export only. |
| FR-103 | Assisted duplicate-record match/merge tooling — candidate pairs surfaced, nothing deleted,… | Covered | FR-A02 | Duplicate matching. |
| FR-104 | A pre-designed, tested notification channel for breach/disclosure communication to affected… | Backlog | – | Breach-notification channel not in SRS; DPDP Act appears only in references. |
| NFR-01 | Full offline capture — every screening function works with zero mobile network | Covered | DC-1, QR-23, FR-A03 | Offline-first. |
| NFR-02 | Zero data loss: entries persist locally and sync automatically in the background; a failed… | Covered | QR-20, FR-A03 | Zero data loss. |
| NFR-03 | No session expiry, no repeated OTP re-login while in the field | Covered | FR-A12, QR-16 | One credential entry per session. |
| NFR-04 | On-screen discretion: no disease name, no red ‘suspected case’ banner, no audio cue; the… | Covered | QR-13 | Screen discretion. |
| NFR-05 | Screening module protected by its own lightweight lock, separate from the phone’s screen lock… | Covered | FR-A12 | Separate module credential. |
| NFR-06 | ≤ 1 minute of device time per person screened | Partly | QR-01 | Stakeholder said 1 minute; SRS target is a 90-second median. Confirm the change. |
| NFR-07 | Devanagari / Hindi labels and input; tap and pictorial selection in place of free typing… | Covered | QR-07 | Language and script. |
| NFR-08 | Low battery draw; usable at low charge (multi-hour daily power cuts) | Partly | SRS 3.5 | Stated as "shall not be battery-hungry"; no measurable QR. |
| NFR-09 | Behavioural discretion: time spent and questions asked at a flagged house must not visibly… | Covered | QR-14 | Behavioural parity. |
| NFR-10 | Usable by a class-10-educated, non-technical worker; no clinical vocabulary anywhere in the… | Covered | QR-06 | Cognitive load. |
| NFR-11 | Any risk rule must be transparent and explainable; the score is collapsed to a word or colour… | Covered | FR-A05, DC-5 | Rule displayed on request; explainable rules only. |
| NFR-12 | Role-scoped access: an ASHA sees only the people she screened in her own area — no browsable… | Covered | FR-X01, QR-12 | Least privilege. |
| NFR-13 | Notifications must never disclose the condition — “PHC appointment” only — and the patient may… | Covered | FR-B02, FR-B03, QR-11 | Contentless messages; opt-out. |
| NFR-14 | Net-zero paperwork: the system must replace existing registers and returns, not add a further… | Covered | DC-4, QR-26 | No second register. |
| NFR-15 | Minimal clinician-facing load: no daily task lists to the Medical Officer; oversight is… | Covered | FR-M08 | No routine task list to the MO. |
| NFR-16 | A Tier-1 screening record must be completable in ~1 minute and a Tier-2 record in ~3 further… | Partly | QR-01 | Single-record time target; Tier-1/Tier-2 split not carried (see FR-18). |
| NFR-17 | Packet format and length must allow the specialist to read and understand a case within about… | Covered | QR-09 | Packet readability. |
| NFR-18 | Packets must arrive the evening before a scheduled slot, not minutes before it. | Covered | FR-S01 | 12 hours ahead. |
| NFR-19 | Field data capture must be offline-first — work done with no tower must never be lost, and… | Covered | DC-1, QR-23 | Offline-first. |
| NFR-20 | Images must be handled for low bandwidth — a small, high-quality crop is preferred over a… | Partly | FR-A13, QR-04 | Face-excluding crop and sync target; an explicit 2G image-size limit is not itemised. |
| NFR-21 | Outcome and status notifications must be pull-based plus a bounded weekly digest, not… | Backlog | – | Weekly digest and pull-based status not in SRS. |
| NFR-22 | Support voice capture of free text in Hindi or Halbi where typing is a barrier, without… | Backlog | – | Voice capture not in SRS v1.0. |
| NFR-23 | The system must function reliably as a store-and-forward channel in areas that cannot sustain… | Covered | FR-S03, QR-08 | Store-and-forward as main path. |
| NFR-24 | Structured clinical fields must be usable by a low-literacy field worker on a small screen… | Covered | QR-06 | Cognitive load. |
| NFR-25 | Asynchronous inputs (packets, digests) should be timed for the specialist’s actual… | Partly | FR-S01 | Timing is 12 h ahead; the 07:00 timing is not specified. |
| NFR-26 | The specialist’s opinion must be durably retrievable and defensible later, not exist only as… | Covered | FR-S05, QR-18 | Opinion recorded durably. |
| NFR-27 | Eliminate transcription-induced data drift across the reporting chain (accuracy). | Covered | DC-4, QR-26, FR-M09 | No re-keying. |
| NFR-28 | Make field data visible to the district at the moment of capture, not on downstream forwarding… | Covered | FR-M01, FR-D01 | Visible within minutes of sync. |
| NFR-29 | Interoperate with and feed existing systems (Nikusth, HMIS, IHIP/IDSP, state Excel formats)… | Covered | SI-4, FR-M09, QR-26 | Nikusth and HMIS formats. |
| NFR-30 | Provide auditability / tamper-evidence for reported figures. | Partly | FR-X02, QR-18 | Audit trail is tamper-resistant; tamper-evidence on reported figures is not separate. |
| NFR-31 | Support two latency tiers — a near-real-time worklist of triggers, and a monthly-to-quarterly… | Covered | FR-D01 | Worklist and monthly indicators separate. |
| NFR-32 | Disclose sync-completeness — what has not yet reached the district — so a gap is never misread… | Covered | FR-D06 | Declared completeness. |
| NFR-33 | Be offline-first; never require live network signal to record a screening or a nil report. | Covered | DC-1, QR-23, FR-D05 | Offline-first. |
| NFR-34 | Enforce role-based, least-privilege access in software, not in a signed policy. | Covered | FR-X01, QR-12 | Server-side least privilege. |
| NFR-35 | Log every drill-down below the coarse default geographic resolution. | Covered | FR-D07 | Finer view requires a logged action. |
| NFR-36 | Default all geographic displays to a coarse resolution (e.g. habitation-level counts) rather… | Covered | FR-D07, QR-19 | Coarse by default. |
| NFR-37 | Screening and consultation venues must be private — out of sightline of neighbours, not… | Operational | – | Venue privacy is field practice. |
| NFR-38 | Facility layout and signage must not make a specific room identifiable as the leprosy/skin… | Operational | – | Facility layout and signage are facility management. |
| NFR-39 | Locally-resident facility staff contact with a given patient must not form a visible pattern… | Operational | – | Staff visit patterns are field practice (QR-14 covers the ASHA). |
| NFR-40 | Any persisted notification (SMS, app) must carry no condition name, department name or… | Covered | FR-B02, QR-11 | No condition, department or programme name. |
| NFR-41 | Message comprehension must not depend on the patient’s reading fluency — short, simple or… | Covered | FR-B01, QR-07 | IVR voice option. |
| NFR-42 | Notification content must remain safe to be read by any other household member who happens to… | Covered | QR-11 | Safe if read by anyone. |
| NFR-43 | Teleconsultation venue must be a private, lockable room, not a community building such as an… | Operational | – | Teleconsultation room is a facility arrangement. |
| NFR-44 | Any device used for teleconsultation must retain nothing of the call afterwards | Backlog | – | Nothing-retained-after-call not in SRS. |
| NFR-45 | Image and lighting quality for remote skin assessment must be sufficient for the intended… | Covered | FR-A13, FR-S04 | Capture coaching; inadequate image handled. |
| NFR-46 | No locally accessible record may display the patient’s name and diagnosis on the same line or… | Partly | DC-2, QR-13 | Name and diagnosis kept apart by field-level sensitivity; see FR-82 trade-off. |
| NFR-47 | Offline-first architecture as a mandatory baseline, not an optional mode | Covered | DC-1 | Mandatory baseline. |
| NFR-48 | System and support model must remain workable at the real operating ratio of ~1,100 users to… | Covered | QR-10, FR-X05, FR-X07 | Workable at the real admin ratio. |
| NFR-49 | Self-service or supervisor-mediated account recovery — no requirement for night-time… | Covered | QR-10, FR-X05 | No night-time administrator needed. |
| NFR-50 | Encryption at rest on the handset, keyed to the user credential | Covered | DC-3, QR-15 | Encrypted under a key derived from the credential. |
| NFR-51 | Hard cap on the volume of caseload data resident on a device — active caseload only, not full… | Covered | DC-3, QR-15 | Active caseload only. |
| NFR-52 | Field-level data sensitivity as a schema property, not a screen/presentation-layer control, so… | Covered | DC-2 | Sensitivity as a schema property. |
| NFR-53 | Read-audit log storage separate from the application database, so compromising the application… | Covered | FR-X02, QR-18 | Audit store separate from the application. |
| NFR-54 | Read-audit log retention measured in years, not days | Covered | FR-X02, QR-18 | Retained at least 7 years. |
| NFR-55 | Authentication model: device binding (enrolled once, cryptographic key) plus a short local PIN… | Covered | FR-A12, FR-X03, FR-X05, QR-16 | Device binding plus local credential. |
| NFR-56 | Session persists through a working session (hours of active use) with a short idle timeout (~2… | Covered | QR-16 | One entry per session; idle re-lock. |
| NFR-57 | Step-up (re-)authentication attached only to sensitive actions (viewing leprosy status,… | Partly | FR-D07, QR-16 | Finer-geography view needs a logged action; step-up for exports and out-of-catchment views is not itemised. |
| NFR-58 | Anomaly flagging on access patterns (e.g. many records from one account across multiple… | Backlog | – | Access-pattern anomaly flagging not in SRS. |
| NFR-59 | Authorisation enforced server-side in all cases, resistant to record-ID manipulation in… | Covered | FR-X01, QR-12 | Tested against ID manipulation. |
| NFR-60 | Every external dependency (SMS gateway, video platform, identity service) degrades gracefully… | Covered | DC-6, QR-24 | Graceful degradation of dependencies. |

## 5. How to explain this in an interview

*"The log captured every statement from the six interviews: 164 functional and non-functional lines. I merged duplicates, rewrote wishes as testable requirements, moved non-software items to field practice, and kept the rest in the SRS as 47 functional and 26 non-functional requirements. About 60% of the log lines are fully covered and another 17% partly covered, and I kept a list of the ones I left out or changed so the decisions can be reviewed."*
