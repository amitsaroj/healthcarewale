# ⚖️ HealthcareWale — Software as Medical Device (SaMD) Exclusion Statement
> **Document ID:** HW-SAMD-001 | **Version:** 1.0 | **Effective Date:** [Insert Date]  
> **Legal Frameworks:** FDA SaMD Final Guidance (2014) · IMDRF SaMD Framework · CDSCO MDR 2017 · EU MDR 2017/745

---

## 1. PURPOSE

This document establishes HealthcareWale's position with respect to Software as a Medical Device (SaMD) regulation globally. It provides legal clarity that HealthcareWale's platform, as currently designed and deployed, does NOT meet the definition of a medical device under applicable regulatory frameworks and is therefore NOT subject to medical device pre-market clearance, 510(k) notification, CE marking, or CDSCO medical device registration.

---

## 2. REGULATORY DEFINITIONS

### 2.1 FDA Definition (United States)
Under the FDA's Final Guidance on SaMD (2014), software is a medical device when it is "intended to be used for one or more medical purposes that perform these purposes without being part of a hardware medical device." Medical purposes include: diagnosis, cure, mitigation, treatment, or prevention of disease.

### 2.2 IMDRF Definition (International)
The International Medical Device Regulators Forum defines SaMD as "software intended to be used for one or more medical purposes that perform these purposes without being part of a hardware medical device."

### 2.3 CDSCO / India Medical Devices Rules 2017
Under MDR 2017, a medical device includes any instrument, apparatus, appliance, software, or system "intended to be used, alone or in combination, for human beings, for one or more of the specific medical purpose(s) of: diagnosis, prevention, monitoring, prediction, prognosis, treatment or alleviation of disease."

---

## 3. HEALTHCAREWALE FEATURE ANALYSIS

The following table analyzes each HealthcareWale feature against SaMD classification criteria:

| Feature | Does It Diagnose? | Does It Treat? | Does It Prescribe? | SaMD Classification | Rationale |
|---|---|---|---|---|---|
| AI Appointment Booking Voice Agent | ❌ No | ❌ No | ❌ No | **NOT SaMD** | Administrative scheduling only |
| WhatsApp Appointment Bot | ❌ No | ❌ No | ❌ No | **NOT SaMD** | Administrative booking workflow |
| Virtual Waiting Room / Token System | ❌ No | ❌ No | ❌ No | **NOT SaMD** | Queue management software |
| Appointment Reminders (WhatsApp/SMS/Voice) | ❌ No | ❌ No | ❌ No | **NOT SaMD** | Notification system |
| Pharmacy Inventory Management | ❌ No | ❌ No | ❌ No | **NOT SaMD** | Stock management software |
| GST Billing & Invoice Generation | ❌ No | ❌ No | ❌ No | **NOT SaMD** | Accounting/billing software |
| Prescription OCR (Medicine Name Extraction) | ❌ No | ❌ No | ❌ No | **NOT SaMD** | Text digitization only; doctor already prescribed |
| Supplier Auto-Ordering | ❌ No | ❌ No | ❌ No | **NOT SaMD** | Supply chain automation |
| PMJAY Claim Filing Assistance | ❌ No | ❌ No | ❌ No | **NOT SaMD** | Administrative claims processing |
| ICD-10 Code Suggestion | ⚠️ **MONITORED** | ❌ No | ❌ No | **BORDERLINE — Administrative** | Codes suggested for billing only; human doctor/staff approval mandatory before use; diagnosis already made by doctor |
| Inventory Demand Forecasting | ❌ No | ❌ No | ❌ No | **NOT SaMD** | Business analytics |
| EMR Record Storage | ❌ No | ❌ No | ❌ No | **NOT SaMD** | Data storage/retrieval only |
| AI Pre-Screening (Chief Complaint Collection) | ⚠️ **MONITORED** | ❌ No | ❌ No | **Designed as NOT SaMD** | Collects stated complaint for routing; does not analyze, score, or assess medically |
| Teleconsultation Platform | ❌ No | ❌ No | ❌ No | **NOT SaMD** | Communication infrastructure only; clinical decisions made by licensed doctor |
| Lab Report Storage/Delivery | ❌ No | ❌ No | ❌ No | **NOT SaMD** | Document management and delivery |

