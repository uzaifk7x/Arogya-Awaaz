# Arogya Awaaz — Phase-by-Phase Implementation Plan

**Event:** Solvothon — Kalyana Karnataka Krishi Kalpa Foundation  
**Product:** Arogya Awaaz  
**Build approach:** Complete one bounded phase, verify its acceptance criteria, record the handoff, and only then begin the next phase.

## 1. Product objective

Build a voice-first hospital grievance and service-monitoring web platform that supports Kannada, Hindi, Urdu, and English. It must register every accepted complaint, classify and route it, track staff action, escalate overdue or repeated issues, maintain a doctor-availability report trail, create a medicine-shortage register, and ask the patient to confirm resolution.

The platform has four product pillars:

1. Patient Voice Assistant.
2. AI Grievance Classification and Routing.
3. Hospital Management Dashboard.
4. Intelligent Hospital Service Monitoring.

## 2. Technical baseline

| Layer | Choice |
|---|---|
| Frontend | React + TypeScript + Node.js toolchain (Vite recommended) |
| UI | Tailwind CSS + shadcn/ui or equivalent accessible components |
| Data fetching | TanStack Query |
| Validation | Zod on frontend; Pydantic on backend |
| Forms | React Hook Form |
| Charts | Recharts |
| Localisation | i18next / react-i18next |
| Backend | Python + FastAPI |
| ORM/migrations | SQLAlchemy 2.x + Alembic |
| Database | PostgreSQL |
| STT/TTS | Bhashini adapters |
| AI | Gemini 3.5 Flash-Lite (`gemini-3.5-flash-lite`) |
| Live refresh | SSE initially |
| Analysis | PostgreSQL views; pandas/DuckDB only if needed |

Use current stable compatible package versions during Phase 1 and pin them in lockfiles. Do not assume a third-party provider has a free production tier; confirm limits, pricing, and permitted use before depending on it.

## 3. Working rules for AI coding agents

Apply these rules to every phase:

- Work **only on the phase assigned in the current prompt**. Do not start a later phase, even if it appears easy.
- First inspect the existing repository and report its current structure. Do not overwrite working code or recreate the project unnecessarily.
- Read `README.md`, `ARCHITECTURE.md`, and the relevant phase in this file before coding.
- Do not invent API endpoints, Bhashini service IDs, Gemini capabilities, CPGRAMS APIs, credentials, database tables, or hospital policies. Use official documentation and environment configuration.
- Keep secrets in environment variables. Never commit API keys or real patient information.
- Follow the architecture boundary: React client → FastAPI API → service layer → SQLAlchemy repository/models → PostgreSQL. External services are accessed through adapters.
- Keep AI output as an untrusted suggestion. Validate schema, normalise fields, resolve doctors/departments from approved master data, and apply deterministic business rules in Python.
- Do not let the LLM execute SQL, update tickets, close complaints, assign staff, send alerts, or submit CPGRAMS grievances directly.
- Add tests for every new business rule and API route. Do not delete or weaken existing tests to obtain a passing build.
- Keep changes small, typed, documented, and consistent with existing conventions.
- If a prerequisite is missing, stop and report the blocker. Do not invent a substitute without documenting it.
- At completion, report: files created/changed, behaviour implemented, commands executed, test results, known limitations, and exact next phase. Stop.

### Standard agent prompt header

Copy this header and append only the task prompt for the phase being performed:

```text
You are working on Arogya Awaaz. Read README.md, ARCHITECTURE.md, and only the assigned phase in IMPLEMENTATION_PLAN.md.
Execute only the assigned phase. Do not implement later phases or make unrelated refactors.
Inspect the existing repository before editing. Preserve working code. Do not invent external APIs or data.
Add tests for the assigned behaviour. Run the relevant tests and report exact results.
If blocked by missing credentials, configuration, or unclear requirements, implement a safe adapter/interface where possible and document the blocker; do not fake a successful integration.
At the end, update docs/BUILD_STATE.md using the handoff format in README.md, then stop.
```

## 4. Phase overview

