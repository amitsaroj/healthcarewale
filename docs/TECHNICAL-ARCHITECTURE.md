# 🏗️ HealthcareWale — Technical Architecture & System Design
> Version: 1.0 | May 2026

---

## 1. SYSTEM ARCHITECTURE OVERVIEW

```
╔══════════════════════════════════════════════════════════════════════════════════╗
║                          HEALTHCAREWALE PLATFORM                               ║
╠══════════════════════════════════════════════════════════════════════════════════╣
║                                                                                  ║
║   ┌─────────────────────────────────────────────────────────────────────────┐   ║
║   │                        CLIENT LAYER                                     │   ║
║   │                                                                         │   ║
║   │  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌─────────┐  │   ║
║   │  │ Patient  │  │  Clinic  │  │ Pharmacy │  │ Hospital │  │Supplier │  │   ║
║   │  │   PWA    │  │   Web    │  │   Web    │  │   Web    │  │   Web   │  │   ║
║   │  └──────────┘  └──────────┘  └──────────┘  └──────────┘  └─────────┘  │   ║
║   │                                                                         │   ║
║   │  ┌──────────────────────┐  ┌────────────────────────────────────────┐  │   ║
║   │  │  React Native App    │  │  WhatsApp Bot    │   AI Voice Agent    │  │   ║
║   │  │  (Android + iOS)     │  │  (Patient/Staff) │   (Hindi/Bengali)   │  │   ║
║   │  └──────────────────────┘  └────────────────────────────────────────┘  │   ║
║   └─────────────────────────────────────────────────────────────────────────┘   ║
║                                         │                                        ║
║   ┌─────────────────────────────────────▼─────────────────────────────────────┐  ║
║   │                     API GATEWAY (AWS API Gateway)                         │  ║
║   │  Rate Limiting │ JWT Auth │ SSL/TLS │ Load Balancer │ Request Logging     │  ║
║   └─────────────────────────────────────┬─────────────────────────────────────┘  ║
║                                         │                                        ║
║   ┌─────────────────────────────────────▼─────────────────────────────────────┐  ║
║   │                     MICROSERVICES LAYER (Node.js)                         │  ║
║   │                                                                            │  ║
║   │  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌───────────────┐  │  ║
║   │  │  Auth    │ │Appoint-  │ │Inventory │ │ Billing  │ │   EMR/PHR     │  │  ║
║   │  │ Service  │ │  ment    │ │ Service  │ │ Service  │ │   Service     │  │  ║
║   │  └──────────┘ └──────────┘ └──────────┘ └──────────┘ └───────────────┘  │  ║
║   │                                                                            │  ║
║   │  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌───────────────┐  │  ║
║   │  │  Voice   │ │WhatsApp  │ │Analytics │ │  Claim   │ │  Supply Chain │  │  ║
║   │  │  AI      │ │Automation│ │ Service  │ │ Service  │ │   Service     │  │  ║
║   │  └──────────┘ └──────────┘ └──────────┘ └──────────┘ └───────────────┘  │  ║
║   │                                                                            │  ║
║   │  ┌──────────┐ ┌──────────┐ ┌──────────┐                                  │  ║
║   │  │Notifica- │ │   OCR    │ │  Queue   │                                  │  ║
║   │  │  tion    │ │ Service  │ │ Manager  │                                  │  ║
║   │  └──────────┘ └──────────┘ └──────────┘                                  │  ║
║   └─────────────────────────────────────┬─────────────────────────────────────┘  ║
║                                         │                                        ║
║   ┌─────────────────────────────────────▼─────────────────────────────────────┐  ║
║   │                         MESSAGE QUEUE (Redis / BullMQ)                     │  ║
║   │   Appointment Jobs │ Notification Jobs │ OCR Jobs │ Report Jobs            │  ║
║   └─────────────────────────────────────┬─────────────────────────────────────┘  ║
║                                         │                                        ║
║   ┌─────────────────────────────────────▼─────────────────────────────────────┐  ║
║   │                           DATA LAYER                                       │  ║
║   │                                                                             │  ║
║   │  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  ┌───────────────┐  │  ║
║   │  │  PostgreSQL  │  │    Redis     │  │   MongoDB    │  │   AWS S3      │  │  ║
║   │  │  (Primary)   │  │  (Cache+     │  │  (Docs/Logs/ │  │  (Files/      │  │  ║
║   │  │  Multi-tenant│  │   Sessions)  │  │   Unstructured│  │   Reports)    │  │  ║
║   │  └──────────────┘  └──────────────┘  └──────────────┘  └───────────────┘  │  ║
║   └─────────────────────────────────────────────────────────────────────────────┘  ║
║                                                                                  ║
║   ┌─────────────────────────────────────────────────────────────────────────────┐  ║
║   │                      EXTERNAL INTEGRATIONS                                  │  ║
║   │  Exotel │ Sarvam AI │ WhatsApp API │ Razorpay │ NHA/ABDM │ Google Vision    │  ║
║   │  Bhashini │ Firebase │ Twilio SMS │ SRL Labs │ Thyrocare │ WB Swasthya Sathi│  ║
║   └─────────────────────────────────────────────────────────────────────────────┘  ║
╚══════════════════════════════════════════════════════════════════════════════════╝
```

