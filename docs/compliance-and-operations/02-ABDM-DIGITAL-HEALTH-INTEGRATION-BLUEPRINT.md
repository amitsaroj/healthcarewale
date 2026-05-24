# 🏛️ HealthcareWale — ABDM & Digital Health Stack Integration Blueprint
> **Document ID:** HW-ABDM-001  
> **Version:** 1.0 | **Effective Date:** [Insert Date]  
> **Compliance Frameworks:** ABDM Health Data Management Policy · NHA FHIR Implementation Guide · PMJAY NHA API Specs · Swasthya Sathi (WB) API Guidelines  
> **Document Owner:** CTO / Technical Lead — HealthcareWale Technologies Pvt. Ltd.

---

## 1. EXECUTIVE OVERVIEW

The Ayushman Bharat Digital Mission (ABDM), launched by the Government of India under the National Health Authority (NHA), establishes the foundational digital health infrastructure for India. HealthcareWale's integration with ABDM is not optional — it is the gateway to:

- PMJAY insurance claim filing (UP: 5.38 crore beneficiaries)
- ABHA-linked health record interoperability
- West Bengal's Swasthya Sathi scheme (joined PMJAY May 2026)
- Positioning HealthcareWale as a government-compliant health platform eligible for NHM tenders and state government contracts

This blueprint defines the complete technical and operational framework for ABDM integration.

---

## 2. ABDM BUILDING BLOCKS

### 2.1 Core ABDM Components

```
┌─────────────────────────────────────────────────────────────────────┐
│                      ABDM DIGITAL HEALTH STACK                      │
├──────────────────┬──────────────────┬───────────────────────────────┤
│   ABHA           │   HFR            │   HPR                         │
│   (Health ID)    │   (Health        │   (Healthcare                 │
│                  │   Facility       │   Professionals               │
│   14-digit       │   Registry)      │   Registry)                   │
│   unique ID      │                  │                               │
│   for patients   │   Clinics,       │   Doctors, nurses,            │
│                  │   hospitals,     │   pharmacists —               │
│                  │   pharmacies     │   verified credentials        │
├──────────────────┴──────────────────┴───────────────────────────────┤
│   HEALTH LOCKER (PHR App / HIU/HIP Model)                          │
│   Stores patient health records in FHIR R4 format                  │
│   Patient controls consent for record access                       │
├─────────────────────────────────────────────────────────────────────┤
│   UHI (Unified Health Interface)                                   │
│   Open protocol for doctor discovery and appointment booking       │
├─────────────────────────────────────────────────────────────────────┤
│   CLAIMS (NHA Gateway)                                             │
│   PMJAY pre-authorization and claim submission API                 │
└─────────────────────────────────────────────────────────────────────┘
```

### 2.2 HealthcareWale's Role in ABDM Ecosystem

| ABDM Role | HealthcareWale Position | Description |
|---|---|---|
| **Health Information Provider (HIP)** | ✅ Yes | Clinics and hospitals on our platform generate and provide health records |
| **Health Information User (HIU)** | ✅ Yes | Doctors on our platform can request to view patient records from ABDM locker |
| **PHR App** | 🔄 Phase 2 | Patient-facing health record viewer linked to ABHA |
| **UHI End User Application (EUA)** | 🔄 Phase 2 | Enable doctor discovery via UHI protocol |
| **PMJAY Empanelment Support** | ✅ Phase 1 | Help hospitals file PMJAY claims via NHA API |

---

## 3. ABHA ID INTEGRATION

### 3.1 ABHA ID Creation Flow

```
Patient opens HealthcareWale app → "Create ABHA ID"
         │
         ▼
System calls ABDM API: POST /v1/registration/aadhaar/generateOtp
(Aadhaar number entered by patient — not stored by HealthcareWale)
         │
         ▼
OTP received on Aadhaar-linked mobile
         │
         ▼
System calls: POST /v1/registration/aadhaar/verifyOTP
         │
         ▼
ABHA ID generated: 14-digit number (e.g., 91-1234-5678-9012)
         │
         ▼
HealthcareWale stores ABHA ID in patient profile (PostgreSQL, encrypted)
         │
         ▼
Patient can now link existing health records from ABDM locker
```

### 3.2 ABHA ID Linking Flow (Existing ID)

```
Patient has existing ABHA ID → Enter in app
         │
         ▼
System calls: POST /v1/search/authModes (find linked mobile/Aadhaar)
         │
         ▼
OTP verification on linked mobile
         │
         ▼
ABHA profile fetched: name, DOB, gender, linked health records
         │
         ▼
Patient profile in HealthcareWale linked to ABHA
         │
         ▼
Patient grants consent for HealthcareWale to access/share FHIR records
```