| Phase | Name | Main result | Gate |
|---|---|---|---|
| 0 | Scope and acceptance freeze | Requirements and rule catalogue | Decisions recorded |
| 1 | Repository and local environment | React/FastAPI/Postgres skeleton | Both apps start |
| 2 | Database and migrations | Core schema and seed data | Migrations and constraints pass |
| 3 | Backend foundation and roles | Auth, permissions, audit event foundation | Role tests pass |
| 4 | Complaint registration core | Durable ticket creation and status API | Ticket lifecycle API passes |
| 5 | Patient voice UI | Multilingual accessible patient experience shell | UI flow works with mock transcript |
| 6 | Bhashini speech integration | ASR/TTS adapters and language flows | Real provider smoke tests pass where credentials exist |
| 7 | Gemini classification and entity resolution | Structured AI extraction and doctor/specialty matching | Schema and hallucination tests pass |
| 8 | Routing, doctor availability, and escalation | Deterministic rules and scheduled checks | Time-window and 48-hour tests pass |
| 9 | Medicine shortage register | Structured stock-out data and routing | Register/export/routing tests pass |
| 10 | Hospital management dashboard | Staff queues, ticket detail, analytics | End-to-end staff flow passes |
| 11 | Patient confirmation and anti-suppression | Verified closure and complaint integrity | False-closure tests pass |
| 12 | Emergency and CPGRAMS referral | Safety path and citizen-authorised external referral | No false automatic submission |
| 13 | QA, deployment, and hackathon demo | Tested, deployable MVP and demo data | Demo checklist passes |

---

## Phase 0 — Scope and acceptance freeze

**Goal:** Remove ambiguity before code is written.

### Tasks

1. Confirm product name, user roles, complaint categories, supported languages, and MVP platform.
2. Define complaint fields: language, transcript, corrected transcript, category, subcategory, location, department, urgency, optional contact method, reporter token, status, timestamps, assigned team, and audit history.
3. Define hospital master data required for departments, staff roles, doctors, specialties, doctor aliases, duty rosters, and escalation contacts.
4. Record the business rules in this document and `ARCHITECTURE.md`.
5. Confirm whether the word “Registration” for medicine complaints means the act of recording the complaint or the hospital Registration counter. **Default assumption:** record it in the Medicine Shortage Register and route it primarily to Pharmacy/Stores/Procurement; allow Registration to be a configurable secondary recipient.
6. Set a demo hospital, demo departments, demo doctors, and fake test patients. Do not use real patient data.

### Acceptance gate

- Four product pillars and user roles are documented.
- Every required rule has one unambiguous implementation statement.
- Demo seed data is clearly fictional.
- Open questions are listed rather than silently guessed.

### Agent task prompt

```text
PHASE 0 ONLY: Inspect the documentation and create a concise requirements/decision checklist for Arogya Awaaz. Do not write application code. Identify contradictions, missing configuration, data fields, user roles, and testable acceptance criteria. Preserve the stated defaults in this plan. Report unresolved questions and stop.
```

## Phase 1 — Repository and local environment

**Goal:** Create a clean, runnable monorepo without implementing product features.

### Tasks

1. Create `frontend/` using React, TypeScript, Vite, and Node.js/npm.
2. Add Tailwind CSS and a basic accessible design system.
3. Add `backend/` using FastAPI, Pydantic, SQLAlchemy, Alembic, and a PostgreSQL driver.
4. Add `.env.example` for frontend/backend configuration. No real credentials.
5. Add health endpoints and a simple frontend page that calls backend health.
6. Add formatting/linting/test commands and lockfiles.
7. Add Docker Compose for local PostgreSQL only if it improves local setup; keep it optional.

### Acceptance gate

- Frontend starts locally and renders a health state.
- FastAPI starts and `/health` returns a valid response.
- Backend can connect to the configured PostgreSQL instance.
- One command or documented commands reproduce the setup.
- No feature-specific mock logic is presented as a real integration.

### Agent task prompt

```text
PHASE 1 ONLY: Scaffold the React/TypeScript frontend and Python/FastAPI backend described in the plan. Add PostgreSQL configuration, environment examples, health checks, lint/test scripts, and setup documentation. Do not implement authentication, complaint logic, AI, Bhashini, or dashboards. Run startup checks and stop.
```

## Phase 2 — Database schema and migrations

**Goal:** Establish the source of truth before implementing workflows.

### Required initial entities

