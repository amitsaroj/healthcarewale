# 📋 HealthcareWale — Functional Requirements Document (FRD)
> Version: 1.0 | Date: May 2026 | Status: Draft
> Target Market: West Bengal & Uttar Pradesh, India (Tier-2/Tier-3)

---

## 1. DOCUMENT OVERVIEW

### 1.1 Purpose
This document defines complete functional requirements for the HealthcareWale platform — an AI-powered healthcare operations SaaS for clinics, pharmacies, hospitals, and distributors in semi-urban India.

### 1.2 Scope
This FRD covers:
- Patient-facing features (appointment, queue, records, delivery)
- Clinic/Doctor features (OPD, EMR, billing, scheduling)
- Pharmacy features (inventory, billing, supplier ordering)
- Hospital features (IPD, OT, discharge, PMJAY)
- Distributor features (supply chain, forecasting)
- AI and automation features (voice, WhatsApp, n8n workflows)
- Government integration (ABHA, PMJAY, Swasthya Sathi)

### 1.3 Stakeholders
| Role | Name/Type |
|---|---|
| Product Owner | Amit Saroj (Founder) |
| End Users | Clinic staff, pharmacists, doctors, patients, distributors |
| Regulatory Bodies | NMC, CDSCO, NHA, DPDP Authority, WB Health Dept, UP SACHIS |

### 1.4 Definitions
| Term | Meaning |
|---|---|
| PHR | Personal Health Record |
| EMR | Electronic Medical Record |
| OPD | Outpatient Department |
| IPD | Inpatient Department |
| PMJAY | Pradhan Mantri Jan Arogya Yojana |
| ABHA | Ayushman Bharat Health Account |
| ABDM | Ayushman Bharat Digital Mission |
| NHA | National Health Authority |
| FHIR | Fast Healthcare Interoperability Resources |
| ICD-10 | International Classification of Diseases (10th revision) |
| BSP | Business Solution Provider (WhatsApp) |
| TTS | Text-to-Speech |
| STT | Speech-to-Text |

---

## 2. SYSTEM OVERVIEW

### 2.1 Platform Description
HealthcareWale is a multi-tenant SaaS platform with:
- Web dashboard (for clinic/pharmacy owners and staff)
- Mobile app (Android + iOS via React Native)
- Patient PWA (no install needed — WhatsApp/browser-based)
- AI Voice Agent (phone calls — Hindi/Bengali)
- WhatsApp Bot (for patients and staff)
- n8n Automation Engine (backend workflow orchestration)

### 2.2 User Roles
| Role | Description | Access Level |
|---|---|---|
| Super Admin | HealthcareWale team | Full platform access |
| Clinic Owner | Owns clinic account | All clinic features |
| Doctor | Registered medical practitioner | EMR, schedule, teleconsult |
| Receptionist / Staff | Clinic front desk | Appointments, queue, billing |
| Pharmacist | Licensed pharmacy staff | Inventory, billing, orders |
| Pharmacy Owner | Owns pharmacy account | All pharmacy features |
| Hospital Admin | Nursing home / hospital management | Full HMS access |
| Distributor | Medicine wholesaler/distributor | Supply chain dashboard |
| Patient | End consumer | Booking, records, delivery |
| Caregiver | Family member managing a patient | Limited patient access |

