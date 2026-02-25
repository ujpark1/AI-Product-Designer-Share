# Desi — AI Product Designer Agent

An AI agent for [Claude Code](https://docs.anthropic.com/en/docs/claude-code) that acts as your expert Product Designer. Desi provides evidence-based design recommendations grounded in cognitive psychology, accessibility standards, and real-world usability data.

**Desi is not a theme or a template.** It's a knowledge-powered design partner that reviews your work, catches issues, and backs every recommendation with specific principles.

---

## What Desi Can Do

| Area | Examples |
|------|----------|
| **UX Psychology** | Apply Jakob's Law, Hick's Law, Fitts's Law, and 12 more cognitive principles to your layouts |
| **Enterprise / B2B** | Design data tables, dashboards, RBAC flows, and admin panels optimized for task completion |
| **AI Usability** | Design human-in-the-loop AI features — copilots, recommendations, chatbots, AI-generated content |
| **Accessibility** | WCAG 2.1 AA/AAA audits, contrast checks, screen reader guidance, dark mode specs |
| **Design Reviews** | Heuristic evaluation with severity scoring (0-4), actionable fixes, and a 12-section checklist |
| **Handoff Docs** | Structured documentation with design rationale for developer handoff |

---

## Installation

### Prerequisites

- [Claude Code CLI](https://docs.anthropic.com/en/docs/claude-code) installed
- An Anthropic API key or Claude Pro/Max subscription

### Setup

1. **Clone the repository**

```bash
git clone https://github.com/ujpark1/ai-product-designer.git
cd ai-product-designer
```

2. **Start Claude Code**

```bash
claude
```

That's it. Claude Code automatically reads `CLAUDE.md` and Desi introduces itself on the first message.

### Alternative: Add to an Existing Project

If you want Desi's knowledge available inside your own project:

```bash
# From your project root
git clone https://github.com/ujpark1/ai-product-designer.git .desi-agent

# Copy the knowledge base
cp -r .desi-agent/knowledge ./knowledge

# Merge or append Desi's CLAUDE.md into your existing CLAUDE.md
cat .desi-agent/CLAUDE.md >> CLAUDE.md

# Clean up
rm -rf .desi-agent
```

---

## Project Structure

```
├── CLAUDE.md                          # Agent system prompt (auto-loaded by Claude Code)
└── knowledge/
    ├── 01-ux-psychology.md            # 15 cognitive laws with design applications
    ├── 02-enterprise-b2b-ux.md        # B2B SaaS & enterprise UX patterns
    ├── 03-ai-usability.md             # AI feature design guidelines (2025-2026)
    ├── 04-accessibility-dark-mode.md  # WCAG specs, dark mode technical standards
    ├── 05-design-evaluation.md        # Heuristic evaluation & handoff documentation
    └── 06-design-review-checklist.md  # 12-section design audit checklist
```

---

## Usage Examples

### Design Review
> "Review this login screen for accessibility and usability issues."

Desi reads the relevant knowledge files, applies Nielsen's 10 Heuristics, and returns a severity-scored list of issues with specific fixes.

### New Feature Design
> "I'm designing a notification center for a B2B SaaS dashboard. What patterns should I use?"

Desi applies enterprise UX principles (progressive disclosure, power user optimization) and cognitive laws (Miller's Law for grouping, Serial Position Effect for priority placement).

### AI Feature Design
> "We're adding an AI writing assistant to our app. How should the UI work?"

Desi applies the Human-in-the-Loop framework, recommends visual distinction for AI content, and specifies undo/cancel/feedback mechanisms.

### Figma Integration
> Share a Figma URL and ask: "Review this design."

Desi uses Figma MCP tools to capture and analyze the design, then runs the full 12-section review checklist.

---

## Knowledge Base

Desi doesn't guess. Every recommendation references a specific principle:

| Principle | What It Means |
|-----------|--------------|
| **Jakob's Law** | Users expect your product to work like others they already know |
| **Miller's Law** | Chunk information into 7±2 groups |
| **Hick's Law** | Fewer choices = faster decisions |
| **Doherty Threshold** | Respond in <400ms to maintain flow |
| **Von Restorff Effect** | The different thing gets noticed |
| **Fitts's Law** | Big, close targets are easier to hit |
| **Serial Position Effect** | First and last items are remembered best |
| **WCAG 2.1 AA** | 4.5:1 contrast, 44px touch targets, keyboard accessible |

See the `knowledge/` folder for the full reference (1,800+ lines of design guidance).

---

## License

MIT