- `hospitals`
- `departments`
- `users`
- `roles` or role assignments
- `doctors`
- `specialties`
- `doctor_aliases`
- `doctor_shifts`
- `doctor_availability_reports`
- `complaints`
- `complaint_events` (append-only audit history)
- `complaint_assignments`
- `escalation_rules`
- `medicine_shortage_records`
- `patient_feedback`
- `notification_attempts`
- `cpgrams_referrals`

Use UUIDs internally. Generate a separate non-sequential public ticket reference/token. Add indexes for status, department, created time, assigned user, doctor, and escalation due time.

### Tasks

1. Define SQLAlchemy models and Pydantic DTOs.
2. Add Alembic initial migration.
3. Add constraints and foreign keys; use enums or constrained strings consistently.
4. Add seed scripts for fictional hospital departments, doctors, aliases, duty windows, escalation rules, and demo users.
5. Add a CSV export query for the medicine shortage register.
6. Avoid storing raw audio by default. Store transcript and provider metadata; make any audio retention an explicit, consent-based configuration.

### Acceptance gate

- Fresh database can be migrated from zero.
- Seed is repeatable and does not duplicate records.
- Foreign keys and unique constraints protect ticket references and master data.
- Complaint events cannot be casually overwritten by staff-facing update logic.

### Agent task prompt

```text
PHASE 2 ONLY: Implement the PostgreSQL schema, SQLAlchemy models, Pydantic schemas, Alembic migrations, and fictional seed data listed in the plan. Include medicine shortage, doctor directory/aliases/shifts, complaint events, feedback, escalation, and CPGRAMS referral tables. Do not implement API endpoints or frontend features. Add migration/model tests and stop.
```

## Phase 3 — Backend foundation, authentication, roles, and audit foundation

**Goal:** Protect the system and establish accountable identities.

### Roles

- `PATIENT_ANONYMOUS`: can create a complaint and access it using a secure receipt token.
- `PATIENT_CONTACTED`: same patient rights plus opted-in status notifications.
- `DEPARTMENT_STAFF`: can see and update complaints assigned to their department.
- `DEPARTMENT_SUPERVISOR`: can assign/reassign department work and review department queues.
- `GRIEVANCE_OFFICER`: can review cross-department complaints, escalations, conduct complaints, and appeals.
- `HOSPITAL_ADMIN`: can configure departments, rules, staff, doctors, and rosters.
- `SYSTEM_ADMIN`: restricted technical administration.

### Tasks

1. Implement staff authentication using secure, HTTP-only cookies or an equivalent well-secured mechanism.
2. Implement role-based and department-scoped authorisation.
3. Add password hashing and account/session controls.
4. Implement audit-event service for all sensitive state transitions.
5. Ensure ordinary staff cannot delete complaint records or edit historical events.
6. Add request IDs, structured logging, and consistent error responses.

### Acceptance gate

- Unauthenticated staff APIs are rejected.
- Department staff cannot access another department's tickets without explicit permission.
- Every sensitive write records actor, action, timestamp, and reason where relevant.
- No secret or personal data appears in application logs.

### Agent task prompt

```text
PHASE 3 ONLY: Implement backend authentication, role-based/department-scoped authorisation, password/session security, structured logging, and the append-only audit-event service. Use the roles in the plan. Do not build complaint business endpoints, AI, or UI. Add permission and audit tests; stop.
```

## Phase 4 — Complaint registration and core lifecycle API

**Goal:** Make internal complaint registration reliable before AI is added.

### Required API capabilities

- Create complaint from a manually supplied transcript (AI is not required yet).
- Read complaint using the private receipt token or authenticated staff access.
- List/search/filter complaints for authorised staff.
- Assign/reassign complaint to a configured department/team.
- Add a staff progress note.
- Move complaint through permitted states.
- Add an escalation event.

### Initial state machine

`SUBMITTED → CLASSIFIED → ASSIGNED → IN_PROGRESS → STAFF_MARKED_RESOLVED → AWAITING_PATIENT_CONFIRMATION → CLOSED`

Additional states: `NEEDS_CLARIFICATION`, `REOPENED`, `REJECTED_WITH_REASON`, `DUPLICATE_LINKED`, and `ESCALATED`. An escalation is preferably an event/flag, not a separate destructive status that hides the underlying work state.

