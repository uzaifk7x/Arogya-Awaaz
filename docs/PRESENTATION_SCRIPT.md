# Arogya Awaaz — Solvothon Presentation Script and Slide Direction

**Event:** Solvothon — Kalyana Karnataka Krishi Kalpa Foundation  
**Project:** Arogya Awaaz  
**Recommended presentation length:** 7 minutes to 7 minutes 20 seconds + demo/Q&A  
**Recommended slide count:** 10 main slides  
**Story:** One patient's voice exposes a service failure; Arogya Awaaz turns that voice into a tracked action, verifies the outcome, and helps the hospital prevent the next failure.

## 1. The story and the central message

The presentation should follow one illustrative patient journey rather than starting with technology. The patient waits for a diagnostic test, cannot easily communicate in the hospital's dominant language, and does not know whether the complaint will be acted upon. The story then reveals four capabilities:

1. Patient Voice Assistant.
2. AI Grievance Classification and Routing.
3. Hospital Management Dashboard.
4. Intelligent Hospital Service Monitoring.

The ending returns to the patient: not “the AI answered”, but “the issue was acted on and the patient could verify the result”.

**Core line:** “Arogya Awaaz does not just collect complaints. It turns every accepted complaint into a traceable action and every repeated complaint into a signal for hospital improvement.”

All patient scenes and example figures in the deck must be labelled as an **illustrative scenario/demo**, not real hospital statistics or a claim about a named hospital.

## 2. Visual direction

### Design style

Use a premium public-service technology aesthetic: cinematic but restrained, human-first, clear, and credible. Avoid a generic hospital stock-photo deck or a crowded software feature list.

### Suggested palette

| Use | Colour |
|---|---|
| Main background | Deep navy `#071C2C` |
| Secondary surface | Slate `#102A3A` |
| Primary accent | Teal `#18B6A4` |
| Warm highlight | Saffron `#F3A712` |
| Main text | Warm white `#F5F7F8` |
| Secondary text | Mist grey `#B8C6CE` |
| Emergency only | Coral red `#E45B5B` |

Use teal for accessible voice/positive progress, saffron for attention/escalation, and red only for emergency or critical status. Keep colour meaning consistent.

### Typography

- English headings: Manrope, Inter, or Aptos Display.
- Body: Inter or Aptos.
- Indian-language examples: Noto Sans Kannada, Noto Sans Devanagari, and a font with Urdu script support such as Noto Nastaliq Urdu where available. Verify glyphs on the actual presentation machine.
- Use 30–36 pt or larger for major slide titles, 20–24 pt for body where possible, and avoid dense paragraphs.

### Layout

- 16:9 widescreen.
- One main idea per slide.
- Use large headlines and short on-slide phrases; keep detail in speaker notes.
- Maintain generous margins and a consistent footer with slide number and Arogya Awaaz wordmark.
- Use custom vector diagrams and UI mockups where possible. Use patient imagery respectfully; do not use identifiable patient photographs or imply a real hospital endorsed the concept.

## 3. Motion and animation system

The deck should feel polished, not noisy. Use motion to make the workflow understandable.

### Recommended transitions

- Default slide transition: Fade, 0.35–0.5 seconds.
- Use Morph between Slides 3–7 when the same complaint ticket visually travels through the four pillars.
- Use Wipe for a timeline or routing line moving from patient to department.
- Avoid spinning, bouncing, random zooms, and sound effects.

### Reusable motion graphics

1. **Voice waveform:** a restrained animated waveform appears as the patient speaks. Use a short looping GIF/video or PowerPoint equalizer bars; stop the animation after transcription.
2. **Speech-to-ticket transformation:** language wave → transcript text → structured fields → ticket ID. Reveal one stage at a time.
3. **Routing path:** a thin teal line travels from the ticket card to the department card; the relevant department lights up.
4. **SLA clock:** a circular progress ring fills; when overdue, use a saffron highlight and an escalation arrow.
5. **Doctor availability timeline:** reveal 09–11, 11–13, 13–15, 15–17 slots. Highlight three affected slots and animate an escalation line to the Medical Superintendent.
6. **Repeat-issue cluster:** multiple small complaint dots collect into one Ward A hotspot. Keep it clearly labelled as illustrative.
7. **Verified closure:** staff completion changes to “Awaiting patient confirmation”; only after a patient “Yes” does the final check appear.