### 2.3 High-Level System Architecture
```
┌─────────────────────────────────────────────────────────────────┐
│                        CLIENT LAYER                             │
│  Patient PWA  │  Mobile App  │  Web Dashboard  │  WhatsApp Bot  │
└──────────────────────┬──────────────────────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────────────────────┐
│                      API GATEWAY (Node.js)                      │
│         Auth │ Rate Limiting │ Load Balancing │ Logging         │
└──────────────────────┬──────────────────────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────────────────────┐
│                    MICROSERVICES LAYER                          │
│  Auth │ Appointment │ Inventory │ Billing │ EMR │ Notification  │
│  Voice AI │ WhatsApp │ Analytics │ Claims │ Supply Chain        │
└──────────────────────┬──────────────────────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────────────────────┐
│                      DATA LAYER                                 │
│  PostgreSQL (primary) │ Redis (cache/queue) │ MongoDB (docs)    │
│  AWS S3 (files/images) │ Elasticsearch (search)                 │
└──────────────────────┬──────────────────────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────────────────────┐
│                   EXTERNAL INTEGRATIONS                         │
│  Exotel │ Sarvam AI │ WhatsApp API │ Razorpay │ ABDM │ NHA      │
│  Google Vision │ Bhashini │ Firebase │ Twilio SMS               │
└─────────────────────────────────────────────────────────────────┘
```

---

## 3. FUNCTIONAL REQUIREMENTS — PATIENT MODULE

### FR-PAT-001: Patient Registration
- Patient can register via mobile number (OTP verification)
- System must support ABHA ID linking during registration
- Patient can create family profiles under one account (max 6 members)
- Required fields: Name, Mobile, Age, Gender, City, Preferred Language (Hindi/Bengali)
- Optional: ABHA ID, Email, Emergency Contact

### FR-PAT-002: Appointment Booking
- Patient can book via: App, WhatsApp bot, AI Voice call, Web browser
- System must show real-time available slots per doctor
- Booking confirmation must be sent via WhatsApp + SMS within 30 seconds
- Patient must receive appointment token/ID after booking
- System must support appointment types: OPD, Follow-up, Emergency, Teleconsultation
- Cancellation must be allowed up to 2 hours before appointment time
- Rescheduling must be allowed up to 4 hours before appointment time

### FR-PAT-003: WhatsApp Appointment Bot
- Bot must respond in patient's preferred language (Hindi or Bengali)
- Conversation flow: Greeting → Doctor Selection → Date → Slot → Confirm → Token
- Bot must handle: New booking, View existing booking, Cancel, Reschedule, FAQ
- Response time: <3 seconds for standard queries
- Fallback: If bot cannot handle query, escalate to human or call back

### FR-PAT-004: AI Voice Booking
- Patient dials clinic number → AI voice agent answers (not IVR tone)
- AI must identify intent: book, enquiry, cancellation, emergency
- AI must speak naturally in Hindi or Bengali based on caller's language
- System must confirm booking via SMS/WhatsApp after call
- Call recording must be stored (30-day retention) for quality review
- AI must handle: doctor availability queries, timing queries, fee queries

### FR-PAT-005: Virtual Waiting Room
- Patient receives token number after booking or walk-in registration
- Live queue status viewable on WhatsApp or PWA without app install
- System must update position every 5 minutes automatically
- Estimated wait time must be calculated based on: avg consultation duration + queue position
- Patient receives WhatsApp alert when: 3 patients ahead, 1 patient ahead, their turn
- Remote waiting: patient can leave clinic and return when alerted

### FR-PAT-006: Appointment Reminders
- Automated reminder: 48 hours before (WhatsApp + SMS)
- Automated reminder: 2 hours before (WhatsApp + AI Voice Call)
- Reminder must include: doctor name, time, clinic address, token, Google Maps link
- Patient can confirm, cancel, or reschedule directly from reminder message
- If no response to reminders, system marks as "likely no-show" and alerts clinic

### FR-PAT-007: Patient Health Records (PHR)
- Store: Prescriptions (photo/PDF), Lab reports, Visit history, Medicine history
- Doctor can view patient records during consultation
- Patient can share records via WhatsApp or download PDF
- Records must be encrypted at rest (AES-256)
- Records retained for minimum 7 years (as per Indian medical records guidelines)
- ABHA-linked records must sync with national ABDM health locker

