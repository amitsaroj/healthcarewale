# 📊 HealthcareWale — AI Data Minimization & Model Training Policy
> **Document ID:** HW-AI-002 | **Version:** 1.0 | **Effective Date:** [Insert Date]

---

## 1. PURPOSE

This policy defines how HealthcareWale collects, anonymizes, and uses patient interaction data in the context of AI model development and improvement. It establishes hard boundaries on data use to protect patient privacy and maintain regulatory compliance under the DPDP Act 2023, GDPR, and HIPAA.

---

## 2. DATA MINIMIZATION PRINCIPLES

HealthcareWale applies data minimization at every stage of AI operation:

### 2.1 Collection Minimization
- AI voice agents receive ONLY the data required for the current interaction: available appointment slots, doctor names, clinic timing — not full patient health history
- OCR engine receives the prescription image only — it does not receive patient name, ABHA ID, or medical history
- Demand forecasting model receives aggregated, medicine-level sales data — not individual patient purchase records
- Chatbot/WhatsApp bot receives message content + patient phone number only — no health record access

### 2.2 Retention Minimization

| Data Type | AI Processing Duration | Storage After Processing |
|---|---|---|
| Voice audio stream | Real-time STT only | Recording: 30 days, then deleted |
| Voice transcript (text) | Intent extraction | 30 days for QA, then deleted |
| WhatsApp messages | Intent detection + booking | 90 days active, 2 years archived |
| Prescription images | OCR processing (~5 seconds) | NOT stored post-processing |
| Patient vitals (BP, glucose) | Anomaly detection check | Stored in patient record per retention policy |
| Appointment interaction logs | Analytics | 3 years, anonymized after 90 days |

### 2.3 Access Minimization
- AI model APIs (Anthropic Claude, OpenAI) receive only the message/prompt — NEVER structured patient records
- LLM API calls are stateless — no patient data persists in LLM provider infrastructure between calls
- Sarvam AI (STT/TTS) receives voice audio stream — processed in-memory, not stored

---

## 3. MODEL TRAINING POLICY

### 3.1 Absolute Prohibitions

**HealthcareWale NEVER:**
- Sends identified patient health data to any LLM provider for model training
- Uses real patient consultation notes, diagnoses, or prescriptions to fine-tune any model
- Shares patient data with AI vendors under training data licenses
- Allows AI vendors to retain patient interaction data for their own model improvement

All major AI API providers (Anthropic, OpenAI, Google) have been selected partly because they offer **Zero Data Retention (ZDR)** or equivalent API policies where inputs are not used for model training by default. HealthcareWale uses only ZDR-eligible API tiers.

### 3.2 Permitted Uses for Internal Model Improvement

Internal AI improvement (improving Hindi intent detection, OCR accuracy, demand forecasting) may use:

| Data Type | Permitted Use | Required Processing |
|---|---|---|
| Voice transcripts | Improve Hindi/Bengali NLU accuracy | Must be de-identified (no name, phone, ABHA ID) before use |
| WhatsApp conversation logs | Improve booking intent detection | De-identified; medical content filtered out |
| OCR outputs | Improve prescription reading accuracy | Prescription images anonymized (doctor name + patient name removed) |
| Appointment interaction logs | Improve slot recommendation | Aggregated only; no individual patient journeys |
| Sales data | Improve demand forecasting | Pharmacy-level aggregation; no patient-level data |

### 3.3 De-identification Standard

Before any data is used for internal model training:

1. **Remove direct identifiers:** Name, phone, email, ABHA ID, address, date of birth, Aadhaar reference
2. **Generalize quasi-identifiers:** Exact date → week number; City → district
3. **Filter health content:** Any text containing diagnosis names, drug names, or dosage information is flagged and removed from training datasets
4. **Safe Harbor verification:** Verified by Data Protection Officer that output meets HIPAA Safe Harbor de-identification standard
5. **Documentation:** De-identification certificate stored in AI Model Registry for each training dataset

### 3.4 Opt-In for Data Contribution

Patients who wish to contribute their anonymized data to improve AI accuracy may opt in via:
- In-app setting: "Help improve HealthcareWale AI (anonymized data only)"
- This opt-in is separate from primary service consent
- Opt-in patients receive a disclosure of exactly what data is used and how
- Opt-in is revocable at any time

---

## 4. THIRD-PARTY AI VENDOR OBLIGATIONS

All AI API vendors used by HealthcareWale must sign a **Data Processing Agreement (DPA)** confirming:
- No retention of HealthcareWale data beyond the immediate API request
- No use of HealthcareWale data for model training
- SOC 2 Type II or equivalent security certification
- Breach notification within 72 hours
- Annual audit rights for HealthcareWale

**Current vendor DPA status:**
| Vendor | DPA Status | ZDR Policy |
|---|---|---|
| Anthropic (Claude API) | ✅ DPA executed | ✅ Enterprise ZDR |
| Google Cloud Vision | ✅ DPA executed | ✅ Data processing terms |
| Sarvam AI | 🔲 In progress | 🔲 Confirming |
| AWS | ✅ DPA executed | ✅ AWS Data Processing Addendum |

---

*HealthcareWale AI Data Minimization & Model Training Policy v1.0 — May 2026*