### Reliability requirements

- Persist the complaint before returning a final public reference.
- Use an idempotency key so a retried network request does not create duplicate tickets.
- If a server write fails, return a clear retryable error; do not falsely announce registration.
- Public receipt tokens must be unguessable and should expose only a minimal patient-safe status view.

### Acceptance gate

- Complaint can be created, read, assigned, updated, and audited.
- Duplicate client retries with the same idempotency key return the same complaint.
- An ordinary staff user cannot delete or silently erase a ticket.
- Invalid state transitions are rejected.

### Agent task prompt

```text
PHASE 4 ONLY: Implement the core complaint registration and lifecycle APIs without AI or Bhashini. Support idempotent creation, secure public receipt lookup, staff search/list, assignment, progress notes, valid state transitions, and audit events. Add API and state-machine tests. Do not build dashboards. Stop after acceptance checks.
```

## Phase 5 — Patient Voice Assistant interface shell

**Goal:** Build the patient experience with a mock transcript adapter before connecting live speech services.

### Screens/states

1. Welcome and language selection: Kannada, Hindi, Urdu, English.
2. Large microphone control and clear recording state.
3. Transcript review/edit/read-back confirmation.
4. Conversational clarification for missing location, department, or doctor identity.
5. Submission confirmation with public reference and QR/receipt option.
6. Voice/tap-based complaint status lookup.
7. Emergency help action, visually distinct from ordinary grievance reporting.

### UX requirements

- Large touch targets and high contrast.
- Low-text, screen-reader-friendly layout.
- No mandatory patient account or phone number.
- Offer “I do not want to provide contact details”.
- Show when the microphone is active and when recording has stopped.
- Never imply that a draft/offline report is registered before the server confirms persistence.

### Acceptance gate

- Complete mock patient journey works on a mobile viewport and kiosk-size viewport.
- All four languages have a selectable UI shell and translation keys (human-reviewed translations can be filled in later).
- No microphone permission denial crashes the page; manual text fallback works.
- The patient can submit a text transcript and receive a real backend ticket.

### Agent task prompt

```text
PHASE 5 ONLY: Build the patient-facing React experience with language selection, microphone UI states, mock transcript, transcript confirmation, clarification prompts, complaint receipt, status lookup, and emergency action placeholder. Connect complaint submission to the existing API. Do not integrate Bhashini or Gemini yet. Ensure mobile/kiosk accessibility and tests; stop.
```

## Phase 6 — Bhashini ASR and TTS integration

**Goal:** Replace the mock speech adapter with real speech-to-text and text-to-speech.

### Tasks

1. Create a Bhashini integration adapter in FastAPI; do not call Bhashini directly from the browser.
2. Configure provider credentials and language/task service IDs through backend environment variables.
3. Support ASR for Kannada, Hindi, Urdu, and English; confirm the exact service/model selected for each language using current Bhashini documentation and account access.
4. Support TTS for the same four languages; test actual voice output and pronunciation.
5. Keep the original transcript and the patient-corrected transcript separately, with language and confidence/provider metadata.
6. If recognition is low confidence, ask the patient to repeat or confirm; never silently rewrite names, medicine details, or complaint facts.
7. Handle timeouts, provider failure, unsupported language, and rate limits with manual text fallback.
8. Keep raw audio ephemeral by default; only retain it when separately consented and necessary.

### Acceptance gate

- Real ASR and TTS smoke tests work for each configured language, or a documented provider limitation is shown rather than faked.
- Provider secrets remain on the server.
- Audio/transcription errors do not create false complaint submissions.
- Patient can review and correct the transcript.

### Agent task prompt

```text
PHASE 6 ONLY: Implement a server-side Bhashini ASR/TTS adapter for Kannada, Hindi, Urdu, and English. Verify exact service IDs and language coverage from current Bhashini documentation/account configuration; never invent IDs. Add mockable provider interfaces, timeout/retry handling, confidence/confirmation behaviour, and integration tests. Do not add Gemini classification or escalation logic. Stop and list any missing credentials or unsupported service.
```

## Phase 7 — Gemini classification and doctor/specialty entity resolution

**Goal:** Turn confirmed speech into a structured complaint draft without allowing the model to invent operational facts.

### AI responsibilities