### FR-PAT-008: Medicine Home Delivery
- Patient uploads prescription via app or WhatsApp photo
- System matches prescription to nearest empanelled pharmacy
- Pharmacy confirms availability and price within 15 minutes
- Patient confirms order and makes payment (UPI/cash-on-delivery)
- Delivery time: 2–6 hours depending on location
- Schedule H drugs: system must verify prescription before dispatch
- Tracking: Real-time delivery status on WhatsApp
- Only licensed, empanelled pharmacies can fulfill orders

### FR-PAT-009: Lab Test Booking
- Patient selects test from catalogue
- System shows available diagnostic partners in patient's city
- Home sample collection must be bookable for applicable tests
- Phlebotomist assigned automatically based on location + availability
- Results: Auto-sent to patient WhatsApp + app + doctor (if linked)
- Report format: PDF with lab letterhead

### FR-PAT-010: Chronic Disease Management
- Patient can enroll in chronic care program: Diabetes, Hypertension, Thyroid, Asthma
- System sends: Medicine reminders (daily/as prescribed), Follow-up reminders (monthly), Diagnostic reminders (quarterly)
- Patient can log readings: Blood pressure, Blood sugar, Weight via WhatsApp or app
- AI alerts doctor if reading is abnormal (e.g., BP > 160/100)
- Family members can be notified for elderly patients

---

## 4. FUNCTIONAL REQUIREMENTS — CLINIC MODULE

### FR-CLI-001: Doctor Schedule Management
- Doctor or admin can set: Working days, Working hours, Break times, Consultation duration, Holidays/leaves
- Changes to schedule auto-update available slots in booking system
- Doctor can set: Max patients per slot, Emergency slots, Teleconsult availability
- System must prevent double-booking under any circumstance
- On-call doctor feature: assign backup doctor when primary is absent

### FR-CLI-002: OPD Queue Management
- Walk-in patients get token from reception desk or self-service kiosk
- Token types: Regular, Priority (senior citizen / differently abled), Emergency
- Doctor dashboard shows: Current patient, Next 3 patients, Total queue count
- Doctor can: Call next patient, Skip patient, Mark consultation complete, Add notes
- Queue auto-adjusts when appointments are cancelled or no-shows confirmed

### FR-CLI-003: Patient CRM
- Each patient has a profile: Contact info, Visit history, Prescriptions, Allergies, Chronic conditions
- Clinic can tag patients: VIP, Chronic, High-risk, Follow-up pending
- Bulk communication: Send WhatsApp message to filtered patient group (e.g., "all diabetic patients")
- Patient acquisition tracking: How did patient find clinic? (referral/ad/walk-in)

### FR-CLI-004: Electronic Medical Records (EMR)
- Doctor can create digital prescription during or after consultation
- Prescription includes: Chief complaint, Diagnosis (ICD-10 code), Medicines (name, dose, frequency, duration), Instructions, Follow-up date
- System auto-suggests ICD-10 codes based on diagnosis text
- Prescription auto-sent to patient via WhatsApp as PDF
- If patient is on medicine delivery platform, prescription triggers auto-fulfillment flow
- Previous prescriptions visible during consultation for reference
- Prescription templates: Doctor can save common prescriptions as templates

### FR-CLI-005: Teleconsultation
- Video call via WebRTC (no third-party app needed)
- Doctor can share screen, annotate images, write prescriptions during call
- Consultation is recorded with patient consent
- Telemedicine guidelines 2020 compliance: Only RMPs can consult, first consult cannot be video-only for emergency drugs
- Fee payment before consultation starts (Razorpay integration)

### FR-CLI-006: Follow-up Automation
- Doctor specifies follow-up period at end of consultation ("Follow up in 2 weeks")
- System auto-schedules reminder to patient at correct time
- Patient receives WhatsApp: "Your follow-up with Dr. [Name] is due. Book now: [link]"
- If patient doesn't book, system retries at: 3 days later, then 7 days later
- Clinic dashboard shows: Pending follow-ups, Overdue follow-ups, Completed

