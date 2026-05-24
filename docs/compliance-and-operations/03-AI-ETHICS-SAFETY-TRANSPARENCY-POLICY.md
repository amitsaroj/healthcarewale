# 🤖 HealthcareWale — AI Ethics, Safety & Transparency Policy
> **Document ID:** HW-AI-001  
> **Version:** 1.0 | **Effective Date:** [Insert Date]  
> **Frameworks:** EU AI Act 2024 · WHO Ethics Guidelines for AI in Health · NITI Aayog AI Principles · FDA SaMD Guidance  
> **Document Owner:** Founder / CTO — HealthcareWale Technologies Pvt. Ltd.

---

## 1. PURPOSE & SCOPE

This policy governs the ethical development, deployment, and oversight of all Artificial Intelligence and Machine Learning systems within HealthcareWale. It applies to:

- **AI Voice Agent:** Hindi/Bengali voice-based appointment booking and enquiry system (Exotel + Sarvam AI + LLM)
- **WhatsApp Automation Bot:** Intent-driven conversational booking and notification system
- **Prescription OCR Engine:** Handwritten prescription reading via Google Cloud Vision + medical NLP
- **Inventory Demand Forecasting Model:** Predictive reorder suggestions for pharmacies
- **PMJAY Claim Pre-validation Engine:** ICD-10 code suggestion and claim rejection prediction
- **Patient Churn Prediction Model:** Identifies patients at risk of disengaging from care
- **Appointment Matching Algorithm:** Matches patient needs to doctor specialty and availability

This policy does NOT govern AI systems operated independently by partner hospitals, clinics, or pharmacies outside HealthcareWale's direct control.

---

## 2. CORE AI ETHICS PRINCIPLES

HealthcareWale commits to the following principles in all AI development and deployment:

### 2.1 Non-Maleficence (Do No Harm)
No AI system deployed on HealthcareWale shall make or recommend clinical decisions. The platform's AI is categorically restricted to **administrative, logistical, and operational** functions. The AI shall never:
- Diagnose medical conditions
- Recommend specific treatments or medications
- Provide dosage guidance
- Triage patients based on clinical urgency without doctor oversight
- Suggest stopping or modifying ongoing medications

Any patient query that enters clinical territory shall trigger an immediate handoff: *"Yeh question doctor se poochhna chahiye. Kya main aapke liye appointment book karun?"*

### 2.2 Beneficence (Serve Patient Welfare)
Every AI decision — from slot matching to reminder scheduling — is optimized for patient welfare, not solely business metrics. Where business interests and patient welfare conflict, patient welfare takes precedence.

### 2.3 Autonomy & Human Override
- Patients retain full control over their appointment decisions. The AI suggests; humans decide.
- Doctors retain full clinical authority. AI-generated ICD-10 codes are suggestions — billing staff and doctors approve before claim submission.
- Any automated action (reminder call, auto-reorder, claim filing) has a configurable human review checkpoint.

### 2.4 Fairness & Non-Discrimination
The AI appointment matching engine shall not discriminate on the basis of:
- Caste, religion, gender, age, disability, sexual orientation, or socioeconomic status
- Language preference (Hindi vs Bengali speakers shall receive equal quality of service)
- PMJAY/Swasthya Sathi status (insured vs uninsured patients receive equal booking access)
- Geographic location (rural vs urban patients within service area)

### 2.5 Transparency & Explainability
- Patients interacting with the AI voice agent are informed at the start of the call: *"Main HealthcareWale ka AI assistant hun"* — the AI identity is never concealed
- AI-generated prescription suggestions or ICD-10 codes include confidence scores visible to reviewing staff
- Inventory demand forecasts show the key drivers (e.g., "Based on your 90-day sales + dengue season pattern in Lucknow")

### 2.6 Accountability
- Every AI decision affecting a patient or clinical record is logged with: model version, input parameters, output decision, confidence score, human approval status
- AI audit logs are retained for 3 years
- Designated AI Safety Officer (initially: Founder Amit Saroj) reviews AI incident reports monthly

---

## 3. AI RISK CLASSIFICATION

Following the EU AI Act 2024 risk-based framework:

