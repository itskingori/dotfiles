---
name: jira
description: Jira conventions and Atlassian CLI (acli) usage. Covers authentication, common ticket commands, and ADF formatting for descriptions. Use when viewing, creating, or editing Jira tickets or comments.
---

## Atlassian CLI (acli)

- Use the `acli` CLI tool for all Jira operations. The CLI should be authenticated; if not, ask me to authenticate.
- Voice: follow "Authorship Voice (Writing As Me)" and "Platform-Specific Defaults" in AGENTS.md for Jira descriptions and comments since you'll be authenticated as me.
- For Jira description edits, write ADF JSON to a temporary file (prefer `mktemp`), pass it with `--from-json`, and do not leave payload files in the repo.

No default project is configured, so the project key will need to be determined in conversation or specified per command.

## Common Commands

```bash
# View ticket details
acli jira workitem view <KEY>

# Edit ticket (simple fields)
acli jira workitem edit --key <KEY> --summary "New summary" --yes

# Edit ticket with description (ADF JSON; see adf-template.json for structure)
tmp_json="$(mktemp)"
cat <<'EOF' >"$tmp_json"
<... ADF JSON HERE ...>
EOF
acli jira workitem edit --from-json "$tmp_json" --yes
rm -f "$tmp_json"
```

## ADF Formatting (Critical)

Jira descriptions must use **Atlassian Document Format (ADF)**, not Markdown or wiki markup.

See [adf-template.json](adf-template.json) for a full example of the ADF JSON structure. Key points:

- Top-level object must have `"version": 1`, `"type": "doc"`, and a `"content"` array
- Each block element (heading, paragraph, bulletList, etc.) is a JSON object with a `"type"` field
- Text nodes use `{"type": "text", "text": "..."}` inside a `"content"` array
- Headings use `"attrs": {"level": 2}` (or 3, 4, etc.)
- List items must be wrapped in `listItem` nodes, each containing a `paragraph`
