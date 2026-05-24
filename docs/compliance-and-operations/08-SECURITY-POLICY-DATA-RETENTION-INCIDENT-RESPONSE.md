# 🔐 HealthcareWale — Information Security Policy
> **Document ID:** HW-SEC-001 | **Version:** 1.0 | **Effective Date:** [Insert Date]  
> **Aligned With:** SOC 2 Type II · ISO 27001:2022 · DPDP Act 2023 · OWASP Top 10 · NIST Cybersecurity Framework  
> **Document Owner:** CTO / Engineering Lead — HealthcareWale Technologies Pvt. Ltd.

---

## 1. PURPOSE & SCOPE

This Information Security Policy establishes the technical, organizational, and physical controls required to protect the confidentiality, integrity, and availability of all data processed by HealthcareWale — including patient health records, pharmacy inventory data, billing records, and platform infrastructure.

**Scope:** All employees, contractors, vendors, and systems that access, process, or store HealthcareWale data.

---

## 2. DATA CLASSIFICATION

| Classification | Description | Examples | Controls |
|---|---|---|---|
| **Critical — PHI** | Patient health information | Prescriptions, diagnoses, lab reports, ABHA IDs | AES-256 encryption, strict RBAC, audit log every access |
| **Critical — PII** | Personally identifiable information | Name, phone, Aadhaar reference, bank details | AES-256 encryption, masked in logs |
| **Confidential** | Business-sensitive data | Revenue data, customer contracts, source code | Encrypted storage, NDA-protected access |
| **Internal** | Operational data | Staff schedules, support tickets, analytics | Password-protected access |
| **Public** | Publicly available | Marketing content, public API docs | No special controls |

---

## 3. ENCRYPTION STANDARDS

### 3.1 Data at Rest
| Data Store | Encryption Standard | Key Management |
|---|---|---|
| PostgreSQL (RDS) | AES-256 (AWS RDS encryption enabled) | AWS KMS — customer-managed key |
| MongoDB Atlas | AES-256 (Atlas encryption at rest) | Atlas KMS |
| AWS S3 (files) | AES-256 (SSE-KMS) | AWS KMS |
| Redis (ElastiCache) | AES-256 (in-transit + at-rest encryption) | AWS KMS |
| Local device (mobile app) | AES-256 (React Native Keychain / Android Keystore) | Device hardware key |

### 3.2 Data in Transit
| Connection | Protocol | Minimum Standard |
|---|---|---|
| Client ↔ API Server | HTTPS | TLS 1.3 (TLS 1.2 minimum) |
| API Server ↔ Database | TLS | TLS 1.2 minimum |
| API Server ↔ External APIs | HTTPS | TLS 1.3 |
| WebSocket (real-time queue) | WSS | TLS 1.3 |
| Video calls | WebRTC | DTLS-SRTP |

### 3.3 Key Rotation
- AES encryption keys rotated annually via AWS KMS automatic rotation
- JWT signing secrets rotated every 90 days
- API keys for external services rotated every 180 days
- Compromised keys rotated immediately upon detection

---

## 4. ACCESS CONTROL

### 4.1 Role-Based Access Control (RBAC) Matrix

| Role | Patient Records | Billing Data | Inventory | System Admin | AI Logs |
|---|---|---|---|---|---|
| Super Admin (Amit) | ✅ Full | ✅ Full | ✅ Full | ✅ Full | ✅ Full |
| Engineering (Developer) | ❌ Prod access blocked | ❌ Prod access blocked | ❌ | ✅ Limited | ✅ Anonymized |
| Customer Support | ✅ Read only (masked) | ✅ Read only | ❌ | ❌ | ❌ |
| Doctor | ✅ Own patients only | ✅ Own billing only | ❌ | ❌ | ❌ |
| Pharmacist | ✅ Prescription only | ✅ Own store only | ✅ Own store | ❌ | ❌ |
| Distributor | ❌ | ✅ Own invoices | ✅ Aggregate | ❌ | ❌ |
| Patient | ✅ Own records only | ✅ Own bills only | ❌ | ❌ | ❌ |