---

## 2. TECH STACK — COMPLETE SPECIFICATION

### 2.1 Frontend
| Layer | Technology | Version | Reason |
|---|---|---|---|
| Web Dashboard | Next.js | 14+ | SSR, fast load, SEO |
| Mobile App | React Native | 0.73+ | Single codebase for Android + iOS |
| Patient PWA | Next.js (PWA) | 14+ | No install required, works on 2G |
| UI Component Library | Tailwind CSS + shadcn/ui | Latest | Fast, clean, responsive |
| State Management | Zustand | 4+ | Lightweight for mobile |
| API Client | Axios + React Query | Latest | Caching + background refetch |
| Forms | React Hook Form + Zod | Latest | Validation |
| Charts/Analytics | Recharts | Latest | Dashboards |
| Offline Support | Workbox (Service Workers) | Latest | Offline billing capability |

### 2.2 Backend
| Layer | Technology | Version | Reason |
|---|---|---|---|
| Runtime | Node.js | 20 LTS | Amit's expertise |
| Framework | Fastify | 4+ | Faster than Express, low overhead |
| API Design | REST + WebSocket | — | REST for CRUD, WS for real-time queue |
| Authentication | JWT + Refresh Tokens | — | Stateless auth |
| ORM | Prisma | 5+ | Type-safe DB access |
| Validation | Zod | Latest | Runtime schema validation |
| Queue | BullMQ + Redis | Latest | Background job processing |
| Caching | Redis | 7+ | Session, rate limit, queue |
| Real-time | Socket.io | Latest | Queue updates, live dashboard |
| File Upload | Multer + S3 | Latest | Prescription photos, reports |
| Testing | Jest + Supertest | Latest | Unit + integration tests |

### 2.3 Database
| Database | Use Case | Hosted On |
|---|---|---|
| PostgreSQL 15 | Primary: Patients, appointments, billing, inventory | AWS RDS (Mumbai) |
| Redis 7 | Cache, sessions, job queues, rate limiting | AWS ElastiCache |
| MongoDB 7 | Unstructured: Logs, chat history, audit trails | MongoDB Atlas (Mumbai) |
| AWS S3 | Files: Prescriptions, lab reports, profile photos | AWS S3 (ap-south-1) |
| Elasticsearch | Full-text search: Medicine search, patient search | AWS OpenSearch |

