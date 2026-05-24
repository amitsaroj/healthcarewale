# COMPLETE USER FLOW & PLATFORM JOURNEY BLUEPRINT

# HealthcareWale — End-to-End Product Workflow Documentation

## Purpose of This Document

This document defines the complete operational journey of every user type inside HealthcareWale.

It covers:
- patient journey
- clinic workflow
- pharmacy workflow
- hospital workflow
- distributor workflow
- admin workflow
- AI workflows
- onboarding flows
- payment flows
- support flows
- seller onboarding
- delivery flows
- compliance flows
- edge-case flows

This document should act as:
- product blueprint
- UX architecture reference
- frontend development guide
- backend workflow guide
- AI automation reference
- investor-readiness documentation

---

# 1. USER TYPES INSIDE HEALTHCAREWALE

## Primary User Roles

### 1. Patient/User
Books appointments, orders medicines, tracks reports.

### 2. Clinic Receptionist
Handles appointments, queues, follow-ups.

### 3. Doctor
Views patients, prescriptions, schedules.

### 4. Pharmacy Owner
Manages inventory, billing, supplier orders.

### 5. Hospital Admin
Handles departments, staff, claims, beds.

### 6. Distributor/Supplier
Manages medicine supply chain.

### 7. Delivery Partner
Handles medicine deliveries.

### 8. Super Admin
Controls platform-wide operations.

### 9. Support Executive
Handles customer issues.

### 10. AI Agent
Automated workflows and communication.

---

# 2. PATIENT APP FLOW

# A. USER REGISTRATION FLOW

## Step 1 — App Install or WhatsApp Entry

User enters platform via:
- Android app
- iOS app
- PWA
- WhatsApp
- website
- QR code at clinic
- referral link

---

## Step 2 — Language Selection

User selects:
- Hindi
- Bengali
- English
- Bhojpuri

Platform stores language preference.

---

## Step 3 — Mobile Verification

User enters:
- phone number

System sends:
- OTP via SMS
- WhatsApp OTP fallback

---

## Step 4 — Basic Profile Setup

User enters:
- name
- age
- gender
- city
- blood group
- emergency contact

Optional:
- ABHA ID
- insurance ID

---

## Step 5 — Family Member Creation

User can add:
- parents
- children
- spouse

Each gets separate health profile.

---

# B. LOGIN FLOW

## Login Methods

- OTP login
- WhatsApp login
- Google login
- ABHA login

---

## Security Layer

- device recognition
- suspicious login detection
- session timeout
- biometric login optional

---

# C. HOME SCREEN FLOW

## Dashboard Sections

- upcoming appointments
- medicine reminders
- reorder medicines
- lab reports
- AI assistant
- nearby clinics
- emergency support

---

# D. APPOINTMENT BOOKING FLOW

## Step 1 — Search Doctor/Clinic

Search by:
- specialty
- clinic name
- city
- symptoms
- language

---

## Step 2 — Select Time Slot

System shows:
- available slots
- queue load
- waiting estimate
- consultation fee

---

## Step 3 — Booking Confirmation

User receives:
- WhatsApp confirmation
- token number
- Google Calendar sync
- reminder schedule

---

## Step 4 — AI Reminder Workflow

System sends:
- 24-hour reminder
- 2-hour reminder
- missed appointment follow-up

---

# E. VIRTUAL WAITING ROOM FLOW

## Features

User can:
- monitor live queue
- estimate wait time
- receive turn alerts
- delay arrival

---

# F. TELECONSULTATION FLOW

## Pre-Consultation

User uploads:
- symptoms
- reports
- prescriptions

---

## During Consultation

Features:
- video call
- voice call
- chat
- live prescription

---

## Post Consultation

User receives:
- digital prescription
- medicine suggestions
- follow-up reminders

---

# G. MEDICINE ORDERING FLOW

## Step 1 — Upload Prescription

Methods:
- camera upload
- gallery upload
- WhatsApp upload

---

## Step 2 — OCR Processing

AI extracts:
- medicines
- dosage
- duration

---

## Step 3 — Pharmacist Verification

Human verification mandatory.

---

## Step 4 — Payment & Delivery

Options:
- COD
- UPI
- card
- wallet

---

## Step 5 — Delivery Tracking

User sees:
- rider status
- ETA
- proof of delivery

---

# H. LAB TEST BOOKING FLOW

## User Journey

- select test
- choose home collection
- choose slot
- payment
- sample collection
- report delivery

---

# I. PATIENT SUPPORT FLOW

## Channels

- WhatsApp
- AI chatbot
- voice assistant
- live support

---

# 3. CLINIC FLOW

# A. CLINIC REGISTRATION FLOW

## Step 1 — Owner Signup

Required:
- clinic name
- doctor details
- GST optional
- address
- license documents

---

## Step 2 — Verification

Team verifies:
- doctor registration
- clinic authenticity
- KYC

---

## Step 3 — Subscription Selection

Plans:
- starter
- growth
- enterprise

---

## Step 4 — Onboarding

Setup:
- doctors
- timings
- rooms
- queues
- WhatsApp templates
- staff accounts

---

# B. RECEPTIONIST FLOW

## Dashboard Functions

- add patient
- manage queue
- confirm appointments
- billing
- follow-up calls
- AI assistant

---

## Walk-in Flow

Receptionist:
- creates token
- assigns doctor
- collects payment
- updates status

---

# C. DOCTOR FLOW

## Doctor Dashboard

Features:
- patient history
- live queue
- prescriptions
- diagnostics requests
- follow-up scheduling

