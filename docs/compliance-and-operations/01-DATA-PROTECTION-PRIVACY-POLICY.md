# 🔒 HealthcareWale — Data Protection & Privacy Policy
> **Document ID:** HW-PRIV-001  
> **Version:** 1.0 | **Effective Date:** [Insert Effective Date]  
> **Jurisdiction:** India (Primary) | United States (HIPAA) | European Union (GDPR)  
> **Compliance Frameworks:** DPDP Act 2023 (India) · HIPAA 1996 (US) · GDPR 2018 (EU) · IT Act 2000 (India)  
> **Last Reviewed:** May 2026 | **Next Review:** May 2027  
> **Document Owner:** Founder & Data Protection Officer — HealthcareWale Technologies Pvt. Ltd.

---

## TABLE OF CONTENTS
1. [Introduction & Scope](#1-introduction--scope)
2. [Definitions](#2-definitions)
3. [Data We Collect](#3-data-we-collect)
4. [Legal Basis for Processing](#4-legal-basis-for-processing)
5. [How We Use Your Data](#5-how-we-use-your-data)
6. [Protected Health Information (PHI) Handling](#6-protected-health-information-phi-handling)
7. [Data Sharing & Third-Party Disclosure](#7-data-sharing--third-party-disclosure)
8. [Data Transfers Across Borders](#8-data-transfers-across-borders)
9. [Data Retention & Deletion](#9-data-retention--deletion)
10. [Your Rights as a Data Principal](#10-your-rights-as-a-data-principal)
11. [Security Measures](#11-security-measures)
12. [Cookies & Tracking Technologies](#12-cookies--tracking-technologies)
13. [Children's Privacy](#13-childrens-privacy)
14. [AI & Automated Decision-Making](#14-ai--automated-decision-making)
15. [Consent Management](#15-consent-management)
16. [Grievance Redressal](#16-grievance-redressal)
17. [Changes to This Policy](#17-changes-to-this-policy)

---

## 1. Introduction & Scope

HealthcareWale Technologies Private Limited ("HealthcareWale," "SwasthAI," "we," "us," or "our") operates an AI-powered healthcare operations platform connecting patients, licensed medical practitioners, pharmacies, hospitals, and pharmaceutical distributors across India, with primary operations in Uttar Pradesh and West Bengal.

This Data Protection & Privacy Policy ("Policy") governs the collection, processing, storage, transfer, and deletion of all personal data and protected health information processed through:
- The HealthcareWale mobile application (Android & iOS)
- The HealthcareWale web dashboard (healthcarewale.in and subdomains)
- The WhatsApp Business automation interface
- The AI Voice Agent system (inbound and outbound calls via Exotel)
- Any API integrations, including ABDM, PMJAY (NHA), Swasthya Sathi (West Bengal), and third-party diagnostic/pharmacy partners

**This Policy applies to:**
- Patients and their authorized caregivers
- Licensed Medical Practitioners (LMPs) onboarded on the platform
- Pharmacy owners and pharmacists
- Hospital administrators and clinical staff
- Pharmaceutical distributors and suppliers
- Visitors to our websites and web properties

**This Policy does NOT apply to:**
- Third-party websites linked from our platform
- Independent data practices of partner hospitals or clinics outside our processing agreement

---

## 2. Definitions

| Term | Definition |
|---|---|
| **Data Principal** | The individual (patient, doctor, pharmacist, or caregiver) whose personal data is being processed |
| **Data Fiduciary** | HealthcareWale Technologies Pvt. Ltd. — the entity determining the purpose and means of processing |
| **Significant Data Fiduciary (SDF)** | Classification under DPDP Act 2023 — applies if HealthcareWale processes high volumes of sensitive data or data of children |
| **Personal Data** | Any data that can directly or indirectly identify a natural person |
| **Sensitive Personal Data (SPD)** | Health data, biometric data, financial data, sexual orientation, religious beliefs — attracts heightened protection under DPDP Act |
| **Protected Health Information (PHI)** | Under HIPAA: individually identifiable health information transmitted or maintained in any form |
| **Processing** | Any operation performed on personal data — collection, storage, use, disclosure, sharing, or deletion |
| **Consent** | Free, specific, informed, unconditional, and unambiguous agreement by the Data Principal to processing |
| **Data Processor** | Third-party entities processing data on HealthcareWale's behalf (e.g., AWS, Sarvam AI, Exotel) |
| **ABHA ID** | Ayushman Bharat Health Account — a 14-digit unique health identifier issued by NHA, India |
| **DPDP Act** | Digital Personal Data Protection Act, 2023 (India) |
| **GDPR** | General Data Protection Regulation, 2018 (European Union) |
| **HIPAA** | Health Insurance Portability and Accountability Act, 1996 (United States) |

---

## 3. Data We Collect

### 3.1 Patient Data

**Identity & Contact Information:**
- Full name, date of birth, gender, mobile number, email address (optional)
- Residential address (city, district, pin code)
- Language preference (Hindi, Bengali, English)
- Emergency contact name and number

**Health & Medical Information (Sensitive Personal Data):**
- ABHA ID (Ayushman Bharat Health Account number)
- Appointment history, visit records, consultation notes
- Prescriptions, diagnosis codes (ICD-10/ICD-11), medicines prescribed
- Lab test orders, diagnostic reports, pathology results
- Chronic condition flags (diabetes, hypertension, cardiac, thyroid, etc.)
- Medication reminders and refill history
- Vital readings logged by patient (blood pressure, blood glucose, weight)
- PMJAY/Swasthya Sathi card number and eligibility data
- Insurance policy information (where provided)
- Allergy history and adverse drug reaction records

**Interaction Data:**
- WhatsApp conversation transcripts (appointment booking, bot interactions)
- AI Voice call recordings and transcripts (inbound booking calls, outbound reminders)
- In-app activity logs (features used, screens viewed)
- Support ticket content and chat history

**Device & Technical Data:**
- Device type, operating system, app version
- IP address, approximate geolocation (city-level only)
- Browser type (for PWA users)
- Firebase push notification token

### 3.2 Medical Practitioner Data

- NMC/State Medical Council registration number and verification documents
- Qualifications, degrees, specializations
- Practice address, clinic name, consultation hours, fee structure
- Consultation records and e-prescription outputs
- Payout details (bank account or UPI for platform fee settlements)
- Identity documents (Aadhaar, PAN) for KYC

### 3.3 Pharmacy & Distributor Data

- GST registration number, drug license number
- Inventory data, purchase orders, sale bills
- Supplier account details, payment records
- Staff names and contact numbers (for access control)

### 3.4 Data We Do NOT Collect

- Aadhaar number in raw form (we use Aadhaar-based authentication via UIDAI APIs only — we do not store the 12-digit number)
- Full payment card numbers (processed by Razorpay PCI-DSS-compliant infrastructure only)
- Precise GPS coordinates of patients (city-level geolocation only)
- Biometric data (fingerprints, retina scans) — unless specifically introduced for staff attendance under separate consent

---

## 4. Legal Basis for Processing

### 4.1 Under DPDP Act 2023 (India)

| Processing Activity | Legal Basis |
|---|---|
| Patient registration and appointment booking | **Consent** — explicit, informed, purpose-specific |
| Appointment reminders via WhatsApp and voice | **Consent** — given at registration, revocable |
| Sharing health records with treating doctor | **Consent** + **Legitimate use** (providing requested healthcare service) |
| PMJAY eligibility verification | **Legal obligation** (NHA API integration mandated for empanelled hospitals) |
| ABHA ID linking | **Consent** (voluntary per ABDM guidelines) |
| Pharmacy billing and GST compliance | **Legal obligation** (GST Act, Drugs & Cosmetics Act) |
| Fraud detection and platform security | **Legitimate use** |
| Medical record retention (7 years) | **Legal obligation** (ICMR guidelines) |

### 4.2 Under GDPR (EU Users — If Applicable)

| Processing Activity | Legal Basis (GDPR Article) |
|---|---|
| Account registration | Art. 6(1)(a) — Consent |
| Healthcare service delivery | Art. 9(2)(h) — Medical purposes |
| Legal/regulatory compliance | Art. 6(1)(c) — Legal obligation |
| Fraud prevention | Art. 6(1)(f) — Legitimate interests |
| Health data processing | Art. 9(2)(a) — Explicit consent |

### 4.3 Under HIPAA (US Users — If Applicable)

HealthcareWale processes PHI only under a valid Business Associate Agreement (BAA) with covered entity partners. Treatment, Payment, and Healthcare Operations (TPO) are the primary permitted uses. We do not use PHI for marketing without separate authorization.

---

## 5. How We Use Your Data

### 5.1 Primary Uses (Core Service Delivery)
- Book, confirm, reschedule, and cancel medical appointments
- Operate AI voice booking agent (inbound and outbound calls)
- Send automated appointment reminders via WhatsApp, SMS, and voice
- Manage virtual waiting room queue and token system
- Generate and deliver digital prescriptions to patients via WhatsApp
- Process medicine delivery orders to partner pharmacies
- File PMJAY/Swasthya Sathi insurance pre-authorization and claims
- Manage pharmacy inventory, billing, and supplier ordering

### 5.2 Secondary Uses (With Separate Consent)
- Chronic disease follow-up programs (opt-in)
- Health education content delivery (opt-in)
- Patient satisfaction surveys post-consultation
- Anonymized, aggregated analytics sold to pharma companies (requires explicit opt-in; data is de-identified before use — see Section 14)

### 5.3 Prohibited Uses
- We will NEVER sell identified patient health data to any third party
- We will NEVER use patient health data for advertising targeting without explicit opt-in
- We will NEVER use patient data to train external LLM models without explicit consent and full de-identification (see AI Data Minimization Policy — HW-AI-002)
- We will NEVER share data with law enforcement without a valid court order, except where immediate risk to life is established

---

## 6. Protected Health Information (PHI) Handling

### 6.1 PHI Classification Matrix

| Data Type | Sensitivity Level | Access Control |
|---|---|---|
| Patient name + diagnosis | **Critical PHI** | Doctor + patient only |
| Prescription content | **Critical PHI** | Doctor + pharmacist + patient |
| Lab reports | **Critical PHI** | Doctor + lab + patient |
| PMJAY card + claim data | **Critical PHI** | Hospital admin + NHA API |
| Appointment history | **High** | Doctor + clinic staff + patient |
| Medicine delivery records | **Medium** | Pharmacy + patient |
| Billing records | **Medium** | Finance team + patient |
| Contact information | **Standard PII** | Support team (with audit log) |

### 6.2 Minimum Necessary Standard

Consistent with HIPAA's Minimum Necessary Rule and DPDP Act's data minimization principle:
- Pharmacists see only the prescription relevant to their dispensing action — not the patient's full medical history
- Delivery partners see only patient name, delivery address, and order ID — not diagnosis or prescription details
- Distributor partners see only aggregate demand data — never individual patient data
- AI voice agents are provided only the data required to complete the specific interaction (slot availability, doctor name, patient token) — no full health record access

### 6.3 De-identification Protocol

When patient data is used for analytics, reporting, or pharma company data products:
1. Direct identifiers removed: Name, phone, address, ABHA ID, email
2. Quasi-identifiers generalized: Exact age → age bracket; Exact location → district-level
3. Diagnosis codes retained only in aggregated, statistical form
4. De-identification reviewed by Data Protection Officer before any data release
5. Safe Harbor method (as defined under HIPAA) applied as baseline standard

---

## 7. Data Sharing & Third-Party Disclosure

### 7.1 Data Processors (Sub-processors)

HealthcareWale shares data with the following processors under Data Processing Agreements (DPAs):

| Processor | Category | Data Shared | Location |
|---|---|---|---|
| Amazon Web Services (AWS) | Cloud infrastructure | All platform data (encrypted) | Mumbai, India (ap-south-1) |
| Interakt / Gupshup | WhatsApp BSP | Message content, phone numbers | India |
| Exotel | Telephony | Call recordings, phone numbers | India |
| Sarvam AI | Voice AI (STT/TTS) | Voice audio streams (not stored) | India |
| Razorpay | Payment processing | Transaction data, billing info | India |
| Anthropic / OpenAI | LLM API | De-identified conversation intent only | US (under DPA) |
| Google Cloud Vision | OCR | Prescription images (not stored post-processing) | US (under DPA) |
| Firebase (Google) | Push notifications | Device tokens, message payloads | US (under DPA) |
| Twilio / TextLocal | SMS | Phone numbers, message content | US / India |
| MongoDB Atlas | Database | Logs, audit trails | Mumbai, India |
| SendGrid | Email | Email address, notification content | US (under DPA) |

### 7.2 Government & Regulatory Disclosure

We are legally required to share data with:
- **National Health Authority (NHA):** PMJAY eligibility and claim processing
- **ABDM:** ABHA ID linking and FHIR-compliant health record exchange (patient-consented)
- **West Bengal Health Dept:** Swasthya Sathi scheme integration
- **GSTN (GST Network):** Pharmacy billing tax data
- **TRAI / DoT:** SMS DLT compliance records
- **Courts / Law Enforcement:** Only under valid court order with legal review

### 7.3 Business Transfers

In the event of a merger, acquisition, or asset sale, patient data will be transferred only with:
- Prior notification to affected Data Principals (minimum 30 days)
- Continuity of privacy protections under this Policy
- Option for patients to request data deletion before transfer completes

---

## 8. Data Transfers Across Borders

### 8.1 Indian Data Residency (Primary)

All primary patient health data is stored in **AWS Mumbai region (ap-south-1)** — within Indian territory, compliant with DPDP Act data localization requirements.

### 8.2 Cross-Border Transfers (Where Applicable)

Where data is processed by US/EU-based processors (Google Cloud Vision, Anthropic, Firebase, SendGrid):
- Only de-identified or non-health operational data is transferred
- Standard Contractual Clauses (SCCs) under GDPR are in place
- Data Processing Agreements executed with each processor
- Voice audio streams sent to Sarvam AI are processed in-memory and not stored post-transcription
- Prescription images sent to Google Cloud Vision are not stored after OCR processing completes

### 8.3 GDPR Adequacy

India does not currently hold an EU adequacy decision. For any EU-resident data subjects, HealthcareWale relies on Standard Contractual Clauses (Art. 46 GDPR) and explicit consent (Art. 49(1)(a) GDPR) for cross-border transfers.

---

## 9. Data Retention & Deletion

| Data Category | Retention Period | Legal Basis |
|---|---|---|
| Patient health records (prescriptions, diagnoses) | **7 years** from last interaction | ICMR Medical Records Guidelines |
| Appointment records | **5 years** | Medical liability standards |
| Financial records / GST invoices / bills | **8 years** | GST Act, Income Tax Act |
| AI voice call recordings | **30 days**, then auto-deleted | Operational quality only |
| WhatsApp chat transcripts | **90 days** active, **2 years** archived | Support and audit |
| Audit logs (system access, data changes) | **3 years** | IT Act 2000, DPDP Act |
| Medicine delivery records | **1 year** | Drugs & Cosmetics Rules |
| Staff attendance and payroll data | **5 years** | Labour laws |
| Marketing opt-in/opt-out records | **3 years after opt-out** | Consent audit trail |
| Deleted patient account data | **30 days post-deletion request**, then permanently purged | DPDP Act S.12 |

### 9.1 Secure Deletion Standards

- Database records: Cryptographic erasure (encryption key destruction) + logical deletion
- S3 files: AWS S3 Object Expiry + Secure Delete
- Backups: Overwritten within the next scheduled backup rotation (max 7 days after deletion)
- Audit trail: Deletion event logged permanently (the fact of deletion, not the deleted data)

---

## 10. Your Rights as a Data Principal

Under the **DPDP Act 2023**, patients and users have the following rights:

| Right | How to Exercise | Response Time |
|---|---|---|
| **Right to Information** — Know what data we hold | WhatsApp to support or email privacy@healthcarewale.in | 7 business days |
| **Right to Correction** — Fix inaccurate personal data | In-app profile edit or support request | 3 business days |
| **Right to Erasure** — Delete your account and data | Written request to privacy@healthcarewale.in | 30 days |
| **Right to Grievance Redressal** — Complain about data handling | Grievance Officer contact (see Section 16) | 30 days |
| **Right to Nominate** — Nominate another person to exercise rights on your behalf in case of death/incapacity | Written nomination submitted to platform | 7 business days |

**Under GDPR (EU users):**
- Right to Access (Art. 15)
- Right to Rectification (Art. 16)
- Right to Erasure / "Right to be Forgotten" (Art. 17)
- Right to Restrict Processing (Art. 18)
- Right to Data Portability (Art. 20)
- Right to Object (Art. 21)
- Right not to be subject to automated decision-making (Art. 22)

**Under HIPAA (US users):**
- Right to access PHI
- Right to request amendment
- Right to accounting of disclosures
- Right to request restrictions
- Right to receive confidential communications

---

## 11. Security Measures

### 11.1 Technical Safeguards
- **Encryption at rest:** AES-256 for all database records and S3 stored files
- **Encryption in transit:** TLS 1.3 minimum for all API communications
- **Database:** Row-Level Security (RLS) in PostgreSQL enforcing tenant isolation
- **Access control:** Role-Based Access Control (RBAC) with least-privilege principle
- **Authentication:** JWT with 30-minute expiry + refresh tokens; 2FA mandatory for admin accounts
- **Network:** AWS VPC with private subnets; no direct public internet access to databases
- **API gateway:** Rate limiting (100 req/min per IP), DDoS protection via Cloudflare WAF
- **Secrets:** All API keys and credentials stored in AWS Secrets Manager (never in code)
- **Vulnerability scanning:** Automated SAST/DAST scanning in CI/CD pipeline (GitHub Actions)

### 11.2 Organizational Safeguards
- Background verification for all employees with access to patient data
- Mandatory data privacy training for all staff (annual + on-hire)
- Signed Non-Disclosure Agreements (NDAs) for all staff and contractors
- Data access on need-to-know basis only, with full audit logging
- Quarterly internal security reviews; annual external penetration test (Phase 2+)

### 11.3 Physical Safeguards
- All production infrastructure is cloud-hosted (AWS) — no on-premise servers
- Offices follow clean-desk policy for any printed documents containing patient data
- No patient data stored on personal employee devices without MDM (Mobile Device Management) controls

---

## 12. Cookies & Tracking Technologies

### 12.1 Web Dashboard & PWA
| Cookie Type | Purpose | Duration | Can Opt Out? |
|---|---|---|---|
| Strictly Necessary | Session management, CSRF protection | Session | No |
| Functional | Language preference, dashboard layout | 1 year | No |
| Analytics | Usage tracking via Mixpanel (anonymized) | 90 days | Yes |
| Marketing | Not used on patient-facing pages | N/A | N/A |

### 12.2 Mobile App
- Firebase Analytics: Crash reporting and app usage (anonymized, no health data)
- No third-party advertising SDKs integrated in mobile app
- No cross-app tracking (no IDFA/GAID used for advertising purposes)

---

## 13. Children's Privacy

- The HealthcareWale platform is **not intended for direct use by persons under 18 years of age**
- Minors' health records may be managed by a parent or legal guardian as an authorized caregiver under a family account
- The caregiver assumes full responsibility for consent on behalf of the minor
- If we discover we have inadvertently collected personal data from an unaccompanied minor, we will delete it within 72 hours of discovery
- Under DPDP Act 2023, processing of children's data requires verifiable parental consent. HealthcareWale will implement age-gating mechanisms before onboarding minor patients directly.

---

## 14. AI & Automated Decision-Making

### 14.1 Nature of AI Decisions

The HealthcareWale AI system makes the following **administrative** automated decisions:
- Doctor-patient appointment slot matching (based on availability and specialty)
- Queue position calculation and estimated wait time
- Inventory reorder quantity suggestions
- Appointment reminder scheduling

**The AI does NOT make:**
- Medical diagnoses
- Treatment recommendations
- Drug prescribing decisions
- Triage urgency classifications that override clinical judgment

### 14.2 Human Override

All AI outputs in clinical contexts are subject to human review:
- Appointment matching: Patient can override and select a different slot
- Triage pre-screening: Doctor always makes final clinical decision
- PMJAY claim coding: Hospital billing staff reviews before submission

### 14.3 AI and Patient Data

- Patient conversations with AI voice agents are used for: intent detection, booking completion, reminder delivery
- Voice audio transcripts are stored for 30 days for quality assurance
- **Patient data is NEVER used to train or fine-tune any AI/LLM model** without explicit, separate, opt-in consent
- De-identified, aggregated interaction data may be used for system performance improvement (e.g., improving Hindi intent detection accuracy) — this does not involve personal health data

See the full **AI Ethics, Safety & Transparency Policy (HW-AI-001)** and **AI Data Minimization & Model Training Policy (HW-AI-002)** for complete details.

---

## 15. Consent Management

### 15.1 How We Obtain Consent

At registration, patients provide:
1. **Primary consent:** Processing of personal and health data for healthcare service delivery
2. **Communication consent:** WhatsApp messages, SMS, and AI voice calls for appointment-related communication
3. **Optional consents (separate checkboxes):**
   - Health education content and tips
   - Chronic disease management program enrollment
   - Anonymized data contribution for health analytics (pharma company reports)
   - Marketing communications (entirely optional)

### 15.2 Consent Records

- All consent events are logged with: timestamp, patient ID, consent type, version of policy at time of consent, channel (app/WhatsApp/voice)
- Consent records are retained for the duration of the account + 3 years after closure
- Consent is version-controlled — if policy changes materially, re-consent is obtained before processing continues

### 15.3 Withdrawing Consent

- Patients can withdraw any non-essential consent at any time via: in-app settings, WhatsApp "STOP" command, or email to privacy@healthcarewale.in
- Withdrawal of consent for core service communication may limit platform functionality
- Withdrawal does not affect lawfulness of processing conducted prior to withdrawal
- Withdrawing consent for health data processing will result in account deactivation within 30 days

---

## 16. Grievance Redressal

### 16.1 Grievance Officer (DPDP Act S.13)

**Name:** [Grievance Officer Name]  
**Designation:** Data Protection & Grievance Officer  
**Organization:** HealthcareWale Technologies Pvt. Ltd.  
**Email:** grievance@healthcarewale.in  
**Phone:** [Designated Grievance Phone Number]  
**Address:** [Registered Office Address], Mohali, Punjab, India  
**Working Hours:** Monday–Friday, 10:00 AM – 6:00 PM IST

**Response Commitment:** Acknowledgment within 48 hours; resolution within 30 days.

### 16.2 Escalation

If unsatisfied with grievance resolution:
- **India:** File a complaint with the **Data Protection Board of India** (once constituted under DPDP Act)
- **EU users:** Lodge a complaint with your local **Data Protection Authority (DPA)**
- **US users:** Contact the **U.S. Department of Health and Human Services (HHS) Office for Civil Rights**

---

## 17. Changes to This Policy

We may update this Policy from time to time. For **material changes** (changes to data types collected, new third-party sharing, or new processing purposes):
- We will notify all registered users via WhatsApp and email (where available) at least **30 days before** the change takes effect
- Continued use of the platform after the effective date constitutes acceptance of the updated Policy
- Where changes require fresh consent under DPDP Act, we will obtain it before processing under new terms

**Policy Version History:**
| Version | Date | Summary of Changes |
|---|---|---|
| 1.0 | May 2026 | Initial policy — platform launch |

---

*This Policy is governed by the laws of India. Disputes shall be subject to the jurisdiction of courts in Mohali, Punjab.*

*HealthcareWale Technologies Pvt. Ltd. | privacy@healthcarewale.in | grievance@healthcarewale.in*
