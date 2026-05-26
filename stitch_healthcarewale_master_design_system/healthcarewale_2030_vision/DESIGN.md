---
name: HealthcareWale 2030 Vision
colors:
  surface: '#0e1322'
  surface-dim: '#0e1322'
  surface-bright: '#343949'
  surface-container-lowest: '#090e1c'
  surface-container-low: '#161b2b'
  surface-container: '#1a1f2f'
  surface-container-high: '#25293a'
  surface-container-highest: '#2f3445'
  on-surface: '#dee1f7'
  on-surface-variant: '#bdc9c8'
  inverse-surface: '#dee1f7'
  inverse-on-surface: '#2b3040'
  outline: '#879392'
  outline-variant: '#3e4949'
  surface-tint: '#76d6d5'
  primary: '#76d6d5'
  on-primary: '#003737'
  primary-container: '#008080'
  on-primary-container: '#e3fffe'
  inverse-primary: '#006a6a'
  secondary: '#7dffa2'
  on-secondary: '#003918'
  secondary-container: '#05e777'
  on-secondary-container: '#00622e'
  tertiary: '#ffb950'
  on-tertiary: '#452b00'
  tertiary-container: '#9d6800'
  on-tertiary-container: '#fff9f5'
  error: '#ffb4ab'
  on-error: '#690005'
  error-container: '#93000a'
  on-error-container: '#ffdad6'
  primary-fixed: '#93f2f2'
  primary-fixed-dim: '#76d6d5'
  on-primary-fixed: '#002020'
  on-primary-fixed-variant: '#004f4f'
  secondary-fixed: '#62ff96'
  secondary-fixed-dim: '#00e475'
  on-secondary-fixed: '#00210b'
  on-secondary-fixed-variant: '#005226'
  tertiary-fixed: '#ffddb3'
  tertiary-fixed-dim: '#ffb950'
  on-tertiary-fixed: '#291800'
  on-tertiary-fixed-variant: '#624000'
  background: '#0e1322'
  on-background: '#dee1f7'
  surface-variant: '#2f3445'
typography:
  display-lg:
    fontFamily: Sora
    fontSize: 48px
    fontWeight: '700'
    lineHeight: '1.1'
    letterSpacing: -0.02em
  headline-lg:
    fontFamily: Sora
    fontSize: 32px
    fontWeight: '600'
    lineHeight: '1.2'
  headline-md:
    fontFamily: Sora
    fontSize: 24px
    fontWeight: '600'
    lineHeight: '1.3'
  body-lg:
    fontFamily: Hanken Grotesk
    fontSize: 18px
    fontWeight: '400'
    lineHeight: '1.6'
  body-md:
    fontFamily: Hanken Grotesk
    fontSize: 16px
    fontWeight: '400'
    lineHeight: '1.5'
  label-caps:
    fontFamily: Hanken Grotesk
    fontSize: 12px
    fontWeight: '700'
    lineHeight: '1'
    letterSpacing: 0.1em
  headline-lg-mobile:
    fontFamily: Sora
    fontSize: 28px
    fontWeight: '600'
    lineHeight: '1.2'
rounded:
  sm: 0.5rem
  DEFAULT: 1rem
  md: 1.5rem
  lg: 2rem
  xl: 3rem
  full: 9999px
spacing:
  base: 8px
  nano: 4px
  compact: 12px
  standard: 24px
  airy: 48px
  container-max: 1440px
  gutter: 24px
---

## Brand & Style

The design system embodies the "2030 Vision"—a future where healthcare is proactive, biometric-integrated, and deeply personalized. The aesthetic is **Futuristic Premium SaaS**, blending the clinical precision of medical technology with the immersive depth of astral exploration.

The visual language utilizes **Glassmorphism** to represent transparency and data clarity, combined with **Organic Geometry** (super-ellipses) to evoke a sense of biological harmony. The emotional response is one of "Informed Calm"—the user should feel they are in a high-tech sanctuary where complex data is distilled into intuitive, life-affirming insights. 

The system prioritizes high-density information for professionals while maintaining breathable margins to prevent cognitive fatigue. It is built for a voice-first, biometric-ready world, ensuring that interaction is fluid across visual and auditory interfaces.

## Colors