| AI System | EU AI Act Classification | Rationale | HealthcareWale Obligation |
|---|---|---|---|
| Appointment booking bot (WhatsApp/Voice) | **Minimal Risk** | Administrative scheduling; no clinical decisions | Transparency disclosure to users |
| Prescription OCR + medicine name extraction | **Limited Risk** | Assists pharmacist; pharmacist makes final decision | Accuracy monitoring; human review mandatory |
| Inventory demand forecasting | **Minimal Risk** | Commercial prediction; no patient impact | Regular accuracy testing |
| ICD-10 code suggestion for PMJAY claims | **High Risk** | Could affect patient insurance entitlement | Mandatory human review; bias testing; accuracy >95% target |
| AI triage pre-screening (symptom collection) | **High Risk** | Could influence patient healthcare-seeking behavior | SaMD boundary enforcement; doctor override mandatory; monthly audit |
| Patient churn prediction | **Limited Risk** | Re-engagement tool; patient can opt out | Transparency; opt-out mechanism |
| Voice agent (Hindi/Bengali NLU) | **Limited Risk** | Language accuracy affects service access | Dialect testing; fallback to human; accuracy monitoring |

---

## 4. ALGORITHMIC BIAS PREVENTION

### 4.1 Known Bias Risks in HealthcareWale Context

| Bias Type | Risk Scenario | Mitigation |
|---|---|---|
| **Language bias** | AI performs better in Standard Hindi than Bhojpuri/Awadhi dialects — rural UP patients may receive worse service | Separate accuracy benchmarking for each dialect; Bhashini API for dialect support |
| **Gender bias** | If training data underrepresents female patients, appointment matching may deprioritize women | Gender-stratified accuracy testing quarterly |
| **Literacy bias** | Voice AI assumes certain vocabulary familiarity — low-literacy patients may struggle | Simplified vocabulary list; tolerance for non-standard phrasing |
| **Urban bias** | OCR trained on printed prescriptions may perform poorly on handwritten prescriptions common in rural areas | Separate OCR accuracy tracking for printed vs handwritten |
| **PMJAY coding bias** | ICD-10 suggestion model may over-code conditions associated with certain demographics | Demographic parity testing on claim coding outputs quarterly |

### 4.2 Bias Testing Protocol

- **Pre-deployment:** All new AI models tested across demographic subgroups before production release
- **Quarterly:** Accuracy metrics computed separately for: gender, age bracket, state (UP vs WB), language, urban vs rural
- **Threshold:** If any subgroup accuracy deviates >5% from overall accuracy, model is flagged for retraining before continued use
- **Documentation:** All bias testing results stored in AI Model Registry (internal tool)

---

## 5. MEDICAL HALLUCINATION PREVENTION

"Hallucination" in healthcare AI refers to the model generating plausible-sounding but clinically incorrect information — a critical risk in medical contexts.

### 5.1 Architectural Safeguards

**Strict System Prompt Boundaries:**
```
System Prompt (AI Voice Agent):
"You are an administrative booking assistant for HealthcareWale.
You MUST ONLY help with: appointment booking, doctor availability,
clinic timings, fee enquiry, appointment cancellation/rescheduling,
and general clinic information.

You MUST REFUSE any question about:
- Medical symptoms, diagnoses, treatments
- Drug interactions or dosage
- Emergency medical advice
- Any clinical guidance whatsoever

If a user asks a medical question, respond ONLY with:
'Yeh sawaal aapko doctor se poochhna chahiye. Kya main aapke liye
appointment book karun?'

You have NO ability to diagnose, treat, or advise on medical matters."
```

**Retrieval-Augmented Generation (RAG):**
- AI responses about clinic information, doctor availability, and fee structures are grounded in real-time database queries — not LLM memory
- The model cannot hallucinate a doctor's availability — it queries the live appointment database

**Output Filtering:**
- LLM outputs are passed through a medical keyword classifier before delivery
- Any output containing: drug names, dosage numbers, symptom diagnoses, treatment recommendations, or emergency guidance is flagged and blocked — a safe fallback message is delivered instead

### 5.2 Hallucination Monitoring

- 5% random sample of AI voice transcripts reviewed weekly for medical content boundary violations
- Any boundary violation triggers immediate system review and model prompt update
- Incident logged in AI Safety Log with severity classification

---

## 6. AI IN TRIAGE & SYMPTOM COLLECTION (STRICT LIMITS)

HealthcareWale's AI triage pre-screening collects basic patient information before consultation to help the doctor prepare. This feature operates within strict boundaries:

**Permitted:**
- "Aaj kaun si problem ke liye aaye hain?" (Chief complaint collection — text only)
- "Pehle bhi yahi problem aayi thi?" (Visit history confirmation)
- Routing patient to appropriate specialist based on stated complaint (e.g., "fever + cough" → General Physician)

**Strictly Prohibited:**
- Severity scoring or clinical urgency classification
- Suggesting a diagnosis based on symptoms
- Recommending any medication, even OTC
- Any statement like "Aapko [condition] ho sakti hai"
- Advising patient to go to emergency without explicitly being triggered by the word "emergency" or "chest pain" / "stroke" keyword alerts

