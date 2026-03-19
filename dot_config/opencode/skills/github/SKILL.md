---
name: github
description: GitHub conventions and gh CLI usage. Covers PR workflow, PR titles, PR descriptions, GitHub Markdown formatting, and gh CLI patterns including HEREDOC body formatting. Use when creating or editing PRs, issues, comments, or any GitHub interaction.
---

## When To Use This Skill

Use this skill for all GitHub work via `gh`, including:

- creating and editing pull requests
- creating and editing issues
- writing and updating PR and issue comments
- reviewing PR status, checks, commits, files, and comments
- handling cross-repo references and links in GitHub-rendered Markdown

## Core Rules

- Use the `gh` CLI for all GitHub operations.
- Follow "Authorship Voice (Writing As Me)" and "Platform-Specific Defaults" in `AGENTS.md`.
- Keep change sets focused: one logical change per PR when possible.
- Prefer deterministic, non-interactive workflows:
  1. explicit flags
  2. `--body-file`
  3. `--editor` or `--web` only when requested

## Authentication And Repository Context

Start by confirming access and repo scope:

```bash
# Check gh installation and auth
gh --version
gh auth status

# Check repository context
gh repo view --json nameWithOwner,defaultBranchRef,url
```

If auth fails, authenticate with `gh auth login`.

## Choosing Body Input Mode

Use the least complex mode that preserves formatting:

1. `--body`
   - Good for short, single-line text.
2. `--body-file <path>`
   - Preferred for multi-line content.
   - Use `--body-file -` to read from stdin for generated content.
3. quoted HEREDOC into `--body` or `--body-file -`
   - Preferred for scripted multi-line Markdown with backticks and code fences.

Safe pattern:

```bash
gh pr create --title "Title" --body-file - <<'EOF'
TL;DR sentence.

### Testing
- I ran local checks.
EOF
```

Do not use unquoted HEREDOCs (`<<EOF`) for Markdown bodies.

## Common Command Patterns

### Pull Requests

```bash
# Create PR with explicit title/body
gh pr create --title "Add workflow-first GitHub skill" --body-file "dot_config/opencode/skills/github/examples/pr-body-structured.md"

# Create draft PR while work is in progress
gh pr create --draft --title "Add workflow-first GitHub skill" --body-file "dot_config/opencode/skills/github/examples/pr-body-structured.md"

# Update existing PR body/title
gh pr edit 39 --title "Refine GitHub skill playbook" --body-file "dot_config/opencode/skills/github/examples/pr-body-structured.md"

# Review PR details and status
gh pr view 39 --json title,body,state,isDraft,baseRefName,headRefName,url
gh pr checks 39
gh pr diff 39
gh pr view 39 --comments
```

### Issues

```bash
# Create issue with markdown body
gh issue create --title "Document GitHub workflows in skill playbook" --body-file "dot_config/opencode/skills/github/examples/issue-body-structured.md"

# View issue details
gh issue view 123 --json title,body,state,labels,assignees,url

# Edit issue content
gh issue edit 123 --title "Clarify GitHub skill workflow coverage" --body-file "dot_config/opencode/skills/github/examples/issue-body-structured.md"
```

### Comments

```bash
# Add PR comment
gh pr comment 39 --body-file "dot_config/opencode/skills/github/examples/pr-comment-minimal.md"

# Edit last PR comment, create one if none exists
gh pr comment 39 --edit-last --create-if-none --body-file "dot_config/opencode/skills/github/examples/pr-comment-minimal.md"

# Add issue comment
gh issue comment 123 --body-file "dot_config/opencode/skills/github/examples/issue-comment-minimal.md"

# Edit last issue comment, create one if none exists
gh issue comment 123 --edit-last --create-if-none --body-file "dot_config/opencode/skills/github/examples/issue-comment-minimal.md"
```

## PR Workflow Conventions

- Create PRs in draft mode when work is incomplete.
- Split unrelated work into separate PRs.
- For UI changes, include screenshots and manual verification steps.
- Keep the PR body current as commits land.

### PR Titles

- For multi-phase work, use `Phase N: <description>`.
- If the team requires ticket references, use `[TICKET] Phase N: <description>`.

### PR Descriptions

- Start with a short, unheaded TL;DR paragraph (1-3 sentences).
- Use `###` as the highest heading level, then `####` or `#####` as needed.
- Use section headings only when useful; omit empty sections.
- For links:
  - `### Related` for GitHub issues, PRs, or discussions
  - `### References` for external links and non-issue/PR/discussion GitHub URLs
- `### Related` and `### References` must be lists, even for one link.
- If both are present, keep order: `### Related`, then `### References`.

Example opener styles:

- `Codifies my PR-writing conventions and adds global authorship voice guidance for external posts.`
- `Updates global opencode guidance to prefer unheaded TL;DR openers and ###-level section structure.`
- `Clarifies where to place GitHub-internal links vs external references in PR descriptions.`

## Issue And Comment Conventions

- Keep issue descriptions outcome-focused and actionable.
- Use comments for progress updates, risks, and decisions, not long-lived specs.
- Prefer editing the last bot-authored status comment when updating rolling progress.
- For cross-repo references, use bare GitHub URLs so cards render automatically.

## GitHub Markdown Guidance

For GitHub-rendered Markdown (PRs, issues, comments, README/docs), use GitHub alert syntax for callouts instead of inline bold labels.

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

Do not use GitHub callout syntax outside GitHub-rendered Markdown contexts (for example, Jira uses ADF).

## Example Files

Use these as copy-and-edit starting points:

- `examples/pr-body-minimal.md`
- `examples/pr-body-structured.md`
- `examples/issue-body-minimal.md`
- `examples/issue-body-structured.md`
- `examples/pr-comment-minimal.md`
- `examples/issue-comment-minimal.md`

## Known Caveats

- `gh pr create --dry-run` can still push branch changes in some flows, so do not assume it is side-effect free.
- `gh pr create` may prompt for push/fork when branch tracking is missing; provide `--head` when you need deterministic behaviour.
- For complex Markdown bodies, `--body-file` is more reliable than heavily escaped inline `--body` strings.