Gemini 3.5 Flash-Lite (`gemini-3.5-flash-lite`) can suggest:

- complaint category and subcategory;
- short neutral summary;
- location phrase;
- department candidate;
- urgency candidate;
- doctor name candidate, if spoken;
- specialty candidate;
- medicine name/strength/form candidate;
- missing information requiring clarification;
- language and confidence metadata if available from the upstream speech adapter.

### Entity-resolution rules

- Maintain a hospital doctor directory with canonical name, staff identifier, department, specialty, aliases, and multilingual alias phrases.
- Map words such as “haddi doctor”, “bones doctor”, “orthopedic”, and approved Kannada/Urdu/Hindi equivalents to the **Orthopedics specialty candidate**.
- Only mention “Doctor Vikas” if the transcript names him or a deterministic directory match identifies him with adequate confidence.
- If more than one doctor matches, ask the patient to choose or send it for staff review.
- Never invent a doctor, specialty, room, stock quantity, appointment time, or officer.
- Do not state that a doctor was definitely absent merely because a patient reported it.

### Output contract

Use a strict Pydantic response schema. Reject extra fields, invalid categories, unsupported department IDs, and free-text instructions. Keep the raw model output for technical debugging only when policy permits; never trust it as an instruction.

### Acceptance gate

- Model returns valid structured output or a controlled retry/fallback.
- Tests cover Kannada/Hindi/Urdu/English examples, transliterated phrases, mixed-language phrases, missing entities, ambiguous doctors, and prompt-injection-like speech.
- The AI's candidate is resolved against database master data before a doctor name is spoken or a complaint is routed.
- Patient sees/hears the generated summary and can correct it before final submission.

### Agent task prompt

```text
PHASE 7 ONLY: Integrate Gemini 3.5 Flash-Lite using model ID gemini-3.5-flash-lite for structured complaint extraction. Create a strict validated schema and directory-backed doctor/specialty alias resolution. Handle code-switching and transliterated terms. Do not let the model write to the database or assign/close tickets. Do not implement escalation or CPGRAMS. Add hallucination/ambiguity tests and stop.
```

## Phase 8 — Department routing, doctor availability, and escalation engine

**Goal:** Turn approved complaint data into deterministic operational actions.

### General routing

- Category/subcategory maps to a configured department and default role.
- Staff-conduct complaints route to the grievance officer or a restricted management queue; do not route them to the person named in the complaint.
- Low-confidence or unrecognised departments go to a human triage queue.
- Keep the original patient wording alongside any neutral summary.

### Doctor unavailability workflow

For a configured 09:00–17:00 duty day, use these default reporting buckets:

| Bucket | Local hospital time |
|---|---|
| 1 | 09:00–11:00 |
| 2 | 11:00–13:00 |
| 3 | 13:00–15:00 |
| 4 | 15:00–17:00 |

A report at 16:00–17:00 belongs to bucket 4. Store the exact reported timestamp as well as its bucket. Configure duty hours and buckets per hospital/doctor; do not hard-code 09:00–17:00 globally.

Escalation rules for the prototype:

1. Three independent complaint submissions about the same doctor in the same duty day trigger higher-authority review.
2. Reports in three distinct two-hour buckets for the same doctor on the same duty day also trigger higher-authority review. The example 09:00–11:00, 11:00–13:00, and 16:00–17:00 therefore affects three distinct buckets and triggers review.
3. Multiple reports in one bucket increase corroboration but count as one affected bucket.
4. A retry of the same submission/session must not count as a new independent complaint.
5. First route the report to the department supervisor; once a threshold is met, escalate to the configured Medical Superintendent/designated higher officer and grievance officer.
6. Keep the report as `UNVERIFIED` until checked against the duty roster, attendance system, or authorised staff record. Store who verified it, when, and the evidence/reference used.

The AI may identify a doctor/specialty candidate, but the rule engine—not the AI—counts reports and performs escalation.

### Two-day no-update escalation

- For an open complaint, measure time since the last meaningful staff update.
- At 48 elapsed hours with no meaningful update, create an escalation event and notify the grievance officer/higher authority.
- A system-generated timestamp refresh, read receipt, or automated “still open” event does not count as meaningful progress.
- Make the time threshold configurable and use hospital local time for display.