### 2.4 AI / ML Layer
| Component | Technology | Purpose |
|---|---|---|
| Voice STT (Speech-to-Text) | Sarvam AI | Convert patient speech → text in Hindi/Bengali |
| Voice TTS (Text-to-Speech) | Sarvam AI | Convert AI response → natural Hindi/Bengali voice |
| LLM (Intent + Response) | Claude API / GPT-4o | Understand patient intent, generate responses |
| OCR Engine | Google Cloud Vision API | Read handwritten prescriptions |
| Medical NLP | Custom fine-tuned model | Map OCR output to medicine database |
| Demand Forecasting | Python (Prophet + scikit-learn) | Predict inventory demand |
| ICD-10 Suggestion | Custom NLP | Suggest diagnosis codes from doctor text |
| Anomaly Detection | Custom ML | Flag abnormal patient readings (BP, sugar) |

### 2.5 Communication Layer
| Service | Provider | Use Case |
|---|---|---|
| Indian Telephony + IVR | Exotel | AI voice calls (booking, reminders) |
| WhatsApp Business API | Interakt (BSP) | Patient/clinic WhatsApp automation |
| SMS Gateway | Twilio / TextLocal | SMS fallback when WhatsApp fails |
| Email | SendGrid | Clinic onboarding, invoices, reports |
| Push Notifications | Firebase Cloud Messaging | App push alerts |
| Video Calls | Daily.co / 100ms | Teleconsultation WebRTC |

### 2.6 Automation & Workflow
| Service | Technology | Purpose |
|---|---|---|
| Workflow Engine | n8n (self-hosted) | All automation workflows |
| Cron Jobs | node-cron | Scheduled tasks (reminders, reports) |
| Event Bus | Redis Pub/Sub | Service-to-service events |
| Webhook Handler | Custom Node.js | Receive webhooks from external services |

### 2.7 Infrastructure
| Component | Service | Config |
|---|---|---|
| Cloud Provider | AWS Mumbai (ap-south-1) | Primary region for data residency compliance |
| Container Orchestration | AWS ECS (Phase 1) → EKS (Phase 3) | Docker containers |
| CI/CD | GitHub Actions | Auto deploy on merge to main |
| DNS + CDN | Cloudflare | Global CDN, DDoS protection |
| SSL | Let's Encrypt / Cloudflare | Auto-renewing SSL |
| Monitoring | Datadog / Grafana + Prometheus | Performance monitoring |
| Error Tracking | Sentry | Real-time error alerting |
| Logging | AWS CloudWatch | Centralized log management |
| Secrets Management | AWS Secrets Manager | API keys, DB credentials |
| Backup | AWS RDS Automated Backups | Daily backup, 7-day retention |

---

## 3. FLOW DIAGRAMS

### 3.1 Patient Appointment Booking via WhatsApp

```
Patient sends WhatsApp message
         │
         ▼
WhatsApp Business API receives message
         │
         ▼
n8n webhook triggers → Intent Detection (LLM)
         │
    ┌────┴─────────────────┬──────────────────┐
    ▼                      ▼                  ▼
"Book appointment"   "Check queue"      "Cancel/other"
    │                      │                  │
    ▼                      ▼                  ▼
Ask: Doctor name?    Show live          Handle intent
         │           queue position
    ▼
Doctor selection presented (buttons)
         │
         ▼
Fetch available slots from Appointment Service
         │
         ▼
Show date options (next 3 days with slots)
         │
         ▼
Patient selects date → Show time slots
         │
         ▼
Patient selects time slot
         │
         ▼
Confirm screen: "Dr. X on [Date] at [Time]? Confirm / Cancel"
         │
    ┌────┴────────┐
    ▼             ▼
 Confirm        Cancel
    │             │
    ▼             ▼
Create appointment     End flow
in PostgreSQL
    │
    ▼
Send confirmation WhatsApp:
"Appointment confirmed ✅
Token: #HW-2456
Dr. Sharma, 10:30 AM, Tue 4 Jun
📍 Apollo Clinic, MG Road
[Add to Calendar] [Get Directions]"
    │
    ▼
Schedule reminder jobs in BullMQ:
- 48h before: WhatsApp reminder
- 2h before: WhatsApp + AI voice call
    │
    ▼
Update clinic dashboard (real-time via Socket.io)
```

---

### 3.2 AI Voice Call Flow (Incoming Patient Call to Clinic)

