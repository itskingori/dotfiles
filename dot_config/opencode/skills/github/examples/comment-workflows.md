# Comment workflows

Follow `../SKILL.md` for writing guidance; this file only shows command patterns.

Use comments for progress updates, risks and decisions.

Default style: for rolling status updates, prefer editing the last status-style comment instead of posting a new comment each time.

## Add a PR comment

```bash
gh pr comment 40 --body-file - <<'EOF'
Status update.
EOF
```

## Update the last PR status-style comment

```bash
gh pr comment 40 \
  --edit-last \
  --create-if-none \
  --body-file - <<'EOF'
Status update.
EOF
```

## Add an issue comment

```bash
gh issue comment 123 --body-file - <<'EOF'
Status update.
EOF
```

## Update the last issue status-style comment

```bash
gh issue comment 123 \
  --edit-last \
  --create-if-none \
  --body-file - <<'EOF'
Status update.
EOF
```

## When to post a new comment instead

- A new decision is made and should be preserved as a distinct entry
- A new discussion thread starts with different stakeholders
- A milestone update should remain separately visible in history