### 3.3 Technical Specifications — ABHA API

| Parameter | Value |
|---|---|
| Base URL (Production) | `https://healthidsbx.abdm.gov.in/api` |
| Base URL (Sandbox) | `https://healthidsbx.abdm.gov.in/api` |
| Authentication | Client ID + Client Secret (OAuth 2.0 Bearer token) |
| Token expiry | 30 minutes |
| Rate limit | 100 requests/minute per client |
| Data format | JSON |
| FHIR Version | R4 (for health records) |
| Registration | abdm.gov.in/developers |

---

## 4. HEALTH INFORMATION PROVIDER (HIP) IMPLEMENTATION

### 4.1 HIP Architecture

As a HIP, HealthcareWale must:
1. Store patient health records in FHIR R4 format
2. Register as HIP on ABDM Health Facility Registry (HFR)
3. Implement consent-based health record sharing via ABDM gateway
4. Receive and respond to health record fetch requests within defined SLA

### 4.2 FHIR R4 Resources Implemented

| FHIR Resource | HealthcareWale Usage |
|---|---|
| `Patient` | Patient demographic record linked to ABHA ID |
| `Practitioner` | Doctor profile linked to HPR registration |
| `Organization` | Clinic/hospital profile linked to HFR |
| `Appointment` | Appointment record with status, date, specialty |
| `Encounter` | OPD/IPD visit record |
| `Condition` | Diagnosis (mapped to ICD-10) |
| `MedicationRequest` | Digital prescription from doctor |
| `DiagnosticReport` | Lab test results |
| `Observation` | Patient vitals (BP, glucose, weight) |
| `DocumentReference` | PDF prescriptions, discharge summaries |
| `Claim` | PMJAY insurance claim record |
| `Coverage` | Patient insurance coverage (PMJAY/Swasthya Sathi) |

### 4.3 Consent Framework (HIP Side)

```
Doctor requests patient's health records
         │
         ▼
HealthcareWale (HIU) sends consent request to ABDM gateway
         │
         ▼
Patient receives notification (WhatsApp + ABDM app)
"Dr. [Name] at [Clinic] is requesting access to your health records.
Purpose: Treatment | Duration: This visit only | [Allow] [Deny]"
         │
         ▼
Patient grants consent → consent artefact generated by ABDM
         │
         ▼
HealthcareWale fetches FHIR records from HIPs holding patient data
         │
         ▼
Records displayed to doctor during consultation
         │
         ▼
Consent artefact stored in audit log
Records deleted from HealthcareWale server after consultation window
```

---

## 5. PMJAY INTEGRATION (NHA CLAIMS API)

### 5.1 PMJAY Eligibility Check Flow

```
Patient arrives at hospital
         │
         ▼
Staff enters: Patient name + Aadhaar last 4 digits OR PMJAY card number
         │
         ▼
API call: NHA eligibility check endpoint
         │
    ┌────┴────────────────┐
    ▼                     ▼
Eligible (card active)  Not eligible
    │                     │
    ▼                     ▼
Display: Patient name,  Offer: Self-pay /
package entitlement,    Other insurance
card validity date
    │
    ▼
Proceed with admission under PMJAY
```

### 5.2 PMJAY Claim Filing Flow

```
Patient discharge initiated
         │
         ▼
System pulls admission data:
- Patient ABHA ID / PMJAY card
- Admitting doctor (HPR registration)
- Diagnosis codes (ICD-10)
- Procedures performed
- Medicines administered
- Ward/bed/duration
         │
         ▼
AI maps procedures to Health Benefit Package (HBP) codes
         │
         ▼
Billing staff reviews mapping + approves
         │
         ▼
Pre-authorization claim submitted (if not done at admission)
         │
         ▼
Final claim submitted via NHA API:
POST /v1/claims/submit
{
  "claimId": "HW-CLM-2026-XXXXX",
  "hospitalHFR": "IN2026XXXXXXXX",
  "patientABHA": "91-XXXX-XXXX-XXXX",
  "pmjayCardId": "XXXXXXXXXXXX",
  "hbpCode": "P12345",
  "icd10Codes": ["E11.9", "I10"],
  "claimAmount": 45000,
  "documents": [base64_discharge_summary, base64_bills, ...]
}
         │
         ▼
Claim status tracked:
Submitted → Under Review → Approved → Payment Initiated → Settled
         │
         ▼
Settlement credited to hospital's linked bank account by NHA
```

### 5.3 PMJAY API Specifications

