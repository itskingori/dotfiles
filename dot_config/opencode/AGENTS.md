# Global Instructions

## Tool Restrictions & Mode Compliance

- **Never circumvent tool restrictions.** If a tool is blocked or a mode (e.g., plan/read-only mode) restricts certain actions, do NOT use alternative tools (e.g., `sed`, `tee`, `echo`, `cat >`, or any Bash command) to achieve the same effect.
- Mode constraints are absolute. If you're in a read-only/plan mode, the only acceptable actions are reading, searching, and planning. No exceptions.
- If you cannot complete a requested action due to mode restrictions, explain the limitation and wait for the mode to change.

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

### Git Hygiene (Non-Destructive, Reviewable History)

- Use one feature branch per change set; prefer small, reviewable PRs.
- Keep commits "one idea each" (see "Git Commit Slicing" below). Avoid mega-commits; commit incrementally.
- Before pushing, it is OK to reorganize commits to improve history clarity when safe.
- If commits are already pushed, prefer a follow-up commit unless I explicitly request history rewrite.
- Rebasing rules:
  - OK to rebase before pushing.
  - If already pushed, only use `git push --force-with-lease` when you own the branch and I explicitly request it.
  - Do not rewrite shared/public history.

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

