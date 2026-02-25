# 06 — Comprehensive Design Review Checklist

Use this checklist to systematically evaluate any design. Score each section and generate a Design Health Score.

---

## How to Use This Checklist

1. **Evaluate** each item as: ✅ Pass | ⚠️ Partial | ❌ Fail | N/A
2. **Score** each section: (Pass count) / (Total applicable items) × 100
3. **Calculate** the overall Design Health Score: Average of all section scores
4. **Prioritize** all ❌ items using the Severity Rating Scale (0-4)

### Design Health Score Interpretation

| Score | Rating | Action |
|-------|--------|--------|
| 90-100% | Excellent | Ship with confidence |
| 75-89% | Good | Address ⚠️ items, ship for non-critical flows |
| 60-74% | Needs Work | Fix ❌ items before shipping |
| Below 60% | Critical | Major redesign needed |

---

## Section 1: Information Architecture & Navigation

- [ ] Navigation structure follows **Jakob's Law** (familiar patterns)
- [ ] Primary navigation has ≤7 items (**Miller's Law**)
- [ ] Current location is always visible (breadcrumbs, active states)
- [ ] Search is available and positioned prominently
- [ ] Content hierarchy is clear (H1 → H2 → H3 logical structure)
- [ ] Related content is grouped (**Gestalt: Proximity**)
- [ ] Navigation is consistent across all pages
- [ ] Destructive navigation (leaving unsaved work) is warned

---

## Section 2: Visual Design & Hierarchy

- [ ] Visual hierarchy clearly guides the eye to the most important element first
- [ ] Primary CTA is visually dominant (**Von Restorff Effect**)
- [ ] Only ONE primary CTA per view (if multiple are present, one must be clearly dominant)
- [ ] Consistent color system (semantic colors for status: error, warning, success, info)
- [ ] Typography scale is consistent (limited set of sizes with clear purpose)
- [ ] Whitespace is used intentionally to create breathing room
- [ ] Visual rhythm/spacing is based on a consistent grid (4px or 8px baseline)
- [ ] Iconography style is consistent (don't mix outlined and filled)
- [ ] Important elements are at list beginning/end (**Serial Position Effect**)

---

## Section 3: Interaction Design

- [ ] Interactive elements look interactive (buttons look clickable, links look like links)
- [ ] Hover/focus/active states exist for all interactive elements
- [ ] Touch/click targets meet minimum size (44×44px web, 48×48dp mobile)
- [ ] Adequate spacing between adjacent interactive targets (≥8px)
- [ ] Primary actions are within easy reach (**Fitts's Law**, thumb zone on mobile)
- [ ] System responds within 400ms for user interactions (**Doherty Threshold**)
- [ ] Loading states shown for any delay >400ms
- [ ] Skeleton screens used instead of full-page spinners (preferred)
- [ ] Animations serve a purpose (don't animate for decoration)
- [ ] Animations respect `prefers-reduced-motion`

---

## Section 4: Forms & Input

- [ ] Form fields are logically grouped with clear section labels
- [ ] Labels are visible (not placeholder-only labels)
- [ ] Required fields are clearly indicated (asterisk + legend, not color alone)
- [ ] Real-time validation with helpful error messages
- [ ] Error messages follow the formula: What happened + Why + How to fix
- [ ] Character counts shown for fields with limits
- [ ] Smart defaults reduce input effort
- [ ] Auto-save for long/complex forms
- [ ] Tab order is logical (left-to-right, top-to-bottom)
- [ ] Input types match content (email, tel, number, date)
- [ ] Autofill/autocomplete attributes are set correctly

---

## Section 5: Content & Messaging

- [ ] Language is user-facing (no developer jargon or HTTP codes)
- [ ] Labels and CTAs use consistent terminology throughout
- [ ] Action labels are specific ("Save changes" not just "Submit")
- [ ] Confirmation messages tell the user what happened
- [ ] Error messages are constructive and blame-free
- [ ] Empty states provide guidance (not just "No data")
- [ ] Helpful microcopy exists where users might hesitate
- [ ] Tone matches the brand and user expectations
- [ ] Content is scannable (headings, bullets, short paragraphs)

---

## Section 6: Accessibility (WCAG 2.1 AA)

### Color & Contrast
- [ ] Body text contrast ≥ 4.5:1
- [ ] Large text contrast ≥ 3:1
- [ ] UI components and icons contrast ≥ 3:1
- [ ] Color is not the sole conveyor of information
- [ ] Focus indicators are visible with ≥ 3:1 contrast
- [ ] Tested with color blindness simulation

### Keyboard & Screen Reader
- [ ] All interactive elements are keyboard-accessible
- [ ] Focus order matches visual layout
- [ ] Skip-to-content link exists
- [ ] Modals trap focus properly
- [ ] ARIA labels present for icon-only buttons
- [ ] Semantic HTML used (headings, lists, landmarks)
- [ ] Dynamic content changes announced to screen readers

### Responsive & Zoom
- [ ] Works at 200% zoom without content loss
- [ ] Text spacing can be overridden (WCAG 1.4.12)
- [ ] No horizontal scrolling at 320px viewport width
- [ ] Touch targets are adequately sized on mobile

---

## Section 7: Dark Mode

- [ ] Background is `#121212` or similar dark grey (NOT `#000000`)
- [ ] Surface elevation uses progressively lighter greys
- [ ] Text contrast meets WCAG 2.1 AA on dark backgrounds
- [ ] Accent colors are desaturated (20-30% less saturation)
- [ ] Images have dark mode treatment (overlay, alternative versions)
- [ ] Focus indicators remain visible
- [ ] Status colors are distinguishable on dark backgrounds
- [ ] `prefers-color-scheme` media query is respected
- [ ] Form inputs have visible borders
- [ ] Charts and data visualizations are legible

---

## Section 8: AI Features (if applicable)

- [ ] AI-generated content is visually distinguished (badge, color, border)
- [ ] Processing shows specific step progress (not just "Loading...")
- [ ] Undo available for all AI actions
- [ ] Cancel available during AI processing
- [ ] Feedback mechanism exists (thumbs up/down minimum)
- [ ] Explanations available for AI recommendations
- [ ] Confidence level displayed when relevant
- [ ] Manual override always possible (human can override AI)
- [ ] Automation level controllable per feature
- [ ] AI limitations/disclaimers are transparent

---

## Section 9: Enterprise Features (if applicable)

- [ ] Role-based access is reflected in the UI (RBAC)
- [ ] Restricted features are hidden or disabled with explanation
- [ ] Bulk operations available for repetitive tasks
- [ ] Keyboard shortcuts for frequent actions
- [ ] Data tables support sort, filter, search, export
- [ ] Saved views/presets for common configurations
- [ ] Audit trail visible for admins
- [ ] Multi-tenancy/branding support
- [ ] Offline/degraded network handling
- [ ] Change management (what's new, update notices)

---

## Section 10: User Flow Quality

- [ ] Core task flows are completable in minimum steps
- [ ] Every path leads to a resolution (no dead ends)
- [ ] Error recovery is possible at every step
- [ ] Feedback is provided at every step (confirmation, status)
- [ ] Back navigation preserves entered data
- [ ] Empty/first-use states guide the user to action
- [ ] Edge cases are handled (overflow text, many items, no data)
- [ ] All documented states exist (default, loading, empty, error, success)

---

## Section 11: Performance Perception

- [ ] Above-the-fold content renders within 1.5 seconds
- [ ] Interactive response within 400ms (**Doherty Threshold**)
- [ ] Skeleton screens used for content loading
- [ ] Optimistic UI for user actions where appropriate
- [ ] Progressive loading for heavy content (images, data)
- [ ] No layout shift during loading (CLS < 0.1)

---

## Section 12: Sustainability

- [ ] Dark mode available (OLED battery savings)
- [ ] Images optimized (WebP/AVIF, responsive srcset)
- [ ] Vector graphics used where possible (SVG over PNG)
- [ ] Lazy loading for below-fold content
- [ ] No auto-playing video (requires user interaction)
- [ ] Page weight under 500KB for critical path

---

## Review Summary Template

```
Design Review: [Project/Feature Name]
Date: [YYYY-MM-DD]
Reviewer: PD (AI Product Designer)

DESIGN HEALTH SCORE: [XX]%

Section Scores:
1. Information Architecture:  [XX]%
2. Visual Design:             [XX]%
3. Interaction Design:        [XX]%
4. Forms & Input:             [XX]%
5. Content & Messaging:       [XX]%
6. Accessibility:             [XX]%
7. Dark Mode:                 [XX]%
8. AI Features:               [XX]% (or N/A)
9. Enterprise Features:       [XX]% (or N/A)
10. User Flow Quality:        [XX]%
11. Performance Perception:   [XX]%
12. Sustainability:           [XX]%

CRITICAL ISSUES (Severity 4):
- [Issue description] → [Recommended fix]

MAJOR ISSUES (Severity 3):
- [Issue description] → [Recommended fix]

MINOR ISSUES (Severity 2):
- [Issue description] → [Recommended fix]

COSMETIC ISSUES (Severity 1):
- [Issue description] → [Recommended fix]

STRENGTHS:
- [What the design does well]

NEXT STEPS:
1. [Prioritized action item]
2. [Prioritized action item]
3. [Prioritized action item]
```
