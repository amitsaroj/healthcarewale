---
name: Premium Clinical Suite
colors:
  surface: '#f8f9ff'
  surface-dim: '#cbdbf5'
  surface-bright: '#f8f9ff'
  surface-container-lowest: '#ffffff'
  surface-container-low: '#eff4ff'
  surface-container: '#e5eeff'
  surface-container-high: '#dce9ff'
  surface-container-highest: '#d3e4fe'
  on-surface: '#0b1c30'
  on-surface-variant: '#3e4949'
  inverse-surface: '#213145'
  inverse-on-surface: '#eaf1ff'
  outline: '#6e7979'
  outline-variant: '#bdc9c8'
  surface-tint: '#006a6a'
  primary: '#006565'
  on-primary: '#ffffff'
  primary-container: '#008080'
  on-primary-container: '#e3fffe'
  inverse-primary: '#76d6d5'
  secondary: '#4f6073'
  on-secondary: '#ffffff'
  secondary-container: '#d2e4fb'
  on-secondary-container: '#556679'
  tertiary: '#006834'
  on-tertiary: '#ffffff'
  tertiary-container: '#008443'
  on-tertiary-container: '#e9ffe9'
  error: '#ba1a1a'
  on-error: '#ffffff'
  error-container: '#ffdad6'
  on-error-container: '#93000a'
  primary-fixed: '#93f2f2'
  primary-fixed-dim: '#76d6d5'
  on-primary-fixed: '#002020'
  on-primary-fixed-variant: '#004f4f'
  secondary-fixed: '#d2e4fb'
  secondary-fixed-dim: '#b7c8de'
  on-secondary-fixed: '#0b1d2d'
  on-secondary-fixed-variant: '#38485a'
  tertiary-fixed: '#6bfe9c'
  tertiary-fixed-dim: '#4ae183'
  on-tertiary-fixed: '#00210c'
  on-tertiary-fixed-variant: '#005228'
  background: '#f8f9ff'
  on-background: '#0b1c30'
  surface-variant: '#d3e4fe'
typography:
  headline-xl:
    fontFamily: Inter
    fontSize: 40px
    fontWeight: '700'
    lineHeight: '1.2'
    letterSpacing: -0.02em
  headline-lg:
    fontFamily: Inter
    fontSize: 32px
    fontWeight: '600'
    lineHeight: '1.25'
    letterSpacing: -0.02em
  headline-md:
    fontFamily: Inter
    fontSize: 24px
    fontWeight: '600'
    lineHeight: '1.3'
    letterSpacing: -0.01em
  body-lg:
    fontFamily: Inter
    fontSize: 18px
    fontWeight: '400'
    lineHeight: '1.6'
  body-md:
    fontFamily: Inter
    fontSize: 16px
    fontWeight: '400'
    lineHeight: '1.6'
  label-lg:
    fontFamily: Inter
    fontSize: 15px
    fontWeight: '600'
    lineHeight: '1.4'
    letterSpacing: 0.05em
  label-md:
    fontFamily: Inter
    fontSize: 13px
    fontWeight: '500'
    lineHeight: '1.4'
  caption:
    fontFamily: Inter
    fontSize: 12px
    fontWeight: '400'
    lineHeight: '1.4'
rounded:
  sm: 0.25rem
  DEFAULT: 0.5rem
  md: 0.75rem
  lg: 1rem
  xl: 1.5rem
  full: 9999px
spacing:
  unit: 8px
  touch-target: 48px
  gutter: 24px
  margin-mobile: 16px
  margin-desktop: 40px
  container-max: 1440px
---

## Brand & Style

The design system is engineered for high-stakes healthcare environments where clarity, speed, and trust are paramount. It adopts a **Modern Corporate** aesthetic influenced by the precision of developer tools (Linear/Vercel) and the fluid accessibility of top-tier fintech (Stripe).

The visual language prioritizes a **Low Cognitive Load** philosophy. This is achieved through a strict "Information First" hierarchy, eliminating decorative clutter in favor of functional density. The system balances clinical sterile precision with approachable human-centric patterns, ensuring that practitioners feel empowered rather than overwhelmed. Key characteristics include high-contrast interactive elements, surgical-grade alignment, and a focus on operational uptime.

## Colors