### FR-CLI-007: Clinic Analytics
- Daily report auto-sent to clinic owner via WhatsApp at end of day
- Metrics: Total OPD, Consultations, Revenue, No-shows, New patients, Repeat patients
- Weekly and monthly trend charts on dashboard
- Doctor-wise performance analytics
- Peak hours heatmap to help optimize staffing
- Revenue breakdown: Consultation, Procedures, Pharmacy (if linked)

### FR-CLI-008: Billing & Payment
- Consultation fee auto-calculated based on doctor and appointment type
- Payment modes: Cash, UPI (Razorpay), Card (Razorpay), Insurance, PMJAY
- Auto-generate and email/WhatsApp receipt
- GST invoice for consultation (if clinic is GST-registered)
- Partial payment and pending balance tracking

---

## 5. FUNCTIONAL REQUIREMENTS — PHARMACY MODULE

### FR-PHR-001: Inventory Management
- Add/edit/delete medicines with: Name, Generic name, Manufacturer, Batch number, Expiry date, MRP, Purchase price, Reorder level, Current stock
- Barcode/QR scanning for medicine entry
- Voice command stock update: "Amoxicillin 500mg — 10 strips aaye" → auto-adds to stock
- Multi-location: Same pharmacy owner can manage multiple store inventories
- Stock audit trail: Every addition/deduction logged with timestamp, staff name

### FR-PHR-002: Expiry Management
- System auto-flags: 90 days to expiry (yellow), 30 days (orange), 7 days (red)
- Daily expiry report sent to pharmacy owner via WhatsApp
- Near-expiry medicines auto-listed for return to distributor
- Dead stock report: Medicines not sold in 90+ days
- Expired medicine disposal log (for compliance)

### FR-PHR-003: GST Billing System
- Create sale bills with: Customer name (optional), Prescription link, Medicines, Quantities, HSN codes, GST rates, Discounts, Total
- Automatic GST calculation per medicine (0%, 5%, 12% based on category)
- Generate: B2C invoice (retail), B2B invoice (with GSTIN)
- GSTR-1 monthly report auto-generated
- Bill delivery: Print, WhatsApp PDF, Email
- Bill correction: Cancel and re-issue with proper credit note

### FR-PHR-004: Prescription OCR
- Pharmacist photographs prescription via phone camera
- AI reads: Medicine names, Dosage, Quantity, Doctor name
- Recognized medicines auto-populate bill — pharmacist verifies and confirms
- System checks: Is medicine available in stock? Is it a Schedule H drug (prescription required)?
- OCR accuracy target: >85% for printed prescriptions, >70% for handwritten
- Fallback: Manual entry if OCR confidence is low

### FR-PHR-005: Supplier Ordering
- System tracks reorder levels per medicine
- When stock drops below reorder level: System generates Purchase Order automatically
- PO auto-sent to preferred supplier via WhatsApp + email
- Pharmacist can review and approve POs before sending (configurable)
- Multiple suppliers per medicine with price comparison
- Supplier confirms delivery date — system logs expected delivery
- When goods received: GRN (Goods Received Note) updates inventory

### FR-PHR-006: Credit Customer Management
- Create credit account for regular patients/institutions
- Track outstanding balance per credit customer
- Auto-send payment reminder at: 7 days, 15 days, 30 days after due date
- Generate statement of accounts on demand (WhatsApp PDF)
- Credit limit setting per customer

### FR-PHR-007: Pharmacy Analytics
- Daily sales summary: Total revenue, # of bills, avg bill value, top 10 medicines sold
- Category-wise analysis: Antibiotics, Vitamins, Chronic, OTC
- Profit margin analysis per medicine
- Expiry loss tracking: Value of medicines expired this month/quarter
- Comparison: This week vs last week, This month vs last month

---

## 6. FUNCTIONAL REQUIREMENTS — HOSPITAL MODULE

