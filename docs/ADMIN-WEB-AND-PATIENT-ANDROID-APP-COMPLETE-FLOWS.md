# Admin Web & Patient Android App — Complete Detailed Flows

# Purpose

This document covers the two most critical missing layers:

1. Super Admin Web Platform
2. Patient Android Application

These are the highest-impact operational systems inside HealthcareWale.

Without clearly defined admin and patient flows:
- development becomes inconsistent
- frontend architecture becomes fragmented
- automation breaks
- analytics become unreliable
- onboarding becomes chaotic

This document defines production-grade workflow logic.

---

# PART 1 — SUPER ADMIN WEB PLATFORM

# 1. SUPER ADMIN ROLE

The Super Admin platform is the operational brain of HealthcareWale.

It manages:
- clinics
- pharmacies
- hospitals
- distributors
- AI systems
- payments
- subscriptions
- compliance
- analytics
- support
- onboarding
- escalations

---

# 2. SUPER ADMIN LOGIN FLOW

## Step 1 — Admin Login

Methods:
- email/password
- Google Workspace login
- OTP verification
- hardware security key optional

---

## Step 2 — MFA Verification

Mandatory:
- OTP
- authenticator app
- session validation

---

## Step 3 — Access Validation

System checks:
- admin role
- region permissions
- IP anomaly detection
- suspicious device detection

---

# 3. SUPER ADMIN DASHBOARD

# Dashboard Layout

## Left Sidebar

Modules:
- overview
- customers
- clinics
- pharmacies
- hospitals
- distributors
- subscriptions
- AI operations
- WhatsApp operations
- billing
- support
- analytics
- compliance
- settings

---

## Top Navigation

Features:
- global search
- alerts
- AI system status
- WhatsApp API status
- notification center
- admin profile

---

## Main Dashboard Widgets

### Revenue Metrics
- MRR
- ARR
- daily collections
- pending invoices
- churn rate

### Customer Metrics
- active clinics
- active pharmacies
- new signups
- inactive accounts

### AI Metrics
- AI calls today
- failed AI workflows
- escalation rates
- AI cost tracking

### Operational Metrics
- support tickets
- onboarding completion
- failed deliveries
- payment failures

---

# 4. CUSTOMER MANAGEMENT FLOW

# A. Customer List View

Admin can filter by:
- city
- subscription
- status
- business type
- revenue tier

---

# B. Customer Detail Page

Shows:
- owner details
- usage analytics
- invoices
- AI usage
- WhatsApp usage
- support history
- onboarding progress
- health score

---

# C. Actions Available

Admin can:
- activate account
- suspend account
- reset password
- upgrade plan
- assign onboarding staff
- trigger support call

---

# 5. ONBOARDING MANAGEMENT FLOW

# A. Onboarding Tracker

Stages:
- signup complete
- KYC submitted
- verification pending
- onboarding scheduled
- training completed
- go-live completed

---

# B. Staff Assignment

Admin assigns:
- onboarding manager
- support executive
- field engineer

---

# C. Go-Live Validation

Checklist:
- billing working
- AI configured
- WhatsApp templates approved
- printers connected
- inventory imported

---

# 6. AI OPERATIONS CENTER

# Main Features

## Live AI Calls

Monitor:
- active calls
- failed calls
- language detection
- confidence scores
- escalations

---

## AI Conversation Logs

Admin can review:
- transcripts
- voice recordings
- sentiment analysis
- error categories

---

## AI Escalation System

Escalation triggers:
- medical ambiguity
- angry users
- failed bookings
- payment disputes

---

# 7. WHATSAPP MANAGEMENT SYSTEM

# Dashboard Features

- message delivery rates
- failed conversations
- template approvals
- spam warnings
- blocked accounts

---

# WhatsApp Billing

Track:
- conversation costs
- template costs
- marketing campaigns
- utility conversations

---

# 8. SUBSCRIPTION & BILLING FLOW

# Subscription Management

Admin can:
- create plans
- assign discounts
- pause subscriptions
- issue refunds
- track failed payments

---

# Invoice System

Features:
- GST invoices
- downloadable PDFs
- payment reminders
- automated receipts

---

# 9. SUPPORT MANAGEMENT FLOW

# Ticket Dashboard

Ticket categories:
- technical
- billing
- AI issue
- delivery issue
- onboarding issue
- compliance issue

---

# Escalation Levels

## L1
Basic support

## L2
Technical team

## L3
Engineering escalation

## L4
Founder escalation

---

# 10. COMPLIANCE MANAGEMENT FLOW

# Admin Responsibilities

Track:
- consent records
- audit logs
- AI interaction logs
- PHI access history
- breach alerts

---

# Compliance Alerts

System warns for:
- unusual data access
- excessive downloads
- suspicious admin activity
- unauthorized API usage

---

# 11. ANALYTICS & BI FLOW

# Executive Dashboard

Reports:
- customer growth
- AI profitability
- pharmacy performance
- clinic retention
- city-wise growth
- churn prediction
- CAC vs LTV

---

# Predictive Analytics

AI predicts:
- churn risk
- payment defaults
- inactive customers
- high-support accounts

---

# 12. SUPER ADMIN MOBILE PANEL

# Features

- alerts
- live AI monitoring
- support escalation
- payment failures
- emergency incidents

---

