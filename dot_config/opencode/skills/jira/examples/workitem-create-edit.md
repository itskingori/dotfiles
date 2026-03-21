# Work item create and edit workflows

Follow `../SKILL.md` for writing guidance; this file only shows command patterns.

## Create a work item

```bash
acli jira workitem create --project "TEAM" --type "Task" --summary "Title"
```

## Edit simple fields

```bash
acli jira workitem edit --key "TEAM-123" --summary "Updated title" --yes
```

## Edit description with canonical ADF payload

```bash
acli jira workitem edit --key "TEAM-123" --description-file "dot_config/opencode/skills/jira/examples/adf-description-structured.json" --yes
```

## Create from a full JSON payload

```bash
acli jira workitem create --from-json "dot_config/opencode/skills/jira/examples/workitem-create.from-json.example.json"
```

## Edit from a full JSON payload

```bash
acli jira workitem edit --from-json "dot_config/opencode/skills/jira/examples/workitem-edit.from-json.example.json" --yes
```

## Temporary file pattern for one-off ADF updates

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
          "text": "Body text."
        }
      ]
    }
  ]
}
EOF

acli jira workitem edit --key "TEAM-123" --description-file "$tmp_json" --yes
rm -f "$tmp_json"
```