### FR-HOS-001: IPD Management
- Real-time bed availability dashboard (ward-wise, room-type-wise)
- Patient admission: Attach ABHA ID, diagnosis, admitting doctor, ward, room, bed
- Daily ward round notes by doctor via app or voice
- Nursing notes at bedside via tablet/phone
- Discharge checklist: Bills cleared, Medicines given, Summary prepared, Instructions given
- Length of stay analytics per diagnosis, per doctor

### FR-HOS-002: PMJAY Claim Management
- Onboard hospital as PMJAY-empanelled (integration with NHA sandbox)
- Verify patient PMJAY eligibility in real-time before admission
- Map treatment to HBP (Health Benefit Package) codes
- Auto-generate pre-authorization request to insurance company
- Fill claim form using patient data already in system (zero re-entry)
- Track claim status: Submitted, Under review, Approved, Rejected, Paid
- Rejection analysis: AI suggests corrections for rejected claims
- Monthly reconciliation: Claims submitted vs paid vs pending

### FR-HOS-003: Operation Theatre Management
- OT booking calendar with surgeon, anesthetist, equipment slots
- Pre-op checklist: Consent form, Blood group, Reports ready, Patient fasting
- OT utilization dashboard: Scheduled vs actual hours, cancellations
- Post-op notes by surgeon via voice or app

### FR-HOS-004: Discharge Summary Generator
- AI auto-populates discharge summary from: Admission diagnosis, Treatments given, Medicines prescribed, Doctor notes, Lab reports
- Doctor reviews and approves with e-signature
- Summary auto-sent to patient WhatsApp as PDF
- FHIR-compliant format for ABDM health locker upload

---

## 7. FUNCTIONAL REQUIREMENTS — DISTRIBUTOR MODULE

### FR-DIS-001: Order Management
- Receive automated purchase orders from pharmacy partners
- Dashboard: New orders, Confirmed orders, Out for delivery, Delivered, Returns
- Order confirmation via WhatsApp reply or dashboard click
- Partial fulfillment: System tracks what was delivered vs ordered
- AI voice call to pharmacist when order is out for delivery

### FR-DIS-002: Demand Forecasting
- AI analyzes 90-day order history per medicine per area
- Seasonal adjustment: Monsoon (dengue medicines), Winter (cough/cold), Summer (ORS/electrolytes)
- Stockout prediction: Alert if current stock won't meet projected demand
- Overstock alert: Identify slow-moving SKUs with high inventory

### FR-DIS-003: Route Optimization
- Plot delivery routes for delivery staff
- Optimize based on: Number of stops, Traffic, Priority orders, Refrigeration needs
- Delivery staff app: View route, confirm delivery, collect signature/photo

---

## 8. FUNCTIONAL REQUIREMENTS — AI & AUTOMATION MODULE

### FR-AI-001: AI Voice Agent
- Incoming calls to clinic number answered by AI (not hold music)
- Supported languages: Hindi, Bengali, Bhojpuri (Phase 2), Hinglish
- Intent detection: Appointment booking, Timing enquiry, Doctor availability, Fee enquiry, Emergency, Cancellation
- Conversation: Natural dialogue, not rigid IVR tree
- Escalation: Transfer to human if intent unrecognized after 2 attempts
- Outbound calls: Appointment reminders, Follow-up reminders, Payment reminders, Order confirmations
- Call logs: Every call recorded with transcript, intent detected, action taken

### FR-AI-002: WhatsApp Automation Engine
- Trigger-based messages: Appointment booked → send confirmation; Lab report ready → send PDF
- Interactive buttons: "Confirm / Cancel / Reschedule" clickable in WhatsApp
- Bot conversation flows: Appointment booking, Medicine order, Queue status, FAQ
- Template messages: Pre-approved by Meta for transactional messages
- Session messages: Free-form replies within 24-hour WhatsApp window
- Broadcast: Send campaign messages to patient segments (opt-in only)
- Anti-spam: Rate limiting, patient opt-out handling (mandatory)

