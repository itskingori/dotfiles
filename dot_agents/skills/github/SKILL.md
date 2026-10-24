---
name: github
description: GitHub conventions and gh CLI usage. Covers PR workflow, PR titles, PR descriptions, GitHub Markdown formatting, and gh CLI patterns including HEREDOC body formatting. Use when creating or editing PRs, issues, comments, or any GitHub interaction.
---

## When To Use This Skill

Use this skill for GitHub work where writing quality matters: PRs, issues, comments, and reviewer-facing updates.

## Core Rules

- Use the `gh` CLI for all GitHub operations.
- Follow "Authorship Voice (Writing As Me)" and "Platform-Specific Defaults" in the global instructions.
- Keep change sets focused: one logical change per PR when practical.

## Authoring Privacy Preflight

Before drafting or publishing repository-targeted GitHub content, determine the destination repository's visibility explicitly, for example with `gh repo view <owner/repo> --json visibility`. Do not infer visibility from the repository owner, organisation or URL.

For public repositories:

- Write content that stands on its own using public context. Prefer public evidence, generic technical descriptions and links public reviewers can access.
- Omit private repository or organisation names, inaccessible links, customer or incident details, internal rollout narratives and private operational background unless disclosure is genuinely necessary.
- The absence of secrets is not sufficient justification for publishing private context.
- Preserve useful technical reasoning by anonymising or generalising private observations instead of deleting the rationale.
- If private context appears necessary, stop before including it in a draft or publishing it. Discuss with the user exactly what would be disclosed, why it is needed and whether it can be generalised or minimised. Ordinary public facts do not require confirmation.

For private or internal repositories, relevant private context may be included when it is appropriate for the intended audience. Normal confidentiality and least-disclosure rules still apply.

## PR Workflow Conventions

- Create PRs in **draft mode** when work is in progress.
- Defer unrelated work to separate PRs even if convenient to do together; keep PRs focused on one logical change.
- For UI changes, include a screenshots checklist section by default.
- Call out anything that requires manual browser verification (JS-driven behaviours) and list concrete steps.
- Keep the PR body current as commits land.
- Only apply phase naming and reviewer-facing series structure when the current PR is part of that active series; do not infer it from mixed-author or unrelated repository history.
- When a PR follows or depends on another PR, include the relevant PR link(s) in `### Related`.
- If execution is restricted (for example plan/read-only mode), you may inspect and draft, but you must still follow this GitHub workflow first.

## PR Titles

- For PRs that are explicitly part of a multi-phase series, prefix PR titles with `Phase N: <description>`
- If the target org/team requires it, include the ticket reference: `[TICKET] Phase N: <description>`

## Links In Issue And PR Descriptions

- Keep descriptions focused on the work. Describe related work by name instead of scattering issue/PR numbers, URLs or Markdown links through prose, acceptance criteria and progress notes.
- Collect related GitHub issues, PRs and discussions in a single `### Related` section at the end of the description. Use a bulleted list of bare URLs, one per item, and deduplicate links.
- Put external documentation and other supporting sources in a separate `### References` section after `### Related`. This includes GitHub URLs that are not issues, PRs or discussions, such as releases and security advisories. Use a bulleted list of bare URLs and deduplicate links here too.
- Omit either section when it has no relevant links. Keep these link sections last, with `### Related` before `### References` when both exist.
- Preserve explicit closing keywords such as `Closes #4` when intentional. Use native GitHub relationships where supported; prose references are not a substitute for those relationships.
- Phase numbering does not require repeating the parent issue link throughout the description. Name the relevant phase or work in the prose and collect its link in `### Related`.
- Apply these rules when creating or updating descriptions, including routine progress updates. Check the complete updated description so edits do not reintroduce inline references or duplicate links.
- For cross-repo PR links, fetch the canonical URL with `gh pr view <number> --repo Org/repo --json url`.

## PR Descriptions

Voice: follow the "Authorship Voice (Writing As Me)" and "Platform-Specific Defaults" sections in the global instructions.

- Only required: start with a short, unheaded TL;DR paragraph (1-3 sentences). Do not start PR descriptions with a heading like `## Summary`.
- Use a hybrid voice: keep the opener content-focused and present-tense; use first-person for testing/validation lines.
- Avoid `##` headings (as they are too visually prominent on GitHub). Use `###` as the highest heading level, then `####` / `#####` as needed.
- Keep the PR description comprehensive and update it as new commits land (why/what/testing/manual steps/follow-ups).
- Describe the diff from base branch to current branch state. Avoid narrating exploratory implementation paths, removed intermediate problems, or transition details that are no longer present in the branch.
- All other sections are optional; choose headings based on the content/context of the change and omit empty sections.
- Use numbered lists when the count or sequence of items matters (e.g., migration steps). Link sections use bulleted lists as specified above.
- Prefer clear, functional section headings when needed; use the following conventions:
  - `### Background`: prior context that remains true regardless of this PR (history, existing behaviour, prior decisions).
  - `### Motivation`: why this change now (problem/pain, goal, success criteria, constraints).
  - `### Changes`: high-level deltas (avoid file-by-file); tradeoffs and migrations when relevant.
  - `### Scope`: what is included in this PR.
  - `### Non-goals`: what is explicitly out of scope.
  - `### Risk`: what could break and how risk is mitigated (include rollback notes when relevant).
  - `### Testing`: what I ran, what I verified manually and any known gaps.
  - `### Reviewing`: optional, brief and reviewer-oriented. Use it to suggest the most efficient review path, not to restate the change summary. Prefer one or two bullets.
  - `### Rollout`: flags, phases, steps and monitoring notes.
  - `### Follow-ups`: deferred work with concrete next actions.
  - `### Related`: related GitHub issues, PRs and discussions (dependencies, follow-ups and linked work). Bare URLs may render as rich cards here.
  - `### References`: external documentation and other supporting sources, including GitHub URLs that are not issues, PRs or discussions.
- Keep `### Related` and `### References` at the end, in that order, after all work-focused sections. Follow "Links In Issue And PR Descriptions" above for their bulleted bare URLs, deduplication and omission when empty.
- Put deferred implementation direction in `### Follow-ups`, not in `### Background` or `### Changes`, unless that direction is itself part of the approved design.

Examples (TL;DR opener styles):
- `Codifies my PR-writing conventions and adds global authorship voice guidance for external posts.`
- `Updates shared agent guidance to prefer unheaded TL;DR openers and ###-level section structure.`
- `Clarifies where to place GitHub-internal links vs external references in PR descriptions.`

## Issue And Comment Conventions

- Keep issue descriptions outcome-focused and actionable.
- Use comments for progress updates, risks and decisions, not long-lived specs.
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
