---
name: github
description: GitHub conventions and gh CLI usage. Covers PR workflow, PR titles, PR descriptions, GitHub Markdown formatting, and gh CLI patterns including HEREDOC body formatting. Use when creating or editing PRs, issues, comments, or any GitHub interaction.
---

## When To Use This Skill

Use this skill for GitHub work where writing quality matters: PRs, issues, comments, and reviewer-facing updates.

## Core Rules

- Use the `gh` CLI for all GitHub operations.
- Follow "Authorship Voice (Writing As Me)" and "Platform-Specific Defaults" in `AGENTS.md`.
- Keep change sets focused: one logical change per PR when practical.

## PR Workflow Conventions

- Create PRs in **draft mode** when work is in progress.
- Defer unrelated work to separate PRs even if convenient to do together; keep PRs focused on one logical change.
- For UI changes, include a screenshots checklist section by default.
- Call out anything that requires manual browser verification (JS-driven behaviours) and list concrete steps.
- Keep the PR body current as commits land.
- Do not use a generic fallback PR structure when repository history or an active stacked PR establishes a stronger pattern.
- When a PR follows an existing PR in a series, mirror established phase naming, include relevant links, and preserve the repository's reviewer-facing section structure.
- If execution is restricted (for example plan/read-only mode), you may inspect and draft, but you must still follow this GitHub workflow first.

## PR Titles

- For multi-phase work, prefix PR titles with `Phase N: <description>`
- If the target org/team requires it, include the ticket reference: `[TICKET] Phase N: <description>`

## PR Descriptions

Voice: follow the "Authorship Voice (Writing As Me)" and "Platform-Specific Defaults" sections in AGENTS.md.

- Only required: start with a short, unheaded TL;DR paragraph (1-3 sentences). Do not start PR descriptions with a heading like `## Summary`.
- Use a hybrid voice: keep the opener content-focused and present-tense; use first-person for testing/validation lines.
- Avoid `##` headings (as they are too visually prominent on GitHub). Use `###` as the highest heading level, then `####` / `#####` as needed.
- Keep the PR description comprehensive and update it as new commits land (why/what/testing/manual steps/follow-ups).
- All other sections are optional; choose headings based on the content/context of the change and omit empty sections.
- Use numbered lists when the count of items matters (e.g., related PRs, migration steps).
- Prefer clear, functional section headings when needed; use the following conventions:
  - `### Background`: prior context that remains true regardless of this PR (history, existing behaviour, prior decisions).
  - `### Motivation`: why this change now (problem/pain, goal, success criteria, constraints).
  - `### Changes`: high-level deltas (avoid file-by-file); tradeoffs and migrations when relevant.
  - `### Scope`: what is included in this PR.
  - `### Non-goals`: what is explicitly out of scope.
  - `### Risk`: what could break and how risk is mitigated (include rollback notes when relevant).
  - `### Testing`: what I ran, what I verified manually, and any known gaps.
  - `### Rollout`: flags, phases, steps, and monitoring notes.
  - `### Follow-ups`: deferred work with concrete next actions.
  - `### Related`: GitHub issues/PRs/discussions only (renders as rich cards on GitHub; excludes releases and security advisories; dependencies/follow-ups/linked work).
  - `### References`: all other links (external trackers/findings/docs/research, plus GitHub URLs that are not issues/PRs/discussions), even when directly motivating.
- The `### Related` and `### References` MUST be lists (bulleted or numbered). Even a single link must be written as a one-item list (`- https://...` or `1. https://...`). Never put a bare URL on its own line under those headings.
- Include `### Related` and `### References` only when relevant links exist.
- If both sections are present, keep this order: `### Related` then `### References`.
- For cross-repo references:
  - Use `gh pr view <number> --repo Org/repo --json url` to fetch PR URLs programmatically
  - Group related PRs in descriptions by status (e.g., merged, pending, cleanup)
  - Use bare GitHub URLs (not markdown links) -- GitHub auto-generates rich link cards

Examples (TL;DR opener styles):
- `Codifies my PR-writing conventions and adds global authorship voice guidance for external posts.`
- `Updates global opencode guidance to prefer unheaded TL;DR openers and ###-level section structure.`
- `Clarifies where to place GitHub-internal links vs external references in PR descriptions.`

## Issue And Comment Conventions

- Keep issue descriptions outcome-focused and actionable.
- Use comments for progress updates, risks, and decisions, not long-lived specs.
- Prefer editing the last status-style comment when updating rolling progress, rather than creating a new comment for each increment.
- For cross-repo references, use bare GitHub URLs so cards render automatically.

## GitHub Markdown Guidance

For any GitHub-rendered Markdown (PR descriptions, issue bodies, comments, READMEs/docs), use GitHub alert syntax for callouts instead of inline bold text:

```markdown
> [!NOTE]
> Highlights information that users should take into account, even when skimming.

> [!TIP]
> Optional information to help a user be more successful.

> [!IMPORTANT]
> Crucial information necessary for users to succeed.

> [!WARNING]
> Critical content demanding immediate user attention due to potential risks.

> [!CAUTION]
> Negative potential consequences of an action.
```

## GitHub CLI (gh)

- Prefer `--body-file` for multi-line Markdown. Use `--body-file -` for generated content.
- For heredocs, always use quoted delimiters (`<<'EOF'`) to prevent shell expansion.
- Prefer deterministic non-interactive input: explicit flags, then `--body-file`, then `--editor` only when requested.

## Example Files

Use these as copy-and-edit starting points:

- `examples/pr-create-edit.md`
- `examples/issue-create-edit.md`
- `examples/comment-workflows.md`
- `examples/review-workflows.md`
