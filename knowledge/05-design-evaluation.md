# 05 — Design Process Evaluation & Documentation

This document provides systematic frameworks for evaluating designs, scoring usability issues, optimizing user flows, and creating comprehensive design documentation for developer handoff.

---

## 1. Nielsen's 10 Usability Heuristics — Deep Application Guide

### H1: Visibility of System Status
> The design should always keep users informed about what is going on, through appropriate feedback within reasonable time.

**Evaluation Questions:**
- Does the system show the current state? (Loading, processing, saved, error)
- Are progress indicators used for operations >1 second?
- Do form fields show validation state in real-time?
- Is the user's current location clear? (Breadcrumbs, active nav state, page title)
- Are background processes visible? (Sync status, upload progress)

**Common Violations:**
- No loading indicator during API calls
- Form submits with no success/failure feedback
- Active navigation item not highlighted
- No "last saved" indicator for auto-save features

---

### H2: Match Between System and Real World
> The design should speak the users' language, with words, phrases, and concepts familiar to the user.

**Evaluation Questions:**
- Is the language user-facing (not developer-facing)?
- Are icons universally recognizable (not abstract)?
- Does the information appear in a natural, logical order?
- Are industry-specific terms used correctly for the target audience?

**Common Violations:**
- Error messages showing HTTP status codes ("Error 500")
- Technical jargon in user-facing UI ("null reference," "timeout exception")
- Illogical field order in forms (asking for city before country)

---

### H3: User Control and Freedom
> Users often perform actions by mistake and need a clearly marked "emergency exit" to leave the unwanted action without going through an extended process.

**Evaluation Questions:**
- Can users undo recent actions? (Ctrl+Z, undo button)
- Can users cancel in-progress operations?
- Can users navigate back easily? (Back button, breadcrumbs)
- Are "destructive" actions reversible or confirmed?
- Can users exit workflows without losing progress?

**Common Violations:**
- No undo for email send, message post, or item deletion
- Multi-step forms that lose data when navigating back
- No cancel option during file uploads
- Account deletion without confirmation or grace period

---

### H4: Consistency and Standards
> Users should not have to wonder whether different words, situations, or actions mean the same thing.

**Evaluation Questions:**
- Are the same words used for the same concepts throughout?
- Do similar actions have the same interaction pattern?
- Does the design follow platform conventions?
- Are visual styles (colors, typography, spacing) consistent?
- Are component behaviors predictable?

**Common Violations:**
- "Submit," "Save," "Confirm," and "Done" used interchangeably
- Some lists are sortable, others aren't (inconsistent)
- Primary button color changes between pages
- Different icon styles mixed (outlined + filled)

---

### H5: Error Prevention
> Good error messages are important, but the best designs prevent problems from occurring in the first place.

**Evaluation Questions:**
- Are destructive actions confirmed before execution?
- Do forms validate in real-time (before submission)?
- Are constraints communicated before the user acts? (File size limits, character counts)
- Are common errors anticipated and designed around?
- Is undo available as a safety net?

**Common Violations:**
- No character count for fields with limits
- No file type/size validation before upload starts
- "Delete" button with no confirmation
- No autosave for long forms

---

### H6: Recognition Rather Than Recall
> Minimize the user's memory load by making elements, actions, and options visible.

**Evaluation Questions:**
- Are recently used/viewed items accessible?
- Do search fields show suggestions and recent searches?
- Are form fields pre-filled when possible?
- Is contextual help available where users need it?
- Are related actions grouped together?

**Common Violations:**
- Search with no history or suggestions
- Requiring users to re-enter information already provided
- Settings buried deep with no search capability
- Error messages that don't indicate which field has the error

---

### H7: Flexibility and Efficiency of Use
> Shortcuts — hidden from novice users — can speed up the interaction for expert users.

**Evaluation Questions:**
- Are keyboard shortcuts available for frequent actions?
- Can users customize their workspace/view?
- Are there power-user features (bulk actions, command palette)?
- Do defaults serve the majority while allowing customization?
- Are there templates or presets for common tasks?

