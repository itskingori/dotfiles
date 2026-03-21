# Issue create and edit workflows

Follow `../SKILL.md` for writing guidance; this file only shows command patterns.

Use these patterns to create and update issues with `gh`.

## Create an issue

```bash
gh issue create \
  --title "Clarify GitHub skill workflow boundaries" \
  --body-file - <<'EOF'
Body text.
EOF
```

## Edit an existing issue

```bash
gh issue edit 123 \
  --title "Refine GitHub skill workflow boundaries" \
  --body-file - <<'EOF'
Body text.
EOF
```

## Use stdin for one-off issue content

```bash
gh issue edit 123 --body-file - <<'EOF'
Body text.
EOF
```