---

## Prescription Flow

Doctor can:
- type prescription
- voice dictate
- select medicine templates

---

# D. FOLLOW-UP AUTOMATION FLOW

System automatically:
- schedules reminders
- sends WhatsApp messages
- triggers AI voice calls

---

# 4. PHARMACY FLOW

# A. PHARMACY ONBOARDING

## Required Information

- pharmacy license
- GST number
- owner KYC
- distributor details

---

# B. BILLING FLOW

## Fast Billing System

Methods:
- barcode scan
- medicine search
- voice billing

---

## GST Calculation

System automatically:
- calculates GST
- prints invoice
- syncs reports

---

# C. INVENTORY FLOW

## Stock Entry

Methods:
- manual
- CSV import
- distributor sync
- voice update

---

## Inventory Alerts

System warns:
- low stock
- near expiry
- dead stock

---

# D. SUPPLIER ORDER FLOW

## Auto Reorder Logic

AI predicts:
- fast-moving inventory
- seasonal demand
- reorder timing

---

## Supplier Communication

Orders via:
- WhatsApp
- API
- AI calls
- distributor app

---

# E. DELIVERY FLOW

## Pharmacy Delivery Process

- order received
- packaging
- rider assignment
- tracking
- delivery confirmation

---

# 5. HOSPITAL FLOW

# A. HOSPITAL REGISTRATION

Requirements:
- hospital license
- departments
- bed count
- admin users

---

# B. OPD FLOW

- patient registration
- token assignment
- consultation
- billing
- pharmacy
- diagnostics

---

# C. IPD FLOW

- admission
- bed assignment
- treatment tracking
- discharge summary
- billing

---

# D. PMJAY CLAIM FLOW

## Steps

- patient eligibility verification
- document upload
- treatment package selection
- claim submission
- approval tracking

---

# 6. DISTRIBUTOR FLOW

# A. DISTRIBUTOR REGISTRATION

Requirements:
- distributor license
- warehouse details
- territories

---

# B. ORDER COLLECTION FLOW

Methods:
- AI voice calls
- WhatsApp orders
- retailer portal
- sales rep entry

---

# C. DELIVERY MANAGEMENT FLOW

Features:
- route planning
- dispatch tracking
- invoice generation
- retailer confirmation

---

# 7. DELIVERY PARTNER FLOW

## Workflow

- login
- order assignment
- pickup
- navigation
- OTP verification
- delivery proof

---

# 8. SUPER ADMIN FLOW

# A. PLATFORM DASHBOARD

Admin can monitor:
- revenue
- AI usage
- customer growth
- churn
- support load
- medicine transactions

---

# B. CUSTOMER MANAGEMENT

Actions:
- activate/deactivate accounts
- manage subscriptions
- refunds
- issue resolution

---

# C. AI CONTROL PANEL

Admin monitors:
- AI calls
- hallucination alerts
- failed workflows
- escalation rates

---

# 9. SUPPORT FLOW

## Ticket Creation

Users can create tickets via:
- app
- WhatsApp
- email
- AI assistant

---

## Ticket Routing

System categorizes:
- technical
- billing
- medical workflow
- delivery issue

---

# 10. PAYMENT FLOW

# Supported Methods

- UPI
- cards
- COD
- net banking
- wallet

---

# Subscription Billing

Features:
- auto-renewal
- invoice generation
- GST invoices
- failed payment recovery

---

# 11. AI WORKFLOW SYSTEM

# AI Voice Calls

Use cases:
- reminders
- follow-ups
- reorder collection
- appointment booking

---

# AI Chatbot

Handles:
- FAQs
- booking assistance
- medicine reminders
- clinic information

---

# Human Escalation

AI escalates when:
- confidence low
- medical ambiguity
- angry customer
- failed workflow

---

# 12. WHATSAPP AUTOMATION FLOW

## Features

- appointment booking
- medicine reminders
- queue updates
- invoice delivery
- reports
- support

---

# 13. COMPLIANCE FLOW

# User Consent

Before AI interactions:
- consent collection
- privacy policy agreement
- recording permissions

---

# Data Protection

System implements:
- encryption
- audit logs
- access controls
- deletion workflows

---

# 14. EDGE CASES

# Internet Failure

Fallbacks:
- offline cache
- SMS backup
- local sync

---

# AI Failure

Fallback:
- human takeover
- support escalation

---

# Delivery Failure

System:
- retries
- reassignment
- refund workflows

---

# 15. MONETIZATION FLOWS

Revenue sources:
- SaaS subscriptions
- AI call billing
- WhatsApp charges
- medicine commissions
- diagnostics commissions
- PMJAY filing fees
- analytics subscriptions

---

# 16. SECURITY FLOW

## Security Layers

- OTP verification
- RBAC
- device tracking
- encrypted PHI
- session monitoring
- suspicious activity alerts

---

# 17. ANALYTICS FLOW

## Metrics

- patient retention
- inventory turnover
- no-show rates
- AI automation savings
- revenue analytics
- doctor productivity

---

# 18. FUTURE EXPANSION FLOWS

Potential future modules:
- insurance
- financing
- biomedical waste management
- ambulance coordination
- rural health workers
- wearable integrations

---

# FINAL STRATEGIC INSIGHT

HealthcareWale is not just an app.

It is:

# an operational infrastructure platform for Indian healthcare businesses.

The success of the platform depends less on fancy AI and more on:
- operational reliability
- low-tech usability
- multilingual workflows
- fast onboarding
- WhatsApp-native experiences
- workflow automation
- trust.
