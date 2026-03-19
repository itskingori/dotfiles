---
name: jira
description: Jira conventions and Atlassian CLI (acli) usage. Covers authentication, common ticket commands, and ADF formatting for descriptions. Use when viewing, creating, or editing Jira tickets or comments.
---

## When To Use This Skill

Use this skill for Jira Cloud work via Atlassian CLI (`acli`), including:

- discovering project keys and work item keys
- viewing, searching, creating, and editing work items
- creating, listing, and updating comments
- writing rich text payloads using Atlassian Document Format (ADF)

## Core Rules

- Use `acli` for all Jira operations.
- Follow "Authorship Voice (Writing As Me)" and "Platform-Specific Defaults" in `AGENTS.md` for Jira descriptions and comments.
- No default project is configured in this repo. Determine or request the project key per task.
- Prefer deterministic, non-interactive commands in this order:
  1. explicit flags
  2. file-based input
  3. editor mode (`--editor`) only when requested

## Authentication And Context

Start here when Jira access may be stale or account context is unclear:

```bash
# Check Jira auth state
acli jira auth status

# Authenticate to Jira Cloud when needed
acli jira auth login --web

# Switch account/site if multiple profiles exist
acli jira auth switch --site "<site>.atlassian.net" --email "<email>"
```

Project discovery:

```bash
# List visible projects
acli jira project list --limit 50 --json

# Inspect one project
acli jira project view --key "TEAM" --json
```

## Choosing The Input Mode

Use the least complex mode that preserves intent:

1. `--description` or `--body`
   - Best for short plain text.
2. `--description-file` or `--body-file`
   - Best for longer text and reusable payload files.
   - For descriptions, this is the default path for ADF documents.
3. `--from-json`
   - Advanced mode for full work item payloads and batch-like edits.
   - Use when multiple fields must be updated atomically.

For comments with rich formatting, the most reliable explicit ADF path is `comment update --body-adf`.

## Common Command Patterns

Work item discovery:

```bash
# Search by JQL
acli jira workitem search --jql "project = TEAM AND statusCategory != Done" --limit 50 --json

# View one work item (note: key is positional here)
acli jira workitem view TEAM-123 --fields key,summary,status,assignee,description --json
```

Work item create/edit:

```bash
# Create a work item (simple path)
acli jira workitem create --project "TEAM" --type "Task" --summary "Add CLI playbook examples"

# Edit simple fields
acli jira workitem edit --key "TEAM-123" --summary "Refine Jira playbook guidance" --yes

# Edit description from an ADF file
acli jira workitem edit --key "TEAM-123" --description-file "dot_config/opencode/skills/jira/examples/adf-description-structured.json" --yes
```

Comments:

```bash
# Create a simple comment
acli jira workitem comment create --key "TEAM-123" --body "Started implementation and validated command coverage."

# List comments to find IDs before updating
acli jira workitem comment list --key "TEAM-123" --json

# Update a specific comment with ADF JSON
acli jira workitem comment update --key "TEAM-123" --id "10001" --body-adf "dot_config/opencode/skills/jira/examples/adf-comment-minimal.json"

# Discover allowed comment visibility values
acli jira workitem comment visibility --group
acli jira workitem comment visibility --role --project "TEAM"
```

## ADF Guidance

Jira rich text is ADF JSON. The top-level shape must be:

```json
{
  "version": 1,
  "type": "doc",
  "content": []
}
```

Start from these example payloads:

- `examples/adf-description-minimal.json`
- `examples/adf-description-structured.json`
- `examples/adf-description-with-code-block.json`
- `examples/adf-description-with-links-and-lists.json`
- `examples/adf-comment-minimal.json`

Advanced examples:

- `examples/workitem-create.from-json.example.json`
- `examples/workitem-edit.from-json.example.json`

## Safe Temp-File Pattern

When creating one-off payloads, keep files out of the repo:

```bash
tmp_json="$(mktemp)"
cat <<'EOF' >"$tmp_json"
{
  "version": 1,
  "type": "doc",
  "content": [
    {
      "type": "paragraph",
      "content": [
        {
          "type": "text",
          "text": "Status update"
        }
      ]
    }
  ]
}
EOF

acli jira workitem edit --key "TEAM-123" --description-file "$tmp_json" --yes
rm -f "$tmp_json"
```

## Known Caveats

- `acli jira workitem view` uses a positional key, while most other commands use `--key`.
- `comment create` docs show inconsistent examples; use the explicit form: `acli jira workitem comment create ...`.
- ADF support can vary by command path. If `comment create` formatting is unreliable, create a plain comment first, then apply rich formatting via `comment update --body-adf`.