```
Patient dials clinic number
         │
         ▼
Exotel receives call → webhook to Voice AI Service
         │
         ▼
Language Detection (Hindi/Bengali based on caller area code)
         │
         ▼
Sarvam AI TTS: "Namaste! Main HealthcareWale ka AI assistant hun.
               Aap appointment book karna chahte hain?"
         │
         ▼
Patient speaks → Sarvam AI STT → text transcript
         │
         ▼
LLM Intent Detection
         │
    ┌────┴──────────────────┬─────────────────┐
    ▼                       ▼                 ▼
"Book appointment"    "Doctor timing"    "Emergency"
    │                       │                 │
    ▼                       ▼                 ▼
Appointment booking    Share timings      "Please call 108
conversation flow      and transfer       or go to nearest
                       to WhatsApp        emergency room"
    │
    ▼
Collect: Doctor name, preferred date
    │
    ▼
Check slot availability in real-time
    │
    ▼
Offer available slots via voice
    │
    ▼
Patient confirms → Create appointment
    │
    ▼
"Appointment booked hai!
Token number hai 2456.
Aapke WhatsApp par confirmation aayega."
    │
    ▼
Send WhatsApp confirmation
    │
    ▼
Store call log + transcript in MongoDB
```

---

### 3.3 Pharmacy Inventory Reorder Flow

```
Inventory Service checks stock levels (every 6 hours via cron)
         │
         ▼
Identify medicines below reorder level
         │
         ▼
For each low-stock medicine:
         │
    ┌────┴────────────────────────────────────┐
    ▼                                         ▼
Auto-approve mode                    Manual-approve mode
(configured by owner)                (configured by owner)
    │                                         │
    ▼                                         ▼
Generate Purchase Order              Send WhatsApp to owner:
immediately                          "Stock low: Paracetamol 500
    │                                Current: 5 strips
    │                                Reorder qty: 50 strips
    │                                Supplier: Sharma Medicos
    │                                [Approve] [Modify] [Skip]"
    │                                         │
    │                                         ▼
    │                                Owner taps [Approve]
    │                                         │
    └─────────────┬───────────────────────────┘
                  ▼
    Generate Purchase Order (PDF)
                  │
                  ▼
    Send PO to supplier via WhatsApp:
    "New Order from Raj Medical Store
    Date: 04 Jun 2026
    1. Paracetamol 500mg - 50 strips
    2. Amoxicillin 250mg - 20 strips
    Total: ₹3,450
    [Confirm Order] [Call Back]"
                  │
                  ▼
    Supplier confirms → delivery date logged
                  │
                  ▼
    GRN created when stock received →
    inventory auto-updated
```

---

### 3.4 PMJAY Claim Filing Flow

```
Patient admitted → Eligibility check
         │
         ▼
NHA API: Verify patient PMJAY card
         │
    ┌────┴──────────┐
    ▼               ▼
Eligible          Not eligible
    │               │
    ▼               ▼
Map treatment    Offer: Self-pay /
to HBP code      other insurance
    │
    ▼
Pre-authorization request sent to insurance
    │
    ▼
Insurance approves → treatment proceeds
    │
    ▼
At discharge:
- System pulls: Admission data, treatment, medicines, procedures
- AI maps to ICD-10 codes
- Auto-fills PMJAY claim form
- Doctor reviews and signs digitally
    │
    ▼
Claim submitted via NHA API
    │
    ▼
Claim status tracked in dashboard:
Submitted → Under review → Approved → Payment received
    │
    ▼
If rejected:
AI analyzes rejection reason →
Suggests correction →
Resubmit with fix
```

---

### 3.5 Prescription OCR + Auto-Billing Flow

