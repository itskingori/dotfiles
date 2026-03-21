# Comment workflows

Follow `../SKILL.md` for writing guidance; this file only shows command patterns.

## Add a plain comment

```bash
acli jira workitem comment create --key "TEAM-123" --body "Status update."
```

## List comments before updating

```bash
acli jira workitem comment list --key "TEAM-123" --json
```

## Update a comment with ADF via temporary file

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
          "text": "Status update."
        }
      ]
    }
  ]
}
EOF

acli jira workitem comment update --key "TEAM-123" --id "10001" --body-adf "$tmp_json"
rm -f "$tmp_json"
```

## Discover allowed visibility values

```bash
acli jira workitem comment visibility --group
acli jira workitem comment visibility --role --project "TEAM"
```
