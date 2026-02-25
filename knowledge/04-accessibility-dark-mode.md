# 04 — Accessibility & Dark Mode Technical Specifications

This document provides precise, implementable specifications for building accessible and dark-mode-ready interfaces. All values are based on WCAG 2.1 AA (minimum) and WCAG 2.2 where applicable.

---

## 1. Regulatory Landscape (2025-2026)

### Active Regulations

| Regulation | Scope | Standard | Deadline |
|-----------|-------|----------|----------|
| **ADA (Americans with Disabilities Act)** | U.S. — all public-facing digital services | WCAG 2.1 AA | In effect |
| **Section 508** | U.S. federal agencies & contractors | WCAG 2.1 AA | In effect |
| **HHS Section 504 Final Rule** | U.S. healthcare platforms | WCAG 2.1 AA | **May 2026** |
| **European Accessibility Act (EAA)** | EU — digital products & services | EN 301 549 (≈ WCAG 2.1 AA) | **June 2025** |
| **AODA** | Ontario, Canada | WCAG 2.0 AA | In effect |
| **EN 301 549** | EU public sector | WCAG 2.1 AA | In effect |

### Critical Alert: Healthcare Platforms
> **HHS Section 504 Final Rule (effective May 2026):** All healthcare-related digital platforms receiving federal funding MUST comply with WCAG 2.1 AA. Non-compliance risks loss of federal funding and legal action. If designing healthcare products, treat this as a **hard requirement**.

---

## 2. Color & Contrast Specifications

### Contrast Ratios (WCAG 2.1 AA)

| Element | Minimum Ratio | Measurement |
|---------|--------------|-------------|
| **Body text** (< 18pt / 14pt bold) | **4.5:1** | Foreground vs. background |
| **Large text** (≥ 18pt / 14pt bold) | **3:1** | Foreground vs. background |
| **UI components & icons** | **3:1** | Against adjacent colors |
| **Focus indicators** | **3:1** | Against surrounding content |
| **Placeholder text** | **4.5:1** | Against input background (often fails!) |
| **Disabled states** | No requirement | But should be distinguishable from enabled |

### WCAG 2.1 AAA (Enhanced — Recommended for Healthcare/Gov)

| Element | Minimum Ratio |
|---------|--------------|
| **Body text** | **7:1** |
| **Large text** | **4.5:1** |

### Color Independence Rule
> **WCAG 1.4.1:** Color must NOT be the **only** means of conveying information.

**Fail Examples:**
- Red text for errors, green for success (no icon/label)
- Chart with only color-coded legend (no patterns or labels)
- Required field indicated only by red asterisk (no text)

**Pass Examples:**
- Error: Red text + error icon + "Error:" label
- Chart: Colors + patterns (stripes, dots) + labels on each data series
- Required: Red asterisk + "(required)" text

### Color Vision Deficiency (CVD) Design

| CVD Type | Prevalence | Problem Colors | Safe Alternatives |
|----------|-----------|----------------|-------------------|
| **Protanopia** (no red) | ~1% male | Red-Green | Blue-Orange |
| **Deuteranopia** (no green) | ~5% male | Red-Green | Blue-Orange |
| **Tritanopia** (no blue) | ~0.01% | Blue-Yellow | Red-Green (ironic!) |
| **Achromatopsia** (no color) | ~0.003% | All | Rely on value contrast only |

**Safe Color Palette Strategy:**
1. Design in grayscale first — ensure information is readable without color
2. Use blue-orange as primary semantic pair (safe for all common CVD types)
3. Test with CVD simulation tools (Figma: Stark plugin, Chrome: DevTools → Rendering → Emulate vision deficiencies)
4. Always pair color with shape, icon, pattern, or text

---

## 3. Dark Mode Technical Specifications

### Background Color: The #000000 Problem

