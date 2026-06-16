---
tags: [workflow, template, prompt, stable]
updated: 2026-06-16
---

# Generic Layout Prompt

> **Implementation prompt for building pages/sections.** This prompt consumes a normalized design spec (generated via [[design-spec-auto-intake]]) and builds production-ready components.
>
> **Quick start:** Say *"Build a page in the style of [website/designer]"* → AI auto-extracts design → generates `design-spec.json` → uses this prompt to build.
>
> For manual spec handoff or Figma-direct workflows, see companion docs: [[new-page]] and [[ai-agent-guide]].

---

## How to Use This Prompt

### Path 1: Auto-Intake (Recommended)

1. **User says:** *"Build a landing page like Stripe"*
2. **AI executes:** [[design-spec-auto-intake]] workflow
3. **Output:** `design-spec.json` (auto-generated)
4. **Pass to this prompt:** Use the JSON as context below

### Path 2: Manual Spec Handoff

1. **You provide:** `design-spec.json` (manually created or from design tool export)
2. **Pass to this prompt:** Reference the JSON file
3. **Continue below:** Fill in [PAGE NAME] and any Figma references

### Path 3: Direct Figma Reference (Legacy)

1. **You provide:** Figma frame URLs
2. **Continue below:** Fill placeholders, use Figma MCP server to extract specs

---

## Design Spec Reference

**Before proceeding, ensure you have a normalized `design-spec.json`.**

If using auto-intake, the JSON is auto-generated. If manual, reference:
- File location: `src/data/specs/design-spec.json` (or your chosen location)
- Contains: All tokens (colors, typography, spacing), layout specs, animations, accessibility requirements

**The implementation below will reference this JSON for all design decisions.**

---

## Implementation Brief

We need to implement the **[PAGE NAME]** page/section based on the design spec.

### Design References

**Design Spec Source:**