The palette is anchored in **Medical Teal**, a color that evokes cleanliness and professional care, paired with **Deep Blue** for authoritative navigation and structural elements.

- **Primary (Teal):** Used for primary actions, active states, and brand highlights.
- **Secondary (Deep Blue):** Reserved for sidebars, headers, and heavy typography to provide a grounded, premium feel.
- **Success (Emerald):** Denotes healthy vitals, completed tasks, and positive inventory status.
- **Warning (Amber):** High-visibility alerts for patient queues or low-stock indicators.
- **Neutral Grayscale:** A systematic range of slates and grays used to define borders and secondary information without competing for attention.

The system supports a **Light Mode** (default for clinical daytime use) and a **Dark Mode** (optimized for night shifts and high-concentration diagnostic work).

## Typography

The design system utilizes **Inter** for its exceptional legibility and systematic weight distribution. 

To support **Hindi and Bengali scripts**, line-heights are intentionally generous (minimum 1.4x - 1.6x) to prevent "crowding" of complex character ascenders and descenders. Labels are scaled larger than standard SaaS defaults to ensure high readability for practitioners moving quickly or viewing screens from a distance. Use **Semi-Bold (600)** for clinical data points to ensure they stand out against UI chrome.

## Layout & Spacing

This design system uses an **8px linear scale** for all spacing and layout decisions. 

- **Grid Model:** A 12-column fluid grid for desktop with a maximum container width of 1440px. 
- **Touch-First:** All interactive elements (buttons, inputs, list items) must maintain a minimum hit area of **48px** to accommodate rapid mobile interaction and gloved-hand use.
- **Operational Density:** While the grid is generous, "Inventory Tables" and "Queue Systems" allow for a "Compact" mode where vertical padding is reduced to 12px to maximize data visibility, provided the horizontal tap target remains accessible.
- **Keyboard Navigation:** Focus states must be highly visible (2px primary-colored offset ring) to support power-user navigation.

## Elevation & Depth

Hierarchy is established through **Tonal Layering** and **Ambient Shadows**.

- **Surface Levels:** The background uses a slight off-white (#F8FAFC) to reduce glare. Primary cards and containers use pure white (#FFFFFF).
- **Depth:** We use a "Natural Light" shadow model. Level 1 (Cards) features a subtle 2px blur with 5% opacity. Level 2 (Modals/Dropdowns) uses a more pronounced 12px blur with 10% opacity.
- **Outlines:** To maintain the premium "Vercel-like" feel, use 1px low-contrast borders (#E2E8F0) on all containers. Shadows should be secondary to borders in defining space, ensuring the UI feels "architectural" rather than "floaty."

## Shapes

The design system uses a **Rounded** (Level 2) shape language. 

- **Standard Radius (8px):** Applied to buttons, input fields, and standard cards.
- **Large Radius (16px):** Used for primary dashboard containers and analytics widgets to create a sophisticated, modern framing.
- **Pill (Full):** Reserved exclusively for Status Badges (e.g., "Active", "In-Queue") and Voice-Activation triggers, distinguishing them from square-ish action buttons.

## Components

### Buttons & Voice Triggers
Buttons feature a subtle top-light gradient to provide a tactile feel. **Voice-first workflows** are represented by a floating "Orb" button that uses a pulsing teal glow when active.

### WhatsApp-Inspired Lists
For patient queues and messaging, use a left-aligned avatar, a bold title (Patient Name), and a secondary line (Medical ID/Status). The interaction pattern mimics mobile messaging apps—swipe-to-action on mobile and hover-actions on desktop.

### Analytics Cards
Feature a "Micro-Sparkline" in the top right corner. Primary metrics use **Headline-LG** weights. Contrast between the metric and the label must exceed 7:1 for accessibility.

### Inventory Tables
Tables utilize "Sticky Headers" and high-contrast row zebra-striping. Inventory status (In-Stock/Low/Out) must be accompanied by both a color indicator and a text label to ensure accessibility for colorblind users.

### Input Fields
Labels are permanently visible (not floating placeholders) to reduce memory load. Focus states use a 1px teal border with a 3px soft outer glow.

### Queue Systems
Queue items use a "Priority Border"—a 4px vertical accent on the left edge of the card (Amber for urgent, Teal for routine). This allows for instant peripheral scanning of patient priority.