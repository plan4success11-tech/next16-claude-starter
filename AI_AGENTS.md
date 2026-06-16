# AI Agent Instructions

## Quick Start for Claude Code & Anti-Gravity

This document provides specific instructions for using this repo with AI agents.

---

## 🤖 For Claude Code

### Setup

1. Open this repo in Claude Code: https://github.com/plan4success11-tech/next16-claude-starter
2. Install dependencies:
   ```bash
   yarn install
   yarn dev
   ```

### Using the Design Workflows

#### Building a New Page from Scratch

**Option 1: Auto-Intake (Recommended)**

Tell Claude:
> "Build a landing page in the style of www.jdsports.com"

Claude will automatically:
1. Execute the `[[design-spec-auto-intake]]` workflow
2. Search and extract all design data from the site
3. Generate a `design-spec.json` file
4. Use the design spec to build production-ready components

**Option 2: Manual Intake**

If you have design specs already:
> "I have a design-spec.json for a pricing page. Build it using `generic-layout-prompt`."

Claude will:
1. Reference the JSON spec
2. Consult `obsidian/workflows/generic-layout-prompt.md`
3. Build components matching the spec exactly

#### Generic Layout Prompt

For detailed instructions on implementing a page/section, reference:
- File: `obsidian/workflows/generic-layout-prompt.md`
- Use this when you want to specify requirements directly

### Key Files for Claude

| File | Purpose |
|------|---------|
| `obsidian/workflows/generic-layout-prompt.md` | Implementation instructions + all component rules |
| `obsidian/workflows/design-spec-auto-intake.md` | AI auto-extraction workflow |
| `obsidian/workflows/ai-agent-guide.md` | Full rules & conventions |
| `obsidian/README.md` | Project documentation (Map of Content) |

### Example Prompts

**Build a new page:**
```
Build a testimonials section in the style of Stripe's pricing page. 
Use design-spec-auto-intake to extract the design, then implement using 
generic-layout-prompt. Make it responsive and animated.
```

**Iterate on existing page:**
```
Update the homepage hero section. It should fade in when scrolled into view, 
and have a gradient background. Reference src/views/home.tsx and consult 
the generic-layout-prompt for animation rules.
```

**Add a component:**
```
Create a Card component in components/ui/card.tsx that accepts a title, 
description, and optional image. Make it semantic and accessible. 
Reference component-conventions.md for structure.
```

### Cost Notes

- **Plan required:** Claude Max (5×) recommended — this repo is token-intensive by design
- Every prompt pulls in documentation context automatically
- Standard Claude.ai Pro will hit usage limits quickly on real sessions

---

## 🔮 For Google Anti-Gravity (or Similar Tools)

### Setup

1. Point the tool at this repo: https://github.com/plan4success11-tech/next16-claude-starter
2. If uploading instead: download the ZIP from GitHub and upload

### Using the Design Workflows

#### Auto-Intake Pattern (If Supported)

If Anti-Gravity supports workflow orchestration, ask:
> "Use the design-spec-auto-intake workflow. Extract design from www.figma.com/..., generate design-spec.json, then build components."

#### Manual Flow (Recommended)

1. **Provide a design source:**
   - URL to a website
   - Figma link
   - Design system documentation
   - Or create a `design-spec.json` yourself

2. **Tell the agent:**
   ```
   I have extracted design data. Use obsidian/workflows/generic-layout-prompt.md 
   to build a [PAGE_NAME] page/section. Reference the design spec and follow 
   all component rules, animations, and accessibility requirements.
   ```

3. **Agent builds:** Components matching the spec + all conventions

### Key References for Anti-Gravity

| File | When to Reference |
|------|-------------------|
| `obsidian/workflows/generic-layout-prompt.md` | Component building, responsive layouts, animations |
| `obsidian/workflows/design-spec-auto-intake.md` | Understanding the auto-intake concept (reference only, may not execute directly) |
| `obsidian/workflows/ai-agent-guide.md` | Project rules: server components, Tailwind tokens, spring animations, semantics |
| `obsidian/architecture/animation-system.md` | How spring animations work in this project |
| `obsidian/architecture/design-system.md` | Design tokens and Tailwind configuration |
| `obsidian/architecture/component-conventions.md` | How to structure and name components |

### Example Instructions

**Build from design URL:**
```
Visit https://www.notion.so/templates and extract design patterns for:
- Layout structure (mobile & desktop)
- Color palette
- Typography scales
- Button and card styles
- Interactive states (hover, focus)

Then use obsidian/workflows/generic-layout-prompt.md to build a dashboard page 
matching those patterns. Ensure responsive design, semantic HTML, and 
Tailwind-only styling (no inline styles).
```

**Build from specs you provide:**
```
Here's a design-spec.json for a landing page. Use 
obsidian/workflows/generic-layout-prompt.md to implement all sections. 
Consult obsidian/architecture/component-conventions.md for folder structure 
and file naming. Use spring animations per obsidian/architecture/animation-system.md.
```

---

## 📋 Shared Requirements (Both Agents)

### Always Consult These Files First

| Document | Purpose |
|----------|---------|
| `obsidian/workflows/ai-agent-guide.md` | Project rules (non-negotiable) |
| `obsidian/architecture/folder-structure.md` | Where to place files |
| `obsidian/architecture/design-system.md` | Design tokens (colors, spacing, typography) |
| `obsidian/architecture/animation-system.md` | Spring-based animations only |
| `obsidian/architecture/component-conventions.md` | Component structure & naming |

### Hard Rules (No Exceptions)

1. **Animations:** Spring-based only (`@react-spring/web`). No CSS transitions or Framer Motion.
2. **Styling:** Tailwind v4 with design tokens. No hardcoded colors/spacing.
3. **Components:** Server components by default. `"use client"` only for hooks/events.
4. **Semantics:** Semantic HTML (`<button>`, `<nav>`, `<section>`). Never `<div>` when better elements exist.
5. **Typing:** No `any`. All props must be typed.
6. **Imports:** Route files import from `views/` only. All logic lives in view components.

### Workflow for Building Pages

1. **Get design spec** (auto-intake or manual)
2. **Reference** `generic-layout-prompt.md`
3. **Consult** component conventions, animation system, design tokens
4. **Build** mobile-first responsive layout
5. **Implement** spring animations per spec
6. **Use** existing components from `components/ui/` and `components/common/`
7. **Test** accessibility, typing, semantic HTML
8. **Update vault** if new patterns emerge (ADR, changelog)

---

## 🚀 Deployment

After Claude/Anti-Gravity builds your site:

```bash
yarn build
yarn lint
```

Then deploy to Vercel:

```bash
npm i -g vercel@latest
vercel --prod
```

Or use the Vercel dashboard: [vercel.com/new](https://vercel.com/new)

---

## 📚 Full Documentation

All project rules, architecture decisions, and API references live in:
- **`obsidian/README.md`** — Map of Content & starting point
- **`obsidian/workflows/`** — All workflows and playbooks
- **`obsidian/architecture/`** — System design & technical decisions

**Start there for deep dives.**

---

## ❓ Questions?

- **Project structure:** See `obsidian/architecture/folder-structure.md`
- **Animation rules:** See `obsidian/architecture/animation-system.md`
- **Component patterns:** See `obsidian/architecture/component-conventions.md`
- **Design tokens:** See `obsidian/architecture/design-system.md`
- **All conventions:** See `obsidian/workflows/ai-agent-guide.md`
