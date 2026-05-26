---
name: Clinical Precision
colors:
  surface: '#f8f9ff'
  surface-dim: '#ccdbf3'
  surface-bright: '#f8f9ff'
  surface-container-lowest: '#ffffff'
  surface-container-low: '#eff4ff'
  surface-container: '#e6eeff'
  surface-container-high: '#dce9ff'
  surface-container-highest: '#d5e3fc'
  on-surface: '#0d1c2e'
  on-surface-variant: '#3e4949'
  inverse-surface: '#233144'
  inverse-on-surface: '#eaf1ff'
  outline: '#6e7979'
  outline-variant: '#bdc9c8'
  surface-tint: '#006a6a'
  primary: '#006565'
  on-primary: '#ffffff'
  primary-container: '#008080'
  on-primary-container: '#e3fffe'
  inverse-primary: '#76d6d5'
  secondary: '#4c56af'
  on-secondary: '#ffffff'
  secondary-container: '#959efd'
  on-secondary-container: '#27308a'
  tertiary: '#156820'
  on-tertiary: '#ffffff'
  tertiary-container: '#338236'
  on-tertiary-container: '#ebffe3'
  error: '#ba1a1a'
  on-error: '#ffffff'
  error-container: '#ffdad6'
  on-error-container: '#93000a'
  primary-fixed: '#93f2f2'
  primary-fixed-dim: '#76d6d5'
  on-primary-fixed: '#002020'
  on-primary-fixed-variant: '#004f4f'
  secondary-fixed: '#e0e0ff'
  secondary-fixed-dim: '#bdc2ff'
  on-secondary-fixed: '#000767'
  on-secondary-fixed-variant: '#343d96'
  tertiary-fixed: '#a3f69c'
  tertiary-fixed-dim: '#88d982'
  on-tertiary-fixed: '#002204'
  on-tertiary-fixed-variant: '#005312'
  background: '#f8f9ff'
  on-background: '#0d1c2e'
  surface-variant: '#d5e3fc'
typography:
  display-lg:
    fontFamily: Inter
    fontSize: 48px
    fontWeight: '700'
    lineHeight: 56px
    letterSpacing: -0.02em
  headline-lg:
    fontFamily: Inter
    fontSize: 32px
    fontWeight: '600'
    lineHeight: 40px
    letterSpacing: -0.01em
  headline-lg-mobile:
    fontFamily: Inter
    fontSize: 24px
    fontWeight: '600'
    lineHeight: 32px
  headline-md:
    fontFamily: Inter
    fontSize: 24px
    fontWeight: '600'
    lineHeight: 32px
  body-lg:
    fontFamily: Inter
    fontSize: 18px
    fontWeight: '400'
    lineHeight: 28px
  body-md:
    fontFamily: Inter
    fontSize: 16px
    fontWeight: '400'
    lineHeight: 24px
  label-xl:
    fontFamily: Inter
    fontSize: 14px
    fontWeight: '700'
    lineHeight: 20px
    letterSpacing: 0.05em
  label-md:
    fontFamily: Inter
    fontSize: 14px
    fontWeight: '600'
    lineHeight: 20px
  caption:
    fontFamily: Inter
    fontSize: 12px
    fontWeight: '500'
    lineHeight: 16px
rounded:
  sm: 0.125rem
  DEFAULT: 0.25rem
  md: 0.375rem
  lg: 0.5rem
  xl: 0.75rem
  full: 9999px
spacing:
  base: 4px
  xs: 4px
  sm: 8px
  md: 16px
  lg: 24px
  xl: 32px
  gutter: 16px
  margin-mobile: 16px
  margin-desktop: 48px
  touch-target-min: 44px
---

## Brand & Style

This design system establishes a high-reliability visual language for medical infrastructure. It bridges the gap between the sleek, high-performance aesthetics of modern SaaS (linear/minimalist) and the life-critical requirements of healthcare. The emotional response is one of **unshakeable competence, clarity, and speed**.

The design style is **Corporate Modern with Functional Minimalism**. It prioritizes extreme legibility and operational throughput. Layouts are spacious but structured, utilizing a "system-first" approach where every pixel serves a functional purpose. The UI minimizes cognitive load by removing decorative flourishes, focusing instead on high-contrast data visualization and clear action hierarchies.

