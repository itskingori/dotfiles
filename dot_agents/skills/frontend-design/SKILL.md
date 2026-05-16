---
name: frontend-design
description: Design and build distinctive, production-ready frontend interfaces with a clear visual direction, grounded in accessibility, responsiveness, and product context.
---

## When To Use This Skill

Use this skill for frontend work where visual quality and design judgement matter: pages, components, flows, dashboards, or marketing surfaces.

## Core Approach

1. Understand purpose, audience, and constraints before writing code.
2. Identify the surface type first: branded marketing surface, content/editorial page, or product/app UI.
3. Choose a clear visual direction and carry it through consistently.
4. Build real, shippable UI code, not concept-only mockups.
5. Match design complexity to product needs, content density, and performance budgets.

## Before Building

- Clarify whether the task extends an existing product UI or starts a new direction.
- Decide what the first viewport must communicate in one glance.
- Identify which design levers matter most for this task: typography, colour, layout, motion, depth, imagery, or interaction feedback.
- Name one memorable quality the interface should communicate (for example: precise, calm, energetic, editorial, playful, industrial).
- State key implementation constraints early (framework, a11y, browser support, runtime budget, design-system requirements).

## Composition And Hierarchy

- Treat the first viewport as one composition, not a pile of independent blocks.
- On branded pages, ensure brand or product identity is unmistakable in the first viewport.
- Give each section one job, one dominant visual idea, and one primary takeaway or action.
- Reduce clutter: avoid competing promos, stat strips, badge piles, and repeated micro-sections unless they are task-critical.

## Design Priorities

- Typography drives hierarchy and tone. Avoid default font stacks when a stronger choice improves the interface.
- Colour should be intentional and cohesive. Use variables or tokens to keep usage consistent.
- Layout should support narrative and scanning. Balance novelty with clarity.
- Motion should clarify state and add emphasis, not distract from content.
- Use imagery as a real visual anchor when the surface depends on atmosphere, place, product, or story.
- Backgrounds and surface details should add depth only when they reinforce the core visual direction.

## Implementation Priorities

- Preserve accessibility basics: semantic structure, keyboard access, focus visibility, and adequate colour contrast.
- Ensure responsive behaviour across common breakpoints and input types.
- Keep performance reasonable: avoid heavy effects that harm readability or speed.
- For visually led work, ship 2-3 intentional motions that reinforce hierarchy or affordance.
- Reuse existing tokens, components, and interaction patterns when working inside an established system.

## Surface-Specific Defaults

- Branded or promotional surfaces: prioritise one strong hero composition, concise copy, and a clear CTA path.
- Product or operational surfaces: prioritise utility copy, scanability, status clarity, and decision support over campaign-style framing.
- Do not force landing-page art direction onto dashboards or tools unless explicitly requested.

## Guardrails

- Do not default to interchangeable SaaS patterns unless the task explicitly asks for them.
- Default away from cards when plain layout communicates as well; use cards when they materially improve interaction or comprehension.
- Do not use decorative gradients or textures as a substitute for a real visual anchor.
- Do not rely on decorative effects to compensate for weak hierarchy or unclear layout.
- Do not force a new aesthetic onto an existing product without explicit direction.
- If an initial idea feels generic, explore a less obvious direction before committing.

## Litmus Checks

- Is the first viewport understandable at a glance as one composition?
- Is brand or product identity clear when the task requires it?
- Does each section have one job?
- Can users scan headings and understand structure quickly?
- Are cards and effects doing real work?
- Does motion improve hierarchy or feedback instead of adding noise?

## Relationship To Other Skills

- This skill is general frontend design guidance.
- Use `tailwind-plus` separately when the task specifically needs Tailwind Plus reference-driven implementation.