### 4.2 Authentication Requirements
- **All users:** Mobile OTP (TOTP) for login
- **Admin accounts:** Mandatory 2FA (TOTP authenticator app)
- **Staff accounts:** Username + password + 2FA
- **API access:** JWT Bearer tokens — 30-minute access token, 7-day refresh token
- **Production server access:** SSH key pairs only; no password-based SSH; keys stored in AWS Secrets Manager
- **Database access:** No direct production DB access from developer machines; only via VPN + bastion host

### 4.3 Zero Trust Network Architecture

```
Internet → Cloudflare WAF (DDoS, WAF rules)
                │
                ▼
         AWS ALB (Load Balancer — HTTPS termination)
                │
                ▼
         AWS VPC Private Subnet
                │
         ┌──────┴──────────────────┐
         ▼                         ▼
    ECS App Containers         n8n / Worker Containers
    (No direct internet)       (No direct internet)
         │                         │
         ▼                         ▼
    RDS PostgreSQL             Redis ElastiCache
    (Private subnet)           (Private subnet)
         │
         ▼
    AWS S3 (VPC Endpoint — no internet traversal)
```

---

## 5. MULTI-TENANT DATA ISOLATION

HealthcareWale is a multi-tenant SaaS platform. Data isolation between tenants (clinics, pharmacies, hospitals) is enforced at:

**Database Level (PostgreSQL):**
```sql
-- Row-Level Security policy example
CREATE POLICY tenant_isolation ON appointments
  USING (tenant_id = current_setting('app.tenant_id')::uuid);

ALTER TABLE appointments ENABLE ROW LEVEL SECURITY;
```

Every query is executed with the tenant's ID set in the PostgreSQL session context. A clinic cannot access another clinic's patient data even with a valid session token.

**API Level:**
Every API request extracts `tenant_id` from the JWT token claims. Requests without a valid tenant context are rejected with 403 Forbidden.

**Logging Level:**
Logs are tagged with `tenant_id` but tenant-level logs are isolated — tenants cannot view each other's logs.

---

## 6. VULNERABILITY MANAGEMENT

### 6.1 SAST/DAST (Automated Scanning)
- **SAST (Static Analysis):** GitHub Actions runs CodeQL on every pull request — critical and high vulnerabilities block merge
- **DAST (Dynamic Analysis):** OWASP ZAP run against staging environment before every major release
- **Dependency scanning:** npm audit + Dependabot alerts for vulnerable packages — critical patches within 24 hours

### 6.2 Penetration Testing
- **Phase 1:** Internal testing using OWASP Top 10 checklist before launch
- **Phase 2+:** Annual external penetration test by a qualified third-party security firm (CERT-IN empanelled firm preferred)
- Penetration test findings: Critical — remediated within 7 days; High — within 30 days; Medium — within 90 days

### 6.3 Bug Bounty Program (Phase 2)
- Responsible disclosure policy published at security@healthcarewale.in
- Rewards for valid vulnerabilities: ₹5,000–₹2,00,000 depending on severity

---

## 7. AUDIT LOGGING

Every sensitive operation is logged with:

| Field | Description |
|---|---|
| `event_id` | Unique event identifier |
| `timestamp` | UTC timestamp (ISO 8601) |
| `user_id` | User performing the action |
| `tenant_id` | Tenant context |
| `action` | CREATE / READ / UPDATE / DELETE |
| `resource` | Resource type (patient, prescription, bill, etc.) |
| `resource_id` | ID of affected resource |
| `ip_address` | Source IP (masked for patient-facing logs) |
| `user_agent` | Browser/app identifier |
| `result` | SUCCESS / FAILURE |
| `reason` | Failure reason if applicable |

**Audit logs are:**
- Written to MongoDB (append-only collection — no delete capability for application users)
- Retained for 3 years
- Protected against tampering (write-once S3 backup with Object Lock)
- Reviewed monthly by Security Officer

---
---

# 🗑️ HealthcareWale — Data Retention & Secure Destruction Policy
> **Document ID:** HW-DATA-001 | **Version:** 1.0 | **Effective Date:** [Insert Date]

---

## 1. RETENTION SCHEDULE