```
Pharmacist takes photo of prescription
         │
         ▼
Image uploaded to AWS S3 via app
         │
         ▼
OCR Service triggered (Google Cloud Vision API)
         │
         ▼
Raw text extracted from image
         │
         ▼
Medical NLP Layer:
- Extract medicine names (fuzzy match against database)
- Extract dose, frequency, quantity
- Identify doctor name (validate if registered)
- Flag Schedule H drugs
         │
         ▼
Confidence score calculated per medicine
         │
    ┌────┴──────────────────────────┐
    ▼                               ▼
High confidence (>85%)         Low confidence (<85%)
    │                               │
    ▼                               ▼
Auto-populate bill             Highlight in yellow —
    │                          pharmacist manually verifies
    │                               │
    └──────────────┬────────────────┘
                   ▼
    Check stock availability for each item
                   │
         ┌─────────┴──────────────┐
         ▼                        ▼
    In stock                Out of stock
         │                        │
         ▼                        ▼
    Add to bill             Suggest generic alternative /
                            Mark as unavailable
                   │
                   ▼
    Pharmacist reviews and confirms bill
                   │
                   ▼
    Generate GST invoice
                   │
                   ▼
    Send to customer via WhatsApp PDF
                   │
                   ▼
    Deduct from inventory automatically
```

---

### 3.6 Complete Patient Journey (End-to-End)

```
1. DISCOVERY
Patient hears about clinic via word-of-mouth / Google
         │
         ▼
2. BOOKING
WhatsApp/Call/App → AI books appointment → Token confirmed
         │
         ▼
3. REMINDERS
48h reminder → 2h reminder (with AI voice call) → Queue alert
         │
         ▼
4. VISIT
Patient arrives → Check-in via WhatsApp → Virtual queue
Doctor calls patient → Consultation → EMR created
Prescription generated → WhatsApp PDF to patient
         │
         ▼
5. POST-VISIT
Lab test ordered → Home sample collection booked
Medicine delivery from empanelled pharmacy
Follow-up scheduled automatically
         │
         ▼
6. CHRONIC CARE
Monthly medicine reminders → Auto-refill
Quarterly diagnostic reminders
Abnormal reading alert to doctor
         │
         ▼
7. RETENTION
Patient stays in ecosystem: Family members added
All health records in one place → switching cost very high
```

---

## 4. DATABASE SCHEMA (Key Tables)

