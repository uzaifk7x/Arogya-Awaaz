# Arogya Awaaz

**Solvothon — Kalyana Karnataka Krishi Kalpa Foundation**

> **Speak in your language. Be heard. Get tracked.**

Arogya Awaaz is a multilingual, voice-first hospital grievance and service-monitoring platform. Patients and attendants report hospital service issues through speech; the system creates a traceable grievance, routes it to the responsible team, monitors action deadlines, and helps hospital administrators identify repeated service failures.

This project is focused on **hospital services, access, staff responsiveness, and grievance accountability**. It is not a diagnostic system and does not replace clinical triage, emergency care, hospital staff, or official grievance authorities.

## The problem

A patient may wait three hours for a diagnostic test, find that the scheduled doctor is unavailable, be unable to obtain a prescribed medicine, encounter unhygienic facilities or rude staff, or be unable to explain a problem because the complaint desk does not support the patient's language. Complaints may be missed, left without an update, or marked resolved without the patient's agreement.

Arogya Awaaz addresses these failures through four connected capabilities:

1. **Patient Voice Assistant** — voice-first reporting and status checks in Kannada, Hindi, Urdu, and English.
2. **AI Grievance Classification and Routing** — speech transcription, structured complaint extraction, department mapping, doctor/specialty matching, and priority suggestions.
3. **Hospital Management Dashboard** — a complete complaint register, staff assignment, status history, response deadlines, escalation queue, and management overview.
4. **Intelligent Hospital Service Monitoring** — repeat-issue detection, doctor-unavailability patterns, medicine-shortage records, overdue-ticket escalation, and trend analytics.

## Core outcomes

- Every successfully submitted complaint receives a durable internal record and unique reference.
- A patient can submit a complaint without typing or speaking English.
- A complaint is routed to a configured department and accountable role.
- Staff actions and status changes are retained in an audit trail.
- A staff member cannot silently erase a complaint or close it as patient-confirmed without verification.
- Repeated and overdue issues reach an appropriate higher authority.
- Administrators can see recurring service failures rather than only individual tickets.

## Supported complaint areas

| Complaint area | Examples | Default owner |
|---|---|---|
| Waiting and diagnostics | Three-hour diagnostic wait, delayed test, queue not moving | Diagnostic department / patient-relations desk |
| Doctor availability | Scheduled doctor not available, specialist unavailable | Department head / Medical Superintendent review |
| Pharmacy and medicines | Prescribed medicine out of stock, pharmacy counter delay | Pharmacy / Stores / Procurement |
| Hygiene and facilities | Unclean washroom, no drinking water, broken lift or bed | Housekeeping / Facilities |
| Staff conduct and responsiveness | Rude staff, unresponsive desk, complaint not acknowledged | Grievance officer / department supervisor |
| Language and accessibility | Patient cannot communicate, missing wheelchair assistance | Patient-relations / accessibility coordinator |
| Billing and registration | Billing queue or registration delay, incorrect service handling | Billing / Registration |
| Safety and urgent situations | Immediate danger, violence, fire, or urgent medical help needed | On-site emergency response team |

Hospital administrators must configure the final department map, officer roles, service deadlines, duty rosters, and escalation recipients before a live deployment.

## Technology decisions

| Layer | Technology |
|---|---|
| Frontend | React + TypeScript, built and managed with Node.js and npm |
| UI | Tailwind CSS, shadcn/ui or an equivalent accessible component system |
| Frontend data | TanStack Query; React Hook Form + Zod for forms |
| Charts | Recharts |
| Internationalisation | i18next / react-i18next |
| Backend | Python + FastAPI + Pydantic |
| Database | PostgreSQL; SQLAlchemy 2.x; Alembic migrations |
| Speech-to-text | Bhashini ASR, selected/configured per language |
| Text-to-speech | Bhashini TTS, selected/configured per language |
| AI classification | Gemini 3.5 Flash-Lite, model ID `gemini-3.5-flash-lite` |
| Live updates | Server-Sent Events (SSE) initially; WebSockets only if a demonstrated need exists |
| Analysis | PostgreSQL SQL views/materialized views; pandas or DuckDB for offline analysis if needed |
| Testing | Pytest, HTTPX, Vitest, React Testing Library, Playwright |

The model name and Bhashini service availability must be checked against the provider documentation at implementation time. Never hard-code a model or service ID into application logic; put them in environment configuration.

## Repository documentation

- [`IMPLEMENTATION_PLAN.md`](./docs/IMPLEMENTATION_PLAN.md) — ordered build phases, bounded agent tasks, acceptance checks, and restart protocol.
- [`ARCHITECTURE.md`](./docs/ARCHITECTURE.md) — component architecture, data model, API boundaries, rules, safety, and security.
- [`SYSTEM_WORKFLOW.md`](./docs/SYSTEM_WORKFLOW.md) — complete patient-to-closure workflow and exception paths.
- [`PRESENTATION_SCRIPT.md`](./docs/PRESENTATION_SCRIPT.md) — Solvothon story, slide-by-slide script, visual design, and animation directions.

## Suggested repository structure

