# 01 — UX Psychology & Behavioral Laws

This document is the foundational knowledge base for cognitive principles that drive every design decision PD makes. Every recommendation should trace back to one or more of these laws.

---

## 1. Jakob's Law (Jakob's Law of Internet User Experience)

**Statement:** Users spend most of their time on *other* sites. They prefer your site to work the same way as all the other sites they already know.

**Design Implications:**
- Adopt familiar UI conventions (e.g., logo top-left links to home, shopping cart icon top-right)
- Follow platform-specific patterns (iOS Human Interface Guidelines, Material Design)
- When innovating, do so incrementally — never break all conventions simultaneously
- Use competitive audits to understand the mental models users bring to your product

**When to Apply:**
- Navigation structure decisions
- Icon and interaction pattern choices
- Onboarding flow design (leverage transfer learning)
- Migration from legacy systems (preserve familiar workflows)

**Anti-Pattern:** Inventing a completely novel navigation scheme "to be different" — this increases cognitive load and abandonment.

---

## 2. Miller's Law (The Magical Number Seven, Plus or Minus Two)

**Statement:** The average person can hold only 7 (±2) items in working memory at any given time.

**Design Implications:**
- Chunk information into groups of 5-9 items maximum
- Phone numbers, credit card fields → break into segments (XXX-XXXX-XXXX)
- Navigation menus → limit top-level items to 5-7
- Dashboard widgets → group related metrics into logical clusters
- Use progressive disclosure to prevent information overload

**When to Apply:**
- Form design (group related fields)
- Navigation architecture (limit primary nav items)
- Data table column planning
- Settings and configuration screens
- Onboarding step counts

**Nuance:** Miller's Law refers to *chunks*, not individual items. A well-organized group of 20 items (in 4 chunks of 5) can be easier to process than 10 unstructured items.

---

## 3. Hick's Law (Hick-Hyman Law)

**Statement:** The time it takes to make a decision increases logarithmically with the number and complexity of choices.

**Formula:** RT = a + b × log₂(n), where n = number of equally probable choices.

**Design Implications:**
- Reduce the number of options visible at any decision point
- Break complex choices into a series of simpler steps (wizard pattern)
- Highlight recommended/default options to reduce decision friction
- Use smart defaults based on user behavior data
- Categorize and filter long lists rather than presenting them flat

**When to Apply:**
- Pricing page design (3 tiers is optimal, highlight "most popular")
- Dropdown menus with many options → use search + categorization
- Settings screens → group into tabs, show common settings first
- E-commerce category pages → faceted filtering
- Any screen where the user must choose between >5 options

**Anti-Pattern:** A single dropdown with 200+ country names and no search/filtering.

**Quantified Example:**
| Choices | Relative Decision Time |
|---------|----------------------|
| 2       | 1.0x (baseline)      |
| 4       | 2.0x                 |
| 8       | 3.0x                 |
| 16      | 4.0x                 |
| 64      | 6.0x                 |

---

## 4. Doherty Threshold

**Statement:** Productivity soars when a computer and its users interact at a pace (<400ms) that ensures neither has to wait on the other.

**Design Implications:**
- Target <400ms for all interactive responses
- If processing takes >400ms, show a progress indicator immediately
- Use optimistic UI updates (show result before server confirms)
- Implement skeleton screens instead of spinners for perceived speed
- Pre-fetch likely next content (e.g., next page of results)

**Specific Thresholds:**
| Response Time | User Perception |
|--------------|----------------|
| 0-100ms      | Instantaneous — direct manipulation feel |
| 100-400ms    | Slight delay — still feels responsive |
| 400ms-1s     | Noticeable lag — user starts to lose focus |
| 1-4s         | Needs progress indicator |
| 4-10s        | Needs progress bar with estimation |
| >10s         | Must allow background processing + notification |

**When to Apply:**
- Search result rendering
- Form submission feedback
- Page transition animations
- API-dependent UI updates
- Real-time collaboration features

---

## 5. Serial Position Effect (Primacy & Recency)

**Statement:** People tend to remember the first items (primacy effect) and last items (recency effect) in a series best, with the middle items most poorly remembered.

**Design Implications:**
- Place the most important actions/information at the **beginning and end** of lists
- In navigation bars, put key items first (left) and last (right)
- In onboarding, make the first and last steps the most impactful
- For CTAs in a list, put the primary CTA first or last — never buried in the middle
- In mobile tab bars (typically 5 items), prioritize the first and last positions

**Application Examples:**
- **Navigation bar:** Home (first) ... Profile/Cart (last)
- **Feature list:** Most compelling feature first, second-most compelling last
- **Pricing table:** Free (first), Enterprise (last), Standard (middle)
- **Email/notification:** Key message in first line and last line

---

## 6. Von Restorff Effect (Isolation Effect)

**Statement:** When multiple similar objects are present, the one that differs from the rest is most likely to be remembered.

**Design Implications:**
- Visually distinguish the most important element (color, size, shape, animation)
- Use color contrast to highlight primary CTAs against secondary options
- In pricing tables, visually elevate the recommended plan (border, badge, scale)
- Important notifications/alerts should break the visual pattern of surrounding content
- Use whitespace to isolate key elements

**Application Rules:**
1. Only ONE element should be "isolated" per view — if everything is special, nothing is
2. The isolation should serve the user's goal, not just visual interest
3. Combine with Serial Position Effect for maximum impact

**Anti-Pattern:** Highlighting 4 out of 5 options, making the "normal" one feel isolated instead of the intended choice.

---

## 7. Fitts's Law

**Statement:** The time to reach a target is a function of the distance to and size of the target.