| Data Category | Retention Period | Storage Location | Destruction Method |
|---|---|---|---|
| Patient health records (prescriptions, diagnoses) | 7 years from last activity | PostgreSQL + S3 | Cryptographic erasure + logical deletion |
| Appointment records | 5 years | PostgreSQL | Logical deletion + backup overwrite |
| GST invoices / financial records | 8 years | PostgreSQL + S3 | Cryptographic erasure |
| AI voice call recordings | 30 days | S3 (lifecycle policy) | AWS S3 auto-expiry |
| WhatsApp transcripts (active) | 90 days active | MongoDB | TTL index auto-deletion |
| WhatsApp transcripts (archived) | 2 years | S3 | Cryptographic erasure |
| Audit logs | 3 years | MongoDB + S3 | Cryptographic erasure |
| Delivery records | 1 year | PostgreSQL | Logical deletion |
| Staff/HR data | 5 years | PostgreSQL | Cryptographic erasure |
| System logs (application) | 90 days | AWS CloudWatch | Auto-expiry |
| Backup snapshots | 7-day rolling | AWS RDS automated | AWS auto-rotation |
| Marketing consent records | 3 years post opt-out | PostgreSQL | Logical deletion |
| Security incident records | 5 years | S3 (separate bucket) | Manual review before deletion |

---

## 2. SECURE DESTRUCTION PROCEDURES

### 2.1 Cryptographic Erasure
For all encrypted data stores:
1. Destroy the encryption key for the specific data (via AWS KMS key deletion)
2. The ciphertext without the key is computationally irretrievable
3. Log key destruction event in audit trail

### 2.2 Database Record Deletion
```sql
-- Soft delete first (mark for deletion, remove from app access)
UPDATE patients SET deleted_at = NOW(), deletion_requested_by = [user_id] 
WHERE id = [patient_id];

-- Hard delete after retention period expires (automated job)
DELETE FROM patients WHERE deleted_at < NOW() - INTERVAL '30 days';
```

### 2.3 S3 File Deletion
- S3 Object Lifecycle rules auto-expire files after retention period
- Versioned objects: All versions deleted (not just current version)
- S3 MFA Delete enabled for sensitive buckets (prevents accidental or malicious mass deletion)

### 2.4 Backup Deletion
- Automated RDS backups: 7-day retention window; AWS auto-deletes beyond this
- Manual backup deletion: Requires two-person authorization (Super Admin + Engineering Lead)

### 2.5 Patient Account Deletion Request
When patient requests account deletion:
1. Account marked `deleted_at` immediately — no app access
2. Data retained for 30 days (legal dispute window)
3. After 30 days: All personal identifiers cryptographically erased or deleted
4. Health records required by law (7 years) are de-identified (not deleted) and retained in anonymized form
5. Patient receives confirmation: "Your account and personal data have been deleted. Anonymized health records are retained per Indian medical law for [X] years."
6. Confirmation email/WhatsApp with deletion receipt

---
---

# 🚨 HealthcareWale — Incident Response & Data Breach Protocol
> **Document ID:** HW-IR-001 | **Version:** 1.0 | **Effective Date:** [Insert Date]

---

## 1. INCIDENT CLASSIFICATION

| Severity | Description | Examples | Response Time |
|---|---|---|---|
| **P0 — Critical** | Active data breach; unauthorized PHI access; ransomware | Database exfiltrated; patient records on dark web | **Immediate — within 1 hour** |
| **P1 — High** | Suspected breach; significant vulnerability exploited; service outage >2 hours | Unusual data access pattern; production DB unreachable | **Within 4 hours** |
| **P2 — Medium** | Security vulnerability discovered; partial service degradation | CVE in a dependency; API slowdown | **Within 24 hours** |
| **P3 — Low** | Minor security issue; no data exposure; single user affected | Brute force attempt blocked; single account anomaly | **Within 7 days** |

---

## 2. INCIDENT RESPONSE TEAM

| Role | Phase 1 Assignment | Responsibility |
|---|---|---|
| **Incident Commander** | Amit Saroj (Founder) | Overall response coordination |
| **Technical Lead** | Engineering Lead | Contain breach, preserve evidence, implement fix |
| **Communications Lead** | Founder (Phase 1) | Customer notification, regulatory notification, PR |
| **Legal Advisor** | External counsel (on-call) | Regulatory obligation assessment, litigation risk |
| **Customer Success** | Support Lead | Handle customer queries during incident |

---