### Acceptance gate

- Unit tests cover every bucket boundary and time zone/date rollover.
- Three distinct reports and three-bucket cases escalate correctly.
- Duplicate retries do not inflate counts.
- A report remains unverified until a permitted verification action is recorded.
- 48-hour overdue escalation is idempotent and does not send duplicate notifications on every worker run.

### Agent task prompt

```text
PHASE 8 ONLY: Implement deterministic category-to-department routing, configurable doctor duty windows, doctor-unavailability report counting, and 48-hour no-update escalation. Use the exact two-hour bucket and two doctor escalation thresholds in the plan. Keep patient reports unverified until an authorised check. Add comprehensive clock/time-zone/idempotency tests. Do not implement dashboard UI or CPGRAMS. Stop.
```

## Phase 9 — Medicine Shortage Register

**Goal:** Ensure every medicine-stock complaint becomes a structured operational record.

### Required fields

- linked complaint ID;
- hospital, pharmacy/store, and department;
- medicine name as spoken;
- normalised/generic name when verified;
- strength, form, and pack size when provided;
- prescribed/required quantity only if patient states it;
- date/time reported;
- patient language;
- verification status (`REPORTED`, `PHARMACY_VERIFIED`, `NOT_IN_STOCK`, `AVAILABLE`, `ORDER_RAISED`, `RESTOCKED`);
- stock-check note and authorised staff member;
- action/indent/procurement reference if one exists.

### Tasks

1. Create the `medicine_shortage_records` workflow linked to the complaint.
2. Add a searchable medicine-shortage register and CSV export.
3. Route the primary task to Pharmacy/Stores/Procurement according to hospital configuration.
4. Allow Registration to be an additional recipient only if the hospital explicitly configures it.
5. Do not interpret an AI-extracted name/strength as a verified inventory item; pharmacy staff must confirm it against the hospital catalogue.
6. Detect repeated reports for the same medicine/location and create a trend alert.

### Acceptance gate

- Each medicine out-of-stock complaint creates one linked shortage record.
- Missing medicine strength/name is marked unknown, not guessed.
- CSV export uses correct columns and does not expose unrelated patient contact details.
- Pharmacy/Stores routing is tested and configurable secondary recipients work.

### Agent task prompt

```text
PHASE 9 ONLY: Implement the Medicine Shortage Register, its linked complaint workflow, pharmacy/store/procurement routing, optional Registration secondary routing, search, and CSV export. Do not create an external spreadsheet integration or invent medicine stock levels. Add validation and routing tests. Stop.
```

## Phase 10 — Hospital management dashboard and monitoring views

**Goal:** Give department staff and hospital administrators the right operational view.

### Department staff view

- assigned tickets;
- status, priority, age, and due time;
- complaint summary and original transcript;
- department/location/doctor/medicine details;
- action notes and attachments (optional, privacy-controlled);
- update/resolve controls according to role.

### Grievance officer/admin view

- all open, overdue, escalated, and reopened complaints;
- department and category filters;
- complaints with repeated locations/categories;
- doctor unavailability alerts and verification state;
- medicine shortage register;
- staff assignment and audit trail;
- CPGRAMS referrals and returned reference IDs;
- analytics: volume, acknowledgement time, resolution time, reopen rate, overdue rate, and recurring hotspots.

### Tasks

1. Build dashboard pages using role-scoped APIs.
2. Add filters, pagination, search, and ticket detail.
3. Add charts from SQL aggregates/materialized views.
4. Add SSE updates for newly created/updated/escalated tickets.
5. Show sample/demo data with a visible “Demo data” label.

### Acceptance gate

- Staff only see the records their role permits.
- Dashboard counts match database test fixtures.
- Charts distinguish reported, verified, resolved, and patient-confirmed states.
- Live updates do not expose one patient's private details to unrelated users.

### Agent task prompt

```text
PHASE 10 ONLY: Build the role-aware React hospital dashboard for department staff, supervisors, grievance officers, and admins. Include ticket queues, filters, ticket details, medicine register, doctor availability alerts, overdue/escalated views, and SQL-backed metrics. Add SSE only if the backend event endpoint exists; otherwise use a clean polling adapter. Do not implement new backend business rules. Add frontend tests and stop.
```

