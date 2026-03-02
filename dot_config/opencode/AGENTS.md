# Global Instructions

## Tool Restrictions & Mode Compliance

- **Never circumvent tool restrictions.** If a tool is blocked or a mode (e.g., plan/read-only mode) restricts certain actions, do NOT use alternative tools (e.g., `sed`, `tee`, `echo`, `cat >`, or any Bash command) to achieve the same effect.
- Mode constraints are absolute. If you're in a read-only/plan mode, the only acceptable actions are reading, searching, and planning. No exceptions.
- If you cannot complete a requested action due to mode restrictions, explain the limitation and wait for the mode to change.

## Security & Privacy

- Do not request, paste, or persist secrets (tokens, API keys, cookies, credentials, private keys).
- If secrets appear in command output or logs, redact them in any written response.
- Do not create or propose committing credential-like files (e.g., `.env`, `credentials.json`) unless I explicitly request it and review is complete.

## Authorship Voice (Posting As Me)

When drafting or posting text in external systems as the user (e.g., GitHub PR bodies/issues/comments, Jira tickets/comments, etc.):

- Default to a content-focused, reviewer-oriented perspective: describe the change in present tense (e.g., "Adds ...", "Updates ...", "Clarifies ...") and avoid "I did ..." framing in the opener.
- Use first-person singular ("I", "my", "I'm") for actions, decisions, and accountability (especially testing/validation), for example "I ran ..." and "I verified ...".
- Avoid "we" unless I explicitly request it for that specific message.
- Do not address the user ("you") in that text; write to the reader/reviewer.
- Do not mention the assistant/AI or narrate the tooling (e.g., "as an AI...", "the agent...").
- Apply these voice rules to all external posts, including PR/issue bodies and comments.

## Dependency Management

- Prefer to use `mise`.
- Prefer deterministic installs e.g. use `npm ci` once `package-lock.json` exists.

## CI/Testing Workflow

- **Always run tests locally before pushing** to catch issues early.
- CI runs automatically on push to PRs; don't wait for CI to verify changes that can be tested locally.
- Use local commands (e.g., test runners, linters, formatters) for fast feedback loops.
- Only rely on CI for things that can't be tested locally (e.g., different OS, services not available locally).

## Git

### Git Hygiene (Non-Destructive, Reviewable History)

- Use one feature branch per change set; prefer small, reviewable PRs.
- Keep commits "one idea each"; split logical changes; avoid mega-commits. When work spans multiple ideas, commit incrementally (finish idea A and commit before starting idea B).
- Before pushing, it is OK to reorganize commits to improve history clarity when safe.
- If commits are already pushed, prefer a follow-up commit unless I explicitly request history rewrite.
- Rebasing rules:
  - OK to rebase before pushing.
  - If already pushed, only use `git push --force-with-lease` when you own the branch; confirm with me before doing it.
  - Do not rewrite shared/public history.

### Git Commit Messages (Context Over Mechanics)

- Keep commit messages free-form; optimize for clarity over strict formats.
- Use imperative, present-tense subjects (e.g., `Add`, `Fix`, `Update`, `Clarify`).
- Keep the subject concise (aim for ~50 chars when practical) and do not end it with a period.
- Where helpful, add a body with localized context about the change (intent/why/constraints/risk/validation), not a file-by-file changelog.
- If adding a body, leave a blank line after the subject and wrap lines at ~72 chars.
- Add context when it helps a future reader understand intent/tradeoffs/risk; not every commit needs a long body.
- When adding context, prefer "why/constraints/risk/validation" over a list of file changes.

Example (generic):

Subject:
`Add <outcome>`

Optional body (when useful):
- Why: <motivation/problem>
- Constraints/Risk: <tradeoffs, rollout notes, edge cases>
- Validation: <tests run + any manual verification>

### Git Branch Naming

- Use short, lowercase, hyphenated names; avoid spaces and punctuation.
- Name branches by area + outcome: `<area>-<short-slug>`.
- Single feature: `<area>-<short-slug>`
- Multi-phase work: `<area>-phase<N>-<short-slug>`

Examples (generic):
- `api-timeout-retry`
- `ui-settings-layout`
- `deps-bump-eslint`
- `dns-phase1-import-records`

## GitHub

### GitHub PR Workflow

