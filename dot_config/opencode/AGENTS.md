# Global Instructions

## Tool Restrictions & Mode Compliance

- **Never circumvent tool restrictions.** If a tool is blocked or a mode (e.g., plan/read-only mode) restricts certain actions, do NOT use alternative tools (e.g., `sed`, `tee`, `echo`, `cat >`, or any Bash command) to achieve the same effect.
- Mode constraints are absolute. If you're in a read-only/plan mode, the only acceptable actions are reading, searching, and planning. No exceptions.
- If you cannot complete a requested action due to mode restrictions, explain the limitation and wait for the mode to change.

## Requirement Shifts & Plan Re-evaluation

- Treat any new instruction source or domain-specific context as a requirements shift. This includes loading a skill, resuming a skill-backed task, receiving new user constraints, or finding repo-local guidance that changes how the task should be done.
- When a requirements shift happens, re-evaluate the current plan and next action before proceeding. Do not assume an earlier plan still applies.
- If the new instructions change the task domain, output format, or execution constraints, update the plan to match active instructions before taking the next domain action.

### GitHub Tasks

- Treat any request involving GitHub as a mandatory domain shift. This includes pull requests, draft PRs, PR titles/bodies, review comments, issues, checks, release notes, `gh` usage, and GitHub URLs.
- Before doing any GitHub-related planning or writing, you **must**:
  1. Re-evaluate active instructions and output-format requirements.
  2. Ensure the `github` skill is active.
  3. Identify and restate:
     - current branch
     - intended base branch
     - whether the work is stacked on another branch/PR
     - local commit scope relative to the proposed base
     - expected title/body structure source, using this order:
       1. active stacked series PRs
       2. explicit written instructions in this repo/active skills
       3. recent same-author PRs in this repository (only when clearly consistent)
       4. generic skill defaults
- Do not draft or propose a PR title/body, issue body, review comment, or GitHub comment until those checks are complete.

## Security & Privacy

- Do not request, paste, or persist secrets (tokens, API keys, cookies, credentials, private keys).
- If secrets appear in command output or logs, redact them in any written response.
- Do not commit or persist credential-like files (e.g., `.env`, `credentials.json`). If I explicitly request this, treat it as high-risk: require explicit confirmation that the content is non-secret and safe for version control, and prefer a secret manager.

## Authorship Voice (Writing As Me)

Use these rules whenever writing in my voice, unless a later section narrows them for a specific platform or format.

### General Voice

- Write clearly, directly, and with intent.
- Prefer a content-focused perspective by default; lead with what changed, what matters, or what the reader should understand.
- Use first-person singular ("I", "my", "I'm") for actions, decisions, opinions, and accountability where it improves clarity.
- Use British English spelling and punctuation consistently (e.g., "organise", "behaviour", "licence", "centre").
- Prefer plain punctuation over typographic flourish: avoid em dashes; use commas, parentheses, or full stops instead.
- Keep punctuation restrained: do not overuse exclamation marks, ellipses, or scare quotes unless they are genuinely needed.
- Avoid filler, hype, and fake enthusiasm.
- Do not mention the assistant/AI or narrate the tooling.

### Platform-Specific Defaults

For GitHub PR bodies, issue bodies, comments, Jira tickets/comments, and similar review-oriented contexts:

- Default to a content-focused, reviewer-oriented perspective.
- Describe changes in present tense where that reads naturally (e.g., "Adds ...", "Updates ...", "Clarifies ...").
- Avoid "I did ..." framing in the opener.
- Avoid "we" unless I explicitly request it.
- Do not address the reader as "you" unless the format or context genuinely requires it.

## Dependency Management

- Prefer to use `mise`.
- Prefer deterministic installs e.g. use `npm ci` once `package-lock.json` exists.

## CI/Testing Workflow

- **Always run tests locally before pushing** to catch issues early.
- CI runs automatically on push to PRs; don't wait for CI to verify changes that can be tested locally.
- Use local commands (e.g., test runners, linters, formatters) for fast feedback loops.
- Only rely on CI for things that can't be tested locally (e.g., different OS, services not available locally).

## Language Guidance

### Elixir

#### Test organisation

