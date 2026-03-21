---
name: jira
description: Jira conventions and Atlassian CLI (acli) usage. Covers authentication, common ticket commands, and ADF formatting for descriptions. Use when viewing, creating, or editing Jira tickets or comments.
---

## When To Use This Skill

Use this skill for Jira work where writing quality matters: issue descriptions, comments, and reviewer-facing updates.

## Core Rules

- Use `acli` for Jira operations.
- Follow "Authorship Voice (Writing As Me)" and "Platform-Specific Defaults" in `AGENTS.md`.
- No default project is configured in this repo, so determine or request the project key per task.
- Keep change sets focused: one logical change per work item update when practical.

## Jira Writing Conventions

- Keep descriptions and comments outcome-focused and actionable.
- Use comments for progress updates, risks, and decisions, not long-lived specifications.
- For rolling progress updates, prefer updating the latest status-style comment instead of posting a new comment for every increment.
- Use clear section headings when helpful (for example: Background, Scope, Risks, Follow-ups).

## Choosing The Input Mode

Use the least complex mode that preserves intent:

1. `--description` or `--body`
   - Best for short plain text.
2. `--description-file` or `--body-file`
   - Best for longer text and reusable payload files.
   - For rich descriptions, this is the default path for ADF documents.
3. `--from-json`
   - Advanced mode for full work item payloads and multi-field edits.

For rich comment formatting, use `comment update --body-adf` with an ADF JSON file.

## ADF Guidance

Jira rich text is ADF JSON. The top-level shape must be:

```json
{
  "version": 1,
  "type": "doc",
  "content": []
}
```

Use `examples/adf-description-structured.json` as the canonical ADF payload reference.

## Atlassian CLI (acli)

- Check auth and context with `acli jira auth status`.
- Prefer file-based input for multi-line content (`--description-file`, `--body-file`, `--body-adf`).
- Use quoted heredocs (`<<'EOF'`) when generating temporary files.
- Keep command recipes in examples files so this skill stays focused on writing quality.

## Example Files

Use these as copy-and-edit starting points:

- `examples/project-and-discovery.md`
- `examples/workitem-create-edit.md`
- `examples/comment-workflows.md`
- `examples/adf-description-structured.json`
- `examples/workitem-create.from-json.example.json`
- `examples/workitem-edit.from-json.example.json`

## Known Caveats

- `acli jira workitem view` uses a positional key, while most other commands use `--key`.
- `comment create` docs show inconsistent examples; use the explicit form: `acli jira workitem comment create ...`.
- If rich formatting from comment create is unreliable, create a plain comment first, then update it with `comment update --body-adf`.