```sql
-- TENANTS (Multi-tenant isolation)
CREATE TABLE tenants (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name VARCHAR(255) NOT NULL,
  type ENUM('clinic','pharmacy','hospital','distributor'),
  plan ENUM('free','basic','pro','enterprise'),
  state VARCHAR(50),
  city VARCHAR(100),
  gst_number VARCHAR(20),
  created_at TIMESTAMP DEFAULT NOW()
);

-- PATIENTS
CREATE TABLE patients (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  tenant_id UUID REFERENCES tenants(id),
  abha_id VARCHAR(20) UNIQUE,
  name VARCHAR(255) NOT NULL,
  phone VARCHAR(15) NOT NULL UNIQUE,
  dob DATE,
  gender ENUM('male','female','other'),
  language_preference ENUM('hindi','bengali','english') DEFAULT 'hindi',
  family_group_id UUID,
  created_at TIMESTAMP DEFAULT NOW()
);

-- APPOINTMENTS
CREATE TABLE appointments (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  tenant_id UUID REFERENCES tenants(id),
  patient_id UUID REFERENCES patients(id),
  doctor_id UUID REFERENCES doctors(id),
  appointment_date DATE NOT NULL,
  appointment_time TIME NOT NULL,
  token_number VARCHAR(10),
  type ENUM('opd','followup','teleconsult','emergency'),
  status ENUM('booked','confirmed','in_progress','completed','cancelled','no_show'),
  booking_channel ENUM('app','whatsapp','voice','walk_in','staff'),
  notes TEXT,
  created_at TIMESTAMP DEFAULT NOW()
);

-- MEDICINES
CREATE TABLE medicines (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name VARCHAR(255) NOT NULL,
  generic_name VARCHAR(255),
  brand VARCHAR(255),
  manufacturer VARCHAR(255),
  hsn_code VARCHAR(10),
  gst_rate DECIMAL(5,2),
  mrp DECIMAL(10,2),
  schedule ENUM('OTC','H','H1','X','G'), -- Drug schedule
  category VARCHAR(100),
  unit VARCHAR(20) -- strip, tablet, ml, bottle
);

-- INVENTORY
CREATE TABLE inventory (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  tenant_id UUID REFERENCES tenants(id),
  medicine_id UUID REFERENCES medicines(id),
  batch_number VARCHAR(50),
  expiry_date DATE NOT NULL,
  purchase_price DECIMAL(10,2),
  mrp DECIMAL(10,2),
  current_stock INTEGER NOT NULL DEFAULT 0,
  reorder_level INTEGER NOT NULL DEFAULT 10,
  preferred_supplier_id UUID,
  created_at TIMESTAMP DEFAULT NOW()
);

-- PRESCRIPTIONS
CREATE TABLE prescriptions (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  patient_id UUID REFERENCES patients(id),
  doctor_id UUID REFERENCES doctors(id),
  appointment_id UUID REFERENCES appointments(id),
  diagnosis TEXT,
  icd10_codes VARCHAR(20)[],
  medicines JSONB, -- [{medicine_id, name, dose, frequency, duration, instructions}]
  follow_up_date DATE,
  follow_up_instructions TEXT,
  created_at TIMESTAMP DEFAULT NOW()
);

-- SALE BILLS
CREATE TABLE sale_bills (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  tenant_id UUID REFERENCES tenants(id),
  patient_id UUID REFERENCES patients(id),
  prescription_id UUID REFERENCES prescriptions(id),
  items JSONB, -- [{medicine_id, name, qty, rate, gst_rate, amount}]
  subtotal DECIMAL(10,2),
  gst_amount DECIMAL(10,2),
  discount DECIMAL(10,2),
  total DECIMAL(10,2),
  payment_mode ENUM('cash','upi','card','credit','insurance','pmjay'),
  bill_date DATE DEFAULT CURRENT_DATE,
  created_at TIMESTAMP DEFAULT NOW()
);
```

---

## 5. API DESIGN (Key Endpoints)

### 5.1 Authentication
```
POST /api/v1/auth/send-otp      → Send OTP to phone
POST /api/v1/auth/verify-otp    → Verify OTP, return JWT
POST /api/v1/auth/refresh       → Refresh JWT token
POST /api/v1/auth/logout        → Invalidate token
```

### 5.2 Appointments
```
GET  /api/v1/appointments/slots?doctorId=&date=    → Available slots
POST /api/v1/appointments/book                     → Book appointment
GET  /api/v1/appointments/:id                      → Get appointment
PUT  /api/v1/appointments/:id/cancel               → Cancel
PUT  /api/v1/appointments/:id/reschedule           → Reschedule
GET  /api/v1/appointments/queue?clinicId=&date=    → Live queue
POST /api/v1/appointments/:id/complete             → Mark done (doctor)
```

### 5.3 Inventory
```
GET  /api/v1/inventory?tenantId=&search=           → Search inventory
POST /api/v1/inventory/add                         → Add stock
PUT  /api/v1/inventory/:id/update                  → Update stock
GET  /api/v1/inventory/expiry-alerts               → Near-expiry list
GET  /api/v1/inventory/reorder-alerts              → Low stock list
POST /api/v1/inventory/voice-update                → Voice command stock update
POST /api/v1/inventory/ocr-prescription            → OCR prescription
```

### 5.4 Billing
```
POST /api/v1/billing/create-bill                   → Create sale bill
GET  /api/v1/billing/:id                           → Get bill
GET  /api/v1/billing/gst-report?month=&year=       → GST report
POST /api/v1/billing/send-whatsapp/:id             → Send bill to customer
POST /api/v1/billing/purchase-order/create         → Create PO to supplier
```

### 5.5 AI / Automation
```
POST /api/v1/voice/incoming-call                   → Exotel webhook (AI agent)
POST /api/v1/whatsapp/webhook                      → WhatsApp message webhook
POST /api/v1/ocr/prescription                      → OCR prescription image
POST /api/v1/ai/icd10-suggest                      → Suggest ICD-10 from text
GET  /api/v1/ai/demand-forecast?medicineId=        → Inventory demand forecast
```

