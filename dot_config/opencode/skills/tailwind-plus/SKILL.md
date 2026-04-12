---
name: tailwind-plus
description: Tailwind Plus UI blocks workflow. Uses a local licensed Tailwind Plus reference set to guide layout and implementation.
license: Proprietary
compatibility: opencode
---

## When To Use This Skill

Use this skill when Tailwind Plus UI blocks should drive page, section, and component implementation.

## Reference Root

Use this exact local reference root: ~/Repositories/itskingori/uix/reference/tailwind-plus

Treat this as a licensed local reference set. Keep exploration scoped to this path unless the task explicitly requires something else. Use this path as inspect-only reference material, not as an editable workspace.

## Workflow

1. Identify the UI intent and constraints from the request.
2. Use `manifest/blocks.json` to identify at least 3 concrete candidate references.
3. Inspect the referenced block files in `ui-blocks/`.
4. Provide a short reference synthesis before planning or implementation:
   - references reviewed
   - why each was relevant
   - patterns to keep
   - patterns to reject
   - proposed direction for the target project
5. Adapt selected patterns to the target codebase and established visual language.
6. Call out setup-sensitive dependencies and implementation caveats.
7. Load or pair with `frontend-design` when the task needs broader visual direction, hierarchy, or composition guidance.

## Minimum Evidence Rule

- Before proposing a design direction, plan, or implementation for homepage, hero, marketing section, or landing page work, inspect at least 3 relevant Tailwind Plus references and summarise what will be adapted versus rejected.
- Do not claim to be using Tailwind Plus references unless actual reference files were inspected in the current session.

## Adaptation Rules

- Adapt Tailwind Plus references to the target codebase and product context rather than copying them verbatim.
- Match the relevant block family to the task. For example, use `ui-blocks/marketing` for homepage and landing-page work, `ui-blocks/application-ui` for product surfaces and `ui-blocks/ecommerce` for shop flows.

## Marketing Adaptation Rules

For homepage, hero, marketing section and landing-page work, use Tailwind Plus references for:
- section anatomy
- layout composition
- responsive breakpoint behaviour
- spacing rhythm
- CTA placement and content density

For the same marketing work, do not copy verbatim:
- product copy
- screenshots/mockups
- decorative motifs that do not fit the product
- full page implementations without adaptation

## Guardrails

- Preserve existing design-system and product patterns when working in an established UI.
- Use reference material as guidance, not copy-paste output.
- Keep context narrowly focused on relevant files and components.
- This skill is for Tailwind Plus references, not general frontend design guidance.
- Flag uncertainty early when references imply multiple valid implementation paths.

## Privacy And Licensing

- Treat all source material under the reference root as licensed local content.
- Do not publish, commit, or redistribute raw reference material unless licensing terms explicitly allow it.
- Prefer derivative implementation in the target project over verbatim reuse.