> **Never use pure black (#000000) as the background in dark mode.**

**Why:**
- **Halation effect:** White text on pure black creates a visual "glow" or blurring, especially for users with astigmatism (~33% of the population)
- **OLED smearing:** On OLED screens, transitioning from pure black to a lighter color can cause visible smearing/ghosting
- **Eye strain:** The extreme contrast (21:1 for white on black) causes faster eye fatigue than a softer contrast

**Recommended Dark Mode Background Scale:**

| Layer | Color | Usage |
|-------|-------|-------|
| **Surface 0 (Darkest)** | `#121212` | App background, base layer |
| **Surface 1** | `#1E1E1E` | Cards, raised containers |
| **Surface 2** | `#232323` | Dropdowns, menus |
| **Surface 3** | `#282828` | Hover states, active items |
| **Surface 4** | `#2C2C2C` | Selected states |
| **Surface 5** | `#333333` | Borders, dividers |

### Text Colors in Dark Mode

| Text Type | Color | Opacity/Hex | Contrast on #121212 |
|-----------|-------|-------------|---------------------|
| **Primary text** | White | 87% → `#DEDEDE` | ~13.5:1 ✓ |
| **Secondary text** | White | 60% → `#999999` | ~5.9:1 ✓ |
| **Disabled text** | White | 38% → `#616161` | ~3.2:1 (AA for large text) |
| **Placeholder** | White | 50% → `#808080` | ~4.6:1 ✓ |

### Color Desaturation for Dark Mode

> High-saturation colors on dark backgrounds cause **visual vibration** (a shimmering/buzzing effect that strains the eyes).

**Rule:** Desaturate all accent/brand colors by 20-30% for dark mode.

**Examples:**

| Color | Light Mode | Dark Mode (Desaturated) |
|-------|-----------|------------------------|
| Primary Blue | `#2196F3` | `#64B5F6` (lighter, less saturated) |
| Success Green | `#4CAF50` | `#81C784` |
| Warning Orange | `#FF9800` | `#FFB74D` |
| Error Red | `#F44336` | `#E57373` |

**Implementation Strategy:**
1. Define separate color tokens for light and dark themes
2. Use CSS custom properties (variables) that switch based on `prefers-color-scheme`
3. Test all states (hover, focus, active, disabled) in both modes
4. Images/illustrations may need dark mode variants or adaptive overlay

### Dark Mode Implementation Checklist

- [ ] Background uses `#121212` (not `#000000`)
- [ ] Elevation/depth is shown through lighter surfaces (not shadows)
- [ ] Text contrast meets WCAG 2.1 AA in dark mode specifically
- [ ] Accent colors are desaturated for dark mode
- [ ] Images have appropriate treatment (darkened overlay, dark variants)
- [ ] Focus indicators are visible on dark backgrounds
- [ ] Status colors (red, green, yellow) are distinguishable on dark backgrounds
- [ ] Scrollbars are styled/visible in dark mode
- [ ] Form inputs have visible borders on dark backgrounds
- [ ] Charts/graphs are legible with dark mode colors
- [ ] Shadows are minimized (use surface elevation instead)
- [ ] `prefers-color-scheme: dark` is respected by default

---

## 4. Interactive Element Accessibility

### Touch & Click Targets

| Platform | Minimum Target Size | Recommended |
|----------|-------------------|-------------|
| **iOS (Apple HIG)** | 44×44 pt | 48×48 pt |
| **Android (Material)** | 48×48 dp | 48×48 dp |
| **WCAG 2.2 (Target Size)** | 24×24 CSS px (AA) | 44×44 CSS px (AAA) |
| **Web (general)** | 44×44 CSS px | 48×48 CSS px |

**Spacing Between Targets:** Minimum 8px gap between adjacent interactive elements to prevent mis-taps.

### Focus Management

**Focus Indicator Requirements (WCAG 2.4.7 / 2.4.11 / 2.4.12):**
- Focus indicator must be visible on ALL interactive elements
- Minimum 2px solid outline (3:1 contrast against adjacent colors)
- Focus must follow a logical order matching visual layout
- Never use `outline: none` without providing a custom focus style
- Custom focus styles should be **more** visible than browser defaults, not less

**Focus Trap Rules:**
- Modals/dialogs must trap focus within them
- Focus returns to the trigger element when modal closes
- Escape key should close modals/dropdowns
- Skip-to-content link should be the first focusable element

### Keyboard Accessibility

**Every interactive element must be operable by keyboard:**

| Action | Key(s) |
|--------|--------|
| Navigate between elements | Tab / Shift+Tab |
| Activate buttons/links | Enter or Space |
| Navigate within groups (tabs, radios) | Arrow keys |
| Close overlays | Escape |
| Navigate menus | Arrow keys + Enter |
| Multi-select | Shift+Click, Ctrl/Cmd+Click |

### ARIA Usage Guidelines

**Rule 1:** Use semantic HTML first. Only add ARIA when native semantics are insufficient.

| Don't | Do |
|-------|-----|
| `<div role="button">` | `<button>` |
| `<span role="link">` | `<a href="...">` |
| `<div role="checkbox">` | `<input type="checkbox">` |

**Common ARIA Patterns:**

| Component | Key ARIA Attributes |
|-----------|-------------------|
| **Modal** | `role="dialog"`, `aria-modal="true"`, `aria-labelledby` |
| **Tabs** | `role="tablist"`, `role="tab"`, `role="tabpanel"`, `aria-selected` |
| **Alert** | `role="alert"` or `aria-live="assertive"` |
| **Status** | `role="status"` or `aria-live="polite"` |
| **Loading** | `aria-busy="true"`, `aria-live="polite"` |
| **Expandable** | `aria-expanded="true/false"` |
| **Sort** | `aria-sort="ascending/descending/none"` |

---

## 5. Content Accessibility

### Typography

| Property | Minimum | Recommended |
|----------|---------|-------------|
| **Body font size** | 16px | 16-18px |
| **Line height** | 1.5× font size | 1.5-1.75× |
| **Paragraph spacing** | 1.5× font size | 2× font size |
| **Letter spacing** | Default | +0.12em for body text |
| **Word spacing** | Default | +0.16em if needed |
| **Maximum line length** | — | 50-75 characters |

**WCAG 1.4.12 (Text Spacing):** Users must be able to override the following without loss of content:
- Line height to 1.5× font size
- Letter spacing to 0.12× font size
- Word spacing to 0.16× font size
- Paragraph spacing to 2× font size

### Motion & Animation

**WCAG 2.3.3 (Animation from Interactions):**
- Respect `prefers-reduced-motion: reduce`
- Provide a global toggle to disable animations
- Auto-playing animations must be pausable, stoppable, or hideable
- No content should flash more than 3 times per second

**Implementation:**
```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```

---

## 6. Sustainable UX Considerations

### Energy-Efficient Design Strategies

| Strategy | Impact | Implementation |
|----------|--------|----------------|
| **Dark mode as default** | OLED screens use ~60% less power in dark mode | Default to dark, respect OS preference |
| **Vector over raster** | SVGs are smaller and scale without re-downloading | Use SVG for icons, illustrations |
| **Lazy loading** | Reduce initial payload and energy consumption | `loading="lazy"` for images below fold |
| **Efficient animations** | GPU-intensive animations drain battery | Use `transform` and `opacity` only, avoid `box-shadow` animation |
| **Image optimization** | Largest contributor to page weight | WebP/AVIF format, responsive `srcset` |
| **Reduced auto-play** | Video auto-play is energy-intensive | Require user interaction to start video |

### Carbon-Aware Design
- Minimize unnecessary network requests
- Cache aggressively for repeat visitors
- Consider "eco mode" for battery-conscious users
- Measure and report page weight (target <500KB initial load for critical path)

---

## Accessibility Testing Checklist

### Automated Testing
- [ ] axe DevTools (browser extension) — zero critical violations
- [ ] Lighthouse Accessibility score ≥ 95
- [ ] Pa11y CI integrated in build pipeline
- [ ] Color contrast checker passed for all text

### Manual Testing
- [ ] Full keyboard navigation (Tab through all interactive elements)
- [ ] Screen reader testing (VoiceOver, NVDA, or JAWS)
- [ ] Zoom to 200% — no content overflow or loss
- [ ] Text spacing override — no content overlap
- [ ] Reduced motion preference respected
- [ ] Dark mode — all elements visible and contrasted
- [ ] Color blindness simulation — information not lost

### User Testing
- [ ] Tested with users who use assistive technology
- [ ] Tested with users who have low vision
- [ ] Tested with users who navigate by keyboard only
- [ ] Tested with users who use voice control