- Create PRs in **draft mode** when work is in progress.
- Defer unrelated work to separate PRs even if convenient to do together; keep PRs focused on one logical change.
- For UI changes, include a screenshots checklist section by default.
- Call out anything that requires manual browser verification (JS-driven behaviours) and list concrete steps.

### GitHub PR Titles

- For multi-phase work, prefix PR titles with `Phase N: <description>`
- If the target org/team requires it, include the ticket reference: `[TICKET] Phase N: <description>`

### GitHub PR Descriptions

- Only required: start with a short, unheaded TL;DR paragraph (1-3 sentences). Do not start PR descriptions with a heading like `## Summary`.
- Use a hybrid voice: keep the opener content-focused and present-tense; use first-person for testing/validation lines.
- Avoid `##` headings (as they are too visually prominent on GitHub). Use `###` as the highest heading level, then `####` / `#####` as needed.
- Keep the PR description comprehensive and update it as new commits land (why/what/testing/manual steps/follow-ups).
- All other sections are optional; choose headings based on the content/context of the change and omit empty sections.
- Use numbered lists when the count of items matters (e.g., related PRs, migration steps)
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
  - `### Related`: directly related GitHub issues/PRs.
  - `### References`: external links used for research/reading/study.
- The `### Related` and `### References` MUST be lists (bulleted or numbered). Even a single link must be written as a one-item list (`- https://...` or `1. https://...`). Never put a bare URL on its own line under those headings.
- Use `### Related` for directly related GitHub issues/PRs (dependencies, follow-ups, or linked work).
- Use `### References` for external links used for research/reading/study.
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

### GitHub Markdown

- For any GitHub-rendered Markdown (PR descriptions, issue bodies, comments, READMEs/docs), use GitHub alert syntax for callouts instead of inline bold text. Avoid GitHub callouts outside GitHub (e.g., Jira uses ADF):
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

## CLI Integrations

### GitHub CLI (gh)

- Use the `gh` CLI for all GitHub operations (PRs, issues, repo info, etc.).
- The CLI should be authenticated; if access fails, ask user to authenticate via `gh auth login`.
- Voice: follow "Authorship Voice (Posting As Me)" for PR bodies and comments since you'll be authenticated as me.

#### PR and Issue Body Formatting

When using `gh pr create`, `gh pr edit`, or `gh issue create` with `--body`:

- **Use quoted HEREDOC** (`<<'EOF'`) to preserve backticks and prevent shell expansion:
  ```bash
  gh pr create --title "Title" --body "$(cat <<'EOF'
  <TL;DR paragraph (1-3 sentences) using authorship voice guidelines>
  EOF
  )"
  ```

- **Never use unquoted HEREDOC** (`<<EOF`) as it causes shell to escape backticks
- **Never use inline strings with escaped backticks** (e.g., `\`code\``) - they render incorrectly

### Atlassian CLI (acli)

- Use the `acli` CLI tool for all Jira operations. The CLI should be authenticated; if not, ask me to authenticate.
- Voice: follow "Authorship Voice (Posting As Me)" for Jira descriptions and comments since you'll be authenticated as me.

No default project is configured, so the project key will need to be determined in conversation or specified per command.

#### Common Commands

```bash
# View ticket details
acli jira workitem view <KEY>

# Edit ticket (simple fields)
acli jira workitem edit --key <KEY> --summary "New summary" --yes

# Edit ticket with description (use JSON for proper formatting)
acli jira workitem edit --from-json ticket.json --yes
```

#### ADF Formatting (Critical)

Jira descriptions must use **Atlassian Document Format (ADF)**, not Markdown or wiki markup.

Example ADF JSON structure for editing a ticket:

```json
{
  "issues": ["<KEY>"],
  "description": {
    "version": 1,
    "type": "doc",
    "content": [
      {
        "type": "heading",
        "attrs": {"level": 2},
        "content": [{"type": "text", "text": "Background"}]
      },
      {
        "type": "paragraph",
        "content": [{"type": "text", "text": "Description text here"}]
      },
      {
        "type": "bulletList",
        "content": [
          {"type": "listItem", "content": [{"type": "paragraph", "content": [{"type": "text", "text": "First item"}]}]},
          {"type": "listItem", "content": [{"type": "paragraph", "content": [{"type": "text", "text": "Second item"}]}]}
        ]
      }
    ]
  }
}
```

When editing descriptions, always write to a temporary JSON file and use `--from-json`.