If using PowerPoint, build elements as editable shapes where practical. Use Morph, Fade, Wipe, and simple motion paths. Keep animations under control so the deck runs smoothly on a standard laptop. Do not rely on a live internet connection for video or audio.

## 4. Slide-by-slide script

---

## Slide 1 — Opening: “Three hours. Still waiting.”

**Time:** 35 seconds  
**Purpose:** Create an immediate human connection.

### On-slide text

**THREE HOURS. STILL WAITING.**

A patient needs a diagnostic test. No clear update. No easy way to be heard.

Small footer: *Illustrative patient scenario*

### Visual composition

- Deep navy full-bleed background.
- Left side: large digital-style timer `03:00:00`.
- Right side: understated corridor/waiting-area silhouette or abstract hospital corridor illustration.
- Small audio waveform or waiting-room indicator.
- No logos or dense data on the opening slide.

### Animation

1. Fade in the corridor silhouette.
2. Timer counts from `00:00:03` to `03:00:00` quickly (or use three staged timer values if a true count-up is unreliable).
3. Reveal “Still waiting.”
4. Pause for a beat before speaking the product name.

### Speaker script

“Imagine coming to a hospital for a diagnostic test. You are told to wait. One hour passes, then two, then three. You want to ask what is happening, but you do not know whom to approach. You may not speak the language used at the counter. And you are not sure whether anyone will record your complaint. This is not just a waiting-time problem. It is a problem of being heard and getting a response.”

### Transition

Use a Fade. Carry the same patient story into the next slide.

---

## Slide 2 — The problem: “The complaint can disappear before the problem is fixed.”

**Time:** 40 seconds  
**Purpose:** Expand from the opening story to the system-level pain points.

### On-slide text

**THE PROBLEM IS BIGGER THAN A WAITING ROOM.**

- Doctors unavailable during duty hours
- Long diagnostic and registration queues
- Medicine stock-outs and pharmacy delays
- Unhygienic facilities and rude/unresponsive staff
- Language barriers
- Complaints left unchecked, suppressed, or falsely marked resolved

### Visual composition

Use six concise issue tiles arranged around the patient silhouette. Use simple line icons: clock, stethoscope, medicine box, water/facility, speech bubbles, warning/audit trail.

### Animation

Reveal issue tiles in two waves:

1. Operational failures: wait, doctor, medicine.
2. Accountability failures: hygiene, language, silence/false closure.

The final tile, “No clear accountability”, should be the visual anchor.

### Speaker script

“The problem is not limited to one diagnostic queue. A doctor may not be available during scheduled hours. Medicines may be out of stock. A washroom may remain unhygienic. Staff may not respond. A patient may speak Kannada, Hindi, or Urdu but find no accessible way to report the issue. And even after a complaint is made, it can remain unchecked—or be marked resolved without the patient agreeing. We need a system that records, routes, monitors, and verifies.”

### Transition

Morph the issue tiles into a single voice waveform that becomes the Arogya Awaaz logo/title.

---

## Slide 3 — The solution: “Arogya Awaaz”

**Time:** 35 seconds  
**Purpose:** Name the product and explain the promise.

### On-slide text

# AROGYA AWAAZ

**Speak in your language. Be heard. Get tracked.**

Voice-first hospital grievance and service monitoring.

### Visual composition

- Large Arogya Awaaz wordmark in the centre.
- A voice waveform travels into a clean complaint ticket card.
- Small language labels: ಕನ್ನಡ · हिन्दी · اردو · English.
- Below: `Report → Route → Resolve → Verify → Improve`.

### Animation

Animate the waveform into a ticket reference. Then reveal the five-step lifecycle from left to right.

