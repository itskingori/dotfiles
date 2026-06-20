---
name: handoff
description: Write a portable handoff prompt for Claude, Codex, opencode or another agent. Use when asked for a handoff, continuation prompt, delegation prompt, or prompt to resume work elsewhere.
---

# Handoff

Write a standalone prompt that lets another agent investigate, discuss, or pick up a specific task from a fresh context.

Use this skill when the user asks for `handoff <task>`, "write a handoff", "handoff to Claude", "handoff to Codex", "delegate this", "continue this in another agent", or wants a prompt for another model or session.

## Core Rule

The handoff is starting context, not a verdict. The receiving agent must own its review, re-check live state and decide whether the task is still valid, already solved, stale, over-scoped or better handled differently.

## Workflow

1. Identify the task from the user's request. If the request is brief, infer the task from current repo context, recent discussion, branch names, linked issues/PRs, docs and obvious nearby context.
2. Gather enough context to orient the receiving agent: repo/product identity, relevant branch/issue/PR names, likely modules, known symptoms, constraints, non-goals and validation expectations.
3. Do not perform the receiving agent's full independent review. Include only enough checked context to make the handoff useful.
4. Write a clipboard-ready prompt for a fresh agent.
5. Copy the prompt to the clipboard when the current environment and tool mode allow it. If clipboard access is unavailable, print the prompt and say so.
6. Final reply: confirm briefly with the task title. Do not paste the full prompt unless the user asks.

## Handoff Prompt Rules

The prompt must:

- Start a discussion, not a command-only work order.
- Ask the receiving agent to do an independent review before changing anything.
- Make clear that the receiving agent owns the review and decision.
- Ask the receiving agent to decide whether the task is a good idea, stale, already solved, over-scoped or better handled differently.
- Avoid filesystem paths unless the user explicitly asks for them.
- Avoid secrets, credential material, private workspace state, logs, caches, history files and machine-specific assumptions.
- Use portable anchors instead: repo owner/name, product or module names, issue/PR URLs, branch names, package names, public symbols, command names, config keys, exact error text, docs titles and search terms.
- Include enough context for the receiving agent to find the right repo, scope the work and understand the desired outcome.
- Include constraints, non-goals, validation expectations and the desired output shape.
- Tell the receiving agent to read local agent/repo instructions before acting.
- Tell the receiving agent to re-check live repo, GitHub, Linear, CI or docs state where relevant.
- Tell the receiving agent not to push, merge, close issues/PRs, label, apply destructive git commands or post public comments unless explicitly asked.

## Prompt Template

Use this shape by default:

```text
I want to discuss and possibly work on: <short task title>

Context:
- <portable repo/product context>
- <what triggered this task>
- <known current state, branch/issue/PR names or URLs if relevant>
- <important constraints and ownership boundaries>

Before doing any implementation:
- Find the right repository from the current directory, a parent directory, or the usual workspace.
- Read the local agent/repo instructions.
- Inspect the relevant code, docs, tests, recent commits and linked issue/PR state.
- Decide whether this task is still real, whether the proposed direction is a good idea and whether a smaller or better fix exists.
- Call out stale assumptions, hidden risks and anything that should stop the work.

Task:
- <what to investigate or implement if the review supports it>
- <expected behaviour or decision criteria>
- <non-goals>

Validation:
- <focused tests/checks/live proof expected>
- <what evidence should be included>
- <what is explicitly not required>

Output:
- Start with your review findings and recommendation.
- Then give the proposed plan or patch summary.
- If you edit code, keep changes scoped and report exact proof run.
- Do not push, merge, close issues/PRs, label, apply destructive git commands or post public comments unless explicitly told.
```

## Clipboard

On macOS, write the prompt to a temporary file and copy it with:

```sh
pbcopy < /tmp/handoff-prompt.txt
```

Avoid inline shell quoting for prompts containing backticks, `$`, quotes or user text. If `pbcopy` is unavailable, use the obvious platform clipboard tool (`wl-copy`, `xclip`, `clip.exe`) or print the prompt and say clipboard copy was unavailable.

## Quality Bar

- No invented facts. Mark facts as reviewed only after checking them.
- No path leakage. Rewrite accidental paths as repo names, modules, symbols, command names, issue/PR URLs, search terms or exact error text.
- No secret-ish material. Redact or omit anything that could expose credentials or private machine state.
- Enough context for a fresh agent to orient; no giant brain dump.
- First substantial instruction to the receiving agent: review, discuss and assess.