### FR-AI-003: n8n Workflow Engine
- Self-hosted n8n instance for all automation workflows
- Pre-built workflow templates: Appointment reminder, Expiry alert, Reorder trigger, Claim status update
- Custom workflow builder: Clinic/pharmacy owners can modify workflows
- Webhook triggers from all modules
- Error handling: Failed workflows logged and alerted to admin
- Version control: Workflow changes tracked with rollback option

### FR-AI-004: Prescription OCR Engine
- Input: Photo via WhatsApp, app camera, or file upload
- Processing: Google Vision API → custom medical NLP layer → medicine name extraction
- Output: Structured list of medicines with name, dose, frequency, quantity
- Confidence score: Each extracted item has confidence %; low-confidence items flagged for manual review
- Drug database matching: Extracted names mapped to system medicine database with fuzzy matching
- Audit log: Original image stored alongside extracted data

---

## 9. FUNCTIONAL REQUIREMENTS — GOVERNMENT INTEGRATION

### FR-GOV-001: ABHA ID Integration
- Patient can create ABHA ID within app (via ABDM API)
- Link existing ABHA ID to patient profile
- Health records auto-synced to ABDM health locker (with consent)
- Consent management: Patient controls what data is shared and with whom
- FHIR R4 format for all health record exchanges

### FR-GOV-002: PMJAY / Ayushman Bharat Integration
- Patient eligibility check via NHA API (name + Aadhaar or ration card)
- PMJAY card scan and verification
- Claim submission via NHA API
- Claim status tracking in real-time
- Hospital-side: Auto-populate HBP codes, pre-auth requests

### FR-GOV-003: Swasthya Sathi (West Bengal)
- Patient Swasthya Sathi card verification
- Treatment pre-authorization request to WB Health Dept
- Claim submission and tracking via WB state portal
- Empanelled hospital list integration

---

## 10. NON-FUNCTIONAL REQUIREMENTS

### 10.1 Performance
| Requirement | Target |
|---|---|
| API Response Time (95th percentile) | < 500ms |
| Appointment booking end-to-end | < 3 seconds |
| WhatsApp message delivery | < 5 seconds |
| AI voice agent response latency | < 1.5 seconds |
| Dashboard load time | < 2 seconds |
| OCR processing time | < 8 seconds |
| System uptime | 99.9% (max 8.7 hours downtime/year) |

### 10.2 Security
- All data encrypted in transit (TLS 1.3) and at rest (AES-256)
- Role-based access control (RBAC) for all modules
- Two-factor authentication (2FA) for admin accounts
- JWT-based session management with 30-minute timeout
- Audit logs: All data access and modifications logged with user ID, timestamp, IP
- DPDP Act 2023 compliance: Consent management, data minimization, breach notification
- No patient health data shared with third parties without explicit consent
- Annual security audit (penetration testing)

### 10.3 Scalability
- Horizontally scalable microservices on AWS Mumbai region
- Database read replicas for analytics queries
- CDN for static assets (Cloudflare)
- Auto-scaling based on load (AWS ECS / EKS)
- Handle 10,000 concurrent users in Phase 2

### 10.4 Reliability & Offline
- Core pharmacy billing must work offline (IndexedDB local cache)
- Offline data syncs when internet connection restored
- Conflict resolution: Last-write-wins with human override for conflicts
- Graceful degradation: If AI fails, system falls back to manual mode

### 10.5 Compliance
- DPDP Act 2023 compliance
- Telemedicine Practice Guidelines 2020
- Drugs and Cosmetics Act 1940
- ABDM FHIR R4 standards
- GST invoicing standards
- IT Act 2000 (intermediary liability)
- ISO 27001 (target by Phase 3)

### 10.6 Accessibility
- App must support Android 8.0+ (low-end Android devices prevalent in UP/WB)
- PWA must work on 2G/3G networks (rural connectivity)
- Text size minimum 16px for readability by elderly users
- Voice-first UX: Critical actions completable by voice alone
- Multi-language: Hindi, Bengali, English (switchable)

