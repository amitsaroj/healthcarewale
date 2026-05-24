# 🧾 Compliance & Operations Audit Prompt
> **Submitted By:** Amit Saroj (Founder)  
> **Date:** May 2026  
> **Purpose:** Triggered full compliance documentation suite creation for HealthcareWale

---

## Original Prompt

System Role & Objective:
You are an expert AI Research, Legal-Tech Consultant, and Software Engineering Agent specializing in global HealthTech compliance (HIPAA, GDPR, DPDP Act, ABDM), AI regulations (EU AI Act, FDA SaMD guidelines), and startup operations. Your task is to audit our existing GitHub repository, identify missing operational, legal, compliance, and product documents for an AI-powered doctor appointment booking platform, draft these documents in highly professional detail, and commit them directly to the repository.

Follow this strict step-by-step execution protocol:

### STEP 1: COMPREHENSIVE REPOSITORY AUDIT
Before doing any external research or writing code, read the entire repository. Analyze the existing codebase, architecture diagrams, database schemas, and current research files.
- Identify the current scope, tech stack, data flows, and any partial documentation already present.
- Do not duplicate existing research; instead, build upon it and fill the regulatory and operational gaps.

### STEP 2: REGULATORY & DOCUMENTATION RESEARCH
Conduct exhaustive research on global healthcare frameworks, digital health missions, and emerging AI safety standards. You must ensure the repository includes complete, institutional-grade drafts/templates for the following document categories:

#### 1. Healthcare, Data Privacy & AI Compliance Documents
- **Data Protection & Privacy Policy:** Fully compliant with HIPAA (US), GDPR (Europe), and the DPDP Act (India). Outlines end-to-end processing of Protected Health Information (PHI) and Personally Identifiable Information (PII).
- **ABDM & Digital Health Stack Integration Blueprint:** Framework for compliance with regional health stacks (e.g., Ayushman Bharat Digital Mission in India for ABHA ID integration, health repository provider workflows), if applicable.
- **AI Ethics, Safety, & Transparency Policy:** Explaining how the AI engine processes user symptoms, matches them to doctors, handles algorithmic bias, avoids medical hallucinations, and safeguards data.
- **AI Data Minimization & Model Training Policy:** Explicitly stating how user conversations are anonymized/de-identified, and verifying whether or not health data is utilized for downstream LLM fine-tuning.

#### 2. Legal, Liability & User-Facing Agreements
- **Informed Consent Form for AI Triage/Interactions:** A mandatory user-facing agreement clarifying that the AI is an administrative/triage booking assistant and DOES NOT provide formal medical advice, diagnoses, or treatment plans.
- **Software as a Medical Device (SaMD) Exclusion Statement:** A legally airtight document detailing how the app's features purposefully remain within administrative/scheduling boundaries to avoid classification as a regulated medical device under FDA or international health authority guidelines.
- **Terms of Service (ToS) & Medical Disclaimer:** Comprehensive terms governing platform use for both patients and healthcare providers, featuring an absolute liability waiver for emergency medical situations.
- **Refund, Cancellation, & Platform Fee Policy:** Explicit rules regarding missed appointments, late cancellations, automated doctor re-scheduling, platform convenience fees, and doctor no-shows.

#### 3. Provider Onboarding, Licensing & Operations
- **Medical Practitioner Service Level Agreement (SLA):** Defining expected response times, digital consultation etiquette, payout structures, platform conduct rules, and tele-consultation boundary limits.
- **Cross-Jurisdiction Telehealth Licensing Policy:** A legal framework ensuring doctors only accept appointments from patients within their legally permitted practicing territory.
- **Provider Verification & Credentialing SOP:** A step-by-step standard operating procedure for backend administrators to verify national medical council registrations, degrees, and active licenses before account activation.

#### 4. Technical Security & Data Governance
- **Information Security Policy (SOC 2 / ISO 27001 aligned):** Technical documentation detailing end-to-end data encryption, database auditing, multi-tenant isolation, and zero-trust access controls.
- **Data Retention & Secure Destruction Policy:** Defining how long patient appointment history, medical records, and AI chat transcripts are stored before being permanently and securely purged.
- **Incident Response & Data Breach Protocol:** A step-by-step technical and PR handbook for the engineering team to execute in the event of a security exploit or data leak.

#### 5. Core Product Strategy & AI Architecture
- **Product Requirement Document (PRD):** A detailed technical breakdown of the AI appointment matching engine, voice/text natural language booking pipelines, real-time doctor availability sync engines, and automated fallback notification systems.

### STEP 3: DOCUMENT CREATION & FILE STRUCTURE
Create a clean, dedicated folder structure in the repository named `/docs/compliance-and-operations/`. Inside this folder, generate detailed Markdown (.md) files for every single document listed above.
- Do not use placeholders or generic text.
- Write complete, robust, professional policy text.

### STEP 4: REPOSITORY INTEGRATION & COMMIT
Once all documents are drafted:
1. Update the main README.md file to add a "Documentation Index" section linking to all newly created files.
2. Commit all changes with clear, descriptive commit messages.
3. Provide a summary listing exactly which files were created and where they are located.

---

## Documents Generated (Output)

| # | File | Description |
|---|---|---|
| 01 | `docs/compliance-and-operations/01-DATA-PROTECTION-PRIVACY-POLICY.md` | HIPAA + GDPR + DPDP Act compliant privacy policy |
| 02 | `docs/compliance-and-operations/02-ABDM-DIGITAL-HEALTH-INTEGRATION-BLUEPRINT.md` | Full ABDM/ABHA/PMJAY integration blueprint |
| 03 | `docs/compliance-and-operations/03-AI-ETHICS-SAFETY-TRANSPARENCY-POLICY.md` | AI ethics, hallucination prevention, EU AI Act alignment |
| 04 | `docs/compliance-and-operations/04-AI-DATA-MINIMIZATION-MODEL-TRAINING-POLICY.md` | AI data minimization and model training rules |
| 05 | `docs/compliance-and-operations/05-INFORMED-CONSENT-FORM-AI-INTERACTIONS.md` | Patient informed consent (Hindi/Bengali/English) |
| 06 | `docs/compliance-and-operations/06-TOS-SAMD-EXCLUSION-REFUND-POLICY.md` | Terms of Service + SaMD exclusion + Refund policy |
| 07 | `docs/compliance-and-operations/07-PROVIDER-SLA-TELEHEALTH-LICENSING-CREDENTIALING-SOP.md` | Provider SLA + telehealth licensing + credentialing SOP |
| 08 | `docs/compliance-and-operations/08-SECURITY-POLICY-DATA-RETENTION-INCIDENT-RESPONSE.md` | InfoSec policy + data retention + breach protocol |
| 09 | `docs/compliance-and-operations/09-PRODUCT-REQUIREMENTS-DOCUMENT-PRD.md` | Full PRD: AI booking engine, voice/WhatsApp pipelines, availability sync |

*Generated by Claude (Anthropic) — May 2026*