### Speaker script

“Arogya Awaaz is a multilingual, voice-first hospital grievance and service-monitoring platform. A patient speaks naturally. The system turns that speech into a confirmed, structured complaint, routes it to the responsible department, tracks the action, and asks the patient whether the issue was actually resolved.”

### Transition

Use Morph to enlarge the first step, “Report”, into Slide 4.

---

## Slide 4 — Pillar 1: Patient Voice Assistant

**Time:** 45 seconds  
**Purpose:** Make language accessibility tangible.

### On-slide text

**1. PATIENT VOICE ASSISTANT**

**No form. No language barrier. Just speak.**

Kannada | Hindi | Urdu | English

### Visual composition

Show a clean mobile/kiosk UI mockup:

- language selector;
- large microphone button;
- animated waveform;
- transcript card;
- Confirm / Edit / Repeat controls;
- “Contact details optional” note.

Use a speech example in mixed Hindi/English:

> “Haddi ka doctor nahi hai. I have been waiting in Orthopedics.”

### Animation

1. Language chips appear.
2. Microphone pulses once while waveform moves.
3. Transcript appears line by line.
4. Patient taps Confirm.
5. A ticket draft appears.

### Speaker script

“Our first pillar is the Patient Voice Assistant. A patient can speak in Kannada, Hindi, Urdu, or English. Bhashini converts speech to text. Before submission, the patient can hear or read the transcript, correct it, and confirm it. A phone number is optional. A patient who does not want to type or disclose contact details can still receive a private complaint reference and follow up later.”

### Transition

The confirmed transcript card slides into a structured AI card on Slide 5.

---

## Slide 5 — Pillar 2: AI Grievance Classification and Routing

**Time:** 55 seconds  
**Purpose:** Show useful AI, not an AI chatbot for its own sake.

### On-slide text

**2. AI CLASSIFICATION & ROUTING**

**From natural speech to an accountable department.**

`Haddi doctor` → `Orthopedics` → `Doctor directory check` → `Department ticket`

### Visual composition

Use a left-to-right pipeline with four stages:

1. Confirmed patient transcript.
2. Gemini 3.5 Flash-Lite structured extraction.
3. Hospital directory match.
4. Assigned department and ticket.

Show a sample structured card:

- Category: Doctor availability
- Specialty: Orthopedics
- Doctor: Not confirmed / directory match required
- Priority: Review
- Status: Reported, awaiting verification

### Animation

1. Phrase highlights.
2. `ORTHOPEDICS` label appears.
3. Directory card checks for a matching doctor.
4. If one exact match exists, show the canonical name; otherwise show “Clarification needed”.
5. Routing line reaches the department inbox.

### Speaker script

“Our second pillar is AI classification and routing. The patient does not need to know the official department name. If someone says ‘haddi doctor’, the system can map that phrase to the Orthopedics specialty using multilingual aliases. Gemini 3.5 Flash-Lite extracts the complaint fields. The backend then checks the hospital's approved doctor and department directory. It never invents a doctor. If the patient mentions Doctor Vikas and that name matches the directory, the ticket can identify him. If the match is unclear, the system asks instead of guessing. The complaint is still recorded, with the reported availability clearly marked as unverified.”

### Transition

Follow the ticket card into the staff dashboard using Morph.

---

## Slide 6 — Pillar 3: Hospital Management Dashboard

**Time:** 45 seconds  
**Purpose:** Show how complaints become staff action.

### On-slide text

**3. HOSPITAL MANAGEMENT DASHBOARD**

**Every complaint has an owner, a status, and a history.**

- Assigned department
- Staff action timeline
- Open / In progress / Awaiting confirmation
- Overdue and escalated queue

### Visual composition

Use a realistic but fictional dashboard mockup. Show:

- KPI strip: Open, In progress, Overdue, Awaiting patient confirmation;
- ticket queue with category, department, age, and status;
- ticket detail drawer with action history;
- role label such as “Housekeeping Supervisor” or “Grievance Officer”.

