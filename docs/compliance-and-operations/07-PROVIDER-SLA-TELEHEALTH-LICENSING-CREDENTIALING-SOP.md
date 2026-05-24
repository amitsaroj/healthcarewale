# 🏥 HealthcareWale — Medical Practitioner Service Level Agreement (SLA)
> **Document ID:** HW-SLA-001 | **Version:** 1.0 | **Effective Date:** [Insert Date]

---

## 1. PARTIES

**Platform Operator:** HealthcareWale Technologies Private Limited ("HealthcareWale")  
**Provider:** Licensed Medical Practitioner / Clinic / Hospital ("Provider")  

This SLA governs the service standards, obligations, and payout terms for all Providers onboarded on the HealthcareWale platform.

---

## 2. PROVIDER OBLIGATIONS

### 2.1 Availability & Scheduling
| Obligation | Standard |
|---|---|
| Schedule accuracy | Provider must keep availability calendar updated within 24 hours of any change |
| Appointment acceptance | Booked appointments are auto-confirmed — Provider may not cancel within 2 hours of appointment time except in genuine emergencies |
| Last-minute cancellations | Maximum 2 last-minute cancellations per month without penalty; 3rd+ triggers a ₹200/cancellation platform fee |
| Response to patient calls | For in-clinic appointments: patient must be attended within 15 minutes of scheduled time; virtual queue managed accordingly |
| Teleconsultation punctuality | Video/audio call initiated within 5 minutes of scheduled time |

### 2.2 Digital Prescription Standards
- All prescriptions issued via the platform must: include patient name, date, diagnosis (ICD-10 code), medicine name (generic preferred), dose, frequency, duration, and doctor's name + registration number + digital signature
- Prescriptions must be generated within 30 minutes of consultation completion
- Schedule H drugs: Prescription must be explicitly marked with drug schedule; platform auto-flags for verification

### 2.3 Platform Conduct
- No solicitation of patients for off-platform consultations to avoid platform fees (results in immediate account suspension)
- No issuance of prescriptions without a genuine consultation
- No certification of fitness, disability, or insurance claims for patients not personally consulted
- Maintain professional conduct consistent with NMC Code of Medical Ethics Regulations, 2002

### 2.4 Data Handling by Provider
- Providers must maintain patient data confidentiality within their own systems
- Providers may not use patient contact information obtained via HealthcareWale for direct marketing outside the platform
- Providers are responsible for securing any exported patient data (EMR exports, PDF prescriptions)

---

## 3. HEALTHCAREWALE OBLIGATIONS TO PROVIDERS

| Obligation | Standard |
|---|---|
| Platform uptime | 99.9% monthly SLA (8.7 hours maximum downtime/year) |
| Payment settlement | Within 7 business days after month-end reconciliation |
| Dispute resolution | Patient complaints regarding a Provider responded to within 5 business days |
| Technical support | Platform issues affecting consultations resolved within 4 hours (critical) |
| Data protection | Patient data protected per Privacy Policy HW-PRIV-001 |
| Transparent analytics | Provider receives monthly analytics report (consultation count, no-show rate, ratings) |

---

## 4. PAYOUT STRUCTURE

### 4.1 Consultation Fee Distribution
| Fee Component | Patient Pays | Doctor Receives | HealthcareWale Platform Fee |
|---|---|---|---|
| Online appointment booking | 100% | 85% | 15% |
| Teleconsultation | 100% | 80% | 20% |
| Walk-in registered via platform | 100% | 90% | 10% |
| PMJAY / Swasthya Sathi claim (govt-paid) | Government pays | 95% of approved amount | 5% |

### 4.2 Payout Deductions
- Late cancellation fee: ₹200/cancellation (3+ per month)
- Verified patient complaint resolution: Cost of remedy (max ₹500/complaint) deducted if Provider at fault
- Platform fee on commissions per Section 4.1

### 4.3 Payment Method
- Primary: Direct bank transfer (NEFT/IMPS) or UPI
- Provider must maintain valid bank details with 30 days' notice for any change
- GST invoicing: Provider must issue GST invoice for professional services (if GST registered)

---

## 5. SUSPENSION & TERMINATION