The palette is anchored in **Deep Space Blue (#0A0F1E)**, providing a sophisticated, low-fatigue background that makes clinical data "pop." 

*   **Medical Teal (#008080)** acts as the primary brand anchor, symbolizing trust and professional stability.
*   **Aurora Green (#00E676)** is the "Vitality" color, used for positive health trends, active biometrics, and "Go" states.
*   **Electric Amber (#FFAB00)** is reserved for critical alerts, cautionary biometric readings, and highlights that require immediate cognitive attention.

The default mode is **Dark**, utilizing semi-transparent "Glass" layers to create depth without clutter. Accent glows are used sparingly to guide the eye toward active voice-listening states or biometric scanning zones.

## Typography

This design system uses **Sora** for all display and headline roles to achieve a geometric, futuristic feel that remains highly legible in high-contrast scenarios. **Hanken Grotesk** is used for body copy and data labels, offering a clean, contemporary grotesque style that handles multi-lingual scripts (English, Hindi, Bengali) with consistent vertical alignment.

For **Hindi and Bengali** implementation:
*   Ensure line-height is increased by 20% compared to English equivalents to accommodate matras and conjuncts.
*   Weight should be bumped up one level (e.g., Regular to Medium) for scripts at small sizes to maintain visual parity with Latin characters.

## Layout & Spacing

The layout follows a **Fluid 12-Column Grid** with high-density components nested within breathable container margins. 

*   **Desktop:** 12 columns, 24px gutters, 80px side margins.
*   **Tablet:** 8 columns, 16px gutters, 40px side margins.
*   **Mobile:** 4 columns, 16px gutters, 20px side margins.

The spacing rhythm is based on a **fixed 8px increment**. "High-density" is achieved by using `compact` (12px) spacing for internal data groups (e.g., heart rate stats), while "Breathable" layout is maintained by using `airy` (48px) spacing between major sections (e.g., Patient Summary vs. Treatment Timeline).

## Elevation & Depth

Depth is established through **Tonal Stacked Glass**. Unlike traditional shadows, this design system uses multi-layered, low-opacity glows to indicate elevation.

1.  **Level 0 (Background):** Deep Space Blue solid fill.
2.  **Level 1 (Cards/Panels):** `backdrop-blur(20px)` with a 1px `rgba(255, 255, 255, 0.1)` border.
3.  **Level 2 (Interactive/Floating):** Level 1 + a soft Aurora Green or Medical Teal outer glow (`blur: 30px, spread: -5px, opacity: 0.15`).
4.  **Level 3 (Modals/Overlays):** Deep glass with a stronger white inner stroke and a high-contrast backdrop dimming layer (`rgba(0, 0, 0, 0.8)`).

Shadows are never pure black; they are always tinted with the Primary or Neutral-Dark hue to maintain the "2030" luminous aesthetic.

## Shapes

The design system utilizes **Super-Ellipses (Squicles)** to create an organic, biological feel. 

*   **Main Containers:** Use `rounded-3xl` (1.5rem / 24px) or `rounded-4xl` (2rem / 32px) for a soft, premium appearance.
*   **Buttons & Controls:** Always pill-shaped (`rounded-full`) to encourage touch and biometric interaction.
*   **Input Fields:** Follow the `rounded-xl` standard to balance form-factor with the roundness of the overall UI.

Avoid sharp 90-degree corners entirely; every vertex should feel smooth and "grown" rather than cut.

## Components

**Buttons:** 
High-gloss surfaces with `Sora` Semibold text. Primary buttons use a Medical Teal to Aurora Green gradient. Secondary buttons are "Ghost" style with a 1px glass border.

**Cards:** 
The core of the high-density layout. They must feature a subtle glass blur and contain "Micro-Data" (sparklines, status dots) in the top-right corner.

**Biometric Status:** 
A unique component consisting of a pulsing Aurora Green ring. This ring serves as both a visual indicator of "System Live" and a touch-point for fingerprint/face-ID triggers.

**Voice-First Interface:** 
When active, a "Waveform" visualization replaces the bottom navigation bar. The waveform uses the Electric Amber and Aurora Green palette to indicate listening and processing states.

**Input Fields:** 
Floating labels with high-contrast borders that "glow" Medical Teal when focused. Support for voice-to-text input is standard, indicated by a microphone icon in the trailing edge.

**Chips/Badges:** 
Ultra-condensed labels using `label-caps`. Used for health markers (e.g., "O2 NORMAL") with high-contrast background fills.