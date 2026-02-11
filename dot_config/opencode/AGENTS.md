# Global Instructions

## Tool Restrictions & Mode Compliance

- **Never circumvent tool restrictions.** If a tool is blocked or a mode (e.g., plan/read-only mode) restricts certain actions, do NOT use alternative tools (e.g., `sed`, `tee`, `echo`, `cat >`, or any Bash command) to achieve the same effect.
- Mode constraints are absolute. If you're in a read-only/plan mode, the only acceptable actions are reading, searching, and planning. No exceptions.
- If you cannot complete a requested action due to mode restrictions, explain the limitation and wait for the mode to change.

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
- Keep commits "one idea each"; split logical changes; avoid mega-commits.
- Prefer fixing commit structure before review: if a fix belongs in an earlier commit, use interactive rebase/commit reordering when safe.
- Rebasing rules:
  - OK to rebase before pushing.
  - If already pushed, only use `git push --force-with-lease` when you own the branch; confirm with me before doing it.
  - Do not rewrite shared/public history.

### Git Commit Messages (Context Over Mechanics)

- Keep commit messages free-form; optimize for clarity over strict formats.
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
- Call out anything that requires manual browser verification (JS-driven behaviors) and list concrete steps.

### GitHub PR Titles

- For multi-phase work, prefix PR titles with `Phase N: <description>`
- In the Intellection GitHub org, also include the Jira ticket reference: `[TICKET] Phase N: <description>`

### GitHub PR Descriptions

- Keep the PR description comprehensive and update it as new commits land (why/what/testing/manual steps/follow-ups).
- Use numbered lists when the count of items matters (e.g., related PRs, migration steps)
- For cross-repo references:
  - Use `gh pr view <number> --repo Org/repo --json url` to fetch PR URLs programmatically
  - Group related PRs in descriptions by status (e.g., merged, pending, cleanup)
  - Use bare GitHub URLs (not markdown links) -- GitHub auto-generates rich link cards

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

#### PR and Issue Body Formatting

When using `gh pr create`, `gh pr edit`, or `gh issue create` with `--body`:

- **Use quoted HEREDOC** (`<<'EOF'`) to preserve backticks and prevent shell expansion:
  ```bash
  gh pr create --title "Title" --body "$(cat <<'EOF'
  ## Summary
  Description with `backticks` preserved correctly.
  EOF
  )"
  ```

- **Never use unquoted HEREDOC** (`<<EOF`) as it causes shell to escape backticks
- **Never use inline strings with escaped backticks** (e.g., `\`code\``) - they render incorrectly

### Atlassian CLI (acli)

Use the `acli` CLI tool for all Jira operations. The CLI should be authenticated; if not, ask me to authenticate.

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