| Trigger | Action |
|---|---|
| NMC/State Council registration expired/cancelled | Immediate suspension pending re-verification |
| 3+ verified patient complaints in 60 days | Account review; 15-day improvement notice |
| Off-platform solicitation confirmed | Immediate suspension; 30-day investigation |
| Prescription fraud confirmed | Permanent termination; regulatory reporting to NMC |
| Data breach caused by Provider | Immediate suspension; liability per contract |
| Voluntary exit | 30-day notice required; in-progress appointments fulfilled or transferred |

---
---

# 🌐 HealthcareWale — Cross-Jurisdiction Telehealth Licensing Policy
> **Document ID:** HW-LEGAL-003 | **Version:** 1.0 | **Effective Date:** [Insert Date]

---

## 1. PURPOSE

This policy ensures that all teleconsultations facilitated through HealthcareWale comply with the territorial licensing requirements of the Indian Medical Council Act, State Medical Council regulations, and the Telemedicine Practice Guidelines 2020.

---

## 2. INDIAN TELEHEALTH LEGAL FRAMEWORK

### 2.1 Telemedicine Practice Guidelines 2020

Issued by the Board of Governors in supersession of MCI, these guidelines:
- Permit Registered Medical Practitioners (RMPs) to provide telemedicine services
- Define a first consultation via telemedicine as permissible but with medication restrictions
- Prohibit prescription of Schedule X drugs via telemedicine
- Require follow-up prescriptions to be based on prior in-person consultation records
- Apply to ALL forms of telemedicine — video, audio, text, WhatsApp

### 2.2 State Medical Council Jurisdiction

In India, medical registration is state-specific. An RMP registered with the Maharashtra Medical Council is legally licensed to practice in Maharashtra. Practicing medicine in another state without that state's council registration is legally ambiguous under the Indian Medical Council Act, 1956.

**Current Legal Position (as of May 2026):**
- NMC Act 2019 established a national medical register — doctors with NMC registration have a stronger cross-state practice basis
- State boundaries for telemedicine practice remain a grey area — pending definitive NMC guidance
- HealthcareWale's position: Follow the most conservative interpretation until definitive guidance is issued

---

## 3. TERRITORIAL RESTRICTIONS ON PLATFORM

### 3.1 Phase 1 (UP + West Bengal)

In Phase 1, HealthcareWale operates only in Uttar Pradesh and West Bengal. All doctors onboarded must hold:
- NMC registration (national) OR
- UP Medical Council registration (for UP-based practice) OR
- West Bengal Medical Council registration (for WB-based practice)

Doctors registered with southern or western state councils wishing to conduct teleconsultations with UP/WB patients must:
- Hold NMC national registration, OR
- Obtain registration with the relevant state council, OR
- Be flagged in the system as "In-State Consultation Only" — restricted to patients in their home state

### 3.2 Teleconsultation Routing Logic

```
Patient in UP books teleconsultation
         │
         ▼
System checks doctor's registration state(s)
         │
    ┌────┴──────────────────────────────┐
    ▼                                  ▼
Doctor holds NMC/UP registration    Doctor holds only another
                                    state's registration
    │                                  │
    ▼                                  ▼
Booking permitted                  Booking blocked
                                   "This doctor is not currently
                                   available for teleconsultation
                                   in your state"
```

### 3.3 International Teleconsultation (Future)

For international patients (e.g., Bangladesh nationals seeking WB doctors — medical tourism use case):
- Indian RMPs are bound by Indian law; foreign medical regulations are not HealthcareWale's responsibility
- International patients are informed: "The consultation follows Indian Telemedicine Guidelines. Prescriptions issued may not be valid in your country. Please consult a local licensed physician for treatment."
- No prescription for Schedule H, H1, or X drugs for international patients via teleconsultation

---

## 4. EMERGENCY EXCEPTION

Telemedicine restrictions may be relaxed in declared public health emergencies (national or state level). HealthcareWale will implement emergency mode configurations per government notification within 48 hours of such declaration.

---
---

# 🔍 HealthcareWale — Provider Verification & Credentialing SOP
> **Document ID:** HW-SOP-001 | **Version:** 1.0 | **Effective Date:** [Insert Date]

