---
name: frontend-design
description: Design and build distinctive, production-ready frontend interfaces with a clear visual direction, grounded in accessibility, responsiveness, and product context.
---

## When To Use This Skill

Use this skill for frontend work where visual quality and design judgement matter: pages, components, flows, dashboards, or marketing surfaces.

## Core Approach

1. Understand purpose, audience, and constraints before writing code.
2. Choose a clear visual direction and carry it through consistently.
3. Build real, shippable UI code, not concept-only mockups.
4. Match design complexity to product needs, content density, and performance budgets.

## Before Building

- Clarify whether the task extends an existing product UI or starts a new direction.
- Identify which design levers matter most for this task: typography, colour, layout, motion, depth, or interaction feedback.
- Name one memorable quality the interface should communicate (for example: precise, calm, energetic, editorial, playful, industrial).
- State key implementation constraints early (framework, a11y, browser support, runtime budget, design-system requirements).

## Design Priorities

- Typography drives hierarchy and tone. Avoid default font stacks when a stronger choice improves the interface.
- Colour should be intentional and cohesive. Use variables or tokens to keep usage consistent.
- Layout should support narrative and scanning. Balance novelty with clarity.
- Motion should clarify state and add emphasis, not distract from content.
- Backgrounds and surface details should add depth only when they reinforce the core visual direction.

## Implementation Priorities

- Preserve accessibility basics: semantic structure, keyboard access, focus visibility, and adequate colour contrast.
- Ensure responsive behaviour across common breakpoints and input types.
- Keep performance reasonable: avoid heavy effects that harm readability or speed.
- Reuse existing tokens, components, and interaction patterns when working inside an established system.

## Guardrails

- Do not default to interchangeable SaaS patterns unless the task explicitly asks for them.
- Do not rely on decorative effects to compensate for weak hierarchy or unclear layout.
- Do not force a new aesthetic onto an existing product without explicit direction.
- If an initial idea feels generic, explore a less obvious direction before committing.

## Relationship To Other Skills

- This skill is general frontend design guidance.
- Use `tailwind-plus` separately when the task specifically needs Tailwind Plus reference-driven implementation.