**Emergency Keyword Protocol:**
If patient says: "emergency", "chest pain", "dil ka dard", "breathing problem", "saans nahi aa rahi", "accident", "unconscious", "stroke":
- AI immediately responds: *"Yeh emergency lag rahi hai. Kripya turant 108 (ambulance) call karein ya nearest emergency room jayein. Main is situation mein aapki madad nahi kar sakta."*
- Call is flagged for immediate human review
- AI does not attempt to book an appointment in an emergency scenario

---

## 7. TRANSPARENCY DISCLOSURES

### 7.1 Patient-Facing Disclosures

**AI Identity Disclosure (Voice):**
Every inbound call handled by AI begins: *"Namaste! Main HealthcareWale ka AI assistant hun. Aapki kaise madad kar sakta hun?"*

**AI Identity Disclosure (WhatsApp):**
First message in any bot conversation: *"Namaste 👋 Main HealthcareWale ka automated assistant hun. Aapki appointment se related madad karunga."*

**AI Limitations Notice (In-App):**
Displayed on first app login and accessible via Settings > About AI:
*"HealthcareWale ka AI system sirf appointment booking aur clinic management mein help karta hai. Yeh koi medical advice, diagnosis, ya treatment suggest nahi karta. Kisi bhi health problem ke liye apne doctor se milein."*

### 7.2 Provider-Facing Disclosures

All ICD-10 code suggestions show:
- Suggested code + description
- Confidence score (e.g., 87%)
- "Suggested by AI — Please verify before submission" watermark
- Human approval required before claim submission

All AI-generated discharge summaries show:
- "AI-Assisted Draft — Requires Doctor Review and Digital Signature" header

---

## 8. AI GOVERNANCE STRUCTURE

| Role | Responsibility |
|---|---|
| **AI Safety Officer** (Founder, Phase 1) | Monthly review of AI logs, incident reports, bias test results |
| **Engineering Lead** | AI model versioning, deployment gates, accuracy monitoring |
| **Medical Advisor** (to be appointed) | Clinical boundary review, emergency protocol validation |
| **Data Protection Officer** | Ensuring AI data use complies with DPDP Act / GDPR |
| **Customer Success** | First line of patient complaints related to AI interactions |

### 8.1 AI Model Change Management

Any change to a production AI model (prompt update, model version upgrade, new feature) requires:
1. Staging environment testing with >500 sample interactions
2. Bias testing across demographic subgroups
3. AI Safety Officer sign-off
4. Gradual rollout (10% → 50% → 100% traffic)
5. 48-hour monitoring period with rollback capability

---

## 9. INCIDENT CLASSIFICATION & RESPONSE

| Severity | Description | Example | Response Time |
|---|---|---|---|
| **P0 — Critical** | AI provides medical advice or emergency guidance failure | AI suggests a diagnosis; AI fails to escalate emergency keyword | Immediate rollback; 1-hour incident report |
| **P1 — High** | AI discloses incorrect doctor availability causing harm | Patient misses critical appointment due to wrong slot info | 4-hour fix; customer notification |
| **P2 — Medium** | AI repeatedly fails to understand a language/dialect | Bhojpuri speakers consistently misunderstood | 7-day fix plan; dialect training |
| **P3 — Low** | AI gives awkward but harmless response | Unusual phrasing in confirmation message | Next sprint fix |

---

## 10. REGULATORY ALIGNMENT

| Regulation | Relevance | HealthcareWale Position |
|---|---|---|
| **EU AI Act 2024** | High Risk AI systems require conformity assessment | Our triage and ICD coding tools are monitored as High Risk even though India-only — EU standard adopted voluntarily |
| **FDA SaMD Guidance** | Software as Medical Device — if AI is used for clinical decisions, it becomes a regulated device | HealthcareWale AI is categorically excluded from SaMD classification — administrative only (see HW-SAMD-001) |
| **NITI Aayog AI Principles** | India's national AI ethics framework | Full alignment — fairness, transparency, accountability, privacy, and safety |
| **WHO Ethics & Governance of AI for Health** | WHO's six core principles for health AI | Full alignment — autonomy, well-being, transparency, accountability, inclusiveness, sustainability |
| **ICMR AI in Health Guidelines** | Indian Council of Medical Research AI standards | Monitored for final guidance; voluntary early alignment |

---

*HealthcareWale AI Ethics, Safety & Transparency Policy v1.0 — May 2026*  
*Review cycle: Bi-annual, or upon any significant AI system change*