---

## 1. PURPOSE

This Standard Operating Procedure defines the step-by-step process for verifying and credentialing medical practitioners, pharmacists, and healthcare facilities before account activation on HealthcareWale.

---

## 2. DOCTOR VERIFICATION PROCESS

### Step 1: Application Submission
Doctor completes online onboarding form:
- Full name (as on registration certificate)
- NMC / State Medical Council registration number
- Primary medical degree (MBBS/MD/MS/BDS/etc.)
- Specialization
- Practice state and city
- Clinic/hospital name and address
- Document uploads: Registration certificate (PDF/image), Degree certificate, Identity proof (Aadhaar/PAN)

### Step 2: Automated HPR Verification (Within 1 hour)

```
System calls HPR API:
GET /v1/hpr/search?regNumber=[REG_NO]&council=[COUNCIL_CODE]
         │
    ┌────┴──────────────────────────────┐
    ▼                                  ▼
HPR record found — name matches    HPR record not found /
degree verified — registration      name mismatch
active                                │
    │                                 ▼
    ▼                             Flag for manual review
Auto-approve HPR check             Email doctor: "Please resubmit
Log: HPR verified ✅               with correct details"
```

### Step 3: Manual Document Review (Within 24 hours)
Admin team reviews:
- Registration certificate matches HPR data (name, reg number, council, expiry)
- Degree certificate matches claimed qualification
- Identity document matches name on registration
- Clinic address verified against Google Maps / local directory

### Step 4: CIBIL / Blacklist Check (For Teleconsultation Providers)
- Check NMC/State Council public deregistration/misconduct lists
- Check HealthcareWale internal blacklist (previous violations)

### Step 5: Account Activation
- If all checks pass: Account activated within 48 hours of application
- Doctor receives WhatsApp: "Your HealthcareWale provider account is verified and active."
- Doctor profile set to visible in booking system

### Step 6: Annual Re-verification
- 30 days before registration expiry: Doctor notified to submit renewal documents
- HPR re-verification run annually for all active doctors
- Failed re-verification: Account suspended until documents updated

---

## 3. PHARMACY VERIFICATION PROCESS

| Step | Check | Source | Timeline |
|---|---|---|---|
| 1 | Drug License (retail/wholesale) | State Drug Control Dept database | Automated where API available; manual otherwise |
| 2 | GST registration | GSTN API | Automated |
| 3 | Pharmacist registration | State Pharmacy Council | Manual check |
| 4 | Physical address verification | Google Maps + field agent (Tier-2 cities) | Within 72 hours |
| 5 | Owner identity (Aadhaar/PAN) | Document review | Within 24 hours |

### Pharmacy Verification Timeline: 72 hours maximum

---

## 4. HOSPITAL / NURSING HOME VERIFICATION

Additional checks beyond standard:
- Clinical Establishments Act registration (state-level)
- NABH accreditation (if claimed — verified via NABH portal)
- PMJAY empanelment status (NHA provider portal)
- Bed count and ICU/emergency capacity (for accurate service listing)
- Medical superintendent's NMC registration

**Timeline:** 5 business days (larger hospitals may require field verification)

---

## 5. VERIFICATION FAILURE HANDLING

| Failure Type | Action | Doctor/Pharmacy Notification |
|---|---|---|
| HPR not found | Manual review initiated | Email + WhatsApp within 24 hours |
| Registration expired | Account suspended | 7-day cure period |
| Document mismatch | Rejected — resubmission invited | Detailed reasons provided |
| Blacklisted registration | Permanent rejection | Legal notice if fraudulent attempt |
| Drug license lapsed | Account suspended | 15-day cure period |

---

## 6. VERIFICATION AUDIT TRAIL

Every verification step is logged:
- Verifier ID (staff who manually approved)
- Timestamp
- Documents reviewed (hash stored — not documents themselves)
- HPR/API response stored
- Approval/rejection reason

Audit trail retained for 5 years per regulatory requirements.

---

*Provider SLA, Telehealth Licensing Policy, and Credentialing SOP v1.0 — May 2026*