```text
arogya-awaaz/
├── README.md
├── IMPLEMENTATION_PLAN.md
├── ARCHITECTURE.md
├── SYSTEM_WORKFLOW.md
├── PRESENTATION_SCRIPT.md
├── frontend/
│   ├── src/
│   │   ├── app/
│   │   ├── components/
│   │   ├── features/
│   │   ├── i18n/
│   │   ├── lib/
│   │   └── types/
│   ├── public/
│   └── package.json
├── backend/
│   ├── app/
│   │   ├── api/
│   │   ├── core/
│   │   ├── db/
│   │   ├── models/
│   │   ├── schemas/
│   │   ├── services/
│   │   ├── integrations/
│   │   └── workers/
│   ├── migrations/
│   ├── tests/
│   └── pyproject.toml
├── docs/
│   └── BUILD_STATE.md
└── .env.example
```

## Non-negotiable product rules

1. **Internal registration is mandatory.** Every successfully accepted complaint is persisted before the API returns a final reference. If the network is unavailable, the client may keep an encrypted/local pending submission and clearly label it as pending sync; it must not claim that the server has registered it until it receives server confirmation.
2. **The AI proposes; the application validates.** Gemini may produce a structured draft. Backend code validates it, resolves entities against hospital master data, applies deterministic routing rules, and writes the record. The model never writes directly to PostgreSQL or sends a notification by itself.
3. **Never invent a doctor.** Doctor names and specialties must resolve against the hospital's approved doctor directory. Ambiguous references require a clarifying question or staff review.
4. **A reported absence is not a verified absence.** Patient reports are stored as reports. A roster/attendance check or authorised staff action is required before the system labels an absence verified.
5. **Staff resolution is not patient confirmation.** A staff member can mark work as completed, but the patient-facing state remains `AWAITING_PATIENT_CONFIRMATION` until confirmation or an authorised independent review.
6. **No complaint deletion by ordinary staff.** Records and status transitions are append-only in the audit history. Corrections require a new event and a reason.
7. **Emergency help is not an ordinary ticket.** An emergency action must immediately instruct the user to alert nearby hospital staff and notify the configured on-site response team. It must not wait for AI classification or ordinary ticket processing.
8. **CPGRAMS is not an automatic dump target.** Every complaint is logged internally. A CPGRAMS referral is a separate citizen-authorised process for an eligible public-authority grievance, unless an authorised official integration is made available by the relevant authority.
9. **Medicine shortages have a dedicated register.** Each relevant complaint creates a structured medicine-shortage entry and is routed primarily to Pharmacy/Stores/Procurement. A hospital may configure the Registration desk as a secondary recipient if its process requires that.
10. **All deadlines are configurable.** The proposed two-day no-update escalation and doctor-availability thresholds are configurable hospital rules, not claims about universal statutory deadlines.

## Key operational rules for the prototype

- **No meaningful update for 48 hours:** escalate an open complaint to the designated grievance officer/higher authority. A system heartbeat does not count as a meaningful update.
- **Doctor availability:** use the hospital duty roster. For a 09:00–17:00 shift, the default two-hour buckets are 09:00–11:00, 11:00–13:00, 13:00–15:00, and 15:00–17:00. A report at 16:30 belongs to the final bucket. Three independent reports about the same doctor in one duty day trigger higher-authority review; reports in three distinct time buckets also trigger escalation. Multiple reports in one bucket strengthen the evidence but do not create additional affected buckets.
- **Medicine out of stock:** create a row in the Medicine Shortage Register (database table with CSV export), link it to the complaint, and route it to Pharmacy/Stores/Procurement. The AI must not invent medicine strength, brand, or stock status.
- **False resolution prevention:** record a staff completion note and timestamp, then seek patient confirmation through an optional SMS/voice callback or a private ticket code/QR at a kiosk. A `No` response reopens the complaint. No contact detail is required to submit a complaint.

## Start here

1. Read `IMPLEMENTATION_PLAN.md` from Phase 0 onward.
2. Read the corresponding section of `ARCHITECTURE.md` before implementing a subsystem.
3. Give an AI coding agent **one phase only** and require it to stop at that phase's acceptance gate.
4. After a phase is accepted, update `docs/BUILD_STATE.md` with changed files, tests, decisions, and the next phase.
5. Do not start the next phase while the current phase has failing acceptance checks.

## External references

- [Gemini 3.5 Flash-Lite model documentation](https://ai.google.dev/gemini-api/docs/models/gemini-3.5-flash-lite) — model ID `gemini-3.5-flash-lite`.
- [Gemini API models overview](https://ai.google.dev/gemini-api/docs/models).
- [Bhashini API documentation](https://bhashini.gitbook.io/bhashini-apis) and [available Bhashini model/service IDs](https://dibd-bhashini.gitbook.io/bhashini-apis/available-models-for-usage) — confirm current ASR/TTS coverage and service IDs before integration.
- [CPGRAMS portal](https://pgportal.gov.in/).
- [DARPG Comprehensive Guidelines for Handling Public Grievances, 23 August 2024](https://www.darpg.gov.in/sites/default/files/Comprehensive_guidelines_for_handling_the_Public_Grievances.pdf).

---

**Project status:** Planning baseline. No production hospital integration, CPGRAMS API access, or clinical/emergency-service integration is assumed by this document.