---

## 6. THIRD-PARTY SERVICES & LIBRARIES

### 6.1 External Services (Paid)

| Service | Provider | Monthly Cost (Est.) | Purpose |
|---|---|---|---|
| WhatsApp Business API | Interakt BSP | ₹3,000–8,000 | Patient/clinic WhatsApp automation |
| Indian Telephony | Exotel | ₹5,000–25,000 (usage) | AI voice calls, IVR |
| Hindi/Bengali Voice AI | Sarvam AI | ₹2,000–10,000 (usage) | STT + TTS in Indian languages |
| LLM / AI Reasoning | Anthropic Claude / OpenAI | ₹5,000–20,000 (usage) | Intent detection, response generation |
| OCR | Google Cloud Vision API | ₹2,000–8,000 (usage) | Prescription reading |
| Payment Gateway | Razorpay | 2% per transaction | Payments, subscriptions, settlements |
| Cloud Hosting | AWS Mumbai | ₹15,000–40,000 | Servers, database, storage |
| SMS Gateway | Twilio / TextLocal | ₹2,000–5,000 (usage) | SMS fallback notifications |
| Email Service | SendGrid | ₹1,500–5,000 | Transactional emails |
| Video Calls | 100ms / Daily.co | ₹2,000–8,000 | Teleconsultation |
| Push Notifications | Firebase | Free–₹2,000 | App push alerts |
| CDN + Security | Cloudflare | Free–₹3,000 | CDN, DDoS, DNS |
| Error Tracking | Sentry | ₹0–3,000 | Real-time error alerts |
| Monitoring | Datadog / Grafana | ₹3,000–10,000 | Performance dashboards |
| Regional Language | Bhashini (Govt) | FREE | Regional dialect support |

### 6.2 Government APIs (Free)

| API | Authority | Purpose |
|---|---|---|
| ABDM Sandbox | National Health Authority | ABHA ID creation, health records |
| PMJAY NHA API | National Health Authority | Patient eligibility, claim filing |
| Bhashini API | Govt of India | Free Indian language translation |
| eSanjeevani API | MoHFW | Telemedicine integration |
| Swasthya Sathi API | WB Government | WB state health scheme |
| GSTIN Verification | GST Portal | Verify pharmacy/supplier GST numbers |
| DigiLocker API | MeitY | Document verification |

### 6.3 NPM Libraries (Backend — Node.js)

```json
{
  "dependencies": {
    "fastify": "^4.26",
    "prisma": "^5.10",
    "@prisma/client": "^5.10",
    "redis": "^4.6",
    "bullmq": "^5.4",
    "socket.io": "^4.7",
    "jsonwebtoken": "^9.0",
    "bcryptjs": "^2.4",
    "zod": "^3.22",
    "axios": "^1.6",
    "multer": "^1.4",
    "aws-sdk": "^2.1585",
    "pdfkit": "^0.14",
    "sharp": "^0.33",
    "node-cron": "^3.0",
    "winston": "^3.11",
    "helmet": "^7.1",
    "cors": "^2.8",
    "dotenv": "^16.4",
    "uuid": "^9.0",
    "dayjs": "^1.11",
    "nodemailer": "^6.9",
    "twilio": "^5.0",
    "razorpay": "^2.9",
    "fuse.js": "^7.0",
    "compromise": "^14.10",
    "natural": "^6.10"
  },
  "devDependencies": {
    "typescript": "^5.3",
    "@types/node": "^20",
    "jest": "^29",
    "supertest": "^6.3",
    "eslint": "^8",
    "prettier": "^3",
    "nodemon": "^3"
  }
}
```

### 6.4 NPM Libraries (Frontend — Next.js / React Native)