---

## 4. DESIGN CONSTRAINTS MAINTAINING NON-SaMD STATUS

HealthcareWale maintains the following product design constraints to ensure no feature crosses into SaMD territory:

### 4.1 No Clinical Decision Support
The platform does not compute, score, or rank clinical urgency, severity, or risk. The AI does not tell patients which condition they may have, which treatment is recommended, or what medication they should take.

### 4.2 Mandatory Human Clinical Authority
Every feature that touches clinical data requires human professional approval:
- ICD-10 codes: Reviewed and approved by hospital billing staff and doctor before claim submission
- Discharge summary AI draft: Requires doctor digital signature before finalization
- Pre-screening chief complaint: Passed directly to doctor — no clinical interpretation by platform

### 4.3 Explicit Non-Diagnostic Language Policy
All AI outputs are reviewed against a medical keyword filter that blocks any phrasing that could constitute a diagnosis, prognosis, or treatment recommendation (see AI Ethics Policy HW-AI-001, Section 5).

### 4.4 Emergency Scope Exclusion
The platform explicitly and categorically excludes emergency medical response functionality. Emergency keyword detection triggers an immediate redirect to 108 — not platform-based triage.

---

## 5. FEATURES REQUIRING ONGOING REGULATORY MONITORING

The following features, while currently designed as non-SaMD, require ongoing regulatory monitoring as they scale:

| Feature | Risk Factor | Monitoring Action |
|---|---|---|
| ICD-10 Code Suggestion | If used without human review, could influence clinical coding | Mandatory human approval lock enforced in code; audit quarterly |
| AI Pre-Screening | If expanded to include severity scoring, would become SaMD | Product roadmap review before any expansion; legal opinion required |
| Patient Vital Anomaly Alerts | Alerting doctor to abnormal BP/glucose could be interpreted as diagnostic | Alert framed as "reading outside normal range — please review" only; no clinical interpretation |

---

## 6. LEGAL DECLARATION

HealthcareWale Technologies Private Limited hereby declares that, as of the effective date of this document:

1. No feature of the HealthcareWale platform is designed, intended, or marketed for the purpose of medical diagnosis, treatment, cure, mitigation, or prevention of disease in human beings.

2. The platform is designed and operated as a healthcare **operations and administrative management** SaaS platform, comparable in regulatory classification to hospital management software, appointment scheduling software, and medical billing software — none of which are classified as medical devices under applicable law.

3. Any feature addition that could qualify the platform as SaMD will require:
   - Legal opinion from a qualified regulatory affairs consultant
   - Pre-market regulatory filing (CDSCO, FDA, or applicable authority) before deployment
   - This document will be updated accordingly

4. This declaration is made in good faith based on current platform design. It does not constitute legal advice and should be reviewed by qualified regulatory counsel before submission to any regulatory authority.

---

*HealthcareWale SaMD Exclusion Statement v1.0 — May 2026*  
*To be reviewed by legal counsel annually or upon any significant feature addition*

---
---

# 📜 HealthcareWale — Terms of Service & Medical Disclaimer
> **Document ID:** HW-TOS-001 | **Version:** 1.0 | **Effective Date:** [Insert Date]

---

## TERMS OF SERVICE

**Operator:** HealthcareWale Technologies Private Limited ("HealthcareWale," "we," "our," "us")  
**Platform:** HealthcareWale mobile app, web dashboard, WhatsApp bot, AI voice service, and all related services

---

### 1. ACCEPTANCE OF TERMS

By accessing, downloading, or using the HealthcareWale platform in any form, you ("User," "Patient," "Provider," or "you") agree to these Terms of Service ("Terms"). If you do not agree, do not use the platform.