**Formula:** T = a + b × log₂(1 + D/W), where D = distance, W = width of the target.

**Design Implications:**
- Make frequently used buttons large and easy to reach
- Place primary actions close to the user's current focus area
- Minimum touch target: **44×44px** (iOS) / **48×48dp** (Android)
- Edge and corner targets are faster (infinite width on screen edges)
- Floating action buttons (FAB) should be in thumb-reach zones on mobile

**Mobile Thumb Zones:**
- Easy reach: Bottom-center of screen
- Okay reach: Bottom-left/right corners
- Hard reach: Top of screen (especially top-left for right-handed users)

---

## 8. Gestalt Principles

### Proximity
Items placed close together are perceived as related. Use consistent spacing to create visual groups without borders.

### Similarity
Elements that look alike (color, shape, size) are perceived as having the same function. Maintain consistent styling for similar actions.

### Continuity
The eye follows the smoothest path. Align elements along clear visual lines. Use consistent left-alignment for readability.

### Closure
The brain completes incomplete shapes. Use this for loading indicators, progress bars, and icon design.

### Common Region
Elements within the same bounded area (card, box, background color) are perceived as grouped. Use cards and containers to organize related content.

### Figure-Ground
Users can distinguish an object (figure) from its surrounding area (ground). Ensure clear distinction between interactive elements and backgrounds. Critical for modal/overlay design.

---

## 9. Cognitive Load Theory

**Three Types of Cognitive Load:**

| Type | Description | Design Strategy |
|------|-------------|----------------|
| **Intrinsic** | Inherent complexity of the task | Cannot be reduced — match user's expertise level |
| **Extraneous** | Caused by poor presentation | Minimize through clear layout, consistent patterns |
| **Germane** | Effort spent building mental models | Support through progressive disclosure, good IA |

**Reduction Strategies:**
- Remove unnecessary elements (visual noise, redundant labels)
- Use recognition over recall (show options, don't make users remember)
- Provide contextual help instead of front-loaded instructions
- Use consistent interaction patterns across the product
- Break complex tasks into manageable steps

---

## 10. Zeigarnik Effect

**Statement:** People remember uncompleted tasks better than completed ones.

**Design Implications:**
- Show progress indicators for multi-step processes (profile completion, onboarding)
- Use progress bars to motivate task completion
- "Complete your profile" prompts leverage this effect
- Gamification elements (achievement progress) tap into this drive

---

## 11. Peak-End Rule

**Statement:** People judge an experience based largely on how they felt at its most intense point (peak) and at its end, rather than the sum or average of every moment.

**Design Implications:**
- Invest heavily in the first impression (onboarding) and final moment (confirmation/thank-you)
- Error states are often "peaks" — make error recovery graceful and helpful
- Checkout completion should feel rewarding (animation, positive messaging)
- Offboarding (account deletion) should be respectful — it's the "end" that sticks

---

## 12. Aesthetic-Usability Effect

**Statement:** Users perceive aesthetically pleasing designs as more usable, even if they aren't objectively more efficient.

**Design Implications:**
- Visual polish is not superficial — it directly impacts perceived usability
- Invest in typography, spacing, and color harmony
- A well-designed error state feels less frustrating than an ugly one
- But never sacrifice actual usability for aesthetics — the effect has limits

---

## 13. Endowment Effect & Loss Aversion

**Statement:** People overvalue things they already possess and are more motivated by the fear of loss than the prospect of equivalent gain.

**Design Implications:**
- Free trials let users "own" the experience before paying
- Show what users will lose if they downgrade ("You'll lose access to X, Y, Z")
- Shopping cart abandonment emails: "Your items are waiting" (they already "own" them mentally)
- Progress indicators: "You've completed 80% — don't lose your progress"

**Ethical Boundary:** Use to inform, not manipulate. Never create false urgency or misleading loss scenarios.

---

## 14. Habit Loop & Persistent Habits Principle

**Statement:** Users develop habitual patterns (Cue → Routine → Reward) that become deeply ingrained over time. Disrupting these habits increases friction.

**Design Implications:**
- Place frequently used features in consistent, predictable locations
- Maintain spatial consistency across updates — don't move core UI elements
- When redesigning, preserve the locations of critical navigation items
- Build positive habit loops: clear trigger → simple action → immediate reward

---

## 15. Identity Principle

**Statement:** Users align with brands and products that reflect their self-image and values. When a product resonates with a user's identity, trust and conversion increase.

**Design Implications:**
- Use language, imagery, and design aesthetics that reflect the target user's aspirations
- Testimonials and social proof should feature people the target user identifies with
- Brand consistency reinforces identity alignment over time
- Personalization features let users make the product "theirs"

---

## Cross-Reference Matrix

| Design Decision | Primary Laws | Secondary Laws |
|----------------|-------------|----------------|
| Navigation structure | Jakob's, Miller's, Serial Position | Gestalt (Proximity) |
| CTA placement | Fitts's, Von Restorff, Serial Position | Aesthetic-Usability |
| Form design | Miller's, Cognitive Load | Hick's, Zeigarnik |
| Loading states | Doherty Threshold | Peak-End, Zeigarnik |
| Onboarding | Peak-End, Zeigarnik | Jakob's, Progressive Disclosure |
| Pricing page | Hick's, Von Restorff | Endowment, Serial Position |
| Error handling | Peak-End, Cognitive Load | Aesthetic-Usability |
| Search & filtering | Hick's, Miller's | Doherty Threshold |
| Mobile layout | Fitts's, Miller's | Gestalt, Serial Position |
| Dark mode | Aesthetic-Usability | Accessibility (see 04) |