| Parameter | Value |
|---|---|
| NHA Sandbox URL | `https://dev.nha.gov.in/nha/api` |
| NHA Production URL | `https://api.nha.gov.in` |
| Authentication | RSA-based digital signature + client certificate |
| Claim format | FHIR ClaimRequest resource |
| Response time SLA | 48 hours for pre-auth; 15 days for final claim |
| Rejection rate (industry avg) | 18–22% — HealthcareWale AI pre-validation targets <8% |

---

## 6. WEST BENGAL SWASTHYA SATHI INTEGRATION

### 6.1 Background

West Bengal joined PMJAY in May 2026 but maintains its own Swasthya Sathi scheme with a separate API gateway operated by the WB Health & Family Welfare Department. HealthcareWale must support BOTH schemes for WB-based hospital customers.

### 6.2 Swasthya Sathi Integration Points

| Feature | Swasthya Sathi | PMJAY (NHA) |
|---|---|---|
| Eligibility check | WB SS API | NHA API |
| Pre-authorization | WB SS portal | NHA portal |
| Claim submission | WB SS API | NHA API |
| Card format | SS card (plastic/digital) | PM-JAY card (QR-based) |
| Coverage limit | ₹5 Lakh/family/year | ₹5 Lakh/family/year |
| State contribution | WB state government | 60% Centre + 40% State |
| API registration | wbhealth.gov.in | nha.gov.in |

### 6.3 Dual-Scheme Patient Handling

```
WB patient arrives at hospital
         │
         ▼
System checks BOTH schemes simultaneously (parallel API calls)
         │
    ┌────┴──────────────────┐
    ▼                       ▼
PMJAY eligible         Swasthya Sathi eligible
    │                       │
    ▼                       ▼
Hospital selects       Hospital selects
preferred scheme       preferred scheme
based on HBP coverage  based on procedure coverage
```

---

## 7. HEALTH PROFESSIONAL REGISTRY (HPR) INTEGRATION

All doctors onboarded on HealthcareWale must be verified against HPR:

```
Doctor submits NMC/State Council registration number
         │
         ▼
API call: HPR verification endpoint
GET /v1/hpr/search?regNumber=XXXX&council=NMC
         │
         ▼
Response: Doctor name, qualifications, registration status, expiry
         │
    ┌────┴──────────────┐
    ▼                   ▼
Verified Active      Not found / Expired
    │                   │
    ▼                   ▼
Account activated    Account blocked — manual review
Auto-linked to HPR   Doctor notified — 7-day remedy period
profile
```

---

## 8. HEALTH FACILITY REGISTRY (HFR) INTEGRATION

All clinics and hospitals onboarded on HealthcareWale must register with HFR:

**HFR Registration Data Required:**
- Facility name, type (clinic/hospital/pharmacy), address
- Ownership type (private/govt/trust)
- Clinical services offered (mapped to ABDM service codes)
- Licensing details (drug license, clinical establishment registration)
- Facility In-charge name and contact (must be HPR-registered practitioner)

**HFR ID Format:** `IN{Year}{State Code}{Sequence Number}` (e.g., `IN2026UP00123456`)

---

## 9. UNIFIED HEALTH INTERFACE (UHI) — PHASE 2

The UHI enables standardized, cross-platform doctor discovery and appointment booking. HealthcareWale will register as a UHI End User Application (EUA) in Phase 2:

- Patients searching "cardiologist near Lucknow" on any UHI-compliant app will find doctors on HealthcareWale
- HealthcareWale doctors can receive bookings from patients on other UHI apps
- Appointment data flows in FHIR Appointment resource format
- Commission and fee settlement follow UHI network rules

---

## 10. COMPLIANCE OBLIGATIONS & TIMELINE

| ABDM Obligation | Deadline | Status |
|---|---|---|
| Register on ABDM Developer Portal | Pre-launch | 🔲 Pending |
| Sandbox testing (ABHA creation, linking) | Pre-launch | 🔲 Pending |
| HPR integration for doctor verification | Pre-launch | 🔲 Pending |
| HFR registration support for onboarded facilities | Month 2 | 🔲 Pending |
| FHIR R4 compliant health record storage | Month 3 | 🔲 Pending |
| HIP certification from NHA | Month 4 | 🔲 Pending |
| PMJAY NHA API integration (sandbox) | Month 3 | 🔲 Pending |
| PMJAY NHA API integration (production) | Month 5 | 🔲 Pending |
| Swasthya Sathi API integration | Month 6 | 🔲 Pending |
| UHI EUA registration | Phase 2 | 🔲 Pending |
| Annual ABDM compliance audit | Ongoing | 🔲 Pending |

---

*HealthcareWale ABDM Integration Blueprint v1.0 — May 2026*  
*All API URLs and specifications subject to change per NHA updates. Monitor abdm.gov.in/developers for latest specs.*