These Terms form a legally binding agreement governed by the laws of India. Disputes are subject to the exclusive jurisdiction of courts in Mohali, Punjab.

---

### 2. ELIGIBILITY

- You must be 18 years or older to create an account independently
- Minors' accounts must be created and managed by a parent or legal guardian
- Medical practitioners must hold a valid NMC or State Medical Council registration to register as a Provider

---

### 3. PLATFORM NATURE & MEDICAL DISCLAIMER

**⚠️ CRITICAL DISCLAIMER — PLEASE READ:**

**3.1 HealthcareWale is NOT a medical service provider.**

HealthcareWale is a **technology platform** that facilitates:
- Administrative appointment scheduling between patients and licensed doctors
- Pharmacy inventory and billing management
- Healthcare operations automation

**HealthcareWale does NOT:**
- Provide medical advice, diagnosis, or treatment
- Employ doctors or pharmacists (providers are independent licensed professionals)
- Guarantee the clinical accuracy or quality of consultations conducted through the platform
- Function as a hospital, clinic, pharmacy, or any licensed healthcare establishment

**3.2 The AI is an administrative assistant, not a medical professional.**

The AI voice agent, WhatsApp bot, and automated features of HealthcareWale are administrative tools. They do not possess medical knowledge, diagnostic capability, or clinical judgment. Any health information you share with these systems is used solely for routing and booking purposes.

**3.3 THIS PLATFORM IS NOT FOR MEDICAL EMERGENCIES.**

If you or someone near you is experiencing a medical emergency — including but not limited to: chest pain, difficulty breathing, loss of consciousness, severe bleeding, stroke symptoms, poisoning, or any life-threatening condition — **DO NOT USE THIS PLATFORM.** Call **108 (National Emergency Ambulance Service)** or proceed immediately to the nearest hospital emergency department.

HealthcareWale accepts NO LIABILITY for outcomes resulting from use of this platform in emergency medical situations.

---

### 4. PROVIDER TERMS

Licensed Medical Practitioners and Pharmacy Owners ("Providers") onboarded on HealthcareWale agree to:

4.1 **Maintain active, valid registration** with NMC, State Medical Council, State Pharmacy Council, or relevant licensing authority throughout their tenure on the platform

4.2 **Practice only within their licensed scope** — specialists shall not consult on conditions outside their registered specialty via the platform

4.3 **Geographic practice limits** — Providers offering teleconsultation shall only accept patients from states/jurisdictions where they are legally permitted to practice (see Telehealth Licensing Policy HW-LEGAL-003)

4.4 **Response obligations** — Providers must respond to booked appointments within the scheduled time or initiate a reschedule at minimum 2 hours before the appointment time

4.5 **Quality standards** — Providers agree to uphold professional conduct standards of the Indian Medical Association and relevant state medical councils

4.6 **Platform exclusivity** — No exclusivity is implied; Providers may use other platforms simultaneously

---

### 5. PATIENT TERMS

Patients using HealthcareWale agree to:

5.1 Provide accurate personal and health information to the extent required for booking and record management

5.2 Not misrepresent identity, age, or insurance eligibility (PMJAY/Swasthya Sathi)

5.3 Honor booked appointments or cancel per the cancellation policy (Section 7)

5.4 Not use the platform to seek controlled substances, narcotics, or Schedule H1 drugs without valid in-person consultation records

5.5 Not use the platform for any fraudulent insurance claim purposes

---

### 6. INTELLECTUAL PROPERTY

All software, designs, workflows, AI models, documentation, brand names ("HealthcareWale," "SwasthAI"), and content on the platform are the intellectual property of HealthcareWale Technologies Private Limited. Unauthorized copying, reverse engineering, or commercial use is prohibited.

---

### 7. LIMITATION OF LIABILITY

To the maximum extent permitted by applicable law:

7.1 HealthcareWale's total liability to any user for any claim arising from use of the platform shall not exceed the total subscription fees paid by that user in the 3 months preceding the claim.