- Prefer test files and directories that mirror the source structure when that improves clarity and reviewability.
- For example, if app code lives in `lib/my_app/accounts/user_sync.ex`, prefer `test/my_app/accounts/user_sync_test.exs`.
- For web code, if app code lives in `lib/my_app_web/live/admin/user_live.ex`, prefer `test/my_app_web/live/admin/user_live_test.exs`.
- Apply the same principle to contexts, schemas, services, controllers, components, and LiveViews when the mapping is useful.
- Do not force a 1:1 test file for tiny or tightly related modules where a shared test file is clearer.
- Avoid large catch-all test files that cover multiple unrelated modules or pages when the tests would be easier to understand split by source area.
- When multiple test files in one area need the same setup data or helpers, extract shared fixtures/support into `test/support/` rather than repeating large helper blocks.
- Keep shared support focused on setup and fixtures; keep assertions and scenario intent in the most specific test file.
- If it is not clear whether tests should be split or combined, ask before choosing a structure.

## Git

### Git Workflow & Hygiene (Non-Destructive, Reviewable History)

- Use one feature branch per change set; prefer small, reviewable PRs.
- Keep commits "one idea each" (see "Git Commit Slicing" below). Avoid mega-commits; commit incrementally.
- When writing commit messages, PR bodies, or documentation for a change, describe the code as it exists in the reviewed state.
- Do not reference discarded exploratory paths, removed intermediate implementations, or transition details unless they remain visible in the final history or are explicitly captured as follow-up context.
- Before pushing, it is OK to reorganize commits to improve history clarity when safe.
- If commits are already pushed, prefer a follow-up commit unless I explicitly request history rewrite.
- Rebasing rules:
  - OK to rebase before pushing.
  - If already pushed, only use `git push --force-with-lease` when you own the branch and I explicitly request it.
  - Do not rewrite shared/public history.
- Keep backup/safety branches local by default unless I explicitly ask to publish them.
- Prefix local backup branches with `backup/` so they are clearly distinct from active working branches.

### Non-Interactive Git Commands

- Assume Git commands may run without an interactive terminal.
- Never run editor-opening Git commands without suppressing the editor first.
- For rebase continuation, use `GIT_EDITOR=true git rebase --continue` unless I explicitly ask to edit the commit message.
- Apply the same pattern to other Git flows that may open an editor in automation or tool-driven sessions.
- When chaining commands, do not place follow-up commands after `git rebase --continue` unless the rebase has completed successfully.

### Git Commit Slicing (One Idea Per Commit)

- Having "one idea" means one primary axis of change, not "one PR worth of work".
- Default axes (split into separate commits when practical):
  - Behaviour/runtime changes (what the system does)
  - Interfaces/contracts (APIs, config schemas, env vars, CLI flags)
  - Tooling/operability (scripts, Makefiles, workflows)
  - Documentation (READMEs, runbooks, notes)
  - Refactors/renames (no behaviour change)
  - Formatting/linting (mechanical-only changes)
  - Tests (test-only changes)
- Rules of thumb:
  - If reviewers could approve one part but reasonably request changes on another, split them.
  - Do not mix behaviour changes with refactors/formatting; split them.
  - Do not bundle docs-only updates into a behaviour change commit; add a docs commit.
  - If multiple independent components are touched, prefer one commit per component.
  - When changing behaviour, include the corresponding test additions/updates in the same commit (keep each commit green and self-contained).
  - Exception: if the change is genuinely trivial and confined (single small diff), a single commit is fine.

### Git Commit Messages (Context Over Mechanics)

- Keep commit messages free-form; optimize for clarity over strict formats.
- Use imperative, present-tense subjects (e.g., `Add`, `Fix`, `Update`, `Clarify`).
- Keep the subject concise (aim for ~50 chars when practical) and do not end it with a period.
- Default to a subject plus body for any non-trivial commit; use a subject-only message only for tiny, obvious, mechanical changes.
- Leave a blank line after the subject and wrap every body line at ~72 chars.
- In the body, describe the final reviewed state and prefer why/constraints/risk/validation over a file-by-file changelog.
- When creating commits non-interactively, use an input method that preserves real newlines; never include literal `\n` escape sequences in the final commit message.
- Keep body content concise; 1-3 short paragraphs or bullets is usually enough.

Example (generic):

Subject:
`Add <outcome>`

Body (default for non-trivial changes):
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