## Phase 11 — Patient feedback, closure verification, and complaint integrity

**Goal:** Prevent “resolved” from meaning only “a staff member clicked a button.”

### Closure workflow

1. Staff selects `Mark work completed`, supplies an action-taken note, and optionally attaches permitted proof.
2. System changes the patient-facing state to `AWAITING_PATIENT_CONFIRMATION`, not final `CLOSED`.
3. If the patient opted into contact, send a consented SMS/voice callback/notification with a secure feedback link or short code.
4. If no contact was supplied, provide a private receipt token/QR so the patient can check status at a kiosk or return to the voice assistant and answer the confirmation prompt.
5. `Yes` → record patient confirmation and close.
6. `No` → reopen and escalate to the grievance officer/supervisor.
7. No response → keep `AWAITING_PATIENT_CONFIRMATION`; after a configurable review period, route to an independent grievance-officer review. Do not treat silence as confirmation.

### Anti-false-resolution controls

- Separate “staff marked complete” from “patient confirms resolved”.
- Preserve the full append-only timeline: submitter token, assignment, updates, staff notes, closure attempt, patient response, reopening, escalation.
- Staff cannot delete a ticket or edit prior events.
- Reassignment and rejection require a reason.
- A grievance officer can independently review disputed closures.
- Complaints about staff conduct are restricted from the named staff member.
- Never fabricate a patient response, OTP validation, photo proof, or successful callback.

### Acceptance gate

- Staff completion cannot immediately create a patient-confirmed closure.
- Anonymous patients can verify through receipt token/QR without contact details.
- `No` reopens; no response remains unconfirmed.
- All actions are auditable and ordinary staff cannot erase history.

### Agent task prompt

```text
PHASE 11 ONLY: Implement patient-confirmed closure, optional consented contact callbacks, anonymous receipt-token/QR feedback, reopen-on-No, no-response review, and immutable audit history. Do not add a mandatory phone number. Do not mark silence as consent. Add adversarial tests for falsely resolved and deleted complaints. Stop.
```

## Phase 12 — Emergency pathway and CPGRAMS referral adapter

**Goal:** Handle urgent cases safely and make external escalation traceable without pretending an unapproved integration exists.

### Emergency pathway

- Provide a permanent, prominent emergency action in the patient UI.
- Trigger an immediate spoken prompt in the selected language: “For immediate medical help, alert the nearest nurse/doctor or hospital emergency desk now. Do not wait for this complaint system.”
- Send an on-site alert to the hospital's configured emergency response role if the facility has approved that workflow.
- Create a separate urgent incident record for audit if permitted, without delaying the immediate instruction.
- Emergency keyword detection may suggest an urgent path, but it must not diagnose or replace hospital triage.
- Do not claim to dispatch an ambulance or call emergency services unless that integration is explicitly implemented, approved, tested, and visible to the user.

### CPGRAMS rules

- Every Arogya Awaaz grievance is logged internally.
- CPGRAMS is an external citizen portal for service-related grievances against public authorities. Arogya Awaaz must not submit every internal complaint to CPGRAMS indiscriminately.
- Offer a **CPGRAMS referral** when the grievance appears to concern an eligible public authority/public service and the citizen chooses to proceed.
- Show the citizen the proposed summary and data to be shared; obtain explicit confirmation before opening/submitting externally.
- If no approved CPGRAMS API/integration contract has been provided by the relevant authority, use a citizen-assisted workflow: generate a concise complaint summary/evidence packet, open the official portal, let the citizen or authorised official submit it, and record the returned CPGRAMS registration ID.
- Do not scrape the portal, automate login/OTP, store CPGRAMS passwords, or claim automatic submission.
- Build a `CPGRAMSAdapter` interface that can use an official API only after the relevant public authority/NIC provides a supported endpoint, credentials, authorisation, and test environment.
- Store referral state: `NOT_APPLICABLE`, `OFFERED`, `CONSENTED`, `READY_FOR_USER_SUBMISSION`, `SUBMITTED_BY_CITIZEN`, `REFERENCE_RECORDED`, `DECLINED`, `FAILED`. The application can mark `SUBMITTED_BY_CITIZEN` only after user confirmation or a verified authorised integration response.

### Acceptance gate