If showing numeric KPIs, label them **Demo data**. Do not imply real hospital adoption or measured impact.

### Animation

1. Ticket card enters the “New” queue.
2. Staff assignment chip appears.
3. Status moves to “In progress”.
4. A timeline adds an action note.
5. The overdue panel highlights an untouched ticket.

### Speaker script

“Our third pillar is the Hospital Management Dashboard. Department staff see the complaints assigned to them. Supervisors can reassign and investigate. Grievance officers see cross-department complaints, overdue tickets, and complaints that have been reopened. Every update has a timestamp and an accountable actor. A complaint cannot simply disappear because someone changed its status.”

### Transition

Zoom into the overdue indicator; let the SLA clock become the centre of Slide 7.

---

## Slide 7 — Pillar 4: Intelligent Hospital Service Monitoring

**Time:** 70 seconds  
**Purpose:** Deliver the most memorable differentiator.

### On-slide text

**4. INTELLIGENT SERVICE MONITORING**

**One complaint is a report. A repeated pattern is a warning.**

Three operational signals:

1. Doctor availability patterns
2. Medicine shortage register
3. Repeated and overdue complaints

### Visual composition

Divide the slide into three clean zones.

**A. Doctor availability timeline**

`09–11` | `11–13` | `13–15` | `15–17`

Highlight reports in 09–11, 11–13, and 15–17. Show a line to “Medical Superintendent / designated higher officer”. Add a small note: “Patient reports are unverified until checked.”

**B. Medicine Shortage Register**

A table row: Medicine as reported | Ward/Pharmacy | Reported time | Verification state | Assigned to Pharmacy/Stores.

**C. Repeated issue and SLA signals**

Show a group of similar sanitation complaint dots converging on “Ward A hotspot”. Show an overdue card “No meaningful update for 48 hours → Escalation”. Label the hotspot as illustrative.

### Animation

1. Reveal the four duty windows.
2. Highlight three affected windows in sequence.
3. Animate an escalation line to the higher authority.
4. Slide a medicine report into the shortage register.
5. Merge repeated complaint dots into a hotspot.
6. Show the 48-hour timer reaching the escalation marker.

### Speaker script

“Our fourth pillar is Intelligent Hospital Service Monitoring. Consider a doctor scheduled from nine to five. Patients report that the doctor was unavailable between nine and eleven, again between eleven and one, and again between four and five. The platform stores the exact report times and maps them into two-hour duty windows. Three independent reports in a day—or three distinct affected windows—trigger higher-authority review. The system does not declare the doctor absent; the authorised hospital officer verifies the roster and attendance.

A medicine stock-out complaint also creates a row in a dedicated Medicine Shortage Register and goes to Pharmacy or Stores. If a complaint receives no meaningful update for 48 hours, it is escalated. Repeated complaints from the same place become a hotspot for management to investigate. This is how Arogya Awaaz moves from ticket handling to service improvement.”

### Transition

The escalation line reaches a verification checkmark, leading into Slide 8.

---

## Slide 8 — Trust: “Resolved by staff is not the same as resolved for the patient.”

**Time:** 45 seconds  
**Purpose:** Address the false-resolution and suppression problem directly.

### On-slide text

**CLOSURE MUST BE VERIFIED.**

Staff marks work completed → Patient confirms → Close

Patient says “No” → Reopen + escalate

No contact details? Use a private ticket QR/reference at the kiosk.

### Visual composition

Show two parallel closure paths:

- Staff completion card: `Work completed`.
- Patient confirmation card: `Yes / No`.

Below, show an immutable event timeline and a secure anonymous ticket QR illustration.

Add a small side note: “No response is not a Yes.”

### Animation

1. Staff selects “Work completed”.
2. State changes to “Awaiting patient confirmation”.
3. Reveal a patient “No” choice; ticket returns to “Reopened”.
4. Reveal an alternative patient “Yes” path; ticket closes.
5. Show audit events stacking beneath both paths.

### Speaker script