## 3. INCIDENT RESPONSE PLAYBOOK

### Phase 1: Detection & Triage (0–1 hour)

```
Incident Detected (alert / customer report / monitoring)
         │
         ▼
Incident Commander notified immediately (WhatsApp + call)
         │
         ▼
Initial severity classification (P0/P1/P2/P3)
         │
         ▼
Incident Response Team activated (for P0/P1)
         │
         ▼
Create incident channel: Slack #incident-[DATE]-[ID]
Log in Incident Register: timestamp, reporter, description, initial severity
```

### Phase 2: Containment (1–4 hours for P0)

**For Data Breach (P0):**
1. Immediately isolate affected systems (take offline if necessary)
2. Revoke all active sessions for potentially compromised accounts
3. Block malicious IP addresses at Cloudflare WAF
4. Take forensic snapshot of affected systems (DO NOT wipe before forensics)
5. Disable compromised API keys / access credentials
6. Preserve all logs (CloudWatch, audit logs, application logs)

**For Ransomware:**
1. Immediately disconnect affected instances from VPC
2. Do NOT pay ransom — escalate to CERT-IN
3. Initiate recovery from last clean backup (confirmed clean)
4. Preserve encrypted systems for forensic analysis

### Phase 3: Eradication & Recovery (4–48 hours)

1. Identify root cause (vulnerability, misconfiguration, insider threat, phishing)
2. Patch or remediate the vulnerability
3. Scan all systems for indicators of compromise
4. Restore from clean backup if data integrity compromised
5. Progressive service restoration: 10% → 50% → 100% with monitoring at each stage
6. Verify all patient data integrity post-restoration

### Phase 4: Regulatory Notification

**Under DPDP Act 2023 (India):**
- Notify **Data Protection Board of India:** Within **72 hours** of becoming aware of a personal data breach
- Notify **affected patients:** As soon as practicable after notification to Board (if breach poses high risk)
- Notification content: Nature of breach, data affected, likely consequences, measures taken, contact for queries

**Under GDPR (EU users — if applicable):**
- Notify supervisory authority: Within **72 hours**
- Notify affected data subjects: Without undue delay if high risk

**Under HIPAA (US users — if applicable):**
- Notify HHS OCR: Within **60 days** (for <500 individuals) or **immediately** (for 500+)
- Notify affected individuals: Within **60 days**

**Under Indian IT Act (Sec. 43A / SPDI Rules):**
- Notify CERT-IN: Per CERT-IN directions (currently 6-hour reporting for significant incidents)

### Phase 5: Customer Communication Template

**WhatsApp / Email to affected patients (P0 breach):**

```
Subject: Important Security Notice from HealthcareWale

Dear [Name],

We are writing to inform you of a security incident that may have 
affected your data on the HealthcareWale platform.

What happened: [Brief, accurate description]
Data affected: [Specific data types — no speculation]
When it occurred: [Date range]
What we have done: [Containment and remediation steps]
What you should do: [Specific actions — change password, monitor account]

We deeply regret this incident. Protecting your health data is our 
highest priority. We have reported this to the relevant authorities 
and are cooperating fully.

For questions: security@healthcarewale.in | [Support Number]

Amit Saroj, Founder, HealthcareWale
```

### Phase 6: Post-Incident Review (Within 14 days)

1. Root cause analysis document (5 Whys methodology)
2. Timeline reconstruction of incident
3. What detection mechanisms failed?
4. What containment could have been faster?
5. Updated controls, patches, or architecture changes implemented
6. Lessons learned shared with full team
7. Insurance claim filed if applicable (cyber insurance)
8. External auditor review commissioned if P0 breach involved PHI

---

## 4. CONTACT NUMBERS FOR REGULATORY NOTIFICATION

| Authority | Contact | For |
|---|---|---|
| CERT-IN | incidents@cert-in.org.in | Cybersecurity incidents |
| Data Protection Board of India | [TBD — Board not yet constituted as of May 2026] | Personal data breaches |
| NHA / ABDM | [NHA helpline] | ABHA/PMJAY data incidents |
| Cyber Crime Portal | cybercrime.gov.in | Criminal complaints |

---

*HealthcareWale Information Security Policy, Data Retention, and Incident Response Protocol v1.0 — May 2026*
