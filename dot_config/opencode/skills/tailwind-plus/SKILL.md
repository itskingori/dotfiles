---
name: tailwind-plus
description: Tailwind Plus UI blocks workflow. Uses a local licensed Tailwind Plus reference set to guide layout and implementation.
license: Proprietary
compatibility: opencode
---

## When To Use This Skill

Use this skill when Tailwind Plus UI blocks should drive page, section, and component implementation.

## Reference Root

Use this exact local reference root: /Users/Kingori/Repositories/itskingori/uix/reference/tailwind-plus

Treat this as a licensed local reference set. Keep exploration scoped to this path unless the task explicitly requires something else.

## Workflow

1. Identify the UI intent and constraints from the request.
2. Inspect local docs, manifests, and taxonomy files in the reference root first.
3. Prioritize `ui-blocks/` candidates that match the requested structure and interaction pattern.
4. Adapt the selected patterns to the target codebase and established visual language.
5. Call out setup-sensitive dependencies and implementation caveats.

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