“We also considered a critical risk: what if a complaint is marked resolved even though the patient's problem remains? Staff completion and patient confirmation are separate states. If the patient has voluntarily shared a contact method, the system can request confirmation by SMS or voice. If not, the patient can use a private QR code or reference at the kiosk. A ‘No’ reopens the issue. Silence never counts as confirmation. The audit history prevents ordinary staff from deleting or silently rewriting a complaint.”

### Transition

Fade to a simple patient-to-hospital-to-government referral path.

---

## Slide 9 — Safety, emergency, and public grievance referral

**Time:** 40 seconds  
**Purpose:** Show responsible boundaries and external accountability.

### On-slide text

**BUILT FOR REAL-WORLD RESPONSIBILITY.**

- Emergency action: alert nearby hospital staff immediately
- CPGRAMS referral: citizen-authorised and eligibility-aware
- Privacy: contact details optional; minimum data collected
- AI: assists classification; hospital staff remain accountable

### Visual composition

Use four horizontal safeguards with a simple icon and one-line description. Keep this slide clean and factual.

### Animation

Each safeguard fades in one at a time. Use coral only for the emergency item.

### Speaker script

“If someone needs immediate medical help, the system tells them to alert the nearest nurse, doctor, or emergency desk immediately. It does not wait for AI. Every complaint is logged internally, while a CPGRAMS referral is offered when the grievance concerns an eligible public authority and the citizen chooses to proceed. We will use a supported official integration only when the relevant authority provides one. We also minimise data collection and keep contact details optional.”

### Transition

Use a fast but restrained fade into the demo scenario.

---

## Slide 10 — Live demonstration and closing

**Time:** 50–70 seconds  
**Purpose:** Show a complete loop and leave one memorable message.

### On-slide text

**FROM A VOICE TO A VERIFIED ACTION.**

Report → Classify → Assign → Resolve → Verify → Improve

Closing line: **Every voice logged. Every complaint acted on. Every resolution verified.**

### Visual composition

Use a single horizontal lifecycle with one active ticket. Keep the patient voice on the left and the hospital service dashboard on the right. End with the Arogya Awaaz name and tagline.

### Demo sequence

1. Speak: “The washroom near Ward A is not clean.”
2. Show transcript confirmation.
3. Show category `SANITATION`, department `HOUSEKEEPING`, and ticket reference.
4. Show the staff dashboard receiving the ticket.
5. Mark work completed with a short action note.
6. Patient answers “No” once to demonstrate reopening, or “Yes” if the demo is designed to finish with closure. Do not attempt both if time is tight.
7. Briefly show an admin repeat-issue indicator with clearly labelled demo data.

If a real Bhashini or Gemini service is unavailable during the event, switch to a clearly labelled demo mode using pre-recorded test inputs. Do not pretend a mock response came from a live provider.

### Speaker script

“Let us follow one complaint from beginning to end. The patient speaks in their language. Arogya Awaaz confirms the transcript, creates a ticket, and routes it to Housekeeping. Staff records the action. The patient is asked whether the problem is actually resolved. If not, it reopens. Meanwhile, repeated reports from the same location remain visible to management. That is the difference between collecting complaints and building accountability.

Arogya Awaaz gives every patient a voice—and gives every hospital team a traceable responsibility. Thank you.”

## 5. Timing plan

| Slide | Topic | Target time |
|---|---|---:|
| 1 | Patient hook | 0:35 |
| 2 | Problem | 0:40 |
| 3 | Arogya Awaaz | 0:35 |
| 4 | Patient Voice Assistant | 0:45 |
| 5 | AI classification/routing | 0:55 |
| 6 | Management dashboard | 0:45 |
| 7 | Intelligent monitoring | 1:10 |
| 8 | Verified closure | 0:45 |
| 9 | Safety and CPGRAMS | 0:40 |
| 10 | Demo and close | 0:50–1:10 |
| **Total** |  | **7:00–7:20** |

If the event has a strict five-minute limit, shorten Slides 2, 6, and 9, keep one sentence per pillar, and perform only the patient-to-ticket-to-confirmation demo.