# PART 2 — PATIENT ANDROID APP COMPLETE FLOW

# 13. PATIENT APP ENTRY FLOW

# Sources of Entry

User enters via:
- Play Store
- clinic QR code
- WhatsApp link
- doctor referral
- pharmacy referral
- Facebook/Instagram ads

---

# 14. SPLASH SCREEN FLOW

# App Startup

Shows:
- HealthcareWale branding
- language selector
- location permission
- internet status

---

# 15. PATIENT REGISTRATION FLOW

# Step 1 — Mobile Number

User enters phone number.

---

# Step 2 — OTP Verification

Methods:
- SMS OTP
- WhatsApp OTP fallback

---

# Step 3 — Profile Creation

Fields:
- full name
- DOB
- gender
- blood group
- city
- emergency contact

Optional:
- ABHA ID
- insurance details

---

# Step 4 — Family Profiles

Add:
- children
- parents
- spouse

Each profile separate.

---

# 16. HOME SCREEN FLOW

# Main Sections

## Quick Actions
- book appointment
- order medicine
- upload prescription
- book lab test
- emergency support

---

## Health Widgets
- upcoming appointments
- medicine reminders
- reports pending
- follow-ups due

---

## AI Assistant Widget

Functions:
- booking assistance
- medicine reminders
- FAQs
- clinic guidance

---

# 17. APPOINTMENT BOOKING FLOW

# Search Options

Search by:
- doctor
- specialty
- clinic
- symptoms
- location

---

# Doctor Profile Page

Shows:
- availability
- consultation fee
- languages spoken
- ratings
- queue estimate

---

# Slot Selection

Features:
- live slot updates
- waiting estimates
- virtual queue visibility

---

# Confirmation Flow

User receives:
- WhatsApp confirmation
- calendar sync
- reminder schedule
- token number

---

# 18. VIRTUAL WAITING ROOM FLOW

# Features

Patient sees:
- live queue
- estimated turn
- delays
- doctor running late alerts

---

# Smart Notifications

Notifications:
- "2 patients remaining"
- "doctor delayed by 15 minutes"
- "arrive now"

---

# 19. DIGITAL PRESCRIPTION FLOW

# Upload Methods

- camera
- gallery
- WhatsApp
- PDF upload

---

# OCR Extraction

AI extracts:
- medicine names
- dosage
- duration

---

# Manual Verification

Pharmacist confirms before processing.

---

# 20. MEDICINE ORDERING FLOW

# Cart System

Features:
- prescription medicines
- OTC medicines
- repeat orders
- chronic subscriptions

---

# Payment Methods

- UPI
- COD
- card
- wallet

---

# Delivery Tracking

Patient sees:
- rider location
- ETA
- OTP verification

---

# 21. LAB TEST FLOW

# Booking Steps

- select test
- choose home collection
- choose slot
- payment
- sample collection
- report upload

---

# Report Flow

Reports delivered via:
- app
- WhatsApp
- PDF download

---

# 22. PATIENT HEALTH RECORDS FLOW

# Sections

- prescriptions
- lab reports
- appointment history
- invoices
- allergies
- chronic conditions

---

# Search Features

Patient can search:
- medicine history
- doctor history
- diagnosis history

---

# 23. FOLLOW-UP & REMINDER FLOW

# Reminder Types

- medicine reminders
- appointment reminders
- lab reminders
- refill reminders

---

# AI Reminder Calls

AI calls patient when:
- medicine refill due
- follow-up missed
- chronic care overdue

---

# 24. PATIENT SUPPORT FLOW

# Support Channels

- AI chatbot
- WhatsApp support
- voice support
- live executive

---

# Escalation Logic

Escalates when:
- payment failed
- delivery delayed
- prescription unclear
- angry customer

---

# 25. PATIENT SETTINGS FLOW

# Features

- language settings
- notification settings
- privacy controls
- data export
- delete account
- biometric login

---

# 26. PATIENT REWARDS & REFERRAL FLOW

# Referral System

Patient can:
- invite friends
- earn credits
- redeem discounts

---

# Loyalty Engine

Rewards for:
- repeat bookings
- medicine orders
- referrals

---

# 27. OFFLINE & LOW-INTERNET FLOW

# Critical Requirement

App must support:
- slow internet
- offline caching
- retry systems
- compressed media

---

# Fallbacks

If internet fails:
- SMS reminders
- offline queue data
- cached prescriptions

---

# 28. SECURITY FLOW

# Security Layers

- OTP login
- device recognition
- encrypted records
- session timeout
- suspicious login alerts

---

# 29. AI PERSONALIZATION FLOW

# AI Recommendations

Suggest:
- repeat medicines
- nearby clinics
- follow-up bookings
- chronic care reminders

---

# AI Boundaries

AI cannot:
- diagnose diseases
- prescribe independently
- replace doctors

---

# 30. FINAL STRATEGIC INSIGHT

The patient app is NOT just a healthcare app.

It is:

# a healthcare relationship management platform.

The admin web platform is NOT just an admin dashboard.

It is:

# the operational command center of the HealthcareWale ecosystem.

If both are designed correctly:
- retention increases
- operational chaos decreases
- AI becomes useful
- support costs reduce
- scalability improves

If both are designed poorly:
- churn explodes
- onboarding fails
- support burden becomes unsustainable
- AI workflows collapse
- operational trust disappears