7.2 HealthcareWale shall not be liable for: clinical outcomes of consultations; errors in prescriptions issued by doctors; missed appointments; pharmacy delivery delays; insurance claim rejections; or any indirect, consequential, or punitive damages.

7.3 HealthcareWale is not liable for the independent professional conduct of any doctor, pharmacist, or healthcare provider using the platform.

---

### 8. GOVERNING LAW & DISPUTE RESOLUTION

These Terms are governed by Indian law. Any dispute shall first be attempted to be resolved through mediation. Unresolved disputes shall be subject to arbitration under the Arbitration and Conciliation Act, 1996, with the seat of arbitration in Mohali, Punjab.

---
---

# 💰 HealthcareWale — Refund, Cancellation & Platform Fee Policy
> **Document ID:** HW-FEE-001 | **Version:** 1.0 | **Effective Date:** [Insert Date]

---

## 1. CONSULTATION APPOINTMENT POLICY

### 1.1 Patient Cancellations
| Cancellation Timing | Refund |
|---|---|
| More than 4 hours before appointment | 100% refund to original payment method within 5–7 business days |
| 2–4 hours before appointment | 50% refund |
| Less than 2 hours before appointment | No refund |
| No-show (patient does not attend without cancellation) | No refund |

### 1.2 Doctor / Provider Cancellations
If a doctor cancels an appointment (for any reason):
- Patient receives 100% refund within 3 business days
- HealthcareWale will attempt to offer an alternative slot with the same or equivalent doctor
- Patient receives a platform credit of ₹50 (equivalent) for the inconvenience

### 1.3 Platform-Initiated Cancellations
If HealthcareWale cancels an appointment due to technical failure, doctor unavailability verification failure, or force majeure:
- 100% refund within 3 business days
- HealthcareWale platform credit of ₹100

---

## 2. MEDICINE DELIVERY POLICY

### 2.1 Order Cancellation
- Orders cancelled before pharmacy confirms: 100% refund
- Orders cancelled after pharmacy confirms but before dispatch: 80% refund (20% processing fee)
- Orders cancelled after dispatch: No refund (return pickup can be arranged for eligible medicines)

### 2.2 Wrong or Damaged Medicine
- Report within 24 hours of delivery via WhatsApp
- HealthcareWale arranges replacement or full refund within 5 business days
- Photographic evidence of wrong/damaged medicine required

### 2.3 Schedule H / Prescription Medicines
- Once dispensed against a valid verified prescription, Schedule H medicines cannot be returned due to cold chain and safety regulations
- Exceptions: Manufacturing defect or damaged packaging only

---

## 3. SAAS SUBSCRIPTION POLICY (B2B — Clinics, Pharmacies, Hospitals)

### 3.1 Free Trial
- 14-day free trial with no payment required
- Trial automatically ends — no auto-charge without explicit payment authorization

### 3.2 Subscription Refunds
| Scenario | Refund |
|---|---|
| Cancel within first 7 days of paid subscription | 100% refund |
| Cancel Day 8–30 | Pro-rated refund for unused days |
| Cancel after Day 30 | No refund for current month; subscription ends at billing cycle end |
| Annual plan — cancel within 30 days | Full refund minus months used |
| Annual plan — cancel after 30 days | Pro-rated refund for remaining complete months |

### 3.3 Platform Fee (Commission)
- Medicine delivery commission (8–12%) is non-refundable once order is delivered
- Lab test commission (12–20%) is non-refundable once test is conducted
- PMJAY claim filing fee (₹75–200) is refundable only if HealthcareWale's system error caused the rejection

---

## 4. PAYMENT METHODS & PROCESSING

- Accepted: UPI, Credit/Debit Card (Razorpay), Net Banking, Cash on Delivery (medicine delivery only)
- Refunds are processed to the original payment method only
- UPI refunds: 1–3 business days
- Card refunds: 5–7 business days (depends on issuing bank)
- Cash on Delivery orders: Refund via UPI/bank transfer after verification

---

*HealthcareWale Terms of Service, Medical Disclaimer & Refund Policy v1.0 — May 2026*