---

## 11. DATA REQUIREMENTS

### 11.1 Data Entities
| Entity | Key Attributes |
|---|---|
| Patient | ID, ABHA ID, Name, Phone, DOB, Gender, Address, Language preference, Family members |
| Doctor | ID, NMC registration, Name, Specialization, Clinic, Schedule, Fee |
| Clinic | ID, Name, Address, GST, License, Doctors, Services |
| Appointment | ID, Patient, Doctor, Clinic, DateTime, Type, Status, Token |
| Prescription | ID, Doctor, Patient, Date, Diagnosis (ICD10), Medicines, Follow-up |
| Medicine | ID, Name, Generic name, Brand, Manufacturer, HSN, GST%, MRP, Category |
| Inventory | ID, Medicine, Pharmacy, Batch, Expiry, Stock, Reorder level, Purchase price |
| Sale Bill | ID, Pharmacy, Customer, Items, GST, Total, Payment mode, Prescription ref |
| Purchase Order | ID, Pharmacy, Supplier, Items, Status, Expected delivery |
| Supplier | ID, Name, GST, Contact, Service area, Medicines |
| Claim | ID, Hospital, Patient, PMJAY/SS ID, HBP codes, Amount, Status |
| Staff | ID, Clinic/Pharmacy, Role, Attendance, Salary |

### 11.2 Data Retention
| Data Type | Retention Period |
|---|---|
| Patient health records | 7 years minimum (per ICMR guidelines) |
| Prescriptions | 5 years |
| Financial records / Bills | 8 years (GST requirement) |
| Call recordings | 30 days |
| Audit logs | 3 years |
| Delivery records | 1 year |

---

## 12. INTEGRATION REQUIREMENTS

### 12.1 Mandatory Integrations (Phase 1)
| Service | Purpose | Provider |
|---|---|---|
| WhatsApp Business API | Patient/clinic communication | Interakt / Gupshup (BSP) |
| SMS Gateway | Fallback notifications | Twilio / TextLocal |
| Indian Telephony / IVR | AI voice calls | Exotel |
| Hindi/Bengali STT/TTS | Voice AI language | Sarvam AI |
| Payment Gateway | Consultation & order payments | Razorpay |
| Cloud Infrastructure | Hosting, storage, CDN | AWS Mumbai |
| Push Notifications | App alerts | Firebase FCM |
| Medicine Database | Drug info, interactions, generics | RxNorm / CIMS India API |

### 12.2 Phase 2 Integrations
| Service | Purpose | Provider |
|---|---|---|
| ABDM API | ABHA ID, health records | NHA (Govt) |
| NHA API | PMJAY eligibility + claims | NHA (Govt) |
| OCR Engine | Prescription reading | Google Cloud Vision |
| Swasthya Sathi API | WB state health scheme | WB Govt |
| GST Portal API | GSTR-1 filing | Govt / ClearTax |
| Delivery Partner | Medicine last-mile delivery | Dunzo / local courier API |
| Diagnostic Lab APIs | Test booking, report delivery | SRL / Thyrocare |
| IoT Temperature | Cold chain monitoring | Custom IoT + MQTT |

### 12.3 Phase 3 Integrations
| Service | Purpose | Provider |
|---|---|---|
| HL7 FHIR Server | National health record interoperability | Open FHIR Server |
| Insurance APIs | Health insurance claim direct submission | Star Health / Niva Bupa |
| Bhashini | Regional dialect translation | Govt Free API |
| Biometric / Aadhaar | Staff attendance + patient ID | UIDAI (Aadhaar) |
| ERP Integration | Connect with distributor ERPs (Tally, Marg) | Tally API / Marg API |

---

*FRD v1.0 — HealthcareWale — Compiled May 2026*
*Next Review: Before Phase 1 Development Kickoff*