**Common Violations:**
- No keyboard shortcuts in a daily-use tool
- Forcing all users through the same rigid workflow
- No bulk action capability for repetitive tasks
- No saved filters or view presets

---

### H8: Aesthetic and Minimalist Design
> Interfaces should not contain information that is irrelevant or rarely needed.

**Evaluation Questions:**
- Is every element on the screen serving a purpose?
- Is the visual hierarchy clear? (What should the user see first?)
- Are secondary/tertiary actions appropriately de-emphasized?
- Is whitespace used effectively to reduce visual clutter?
- Are content-to-chrome ratios healthy?

**Common Violations:**
- Competing CTAs of equal visual weight
- Dense screens with no clear entry point
- Decorative elements that add no informational value
- Tooltips/badges/labels that repeat obvious information

---

### H9: Help Users Recognize, Diagnose, and Recover from Errors
> Error messages should be expressed in plain language, precisely indicate the problem, and constructively suggest a solution.

**Evaluation Questions:**
- Are error messages written in plain language?
- Do they explain what went wrong specifically?
- Do they suggest how to fix the problem?
- Are errors displayed near the source of the problem?
- Is the error state visually distinct but not alarming?

**Error Message Formula:**
```
[What happened] + [Why it happened (if helpful)] + [What to do next]
```

**Bad:** "Error: Invalid input"
**Good:** "This email is already registered. Try signing in instead, or use a different email."

---

### H10: Help and Documentation
> It's best if the system can be used without documentation, but it may be necessary to provide help and documentation.

**Evaluation Questions:**
- Is help searchable?
- Is contextual help available (tooltips, inline hints)?
- Are help articles task-oriented (not just feature descriptions)?
- Is there a clear path to human support when self-service fails?
- Are first-time features accompanied by onboarding guidance?

---

## 2. Severity Rating Scale

Use this scale to prioritize usability issues found during evaluation:

| Rating | Label | Definition | Action |
|--------|-------|-----------|--------|
| **0** | Not a Problem | Evaluator disagrees this is a usability problem | No action needed |
| **1** | Cosmetic | Superficial issue; fix only if extra time is available | Low priority — backlog |
| **2** | Minor | Minor usability problem; fixing should be given low priority | Medium priority — next sprint |
| **3** | Major | Major usability problem; important to fix, high priority | High priority — this sprint |
| **4** | Catastrophe | Usability catastrophe; imperative to fix before release | **Blocker — fix immediately** |

### Severity Scoring Criteria

Score each issue across three dimensions:

| Dimension | Low (1) | High (3) |
|-----------|---------|----------|
| **Frequency** | Rare edge case | Happens to most users regularly |
| **Impact** | Annoying but user can proceed | User cannot complete task |
| **Persistence** | One-time (user learns to avoid) | Repeated (no workaround) |

**Severity = max(Frequency, Impact, Persistence)**
- If any dimension scores 3 AND the user cannot complete a core task → Severity 4

---

## 3. User Flow Optimization

### Flow Diagram Standards

**Direction:** Always one direction — **left to right** OR **top to bottom** (never mix).

**Node Types:**

| Shape | Meaning | Example |
|-------|---------|---------|
| **Rounded rectangle** | Start/End point | "User opens app" / "Task complete" |
| **Rectangle** | Action/Screen | "Fills out form" / "Dashboard view" |
| **Diamond** | Decision point | "Is user logged in?" → Yes/No |
| **Parallelogram** | Input/Output | "User enters email" |
| **Circle** | Connector (continues elsewhere) | A, B (reference markers) |

### Flow Optimization Checklist

- [ ] **Minimum steps:** Can any steps be combined or eliminated?
- [ ] **Dead ends:** Does every path lead to a resolution? (No orphaned states)
- [ ] **Error recovery:** At every step, what happens if something goes wrong?
- [ ] **Feedback at every step:** Does the user receive confirmation/status at each point?
- [ ] **Back navigation:** Can the user go back without losing data?
- [ ] **Edge cases:** What about empty states, first-time users, error states?
- [ ] **Accessibility path:** Can the entire flow be completed via keyboard? Via screen reader?
- [ ] **Performance:** Are there bottlenecks (API calls, file uploads) that need loading states?