## 6. How to build the actual PowerPoint

1. Set page size to **Widescreen 16:9**.
2. Create a master theme using the navy/teal/saffron palette and the selected fonts.
3. Create reusable master elements: title position, footer, slide number, section marker, and background grid/texture.
4. Build the four feature slides using the same visual grammar: large number, pillar title, one key statement, one UI/diagram visual, and a small proof point.
5. Build diagrams using editable PowerPoint shapes or SVGs. Do not use screenshots for every diagram; editable elements make last-minute changes safer.
6. Use PowerPoint Morph between the solution and four feature slides so the same ticket moves through the system.
7. Use Fade/Wipe for sequential reveals. Keep most animations under 0.6 seconds; use the duty-window timeline and voice waveform as the only more complex motion elements.
8. Do not use more than two animation styles on one slide.
9. Keep all text large enough to read from the back of a room. Avoid paragraphs on slides; speaker notes carry the script.
10. Test the deck on the presentation laptop. Check Kannada, Devanagari, and Urdu glyph rendering; embed fonts only where licensing and PowerPoint support permit.
11. Export a PDF backup and a video or screen recording of the key demo path. Do not depend on internet access or live provider quotas for the only demo path.
12. Rehearse once with animation and once in a no-animation/PDF fallback mode.

## 7. What not to put in the deck

- Do not claim that CPGRAMS auto-submission is live unless an authorised integration has been implemented and tested.
- Do not claim that the AI verifies a doctor’s physical presence.
- Do not call a patient report a proven allegation.
- Do not show real patient names, phone numbers, prescriptions, or clinical details.
- Do not invent adoption figures, percentage improvements, hospital partnerships, or measured impact.
- Do not suggest that the app diagnoses emergencies or dispatches ambulances.
- Do not say every hospital has the same two-day deadline; it is a configurable Arogya Awaaz escalation rule.

## 8. Likely judge questions and concise answers

**Q: What is actually innovative here?**  
A: It combines multilingual voice access with verifiable ticket lifecycle management and service-level monitoring. The differentiator is the closed loop from a patient's spoken report to department action, patient confirmation, and recurring-issue analysis.

**Q: What happens if the AI misunderstands Kannada, Hindi, or Urdu?**  
A: The patient reviews and confirms the transcript. Low-confidence or ambiguous cases are clarified or sent to human triage. AI suggestions are checked against the hospital's department and doctor directory.

**Q: How do you stop staff from marking every complaint resolved?**  
A: Staff completion and patient confirmation are separate states. The patient can reopen. No response does not count as confirmation, and all changes remain in an audit history.

**Q: What if the patient has no phone?**  
A: A phone number is optional. The patient gets a private receipt token/QR and can use a hospital kiosk or voice assistant to check status and confirm the resolution.

**Q: How does the doctor-availability feature know a doctor is absent?**  
A: It does not infer physical absence from speech. It records patient reports, groups them into the configured duty windows, escalates repeated patterns, and asks an authorised officer to verify the roster or attendance.

**Q: Does it automatically file every complaint on CPGRAMS?**  
A: No. Every complaint is logged inside Arogya Awaaz. CPGRAMS is a separate citizen portal for eligible public-authority grievances. The citizen reviews and authorises the referral; automatic submission requires an approved official integration.

**Q: What happens during a medical emergency?**  
A: The emergency action immediately tells the user to alert nearby hospital staff and can notify a configured on-site responder. It does not wait for an AI response or provide medical diagnosis.

**Q: How will a hospital use the insights?**  
A: Management can identify repeat problems by department and location, see overdue and reopened tickets, monitor response times, and review recurring doctor-availability or medicine-shortage reports.

## 9. Closing one-liner options

Recommended:

> **“Arogya Awaaz: Every voice logged. Every complaint acted on. Every resolution verified.”**

Alternatives:

- “A better hospital begins when every patient is heard.”
- “From patient voice to hospital accountability.”
- “Not just a complaint system. A continuous feedback loop for better hospital services.”