- **Target Audience:** Clinicians, hospital administrators, and frontline health workers.
- **Tone:** Professional, clinical, and efficient.
- **Key Influence:** High-density dashboards that remain readable under stress.

## Colors

The palette is rooted in medical trust and operational status. 

- **Medical Teal (Primary):** Used for primary actions, active states, and brand-identifying elements. It provides a modern, sterile yet approachable feel.
- **Deep Blue (Secondary):** Reserved for global navigation, structural headers, and elements that require an aura of authority and stability.
- **Functional Semantics:** Emerald Green is strictly for success states and "healthy" vitals. Amber is utilized for non-blocking alerts. Red is reserved for critical clinical errors or patient emergencies.
- **Neutrals:** A sophisticated slate-based grayscale is used to maintain a cool, professional temperature, avoiding the "dirty" look of warmer grays.

## Typography

The typography system relies exclusively on **Inter** to ensure maximum legibility across digital interfaces and multilingual support for English, Hindi, and Bengali. 

- **Visual Weight:** Heavy weights (600-700) are used for labels and headers to ensure they are readable at a glance in high-stress environments.
- **Scale:** A tight scale prevents information density from becoming overwhelming. 
- **Multilingual Support:** When rendering Indic scripts (Hindi/Bengali), line-height is increased by 15% automatically to accommodate descenders and matras without clipping.
- **Labels:** Uppercase labels with slight letter spacing are used for metadata and category headers to distinguish them clearly from interactive body text.

## Layout & Spacing

This design system uses a **12-column fluid grid** for desktop and a **4-column grid** for mobile. The layout philosophy is "Information First."

- **Spacing Rhythm:** Based on a 4px baseline grid. Most components use 16px (md) or 24px (lg) padding to ensure high touch-accuracy.
- **Operational Speed:** Layouts prioritize the "F-pattern" for scanning clinical records. Primary actions are consistently placed in the bottom-right for mobile (thumb-zone) and top-right for desktop.
- **Touch Targets:** A strict minimum of 44x44px is enforced for all interactive elements to accommodate gloved hands or rapid movement.

## Elevation & Depth

To maintain a "clean" and "surgical" feel, the system uses **Tonal Layering** supplemented by subtle **Low-Contrast Outlines**.

- **Surfaces:** The background uses a very light cool gray (#F8FAFC). Cards and containers use pure white (#FFFFFF) with a 1px border (#E2E8F0).
- **Shadows:** Shadows are used sparingly to indicate modality (e.g., a diagnostic pop-up). When used, they are "Ambient Shadows"—highly diffused, low-opacity (10%), and slightly tinted with the Secondary Blue to maintain color harmony.
- **Depth Levels:**
    - Level 0: Background.
    - Level 1: Main content cards (1px border).
    - Level 2: Hover states and active dropdowns (Soft shadow, 4px blur).
    - Level 3: Modals and urgent alerts (Deep shadow, 12px blur).

## Shapes

The shape language is **Soft and Professional**. 

A `0.25rem` (4px) base radius is used for most UI components (inputs, buttons, small cards). This provides a precise, modern feel that looks systematic and reliable. Larger containers or "WhatsApp-inspired" chat bubbles may use `rounded-lg` (8px) to feel more approachable and familiar during communication-heavy tasks.

## Components

- **Buttons:** Primary buttons use Medical Teal with white text. High-emphasis actions (Save, Send) use the full 44px height. Secondary buttons use a ghost style (Teal outline, no fill).
- **Input Fields:** Large, highly visible fields with 1px borders that thicken to 2px Teal on focus. Labels are always persistent (never hidden as placeholders) to reduce memory load.
- **Status Indicators (Connectivity):** A dedicated "Sync Bar" appears at the top of the viewport. 
    - *Full Green:* Online.
    - *Amber Pulsing:* Low bandwidth (automatic image compression active).
    - *Red Outline:* Offline (data cached locally).
- **Voice-Action Elements:** A prominent, floating microphone action button (Secondary Blue) is available in clinical entry screens, styled with a gentle pulse animation to indicate readiness.
- **WhatsApp-Inspired Cues:** Message-based updates use familiar double-tick icons for "Read/Received" status in patient-clinician chats, leveraging existing user mental models.
- **Cards:** Clinical data cards use "Sectioned Rows" with thin dividers to separate patient vitals, ensuring data doesn't bleed together during quick scrolls.