```json
{
  "dependencies": {
    "next": "14.x",
    "react": "^18",
    "react-native": "0.73.x",
    "@tanstack/react-query": "^5",
    "zustand": "^4",
    "react-hook-form": "^7",
    "zod": "^3",
    "axios": "^1.6",
    "tailwindcss": "^3",
    "framer-motion": "^11",
    "recharts": "^2.10",
    "lucide-react": "latest",
    "date-fns": "^3",
    "react-native-camera": "^4",
    "react-native-voice": "^3",
    "react-native-permissions": "^4",
    "@react-native-async-storage/async-storage": "^1.22",
    "react-native-push-notification": "^8",
    "react-native-maps": "^1.10",
    "@gorhom/bottom-sheet": "^4",
    "socket.io-client": "^4.7",
    "i18n-js": "^4.3",
    "next-pwa": "^5.6"
  }
}
```

### 6.5 Python Libraries (AI/ML Service)

```
prophet==1.1.5          # Demand forecasting
scikit-learn==1.4.0     # ML models
pandas==2.2.0           # Data processing
numpy==1.26.0           # Numerical ops
fastapi==0.110.0        # Python ML API server
uvicorn==0.29.0         # ASGI server
google-cloud-vision==3.7.0  # OCR
transformers==4.38.0    # NLP models (HuggingFace)
torch==2.2.0            # PyTorch for custom models
fuzzywuzzy==0.18.0      # Fuzzy string matching for medicine names
indic-nlp-library==0.91 # Indian language NLP
```

---

## 7. DEPLOYMENT ARCHITECTURE

```
                     ┌──────────────────────────────────────┐
                     │         CLOUDFLARE CDN                │
                     │  (DDoS Protection + Global Cache)     │
                     └──────────────┬───────────────────────┘
                                    │
                     ┌──────────────▼───────────────────────┐
                     │         AWS Mumbai Region             │
                     │         (ap-south-1)                  │
                     │                                       │
                     │  ┌─────────────────────────────────┐  │
                     │  │      AWS Application Load        │  │
                     │  │       Balancer (ALB)             │  │
                     │  └──────────┬──────────────────────┘  │
                     │             │                          │
                     │  ┌──────────▼──────────────────────┐  │
                     │  │   AWS ECS (Docker Containers)    │  │
                     │  │                                  │  │
                     │  │  ┌────────┐ ┌────────┐          │  │
                     │  │  │ API    │ │ Worker │          │  │
                     │  │  │ Server │ │ Service│          │  │
                     │  │  │ (x3)   │ │ (x2)  │          │  │
                     │  │  └────────┘ └────────┘          │  │
                     │  └──────────────────────────────────┘  │
                     │                                        │
                     │  ┌──────────────────────────────────┐  │
                     │  │         Data Layer               │  │
                     │  │  RDS PostgreSQL (Multi-AZ)       │  │
                     │  │  ElastiCache Redis               │  │
                     │  │  S3 Buckets (Encrypted)          │  │
                     │  └──────────────────────────────────┘  │
                     │                                        │
                     │  ┌──────────────────────────────────┐  │
                     │  │      Self-Hosted Services        │  │
                     │  │  n8n (EC2)  │  ML Service (EC2) │  │
                     │  └──────────────────────────────────┘  │
                     └──────────────────────────────────────┘
```

---

## 8. SECURITY ARCHITECTURE

```
Security Layers:
1. Cloudflare WAF → Block malicious traffic before reaching servers
2. AWS VPC → All services in private subnet, only ALB is public
3. API Gateway → Rate limiting (100 req/min per IP)
4. JWT Authentication → Every API call requires valid token
5. RBAC → Role-based access, users see only their data
6. Multi-tenant isolation → Tenant ID in every DB query (Row-Level Security)
7. Data encryption → TLS 1.3 in transit, AES-256 at rest
8. Audit logging → Every CRUD operation logged (MongoDB)
9. DPDP Act compliance → Consent flags in patient table
10. PII masking → Logs never contain phone numbers or health data
```

---

*HealthcareWale — Technical Architecture v1.0 — May 2026*
