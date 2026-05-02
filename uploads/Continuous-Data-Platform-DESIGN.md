---
version: "alpha"
name: "Continuous Data Platform"
description: "Continuous Data CTA Section is designed for building reusable UI components in modern web projects. Key features include reusable structure, responsive behavior, and production-ready presentation. It is suitable for component libraries and responsive product interfaces."
colors:
  primary: "#1E293B"
  secondary: "#334155"
  tertiary: "#3B82F6"
  neutral: "#FFFFFF"
  background: "#1E293B"
  surface: "#334155"
  text-primary: "#94A3B8"
  text-secondary: "#60A5FA"
  border: "#334155"
  accent: "#1E293B"
typography:
  display-lg:
    fontFamily: "Georgia"
    fontSize: "72px"
    fontWeight: 400
    lineHeight: "72px"
    letterSpacing: "-0.025em"
  body-md:
    fontFamily: "System Font"
    fontSize: "18px"
    fontWeight: 400
    lineHeight: "29.25px"
  label-md:
    fontFamily: "System Font"
    fontSize: "14px"
    fontWeight: 500
    lineHeight: "20px"
rounded:
  full: "9999px"
spacing:
  base: "4px"
  sm: "4px"
  md: "8px"
  lg: "12px"
  xl: "20px"
  gap: "4px"
  section-padding: "24px"
components:
  button-primary:
    backgroundColor: "{colors.secondary}"
    textColor: "{colors.text-secondary}"
    typography: "{typography.label-md}"
    rounded: "{rounded.full}"
    padding: "8px"
  button-secondary:
    textColor: "{colors.text-secondary}"
    typography: "{typography.label-md}"
    rounded: "{rounded.full}"
    padding: "8px"
  button-link:
    textColor: "{colors.text-primary}"
    typography: "{typography.label-md}"
    rounded: "{rounded.full}"
    padding: "8px"
---

## Overview

- **Composition cues:**
  - Layout: Grid
  - Content Width: Full Bleed
  - Framing: Glassy
  - Grid: Strong

## Colors

The color system uses dark mode with #1E293B as the main accent and #FFFFFF as the neutral foundation.

- **Primary (#1E293B):** Main accent and emphasis color.
- **Secondary (#334155):** Supporting accent for secondary emphasis.
- **Tertiary (#3B82F6):** Reserved accent for supporting contrast moments.
- **Neutral (#FFFFFF):** Neutral foundation for backgrounds, surfaces, and supporting chrome.

- **Usage:** Background: #1E293B; Surface: #334155; Text Primary: #94A3B8; Text Secondary: #60A5FA; Border: #334155; Accent: #1E293B

- **Gradients:** bg-gradient-to-br from-indigo-400 to-cyan-300 via-blue-400, bg-gradient-to-r from-blue-600 to-indigo-600

## Typography

Typography pairs Georgia for display hierarchy with System Font for supporting content and interface copy.

- **Display (`display-lg`):** Georgia, 72px, weight 400, line-height 72px, letter-spacing -0.025em.
- **Body (`body-md`):** System Font, 18px, weight 400, line-height 29.25px.
- **Labels (`label-md`):** System Font, 14px, weight 500, line-height 20px.

## Layout

Layout follows a grid composition with reusable spacing tokens. Preserve the grid, full bleed structural frame before changing ornament or component styling. Use 4px as the base rhythm and let larger gaps step up from that cadence instead of introducing unrelated spacing values.

Treat the page as a grid / full bleed composition, and keep that framing stable when adding or remixing sections.

- **Layout type:** Grid
- **Content width:** Full Bleed
- **Base unit:** 4px
- **Scale:** 4px, 8px, 12px, 20px, 24px, 32px, 40px, 96px
- **Section padding:** 24px, 152px
- **Gaps:** 4px, 8px

## Elevation & Depth

Depth is communicated through glass, border contrast, and reusable shadow or blur treatments. Keep those recipes consistent across hero panels, cards, and controls so the page reads as one material system.

Surfaces should read as glass first, with borders, shadows, and blur only reinforcing that material choice.

- **Surface style:** Glass
- **Borders:** 0.8px #334155; 0.8px #3B82F6
- **Shadows:** rgba(0, 0, 0, 0) 0px 0px 0px 0px, rgba(0, 0, 0, 0) 0px 0px 0px 0px, rgba(0, 0, 0, 0.05) 0px 1px 2px 0px; rgba(0, 0, 0, 0) 0px 0px 0px 0px, rgba(0, 0, 0, 0) 0px 0px 0px 0px, rgba(0, 0, 0, 0.2) 0px 1px 2px 0px; rgba(0, 0, 0, 0) 0px 0px 0px 0px, rgba(0, 0, 0, 0) 0px 0px 0px 0px, rgba(30, 58, 138, 0.5) 0px 10px 15px -3px, rgba(30, 58, 138, 0.5) 0px 4px 6px -4px
- **Blur:** 12px

### Techniques
- **Gradient border shell:** Use a thin gradient border shell around the main card. Wrap the surface in an outer shell with 22px padding and a 9999px radius. Drive the shell with linear-gradient(to right, rgb(37, 99, 235), rgb(79, 70, 229)) so the edge reads like premium depth instead of a flat stroke. Keep the actual stroke understated so the gradient shell remains the hero edge treatment. Inset the real content surface inside the wrapper with a slightly smaller radius so the gradient only appears as a hairline frame.

## Shapes

Shapes rely on a tight radius system anchored by 9999px and scaled across cards, buttons, and supporting surfaces. Icon geometry should stay compatible with that soft-to-controlled silhouette.

Use the radius family intentionally: larger surfaces can open up, but controls and badges should stay within the same rounded DNA instead of inventing sharper or pill-only exceptions.

- **Corner radii:** 9999px
- **Icon treatment:** Linear
- **Icon sets:** Solar

## Components

Anchor interactions to the detected button styles.

### Buttons
- **Primary:** background #334155, text #60A5FA, radius 9999px, padding 8px, border 0px solid rgb(229, 231, 235).
- **Secondary:** text #60A5FA, radius 9999px, padding 8px, border 0.8px solid rgb(59, 130, 246).
- **Links:** text #94A3B8, radius 9999px, padding 8px, border 0px solid rgb(229, 231, 235).

### Iconography
- **Treatment:** Linear.
- **Sets:** Solar.

## Do's and Don'ts

Use these constraints to keep future generations aligned with the current system instead of drifting into adjacent styles.

### Do
- Do use the primary palette as the main accent for emphasis and action states.
- Do keep spacing aligned to the detected 4px rhythm.
- Do reuse the Glass surface treatment consistently across cards and controls.
- Do keep corner radii within the detected 9999px family.

### Don't
- Don't introduce extra accent colors outside the core palette roles unless the page needs a new semantic state.
- Don't mix unrelated shadow or blur recipes that break the current depth system.
- Don't exceed the detected moderate motion intensity without a deliberate reason.

## Motion

Motion feels controlled and interface-led across text, layout, and section transitions. Timing clusters around 150ms. Easing favors ease and cubic-bezier(0.4. Hover behavior focuses on text and shadow changes.

**Motion Level:** moderate

**Durations:** 150ms

**Easings:** ease, cubic-bezier(0.4, 0, 0.2, 1)

**Hover Patterns:** text, shadow, color
