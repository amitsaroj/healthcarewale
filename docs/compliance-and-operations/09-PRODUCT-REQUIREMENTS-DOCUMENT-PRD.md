# 📱 HealthcareWale — Product Requirements Document (PRD)
> **Document ID:** HW-PRD-001 | **Version:** 1.0 | **Effective Date:** [Insert Date]  
> **Document Owner:** Founder / Product Lead — HealthcareWale Technologies Pvt. Ltd.  
> **Status:** Active — Pre-Development Review

---

## TABLE OF CONTENTS
1. [Product Vision & Goals](#1-product-vision--goals)
2. [AI Appointment Matching Engine](#2-ai-appointment-matching-engine)
3. [Voice Booking Pipeline (Hindi/Bengali)](#3-voice-booking-pipeline-hindibengali)
4. [WhatsApp Text Booking Pipeline](#4-whatsapp-text-booking-pipeline)
5. [Real-Time Doctor Availability Sync Engine](#5-real-time-doctor-availability-sync-engine)
6. [Automated Fallback Notification System](#6-automated-fallback-notification-system)
7. [AI Triage Pre-Screening Pipeline](#7-ai-triage-pre-screening-pipeline)
8. [Pharmacy Voice & OCR Pipeline](#8-pharmacy-voice--ocr-pipeline)
9. [PMJAY Claim Intelligence Engine](#9-pmjay-claim-intelligence-engine)
10. [Analytics & Reporting Engine](#10-analytics--reporting-engine)
11. [Acceptance Criteria Summary](#11-acceptance-criteria-summary)
12. [Non-Goals](#12-non-goals)

---

## 1. PRODUCT VISION & GOALS

### 1.1 Problem Statement

Healthcare in Tier-2/Tier-3 India operates in an operational vacuum:

| Stakeholder | Pain | Quantified Impact |
|---|---|---|
| Clinic (Doctor) | 30–40% of incoming calls go unanswered | ₹10,000–30,000/month in lost consultations |
| Patient | Average wait time 45–90 min even with "appointment" | 60% of patients reduce healthcare visits due to friction |
| Pharmacy | 15–25% of stock expires or becomes dead stock | ₹3,000–8,000/month loss per pharmacy |
| Hospital | PMJAY claim rejection rate 18–22% | ₹50,000–5,00,000/month in rejected revenue |
| Distributor | Manual order collection via 40–60 calls/day | 3–4 hours/day in unproductive order management |

### 1.2 Product Vision

> Build the operating system for semi-urban Indian healthcare — a single AI-powered platform that makes every clinic, pharmacy, and hospital operate as efficiently as the best urban private hospital, at 1/100th the cost.

### 1.3 Phase 1 Product Goals (Month 1–6)

| Goal | Metric | Target |
|---|---|---|
| Reduce missed patient calls | % calls answered by AI | >90% |
| Reduce appointment no-shows | No-show rate reduction | 30% reduction |
| Reduce pharmacy expiry losses | Monthly expiry loss per pharmacy | <₹1,000/month (from ₹5,000 avg) |
| Automate supplier ordering | % orders placed automatically | >70% |
| Billing accuracy | GST billing error rate | <0.5% |

---

## 2. AI APPOINTMENT MATCHING ENGINE

### 2.1 Overview

The Appointment Matching Engine (AME) is the core intelligence layer that maps patient booking requests to the correct doctor, specialty, date, and time slot. It operates across all booking channels: voice, WhatsApp, app, and web.

### 2.2 Matching Algorithm Logic

```
INPUT: Patient request
{
  stated_complaint: "bukhar aur khansi" (fever and cough),
  preferred_doctor: null,
  preferred_date: "kal" (tomorrow),
  preferred_time: "subah" (morning),
  location: "Lucknow, UP",
  language: "Hindi",
  insurance: "PMJAY",
  patient_history: [past_visits] // optional, if ABHA linked
}

STEP 1: Complaint → Specialty Mapping
"bukhar aur khansi" → General Physician
(Mapping table: 500+ common Hindi/Bengali complaint phrases → ICD specialty)

STEP 2: Filter Available Doctors
- Specialty = General Physician
- Location = Lucknow (within 10km radius)
- Date = Tomorrow
- Time = Morning (8 AM – 12 PM)
- Insurance = PMJAY accepted (if patient is PMJAY beneficiary)
- Language = Hindi-speaking

STEP 3: Rank Filtered Doctors
Score = (
  availability_score × 0.4 +     // Has open slots tomorrow morning
  rating_score × 0.25 +          // Patient rating average
  distance_score × 0.2 +         // Closer = higher score
  wait_time_score × 0.15         // Shorter current queue = higher score
)

STEP 4: Present Options
Top 3 doctors shown to patient with:
- Doctor name + specialization
- Next available slot time
- Consultation fee
- Distance from patient
- Estimated wait time at clinic

STEP 5: Patient Selects → Slot Reserved (hold for 5 minutes)
STEP 6: Patient Confirms → Appointment Created in DB
STEP 7: Confirmation sent via WhatsApp + SMS
```

### 2.3 Complaint-to-Specialty Mapping (Hindi/Bengali)

| Patient Says (Hindi) | Patient Says (Bengali) | Routed To |
|---|---|---|
| "bukhar", "tez bukhaar", "bimari" | "jor", "bimari" | General Physician |
| "dil mein dard", "seene mein dard" | "buke byatha" | Cardiologist |
| "sugar", "madhumeh", "diabetes" | "diabetes", "blood sugar" | Endocrinologist / Gen Physician |
| "BP hai", "blood pressure" | "pressure ache" | General Physician / Cardiologist |
| "bachche ko tez bukhaar" | "bachar jor" | Pediatrician |
| "pet mein dard", "ulti dast" | "pete byatha" | Gastroenterologist / Gen Physician |
| "haddi mein dard", "ghutne mein" | "harde byatha" | Orthopedician |
| "aankhon mein takleef" | "chokhe somosya" | Ophthalmologist |
| "dant mein dard" | "danter byatha" | Dentist |
| "mahila rog", "periods" | "masik" | Gynecologist / Obstetrician |
| "skin par daane", "kharish" | "gaye problem" | Dermatologist |
| "mansik takleef", "tension" | "moner somosya" | Psychiatrist / Counsellor |

**Mapping coverage target:** 500+ phrases in Hindi, 400+ in Bengali at Phase 1 launch

### 2.4 Edge Cases & Fallbacks

| Edge Case | Handling |
|---|---|
| Patient complaint unrecognized | Ask: "Kaunse doctor se milna chahte hain?" — let patient specify specialty |
| No doctor available in specialty | Offer: Nearest available General Physician + note specialty unavailability |
| All slots full for requested date | Offer next 3 available dates with earliest slot |
| Patient requests specific doctor who is unavailable | Inform unavailability + offer their next available slot + similar doctor alternative |
| Emergency keyword detected | Redirect to 108 immediately — do not continue booking |
| Patient changes preference mid-flow | Restart matching from patient's new preference |

### 2.5 Slot Reservation & Conflict Prevention

```sql
-- Optimistic locking for slot reservation (prevents double-booking)
BEGIN TRANSACTION;

-- Check slot availability with row lock
SELECT id, status FROM appointment_slots 
WHERE doctor_id = $1 AND slot_datetime = $2 AND status = 'available'
FOR UPDATE SKIP LOCKED;  -- Skip if another transaction holds the lock

-- If found, reserve it
UPDATE appointment_slots 
SET status = 'reserved', reserved_by = $3, reserved_until = NOW() + INTERVAL '5 minutes'
WHERE id = $4;

COMMIT;

-- Cleanup job: Release expired reservations (runs every 60 seconds)
UPDATE appointment_slots 
SET status = 'available', reserved_by = NULL, reserved_until = NULL
WHERE status = 'reserved' AND reserved_until < NOW();
```

---

## 3. VOICE BOOKING PIPELINE (HINDI/BENGALI)

### 3.1 Architecture Overview

```
Patient dials clinic virtual number (Exotel)
              │
              ▼
    Exotel WebSocket stream → Voice AI Service (Node.js)
              │
              ▼
    Sarvam AI: Real-time STT (Speech-to-Text)
    Audio stream → Hindi/Bengali text transcript
              │
              ▼
    LLM Intent Engine (Claude API)
    System prompt: admin-only booking assistant
    Input: transcript + conversation history
    Output: intent + entities + next action
              │
    ┌─────────┴─────────────────────────────┐
    ▼                                       ▼
Booking intent confirmed           Unrecognized intent (2nd attempt)
    │                                       │
    ▼                                       ▼
Appointment Matching Engine        Human escalation or callback offer
    │
    ▼
Database write: appointment created
    │
    ▼
Sarvam AI: TTS (Text-to-Speech)
Response text → Hindi/Bengali audio
    │
    ▼
Audio streamed back to patient via Exotel
    │
    ▼
Post-call: WhatsApp confirmation sent
Call transcript stored (30 days)
```

### 3.2 Voice Pipeline Technical Specifications

| Component | Specification | Target Performance |
|---|---|---|
| STT latency (Sarvam AI) | Real-time streaming | <500ms per utterance |
| LLM response time (Claude API) | Streaming | <1 second |
| TTS generation (Sarvam AI) | Streaming audio | <800ms |
| End-to-end turn latency | STT + LLM + TTS | <2.5 seconds |
| Concurrent call capacity (Phase 1) | Exotel plan | 50 concurrent calls |
| Call recording storage | AWS S3 | 30-day retention, auto-expire |
| Language detection | Automatic | Hindi/Bengali auto-detected from first utterance |
| Fallback to human | After 2 failed intent detections | Transfer to clinic number or offer callback |

### 3.3 Voice Conversation Flow — Appointment Booking

```
TURN 1 — AI: "Namaste! Main HealthcareWale ka AI assistant hun. 
         Aap doctor se appointment lena chahte hain?"

TURN 2 — Patient: "Haan, mujhe bukhaar hai"

TURN 3 — AI: "Aapko General Physician se milna chahiye. 
         [Clinic Name] mein kal subah 10 baje aur 11 baje slot available hai.
         Kaunsa time better hai aapke liye?"

TURN 4 — Patient: "10 baje theek hai"

TURN 5 — AI: "Theek hai. Aapka naam kya hai?"

TURN 6 — Patient: "Ramesh Kumar"

TURN 7 — AI: "Dhanyawaad Ramesh ji. 
         [Date] ko subah 10 baje Dr. [Name] ke saath appointment confirm ho gayi hai.
         Token number hai: HW-2456.
         Aapke WhatsApp par confirmation aa jayegi."

[Call ends]
[WhatsApp confirmation sent automatically]
[Appointment written to database]
[Reminder jobs scheduled: 48h + 2h]
```

### 3.4 Outbound Call Pipeline (Reminders & Follow-ups)

```
BullMQ job triggered: "send_voice_reminder"
{
  patient_phone: "+91XXXXXXXXXX",
  appointment_id: "APT-XXXXX",
  doctor_name: "Dr. Sharma",
  time: "10:00 AM",
  date: "Tomorrow (4 June)",
  clinic_address: "...",
  language: "Hindi"
}
          │
          ▼
Exotel API: Initiate outbound call to patient
          │
          ▼
Call connects → Sarvam TTS plays reminder:
"Namaste [Name] ji! Kal subah 10 baje Dr. Sharma ke saath
aapki appointment hai. Kya aap aa sakte hain?
'1 dabayein' confirm karne ke liye, '2 dabayein' cancel karne ke liye."
          │
     ┌────┴────────────────────┐
     ▼                         ▼
Patient presses 1           Patient presses 2
(Confirm)                   (Cancel / No response)
     │                         │
     ▼                         ▼
Appointment marked          Appointment marked "likely_no_show"
"confirmed"                 Clinic dashboard alert
WhatsApp sent:              AI attempts rescheduling offer via WhatsApp
"Appointment confirmed ✅"
```

---

## 4. WHATSAPP TEXT BOOKING PIPELINE

### 4.1 Architecture Overview

```
Patient sends WhatsApp message to clinic's WhatsApp Business number
              │
              ▼
Meta WhatsApp Cloud API → Webhook → n8n (Workflow Engine)
              │
              ▼
n8n triggers: Intent Classification Node
LLM call with conversation history + system prompt
              │
              ▼
Intent identified → Route to appropriate workflow:
  • booking_new → Appointment Booking Workflow
  • booking_cancel → Cancellation Workflow
  • booking_reschedule → Reschedule Workflow
  • queue_status → Queue Status Workflow
  • faq → FAQ Response Workflow
  • medicine_order → Medicine Delivery Workflow
  • unknown → Fallback Workflow
```

### 4.2 WhatsApp Conversation State Machine

```
STATE: IDLE
Patient sends first message → STATE: ACTIVE_SESSION (24-hour window)

STATE: ACTIVE_SESSION
├── New booking intent → STATE: BOOKING_FLOW
│   ├── Specialty selection → STATE: BOOKING_SPECIALTY
│   ├── Date selection → STATE: BOOKING_DATE
│   ├── Slot selection → STATE: BOOKING_SLOT
│   ├── Name confirmation → STATE: BOOKING_CONFIRM
│   └── Confirmed → STATE: BOOKING_COMPLETE → STATE: IDLE
│
├── Cancel intent → STATE: CANCEL_FLOW
│   ├── Show existing appointments
│   ├── Patient confirms cancellation
│   └── Cancelled → STATE: IDLE
│
├── Queue status intent → Fetch queue position → Reply → STATE: IDLE
│
└── Unknown intent (2 times) → "Main samajh nahi paya. 
    Kya aap clinic ko seedha call karna chahenge? [number]"
    → STATE: IDLE
```

### 4.3 Interactive Button Templates (WhatsApp)

```json
// Appointment confirmation message with interactive buttons
{
  "type": "interactive",
  "interactive": {
    "type": "button",
    "body": {
      "text": "Dr. Sharma ke saath 4 June, 10:00 AM ko appointment confirm karein?\n\n📍 [Clinic Name], MG Road, Lucknow\n💰 Consultation Fee: ₹500"
    },
    "action": {
      "buttons": [
        { "type": "reply", "reply": { "id": "confirm_apt", "title": "✅ Confirm" }},
        { "type": "reply", "reply": { "id": "change_time", "title": "🕐 Change Time" }},
        { "type": "reply", "reply": { "id": "cancel_apt", "title": "❌ Cancel" }}
      ]
    }
  }
}
```

### 4.4 WhatsApp Template Messages (Meta-Approved)

| Template Name | Trigger | Content |
|---|---|---|
| `appointment_confirmation` | New booking created | "Appointment confirmed ✅ Token: {token}. Dr. {doctor} on {date} at {time}. {clinic_address}" |
| `appointment_reminder_24h` | 24 hours before | "Reminder: Your appointment with Dr. {doctor} is TOMORROW at {time}. [Confirm] [Reschedule] [Cancel]" |
| `appointment_reminder_2h` | 2 hours before | "Your appointment is in 2 hours! Dr. {doctor} at {time}. Queue position: {position}" |
| `queue_update` | Every 5 min (when patient in queue) | "Queue update: {number} patients before you. Estimated wait: {minutes} min." |
| `prescription_ready` | Post-consultation | "Your prescription from Dr. {doctor} is ready. [Download PDF]" |
| `medicine_order_confirmed` | Pharmacy order placed | "Medicine order confirmed! Delivery in {time}. Track: {link}" |
| `followup_due` | Follow-up date approaching | "Your follow-up with Dr. {doctor} is due. Book now: {booking_link}" |
| `expiry_alert` | For pharmacies | "⚠️ {medicine_name} — {quantity} strips expire on {date}. Action needed." |

---

## 5. REAL-TIME DOCTOR AVAILABILITY SYNC ENGINE

### 5.1 Overview

The availability sync engine ensures that slot availability shown to patients is always accurate — preventing double bookings and frustrating "slot taken" experiences after patients select a time.

### 5.2 Slot Generation Logic

```javascript
// Generate slots for a doctor for a given date
async function generateSlots(doctorId, date) {
  const schedule = await getDoctorSchedule(doctorId, getDayOfWeek(date));
  
  if (!schedule || schedule.is_holiday) return [];
  
  const slots = [];
  let current = schedule.start_time; // e.g., "09:00"
  
  while (current < schedule.end_time) { // e.g., "13:00"
    // Skip break times
    if (!isBreakTime(current, schedule.breaks)) {
      slots.push({
        doctor_id: doctorId,
        date: date,
        start_time: current,
        duration_minutes: schedule.avg_consultation_minutes, // e.g., 15
        status: 'available',
        slot_type: 'regular'
      });
    }
    current = addMinutes(current, schedule.avg_consultation_minutes);
  }
  
  // Add emergency slots (last 2 slots of day reserved for walk-in emergencies)
  slots[slots.length - 1].slot_type = 'emergency';
  slots[slots.length - 2].slot_type = 'emergency';
  
  return slots;
}
```

### 5.3 Real-Time Availability Events

| Event | Trigger | Sync Action |
|---|---|---|
| Appointment booked | Patient confirms booking | Slot marked `booked` → all booking channels updated |
| Appointment cancelled | Patient or doctor cancels | Slot marked `available` → slot re-opened in booking system |
| Doctor goes on leave | Doctor updates leave in dashboard | All future slots for leave period cancelled → patients notified |
| Walk-in registered | Reception adds walk-in | Emergency slot consumed → queue updated |
| Doctor running late | Reception marks delay | Wait time estimates updated → patients in queue notified |
| Consultation complete | Doctor marks complete | Next patient called → queue advanced |

### 5.4 Availability Cache Strategy

```
PostgreSQL (source of truth)
    │
    ▼
Redis cache: doctor_availability:{doctor_id}:{date}
TTL: 60 seconds (auto-refresh)
    │
    ▼
Booking channels read from cache (fast, <10ms)
    │
Cache invalidated immediately on:
- New booking confirmed
- Cancellation processed
- Doctor schedule change
```

---

## 6. AUTOMATED FALLBACK NOTIFICATION SYSTEM

### 6.1 Channel Priority Stack

When sending any notification, HealthcareWale uses a priority-ordered channel stack:

```
PRIMARY: WhatsApp (delivery rate: ~95% for active WhatsApp users)
    │
    │ If WhatsApp fails (user not on WhatsApp / delivery failed after 5 min):
    ▼
SECONDARY: SMS (delivery rate: ~98% for any mobile number)
    │
    │ If SMS fails (DND, network issue):
    ▼  
TERTIARY: AI Voice Call (100% attempt rate; delivery = call answered)
    │
    │ If all digital channels fail for appointment reminder:
    ▼
FALLBACK LOG: Clinic reception dashboard alert — "Patient [Name] unreachable — please call manually"
```

### 6.2 Fallback Decision Engine (n8n Workflow)

```
n8n workflow: "send_appointment_reminder"
    │
    ▼
Step 1: Send WhatsApp message (Interakt API)
    │
    ▼ Wait 5 minutes
    │
Step 2: Check WhatsApp delivery status
    │
    ├── Delivered ✅ → End workflow
    │
    └── Failed / Unread ❌
            │
            ▼
        Step 3: Send SMS (Twilio API)
            │
            ▼ Wait 30 minutes
            │
        Step 4: Check SMS delivery status
            │
            ├── Delivered ✅ → End workflow
            │
            └── Failed ❌
                    │
                    ▼
                Step 5: Initiate AI voice call (Exotel API)
                    │
                    ├── Call answered → reminder delivered
                    │
                    └── Not answered → log as "unreachable"
                                     → Clinic dashboard alert
                                     → Optional: schedule retry in 2 hours
```

### 6.3 Notification Event Matrix

| Event | WhatsApp | SMS | Voice Call | Dashboard Alert |
|---|---|---|---|---|
| Appointment confirmed | ✅ Primary | ✅ Fallback | ❌ | ❌ |
| Reminder 48h before | ✅ Primary | ✅ Fallback | ❌ | ❌ |
| Reminder 2h before | ✅ Primary | ✅ Fallback | ✅ Fallback | ❌ |
| No-show detected | ✅ (reschedule offer) | ✅ Fallback | ✅ Fallback | ✅ |
| Prescription ready | ✅ Primary | ✅ Fallback | ❌ | ❌ |
| Medicine delivery update | ✅ Primary | ✅ Fallback | ❌ | ❌ |
| PMJAY claim approved | ✅ Primary | ✅ Fallback | ❌ | ✅ |
| Low stock alert (pharmacy) | ✅ Primary | ❌ | ❌ | ✅ |
| Expiry alert (pharmacy) | ✅ Primary | ❌ | ❌ | ✅ |
| Payment reminder (credit) | ✅ Primary | ✅ Fallback | ✅ Escalation | ✅ |

### 6.4 Anti-Spam & Rate Limiting

- Maximum 3 notifications per patient per day (across all events)
- No notifications between 10 PM – 8 AM
- Patients can opt out of any notification type independently
- TRAI DND compliance: All SMS sent via DLT-registered templates only
- WhatsApp opt-out: Patient sends "STOP" → immediately removed from all broadcasts

---

## 7. AI TRIAGE PRE-SCREENING PIPELINE

### 7.1 Purpose & Strict Scope

The pre-screening pipeline collects the patient's chief complaint before consultation to:
- Help the doctor prepare (not diagnose)
- Route to correct specialty (if not pre-selected)
- Reduce consultation time by having basic history ready

**This pipeline does NOT:**
- Score clinical severity
- Suggest possible diagnoses
- Recommend any treatment or medication
- Override doctor's clinical judgment

### 7.2 Pre-Screening Flow

```
Patient books appointment → Receives WhatsApp message:

"Dr. [Name] ke saath aapki appointment kal hai.
Doctor ko better prepare karne ke liye, aap apni problem
thodi batayein (optional):"

Patient responds:
"Mujhe 3 din se bukhaar hai aur sar mein dard hai.
Khansi bhi hai thodi"

System:
1. Extract chief complaint: fever (3 days), headache, mild cough
2. NO clinical analysis — store as free text
3. Attach to patient's appointment record
4. Doctor sees this on dashboard when patient's turn comes

Doctor dashboard shows:
"Patient's stated complaint: 3-din se bukhaar, sar mein dard, thodi khansi
[Patient's exact words — no AI interpretation]"
```

### 7.3 Emergency Keyword Detection

```javascript
const EMERGENCY_KEYWORDS_HINDI = [
  'emergency', 'bahut tez dard', 'chest pain', 'seene mein dard',
  'saans nahi aa rahi', 'behosh', 'accident', 'sar par chot',
  'bahut zyada khoon', 'stroke', 'laqwa', 'dil ka daura'
];

const EMERGENCY_KEYWORDS_BENGALI = [
  'emergency', 'khub byatha', 'buke byatha', 'sas aste parchhina',
  'behos', 'accident', 'matha te chot', 'onek rokto', 'stroke'
];

function detectEmergency(message, language) {
  const keywords = language === 'bengali' 
    ? EMERGENCY_KEYWORDS_BENGALI 
    : EMERGENCY_KEYWORDS_HINDI;
  
  return keywords.some(kw => message.toLowerCase().includes(kw));
}

// If emergency detected anywhere in the booking flow:
if (detectEmergency(patientMessage, patientLanguage)) {
  sendImmediateResponse(
    "Yeh emergency lag rahi hai. Kripya turant 108 call karein " +
    "ya nearest emergency room jayein. " +
    "HealthcareWale emergency services provide nahi karta."
  );
  logEmergencyEvent(patientId, patientMessage, timestamp);
  terminateBookingFlow();
}
```

---

## 8. PHARMACY VOICE & OCR PIPELINE

### 8.1 Voice Stock Update Pipeline

```
Pharmacist speaks into phone mic or WhatsApp voice note:
"Paracetamol 500mg — 20 strip aaye Sharma Medical se, 
 rate 8 rupaye 50 paise strip"
              │
              ▼
Sarvam AI STT → Hindi text transcript
              │
              ▼
Medical NLP Extraction:
{
  "action": "stock_in",
  "medicine_name": "Paracetamol 500mg",
  "quantity": 20,
  "unit": "strip",
  "supplier": "Sharma Medical",
  "purchase_price": 8.50,
  "per_unit": "strip"
}
              │
              ▼
Fuzzy match medicine name against inventory database
(handles: "Paracitamol", "Perasetamol", "Crocin" → Paracetamol 500mg)
              │
              ▼
Stock added to inventory:
medicine_id: [UUID for Paracetamol 500mg]
quantity_added: 20
purchase_price: 8.50/strip
              │
              ▼
Confirmation sent back to pharmacist:
"✅ Paracetamol 500mg — 20 strip add ho gayi. 
 Current stock: 85 strips."
```

### 8.2 Prescription OCR Pipeline

```
Pharmacist photographs prescription via app camera
              │
              ▼
Image uploaded to S3 (temp bucket, auto-delete 24h)
              │
              ▼
Google Cloud Vision API: Extract all text from image
              │
              ▼
Medical NLP Post-Processing:
1. Identify medicine section (after "Rx" or "℞")
2. Parse each line: medicine_name | dose | frequency | duration
3. Fuzzy match each medicine name to inventory database
4. Flag Schedule H drugs
5. Calculate confidence score per medicine
              │
              ▼
Output:
[
  { "name": "Amoxicillin 500mg", "dose": "1 cap", "freq": "TDS", 
    "duration": "5 days", "qty": 15, "confidence": 0.94, 
    "schedule": "H", "in_stock": true },
  { "name": "Paracetamol 500mg", "dose": "1 tab", "freq": "SOS",
    "duration": "3 days", "qty": 9, "confidence": 0.89,
    "schedule": "OTC", "in_stock": true },
  { "name": "[unrecognized]", "raw": "Bco Zn Tab",
    "confidence": 0.45, "flagged_for_review": true }
]
              │
              ▼
Pharmacist review screen:
- High confidence (>85%): Auto-populated, shown in green
- Medium confidence (60–85%): Shown in yellow, tap to confirm
- Low confidence (<60%): Shown in red, requires manual entry
- Schedule H items: Shown with 🔴 flag — prescription image stored
              │
              ▼
Pharmacist approves → Bill generated → Inventory deducted
Prescription image + bill linked in database
```

### 8.3 OCR Accuracy Targets

| Prescription Type | Phase 1 Target | Phase 2 Target |
|---|---|---|
| Printed/typed prescriptions | 90%+ | 95%+ |
| Clear handwritten (doctor block letters) | 75%+ | 85%+ |
| Difficult handwritten | 60%+ | 75%+ |
| Overall (blended) | 78%+ | 87%+ |

---

## 9. PMJAY CLAIM INTELLIGENCE ENGINE

### 9.1 ICD-10 Code Suggestion

```
Doctor enters diagnosis text:
"Type 2 Diabetes Mellitus with Hypertension, managed"
              │
              ▼
NLP Model: Symptom/Condition Entity Extraction
Entities: ["Type 2 Diabetes Mellitus", "Hypertension"]
              │
              ▼
ICD-10 Mapping (vector similarity search):
"Type 2 Diabetes Mellitus" → E11.9 (confidence: 0.97)
"Hypertension" → I10 (confidence: 0.96)
              │
              ▼
Display to billing staff:
"Suggested ICD-10 Codes:
 E11.9 — Type 2 diabetes mellitus without complications [97% confidence]
 I10 — Essential (primary) hypertension [96% confidence]
 ✏️ Modify | ✅ Approve"
              │
              ▼
Staff approves → Codes added to claim
Staff modifies → Modified codes added → modification logged
Claim submitted with ICD-10 codes to NHA API
```

### 9.2 Pre-Submission Claim Validation

Before submitting any PMJAY claim, system runs validation:

```javascript
async function validateClaimBeforeSubmission(claim) {
  const errors = [];
  const warnings = [];
  
  // Check 1: Patient PMJAY eligibility not expired
  const eligibility = await checkPMJAYEligibility(claim.patient_pmjay_id);
  if (!eligibility.active) errors.push("PMJAY card inactive or expired");
  
  // Check 2: HBP code exists and matches specialty
  const hbp = await validateHBPCode(claim.hbp_code, claim.specialty);
  if (!hbp.valid) errors.push(`HBP code ${claim.hbp_code} invalid for ${claim.specialty}`);
  
  // Check 3: Claim amount within HBP package limit
  if (claim.amount > hbp.max_amount) 
    errors.push(`Claim amount ₹${claim.amount} exceeds HBP limit ₹${hbp.max_amount}`);
  
  // Check 4: Required documents attached
  const required_docs = ['discharge_summary', 'admission_record', 'investigation_reports'];
  required_docs.forEach(doc => {
    if (!claim.documents[doc]) errors.push(`Missing required document: ${doc}`);
  });
  
  // Check 5: ICD-10 codes consistent with HBP package
  const icd_hbp_match = validateICD10againstHBP(claim.icd10_codes, claim.hbp_code);
  if (!icd_hbp_match) warnings.push("ICD-10 codes may not match HBP package — please verify");
  
  // Check 6: Duplicate claim detection
  const duplicate = await checkDuplicateClaim(claim.patient_abha, claim.admission_date);
  if (duplicate) errors.push("Potential duplicate claim detected for same patient/date");
  
  return { valid: errors.length === 0, errors, warnings };
}
```

**Target:** Reduce PMJAY claim rejection rate from industry average 18–22% to <8%

---

## 10. ANALYTICS & REPORTING ENGINE

### 10.1 Super Admin Dashboard (Amit's View)

Real-time metrics visible to Super Admin:

| Metric | Refresh Rate | Data Source |
|---|---|---|
| Total active customers (by type) | Real-time | PostgreSQL |
| MRR / ARR | Daily | Razorpay + PostgreSQL |
| New signups today / this week | Real-time | PostgreSQL |
| Churn events (cancellations) | Real-time | PostgreSQL |
| AI voice call volume | Hourly | Exotel API |
| WhatsApp message volume | Hourly | Interakt API |
| Platform uptime | Real-time | AWS CloudWatch |
| Top 10 customers by revenue | Daily | PostgreSQL |
| Support ticket volume | Hourly | Support CRM |
| AI accuracy metrics | Daily | AI logs |

### 10.2 Clinic Owner Dashboard

Auto-generated daily report sent to clinic owner at 8 PM via WhatsApp:

```
📊 Aaj Ka Report — [Clinic Name]
Date: [Date]

👥 OPD Today: 47 patients
✅ Completed: 42
❌ No-shows: 5 (10.6%)
⏰ Avg wait time: 23 min

💰 Revenue Today: ₹23,500
📈 vs Yesterday: +12%

📱 Appointments via HealthcareWale: 31
📞 AI calls handled: 18
💬 WhatsApp bookings: 13

🔔 Tomorrow's appointments: 52 booked
```

### 10.3 Pharmacy Owner Dashboard

Weekly report every Monday morning:

```
📊 Weekly Report — [Pharmacy Name]
Week: [Date Range]

💊 Bills generated: 423
💰 Total revenue: ₹1,87,450
📈 vs Last week: +8.3%

⚠️ Expiry alerts: 6 medicines
🔴 Critical (< 7 days): 2
🟡 Warning (< 30 days): 4

📦 Auto-orders placed: 3
✅ Delivered: 2 | ⏳ Pending: 1

🔻 Low stock: 5 medicines
Top selling: Paracetamol 500mg (280 strips)
```

---

## 11. ACCEPTANCE CRITERIA SUMMARY

| Feature | Acceptance Criterion |
|---|---|
| AI Voice Booking (Hindi) | 90%+ of standard booking intents correctly handled without human intervention |
| AI Voice Booking (Bengali) | 85%+ intent recognition (lower due to dialect diversity) |
| WhatsApp Booking Bot | Complete booking flow in <10 message turns; confirmation in <30 seconds |
| Appointment Matching | Zero double-bookings in production; <3 second response time |
| No-Show Reduction | 25%+ reduction vs baseline in first 90 days |
| Prescription OCR | 78%+ overall accuracy on blended prescription types |
| Pharmacy Voice Update | 90%+ medicine name recognition on standard generic names |
| PMJAY Claim Validation | Pre-validation catches >80% of rejection-causing errors before submission |
| Fallback Notification | 99%+ appointment reminder delivery (across all channels) |
| Platform Uptime | 99.9% monthly uptime |
| Data Security | Zero PHI data exposure incidents |
| Emergency Detection | 100% of emergency keywords trigger 108 redirect — no exceptions |

---

## 12. NON-GOALS

The following are explicitly out of scope for this product:

| Non-Goal | Reason |
|---|---|
| Medical diagnosis via AI | SaMD classification risk; clinical liability |
| Drug interaction checking | Medical device territory; requires clinical validation |
| Automated prescription generation without doctor | Illegal under Telemedicine Guidelines 2020 |
| Emergency medical response | Outside platform scope; 108 exists for this |
| Replacing PMJAY adjudicators | Claims still reviewed by NHA; we file, not adjudicate |
| Building our own LLM/AI model | Use best-in-class APIs; model building not core competency |
| E-pharmacy license (direct selling) | Legal risk; intermediary model preferred |
| Biometric patient identification | Not required for Phase 1; future consideration |

---

*HealthcareWale Product Requirements Document v1.0 — May 2026*  
*Review cycle: Monthly during active development*
