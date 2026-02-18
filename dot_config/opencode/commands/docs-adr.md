---
description: Compress decisions into an ADR
agent: plan
subtask: false
---

You are running during a work session (at any point). Compress key decisions from THIS CHAT SESSION + the repo evidence below into a proposed ADR.

Strict rules:
- Plan agent only: do not modify files, do not apply patches, do not run any git commands that change state.
- Your first response should ASK QUESTIONS first (to confirm/clarify), not immediately finalize the ADR.
- Use shell output + file references as evidence. Keep evidence excerpts short and relevant.

Repo ADR conventions:
- Existing ADRs (numbering + slug conventions):
!`ls -1 docs/adr | sort`

Generic ADR shape (follow this structure unless there is a strong reason not to):
```md
# ADR NNNN: <Title>

## Context

## Decision

## Consequences
```

Evidence snapshot (ground the ADR in what actually changed):
!`git status -sb`
!`git log --oneline -20`
!`git diff --stat`
!`git diff --name-only`

Workflow:
1) Extract candidate decisions from the session. Do not drop decisions due to an arbitrary cap.
   - If there are many, group them by theme and keep the initial pass compact.
   - For each candidate, include:
     - One-sentence decision statement
     - Why it matters (1 sentence)
     - Evidence pointers only (relevant commit subject(s) and/or file paths); do not include code excerpts or large diffs.
     - ADR-worthy? yes/no (with a short reason)
2) Pick the single best ADR to write now and propose:
   - Title
   - Proposed new file path under `docs/adr/` using the next 4-digit number + kebab-case slug
3) Ask 4-8 targeted questions needed to write a correct ADR (only questions that materially affect the decision record).
4) Stop and wait for answers.

After the user answers, produce:
- Proposed file path
- A single fenced code block containing the final ADR, wrapped in clear markers:

  BEGIN ADR DRAFT
  <full ADR markdown>
  END ADR DRAFT

To proceed with writing the file, switch to the build agent and ask it to write the ADR between the markers into the proposed path, then show `git status` and `git diff` (commit only if explicitly requested).
