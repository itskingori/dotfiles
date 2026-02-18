---
description: Document decisions into an ADR
agent: plan
subtask: false
---

You are running the `/docs-adr` command during a work session (at any point). Document key decisions from THIS CHAT SESSION + the repo evidence below into a proposed ADR.

Strict rules:
- Plan agent only: do not modify files, do not apply patches, do not run any git commands that change state.
- Your first response should ASK QUESTIONS first (to confirm/clarify), not immediately finalize the ADR.
- Use shell output + file references as evidence. Keep evidence excerpts short and relevant.
- Use `docs/adr/` as the ADR location. If `docs/adr/` is missing, ask whether to create it and stop.
- Never include secrets in ADR content (tokens, keys, cookies, credentials, private URLs). Use placeholder names or secret-manager references.

Repo ADR conventions:
- Existing ADRs (numbering + slug conventions):
!`test -d docs/adr && ls -1 docs/adr | sort || echo "docs/adr/ is missing"`

Generic ADR shape (follow this structure unless there is a strong reason not to):
```md
# ADR NNNN: <Title>

## Context

## Decision

## Consequences
```

Evidence snapshot (ground the ADR in what actually changed):
!`git rev-parse --is-inside-work-tree >/dev/null 2>&1 && git status -sb || echo "Not in a git worktree."`
!`git rev-parse --is-inside-work-tree >/dev/null 2>&1 && (git rev-parse --verify HEAD >/dev/null 2>&1 && git log --oneline -20 || echo "No commits yet.") || true`
!`git rev-parse --is-inside-work-tree >/dev/null 2>&1 && git diff --stat || true`
!`git rev-parse --is-inside-work-tree >/dev/null 2>&1 && git diff --name-only || true`
!`git rev-parse --is-inside-work-tree >/dev/null 2>&1 && git diff --cached --stat || true`
!`git rev-parse --is-inside-work-tree >/dev/null 2>&1 && git diff --cached --name-only || true`

Preflight:
- Confirm `docs/adr/` exists from repo evidence. If missing, ask one targeted question about creating it and stop.

Workflow:
1) Extract candidate decisions from the session. Do not drop decisions due to an arbitrary cap.
   - If there are many, group them by theme and keep the initial pass compact.
   - For each candidate, include:
     - One-sentence decision statement
     - Why it matters (1 sentence)
     - Evidence pointers only (relevant commit subject(s) and/or file paths); do not include code excerpts or large diffs.
     - ADR-worthy? yes/no (with a short reason)
2) Select the ADR theme to write now:
    - If multiple distinct themes exist, list them and ask the user to choose one theme to draft now; then stop and wait.
    - If you asked for theme selection, do not ask step 3 questions in the same response.
    - If there is only one clear theme, proceed without asking for theme selection.
    - Propose: Title, proposed new file path under `docs/adr/` using the next 4-digit number + kebab-case slug, and numbering basis (`0001` if no existing `docs/adr/NNNN-*.md` files).
3) Ask 4-8 targeted questions needed to write a correct ADR (only questions that materially affect the decision record).
   - Questions must cover: decision statement, status (proposed/accepted/superseded), scope, alternatives considered, rollout/testing impact, and ownership or follow-up.
4) Stop and wait for answers.

After the user answers, produce:
- Proposed file path in the form `docs/adr/NNNN-kebab-case-slug.md`
- A single fenced code block containing the final ADR, wrapped in clear markers:

  BEGIN ADR DRAFT
  <full ADR markdown>
  END ADR DRAFT

- If additional ADR themes remain, add exactly one final line: `Next: additional ADR themes were identified; run /docs-adr again to draft the next theme.`
- Keep the output minimal: no extra prose outside the required path line, ADR code block, and optional final line above.

To proceed with writing the file, switch to the build agent and ask it to write the ADR between the markers into the proposed path, then show `git status` and `git diff` (commit only if explicitly requested).