### Measuring Flow Quality

| Metric | Definition | Target |
|--------|-----------|--------|
| **Task completion rate** | % of users who finish the flow | >90% for core flows |
| **Time on task** | Average time to complete | Decreasing over time |
| **Error rate** | % of users who encounter errors | <5% for core flows |
| **Drop-off rate** | % who abandon at each step | Identify and fix top drop-off points |
| **Satisfaction (SUS/CSAT)** | User-reported ease of use | SUS >68 (above average) |

---

## 4. Design Handoff Documentation

### The Handoff Document Structure

A complete design handoff should include:

#### A. Design Overview
- **Problem statement:** What user problem does this solve?
- **Success metrics:** How will we measure if this works?
- **Target users:** Who is this for? (Persona reference)
- **Scope:** What's included and explicitly excluded

#### B. Design Rationale
> This is the most commonly missing — and most critical — part of handoff.

For every significant design decision, document:
- **What:** The design decision made
- **Why:** The reasoning (reference to user research, psychology principle, business goal)
- **Alternatives considered:** What other approaches were evaluated and why they were rejected
- **Constraints:** What limitations influenced the decision (technical, time, brand)

**Example:**
```
Decision: Use a step-by-step wizard instead of a single long form for the onboarding flow.
Why: User research showed 67% drop-off on the previous single-page form.
     Hick's Law suggests reducing visible choices at each step improves completion.
Alternatives: Accordion-style form (rejected — still shows all fields),
              Multi-column layout (rejected — not mobile-friendly).
Constraint: Must work on mobile (320px minimum width).
```

#### C. Specifications

**Layout Specs:**
- Grid system (12-column, 8px baseline grid)
- Breakpoints (mobile, tablet, desktop)
- Spacing tokens used
- Component positioning (with annotations)

**Component Specs:**
- Component name and variant used
- Props/states (default, hover, active, focus, disabled, error, loading)
- Content constraints (min/max character counts)
- Responsive behavior at each breakpoint

**Interaction Specs:**
- Trigger → Action → Feedback (for every interactive element)
- Animation details (duration, easing, property)
- Conditional logic (if X, then show Y)
- Keyboard interactions
- Screen reader announcements

**Content Specs:**
- Final copy for all labels, messages, and CTAs
- Truncation rules for dynamic content
- Localization notes (text expansion, RTL behavior)
- Placeholder and empty state content

#### D. States & Edge Cases

**Required States to Document:**

| State | Description |
|-------|-------------|
| **Default** | Normal, idle state |
| **Loading** | Data being fetched |
| **Empty** | No data yet (first use) |
| **Error** | Something went wrong |
| **Success** | Action completed successfully |
| **Partial** | Some data loaded, some failed |
| **Offline** | No network connection |
| **Permission denied** | User lacks access |
| **Overflow** | Too much data (long names, many items) |
| **Skeleton** | Loading placeholder |

#### E. Accessibility Notes
- Tab order specification
- ARIA attributes needed
- Screen reader announcement text
- Focus management behavior
- Color contrast verification results

---

## 5. Design Review Meeting Framework

### Pre-Review Preparation
1. Share designs with reviewers 24 hours in advance
2. Provide context document (problem statement, constraints, personas)
3. Define the scope of feedback being sought
4. Prepare a walkthrough script covering all key flows

### Review Session Structure (60 minutes)

| Time | Activity |
|------|----------|
| 0-5 min | Context setting (problem, users, constraints) |
| 5-15 min | Designer walkthrough of key flows |
| 15-40 min | Structured feedback (heuristic-by-heuristic) |
| 40-50 min | Prioritization of issues (severity scoring) |
| 50-60 min | Action items and next steps |

### Post-Review Documentation
- List all issues found with severity ratings
- Assign owners and deadlines for each issue
- Schedule follow-up review if Severity 3-4 issues exist
- Update design file with review annotations