- Emergency action is available without AI and clearly says to alert nearby staff immediately.
- CPGRAMS link points to the official portal.
- No fake CPGRAMS reference ID can be created.
- Citizen consent and the returned portal reference are recorded.
- No unauthorised portal automation is present.

### Agent task prompt

```text
PHASE 12 ONLY: Implement the urgent on-site help pathway and a CPGRAMS referral adapter with a citizen-assisted fallback. Do not automate portal login, OTP, scraping, or submission without an official authorised API contract. Every grievance remains internally logged. Add consent, referral status, and reference-ID validation. Add tests proving emergency instructions do not wait for Gemini. Stop.
```

## Phase 13 — End-to-end QA, deployment, and hackathon demonstration

**Goal:** Prove that the full story works reliably and honestly.

### Required test journeys

1. Kannada-speaking patient reports a three-hour diagnostic delay; ticket is registered and routed.
2. Hindi/Urdu mixed-language patient says “haddi doctor nahi hai”; system maps the phrase to Orthopedics, asks for clarification if the doctor is ambiguous, and never invents a doctor.
3. Three independent reports about the same doctor or three distinct affected duty buckets trigger higher-authority review.
4. A 16:30 report is grouped into 15:00–17:00.
5. Open complaint with no meaningful update for 48 hours escalates exactly once.
6. Medicine stock-out creates a medicine register row and routes to Pharmacy/Stores.
7. Staff marks completed; patient says “No”; complaint reopens.
8. Anonymous patient checks a complaint with a secure receipt token and confirms resolution.
9. Complaint about rude staff is visible only to authorised grievance officers/managers.
10. Patient uses emergency action while Gemini/Bhashini is unavailable; immediate on-screen/spoken safety instruction still appears.
11. CPGRAMS referral is offered only where configured/eligible and cannot be marked submitted without citizen confirmation or authorised response.
12. Bhashini outage falls back to text entry; database outage never produces a false successful registration message.

### Deployment tasks

- Use environment variables and managed secrets.
- Use HTTPS and secure cookie settings.
- Apply migrations on deployment through a controlled step.
- Configure database backups and log retention.
- Seed only fictional demo data in the hackathon environment.
- Configure CORS and allowed origins explicitly.
- Add a simple status/health page and provider health checks.
- Prepare a local demo fallback if internet/API quota fails; clearly label mock mode.

### Acceptance gate

- All critical journeys pass in a recorded rehearsal.
- No patient-identifying real data is used in the presentation environment.
- All external provider calls either work or show a truthful fallback.
- Demo rehearsed with a time limit and a backup video/screenshots.
- Known limitations are disclosed in the final slide/Q&A notes.

### Agent task prompt

```text
PHASE 13 ONLY: Run end-to-end QA, fix only defects that prevent the specified journeys, prepare environment/deployment instructions, seed fictional demo data, and create a deterministic hackathon demo script. Do not add new product features. Run all tests and record exact results, known limitations, and demo fallback behaviour. Stop.
```

---

## 5. Build-state handoff format

Create `docs/BUILD_STATE.md` after Phase 1 and update it after every accepted phase. Copy this structure:

```markdown
# Arogya Awaaz — Build State

- Last completed phase:
- Current repository commit/branch:
- Date updated:

## Implemented
- ...

## Files changed
- ...

## Commands run and results
- ...

## Tests
- Passing:
- Failing:
- Not run:

## Configuration still required
- ...

## Known issues / decisions
- ...

## Exact next task
- Phase:
- Goal:
- First file/area to inspect:
```

When continuing in a new agent session, provide `README.md`, `ARCHITECTURE.md`, `SYSTEM_WORKFLOW.md`, this implementation plan, and the latest `docs/BUILD_STATE.md`. Ask the agent to work on the exact next phase only.

## 6. Final definition of done

The MVP is ready when a patient can speak or type a complaint in one of the four target languages, confirm the transcript, receive a real internal ticket, and later verify the outcome; staff can assign and act on it; the system can flag doctor unavailability and medicine shortages; a 48-hour no-update rule can escalate; repeated issues are visible to management; and the full activity trail is preserved. The system must not claim unapproved CPGRAMS automation, unverified doctor absence, medical diagnosis, or patient-confirmed closure without evidence.
