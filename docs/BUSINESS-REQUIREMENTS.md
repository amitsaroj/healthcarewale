# 📊 HealthcareWale — Complete Business Requirements Document (BRD)
> Version: 1.0 | May 2026 | Founder: Amit Saroj

---

## TABLE OF CONTENTS
1. [Executive Summary](#1-executive-summary)
2. [Business Objectives & Goals](#2-business-objectives--goals)
3. [Business Model Canvas](#3-business-model-canvas)
4. [Stakeholder Requirements](#4-stakeholder-requirements)
5. [Operational Requirements](#5-operational-requirements)
6. [Legal & Compliance Requirements](#6-legal--compliance-requirements)
7. [Financial Requirements](#7-financial-requirements)
8. [Human Resource Requirements](#8-human-resource-requirements)
9. [Technology Procurement Requirements](#9-technology-procurement-requirements)
10. [Risk Register](#10-risk-register)
11. [Success Criteria](#11-success-criteria)
12. [Exit Strategy](#12-exit-strategy)

---

## 1. EXECUTIVE SUMMARY

**Company Name:** HealthcareWale (SwasthAI)
**Founder:** Amit Saroj
**Headquarters:** Mohali, Punjab (Operations focused on UP + West Bengal)
**Business Type:** B2B SaaS + B2C Healthcare Platform
**Stage:** Pre-revenue / MVP Development
**Target Launch:** Q3 2026

**One-Line Definition:**
> HealthcareWale is an AI-powered, voice-first, WhatsApp-native healthcare operations platform built for clinics, pharmacies, hospitals, and distributors in Tier-2 and Tier-3 India.

**Core Problem Solved:**
Semi-urban Indian healthcare operations are broken. Clinics miss patient calls. Pharmacies lose money to expiry. Distributors receive orders manually. No single platform fixes all of this for the ₹500–₹5,000/month budget segment. HealthcareWale does.

---

## 2. BUSINESS OBJECTIVES & GOALS

### 2.1 Short-Term (0–6 Months)
- Build and launch MVP with pharmacy inventory + clinic appointment modules
- Acquire 100–250 paying customers in Uttar Pradesh (Lucknow, Gorakhpur, Varanasi)
- Achieve MRR of ₹3–5 Lakh
- Validate product-market fit: <5% monthly churn, NPS > 40
- Register company (Private Limited)
- Obtain initial regulatory clearances

### 2.2 Medium-Term (6–18 Months)
- Expand to West Bengal market (Kolkata, Durgapur, Siliguri, Howrah)
- Launch hospital/nursing home HMS module
- Launch medicine delivery and lab test booking
- Achieve 3,000 paying customers
- Achieve MRR of ₹25–35 Lakh
- Raise Seed funding (₹2–5 Crore) from angel investors or VC

### 2.3 Long-Term (18–36 Months)
- Expand to Bihar, MP, Jharkhand, Odisha
- 15,000+ paying customers
- ARR of ₹10–15 Crore
- White-label contracts with 3–5 hospital chains / state governments
- Raise Series A (₹15–30 Crore)
- Potential acquisition target for Tata Health, Reliance, or Apollo

---

## 3. BUSINESS MODEL CANVAS

```
┌──────────────────────────────────────────────────────────────────────────────┐
│                        HEALTHCAREWALE BUSINESS MODEL CANVAS                  │
├────────────────┬───────────────────────┬──────────────┬──────────────────────┤
│ KEY PARTNERS   │ KEY ACTIVITIES        │ VALUE PROPS  │ CUSTOMER RELATIONS   │
│                │                       │              │                      │
│ • Exotel       │ • Build & maintain    │ For Pharmacy:│ • WhatsApp-first     │
│ • Sarvam AI    │   AI voice platform   │ → No expiry  │   support            │
│ • Interakt     │ • On-ground sales     │   losses     │ • Personal onboarding│
│ • Razorpay     │   in UP/WB            │ → Auto billing│ • Weekly tips       │
│ • AWS Mumbai   │ • Customer success    │ → Voice stock │ • Community groups  │
│ • NHA/ABDM     │   & support           │   updates    │ • Dedicated account  │
│ • SRL/Thyrocare│ • Partnership mgmt    │              │   manager (Pro+)     │
│ • IMA chapters │ • Regulatory          │ For Clinic:  │                      │
│ • Pharma MRs   │   compliance          │ → AI answers │                      │
│ • WB Govt      │ • Product development │   all calls  │                      │
│                │                       │ → Zero no-   │                      │
├────────────────┤                       │   shows      │                      │
│ KEY RESOURCES  │                       │ → Auto follow│                      │
│                │                       │   ups        │                      │
│ • Tech platform│                       │              │                      │
│ • n8n workflows│                       │ For Hospital:│                      │
│ • Amit's tech  │                       │ → PMJAY fast │                      │
│   skills       │                       │   claims     │                      │
│ • WhatsApp API │                       │ → Digital EMR│                      │
│ • Exotel IVR   │                       │              │                      │
│ • Customer data│                       │ For Distributor:                    │
│                │                       │ → Auto order │                      │
│                │                       │   collection │                      │
├────────────────┴───────────────────────┤              ├──────────────────────┤
│ COST STRUCTURE                         │              │ CHANNELS             │
│                                        │              │                      │
│ Fixed:                                 │              │ • WhatsApp groups    │
│ • AWS servers: ₹15,000/month           │              │ • YouTube (Hindi/    │
│ • Team salaries: ₹1,00,000+/month     │              │   Bengali)           │
│ • Office/ops: ₹30,000/month           │              │ • Field sales        │
│                                        │              │ • Google Ads         │
│ Variable:                              │              │ • Pharma MR network  │
│ • WhatsApp API: ₹0.18/msg             │              │ • IMA chapters       │
│ • Exotel calls: ₹0.50–1.50/min       │              │ • Facebook/Instagram │
│ • AI API: ₹0.01–0.05/call            │              │ • Medical fairs      │
│ • OCR: ₹0.07/image                   │              │                      │
├────────────────────────────────────────┴──────────────┼──────────────────────┤
│ REVENUE STREAMS                                        │ CUSTOMER SEGMENTS    │
│                                                        │                      │
│ 1. SaaS Subscriptions (₹299–₹24,999/month)            │ • Medical stores     │
│ 2. AI Voice Call Billing (₹1.50–3/call)               │ • Solo clinics/docs  │
│ 3. WhatsApp Message Billing (₹0.35/msg)               │ • Nursing homes      │
│ 4. Medicine Delivery Commission (8–12%)               │ • Hospitals          │
│ 5. Lab Test Commission (12–20%)                       │ • Pharma distributors│
│ 6. PMJAY Claim Fees (₹75–200/claim)                  │ • Patients (B2C)     │
│ 7. White-Label Licensing (₹25K–10L/month)            │                      │
│ 8. Pharma Analytics (₹15K–2L/report)                │                      │
│ 9. Premium Add-Ons (₹299–4,999/month)               │                      │
└────────────────────────────────────────────────────────┴──────────────────────┘
```

---

## 4. STAKEHOLDER REQUIREMENTS

### 4.1 Pharmacy Owner Requirements
| Requirement | Priority | Acceptance Criteria |
|---|---|---|
| App must work on low-end Android (₹5,000 phones) | Critical | Runs smoothly on 2GB RAM, Android 8 |
| Must work in Hindi — no English forcing | Critical | Full UI in Hindi, voice commands in Hindi |
| Billing must be GST-compliant | Critical | GSTIN, HSN, tax breakup in every bill |
| Expiry alerts must be automated | Critical | Push notification + WhatsApp 30/15/7 days before |
| Setup must take <30 minutes | High | New user completes setup in under 30 min |
| Must work offline when internet fails | High | Billing works offline, syncs on reconnect |
| Price must be under ₹1,000/month | Critical | Starter plan at ₹299, Growth at ₹599 |

### 4.2 Clinic / Doctor Requirements
| Requirement | Priority | Acceptance Criteria |
|---|---|---|
| AI voice must sound natural, not robotic | Critical | Patient cannot tell it's AI in first 10 seconds |
| Voice must work in Hindi and Bengali | Critical | Both languages supported at launch |
| Doctor must not need to install anything new | High | Works via existing WhatsApp + browser |
| Appointment system must prevent double-booking | Critical | Zero double-booking incidents |
| Patient records must be private and secure | Critical | DPDP Act compliance, encrypted storage |
| Integration with existing phone number | High | Works with clinic's existing mobile/landline |
| Prescription generation within consultation | High | Doctor can create digital prescription in 2 min |

### 4.3 Patient Requirements
| Requirement | Priority | Acceptance Criteria |
|---|---|---|
| No app download required for basic features | Critical | WhatsApp + SMS sufficient for booking |
| Book appointment in <3 minutes | Critical | End-to-end booking in 3 minutes or less |
| Reminders in preferred language | High | Hindi or Bengali based on patient preference |
| View queue status without visiting clinic | High | Real-time queue visible on WhatsApp |
| Access own health records | Medium | Records accessible via app/link |
| Data privacy respected | Critical | Explicit consent for all data collection |

### 4.4 Distributor Requirements
| Requirement | Priority | Acceptance Criteria |
|---|---|---|
| Receive orders automatically without manual entry | Critical | Orders arrive via WhatsApp/dashboard automatically |
| Track all outstanding payments | High | Payment dashboard with aging report |
| Forecast demand to optimize stocking | Medium | AI demand prediction with 80%+ accuracy |
| Simple interface — not complex ERP | Critical | Non-tech staff can use within 1 hour of training |

---

## 5. OPERATIONAL REQUIREMENTS

### 5.1 Customer Support Operations

**Support Channels:**
- WhatsApp: Primary channel (response within 2 hours, business hours)
- Phone: For Pro/Enterprise customers (dedicated number)
- Email: For billing/account issues
- In-app chat: AI-first, escalates to human

**Support Team Size by Phase:**
| Phase | Customers | Support Staff |
|---|---|---|
| Phase 1 (0–6 months) | 0–250 | Amit + 1 part-time |
| Phase 2 (6–18 months) | 250–3,000 | 3–5 full-time |
| Phase 3 (18–36 months) | 3,000–15,000 | 10–20 full-time |

**Support SLA:**
| Plan | First Response | Resolution |
|---|---|---|
| Starter | 8 hours | 48 hours |
| Growth | 4 hours | 24 hours |
| Pro/Enterprise | 2 hours | 8 hours |

**AI-First Support:**
- n8n workflow: Customer WhatsApps issue → AI tries to resolve → If unresolved → escalates to human
- Self-service help library in Hindi + Bengali (video tutorials)
- Target: AI resolves 70% of support queries without human intervention

### 5.2 Onboarding Operations

**Standard Onboarding Process:**
```
Step 1: Signup → Auto WhatsApp welcome with video tutorial link
Step 2: Day 1 check-in call (15 min) — set up their top 50 medicines / doctor schedule
Step 3: Day 3 check-in WhatsApp — is it working?
Step 4: Day 7 success review — what value have they got so far?
Step 5: Day 14 conversion call (if on free trial)
Step 6: Day 30 NPS survey + upsell opportunity
```

**Onboarding Time Target:**
- Pharmacy: Fully operational in 2 hours (medicines added, billing live, expiry tracking on)
- Clinic: Fully operational in 3 hours (doctor schedule set, WhatsApp bot live, voice agent active)
- Hospital: 1–2 days (more complex, dedicated implementation support)

### 5.3 Quality Assurance Operations

- Monthly audit of AI voice call transcripts (random 5% sample)
- Monthly OCR accuracy check on prescription readings
- Quarterly security audit
- Monthly uptime review (target: 99.9%)
- Daily automated system health checks via monitoring dashboard

---

## 6. LEGAL & COMPLIANCE REQUIREMENTS

### 6.1 Company Setup (Immediate — Month 1)
| Task | Timeline | Cost (Est.) |
|---|---|---|
| Register Private Limited Company | Week 1–2 | ₹15,000–25,000 |
| GST Registration | Week 2–3 | ₹2,000–5,000 |
| MSME Registration (Udyam) | Week 2 | Free |
| Open current bank account | Week 2 | ₹5,000–10,000 min balance |
| Trademark application "HealthcareWale" | Month 2 | ₹5,000–10,000 |
| Domain + SSL certificate | Week 1 | ₹2,000–5,000/year |

### 6.2 Healthcare Compliance (Before Launch)
| Regulation | Requirement | Action |
|---|---|---|
| Telemedicine Guidelines 2020 | Teleconsult only with registered RMPs | Doctor NMC/state registration verification mandatory |
| DPDP Act 2023 | Patient consent, data privacy, breach notification | Consent management system, privacy policy in Hindi/Bengali |
| Drugs & Cosmetics Act | No prescription-free dispensing of Schedule H drugs | OCR system must flag Schedule H; prescription verification mandatory |
| ABDM Guidelines | ABHA integration, FHIR compliance | Register on ABDM developer portal; sandbox testing |
| IT Act 2000 | Intermediary liability protection | Terms of service clearly defining intermediary role |
| Consumer Protection Act 2019 | Refund, grievance redressal | Refund policy, grievance officer appointment |

### 6.3 Data Handling Policy
- All patient health data stored in AWS Mumbai (Indian data residency)
- Encryption: AES-256 at rest, TLS 1.3 in transit
- Patient data never sold to third parties without explicit opt-in consent
- Anonymized, aggregated data may be used for analytics products
- Right to erasure: Patient can request data deletion within 30 days
- Data retention per Indian medical records guidelines (7 years for health records)

### 6.4 E-Pharmacy Compliance Position
**Position:** HealthcareWale operates as a **technology aggregator/intermediary**, NOT as an e-pharmacy. The platform connects patients with licensed, physical pharmacies. Licensed pharmacists at partner pharmacies fulfill all orders. HealthcareWale does not stock, store, or directly dispense medicines. This positions the platform as an IT intermediary under the IT Act, similar to how Zomato/Swiggy is a food aggregator, not a restaurant.

---

## 7. FINANCIAL REQUIREMENTS

### 7.1 Startup Capital Requirement

**Bootstrap Budget (Self-Funded — First 6 Months):**

| Category | Month 1 | Month 2–3 | Month 4–6 | Total |
|---|---|---|---|---|
| Company Registration + Legal | ₹40,000 | — | — | ₹40,000 |
| AWS Hosting + Setup | ₹20,000 | ₹15,000/mo | ₹20,000/mo | ₹1,25,000 |
| WhatsApp API (Interakt) | ₹5,000 | ₹5,000/mo | ₹8,000/mo | ₹51,000 |
| Exotel (Voice) | ₹5,000 | ₹8,000/mo | ₹15,000/mo | ₹67,000 |
| AI API (Claude/OpenAI) | ₹5,000 | ₹8,000/mo | ₹12,000/mo | ₹57,000 |
| Domain + Tools + Misc SaaS | ₹10,000 | ₹5,000/mo | ₹5,000/mo | ₹40,000 |
| Marketing (Ads + Print) | ₹30,000 | ₹30,000/mo | ₹50,000/mo | ₹2,30,000 |
| Field Travel + Demos | ₹15,000 | ₹20,000/mo | ₹25,000/mo | ₹1,10,000 |
| Freelancer/Part-time Help | ₹0 | ₹20,000/mo | ₹30,000/mo | ₹1,00,000 |
| Buffer/Emergency | ₹50,000 | — | — | ₹50,000 |
| **TOTAL** | **₹1,80,000** | **₹1,11,000/mo** | **₹1,65,000/mo** | **~₹8.5 Lakh** |

**Minimum viable capital needed to launch and reach Month 7 profitability: ₹8–10 Lakh**

### 7.2 Seed Funding Plan (Month 6–12)

**When to raise:** After reaching 200+ paying customers and ₹2L+ MRR (proof of product-market fit)

**How much to raise:** ₹2–5 Crore Seed round

**Use of funds:**
- 40% → Engineering team (2–3 developers)
- 25% → Sales & marketing (field team in UP + WB)
- 20% → Customer success and support team
- 10% → Infrastructure scaling
- 5% → Legal, compliance, misc

**Target investors:**
- India-focused healthcare VC: Healthquad, Kae Capital, Stellaris
- Angel investors: IIT/IIM alumni networks, Ex-healthcare professionals
- Government grants: Startup India, BIRAC (healthcare innovation grants), WB startup scheme

### 7.3 Unit Economics (At Scale)

| Metric | Pharmacy | Clinic | Hospital |
|---|---|---|---|
| Average MRR | ₹599 | ₹999 | ₹7,999 |
| Gross margin | 65% | 68% | 72% |
| CAC (Customer Acquisition Cost) | ₹800–1,500 | ₹2,000–4,000 | ₹8,000–20,000 |
| LTV (Customer Lifetime Value, 3yr) | ₹12,500 | ₹28,000 | ₹2,15,000 |
| LTV:CAC Ratio | 8:1 | 7:1 | 15:1 |
| Payback period | 2–3 months | 3–4 months | 3–4 months |

> LTV:CAC of 3:1+ is considered healthy for SaaS. HealthcareWale targets 7:1+ which is excellent.

---

## 8. HUMAN RESOURCE REQUIREMENTS

### 8.1 Founding Team (Phase 1 — Month 1–6)

| Role | Person | Responsibility |
|---|---|---|
| Founder / CEO / Super Admin | Amit Saroj | Product, tech, sales, strategy — everything |
| Part-time Field Sales Agent | Hire locally | 20 store visits/day in target city |
| Part-time Customer Support | Hire remotely | Handle WhatsApp queries, onboarding calls |
| Freelance UI Designer | Contract | App screens, marketing materials |

**Total Phase 1 payroll: ₹50,000–80,000/month**

### 8.2 Phase 2 Team (Month 7–18)

| Role | Count | Monthly Cost |
|---|---|---|
| Full-Stack Developer (Node.js) | 2 | ₹60,000–80,000 each |
| React Native Developer | 1 | ₹50,000–70,000 |
| AI/ML Engineer (Part-time) | 1 | ₹40,000–60,000 |
| Sales Manager (UP) | 1 | ₹35,000 + commission |
| Sales Executive (WB) | 2 | ₹20,000 + commission each |
| Customer Success | 2 | ₹20,000–25,000 each |
| Marketing (Digital) | 1 | ₹30,000–40,000 |

**Total Phase 2 payroll: ₹4–6 Lakh/month**

### 8.3 Phase 3 Team (Month 19–36) — 50–80 People

| Department | Head Count |
|---|---|
| Engineering | 15–20 |
| Product | 3–5 |
| Sales (multi-state) | 15–20 |
| Customer Success | 8–12 |
| Marketing | 4–6 |
| Finance & Legal | 3–4 |
| HR & Admin | 2–3 |
| Leadership (VPs) | 3–5 |

---

## 9. TECHNOLOGY PROCUREMENT REQUIREMENTS

### 9.1 Immediate Procurement (Before Launch)

| Service | Provider | Action Required | Est. Setup Time |
|---|---|---|---|
| WhatsApp Business API | Interakt.ai | Apply for BSP account, Meta business verification | 5–7 business days |
| Indian Telephony | Exotel | Sign up, get virtual number, configure IVR | 2–3 days |
| Voice AI (Hindi/Bengali) | Sarvam AI | API access request, sandbox testing | 3–5 days |
| LLM API | Anthropic (Claude) | API key, set up rate limits | 1 day |
| Payment Gateway | Razorpay | Business account, KYC verification | 2–3 days |
| Cloud Hosting | AWS Mumbai | Account setup, VPC, RDS, EC2 | 2–3 days |
| Domain + Email | GoDaddy / Cloudflare | healthcarewale.in registration | 1 day |
| ABDM Sandbox | NHA (abdm.gov.in) | Developer registration, sandbox access | 3–7 days |
| OCR | Google Cloud Vision | GCP account, API enable | 1 day |
| SMS | Twilio / TextLocal | Account + DLT registration (mandatory in India) | 5–7 days |
| n8n | Self-hosted on EC2 | Install on EC2 instance | 1 day |
| Error Tracking | Sentry | Free tier signup | 1 hour |
| Analytics | Mixpanel | Free tier signup, SDK integration | 1 day |

**⚠️ DLT Registration (Important for India SMS):**
All SMS sent in India must be registered on TRAI's Distributed Ledger Technology portal via your telecom provider. Without DLT, SMS will not be delivered. This takes 5–7 days. Do this on Day 1.

### 9.2 Development Tools
| Tool | Purpose | Cost |
|---|---|---|
| GitHub | Code repository (private repos) | Free / ₹400/month |
| Linear | Project management | Free / ₹1,200/month |
| Figma | UI design | Free / ₹1,200/month |
| Postman | API testing | Free |
| DataDog / Grafana | Monitoring | ₹0–3,000/month |
| Notion | Documentation | Free / ₹800/month |
| Loom | Video recording for demos | Free / ₹800/month |
| Intercom / Freshdesk | Customer support CRM | ₹2,000–5,000/month |

---

## 10. RISK REGISTER

| Risk | Probability | Impact | Mitigation |
|---|---|---|---|
| E-pharmacy regulation change | High | High | Position as aggregator not seller; legal counsel on standby |
| WhatsApp API suspended by Meta | Medium | Critical | Build SMS + voice as equal backup channels simultaneously |
| Low conversion from free to paid | Medium | High | Shorten trial to 7 days; do more personal onboarding |
| Key staff leaves suddenly | Low | High | Document everything; no single point of failure |
| AWS outage in Mumbai region | Low | High | Multi-AZ setup; automated failover |
| Competitor copies features | High | Medium | Build faster; focus on distribution and relationships as moat |
| Data breach | Low | Critical | Security audits; cyber insurance; DPDP Act breach protocol |
| WB political risk (state scheme changes) | Medium | Medium | Lead with Swasthya Sathi integration; don't rely only on PMJAY |
| Cash flow crunch before revenue | Medium | High | Keep 6-month runway in bank always |
| Indian language AI quality insufficient | Medium | High | Test extensively before launch; Bhashini backup for Sarvam |
| Doctor resistance to technology | High | Medium | Let clinic managers / receptionists adopt first; avoid doctor-first sales |
| Regulatory: CDSCO notice for medicine delivery | Medium | High | Intermediary model; legal opinion documented |

---

## 11. SUCCESS CRITERIA

### 11.1 Product Success
- [ ] AI voice agent successfully handles 85%+ calls without human intervention
- [ ] Prescription OCR accuracy >85% for printed, >70% for handwritten
- [ ] Platform uptime >99.9%
- [ ] App loads in <3 seconds on 3G connection
- [ ] Billing works fully offline and syncs correctly on reconnect
- [ ] Zero double-booking incidents in appointment system

### 11.2 Business Success
- [ ] 100 paying customers by Month 6
- [ ] Monthly churn <5%
- [ ] MRR growing 20%+ month-over-month for first 12 months
- [ ] LTV:CAC ratio >5:1
- [ ] Cash-flow positive by Month 7–9
- [ ] NPS score >40 by Month 6

### 11.3 Mission Success
- [ ] Measurable reduction in medicine expiry losses for pharmacy customers
- [ ] Measurable reduction in no-show rates for clinic customers
- [ ] PMJAY claim acceptance rate >90% for hospital customers
- [ ] Patient wait time reduction >30% for clinic customers

---

## 12. EXIT STRATEGY

> This section is for long-term planning and investor conversations.

### 12.1 Potential Exit Paths (5–7 Year Horizon)

**Strategic Acquisition (Most Likely)**
- Buyers: Tata Health (backed by Tata Digital), Reliance Netmeds, Apollo Health, Manipal Hospitals, MediBuddy
- Why they'd buy: HealthcareWale's semi-urban market penetration, pharmacy network, and AI voice infrastructure are difficult to replicate
- Acquisition valuation multiple: 8–15x ARR for profitable Indian healthtech SaaS
- At ₹15 Crore ARR: Acquisition value = ₹120–225 Crore

**IPO (If scale reaches ₹100+ Crore ARR)**
- Possible via NSE Emerge or mainboard if scale warrants
- Timeline: 7–10 years from founding

**Secondary Sale / Private Equity**
- PE firms acquiring profitable Indian SaaS businesses at 6–10x ARR
- Possible at ₹25+ Crore ARR with >15% net margins

### 12.2 Amit's (Founder) Exit Options
- Partial secondary sale to VC at Series B/C — personal liquidity without full exit
- Full acquisition exit — typical 2–3 year earnout with acquiring company
- Stay on as CEO post-acquisition if structure allows

---

*HealthcareWale — Business Requirements Document v1.0 — May 2026*
*Prepared by: Claude (Anthropic) for Amit Saroj, Founder & Super Admin*
